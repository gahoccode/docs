Certainly! Here are the extracted details for MCP servers regarding installation, scopes, and use cases:

### MCP Servers Installation Methods

1. **Add a Remote HTTP Server**: 
   - HTTP servers are recommended for connecting to remote MCP servers and are widely supported for cloud-based services.
   - **Basic syntax**:
     ```bash
     claude mcp add --transport http <name> <url>
     ```
   - **Example**:
     ```bash
     claude mcp add --transport http notion https://mcp.notion.com/mcp
     ```

2. **Add a Remote SSE Server**:
   - SSE (Server-Sent Events) transport is deprecated. Use HTTP where possible.
   - **Basic syntax**:
     ```bash
     claude mcp add --transport sse <name> <url>
     ```
   - **Example**:
     ```bash
     claude mcp add --transport sse asana https://mcp.asana.com/sse
     ```

3. **Add a Local Stdio Server**:
   - Stdio servers run as local processes, ideal for tools needing system access or custom scripts.
   - **Basic syntax**:
     ```bash
     claude mcp add --transport stdio <name> <command> [args...]
     ```
   - **Example**:
     ```bash
     claude mcp add --transport stdio airtable --env AIRTABLE_API_KEY=YOUR_KEY -- npx -y airtable-mcp-server
     ```

### MCP Installation Scopes

1. **Local Scope**:
   - Default configuration, project-specific and private.
   - **Example**:
     ```bash
     claude mcp add --transport http stripe --scope local https://mcp.stripe.com
     ```

2. **Project Scope**:
   - Enables team collaboration by storing configurations in a `.mcp.json` file at the project's root.
   - **Example**:
     ```bash
     claude mcp add --transport http paypal --scope project https://mcp.paypal.com/mcp
     ```

3. **User Scope**:
   - Cross-project accessibility, private to the user.
   - **Example**:
     ```bash
     claude mcp add --transport http hubspot --scope user https://mcp.hubspot.com/anthropic
     ```

### MCP Use Cases

1. **Monitor Errors with Sentry**:
   - Add Sentry MCP server and authenticate to debug production issues.
   - **Example**:
     ```bash
     claude mcp add --transport http sentry https://mcp.sentry.dev/mcp
     ```

2. **Connect to GitHub for Code Reviews**:
   - Add GitHub MCP server to review PRs and manage issues.
   - **Example**:
     ```bash
     claude mcp add --transport http github https://api.githubcopilot.com/mcp/
     ```

3. **Query Your PostgreSQL Database**:
   - Add a PostgreSQL server to query your database naturally.
   - **Example**:
     ```bash
     claude mcp add --transport stdio db -- npx -y @bytebase/dbhub --dsn "postgresql://readonly:pass@prod.db.com:5432/analytics"
     ```
