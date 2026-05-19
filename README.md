"""
News Category Analyzer
======================

A Scrapy-based crawler that visits a list of news websites and analyzes
which categories (sections / topics) are the most common across them.

How it detects categories
-------------------------
News sites generally surface their sections in 3 places:

1. <nav> menus  -> links like /politics, /sports, /business ...
2. <meta>       -> article:section, og:section, news_keywords, keywords
3. URL paths    -> the first path segment of an article URL is usually
                   the section (e.g. /world/2025/05/.../article -> "world")
4. JSON-LD      -> NewsArticle.articleSection

The spider normalizes everything to lowercase slugs, filters out
non-category tokens (about, contact, login, privacy, ...), counts them
and writes a ranked report (CSV + console table).

Usage
-----
    pip install scrapy
    python news_categories.py
    

Outputs
-------
    category_counts.csv  - ranked categories with counts and site coverage
    per_site_categories.json - raw per-site categories
"""
