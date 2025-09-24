---
title: "Convex Cursor Rules"
description: "A comprehensive guide to Convex development practices, covering general specifications, query and mutation examples, HTTP routing, scheduled jobs, and file handling."
category: "rules"
tags: ["Convex", "React", "Web Development", "TypeScript"]
tech_stack: ["Convex", "React", "Vite", "Shadcn", "Tailwind CSS"]
---

You are an expert in Convex, React, and web development practices. This guide provides essential rules and examples for effective development using Convex and related technologies.

# Convex Development Guide

## General Development Specifications
- **Style**: Use concise TypeScript, functional programming, declarations, iterations, modular structures, and descriptive variable names. Structure components as:
  - **Exported components**
  - **Subcomponents**
  - **Helpers**
  - **Static types**
- **Naming Conventions**: Use dash-separated directory names and named exports.
- **TypeScript Guidelines**:
  - Use `interface` instead of `type` where applicable.
  - Avoid using enums; prefer function components.
- **Syntax**: Favor concise function keywords and declaration JSX.
- **Error Handling**: Log errors early, provide user messages, utilize Zod for form validation, and return values with error bounds.
- **UI Frameworks**: Use Shadcn, Radix, Tailwind CSS, ensuring responsiveness with a mobile-first approach.
- **Performance**: Minimize the use of `useClient`, `useEffect`, and `useState`. Leverage RSC, Suspense, dynamic loading, and image optimization.
- **Key Considerations**: Utilize Nuxt URL, monitor Web Vitals, and limit the use of `useClient`.
- **Documentation**: Refer to Convex documentation for data fetching, file storage, and HTTP actions. Use `react-router-dom` for routing and Tailwind CSS for styling.

## Convex Specifics

### Query Example
```typescript
import { query } from "./_generated/server";
import { v } from "convex/values";

export const getTaskList = query({
  args: { taskListId: v.id("taskLists") },
  handler: async (ctx, args) => {
    const tasks = await ctx.db
      .query("tasks")
      .filter((q) => q.eq(q.field("taskListId"), args.taskListId))
      .order("desc")
      .take(100);
    return tasks;
  }
});
```
- **Naming**: Use `path + file + export = api.path.name`.
- **Nesting**: For example, `convex/foo/file.ts = api.foo.file.fn`.
- **Definition**: Use `export default = api.file.default`.
- **Non-JS**: Specify strings as `"path/file:fn"`.
- **Constructor**: Use `query({ handler: () => {} })`.
- **Arguments**: The second parameter should be named and serialized.
- **Context**: The first parameter includes `db`, `storage`, and `auth`.
- **Helper Function**: Define as `async function helper(ctx: QueryCtx, arg) {}`.
- **NPM Import**: Example: `import { faker } from "@faker-js/faker"`.

**IMPORTANT**: Prefer using Convex indexes over filters. Here’s an example:
```typescript
import { defineSchema, defineTable } from "convex/server";
import { v } from "convex/values";

export default defineSchema({
  messages: defineTable({
    channel: v.id("channels"),
    body: v.string(),
    user: v.id("users"),
  })
    .index("by_channel", ["channel"])
    .index("by_channel_user", ["channel", "user"]),
});
```
Using an index:
```typescript
const messages = await ctx.db
  .query("messages")
  .withIndex("by_channel", (q) =>
    q
      .eq("channel", channel)
      .gt("_creationTime", Date.now() - 2 * 60000)
      .lt("_creationTime", Date.now() - 60000),
  )
  .collect();
```

### Mutation Example
```typescript
import { mutation } from "./_generated/server";
import { v } from "convex/values";

export const createTask = mutation({
  args: { text: v.string() },
  handler: async (ctx, args) => {
    const newTaskId = await ctx.db.insert("tasks", { text: args.text });
    return newTaskId;
  }
});
```

### Action Example
```typescript
import { action } from "./_generated/server";
import { internal } from "./_generated/api";
import { v } from "convex/values";

export const sendGif = action({
  args: { queryString: v.string(), author: v.string() },
  handler: async (ctx, { queryString, author }) => {
    const data = await fetch(giphyUrl(queryString));
    const json = await data.json();
    if (!data.ok) {
      throw new Error("Giphy error: " + JSON.stringify(json));
    }
    const gifEmbedUrl = json.data.embed_url;
    await ctx.runMutation(internal.messages.sendGifMessage, {
      body: gifEmbedUrl,
      author
    });
  }
});
```

### HTTP Router Example
```typescript
import { httpRouter } from "convex/server";

const http = httpRouter();
http.route({
  path: "/postMessage",
  method: "POST",
  handler: postMessage,
});
http.route({
  pathPrefix: "/getAuthorMessages/",
  method: "GET",
  handler: getByAuthorPathSuffix,
});
export default http;
```

### Scheduled Jobs Example
```typescript
import { cronJobs } from "convex/server";
import { internal } from "./_generated/api";

const crons = cronJobs();
crons.interval(
  "clear messages table",
  { minutes: 1 },
  internal.messages.clearAll,
);
crons.monthly(
  "payment reminder",
  { day: 1, hourUTC: 16, minuteUTC: 0 },
  internal.payments.sendPaymentEmail,
  { email: "my_email@gmail.com" },
);
export default crons;
```

### File Handling
**Upload Process**: Consists of three steps (generate URL, POST, save ID).

**Generate Upload URL**:
```typescript
import { mutation } from "./_generated/server";

export const generateUploadUrl = mutation(async (ctx) => {
  return await ctx.storage.generateUploadUrl();
});
```

**Save File ID**:
```typescript
import { mutation } from "./_generated/server";
import { v } from "convex/values";

export const sendImage = mutation({
  args: { storageId: v.id("_storage"), author: v.string() },
  handler: async (ctx, args) => {
    await ctx.db.insert("messages", {
      body: args.storageId,
      author: args.author,
      format: "image",
    });
  }
});
```
Refer to Convex documentation for data fetching, file storage, vector databases, and authentication. Follow TanStack documentation for routing.