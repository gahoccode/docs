The Claude Code Model Configuration instructions include three methods for changing the model used with Claude Code:

1. **Easiest Method: Use /model Command**
   - Start Claude Code by typing `claude`.
   - Input `/model` and select the desired model from the interactive menu for immediate changes.

2. **Change Model for Current Session Only**
   - Start a new Terminal session.
   - Use the `--model` flag when starting Claude Code for one-time session changes. Example commands:
     - For Haiku 4.5: `claude --model`
     - For Sonnet 4.5: `claude --model claude-sonnet-4-5-20250929`
     - Continue similarly for other supported models.

3. **Change Default Model for All Future Sessions**
   - Check your shell type with `echo $SHELL`.
   - For ZSH users (macOS), add the model setting to `~/.zshrc`. For BASH users (Linux), add it to `~/.bashrc`.
     - Example for ZSH: `echo 'export ANTHROPIC_MODEL="claude-haiku-4-5-20251001"' >> ~/.zshrc`
   - Apply the changes using `source ~/.zshrc` or `source ~/.bashrc`.
   - Close and reopen the Terminal, then start a new Claude Code session with `claude`.

4. **The available model IDs for Claude Code are:**

   - `claude-haiku-4-5-20251001`
   - `claude-sonnet-4-5-20250929`
   - `claude-opus-4-1-20250805`
   - `claude-opus-4-20250514`
   - `claude-sonnet-4-20250514`
   - `claude-3-7-sonnet-20250219`
   - `claude-3-5-haiku-20241022`

5. **Environment Variables**

   - **`ANTHROPIC_DEFAULT_OPUS_MODEL`** - The model to use for `opus`, or for `opusplan` when Plan Mode is active.
   - **`ANTHROPIC_DEFAULT_SONNET_MODEL`** - The model to use for `sonnet`, or for `opusplan` when Plan Mode is not active.
   - **`ANTHROPIC_DEFAULT_HAIKU_MODEL`** - The model to use for `haiku`, or background functionality.
   - **`CLAUDE_CODE_SUBAGENT_MODEL`** - The model to use for subagents.

Note: `ANTHROPIC_SMALL_FAST_MODEL` is deprecated in favor of `ANTHROPIC_DEFAULT_HAIKU_MODEL`.

For prompt caching configuration:

   - **`DISABLE_PROMPT_CACHING`** - Set to `1` to disable prompt caching for all models.
   - **`DISABLE_PROMPT_CACHING_HAIKU`** - Set to `1` to disable prompt caching for Haiku models only.
   - **`DISABLE_PROMPT_CACHING_SONNET`** - Set to `1` to disable prompt caching for Sonnet models only.
   - **`DISABLE_PROMPT_CACHING_OPUS`** - Set to `1` to disable prompt caching for Opus models only.

