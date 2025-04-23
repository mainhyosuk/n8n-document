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
    * Lazy Loading
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



  * [Handling Lazy-Loaded Images](#handling-lazy-loaded-images)
  * [Example: Ensuring Lazy Images Appear](#example-ensuring-lazy-images-appear)
  * [Combining with Other Link & Media Filters](#combining-with-other-link-media-filters)
  * [Tips & Troubleshooting](#tips-troubleshooting)



## Handling Lazy-Loaded Images

Many websites now load images **lazily** as you scroll. If you need to ensure they appear in your final crawl (and in `result.media`), consider:

1. **`wait_for_images=True`** – Wait for images to fully load. 2. **`scan_full_page`** – Force the crawler to scroll the entire page, triggering lazy loads. 3. **`scroll_delay`** – Add small delays between scroll steps. 

**Note** : If the site requires multiple “Load More” triggers or complex interactions, see the [Page Interaction docs](../../core/page-interaction/).

### Example: Ensuring Lazy Images Appear

```
`import asyncio from crawl4ai import AsyncWebCrawler, CrawlerRunConfig, BrowserConfig from crawl4ai.async_configs import CacheMode async def main(): config = CrawlerRunConfig( # Force the crawler to wait until images are fully loaded wait_for_images=True, # Option 1: If you want to automatically scroll the page to load images scan_full_page=True, # Tells the crawler to try scrolling the entire page scroll_delay=0.5, # Delay (seconds) between scroll steps # Option 2: If the site uses a 'Load More' or JS triggers for images, # you can also specify js_code or wait_for logic here. cache_mode=CacheMode.BYPASS, verbose=True ) async with AsyncWebCrawler(config=BrowserConfig(headless=True)) as crawler: result = await crawler.arun("https://www.example.com/gallery", config=config) if result.success: images = result.media.get("images", []) print("Images found:", len(images)) for i, img in enumerate(images[:5]): print(f"[Image {i}] URL: {img['src']}, Score: {img.get('score','N/A')}") else: print("Error:", result.error_message) if __name__ == "__main__": asyncio.run(main()) `
```

**Explanation** :

  * **`wait_for_images=True`** The crawler tries to ensure images have finished loading before finalizing the HTML. 
  * **`scan_full_page=True`** Tells the crawler to attempt scrolling from top to bottom. Each scroll step helps trigger lazy loading. 
  * **`scroll_delay=0.5`** Pause half a second between each scroll step. Helps the site load images before continuing.



**When to Use** :

  * **Lazy-Loading** : If images appear only when the user scrolls into view, `scan_full_page` + `scroll_delay` helps the crawler see them. 
  * **Heavier Pages** : If a page is extremely long, be mindful that scanning the entire page can be slow. Adjust `scroll_delay` or the max scroll steps as needed.



## Combining with Other Link & Media Filters

You can still combine **lazy-load** logic with the usual **exclude_external_images** , **exclude_domains** , or link filtration:

```
`config = CrawlerRunConfig( wait_for_images=True, scan_full_page=True, scroll_delay=0.5, # Filter out external images if you only want local ones exclude_external_images=True, # Exclude certain domains for links exclude_domains=["spammycdn.com"], ) `
```

This approach ensures you see **all** images from the main domain while ignoring external ones, and the crawler physically scrolls the entire page so that lazy-loading triggers.

## Tips & Troubleshooting

1. **Long Pages** - Setting `scan_full_page=True` on extremely long or infinite-scroll pages can be resource-intensive. - Consider using [hooks](../../core/page-interaction/) or specialized logic to load specific sections or “Load More” triggers repeatedly.

2. **Mixed Image Behavior** - Some sites load images in batches as you scroll. If you’re missing images, increase your `scroll_delay` or call multiple partial scrolls in a loop with JS code or hooks.

3. **Combining with Dynamic Wait** - If the site has a placeholder that only changes to a real image after a certain event, you might do `wait_for="css:img.loaded"` or a custom JS `wait_for`.

4. **Caching** - If `cache_mode` is enabled, repeated crawls might skip some network fetches. If you suspect caching is missing new images, set `cache_mode=CacheMode.BYPASS` for fresh fetches.

With **lazy-loading** support, **wait_for_images** , and **scan_full_page** settings, you can capture the entire gallery or feed of images you expect—even if the site only loads them as the user scrolls. Combine these with the standard media filtering and domain exclusion for a complete link & media handling strategy.

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
