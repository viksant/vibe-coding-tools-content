---
title: "gRPC Reflection"
description: "Enables gRPC service discovery and method invocation using reflection, supporting custom headers for flexible API interactions."
category: "mcps-servers"
tags: ["mcp", "utility", "api", "server", "data", "integration"]
tech_stack: ["gRPC", "Protocol Buffers", "Microservices", "API Testing", "Service Discovery"]
---

# gRPC Reflection

This MCP server provides seamless integration with gRPC services by leveraging gRPC reflection capabilities through grpcurl. It allows developers to dynamically discover available services, list methods, and invoke remote procedures without requiring pre-compiled protobuf definitions. The server supports custom headers for authentication and metadata, making it ideal for testing, debugging, and interacting with gRPC-based microservices in development and production environments.

Key benefits include simplified API exploration through automatic service discovery, flexible invocation with header customization, and streamlined debugging workflows. Use cases range from rapid prototyping and API testing to automated service validation and integration testing pipelines. Developers can quickly inspect service contracts, test method calls, and validate API behavior across different gRPC implementations without manual setup or protocol buffer compilation.

## Details

- **GitHub**: https://github.com/wricardo/grpcurl-mcp
- **Logo**: 
