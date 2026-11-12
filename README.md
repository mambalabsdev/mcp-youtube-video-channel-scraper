# YouTube Channel and Video List Scraper MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-youtube-video-channel-scraper/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-youtube-video-channel-scraper) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-youtube-video-channel-scraper%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-youtube-video-channel-scraper&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-youtube-video-channel-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-youtube-video-channel-scraper) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-youtube-video-channel-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-youtube-video-channel-scraper) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-youtube-video-channel-scraper)](https://github.com/mambalabsdev/mcp-youtube-video-channel-scraper/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-youtube-video-channel-scraper)

An MCP server for the Mamba Labs YouTube Channel and Video List Scraper actor on Apify. Scrape public YouTube channels, playlists, and search lists as flat rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give YouTube channels, playlists, or search terms. You get a row per video, with title, rounded views, relative date, and length, a row per channel with subscribers, total views, and links, and a free report per source that says whether its list was read to the end.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-youtube-video-channel-scraper": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-youtube-video-channel-scraper"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `scrape_youtube_videos_channels` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "List the last 20 videos from the NASA channel with their views."
- "Search YouTube for home espresso and give me the top 10 videos."
- "How many subscribers does Veritasium have, and what links does the channel publish?"

## Tool

`scrape_youtube_videos_channels`. One tool. Example arguments:

```json
{
  "urls": [
    "https://www.youtube.com/@NASA"
  ],
  "max_videos_per_source": 5
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `urls` | array | no | Channel, @handle, playlist, or search result addresses, or a bare channel ID or @handle. Up to 200 sources a run, counted with search terms. A single video address returns one free row: this actor does not open video pages. Clay users: wrap a column in a one item list. |
| `search_terms` | array | no | Terms to search on YouTube. Each term returns videos in YouTube's order, for a logged out US visitor. Clay users: wrap a column in a one item list. |
| `max_videos_per_source` | number | no | Per channel, playlist, or search term. Default 30, maximum 5000. Set 0 on a channel to get only its channel row. |
| `include_channel_row` | boolean | no | yes (default) adds one row per channel source with subscribers, total views, video count, joined date, country, and links. no skips it. |
| `channel_tab` | string | no | Which channel list to read: videos (default), shorts, or streams. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge that would pass this amount. Reports are always delivered. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `video-row`, one video from a list: title, rounded views, relative date, and length | $0.0012 | $0.00114 | $0.00108 | $0.00102 |
| `channel-row`, one channel | $0.001 | $0.00095 | $0.0009 | $0.00085 |
| `apify-actor-start`, per run start | $0.0025 | $0.0025 | $0.0025 | $0.0025 |

Source reports, refused pages, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/youtube-video-channel-scraper](https://apify.com/mambalabs/youtube-video-channel-scraper)

## License

MIT. See [LICENSE](LICENSE).
