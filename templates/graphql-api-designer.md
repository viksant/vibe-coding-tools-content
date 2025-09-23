---
title: "GraphQL API Designer"
description: "Design and implement comprehensive GraphQL APIs with resolvers, subscriptions, and optimization"
category: "template-prompt"
tags: ["graphql", "api-design", "resolvers", "subscriptions", "schema", "apollo"]
tech_stack: ["graphql", "apollo-server", "relay", "prisma"]
---

# GraphQL API Designer

You are a GraphQL expert specializing in designing scalable, efficient GraphQL APIs.

## GraphQL API Requirements
- **Framework**: [INSERT FRAMEWORK - Apollo Server, GraphQL Yoga, Mercurius]
- **Database**: [INSERT DATABASE - PostgreSQL, MongoDB, Prisma]
- **Authentication**: [INSERT AUTH - JWT, OAuth, Session-based]
- **Real-time**: [INSERT REAL-TIME - Subscriptions, Live Queries]
- **Caching**: [INSERT CACHING - Redis, DataLoader, Query caching]
- **Client**: [INSERT CLIENT - Apollo Client, Relay, urql]

## Schema Requirements
[INSERT DOMAIN MODEL AND BUSINESS REQUIREMENTS]

## Output Format

### GraphQL Schema Definition

```graphql
# schema.graphql

# Scalars
scalar DateTime
scalar Upload
scalar JSON

# Enums
enum UserRole {
  ADMIN
  MODERATOR
  USER
}

enum OrderStatus {
  PENDING
  PROCESSING
  SHIPPED
  DELIVERED
  CANCELLED
}

# Input Types
input CreateUserInput {
  email: String!
  password: String!
  name: String!
  role: UserRole = USER
}

input UpdateUserInput {
  email: String
  name: String
  role: UserRole
}

input UserFilters {
  role: UserRole
  isActive: Boolean
  createdAfter: DateTime
}

input PaginationInput {
  first: Int
  after: String
  last: Int
  before: String
}

# Types
type User {
  id: ID!
  email: String!
  name: String!
  role: UserRole!
  isActive: Boolean!
  avatar: String
  createdAt: DateTime!
  updatedAt: DateTime!
  
  # Relationships
  posts(first: Int, after: String): PostConnection!
  orders: [Order!]!
  profile: UserProfile
  
  # Computed fields
  postsCount: Int!
  totalSpent: Float!
}

type UserProfile {
  id: ID!
  bio: String
  website: String
  location: String
  birthDate: DateTime
  user: User!
}

type Post {
  id: ID!
  title: String!
  content: String!
  published: Boolean!
  publishedAt: DateTime
  createdAt: DateTime!
  updatedAt: DateTime!
  
  # Relationships
  author: User!
  comments(first: Int, after: String): CommentConnection!
  tags: [Tag!]!
  
  # Computed fields
  commentsCount: Int!
  likesCount: Int!
  readingTime: Int!
}

type Comment {
  id: ID!
  content: String!
  createdAt: DateTime!
  updatedAt: DateTime!
  
  # Relationships
  author: User!
  post: Post!
  parent: Comment
  replies: [Comment!]!
}

type Tag {
  id: ID!
  name: String!
  slug: String!
  description: String
  postsCount: Int!
  posts(first: Int, after: String): PostConnection!
}

# Connection Types (Relay-style pagination)
type PostConnection {
  edges: [PostEdge!]!
  pageInfo: PageInfo!
  totalCount: Int!
}

type PostEdge {
  node: Post!
  cursor: String!
}

type CommentConnection {
  edges: [CommentEdge!]!
  pageInfo: PageInfo!
  totalCount: Int!
}

type CommentEdge {
  node: Comment!
  cursor: String!
}

type PageInfo {
  hasNextPage: Boolean!
  hasPreviousPage: Boolean!
  startCursor: String
  endCursor: String
}

# Union Types
union SearchResult = User | Post | Tag

# Interface
interface Node {
  id: ID!
}

# Mutations
type Mutation {
  # User mutations
  createUser(input: CreateUserInput!): UserPayload!
  updateUser(id: ID!, input: UpdateUserInput!): UserPayload!
  deleteUser(id: ID!): DeletePayload!
  
  # Post mutations
  createPost(input: CreatePostInput!): PostPayload!
  updatePost(id: ID!, input: UpdatePostInput!): PostPayload!
  deletePost(id: ID!): DeletePayload!
  publishPost(id: ID!): PostPayload!
  
  # Comment mutations
  createComment(input: CreateCommentInput!): CommentPayload!
  updateComment(id: ID!, input: UpdateCommentInput!): CommentPayload!
  deleteComment(id: ID!): DeletePayload!
  
  # File upload
  uploadFile(file: Upload!): FilePayload!
}

# Payload Types
type UserPayload {
  success: Boolean!
  message: String
  user: User
  errors: [FieldError!]
}

type PostPayload {
  success: Boolean!
  message: String
  post: Post
  errors: [FieldError!]
}

type CommentPayload {
  success: Boolean!
  message: String
  comment: Comment
  errors: [FieldError!]
}

type DeletePayload {
  success: Boolean!
  message: String
  deletedId: ID
}

type FilePayload {
  success: Boolean!
  message: String
  url: String
  filename: String
}

type FieldError {
  field: String!
  message: String!
}

# Queries
type Query {
  # User queries
  user(id: ID!): User
  users(
    filters: UserFilters
    pagination: PaginationInput
    sortBy: String
    sortOrder: SortOrder
  ): UserConnection!
  me: User
  
  # Post queries
  post(id: ID, slug: String): Post
  posts(
    filters: PostFilters
    pagination: PaginationInput
    sortBy: String
    sortOrder: SortOrder
  ): PostConnection!
  
  # Search
  search(
    query: String!
    type: SearchType
    first: Int
    after: String
  ): SearchConnection!
  
  # Analytics
  analytics: Analytics!
}

# Subscriptions
type Subscription {
  # Real-time post updates
  postAdded: Post!
  postUpdated(id: ID!): Post!
  postDeleted: ID!
  
  # Real-time comments
  commentAdded(postId: ID!): Comment!
  commentUpdated(id: ID!): Comment!
  commentDeleted: ID!
  
  # User notifications
  notificationAdded(userId: ID!): Notification!
}
```

