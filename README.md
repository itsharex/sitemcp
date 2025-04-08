# sitemcp

Fetch an entire site and use it as a MCP Server

https://github.com/user-attachments/assets/ebe2d7c6-4ddc-4a37-8e1e-d80fac49d8ae

<details>
  <summary><bold>Demo in Japanese</bold></summary>

https://github.com/user-attachments/assets/24288140-be2a-416c-9e7c-c49be056a373

</details>


> [!NOTE]
> `sitemcp` is a fork of [`sitefetch`](https://github.com/egoist/sitefetch) by [@egoist](https://github.com/egoist)

## Install

One-off usage (choose one of the followings):

```bash
bunx sitemcp
npx sitemcp
pnpx sitemcp
```

Install globally (choose one of the followings):

```bash
bun i -g sitemcp
npm i -g sitemcp
pnpm i -g sitemcp
```

## Usage

```bash
sitemcp https://daisyui.com

# or better concurrency
sitemcp https://daisyui.com --concurrency 10
```

### Match specific pages

Use the `-m, --match` flag to specify the pages you want to fetch:

```bash
sitemcp https://vite.dev -m "/blog/**" -m "/guide/**"
```

The match pattern is tested against the pathname of target pages, powered by micromatch, you can check out all the supported [matching features](https://github.com/micromatch/micromatch#matching-features).

### Content selector

We use [mozilla/readability](https://github.com/mozilla/readability) to extract readable content from the web page, but on some pages it might return irrelevant contents, in this case you can specify a CSS selector so we know where to find the readable content:

```sitemcp
sitemcp https://vite.dev --content-selector ".content"
```

## How to configure with MCP Client

You can execute server from your MCP client (e.g. Claude Desktop).

The below example configuration for Claude Desktop

```json
{
  "mcpServers": {
    "daisy-ui": {
      "command": "npx",
      "args": [
        "-y",
        "sitemcp",
        "https://daisyui.com",
        "-m",
        "/components/**",
      ]
    }
  }
}

```

## Tips

- Some site has a lot of pages. It is better to run `sitemcp` before registering the server to the MCP client. `sitemcp` caches the pages in `~/.cache/sitemcp` by default. You can disable by `--no-cache` flag.

## License

MIT.
