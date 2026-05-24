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
playwright install chromium
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
| `timeout` | `int` | `60000` | Default navigation timeout (ms) |
| `slow_mo` | `int` | `50` | Milliseconds to wait between actions (helps avoid detection) |
| `viewport` | `dict` | `{"width": 1280, "height": 800}` | Browser viewport size |
| `locale` | `str` | `None` | Browser locale (e.g. `"en-US"`) |
| `ignore_https_errors` | `bool` | `False` | Ignore HTTPS/SSL certificate errors |

> **Personal note:** Bumped the default `timeout` from 30000 to 60000 ms — 30s was too aggressive for slower sites I was scraping.

> **Personal note:** Added `slow_mo=50` as my default — found that firing actions too fast was triggering rate limits on a few sites. 50ms feels like a good balance between speed and looking human.

> **Personal note:** Changed default `viewport` to `{"width": 1920, "height": 1080}` in my local config — more sites seem to expect a full HD viewport and the 1280x800 default was occasionally triggering responsive layouts that broke my selectors.
