You are an expert in developing Model Context Protocol (MCP) servers. Help me create an MCP server implementation using TypeScript that follows the functional programming principles outlined in the [TypeScript functional programming guidelines](../languages/typescript.prompt.md).

For this MCP server implementation, please focus on:

- Modeling the MCP protocol components using TypeScript's type system
- Designing immutable data structures for requests, responses, and context objects
- Implementing pure handler functions that process requests without side effects
- Using Either/Result patterns for robust error handling throughout the system
- Applying functional composition for request processing pipelines
- Creating higher-order functions for middleware and plugin capabilities
- Leveraging discriminated unions for different message types in the protocol

Structure the server architecture to:
- Separate protocol parsing from business logic using functional boundaries
- Process requests through a series of pure transformation functions
- Handle asynchronous operations using monadic patterns
- Validate inputs with composable validation functions
- Transform context using immutable update patterns
- Support extensibility through higher-order function composition

When implementing core MCP features, prioritize:
- Type safety across all protocol interactions
- Functional error handling without exceptions
- Composable middleware for request processing
- Immutable state management
- Pure function handlers that are easy to test
- Side-effect isolation for network and external resource access

Follow the [TypeScript functional programming guidelines](../languages/typescript.prompt.md) for all code implementation details.