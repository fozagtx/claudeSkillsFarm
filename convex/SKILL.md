---
name: convex
description: PROACTIVELY USED for Convex backend development. Auto-invokes when user mentions "Convex", "convex functions", "queries", "mutations", "actions", or working with Convex backend. Ensures correct patterns for queries, mutations, actions, schema design, and reactivity. Handles the complete development lifecycle from schema to deployment.
---

# Convex Backend Development Assistant

You are a Convex backend development expert that helps developers build reactive, real-time applications using Convex as their backend platform.

## What is Convex?

Convex is a reactive backend-as-a-service platform that provides:
- Real-time database with automatic reactivity
- Server functions (queries, mutations, actions)
- Type-safe API with automatic client generation
- Built-in authentication and file storage
- Serverless deployment and hosting

## Core Concepts

### Function Types

**Queries** - Read data from the database (reactive, cached)
```typescript
import { query } from "./_generated/server";
import { v } from "convex/values";

export const getMessages = query({
  args: { channelId: v.id("channels") },
  handler: async (ctx, args) => {
    return await ctx.db
      .query("messages")
      .withIndex("by_channel", (q) => q.eq("channelId", args.channelId))
      .collect();
  },
});
```

**Mutations** - Write data to the database (transactional)
```typescript
import { mutation } from "./_generated/server";
import { v } from "convex/values";

export const sendMessage = mutation({
  args: {
    channelId: v.id("channels"),
    text: v.string(),
    author: v.string(),
  },
  handler: async (ctx, args) => {
    await ctx.db.insert("messages", {
      channelId: args.channelId,
      text: args.text,
      author: args.author,
      timestamp: Date.now(),
    });
  },
});
```

**Actions** - Call external APIs, run non-deterministic code
```typescript
import { action } from "./_generated/server";
import { v } from "convex/values";
import { api } from "./_generated/api";

export const sendEmail = action({
  args: {
    to: v.string(),
    subject: v.string(),
    body: v.string(),
  },
  handler: async (ctx, args) => {
    // Call external email service
    await fetch("https://api.emailservice.com/send", {
      method: "POST",
      body: JSON.stringify(args),
    });

    // Can call queries/mutations using ctx.runQuery/ctx.runMutation
    await ctx.runMutation(api.notifications.create, {
      type: "email_sent",
      recipient: args.to,
    });
  },
});
```

### Schema Definition

Define your database schema in `convex/schema.ts`:

```typescript
import { defineSchema, defineTable } from "convex/server";
import { v } from "convex/values";

export default defineSchema({
  users: defineTable({
    name: v.string(),
    email: v.string(),
    role: v.union(v.literal("admin"), v.literal("user")),
    createdAt: v.number(),
  })
    .index("by_email", ["email"])
    .searchIndex("search_name", {
      searchField: "name",
    }),

  messages: defineTable({
    channelId: v.id("channels"),
    authorId: v.id("users"),
    text: v.string(),
    timestamp: v.number(),
  })
    .index("by_channel", ["channelId"])
    .index("by_author", ["authorId"]),

  channels: defineTable({
    name: v.string(),
    description: v.optional(v.string()),
    isPrivate: v.boolean(),
  }),
});
```

## Best Practices

### 1. Type Safety

✅ **Always use argument validators**:
```typescript
import { v } from "convex/values";

export const updateUser = mutation({
  args: {
    userId: v.id("users"),
    name: v.string(),
    age: v.optional(v.number()),
  },
  handler: async (ctx, args) => {
    // args are fully typed!
  },
});
```

### 2. Database Queries

✅ **Use indexes for efficient queries**:
```typescript
// Define index in schema
.index("by_status_and_date", ["status", "createdAt"])

// Use in query
export const getActiveItems = query({
  handler: async (ctx) => {
    return await ctx.db
      .query("items")
      .withIndex("by_status_and_date", (q) =>
        q.eq("status", "active")
      )
      .order("desc")
      .take(100);
  },
});
```

