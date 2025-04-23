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
    * File Downloading
    * [Lazy Loading](../lazy-loading/)
    * [Hooks & Auth](../hooks-auth/)
    * [Proxy & Security](../proxy-security/)
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



  * [Download Handling in Crawl4AI](#download-handling-in-crawl4ai)
  * [Enabling Downloads](#enabling-downloads)
  * [Specifying Download Location](#specifying-download-location)
  * [Triggering Downloads](#triggering-downloads)
  * [Accessing Downloaded Files](#accessing-downloaded-files)
  * [Example: Downloading Multiple Files](#example-downloading-multiple-files)
  * [Important Considerations](#important-considerations)



# Download Handling in Crawl4AI

This guide explains how to use Crawl4AI to handle file downloads during crawling. You'll learn how to trigger downloads, specify download locations, and access downloaded files.

## Enabling Downloads

To enable downloads, set the `accept_downloads` parameter in the `BrowserConfig` object and pass it to the crawler.

```
`from crawl4ai.async_configs import BrowserConfig, AsyncWebCrawler async def main(): config = BrowserConfig(accept_downloads=True) # Enable downloads globally async with AsyncWebCrawler(config=config) as crawler: # ... your crawling logic ... asyncio.run(main()) `
```

## Specifying Download Location

Specify the download directory using the `downloads_path` attribute in the `BrowserConfig` object. If not provided, Crawl4AI defaults to creating a "downloads" directory inside the `.crawl4ai` folder in your home directory.

```
`from crawl4ai.async_configs import BrowserConfig import os downloads_path = os.path.join(os.getcwd(), "my_downloads") # Custom download path os.makedirs(downloads_path, exist_ok=True) config = BrowserConfig(accept_downloads=True, downloads_path=downloads_path) async def main(): async with AsyncWebCrawler(config=config) as crawler: result = await crawler.arun(url="https://example.com") # ... `
```

## Triggering Downloads

Downloads are typically triggered by user interactions on a web page, such as clicking a download button. Use `js_code` in `CrawlerRunConfig` to simulate these actions and `wait_for` to allow sufficient time for downloads to start.

```
`from crawl4ai.async_configs import CrawlerRunConfig config = CrawlerRunConfig( js_code=""" const downloadLink = document.querySelector('a[href$=".exe"]'); if (downloadLink) { downloadLink.click(); } """, wait_for=5 # Wait 5 seconds for the download to start ) result = await crawler.arun(url="https://www.python.org/downloads/", config=config) `
```

## Accessing Downloaded Files

The `downloaded_files` attribute of the `CrawlResult` object contains paths to downloaded files.

```
`if result.downloaded_files: print("Downloaded files:") for file_path in result.downloaded_files: print(f"- {file_path}") file_size = os.path.getsize(file_path) print(f"- File size: {file_size} bytes") else: print("No files downloaded.") `
```

## Example: Downloading Multiple Files

```
`from crawl4ai.async_configs import BrowserConfig, CrawlerRunConfig import os from pathlib import Path async def download_multiple_files(url: str, download_path: str): config = BrowserConfig(accept_downloads=True, downloads_path=download_path) async with AsyncWebCrawler(config=config) as crawler: run_config = CrawlerRunConfig( js_code=""" const downloadLinks = document.querySelectorAll('a[download]'); for (const link of downloadLinks) { link.click(); // Delay between clicks await new Promise(r => setTimeout(r, 2000)); } """, wait_for=10 # Wait for all downloads to start ) result = await crawler.arun(url=url, config=run_config) if result.downloaded_files: print("Downloaded files:") for file in result.downloaded_files: print(f"- {file}") else: print("No files downloaded.") # Usage download_path = os.path.join(Path.home(), ".crawl4ai", "downloads") os.makedirs(download_path, exist_ok=True) asyncio.run(download_multiple_files("https://www.python.org/downloads/windows/", download_path)) `
```

## Important Considerations

  * **Browser Context:** Downloads are managed within the browser context. Ensure `js_code` correctly targets the download triggers on the webpage.
  * **Timing:** Use `wait_for` in `CrawlerRunConfig` to manage download timing.
  * **Error Handling:** Handle errors to manage failed downloads or incorrect paths gracefully.
  * **Security:** Scan downloaded files for potential security threats before use.



This revised guide ensures consistency with the `Crawl4AI` codebase by using `BrowserConfig` and `CrawlerRunConfig` for all download-related configurations. Let me know if further adjustments are needed!

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
