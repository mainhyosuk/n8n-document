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
    * [AsyncWebCrawler](../async-webcrawler/)
    * [arun()](../arun/)
    * arun_many()
    * [Browser, Crawler & LLM Config](../parameters/)
    * [CrawlResult](../crawl-result/)
    * [Strategies](../strategies/)



  * [arun_many(...) Reference](#arun_many-reference)
  * [Function Signature](#function-signature)
  * [Differences from arun()](#differences-from-arun)
  * [Dispatcher Reference](#dispatcher-reference)
  * [Common Pitfalls](#common-pitfalls)
  * [Conclusion](#conclusion)



# `arun_many(...)` Reference

> **Note** : This function is very similar to [`arun()`](../arun/) but focused on **concurrent** or **batch** crawling. If you’re unfamiliar with `arun()` usage, please read that doc first, then review this for differences.

## Function Signature

```
`async def arun_many( urls: Union[List[str], List[Any]], config: Optional[CrawlerRunConfig] = None, dispatcher: Optional[BaseDispatcher] = None, ... ) -> Union[List[CrawlResult], AsyncGenerator[CrawlResult, None]]: """ Crawl multiple URLs concurrently or in batches. :param urls: A list of URLs (or tasks) to crawl. :param config: (Optional) A default `CrawlerRunConfig` applying to each crawl. :param dispatcher: (Optional) A concurrency controller (e.g. MemoryAdaptiveDispatcher). ... :return: Either a list of `CrawlResult` objects, or an async generator if streaming is enabled. """ `
```

## Differences from `arun()`

1. **Multiple URLs** : 

  * Instead of crawling a single URL, you pass a list of them (strings or tasks). 
  * The function returns either a **list** of `CrawlResult` or an **async generator** if streaming is enabled.



2. **Concurrency & Dispatchers**: 

  * **`dispatcher`** param allows advanced concurrency control. 
  * If omitted, a default dispatcher (like `MemoryAdaptiveDispatcher`) is used internally. 
  * Dispatchers handle concurrency, rate limiting, and memory-based adaptive throttling (see [Multi-URL Crawling](../../advanced/multi-url-crawling/)).



3. **Streaming Support** : 

  * Enable streaming by setting `stream=True` in your `CrawlerRunConfig`.
  * When streaming, use `async for` to process results as they become available.
  * Ideal for processing large numbers of URLs without waiting for all to complete.



4. **Parallel** Execution**: 

  * `arun_many()` can run multiple requests concurrently under the hood. 
  * Each `CrawlResult` might also include a **`dispatch_result`** with concurrency details (like memory usage, start/end times).



### Basic Example (Batch Mode)

```
`# Minimal usage: The default dispatcher will be used results = await crawler.arun_many( urls=["https://site1.com", "https://site2.com"], config=CrawlerRunConfig(stream=False) # Default behavior ) for res in results: if res.success: print(res.url, "crawled OK!") else: print("Failed:", res.url, "-", res.error_message) `
```

### Streaming Example

```
`config = CrawlerRunConfig( stream=True, # Enable streaming mode cache_mode=CacheMode.BYPASS ) # Process results as they complete async for result in await crawler.arun_many( urls=["https://site1.com", "https://site2.com", "https://site3.com"], config=config ): if result.success: print(f"Just completed: {result.url}") # Process each result immediately process_result(result) `
```

### With a Custom Dispatcher

```
`dispatcher = MemoryAdaptiveDispatcher( memory_threshold_percent=70.0, max_session_permit=10 ) results = await crawler.arun_many( urls=["https://site1.com", "https://site2.com", "https://site3.com"], config=my_run_config, dispatcher=dispatcher ) `
```

**Key Points** : - Each URL is processed by the same or separate sessions, depending on the dispatcher’s strategy. - `dispatch_result` in each `CrawlResult` (if using concurrency) can hold memory and timing info. - If you need to handle authentication or session IDs, pass them in each individual task or within your run config.

### Return Value

Either a **list** of [`CrawlResult`](../crawl-result/) objects, or an **async generator** if streaming is enabled. You can iterate to check `result.success` or read each item’s `extracted_content`, `markdown`, or `dispatch_result`.

## Dispatcher Reference

  * **`MemoryAdaptiveDispatcher`** : Dynamically manages concurrency based on system memory usage. 
  * **`SemaphoreDispatcher`** : Fixed concurrency limit, simpler but less adaptive. 



For advanced usage or custom settings, see [Multi-URL Crawling with Dispatchers](../../advanced/multi-url-crawling/).

## Common Pitfalls

1. **Large Lists** : If you pass thousands of URLs, be mindful of memory or rate-limits. A dispatcher can help. 

2. **Session Reuse** : If you need specialized logins or persistent contexts, ensure your dispatcher or tasks handle sessions accordingly. 

3. **Error Handling** : Each `CrawlResult` might fail for different reasons—always check `result.success` or the `error_message` before proceeding.

## Conclusion

Use `arun_many()` when you want to **crawl multiple URLs** simultaneously or in controlled parallel tasks. If you need advanced concurrency features (like memory-based adaptive throttling or complex rate-limiting), provide a **dispatcher**. Each result is a standard `CrawlResult`, possibly augmented with concurrency stats (`dispatch_result`) for deeper inspection. For more details on concurrency logic and dispatchers, see the [Advanced Multi-URL Crawling](../../advanced/multi-url-crawling/) docs.

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