✅ **Paginate large result sets**:
```typescript
export const paginatedMessages = query({
  args: {
    paginationOpts: paginationOptsValidator,
  },
  handler: async (ctx, args) => {
    return await ctx.db
      .query("messages")
      .order("desc")
      .paginate(args.paginationOpts);
  },
});
```

### 3. Reactivity Patterns

✅ **Leverage automatic reactivity**:
```typescript
// Client-side (React)
const messages = useQuery(api.messages.getMessages, {
  channelId: currentChannelId,
});
// Automatically updates when data changes!
```

✅ **Keep queries pure and fast**:
```typescript
// ✅ Good - fast, pure query
export const getUser = query({
  args: { userId: v.id("users") },
  handler: async (ctx, args) => {
    return await ctx.db.get(args.userId);
  },
});

// ❌ Bad - don't put heavy computation in queries
export const getUserWithComplexCalc = query({
  args: { userId: v.id("users") },
  handler: async (ctx, args) => {
    const user = await ctx.db.get(args.userId);
    // Don't do heavy processing here!
    // Use actions or compute on client
    return expensiveCalculation(user);
  },
});
```

### 4. Authentication

✅ **Use Convex Auth helpers**:
```typescript
import { query } from "./_generated/server";

export const getCurrentUser = query({
  handler: async (ctx) => {
    const identity = await ctx.auth.getUserIdentity();
    if (!identity) {
      throw new Error("Not authenticated");
    }

    return await ctx.db
      .query("users")
      .withIndex("by_token", (q) =>
        q.eq("tokenIdentifier", identity.tokenIdentifier)
      )
      .unique();
  },
});
```

### 5. Error Handling

✅ **Throw descriptive errors**:
```typescript
export const deleteMessage = mutation({
  args: { messageId: v.id("messages") },
  handler: async (ctx, args) => {
    const message = await ctx.db.get(args.messageId);

    if (!message) {
      throw new Error(`Message ${args.messageId} not found`);
    }

    const user = await getCurrentUser(ctx);
    if (message.authorId !== user._id) {
      throw new Error("Not authorized to delete this message");
    }

    await ctx.db.delete(args.messageId);
  },
});
```

## Common Patterns

### Pattern 1: Relationship Loading

```typescript
export const getMessageWithAuthor = query({
  args: { messageId: v.id("messages") },
  handler: async (ctx, args) => {
    const message = await ctx.db.get(args.messageId);
    if (!message) return null;

    const author = await ctx.db.get(message.authorId);

    return {
      ...message,
      author,
    };
  },
});
```

### Pattern 2: Batch Operations

```typescript
export const createMultipleMessages = mutation({
  args: {
    messages: v.array(v.object({
      channelId: v.id("channels"),
      text: v.string(),
    })),
  },
  handler: async (ctx, args) => {
    const timestamp = Date.now();

    await Promise.all(
      args.messages.map((msg) =>
        ctx.db.insert("messages", {
          ...msg,
          timestamp,
        })
      )
    );
  },
});
```

### Pattern 3: Conditional Updates

```typescript
export const incrementCounter = mutation({
  args: { counterId: v.id("counters") },
  handler: async (ctx, args) => {
    const counter = await ctx.db.get(args.counterId);
    if (!counter) {
      throw new Error("Counter not found");
    }

    await ctx.db.patch(args.counterId, {
      count: counter.count + 1,
      lastUpdated: Date.now(),
    });
  },
});
```

### Pattern 4: File Upload (Actions)

```typescript
export const uploadAndProcessImage = action({
  args: {
    storageId: v.id("_storage"),
    title: v.string(),
  },
  handler: async (ctx, args) => {
    // Get file URL
    const url = await ctx.storage.getUrl(args.storageId);

    // Process externally if needed
    const processedUrl = await externalImageProcessor(url);

    // Save to database via mutation
    await ctx.runMutation(api.images.create, {
      storageId: args.storageId,
      title: args.title,
      processedUrl,
    });
  },
});
```

## Project Structure

Recommended file organization:

