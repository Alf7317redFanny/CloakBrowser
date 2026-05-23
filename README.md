# CloakBrowser

> A privacy-focused browser automation and scraping tool — Fork of [CloakHQ/CloakBrowser](https://github.com/CloakHQ/CloakBrowser)

[![CI](https://github.com/your-org/CloakBrowser/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/CloakBrowser/actions/workflows/ci.yml)
[![PyPI version](https://badge.fury.io/py/cloakbrowser.svg)](https://badge.fury.io/py/cloakbrowser)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

CloakBrowser is a Python library that provides a stealth-capable browser automation interface built on top of Playwright. It helps bypass common bot detection mechanisms while giving you a clean API for browser automation tasks.

## Features

- 🕵️ Stealth mode — evades common fingerprinting and bot detection
- 🔄 Automatic browser profile rotation
- 🌐 Proxy support (HTTP, SOCKS5)
- 📸 Screenshot and PDF capture
- 🍪 Cookie and session management
- ⚡ Async-first API
- 🧩 Playwright-compatible interface

## Installation

```bash
pip install cloakbrowser
```

Then install the browser binaries:

```bash
playwrightinstall chromium
```

## Quick Start

```python
import asyncio
from cloakbrowser import CloakBrowser

async def main():
    async with CloakBrowser() as browser:
        page = await browser.new_page()
        await page.goto("https://example.com")
        title = await page.title()
        print(f"Page title: {title}")
        await page.screenshot(path="screenshot.png")

asyncio.run(main())
```

## Usage with Proxy

```python
from cloakbrowser import CloakBrowser, ProxyConfig

async def main():
    proxy = ProxyConfig(
        server="socks5://proxy.example.com:1080",
        username="user",
        password="pass"
    )

    async with CloakBrowser(proxy=proxy) as browser:
        page = await browser.new_page()
        await page.goto("https://httpbin.org/ip")
        print(await page.content())
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `headless` | `bool` | `True` | Run browser in headless mode |
| `stealth` | `bool` | `True` | Enable stealth mode |
| `proxy` | `ProxyConfig` | `None` | Proxy configuration |
| `user_agent` | `str` | auto | Custom user agent string |
| `timeout` | `int` | `30000` | Default navigation timeout (ms) |

## Development

```bash
# Clone the repo
git clone https://github.com/your-org/CloakBrowser.git
cd CloakBrowser

# Install dev dependencies
pip install -e ".[dev]"

# Run tests
pytest

# Lint
ruff check .
```

## Contributing

Pull requests are welcome! Please open an issue first to discuss what you'd like to change.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT — see [LICENSE](LICENSE) for details.

## Acknowledgements

- Original project: [CloakHQ/CloakBrowser](https://github.com/CloakHQ/CloakBrowser)
- Built on [Playwright for Python](https://playwright.dev/python/)
- Stealth patches inspired by [playwright-stealth](https://github.com/AtuboDad/playwright_stealth)
