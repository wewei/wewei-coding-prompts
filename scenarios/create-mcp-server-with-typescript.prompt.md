You are an expert in developing Model Context Protocol (MCP) servers. Help me create an MCP server implementation using TypeScript that follows the functional programming principles outlined in the [TypeScript functional programming guidelines](../languages/typescript.prompt.md).

Use the [mcp-framework](https://www.npmjs.com/package/mcp-framework) package as the foundation for the implementation. This framework provides:

- Automatic discovery and loading of tools, resources, and prompts through a directory-based structure
- Multiple transport support (stdio, SSE, HTTP Stream)
- TypeScript-first development with full type safety
- Powerful base classes for tools, prompts, and resources

## Setup Process

### Creating a new MCP server

```bash
# Step 1: Check if mcp-framework is installed globally
pnpm list -g mcp-framework || pnpm install -g mcp-framework

# Step 2: Create a new MCP server project
mcp create my-mcp-server

# Step 3: Navigate to the project
cd my-mcp-server
```

### Adding Components

```bash
# Add a tool
mcp add tool data-fetch-tool

# Add a prompt
mcp add prompt data-analysis-prompt

# Add a resource
mcp add resource market-data
```

### CLI Options

The mcp-framework CLI supports several options:

```bash
# Create with HTTP transport (experimental)
mcp create my-mcp-server --http --port 1337 --cors

# Options explanation:
# --http: Use HTTP transport instead of default stdio
# --port: Specify HTTP port (default: 8080)
# --cors: Enable CORS with wildcard (*) access
```

## Code Examples

### Tool Implementation

Here's a simple example of creating a tool with the mcp-framework:

```typescript
import { MCPTool } from "mcp-framework";
import { z } from "zod";

// Define the input type with readonly properties for immutability
type ExampleInput = Readonly<{
  message: string;
}>;

class ExampleTool extends MCPTool<ExampleInput> {
  // Use readonly for immutable properties
  readonly name = "example_tool";
  readonly description = "An example tool that processes messages";
  
  // Schema validation using Zod
  readonly schema = {
    message: {
      type: z.string(),
      description: "Message to process",
    },
  };

  // Pure function approach with no side effects
  async execute(input: ExampleInput): Promise<string> {
    // Using immutable approach to transform data
    return `Processed: ${input.message}`;
  }
}

export default ExampleTool;
```

### Server Configuration

The mcp-framework makes server configuration straightforward. Here are examples of different transport configurations:

#### Basic Server (stdio transport)

```typescript
import { MCPServer } from "mcp-framework";

// Create a basic server with stdio transport (default)
const server = new MCPServer();

// Start the server
await server.start();
```

#### SSE Transport Configuration

```typescript
import { MCPServer, JWTAuthProvider } from "mcp-framework";
import { Algorithm } from "jsonwebtoken";

// Create a server with SSE transport and authentication
const server = new MCPServer({
  transport: {
    type: "sse",
    options: {
      port: 8080, // Optional (default: 8080)
      endpoint: "/sse", // Optional (default: "/sse")
      messageEndpoint: "/messages", // Optional (default: "/messages")
      // Authentication configuration
      auth: {
        provider: new JWTAuthProvider({
          secret: process.env.JWT_SECRET as string,
          algorithms: ["HS256" as Algorithm], // Optional (default: ["HS256"])
          headerName: "Authorization" // Optional (default: "Authorization")
        }),
        endpoints: {
          sse: true, // Protect SSE endpoint (default: false)
          messages: true // Protect message endpoint (default: true)
        }
      },
      // CORS configuration
      cors: {
        allowOrigin: "*", // Optional (default: "*")
        allowMethods: "GET, POST, OPTIONS", // Optional
        allowHeaders: "Content-Type, Authorization" // Optional
      }
    }
  }
});

// Start the server
await server.start();
```

#### HTTP Stream Transport

```typescript
import { MCPServer } from "mcp-framework";

// Create a server with HTTP Stream transport in batch mode (default)
const batchServer = new MCPServer({
  transport: {
    type: "http-stream",
    options: {
      responseMode: "batch" // Default behavior
    }
  }
});

// Create a server with HTTP Stream transport in stream mode
const streamServer = new MCPServer({
  transport: {
    type: "http-stream",
    options: {
      responseMode: "stream"
    }
  }
});

// Start the server
await batchServer.start();
```

When implementing MCP server features with functional programming principles, prioritize:
- Immutable data structures with readonly properties
- Pure functions that don't modify their inputs
- Type safety across all protocol interactions
- Functional error handling with Result/Either types
- Composable functions for request processing pipelines
- Clear separation of side effects from pure logic

Follow the [TypeScript functional programming guidelines](../languages/typescript.prompt.md) for all code implementation details, while leveraging the mcp-framework patterns for MCP-specific functionality.