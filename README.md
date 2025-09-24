# MCP Jira Python

A Model Context Protocol (MCP) server implementation for Jira integration in Python. This server provides comprehensive Jira functionality through MCP tools, enabling AI assistants to interact with Jira instances seamlessly.

## Features

- **Issue Management**: Create, read, update, and delete Jira issues
- **Comments & Attachments**: Add comments and manage file attachments
- **Issue Linking**: Create relationships between issues
- **Search & Discovery**: Search issues and retrieve metadata
- **User Management**: Get user information and permissions
- **Field Management**: List available fields and issue types

## Available Tools

### Issue Operations
- `create_jira_issue` - Create new Jira issues
- `get_issue` - Retrieve issue details by key
- `update_issue` - Update existing issues
- `delete_issue` - Delete issues
- `search_issues` - Search issues using JQL

### Comments & Attachments
- `add_comment` - Add comments to issues
- `add_comment_with_attachment` - Add comments with file attachments
- `attach_file` - Attach files to issues
- `attach_content` - Attach content as files to issues
- `get_issue_attachment` - Retrieve issue attachments

### Linking & Relationships
- `create_issue_link` - Create links between issues
- `list_link_types` - List available link types

### Metadata & Discovery
- `get_user` - Get user information
- `list_fields` - List available Jira fields
- `list_issue_types` - List available issue types

## Installation

### Prerequisites
- Python 3.13 or higher
- Jira instance with API access
- API token for authentication

### Install Dependencies

```bash
pip install mcp>=1.2.1 jira
```

Or using uv:
```bash
uv add mcp>=1.2.1 jira
```

## Configuration

### Environment Variables

Set the following environment variables:

```bash
export JIRA_HOST="your-domain.atlassian.net"
export JIRA_EMAIL="your-email@example.com"
export JIRA_API_TOKEN="your-api-token"
```

### Getting a Jira API Token

1. Go to [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Click "Create API token"
3. Give it a label and copy the generated token
4. Use this token as your `JIRA_API_TOKEN`

## Usage

### Running the Server

```bash
python -m mcp_jira_python.server
```

Or using the installed script:
```bash
jira-api
```

### MCP Client Integration

Add to your MCP client configuration:

```json
{
  "mcpServers": {
    "jira": {
      "command": "python",
      "args": ["-m", "mcp_jira_python.server"],
      "env": {
        "JIRA_HOST": "your-domain.atlassian.net",
        "JIRA_EMAIL": "your-email@example.com",
        "JIRA_API_TOKEN": "your-api-token"
      }
    }
  }
}
```

### Example Client Usage

See `examples/client.py` for a complete example of how to use this MCP server with the Anthropic Claude API.

```bash
python examples/client.py path/to/server.py
```

## Development

### Project Structure

```
src/mcp_jira_python/
├── __init__.py
├── server.py              # Main MCP server implementation
└── tools/                 # Individual tool implementations
    ├── __init__.py
    ├── base.py            # Base tool class
    ├── create_issue.py    # Issue creation
    ├── get_issue.py       # Issue retrieval
    ├── update_issue.py    # Issue updates
    ├── delete_issue.py    # Issue deletion
    ├── search_issues.py   # Issue search
    ├── add_comment.py     # Comment management
    ├── attach_file.py     # File attachments
    └── ...                # Other tool implementations
```

### Adding New Tools

1. Create a new tool class inheriting from `BaseTool`
2. Implement the required methods
3. Add the tool to `tools/__init__.py`
4. Register it in the `_TOOLS` dictionary

### Testing

```bash
python -m pytest tests/
```

## Security Considerations

- Store API tokens securely using environment variables
- Use HTTPS for all Jira communications
- Implement proper error handling for sensitive operations
- Consider rate limiting for production deployments

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## License

This project is licensed under the terms specified in the LICENSE file.

## Troubleshooting

### Common Issues

**Authentication Errors**
- Verify your API token is correct and hasn't expired
- Ensure your email matches your Atlassian account
- Check that your Jira host URL is correct

**Connection Issues**
- Verify network connectivity to your Jira instance
- Check firewall settings
- Ensure HTTPS is properly configured

**Tool Execution Errors**
- Check that required fields are provided
- Verify user permissions for the requested operations
- Review Jira logs for detailed error information

### Debug Mode

Set environment variable for detailed logging:
```bash
export MCP_LOG_LEVEL=DEBUG
```

## Support

For issues and questions:
- Check the existing issues in the repository
- Review Jira API documentation
- Consult MCP protocol specifications