
[Offical MCP Client Guide](https://modelcontextprotocol.io/docs/develop/build-client)


# Build an MCP client

## Get Started

Learn how to build an LLM-powered chatbot client connecting to MCP servers. Prior knowledge from the "Build an MCP Server" tutorial is beneficial. Tutorials are available in:

- Python
- Node
- Java
- Kotlin
- C#

Complete code for this tutorial is available [here](https://github.com/modelcontextprotocol/quickstart-resources/tree/main/mcp-client-python).

## System Requirements

Ensure the system has:

- Mac or Windows computer
- Latest Python version
- Latest version of `uv`

## Setting Up Your Environment

Create a new Python project with `uv`:

```bash
uv init mcp-client
cd mcp-client
uv venv
source .venv/bin/activate  # For macOS/Linux
uv add mcp anthropic python-dotenv
rm main.py
touch client.py
```

## Setting Up Your API Key

You need an Anthropic API key from the [Anthropic Console](https://console.anthropic.com/settings/keys). Store it in a `.env` file:

```bash
echo "ANTHROPIC_API_KEY=your-api-key-goes-here" > .env
```

Add `.env` to `.gitignore`:

```bash
echo ".env" >> .gitignore
```

## Creating the Client

### Basic Client Structure

Set up imports and initialize the client class:

```python
import asyncio
from typing import Optional
from contextlib import AsyncExitStack
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client
from anthropic import Anthropic
from dotenv import load_dotenv

load_dotenv()

class MCPClient:
    def __init__(self):
        self.session: Optional[ClientSession] = None
        self.exit_stack = AsyncExitStack()
        self.anthropic = Anthropic()
    # methods will go here
```

### Server Connection Management

Implement server connection method:

```python
async def connect_to_server(self, server_script_path: str):
    is_python = server_script_path.endswith('.py')
    is_js = server_script_path.endswith('.js')
    if not (is_python or is_js):
        raise ValueError("Server script must be a .py or .js file")
    command = "python" if is_python else "node"
    server_params = StdioServerParameters(command=command, args=[server_script_path], env=None)
    stdio_transport = await self.exit_stack.enter_async_context(stdio_client(server_params))
    self.stdio, self.write = stdio_transport
    self.session = await self.exit_stack.enter_async_context(ClientSession(self.stdio, self.write))
    await self.session.initialize()
    response = await self.session.list_tools()
    tools = response.tools
    print("\nConnected to server with tools:", [tool.name for tool in tools])
```

### Query Processing Logic

Add core functionality for processing queries and handling tool calls:

```python
async def process_query(self, query: str) -> str:
    messages = [{"role": "user", "content": query}]
    response = await self.session.list_tools()
    available_tools = [{"name": tool.name, "description": tool.description, "input_schema": tool.inputSchema} for tool in response.tools]
    response = self.anthropic.messages.create(model="claude-3-5-sonnet-20241022", max_tokens=1000, messages=messages, tools=available_tools)
    final_text = []
    assistant_message_content = []
    for content in response.content:
        if content.type == 'text':
            final_text.append(content.text)
            assistant_message_content.append(content)
        elif content.type == 'tool_use':
            tool_name = content.name
            tool_args = content.input
            result = await self.session.call_tool(tool_name, tool_args)
            final_text.append(f"[Calling tool {tool_name} with args {tool_args}]")
            assistant_message_content.append(content)
            messages.append({"role": "assistant", "content": assistant_message_content})
            messages.append({"role": "user", "content": [{"type": "tool_result", "tool_use_id": content.id, "content": result.content}]})
            response = self.anthropic.messages.create(model="claude-3-5-sonnet-20241022", max_tokens=1000, messages=messages, tools=available_tools)
            final_text.append(response.content[0].text)
    return "\n".join(final_text)
```

### Interactive Chat Interface

Add chat loop and cleanup functionality:

```python
async def chat_loop(self):
    print("\nMCP Client Started!")
    print("Type your queries or 'quit' to exit.")
    while True:
        try:
            query = input("\nQuery: ").strip()
            if query.lower() == 'quit':
                break
            response = await self.process_query(query)
            print("\n" + response)
        except Exception as e:
            print(f"\nError: {str(e)}")
async def cleanup(self):
    await self.exit_stack.aclose()
```

### Main Entry Point

Add main execution logic:

```python
async def main():
    if len(sys.argv) < 2:
        print("Usage: python client.py <path_to_server_script>")
        sys.exit(1)
    client = MCPClient()
    try:
        await client.connect_to_server(sys.argv[1])
        await client.chat_loop()
    finally:
        await client.cleanup()

if __name__ == "__main__":
    import sys
    asyncio.run(main())
```

Complete `client.py` file is available [here](https://github.com/modelcontextprotocol/quickstart-resources/blob/main/mcp-client-python/client.py).

## Key Components Explained

1. **Client Initialization**: Initializes with session management and API clients, uses `AsyncExitStack` for resource management.
2. **Server Connection**: Supports Python and Node.js servers, validates server script type, and initializes session.
3. **Query Processing**: Maintains conversation context, manages message flow, and combines results.
4. **Interactive Interface**: Command-line interface for user input with basic error handling.
5. **Resource Management**: Clean up resources and manage connections.

## Common Customization Points

1. **Tool Handling**: Modify `process_query()` for specific tool types.
2. **Response Processing**: Customize response formatting and logging.
3. **User Interface**: Add GUI or web interface.

## Running the Client

Run your client with any MCP server:

```bash
uv run client.py path/to/server.py
```

## How It Works

Upon querying:
1. Lists available tools from server.
2. Sends query to Claude.
3. Executes requested tool calls through server.
4. Displays response.

## Best Practices

- **Error Handling**: Use try-catch blocks.
- **Resource Management**: Use `AsyncExitStack`, close connections, and handle disconnections.
- **Security**: Store keys securely, validate responses, cautious with tool permissions.
- **Tool Names**: Validate names according to format.

## Troubleshooting

- **Server Path Issues**: Check and correct path usage.
- **Response Timing**: First response can take up to 30 seconds.
- **Common Error Messages**: Address specific issues like `FileNotFoundError` or `Connection refused`.

## Next steps

- Example servers: Explore MCP servers and implementations.
- Example clients: View clients supporting MCP integrations.
