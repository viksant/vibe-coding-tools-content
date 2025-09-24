---
title: "Google Ads Library MCP"
description: "Comprehensive Google Ads transparency research with AI media analysis and caching."
category: "mcp-servers"
tags: ["API", "server", "data analysis", "media analysis", "caching", "transparency"]
tech_stack: ["Google Ads API", "SQLite", "Gemini AI", "FastMCP", "Media Intelligence", "Claude vision"]
---

This MCP server enables deep analysis of Google Ads transparency data through a robust FastMCP-based architecture featuring three integrated services. 

It provides access to Google's Ads Transparency API through ScrapeCreators, maintains a persistent SQLite media cache in `~/.cache/google-ads-mcp/` to optimize performance, and leverages Gemini AI for sophisticated video content analysis. 

The server exposes seven specialized tools for ad search, data retrieval, AI-powered media analysis, and cache management. 

It supports both image analysis using Claude vision capabilities and video processing through Gemini, with comprehensive error handling and intelligent caching strategies to minimize redundant API calls and ensure reliable operation.