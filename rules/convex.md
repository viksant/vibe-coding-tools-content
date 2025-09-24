---
title: "Convex Cursor Rules"
description: "A comprehensive guide to Convex development practices, covering general specifications, query and mutation examples, HTTP routing, scheduled jobs, and file handling."
category: "rules"
tags: ["Convex", "React", "Web Development", "TypeScript"]
tech_stack: ["Convex", "React", "Vite", "Shadcn", "Tailwind CSS"]
---

You’re diving into Convex, React, and web development practices. This guide will help you navigate effective development using Convex and its related technologies.

# Convex Development Guide

## General Development Specifications

Let’s start with some general guidelines.

- **Style**: Keep your TypeScript concise. Use functional programming, create modular structures, and choose descriptive variable names. Structure your components like this:
  - **Exported components**
  - **Subcomponents**
  - **Helpers**
  - **Static types**
  
- **Naming Conventions**: Stick to dash-separated directory names and named exports.

- **TypeScript Guidelines**:
  - Use `interface` instead of `type` when you can.
  - Skip enums; go for function components instead.

- **Syntax**: Opt for concise function keywords and declaration JSX.

- **Error Handling**: Log errors early, provide helpful messages to users, use Zod for form validation, and return values with error bounds.

- **UI Frameworks**: Use Shadcn, Radix, and Tailwind CSS. Make sure your design is responsive and takes a mobile-first approach.

- **Performance**: Limit the use of `useClient`, `useEffect`, and `useState`. Use RSC, Suspense, dynamic loading, and optimize images.

- **Key Considerations**: Check out Nuxt URL, keep an eye on Web Vitals, and limit `useClient`.

- **Documentation**: Always refer to Convex documentation for guidance on data fetching, file storage, and HTTP actions. For routing, use `react-router-dom` and rely on Tailwind CSS for styling.

## Convex Specifics

Now, let’s look at some specific examples.

### Query Example

Here’s how you can set up a query:

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

- **Naming**: Format it like `path + file + export = api.path.name`.
- **Nesting**: For example, `convex/foo/file.ts = api.foo.file.fn`.
- **Definition**: Use `export default = api.file.default`.
- **Non-JS**: Specify strings as `"path/file:fn"`.
- **Constructor**: Use `query({ handler: () => {} })`.
- **Arguments**: Ensure the second parameter is named and serialized.
- **Context**: The first parameter should include `db`, `storage`, and `auth`.
- **Helper Function**: Define as `async function helper(ctx: QueryCtx, arg) {}`.
- **NPM Import**: Example: `import { faker } from "@faker-js/faker"`.

**Important**: Always prefer using Convex indexes over filters. Take a look at this example:

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

Using an index looks like this:

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

Here’s a straightforward mutation example:

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

Now let’s look at an action:

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

Setting up an HTTP router is also simple:

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

Creating scheduled jobs can be done like this:

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

Let’s talk about file handling. The upload process involves three steps: generating a URL, posting the upload, and saving the ID.

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

For more details on data fetching, file storage, vector databases, and authentication, check out the Convex documentation. Also, consult TanStack documentation for routing guidance.