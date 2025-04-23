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



  * [🚀 Crawl4AI 0.4.2 Update: Smarter Crawling Just Got Easier (Dec 12, 2024)](#crawl4ai-042-update-smarter-crawling-just-got-easier-dec-12-2024)
  * [Hey Developers,](#hey-developers)
  * [🔧 Configurable Browser and Crawler Behavior](#configurable-browser-and-crawler-behavior)
  * [🔐 Streamlined Session Management](#streamlined-session-management)
  * [🔢 Handling Large Pages: Supercharged Screenshots and PDF Conversion](#handling-large-pages-supercharged-screenshots-and-pdf-conversion)
  * [🔧 Other Cool Stuff](#other-cool-stuff)
  * [📊 Performance Boosts and Dev-friendly Updates](#performance-boosts-and-dev-friendly-updates)
  * [🔠 Use Cases You’ll Love](#use-cases-youll-love)
  * [Let’s Get Crawling](#lets-get-crawling)



## 🚀 Crawl4AI 0.4.2 Update: Smarter Crawling Just Got Easier (Dec 12, 2024)

### Hey Developers,

I’m excited to share Crawl4AI 0.4.2—a major upgrade that makes crawling smarter, faster, and a whole lot more intuitive. I’ve packed in a bunch of new features to simplify your workflows and improve your experience. Let’s cut to the chase!

### 🔧 **Configurable Browser and Crawler Behavior**

You’ve asked for better control over how browsers and crawlers are configured, and now you’ve got it. With the new `BrowserConfig` and `CrawlerRunConfig` objects, you can set up your browser and crawling behavior exactly how you want. No more cluttering `arun` with a dozen arguments—just pass in your configs and go.

**Example:**

```
`from crawl4ai import BrowserConfig, CrawlerRunConfig, AsyncWebCrawler browser_config = BrowserConfig(headless=True, viewport_width=1920, viewport_height=1080) crawler_config = CrawlerRunConfig(cache_mode="BYPASS") async with AsyncWebCrawler(config=browser_config) as crawler: result = await crawler.arun(url="https://example.com", config=crawler_config) print(result.markdown[:500]) `
```

This setup is a game-changer for scalability, keeping your code clean and flexible as we add more parameters in the future.

Remember: If you like to use the old way, you can still pass arguments directly to `arun` as before, no worries!

### 🔐 **Streamlined Session Management**

Here’s the big one: You can now pass local storage and cookies directly. Whether it’s setting values programmatically or importing a saved JSON state, managing sessions has never been easier. This is a must-have for authenticated crawls—just export your storage state once and reuse it effortlessly across runs.

**Example:** 1. Open a browser, log in manually, and export the storage state. 2. Import the JSON file for seamless authenticated crawling:

```
`result = await crawler.arun( url="https://example.com/protected", storage_state="my_storage_state.json" ) `
```

### 🔢 **Handling Large Pages: Supercharged Screenshots and PDF Conversion**

Two big upgrades here:

  * **Blazing-fast long-page screenshots** : Turn extremely long web pages into clean, high-quality screenshots—without breaking a sweat. It’s optimized to handle large content without lag.

  * **Full-page PDF exports** : Now, you can also convert any page into a PDF with all the details intact. Perfect for archiving or sharing complex layouts.




### 🔧 **Other Cool Stuff**

  * **Anti-bot enhancements** : Magic mode now handles overlays, user simulation, and anti-detection features like a pro.
  * **JavaScript execution** : Execute custom JS snippets to handle dynamic content. No more wrestling with endless page interactions.



### 📊 **Performance Boosts and Dev-friendly Updates**

  * Faster rendering and viewport adjustments for better performance.
  * Improved cookie and local storage handling for seamless authentication.
  * Better debugging with detailed logs and actionable error messages.



### 🔠 **Use Cases You’ll Love**

1. **Authenticated Crawls** : Login once, export your storage state, and reuse it across multiple requests without the headache. 2. **Long-page Screenshots** : Perfect for blogs, e-commerce pages, or any endless-scroll website. 3. **PDF Export** : Create professional-looking page PDFs in seconds.

### Let’s Get Crawling

Crawl4AI 0.4.2 is ready for you to download and try. I’m always looking for ways to improve, so don’t hold back—share your thoughts and feedback.

Happy Crawling! 🚀

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
