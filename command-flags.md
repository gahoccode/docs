Here are all the CLI commands along with their descriptions and examples:

### CLI Commands

- **`claude`**  
  **Description:** Start interactive REPL  
  **Example:**  
  ```claude```  

- **`claude "query"`**  
  **Description:** Start REPL with initial prompt  
  **Example:**  
  ```claude "explain this project"```  

- **`claude -p "query"`**  
  **Description:** Query via SDK, then exit  
  **Example:**  
  ```claude -p "explain this function"```  

- **`cat file | claude -p "query"`**  
  **Description:** Process piped content  
  **Example:**  
  ```cat logs.txt | claude -p "explain"```  

- **`claude -c`**  
  **Description:** Continue most recent conversation  
  **Example:**  
  ```claude -c```  

- **`claude -c -p "query"`**  
  **Description:** Continue via SDK  
  **Example:**  
  ```claude -c -p "Check for type errors"```  

- **`claude -r "<session-id>" "query"`**  
  **Description:** Resume session by ID  
  **Example:**  
  ```claude -r "abc123" "Finish this PR"```  

- **`claude update`**  
  **Description:** Update to latest version  
  **Example:**  
  ```claude update```  

- **`claude mcp`**  
  **Description:** Configure Model Context Protocol (MCP) servers  
  **Example:** See the [Claude Code MCP documentation](https://docs.claude.com/en/docs/claude-code/mcp).  

### CLI Flags

- **`--add-dir`**  
  **Description:** Add additional working directories for Claude to access (validates each path exists as a directory)  
  **Example:**  
  ```claude --add-dir ../apps ../lib```  

- **`--agents`**  
  **Description:** Define custom [subagents](https://docs.claude.com/en/docs/claude-code/sub-agents) dynamically via JSON  
  **Example:**  
  ```claude --agents '{"reviewer":{"description":"Reviews code","prompt":"You are a code reviewer"}}'```  

- **`--allowedTools`**  
  **Description:** A list of tools that should be allowed without prompting the user for permission, in addition to [settings.json files](https://docs.claude.com/en/docs/claude-code/settings)  
  **Example:**  
  ```"Bash(git log:*)" "Bash(git diff:*)" "Read"```  

- **`--disallowedTools`**  
  **Description:** A list of tools that should be disallowed without prompting the user for permission, in addition to [settings.json files](https://docs.claude.com/en/docs/claude-code/settings)  
  **Example:**  
  ```"Bash(git log:*)" "Bash(git diff:*)" "Edit"```  

- **`--print`, `-p`**  
  **Description:** Print response without interactive mode  
  **Example:**  
  ```claude -p "query"```  

- **`--append-system-prompt`**  
  **Description:** Append to system prompt (only with `--print`)  
  **Example:**  
  ```claude --append-system-prompt "Custom instruction"```  

- **`--output-format`**  
  **Description:** Specify output format for print mode (options: `text`, `json`, `stream-json`)  
  **Example:**  
  ```claude -p "query" --output-format json```  

- **`--input-format`**  
  **Description:** Specify input format for print mode (options: `text`, `stream-json`)  
  **Example:**  
  ```claude -p --output-format json --input-format stream-json```  

- **`--include-partial-messages`**  
  **Description:** Include partial streaming events in output (requires `--print` and `--output-format=stream-json`)  
  **Example:**  
  ```claude -p --output-format stream-json --include-partial-messages "query"```  

- **`--verbose`**  
  **Description:** Enable verbose logging, shows full turn-by-turn output (helpful for debugging in both print and interactive modes)  
  **Example:**  
  ```claude --verbose```  

- **`--max-turns`**  
  **Description:** Limit the number of agentic turns in non-interactive mode  
  **Example:**  
  ```claude -p --max-turns 3 "query"```  

- **`--model`**  
  **Description:** Sets the model for the current session with an alias for the latest model (`sonnet` or `opus`) or a model's full name  
  **Example:**  
  ```claude --model claude-sonnet-4-5-20250929```  

- **`--permission-mode`**  
  **Description:** Begin in a specified [permission mode](https://docs.claude.com/en/docs/claude-code/iam#permission-modes)  
  **Example:**  
  ```claude --permission-mode plan```  

- **`--permission-prompt-tool`**  
  **Description:** Specify an MCP tool to handle permission prompts in non-interactive mode  
  **Example:**  
  ```claude -p --permission-prompt-tool mcp_auth_tool "query"```  

- **`--resume`**  
  **Description:** Resume a specific session by ID, or by choosing in interactive mode  
  **Example:**  
  ```claude --resume abc123 "query"```  

- **`--continue`**  
  **Description:** Load the most recent conversation in the current directory  
  **Example:**  
  ```claude --continue```  

- **`--dangerously-skip-permissions`**  
  **Description:** Skip permission prompts (use with caution)  
  **Example:**  
  ```claude --dangerously-skip-permissions```