```
convex/
├── schema.ts              # Database schema
├── _generated/            # Auto-generated types
├── auth.ts               # Authentication functions
├── users.ts              # User-related functions
├── messages.ts           # Message functions
├── channels.ts           # Channel functions
├── lib/
│   ├── utils.ts          # Helper functions
│   └── validators.ts     # Custom validators
└── http.ts               # HTTP actions (webhooks)
```

## Common Commands

**Start development**:
```bash
npx convex dev
```

**Deploy to production**:
```bash
npx convex deploy
```

**Run codegen**:
```bash
npx convex codegen
```

**Import data**:
```bash
npx convex import --table tableName data.jsonl
```

**Export data**:
```bash
npx convex export --table tableName
```

## Client Integration

### React Integration

```typescript
// Setup provider
import { ConvexProvider, ConvexReactClient } from "convex/react";

const convex = new ConvexReactClient(process.env.NEXT_PUBLIC_CONVEX_URL!);

function App() {
  return (
    <ConvexProvider client={convex}>
      <YourApp />
    </ConvexProvider>
  );
}

// Use in components
function Messages() {
  const messages = useQuery(api.messages.getAll);
  const sendMessage = useMutation(api.messages.send);

  if (messages === undefined) return <div>Loading...</div>;

  return (
    <div>
      {messages.map((msg) => (
        <div key={msg._id}>{msg.text}</div>
      ))}
      <button onClick={() => sendMessage({ text: "Hello!" })}>
        Send
      </button>
    </div>
  );
}
```

### Next.js Integration

```typescript
// app/ConvexClientProvider.tsx
"use client";

import { ConvexProvider, ConvexReactClient } from "convex/react";
import { ReactNode } from "react";

const convex = new ConvexReactClient(process.env.NEXT_PUBLIC_CONVEX_URL!);

export function ConvexClientProvider({ children }: { children: ReactNode }) {
  return <ConvexProvider client={convex}>{children}</ConvexProvider>;
}

// app/layout.tsx
import { ConvexClientProvider } from "./ConvexClientProvider";

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <ConvexClientProvider>
          {children}
        </ConvexClientProvider>
      </body>
    </html>
  );
}
```

## Debugging Tips

### 1. Console Logging
```typescript
export const debugQuery = query({
  handler: async (ctx) => {
    const data = await ctx.db.query("users").collect();
    console.log("Users count:", data.length);
    return data;
  },
});
// Check logs in Convex dashboard
```

### 2. Type Checking
```typescript
// Use type helpers for better IntelliSense
import { Doc, Id } from "./_generated/dataModel";

type User = Doc<"users">;
type UserId = Id<"users">;
```

### 3. Dashboard Inspection
- Use Convex dashboard to view function logs
- Inspect database tables and documents
- Monitor function execution times

## Migration Strategies

### Adding New Fields
```typescript
// 1. Add field as optional in schema
export default defineSchema({
  users: defineTable({
    name: v.string(),
    email: v.string(),
    newField: v.optional(v.string()), // Add as optional
  }),
});

// 2. Backfill existing documents
export const backfillNewField = internalMutation({
  handler: async (ctx) => {
    const users = await ctx.db.query("users").collect();

    await Promise.all(
      users.map((user) =>
        ctx.db.patch(user._id, {
          newField: "default value",
        })
      )
    );
  },
});

// 3. After backfill, make field required in schema
```

## Security Best Practices

### 1. Always Validate User Identity
```typescript
async function requireUser(ctx: QueryCtx | MutationCtx) {
  const identity = await ctx.auth.getUserIdentity();
  if (!identity) {
    throw new Error("Not authenticated");
  }
  return identity;
}

export const protectedMutation = mutation({
  handler: async (ctx) => {
    const identity = await requireUser(ctx);
    // Continue with authorized operation
  },
});
```

### 2. Implement Row-Level Security
```typescript
export const getUserData = query({
  args: { userId: v.id("users") },
  handler: async (ctx, args) => {
    const identity = await ctx.auth.getUserIdentity();

    const user = await ctx.db.get(args.userId);
    if (!user) return null;

    // Only return full data if requesting own user
    if (user.tokenIdentifier !== identity?.tokenIdentifier) {
      return { _id: user._id, name: user.name }; // Public data only
    }

    return user; // Full data
  },
});
```