### Resolver Implementation

```javascript
// resolvers/index.js
import { GraphQLScalarType } from 'graphql';
import { Kind } from 'graphql/language';
import { DateTimeResolver, JSONResolver } from 'graphql-scalars';
import DataLoader from 'dataloader';

// Custom scalar resolvers
const Upload = new GraphQLScalarType({
  name: 'Upload',
  description: 'The `Upload` scalar type represents a file upload.',
});

// DataLoader for N+1 problem resolution
const createLoaders = ({ db }) => ({
  userById: new DataLoader(async (ids) => {
    const users = await db.user.findMany({
      where: { id: { in: ids } }
    });
    return ids.map(id => users.find(user => user.id === id));
  }),
  
  postsByUserId: new DataLoader(async (userIds) => {
    const posts = await db.post.findMany({
      where: { authorId: { in: userIds } },
      include: { author: true }
    });
    
    return userIds.map(userId => 
      posts.filter(post => post.authorId === userId)
    );
  }),
  
  commentsByPostId: new DataLoader(async (postIds) => {
    const comments = await db.comment.findMany({
      where: { postId: { in: postIds } },
      include: { author: true }
    });
    
    return postIds.map(postId =>
      comments.filter(comment => comment.postId === postId)
    );
  })
});

// Main resolver object
const resolvers = {
  // Scalar resolvers
  DateTime: DateTimeResolver,
  JSON: JSONResolver,
  Upload,

  // Query resolvers
  Query: {
    // User queries
    user: async (parent, { id }, { db, loaders }) => {
      return loaders.userById.load(id);
    },
    
    users: async (parent, { filters, pagination, sortBy, sortOrder }, { db }) => {
      const where = buildUserFilters(filters);
      const orderBy = buildOrderBy(sortBy, sortOrder);
      const { first, after, last, before } = pagination || {};
      
      // Implement cursor-based pagination
      const take = first || last || 10;
      const cursor = after || before;
      
      const users = await db.user.findMany({
        where,
        orderBy,
        take: take + 1, // +1 to check if there's a next page
        cursor: cursor ? { id: cursor } : undefined,
        skip: cursor ? 1 : 0
      });
      
      const hasNextPage = users.length > take;
      const edges = users.slice(0, take).map(user => ({
        node: user,
        cursor: user.id
      }));
      
      return {
        edges,
        pageInfo: {
          hasNextPage,
          hasPreviousPage: !!after,
          startCursor: edges[0]?.cursor,
          endCursor: edges[edges.length - 1]?.cursor
        },
        totalCount: await db.user.count({ where })
      };
    },
    
    me: async (parent, args, { user, db, loaders }) => {
      if (!user) throw new Error('Not authenticated');
      return loaders.userById.load(user.id);
    },
    
    // Post queries
    post: async (parent, { id, slug }, { db }) => {
      const where = id ? { id } : { slug };
      return db.post.findUnique({ where, include: { author: true, tags: true } });
    },
    
    posts: async (parent, { filters, pagination, sortBy, sortOrder }, { db }) => {
      // Similar pagination logic as users
      const where = buildPostFilters(filters);
      const orderBy = buildOrderBy(sortBy, sortOrder);
      
      return paginatedQuery(db.post, { where, orderBy }, pagination);
    },
    
    // Search
    search: async (parent, { query, type, first, after }, { db }) => {
      const searchResults = await performSearch(db, query, type, first, after);
      return searchResults;
    }
  },

  // Mutation resolvers
  Mutation: {
    createUser: async (parent, { input }, { db, user }) => {
      try {
        // Validate permissions
        if (!user || user.role !== 'ADMIN') {
          throw new Error('Insufficient permissions');
        }
        
        // Validate input
        const errors = await validateUserInput(input);
        if (errors.length > 0) {
          return { success: false, errors };
        }
        
        // Hash password
        const hashedPassword = await hashPassword(input.password);
        
        // Create user
        const newUser = await db.user.create({
          data: {
            ...input,
            password: hashedPassword
          }
        });
        
        return {
          success: true,
          message: 'User created successfully',
          user: newUser
        };
      } catch (error) {
        return {
          success: false,
          message: error.message,
          errors: [{ field: 'general', message: error.message }]
        };
      }
    },
    
    createPost: async (parent, { input }, { db, user }) => {
      try {
        if (!user) throw new Error('Not authenticated');
        
        const post = await db.post.create({
          data: {
            ...input,
            authorId: user.id
          },
          include: { author: true, tags: true }
        });
        
        // Publish subscription
        pubsub.publish('POST_ADDED', { postAdded: post });
        
        return {
          success: true,
          message: 'Post created successfully',
          post
        };
      } catch (error) {
        return {
          success: false,
          message: error.message,
          errors: [{ field: 'general', message: error.message }]
        };
      }
    },
    
    uploadFile: async (parent, { file }, { db, user }) => {
      try {
        if (!user) throw new Error('Not authenticated');
        
        const { createReadStream, filename, mimetype } = await file;
        const stream = createReadStream();
        
        // Upload to cloud storage (S3, CloudFlare, etc.)
        const url = await uploadToStorage(stream, filename, mimetype);
        
        return {
          success: true,
          url,
          filename
        };
      } catch (error) {
        return {
          success: false,
          message: error.message
        };
      }
    }
  },

  // Type resolvers
  User: {
    posts: async (parent, { first, after }, { loaders }) => {
      const posts = await loaders.postsByUserId.load(parent.id);
      return paginateArray(posts, { first, after });
    },
    
    postsCount: async (parent, args, { db }) => {
      return db.post.count({ where: { authorId: parent.id } });
    },
    
    totalSpent: async (parent, args, { db }) => {
      const orders = await db.order.findMany({
        where: { userId: parent.id, status: 'COMPLETED' }
      });
      return orders.reduce((total, order) => total + order.amount, 0);
    },
    
    profile: async (parent, args, { db }) => {
      return db.userProfile.findUnique({
        where: { userId: parent.id }
      });
    }
  },

  Post: {
    author: async (parent, args, { loaders }) => {
      return loaders.userById.load(parent.authorId);
    },
    
    comments: async (parent, { first, after }, { loaders }) => {
      const comments = await loaders.commentsByPostId.load(parent.id);
      return paginateArray(comments, { first, after });
    },
    
    commentsCount: async (parent, args, { db }) => {
      return db.comment.count({ where: { postId: parent.id } });
    },
    
    readingTime: (parent) => {
      const wordsPerMinute = 200;
      const wordCount = parent.content.split(' ').length;
      return Math.ceil(wordCount / wordsPerMinute);
    }
  },

  Comment: {
    author: async (parent, args, { loaders }) => {
      return loaders.userById.load(parent.authorId);
    },
    
    post: async (parent, args, { db }) => {
      return db.post.findUnique({ where: { id: parent.postId } });
    },
    
    replies: async (parent, args, { db }) => {
      return db.comment.findMany({
        where: { parentId: parent.id },
        include: { author: true }
      });
    }
  },

  // Subscription resolvers
  Subscription: {
    postAdded: {
      subscribe: () => pubsub.asyncIterator(['POST_ADDED'])
    },
    
    postUpdated: {
      subscribe: withFilter(
        () => pubsub.asyncIterator(['POST_UPDATED']),
        (payload, variables) => {
          return payload.postUpdated.id === variables.id;
        }
      )
    },
    
    commentAdded: {
      subscribe: withFilter(
        () => pubsub.asyncIterator(['COMMENT_ADDED']),
        (payload, variables) => {
          return payload.commentAdded.postId === variables.postId;
        }
      )
    }
  },

  // Union resolver
  SearchResult: {
    __resolveType: (obj) => {
      if (obj.email) return 'User';
      if (obj.title) return 'Post';
      if (obj.slug) return 'Tag';
      return null;
    }
  }
};

// Helper functions
const buildUserFilters = (filters) => {
  if (!filters) return {};
  
  const where = {};
  if (filters.role) where.role = filters.role;
  if (filters.isActive !== undefined) where.isActive = filters.isActive;
  if (filters.createdAfter) where.createdAt = { gte: filters.createdAfter };
  
  return where;
};

const buildOrderBy = (sortBy, sortOrder) => {
  if (!sortBy) return { createdAt: 'desc' };
  
  return {
    [sortBy]: sortOrder === 'ASC' ? 'asc' : 'desc'
  };
};

const validateUserInput = async (input) => {
  const errors = [];
  
  if (!input.email || !isValidEmail(input.email)) {
    errors.push({ field: 'email', message: 'Valid email is required' });
  }
  
  if (!input.password || input.password.length < 8) {
    errors.push({ field: 'password', message: 'Password must be at least 8 characters' });
  }
  
  return errors;
};

export default resolvers;
```

