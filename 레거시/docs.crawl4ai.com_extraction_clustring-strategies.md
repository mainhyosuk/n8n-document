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
    * [LLM-Free Strategies](../no-llm-strategies/)
    * [LLM Strategies](../llm-strategies/)
    * Clustering Strategies
    * [Chunking](../chunking/)
  * API Reference
    * [AsyncWebCrawler](../../api/async-webcrawler/)
    * [arun()](../../api/arun/)
    * [arun_many()](../../api/arun_many/)
    * [Browser, Crawler & LLM Config](../../api/parameters/)
    * [CrawlResult](../../api/crawl-result/)
    * [Strategies](../../api/strategies/)



  * [Cosine Strategy](#cosine-strategy)
  * [How It Works](#how-it-works)
  * [Basic Usage](#basic-usage)
  * [Configuration Options](#configuration-options)
  * [Use Cases](#use-cases)
  * [Advanced Features](#advanced-features)
  * [Best Practices](#best-practices)
  * [Error Handling](#error-handling)



# Cosine Strategy

The Cosine Strategy in Crawl4AI uses similarity-based clustering to identify and extract relevant content sections from web pages. This strategy is particularly useful when you need to find and extract content based on semantic similarity rather than structural patterns.

## How It Works

The Cosine Strategy: 1. Breaks down page content into meaningful chunks 2. Converts text into vector representations 3. Calculates similarity between chunks 4. Clusters similar content together 5. Ranks and filters content based on relevance

## Basic Usage

```
`from crawl4ai.extraction_strategy import CosineStrategy strategy = CosineStrategy( semantic_filter="product reviews", # Target content type word_count_threshold=10, # Minimum words per cluster sim_threshold=0.3 # Similarity threshold ) async with AsyncWebCrawler() as crawler: result = await crawler.arun( url="https://example.com/reviews", extraction_strategy=strategy ) content = result.extracted_content `
```

## Configuration Options

### Core Parameters

```
`CosineStrategy( # Content Filtering semantic_filter: str = None, # Keywords/topic for content filtering word_count_threshold: int = 10, # Minimum words per cluster sim_threshold: float = 0.3, # Similarity threshold (0.0 to 1.0) # Clustering Parameters max_dist: float = 0.2, # Maximum distance for clustering linkage_method: str = 'ward', # Clustering linkage method top_k: int = 3, # Number of top categories to extract # Model Configuration model_name: str = 'sentence-transformers/all-MiniLM-L6-v2', # Embedding model verbose: bool = False # Enable logging ) `
```

### Parameter Details

1. **semantic_filter** - Sets the target topic or content type - Use keywords relevant to your desired content - Example: "technical specifications", "user reviews", "pricing information"

2. **sim_threshold** - Controls how similar content must be to be grouped together - Higher values (e.g., 0.8) mean stricter matching - Lower values (e.g., 0.3) allow more variation 

```
`# Strict matching strategy = CosineStrategy(sim_threshold=0.8) # Loose matching strategy = CosineStrategy(sim_threshold=0.3) `
```

3. **word_count_threshold** - Filters out short content blocks - Helps eliminate noise and irrelevant content 

```
`# Only consider substantial paragraphs strategy = CosineStrategy(word_count_threshold=50) `
```

4. **top_k** - Number of top content clusters to return - Higher values return more diverse content 

```
`# Get top 5 most relevant content clusters strategy = CosineStrategy(top_k=5) `
```

## Use Cases

### 1. Article Content Extraction

```
`strategy = CosineStrategy( semantic_filter="main article content", word_count_threshold=100, # Longer blocks for articles top_k=1 # Usually want single main content ) result = await crawler.arun( url="https://example.com/blog/post", extraction_strategy=strategy ) `
```

### 2. Product Review Analysis

```
`strategy = CosineStrategy( semantic_filter="customer reviews and ratings", word_count_threshold=20, # Reviews can be shorter top_k=10, # Get multiple reviews sim_threshold=0.4 # Allow variety in review content ) `
```

### 3. Technical Documentation

```
`strategy = CosineStrategy( semantic_filter="technical specifications documentation", word_count_threshold=30, sim_threshold=0.6, # Stricter matching for technical content max_dist=0.3 # Allow related technical sections ) `
```

## Advanced Features

### Custom Clustering

```
`strategy = CosineStrategy( linkage_method='complete', # Alternative clustering method max_dist=0.4, # Larger clusters model_name='sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2' # Multilingual support ) `
```

### Content Filtering Pipeline

```
`strategy = CosineStrategy( semantic_filter="pricing plans features", word_count_threshold=15, sim_threshold=0.5, top_k=3 ) async def extract_pricing_features(url: str): async with AsyncWebCrawler() as crawler: result = await crawler.arun( url=url, extraction_strategy=strategy ) if result.success: content = json.loads(result.extracted_content) return { 'pricing_features': content, 'clusters': len(content), 'similarity_scores': [item['score'] for item in content] } `
```

## Best Practices

1. **Adjust Thresholds Iteratively** - Start with default values - Adjust based on results - Monitor clustering quality

2. **Choose Appropriate Word Count Thresholds** - Higher for articles (100+) - Lower for reviews/comments (20+) - Medium for product descriptions (50+)

3. **Optimize Performance**

```
`strategy = CosineStrategy( word_count_threshold=10, # Filter early top_k=5, # Limit results verbose=True # Monitor performance ) `
```

4. **Handle Different Content Types**

```
`# For mixed content pages strategy = CosineStrategy( semantic_filter="product features", sim_threshold=0.4, # More flexible matching max_dist=0.3, # Larger clusters top_k=3 # Multiple relevant sections ) `
```

## Error Handling

```
`try: result = await crawler.arun( url="https://example.com", extraction_strategy=strategy ) if result.success: content = json.loads(result.extracted_content) if not content: print("No relevant content found") else: print(f"Extraction failed: {result.error_message}") except Exception as e: print(f"Error during extraction: {str(e)}") `
```

The Cosine Strategy is particularly effective when: - Content structure is inconsistent - You need semantic understanding - You want to find similar content blocks - Structure-based extraction (CSS/XPath) isn't reliable

It works well with other strategies and can be used as a pre-processing step for LLM-based extraction.

Site built with [MkDocs](http://www.mkdocs.org) and [Terminal for MkDocs](https://github.com/ntno/mkdocs-terminal). 

##### Search

xClose

Type to start searching
