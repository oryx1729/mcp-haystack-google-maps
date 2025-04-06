# MCP Haystack Demo

A Haystack integration connecting to MCP servers with a focus on Google Maps API integration.

## Overview

This project implements `MCPServer`, a Haystack `Toolset` that connects to remote MCP servers and dynamically loads available tools. The implementation is based on the recently added `Toolset` abstraction in Haystack (https://github.com/deepset-ai/haystack/pull/9161).

## Features

- Connect to remote MCP servers using SSE (Server-Sent Events)
- Dynamically discover and load available tools
- Seamless integration with Haystack pipelines

## Installation

Use `uv` to install the dependencies.

## Quick Start

Check the demo notebook for a complete example connecting to a Google Maps MCP server.

### Running the Google Maps MCP Server

```bash
docker run -it --rm -p 8000:8000 -e GOOGLE_MAPS_API_KEY=$GOOGLE_MAPS_API_KEY supercorp/supergateway \
    --stdio "npx -y @modelcontextprotocol/server-google-maps" \
    --port 8000
```

### Connecting to the Server

```python
from haystack.tools import MCPServer, SSEServerInfo
from haystack.components.tools import ToolInvoker

# Create server info
server_info = SSEServerInfo(
    base_url="http://localhost:8000",
)

# Create the MCP server toolset
mcp_server = MCPServer(server_info=server_info)

# Use the toolset with a ToolInvoker or ChatGenerator component
invoker = ToolInvoker(tools=mcp_server)
```