### Apollo Server Setup

```javascript
// server.js
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';
import { makeExecutableSchema } from '@graphql-tools/schema';
import { applyMiddleware } from 'graphql-middleware';
import { shield, rule, and, or } from 'graphql-shield';
import { RateLimiterMemory } from 'rate-limiter-flexible';
import jwt from 'jsonwebtoken';
import depthLimit from 'graphql-depth-limit';
import costAnalysis from 'graphql-cost-analysis';

import typeDefs from './schema.graphql';
import resolvers from './resolvers/index.js';

// Rate limiting
const rateLimiter = new RateLimiterMemory({
  keyName: 'ip',
  points: 100, // Number of requests
  duration: 60, // Per 60 seconds
});

// Authentication rules
const isAuthenticated = rule({ cache: 'contextual' })(
  async (parent, args, { user }) => {
    return user !== null;
  }
);

const isAdmin = rule({ cache: 'contextual' })(
  async (parent, args, { user }) => {
    return user && user.role === 'ADMIN';
  }
);

const isOwner = rule({ cache: 'contextual' })(
  async (parent, { id }, { user, db }) => {
    if (!user) return false;
    
    const resource = await db.post.findUnique({ where: { id } });
    return resource && resource.authorId === user.id;
  }
);

// Permissions shield
const permissions = shield({
  Query: {
    me: isAuthenticated,
    users: isAuthenticated,
  },
  Mutation: {
    createUser: isAdmin,
    updateUser: or(isAdmin, isOwner),
    deleteUser: isAdmin,
    createPost: isAuthenticated,
    updatePost: and(isAuthenticated, isOwner),
    deletePost: and(isAuthenticated, isOwner),
  }
}, {
  allowExternalErrors: true,
  fallbackError: 'Insufficient permissions'
});

// Create executable schema
const schema = makeExecutableSchema({
  typeDefs,
  resolvers,
});

// Apply middleware
const protectedSchema = applyMiddleware(schema, permissions);

// Create Apollo Server
const server = new ApolloServer({
  schema: protectedSchema,
  plugins: [
    // Query complexity analysis
    costAnalysis({
      maximumCost: 1000,
      defaultCost: 1,
      scalarCost: 1,
      objectCost: 1,
      listFactor: 10,
      introspectionCost: 1000,
      createError: (max, actual) => {
        return new Error(`Query cost ${actual} exceeds maximum cost ${max}`);
      }
    }),
    
    // Development-only query playground
    ...(process.env.NODE_ENV === 'development' ? [
      require('@apollo/server/plugin/landingPage/graphQLPlayground').default()
    ] : [])
  ],
  validationRules: [
    depthLimit(10), // Limit query depth
  ],
  formatError: (error) => {
    // Log error for monitoring
    console.error('GraphQL Error:', error);
    
    // Don't expose internal errors in production
    if (process.env.NODE_ENV === 'production') {
      if (error.message.startsWith('Database')) {
        return new Error('Internal server error');
      }
    }
    
    return error;
  }
});

// Context function
const createContext = async ({ req }) => {
  // Rate limiting
  try {
    await rateLimiter.consume(req.ip);
  } catch (rejRes) {
    throw new Error('Too many requests');
  }
  
  // Authentication
  let user = null;
  const token = req.headers.authorization?.replace('Bearer ', '');
  
  if (token) {
    try {
      const decoded = jwt.verify(token, process.env.JWT_SECRET);
      user = await db.user.findUnique({ where: { id: decoded.userId } });
    } catch (error) {
      // Invalid token - continue without user
    }
  }
  
  return {
    db,
    user,
    loaders: createLoaders({ db }),
    pubsub
  };
};

// Start server
const { url } = await startStandaloneServer(server, {
  listen: { port: process.env.PORT || 4000 },
  context: createContext
});

console.log(`🚀 Server ready at ${url}`);
```

