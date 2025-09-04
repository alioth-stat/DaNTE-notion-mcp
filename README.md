<img width="1920" height="1080" alt="Dante Banner" src="https://github.com/user-attachments/assets/93152540-c8a8-40fe-813e-4ff82044137c" />
# Notion Automatic Workflow

A Python script that automatically processes todo items from a Notion page using Claude Code AI assistant. The script finds a specified Notion page, extracts uncompleted todo items, implements the code changes described in each todo, commits the changes, and marks the todos as complete.

## Features

- 🔍 **Automatic Page Discovery**: Searches for Notion pages by name
- ✅ **Todo Processing**: Extracts and processes unchecked todo items
- 🤖 **AI-Powered Implementation**: Uses Claude Code to implement code changes
- 📝 **Git Integration**: Automatically commits changes with descriptive messages
- ✨ **Notion Updates**: Marks completed todos as done in Notion

## Prerequisites

### System Requirements
- Python 3.9 or higher
- Node.js 16.0.0 or higher
- npm (Node Package Manager)
- Git (for committing changes)

### Required Services
- [Anthropic API Key](https://console.anthropic.com/) - for Claude access
- [Notion Integration Token](https://developers.notion.com/docs/create-a-notion-integration) - for Notion API access

## Installation

### 1. Clone or Download
```bash
git clone <repository-url>
cd Notionmcp
```

### 2. Install Python Dependencies
```bash
pip3 install python-dotenv rich
```

### 3. Install Claude Code
```bash
npm install -g @anthropic/claude-code
```

### 4. Set Up Environment Variables
Create a `.env` file in the project directory:
```bash
cp .env.example .env  # if available, or create manually
```

Edit the `.env` file with your API keys:
```env
NOTION_INTERNAL_INTEGRATION_SECRET=your_notion_integration_token
ANTHROPIC_API_KEY=your_anthropic_api_key
OPENAI_API_KEY=your_openai_api_key  # optional
```

### 5. Configure Notion Integration
1. Go to [Notion Integrations](https://www.notion.so/my-integrations)
2. Create a new integration
3. Copy the "Internal Integration Token"
4. Share your Notion pages/databases with the integration

### 6. Verify MCP Configuration
Ensure `mcp.json` exists and contains:
```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer YOUR_NOTION_TOKEN\", \"Notion-Version\": \"2022-06-28\"}"
      }
    }
  }
}
```

## Usage

### Basic Usage
```bash
python3 notion_automatic_workflow.py "<notion_page_name>"
```

### Example
```bash
python3 notion_automatic_workflow.py "TARSE"
```

## How It Works

1. **Page Discovery**: Searches Notion for a page with the specified name
2. **Content Extraction**: Retrieves all blocks from the page, focusing on todo items
3. **Todo Processing**: For each unchecked todo:
   - Reads and understands the todo description
   - Uses Claude Code to implement the required changes
   - Tests the implementation if tests are available
   - Commits changes with a descriptive message
   - Marks the todo as complete in Notion
4. **Summary**: Provides a report of all processed todos

## Troubleshooting

### Common Issues

**"Invalid API key" Error**
- Verify your `ANTHROPIC_API_KEY` in the `.env` file
- Ensure the API key is valid and has sufficient credits

**"NOTION_INTERNAL_INTEGRATION_SECRET not found"**
- Check that your `.env` file exists and contains the Notion token
- Verify the integration token is correct

**"Command 'claude' not found"**
- Install Claude Code: `npm install -g @anthropic/claude-code`
- Ensure npm global bin directory is in your PATH

**"No such file or directory: uv"**
- This error was fixed in the script - ensure you're using the updated version

**MCP Server Connection Issues**
- Verify Node.js is installed (`node --version`)
- Check that the Notion API version in `mcp.json` is supported (2022-06-28)

### Debug Mode
For detailed debugging, you can run Claude Code manually:
```bash
claude -p "Find Notion page named <PAGE_NAME>" --mcp-config mcp.json --verbose
```

## Project Structure

```
Notionmcp/
├── notion_automatic_workflow.py  # Main script
├── dependencies.json            # Dependency specification
├── mcp.json                    # MCP server configuration
├── .env                        # Environment variables
└── README.md                   # This file
```

## Dependencies

See `dependencies.json` for a complete list of all required dependencies, including:
- Python packages (python-dotenv, rich)
- System tools (Claude Code, Node.js)
- MCP servers (@notionhq/notion-mcp-server)
- Environment variables and configuration files

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Disclaimer  

This project is a fan creation and is not affiliated with Digital Extremes or the Warframe game. Dante and Warframe are trademarks of Digital Extremes Ltd.  


## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:
- Check the troubleshooting section above
- Review the `dependencies.json` file for requirements
- Ensure all environment variables are properly configured
