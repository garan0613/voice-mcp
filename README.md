# 🎙️ voice-mcp

An MCP (Model Context Protocol) server for AI voice synthesis with an inline audio player. Give your AI assistant a custom cloned voice!

![License](https://img.shields.io/badge/license-MIT-green)

## Features

- 🎤 **Custom Voice Cloning** — Use MiniMax TTS API with your own cloned voice
- 🎵 **Inline Audio Player** — Beautiful WeChat-style player with waveform visualization
- 📝 **Transcript Toggle** — Show/hide the spoken text
- 🌙 **Dark Mode Support** — Automatic theme adaptation
- ⚡ **Cloudflare Workers** — Fast, serverless deployment

## Demo

When you call the `speak` tool, you get:
- A sleek audio player with play/pause button
- Animated waveform that follows playback progress
- Duration display
- Expandable transcript

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/garan0613/voice-mcp.git
cd voice-mcp
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure MiniMax API

You'll need a MiniMax account with voice cloning enabled.

Add your secrets to Cloudflare:

```bash
npx wrangler secret put MINIMAX_API_KEY
npx wrangler secret put MINIMAX_GROUP_ID
npx wrangler secret put VOICE_ID
npx wrangler secret put BOT_NAME  # Optional, defaults to "AI"
```

### 4. Deploy

```bash
npx wrangler deploy
```

### 5. Connect to Claude.ai

1. Go to **Settings → Connectors → Add Connector**
2. Enter your Worker URL: `https://your-worker.workers.dev/mcp`
3. Done! The `speak` tool is now available.

## Configuration

| Variable | Required | Description |
|----------|----------|-------------|
| `MINIMAX_API_KEY` | ✅ | Your MiniMax API key |
| `MINIMAX_GROUP_ID` | ✅ | Your MiniMax group ID |
| `VOICE_ID` | ✅ | The cloned voice ID |
| `BOT_NAME` | ❌ | Display name (default: "AI") |

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /mcp` | MCP server (SSE protocol) |
| `GET /speak?text=Hello` | Direct audio file |
| `GET /status` | Health check |

## How to Clone a Voice

1. Go to [MiniMax Console](https://platform.minimaxi.com/)
2. Navigate to Voice Cloning
3. Upload 10-30 seconds of clear audio
4. Wait for processing (usually a few minutes)
5. Copy the Voice ID

## Custom Deployment

### Using a Custom Domain

1. Add your domain to Cloudflare
2. Create a DNS record pointing to your Worker
3. Update `wrangler.jsonc`:

```json
{
  "routes": [
    { "pattern": "voice.yourdomain.com/*", "zone_name": "yourdomain.com" }
  ]
}
```

### Self-Hosting (Node.js)

The core MCP logic can be adapted for other platforms. You'll need to:

1. Replace `createMcpHandler` with a standard HTTP/SSE handler
2. Use `@modelcontextprotocol/sdk` directly
3. Handle the SSE transport yourself

## Tech Stack

- [Cloudflare Workers](https://workers.cloudflare.com/) — Serverless runtime
- [MCP SDK](https://github.com/modelcontextprotocol/sdk) — Model Context Protocol
- [MiniMax TTS](https://platform.minimaxi.com/) — Voice synthesis
- [ext-apps](https://modelcontextprotocol.io/docs/concepts/ext-apps) — Inline UI rendering

## License

MIT © 2026

## Credits

Inspired by the need to give AI assistants a voice. Built with ❤️
