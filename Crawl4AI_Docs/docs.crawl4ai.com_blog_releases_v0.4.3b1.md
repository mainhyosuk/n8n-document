[Crawl4AI Documentation (v0.5.x)](https://docs.crawl4ai.com/)

  * [ Home ](../../..)
  * [ Quick Start ](../../../core/quickstart/)
  * [ Search ](#)



  * [Home](../../..)
  * Setup & Installation
    * [Installation](../../../core/installation/)
    * [Docker Deployment](../../../core/docker-deployment/)
  * [Quick Start](../../../core/quickstart/)
  * Blog & Changelog
    * [Blog Home](../../)
    * [Changelog](https://github.com/unclecode/crawl4ai/blob/main/CHANGELOG.md)
  * Core
    * [Command Line Interface](../../../core/cli/)
    * [Simple Crawling](../../../core/simple-crawling/)
    * [Deep Crawling](../../../core/deep-crawling/)
    * [Crawler Result](../../../core/crawler-result/)
    * [Browser, Crawler & LLM Config](../../../core/browser-crawler-config/)
    * [Markdown Generation](../../../core/markdown-generation/)
    * [Fit Markdown](../../../core/fit-markdown/)
    * [Page Interaction](../../../core/page-interaction/)
    * [Content Selection](../../../core/content-selection/)
    * [Cache Modes](../../../core/cache-modes/)
    * [Local Files & Raw HTML](../../../core/local-files/)
    * [Link & Media](../../../core/link-media/)
  * Advanced
    * [Overview](../../../advanced/advanced-features/)
    * [File Downloading](../../../advanced/file-downloading/)
    * [Lazy Loading](../../../advanced/lazy-loading/)
    * [Hooks & Auth](../../../advanced/hooks-auth/)
    * [Proxy & Security](../../../advanced/proxy-security/)
    * [Session Management](../../../advanced/session-management/)
    * [Multi-URL Crawling](../../../advanced/multi-url-crawling/)
    * [Crawl Dispatcher](../../../advanced/crawl-dispatcher/)
    * [Identity Based Crawling](../../../advanced/identity-based-crawling/)
    * [SSL Certificate](../../../advanced/ssl-certificate/)
  * Extraction
    * [LLM-Free Strategies](../../../extraction/no-llm-strategies/)
    * [LLM Strategies](../../../extraction/llm-strategies/)
    * [Clustering Strategies](../../../extraction/clustring-strategies/)
    * [Chunking](../../../extraction/chunking/)
  * API Reference
    * [AsyncWebCrawler](../../../api/async-webcrawler/)
    * [arun()](../../../api/arun/)
    * [arun_many()](../../../api/arun_many/)
    * [Browser, Crawler & LLM Config](../../../api/parameters/)
    * [CrawlResult](../../../api/crawl-result/)
    * [Strategies](../../../api/strategies/)



  * [Crawl4AI 0.4.3: Major Performance Boost & LLM Integration](#crawl4ai-043-major-performance-boost-llm-integration)
  * [⚡ Speed & Efficiency Improvements](#speed-efficiency-improvements)
  * [🤖 LLM Integration](#llm-integration)
  * [🔧 Core Improvements](#core-improvements)
  * [Performance Impact](#performance-impact)
  * [Getting Started](#getting-started)
  * [Stay Connected](#stay-connected)



# Crawl4AI 0.4.3: Major Performance Boost & LLM Integration

We're excited to announce Crawl4AI 0.4.3, focusing on three key areas: Speed & Efficiency, LLM Integration, and Core Platform Improvements. This release significantly improves crawling performance while adding powerful new LLM-powered features.

## ⚡ Speed & Efficiency Improvements

### 1. Memory-Adaptive Dispatcher System

The new dispatcher system provides intelligent resource management and real-time monitoring:

```
`from crawl4ai import AsyncWebCrawler, CrawlerRunConfig, DisplayMode from crawl4ai.async_dispatcher import MemoryAdaptiveDispatcher, CrawlerMonitor async def main(): urls = ["https://example1.com", "https://example2.com"] * 50 # Configure memory-aware dispatch dispatcher = MemoryAdaptiveDispatcher( memory_threshold_percent=80.0, # Auto-throttle at 80% memory check_interval=0.5, # Check every 0.5 seconds max_session_permit=20, # Max concurrent sessions monitor=CrawlerMonitor( # Real-time monitoring display_mode=DisplayMode.DETAILED ) ) async with AsyncWebCrawler() as crawler: results = await dispatcher.run_urls( urls=urls, crawler=crawler, config=CrawlerRunConfig() ) `
```

### 2. Streaming Support

Process crawled URLs in real-time instead of waiting for all results:

```
`config = CrawlerRunConfig(stream=True) async with AsyncWebCrawler() as crawler: async for result in await crawler.arun_many(urls, config=config): print(f"Got result for {result.url}") # Process each result immediately `
```

### 3. LXML-Based Scraping

New LXML scraping strategy offering up to 20x faster parsing:

```
`config = CrawlerRunConfig( scraping_strategy=LXMLWebScrapingStrategy(), cache_mode=CacheMode.ENABLED ) `
```

## 🤖 LLM Integration

### 1. LLM-Powered Markdown Generation

Smart content filtering and organization using LLMs:

```
`config = CrawlerRunConfig( markdown_generator=DefaultMarkdownGenerator( content_filter=LLMContentFilter( provider="openai/gpt-4o", instruction="Extract technical documentation and code examples" ) ) ) `
```

### 2. Automatic Schema Generation

Generate extraction schemas instantly using LLMs instead of manual CSS/XPath writing:

```
`schema = JsonCssExtractionStrategy.generate_schema( html_content, schema_type="CSS", query="Extract product name, price, and description" ) `
```

## 🔧 Core Improvements

### 1. Proxy Support & Rotation

Integrated proxy support with automatic rotation and verification:

```
`config = CrawlerRunConfig( proxy_config={ "server": "http://proxy:8080", "username": "user", "password": "pass" } ) `
```

### 2. Robots.txt Compliance

Built-in robots.txt support with SQLite caching:

```
`config = CrawlerRunConfig(check_robots_txt=True) result = await crawler.arun(url, config=config) if result.status_code == 403: print("Access blocked by robots.txt") `
```

### 3. URL Redirection Tracking

Track final URLs after redirects:

```
`result = await crawler.arun(url) print(f"Initial URL: {url}") print(f"Final URL: {result.redirected_url}") `
```

## Performance Impact

  * Memory usage reduced by up to 40% with adaptive dispatcher
  * Parsing speed increased up to 20x with LXML strategy
  * Streaming reduces memory footprint for large crawls by ~60%



## Getting Started

```
`pip install -U crawl4ai `
```

For complete examples, check our [demo repository](https://github.com/unclecode/crawl4ai/examples).

## Stay Connected

  * Star us on [GitHub](https://github.com/unclecode/crawl4ai)
  * Follow [@unclecode](https://twitter.com/unclecode)
  * Join our [Discord](https://discord.gg/crawl4ai)



Happy crawling! 🕷️

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
