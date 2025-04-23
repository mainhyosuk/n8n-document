[Crawl4AI Documentation (v0.5.x)](https://docs.crawl4ai.com/)

  * [ Home ](../..)
  * [ Quick Start ](../../core/quickstart/)
  * [ Search ](#)



  * [Home](../..)
  * Setup & Installation
    * [Installation](../../core/installation/)
    * [Docker Deployment](../../core/docker-deployment/)
  * [Quick Start](../../core/quickstart/)
  * Blog & Changelog
    * [Blog Home](../../blog/)
    * [Changelog](https://github.com/unclecode/crawl4ai/blob/main/CHANGELOG.md)
  * Core
    * [Command Line Interface](../../core/cli/)
    * [Simple Crawling](../../core/simple-crawling/)
    * [Deep Crawling](../../core/deep-crawling/)
    * [Crawler Result](../../core/crawler-result/)
    * [Browser, Crawler & LLM Config](../../core/browser-crawler-config/)
    * [Markdown Generation](../../core/markdown-generation/)
    * [Fit Markdown](../../core/fit-markdown/)
    * [Page Interaction](../../core/page-interaction/)
    * [Content Selection](../../core/content-selection/)
    * [Cache Modes](../../core/cache-modes/)
    * [Local Files & Raw HTML](../../core/local-files/)
    * [Link & Media](../../core/link-media/)
  * Advanced
    * [Overview](../advanced-features/)
    * [File Downloading](../file-downloading/)
    * [Lazy Loading](../lazy-loading/)
    * [Hooks & Auth](../hooks-auth/)
    * Proxy & Security
    * [Session Management](../session-management/)
    * [Multi-URL Crawling](../multi-url-crawling/)
    * [Crawl Dispatcher](../crawl-dispatcher/)
    * [Identity Based Crawling](../identity-based-crawling/)
    * [SSL Certificate](../ssl-certificate/)
  * Extraction
    * [LLM-Free Strategies](../../extraction/no-llm-strategies/)
    * [LLM Strategies](../../extraction/llm-strategies/)
    * [Clustering Strategies](../../extraction/clustring-strategies/)
    * [Chunking](../../extraction/chunking/)
  * API Reference
    * [AsyncWebCrawler](../../api/async-webcrawler/)
    * [arun()](../../api/arun/)
    * [arun_many()](../../api/arun_many/)
    * [Browser, Crawler & LLM Config](../../api/parameters/)
    * [CrawlResult](../../api/crawl-result/)
    * [Strategies](../../api/strategies/)



  * [Proxy](#proxy)
  * [Basic Proxy Setup](#basic-proxy-setup)
  * [Authenticated Proxy](#authenticated-proxy)
  * [Rotating Proxies](#rotating-proxies)



# Proxy

## Basic Proxy Setup

Simple proxy configuration with `BrowserConfig`:

```
`from crawl4ai.async_configs import BrowserConfig # Using proxy URL browser_config = BrowserConfig(proxy="http://proxy.example.com:8080") async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun(url="https://example.com") # Using SOCKS proxy browser_config = BrowserConfig(proxy="socks5://proxy.example.com:1080") async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun(url="https://example.com") `
```

## Authenticated Proxy

Use an authenticated proxy with `BrowserConfig`:

```
`from crawl4ai.async_configs import BrowserConfig proxy_config = { "server": "http://proxy.example.com:8080", "username": "user", "password": "pass" } browser_config = BrowserConfig(proxy_config=proxy_config) async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun(url="https://example.com") `
```

Here's the corrected documentation:

## Rotating Proxies

Example using a proxy rotation service dynamically:

```
`from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig async def get_next_proxy(): # Your proxy rotation logic here return {"server": "http://next.proxy.com:8080"} async def main(): browser_config = BrowserConfig() run_config = CrawlerRunConfig() async with AsyncWebCrawler(config=browser_config) as crawler: # For each URL, create a new run config with different proxy for url in urls: proxy = await get_next_proxy() # Clone the config and update proxy - this creates a new browser context current_config = run_config.clone(proxy_config=proxy) result = await crawler.arun(url=url, config=current_config) if __name__ == "__main__": import asyncio asyncio.run(main()) `
```

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
