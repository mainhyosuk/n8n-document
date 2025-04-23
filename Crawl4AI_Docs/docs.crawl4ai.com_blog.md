[Crawl4AI Documentation (v0.5.x)](https://docs.crawl4ai.com/)

  * [ Home ](..)
  * [ Quick Start ](../core/quickstart/)
  * [ Search ](#)



  * [Home](..)
  * Setup & Installation
    * [Installation](../core/installation/)
    * [Docker Deployment](../core/docker-deployment/)
  * [Quick Start](../core/quickstart/)
  * Blog & Changelog
    * Blog Home
    * [Changelog](https://github.com/unclecode/crawl4ai/blob/main/CHANGELOG.md)
  * Core
    * [Command Line Interface](../core/cli/)
    * [Simple Crawling](../core/simple-crawling/)
    * [Deep Crawling](../core/deep-crawling/)
    * [Crawler Result](../core/crawler-result/)
    * [Browser, Crawler & LLM Config](../core/browser-crawler-config/)
    * [Markdown Generation](../core/markdown-generation/)
    * [Fit Markdown](../core/fit-markdown/)
    * [Page Interaction](../core/page-interaction/)
    * [Content Selection](../core/content-selection/)
    * [Cache Modes](../core/cache-modes/)
    * [Local Files & Raw HTML](../core/local-files/)
    * [Link & Media](../core/link-media/)
  * Advanced
    * [Overview](../advanced/advanced-features/)
    * [File Downloading](../advanced/file-downloading/)
    * [Lazy Loading](../advanced/lazy-loading/)
    * [Hooks & Auth](../advanced/hooks-auth/)
    * [Proxy & Security](../advanced/proxy-security/)
    * [Session Management](../advanced/session-management/)
    * [Multi-URL Crawling](../advanced/multi-url-crawling/)
    * [Crawl Dispatcher](../advanced/crawl-dispatcher/)
    * [Identity Based Crawling](../advanced/identity-based-crawling/)
    * [SSL Certificate](../advanced/ssl-certificate/)
  * Extraction
    * [LLM-Free Strategies](../extraction/no-llm-strategies/)
    * [LLM Strategies](../extraction/llm-strategies/)
    * [Clustering Strategies](../extraction/clustring-strategies/)
    * [Chunking](../extraction/chunking/)
  * API Reference
    * [AsyncWebCrawler](../api/async-webcrawler/)
    * [arun()](../api/arun/)
    * [arun_many()](../api/arun_many/)
    * [Browser, Crawler & LLM Config](../api/parameters/)
    * [CrawlResult](../api/crawl-result/)
    * [Strategies](../api/strategies/)



  * [Crawl4AI Blog](#crawl4ai-blog)
  * [Latest Release](#latest-release)
  * [License Change](#license-change)
  * [Project History](#project-history)
  * [Stay Updated](#stay-updated)



# Crawl4AI Blog

Welcome to the Crawl4AI blog! Here you'll find detailed release notes, technical insights, and updates about the project. Whether you're looking for the latest improvements or want to dive deep into web crawling techniques, this is the place.

## Latest Release

### [Crawl4AI v0.5.0: Deep Crawling, Scalability, and a New CLI!](releases/0.5.0/)

My dear friends and crawlers, there you go, this is the release of Crawl4AI v0.5.0! This release brings a wealth of new features, performance improvements, and a more streamlined developer experience. Here's a breakdown of what's new:

**Major New Features:**

  * **Deep Crawling:** Explore entire websites with configurable strategies (BFS, DFS, Best-First). Define custom filters and URL scoring for targeted crawls.
  * **Memory-Adaptive Dispatcher:** Handle large-scale crawls with ease! Our new dispatcher dynamically adjusts concurrency based on available memory and includes built-in rate limiting.
  * **Multiple Crawler Strategies:** Choose between the full-featured Playwright browser-based crawler or a new, _much_ faster HTTP-only crawler for simpler tasks.
  * **Docker Deployment:** Deploy Crawl4AI as a scalable, self-contained service with built-in API endpoints and optional JWT authentication.
  * **Command-Line Interface (CLI):** Interact with Crawl4AI directly from your terminal. Crawl, configure, and extract data with simple commands.
  * **LLM Configuration (`LLMConfig`):** A new, unified way to configure LLM providers (OpenAI, Anthropic, Ollama, etc.) for extraction, filtering, and schema generation. Simplifies API key management and switching between models.



**Minor Updates & Improvements:**

  * **LXML Scraping Mode:** Faster HTML parsing with `LXMLWebScrapingStrategy`.
  * **Proxy Rotation:** Added `ProxyRotationStrategy` with a `RoundRobinProxyStrategy` implementation.
  * **PDF Processing:** Extract text, images, and metadata from PDF files.
  * **URL Redirection Tracking:** Automatically follows and records redirects.
  * **Robots.txt Compliance:** Optionally respect website crawling rules.
  * **LLM-Powered Schema Generation:** Automatically create extraction schemas using an LLM.
  * **`LLMContentFilter`:** Generate high-quality, focused markdown using an LLM.
  * **Improved Error Handling & Stability:** Numerous bug fixes and performance enhancements.
  * **Enhanced Documentation:** Updated guides and examples.



**Breaking Changes & Migration:**

This release includes several breaking changes to improve the library's structure and consistency. Here's what you need to know:

  * **`arun_many()` Behavior:** Now uses the `MemoryAdaptiveDispatcher` by default. The return type depends on the `stream` parameter in `CrawlerRunConfig`. Adjust code that relied on unbounded concurrency.
  * **`max_depth` Location:** Moved to `CrawlerRunConfig` and now controls _crawl depth_.
  * **Deep Crawling Imports:** Import `DeepCrawlStrategy` and related classes from `crawl4ai.deep_crawling`.
  * **`BrowserContext` API:** Updated; the old `get_context` method is deprecated.
  * **Optional Model Fields:** Many data model fields are now optional. Handle potential `None` values.
  * **`ScrapingMode` Enum:** Replaced with strategy pattern (`WebScrapingStrategy`, `LXMLWebScrapingStrategy`).
  * **`content_filter` Parameter:** Removed from `CrawlerRunConfig`. Use extraction strategies or markdown generators with filters.
  * **Removed Functionality:** The synchronous `WebCrawler`, the old CLI, and docs management tools have been removed.
  * **Docker:** Significant changes to deployment. See the [Docker documentation](../deploy/docker/README.md).
  * **`ssl_certificate.json`:** This file has been removed.
  * **Config** : FastFilterChain has been replaced with FilterChain
  * **Deep-Crawl** : DeepCrawlStrategy.arun now returns Union[CrawlResultT, List[CrawlResultT], AsyncGenerator[CrawlResultT, None]]
  * **Proxy** : Removed synchronous WebCrawler support and related rate limiting configurations
  * **LLM Parameters:** Use the new `LLMConfig` object instead of passing `provider`, `api_token`, `base_url`, and `api_base` directly to `LLMExtractionStrategy` and `LLMContentFilter`.



**In short:** Update imports, adjust `arun_many()` usage, check for optional fields, and review the Docker deployment guide.

## License Change

Crawl4AI v0.5.0 updates the license to Apache 2.0 _with a required attribution clause_. This means you are free to use, modify, and distribute Crawl4AI (even commercially), but you _must_ clearly attribute the project in any public use or distribution. See the updated `LICENSE` file for the full legal text and specific requirements.

**Get Started:**

  * **Installation:** `pip install "crawl4ai[all]"` (or use the Docker image)
  * **Documentation:** <https://docs.crawl4ai.com>
  * **GitHub:** <https://github.com/unclecode/crawl4ai>



I'm very excited to see what you build with Crawl4AI v0.5.0!

### [0.4.2 - Configurable Crawlers, Session Management, and Smarter Screenshots](releases/0.4.2/)

_December 12, 2024_

The 0.4.2 update brings massive improvements to configuration, making crawlers and browsers easier to manage with dedicated objects. You can now import/export local storage for seamless session management. Plus, long-page screenshots are faster and cleaner, and full-page PDF exports are now possible. Check out all the new features to make your crawling experience even smoother.

[Read full release notes →](releases/0.4.2/)

### [0.4.1 - Smarter Crawling with Lazy-Load Handling, Text-Only Mode, and More](releases/0.4.1/)

_December 8, 2024_

This release brings major improvements to handling lazy-loaded images, a blazing-fast Text-Only Mode, full-page scanning for infinite scrolls, dynamic viewport adjustments, and session reuse for efficient crawling. If you're looking to improve speed, reliability, or handle dynamic content with ease, this update has you covered.

[Read full release notes →](releases/0.4.1/)

### [0.4.0 - Major Content Filtering Update](releases/0.4.0/)

_December 1, 2024_

Introduced significant improvements to content filtering, multi-threaded environment handling, and user-agent generation. This release features the new PruningContentFilter, enhanced thread safety, and improved test coverage.

[Read full release notes →](releases/0.4.0/)

## Project History

Curious about how Crawl4AI has evolved? Check out our [complete changelog](https://github.com/unclecode/crawl4ai/blob/main/CHANGELOG.md) for a detailed history of all versions and updates.

## Stay Updated

  * Star us on [GitHub](https://github.com/unclecode/crawl4ai)
  * Follow [@unclecode](https://twitter.com/unclecode) on Twitter
  * Join our community discussions on GitHub



Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
