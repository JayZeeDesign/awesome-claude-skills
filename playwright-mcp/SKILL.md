---
name: playwright-mcp
description: Guide for using the Playwright MCP (Model Context Protocol) server to perform browser automation, web testing, and UI verification through direct tool calls. Use when you need to interact with web applications, take screenshots, or test web interfaces without writing custom scripts.
---

# Playwright MCP Server

The Playwright MCP server provides browser automation tools directly to Claude through the Model Context Protocol. Unlike the webapp-testing skill which requires writing Python scripts, the Playwright MCP enables browser automation through simple tool calls.

## Installation

To use the Playwright MCP server, add it to your Claude configuration:

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

This adds the following configuration to `~/.config/claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

After adding the MCP server, restart Claude for the changes to take effect.

## Available Tools

The Playwright MCP server provides tools for:

- **Browser Navigation**: Navigate to URLs and interact with web pages
- **Element Interaction**: Click buttons, fill forms, and interact with UI elements
- **Screenshot Capture**: Take screenshots of entire pages or specific elements
- **Content Extraction**: Extract text, HTML, or specific data from web pages
- **Page Evaluation**: Run JavaScript in the browser context
- **Waiting & Timing**: Wait for elements, network requests, or specific conditions

## When to Use Playwright MCP vs webapp-testing

**Use Playwright MCP when:**
- You need quick, interactive browser automation
- Testing simple workflows or UI interactions
- Taking screenshots for visual verification
- Extracting data from web pages
- You want Claude to handle browser automation directly

**Use webapp-testing skill (Python scripts) when:**
- You need complex, reusable test automation
- Running tests as part of CI/CD pipelines
- Managing multiple servers (frontend + backend)
- Creating persistent test suites
- You need fine-grained control over Playwright API

## Example Usage Patterns

### Basic Navigation and Screenshot
```
Navigate to https://example.com and take a screenshot of the homepage
```

### Form Interaction
```
Go to the login page, fill in the username "test@example.com" and password "password123", then click the login button
```

### Content Extraction
```
Navigate to the product page and extract all product names and prices
```

### Element Verification
```
Check if the "Add to Cart" button is visible on the product page
```

## Best Practices

1. **Wait for Content**: Always ensure pages are fully loaded before interacting
2. **Use Descriptive Selectors**: Prefer text-based selectors (e.g., "Click the 'Submit' button") over CSS selectors
3. **Take Screenshots**: Capture screenshots to verify visual state when debugging
4. **Handle Errors Gracefully**: Be prepared for elements that might not exist
5. **Respect Rate Limits**: Don't overwhelm servers with rapid requests

## Comparison with Other Approaches

| Feature | Playwright MCP | webapp-testing | Manual Playwright Scripts |
|---------|---------------|----------------|---------------------------|
| Setup Complexity | Low | Medium | High |
| Interactivity | High | Low | Medium |
| Reusability | Medium | High | High |
| CI/CD Integration | Low | High | High |
| Learning Curve | Low | Medium | High |
| Control Level | Medium | High | High |

## Related Skills

- **webapp-testing**: For complex, script-based Playwright automation
- **artifacts-builder**: For creating interactive web UIs to test

## Security Considerations

- The Playwright MCP server can navigate to any URL and execute JavaScript
- Only use it on trusted websites
- Be cautious with sensitive information (passwords, API keys)
- Screenshots may contain sensitive data - handle appropriately

## Troubleshooting

**MCP server not available:**
- Ensure you've restarted Claude after adding the configuration
- Verify the configuration in `~/.config/claude/claude_desktop_config.json`
- Check that `npx` is available in your PATH

**Browser not launching:**
- Ensure Playwright browsers are installed: `npx playwright install`
- Check for permission issues with browser binaries

**Timeout errors:**
- Increase timeout values for slow-loading pages
- Ensure network connectivity
- Verify the target website is accessible
