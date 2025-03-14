# nostreads

A Nostr-native service for crawling and publishing web content in a readable, long-form format (NIP-23 events).
Users can interact with a bot directly on Nostr to request URL crawls or use an optional web interface for additional features.

---

## Concept

- **Bot-First Approach**:
  - Users send requests (DM or mention) to the bot with a URL.
  - The bot crawls the page, extracts main content, and publishes a NIP-23 event.
  - The event is accessible on any relay the bot posts to.

- **Optional Web Frontend**:
  - Provides filtering, searching, customizable reading views, and future advanced features like AI summaries or paywall handling.

---

## Architecture

```
nostreads/
├─ cmd/
│   ├─ server/
│   │   └─ server.go     (Backend / API)
│   └─ bot/
│       └─ bot.go        (Bot entry point)
├─ internal/
│   ├─ crawler/          (Crawling & readability extraction)
│   └─ nostr/            (NIP-23 publishing, relay interaction)
└─ web/
├─ svelte/           (Source for the optional frontend)
└─ dist/             (Compiled frontend assets)
```
1. **Bot**: Listens on relays for commands, fetches and parses content, then publishes it in readable format.
2. **Server**: Provides an HTTP API for crawling or advanced indexing. The web UI interacts with this API.
3. **Crawler**: Handles URL fetching, HTML parsing, and readability extraction.
4. **Nostr Integration**: Creates and signs NIP-23 events and communicates with relays.

---

## Prototype Status

- **Core Features**:
  - Basic bot that receives “crawl [URL]” requests and posts results as NIP-23 events.
  - Simple crawler module for extracting text.
  - Early server scaffolding for future features or a custom front end.

- **Future Enhancements**:
  - Paywall detection (currently returns a message if paywalled).
  - Offline reading, advanced filtering, AI summaries.
  - Synchronizing user preferences (fonts, color scheme) via Nostr events or local storage.

---

## Getting Started

1. **Clone & Setup**
   ```bash
   git clone https://github.com/<yourusername>/nostreads.git
   cd nostreads
   go mod tidy
    ```
	2.	Run the Bot
    ```bash
    go run ./cmd/bot
    ```

	3.	Run the Server
    ```bash
    go run ./cmd/server
    ```

	4.	(Optional) Build Frontend
    ```bash
    cd web/svelte
    npm install
    npm run build
    ```