### Client-side Usage (Apollo Client)

```typescript
// client/apollo.ts
import { ApolloClient, InMemoryCache, createHttpLink, from } from '@apollo/client';
import { setContext } from '@apollo/client/link/context';
import { onError } from '@apollo/client/link/error';
import { createUploadLink } from 'apollo-upload-client';

// HTTP link for queries and mutations
const httpLink = createHttpLink({
  uri: process.env.NEXT_PUBLIC_GRAPHQL_ENDPOINT,
});

// Upload link for file uploads
const uploadLink = createUploadLink({
  uri: process.env.NEXT_PUBLIC_GRAPHQL_ENDPOINT,
});

// Auth link
const authLink = setContext((_, { headers }) => {
  const token = localStorage.getItem('token');
  
  return {
    headers: {
      ...headers,
      authorization: token ? `Bearer ${token}` : "",
    }
  };
});

// Error link
const errorLink = onError(({ graphQLErrors, networkError, operation, forward }) => {
  if (graphQLErrors) {
    graphQLErrors.forEach(({ message, locations, path }) => {
      console.error(`GraphQL error: Message: ${message}, Location: ${locations}, Path: ${path}`);
    });
  }
  
  if (networkError) {
    console.error(`Network error: ${networkError}`);
    
    // Handle authentication errors
    if (networkError.statusCode === 401) {
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
  }
});

// Create Apollo Client
export const client = new ApolloClient({
  link: from([
    errorLink,
    authLink,
    uploadLink
  ]),
  cache: new InMemoryCache({
    typePolicies: {
      User: {
        fields: {
          posts: {
            merge(existing = { edges: [] }, incoming) {
              return {
                ...incoming,
                edges: [...existing.edges, ...incoming.edges]
              };
            }
          }
        }
      }
    }
  }),
  defaultOptions: {
    watchQuery: {
      errorPolicy: 'all'
    }
  }
});

// GraphQL queries and mutations
export const GET_POSTS = gql`
  query GetPosts($first: Int, $after: String) {
    posts(pagination: { first: $first, after: $after }) {
      edges {
        node {
          id
          title
          content
          publishedAt
          author {
            id
            name
            avatar
          }
          commentsCount
          likesCount
        }
        cursor
      }
      pageInfo {
        hasNextPage
        endCursor
      }
    }
  }
`;

export const CREATE_POST = gql`
  mutation CreatePost($input: CreatePostInput!) {
    createPost(input: $input) {
      success
      message
      post {
        id
        title
        content
        author {
          id
          name
        }
      }
      errors {
        field
        message
      }
    }
  }
`;
```

## Success Criteria
- Schema follows GraphQL best practices
- N+1 queries resolved with DataLoaders
- Proper authentication and authorization
- Real-time subscriptions working
- Query complexity and rate limiting implemented