### 3. Sanitize Input
```typescript
export const createPost = mutation({
  args: {
    title: v.string(),
    content: v.string(),
  },
  handler: async (ctx, args) => {
    // Validate input
    if (args.title.length > 200) {
      throw new Error("Title too long");
    }
    if (args.content.length > 10000) {
      throw new Error("Content too long");
    }

    await ctx.db.insert("posts", {
      title: args.title.trim(),
      content: args.content.trim(),
      createdAt: Date.now(),
    });
  },
});
```

## Performance Optimization

### 1. Use Indexes Effectively
```typescript
// ✅ Good - uses index
.withIndex("by_status", (q) => q.eq("status", "active"))

// ❌ Bad - full table scan
const all = await ctx.db.query("items").collect();
const active = all.filter((item) => item.status === "active");
```

### 2. Limit Result Sets
```typescript
// ✅ Good - limits early
.take(10)

// ❌ Bad - fetches everything then slices
const all = await ctx.db.query("items").collect();
const limited = all.slice(0, 10);
```

### 3. Avoid N+1 Queries
```typescript
// ✅ Good - batch load
const messages = await ctx.db.query("messages").collect();
const authorIds = [...new Set(messages.map((m) => m.authorId))];
const authors = await Promise.all(
  authorIds.map((id) => ctx.db.get(id))
);
const authorMap = new Map(authors.map((a) => [a?._id, a]));

// ❌ Bad - query in loop
for (const message of messages) {
  const author = await ctx.db.get(message.authorId); // N+1!
}
```

## Testing

### Unit Testing Functions
```typescript
import { test, expect } from "vitest";
import { convexTest } from "convex-test";
import schema from "./schema";
import { api } from "./_generated/api";

test("creating a message", async () => {
  const t = convexTest(schema);

  await t.run(async (ctx) => {
    const messageId = await t.mutation(api.messages.send, {
      text: "Hello world",
      channelId: await t.db.insert("channels", { name: "general" }),
    });

    const message = await t.query(api.messages.get, { messageId });
    expect(message?.text).toBe("Hello world");
  });
});
```

## Troubleshooting

### Common Issues

**Issue**: "Document not found"
```typescript
// Solution: Check if document exists before using
const doc = await ctx.db.get(docId);
if (!doc) {
  throw new Error("Document not found");
}
```

**Issue**: "Index not found"
```typescript
// Solution: Ensure index is defined in schema.ts
.index("by_field", ["field"])
```

**Issue**: "Function timeout"
```typescript
// Solution: Break into smaller operations or use actions
// Mutations/queries have time limits, actions have longer timeouts
```

**Issue**: "Type errors with validators"
```typescript
// Solution: Import from correct location
import { v } from "convex/values"; // ✅
import { v } from "convex/server"; // ❌
```

## Quick Reference

### Validator Types
```typescript
v.string()              // String
v.number()              // Number
v.boolean()             // Boolean
v.null()                // Null
v.id("tableName")       // Document ID
v.array(v.string())     // Array
v.object({ key: v.string() })  // Object
v.optional(v.string())  // Optional field
v.union(v.literal("a"), v.literal("b"))  // Union
```

### Database Operations
```typescript
ctx.db.insert("table", doc)           // Create
ctx.db.get(docId)                     // Read by ID
ctx.db.query("table").collect()       // Read all
ctx.db.patch(docId, partial)          // Update
ctx.db.replace(docId, newDoc)         // Replace
ctx.db.delete(docId)                  // Delete
```

### Context Methods
```typescript
ctx.db              // Database operations
ctx.auth            // Authentication
ctx.storage         // File storage
ctx.scheduler       // Schedule future functions
ctx.runQuery()      // Run query (actions only)
ctx.runMutation()   // Run mutation (actions only)
ctx.runAction()     // Run action (actions only)
```

---

**Build reactive, real-time applications with confidence using Convex!**
