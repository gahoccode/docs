The FastMCP command-line interface (CLI) facilitates running, developing, and installing MCP servers. Here's a guide on how to use it:

### Overview
FastMCP's CLI allows you to perform various tasks directly from your terminal, such as running servers, setting up development environments, and inspecting configurations. The CLI is installed with FastMCP, providing several powerful commands:

### Commands

1. **`fastmcp run`**
   - **Purpose:** Run a FastMCP server or proxy a remote server.
   - **Syntax:** `fastmcp run server.py`
   - **Options:** 
     - `--transport`, `-t` (Choose protocol: `stdio`, `http`, etc.)
     - `--host` (Specify host for http transport)
     - `--port`, `-p` (Specify port for http transport)
     - `--python` (Specify Python version)
   - **Entrypoints:** 
     - Inferred server instance (`server.py`)
     - Explicit server entrypoint (`server.py:custom_name`)
     - Factory function (`server.py:create_server`)
     - FastMCP configuration (`fastmcp.json`)

2. **`fastmcp dev`**
   - **Purpose:** Run a server with MCP Inspector for testing.
   - **Syntax:** `fastmcp dev server.py`
   - **Options:** 
     - `--with`, `--with-editable`
     - `--python` (Specify Python version)
   - **Entrypoints:** Same as `fastmcp run`.

3. **`fastmcp install`**
   - **Purpose:** Install a server in MCP client applications.
   - **Syntax:** `fastmcp install claude-code server.py`
   - **Options:** 
     - `--server-name`, `-n` (Custom server name)
     - `--env` (Environment variables)
     - `--with-requirements` (Dependencies)
   - **Entrypoints:** Same as `fastmcp run`.

4. **`fastmcp inspect`**
   - **Purpose:** View summary information or generate a detailed JSON report about a server.
   - **Syntax:** `fastmcp inspect server.py`
   - **Options:** 
     - `--format`, `-f` (`fastmcp` or `mcp`)
     - `--output`, `-o` (Output file)
   - **Entrypoints:** Same as `fastmcp run`.
   
5. **`fastmcp project prepare`**
   - **Purpose:** Create a persistent uv project directory from a `fastmcp.json`'s configuration.
   - **Syntax:** `fastmcp project prepare fastmcp.json --output-dir ./env`

6. **`fastmcp version`**
   - **Purpose:** Display version information.
   - **Syntax:** `fastmcp version`
   - **Options:** 
     - `--copy` (Copy version info to clipboard)

### Best Practices

- Use the **factory function** pattern to include setup code since `fastmcp run` ignores the `if __name__ == "__main__"` block.
- Using **`fastmcp dev`** allows bypassing the local environment, relying on the `uv run` subprocess, ideal for testing.
- The `--skip-env` flag in `fastmcp run` can prevent unnecessary environment setups if you're in a configured environment.

This guide should give you a solid starting point for using FastMCP's CLI to manage MCP servers effectively.
