[Crawl4AI Documentation (v0.5.x)](https://docs.crawl4ai.com/)

  * [ Home ](../..)
  * [ Quick Start ](../quickstart/)
  * [ Search ](#)



  * [Home](../..)
  * Setup & Installation
    * [Installation](../installation/)
    * [Docker Deployment](../docker-deployment/)
  * [Quick Start](../quickstart/)
  * Blog & Changelog
    * [Blog Home](../../blog/)
    * [Changelog](https://github.com/unclecode/crawl4ai/blob/main/CHANGELOG.md)
  * Core
    * [Command Line Interface](../cli/)
    * Simple Crawling
    * [Deep Crawling](../deep-crawling/)
    * [Crawler Result](../crawler-result/)
    * [Browser, Crawler & LLM Config](../browser-crawler-config/)
    * [Markdown Generation](../markdown-generation/)
    * [Fit Markdown](../fit-markdown/)
    * [Page Interaction](../page-interaction/)
    * [Content Selection](../content-selection/)
    * [Cache Modes](../cache-modes/)
    * [Local Files & Raw HTML](../local-files/)
    * [Link & Media](../link-media/)
  * Advanced
    * [Overview](../../advanced/advanced-features/)
    * [File Downloading](../../advanced/file-downloading/)
    * [Lazy Loading](../../advanced/lazy-loading/)
    * [Hooks & Auth](../../advanced/hooks-auth/)
    * [Proxy & Security](../../advanced/proxy-security/)
    * [Session Management](../../advanced/session-management/)
    * [Multi-URL Crawling](../../advanced/multi-url-crawling/)
    * [Crawl Dispatcher](../../advanced/crawl-dispatcher/)
    * [Identity Based Crawling](../../advanced/identity-based-crawling/)
    * [SSL Certificate](../../advanced/ssl-certificate/)
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



  * [Simple Crawling](#simple-crawling)
  * [Basic Usage](#basic-usage)
  * [Understanding the Response](#understanding-the-response)
  * [Adding Basic Options](#adding-basic-options)
  * [Handling Errors](#handling-errors)
  * [Logging and Debugging](#logging-and-debugging)
  * [Complete Example](#complete-example)



# Simple Crawling

This guide covers the basics of web crawling with Crawl4AI. You'll learn how to set up a crawler, make your first request, and understand the response.

## Basic Usage

Set up a simple crawl using `BrowserConfig` and `CrawlerRunConfig`:

```
`import asyncio from crawl4ai import AsyncWebCrawler from crawl4ai.async_configs import BrowserConfig, CrawlerRunConfig async def main(): browser_config = BrowserConfig() # Default browser configuration run_config = CrawlerRunConfig() # Default crawl run configuration async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun( url="https://example.com", config=run_config ) print(result.markdown) # Print clean markdown content if __name__ == "__main__": asyncio.run(main()) `
```

## Understanding the Response

The `arun()` method returns a `CrawlResult` object with several useful properties. Here's a quick overview (see [CrawlResult](../../api/crawl-result/) for complete details):

```
`result = await crawler.arun( url="https://example.com", config=CrawlerRunConfig(fit_markdown=True) ) # Different content formats print(result.html) # Raw HTML print(result.cleaned_html) # Cleaned HTML print(result.markdown.raw_markdown) # Raw markdown from cleaned html print(result.markdown.fit_markdown) # Most relevant content in markdown # Check success status print(result.success) # True if crawl succeeded print(result.status_code) # HTTP status code (e.g., 200, 404) # Access extracted media and links print(result.media) # Dictionary of found media (images, videos, audio) print(result.links) # Dictionary of internal and external links `
```

## Adding Basic Options

Customize your crawl using `CrawlerRunConfig`:

```
`run_config = CrawlerRunConfig( word_count_threshold=10, # Minimum words per content block exclude_external_links=True, # Remove external links remove_overlay_elements=True, # Remove popups/modals process_iframes=True # Process iframe content ) result = await crawler.arun( url="https://example.com", config=run_config ) `
```

## Handling Errors

Always check if the crawl was successful:

```
`run_config = CrawlerRunConfig() result = await crawler.arun(url="https://example.com", config=run_config) if not result.success: print(f"Crawl failed: {result.error_message}") print(f"Status code: {result.status_code}") `
```

## Logging and Debugging

Enable verbose logging in `BrowserConfig`:

```
`browser_config = BrowserConfig(verbose=True) async with AsyncWebCrawler(config=browser_config) as crawler: run_config = CrawlerRunConfig() result = await crawler.arun(url="https://example.com", config=run_config) `
```

## Complete Example

Here's a more comprehensive example demonstrating common usage patterns:

```
`import asyncio from crawl4ai import AsyncWebCrawler from crawl4ai.async_configs import BrowserConfig, CrawlerRunConfig, CacheMode async def main(): browser_config = BrowserConfig(verbose=True) run_config = CrawlerRunConfig( # Content filtering word_count_threshold=10, excluded_tags=['form', 'header'], exclude_external_links=True, # Content processing process_iframes=True, remove_overlay_elements=True, # Cache control cache_mode=CacheMode.ENABLED # Use cache if available ) async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun( url="https://example.com", config=run_config ) if result.success: # Print clean content print("Content:", result.markdown[:500]) # First 500 chars # Process images for image in result.media["images"]: print(f"Found image: {image['src']}") # Process links for link in result.links["internal"]: print(f"Internal link: {link['href']}") else: print(f"Crawl failed: {result.error_message}") if __name__ == "__main__": asyncio.run(main()) `
```

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
