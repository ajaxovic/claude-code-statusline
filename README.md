# Claude Code Status Line

A Python status line script for Claude Code that displays your current model, API usage limits, and working directory.

## Features

- **Model Display**: Shows the currently active Claude model
- **Usage Tracking**: Real-time 5-hour and 7-day API usage limits with color-coded alerts
  - 🟢 Green: < 50% usage
  - 🟡 Yellow: 50-80% usage
  - 🔴 Red: > 80% usage
- **Directory Info**: Displays current working directory
- **OAuth Integration**: Automatically reads credentials from Claude Code

## Prerequisites

- Python 3.10 or higher
- Claude Code with OAuth authentication configured
- Supported platforms: macOS, Linux (Windows not supported)

## Installation

1. **Clone or download this repository**
   ```bash
   git clone <repository-url>
   cd claude-code-statusline
   ```

2. **Configure Claude Code**

   Add the following to your `.claude/settings.json`:
   ```json
   {
     "statusLine": {
       "type": "command",
       "command": "python3 /path/to/statusline.py",
       "padding": 0
     }
   }
   ```

   Replace `/path/to/statusline.py` with the absolute path to this script.

4. **Restart Claude Code**

## How It Works

The script:
1. Receives session data from Claude Code via stdin (JSON format)
2. Retrieves your OAuth access token:
   - **macOS**: From Keychain using `security find-generic-password`
   - **Linux**: From `~/.claude/.credentials.json`
   - **Windows**: Not supported (returns empty)
3. Fetches current usage data from Anthropic's API
4. Outputs a formatted status line with ANSI colors

## Example Output

```
Sonnet 4.5 | 5h: 23% | 7d: 45% | Dir: /Users/you/projects/myapp
```

## Troubleshooting

- **"No credentials" message**: Ensure you're logged in to Claude Code with OAuth
- **"Usage: N/A" message**: API request failed (check network connection)
- **Script not updating**: Verify the path in `.claude/settings.json` is absolute and executable

## Documentation

For more information about status lines in Claude Code, see the [official documentation](https://code.claude.com/docs/en/statusline).