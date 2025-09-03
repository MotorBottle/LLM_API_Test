# LLM API Test Tool

A Vue.js-based web interface for testing Large Language Model APIs with support for streaming, thinking content, and various API formats.

## Features

- **Clean Web Interface** - User-friendly Vue.js interface with no backend required
- **API Configuration** - Configurable base URL, API key, model name, and streaming mode
- **Message Management** - Dynamic message blocks with role selection (system/user/assistant)
- **Streaming Support** - Real-time streaming responses with progressive text display
- **Thinking Content** - Special handling for LLM reasoning/thinking sections
- **Response Toggle** - Switch between styled view and raw JSON output
- **Auto-save** - Automatically remembers your configuration and messages
- **Export to cURL** - Generate cURL commands from your configuration
- **Privacy-focused** - All processing happens locally in your browser

## Quick Start

### Option 1: Direct File Access
1. Clone or download this repository
2. Open `index.html` directly in your web browser
3. Configure your API settings and start testing

### Option 2: Using Caddy (Recommended)
1. Install [Caddy](https://caddyserver.com/)
2. Navigate to the project directory
3. Run: `caddy run`
4. Open `http://localhost:8080` in your browser

## Configuration

### API Settings
- **Base URL**: Your LLM API endpoint (e.g., `http://127.0.0.1:3000/v1/chat/completions`)
- **API Key**: Your API authentication key
- **Model Name**: The model to use (e.g., `llama3.1:70b`)
- **Streaming**: Enable/disable real-time streaming responses

### Additional Parameters
Configure extra parameters in JSON format:
```json
{
  "num_ctx": 2048,
  "max_tokens": 10,
  "temperature": 0.7
}
```

## Usage

1. **Configure API**: Set your base URL, API key, and model name
2. **Add Messages**: Create conversation messages with different roles
3. **Send Request**: Click "Send Request" to test your API
4. **View Response**: Toggle between styled and raw JSON views
5. **Save/Load**: Your configuration is auto-saved and can be manually managed

## HTTP/HTTPS Compatibility

⚠️ **Important**: If your API uses HTTP (not HTTPS), you must access this web page via HTTP as well to avoid CORS policy errors.

- ✅ API: `http://localhost:3000` → Page: `http://localhost:8080`
- ❌ API: `http://localhost:3000` → Page: `https://example.com` (CORS error)
- ❌ API: `http://localhost:3000` → Page: `file:///path/to/index.html` (CORS error)

## Supported API Formats

### OpenAI-Compatible APIs
```json
{
  "model": "gpt-4",
  "messages": [...],
  "stream": false,
  "max_tokens": 100
}
```

### Thinking Content Support
The tool automatically detects and displays thinking content from APIs that support reasoning traces:

**Response with thinking:**
```json
{
  "choices": [{
    "message": {
      "thinking": "Let me think about this step by step...",
      "content": "The answer is 42."
    }
  }]
}
```

## Files

- `index.html` - Main application (single-file Vue.js app)
- `Caddyfile` - Caddy server configuration
- `sample code` - Original cURL example
- `LICENSE` - MIT license
- `README.md` - This file

## Browser Compatibility

- Modern browsers with ES6+ support
- Chrome, Firefox, Safari, Edge (latest versions)
- Requires JavaScript enabled

## Privacy & Security

- **Client-side only**: All processing happens in your browser
- **No data collection**: No analytics or tracking
- **Local storage**: Configuration saved to browser's localStorage
- **Direct API calls**: Requests go directly from your browser to your API

## Development

This is a single-file Vue.js application with no build process required. To modify:

1. Edit `index.html`
2. Refresh your browser to see changes
3. Use browser developer tools for debugging

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Contributing

1. Fork the repository
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## Troubleshooting

### CORS Errors
- Ensure protocol matching (HTTP page for HTTP API)
- Use Caddy to serve the page properly
- Check your API's CORS configuration

### Streaming Issues
- Verify your API supports Server-Sent Events (SSE)
- Check the streaming response format matches expected patterns
- Enable browser dev tools to debug streaming responses

### Configuration Not Saving
- Check if localStorage is enabled in your browser
- Clear browser cache and try again
- Use manual Save/Load Config buttons

## API Response Examples

### Non-streaming Response
```json
{
  "choices": [{
    "message": {
      "role": "assistant", 
      "content": "Hello! How can I help you today?"
    }
  }]
}
```

### Streaming Response
```
data: {"choices":[{"delta":{"content":"Hello"}}]}

data: {"choices":[{"delta":{"content":" there"}}]}

data: [DONE]
```