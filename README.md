<p align="center">
  <img src="assets/mascot.png" alt="FlowBot" width="180"/>
</p>

<h1 align="center">FlowBot</h1>

<p align="center">
  <strong>Your easy guide to getting around Boston</strong><br>
  One conversation replaces five apps.
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=white" alt="React"/></a>
  <a href="#"><img src="https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript"/></a>
  <a href="#"><img src="https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python"/></a>
  <a href="#"><img src="https://img.shields.io/badge/Flask-3-000000?style=flat-square&logo=flask&logoColor=white" alt="Flask"/></a>
  <a href="#"><img src="https://img.shields.io/badge/SQLite-3-003B57?style=flat-square&logo=sqlite&logoColor=white" alt="SQLite"/></a>
  <a href="#"><img src="https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" alt="Tailwind"/></a>
  <a href="#"><img src="https://img.shields.io/badge/Vite-6-646CFF?style=flat-square&logo=vite&logoColor=white" alt="Vite"/></a>
  <a href="#"><img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License"/></a>
</p>

<p align="center">
  <a href="#what-is-flowbot">What is FlowBot?</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#features">Features</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#the-problem">The Problem</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#our-solution">Our Solution</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#demo">Demo</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#architecture">Architecture</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#data-sources">Data Sources</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;
  <a href="#team">Team</a>
</p>

---

## What is FlowBot?

FlowBot is a conversational chatbot that helps you navigate Boston using **buses, trains, bikes, walking, and driving** — all in one place. Instead of switching between MBTA, Google Maps, Bluebikes, and parking apps, you ask FlowBot a single question and get a clear, sourced answer comparing your options.

> *"I want to commute to Boston now."*
>
> FlowBot compares routes across every mode — time, cost, and convenience — so you can pick the best one.

This is a **showcase repository**. We share our design, architecture, and data sources openly as a learning resource. Source code is maintained privately.

---

## Features

<p align="center">
  <img src="assets/page2_modes.png" alt="FlowBot covers Bus, Parking, Car, Train, Bike, and Walking" width="700"/>
</p>

| | Feature | What It Does |
|---|---|---|
| :bus: | **Bus & Train** | Real-time MBTA schedules, route options, service alerts |
| :car: | **Driving** | Traffic-aware directions with time and cost estimates |
| :parking: | **Parking + Sign Reader** | Upload a photo of any parking sign — get a plain-English answer plus nearby alternatives |
| :bike: | **Biking** | Live Bluebikes station availability (bikes and open docks) |
| :walking: | **Walking** | Walkable route suggestions with distance and time |
| :bar_chart: | **Smart Comparison** | Side-by-side breakdown across all modes for the same trip |

---

## The Problem

<p align="center">
  <img src="assets/page3_problems.png" alt="Problems: Unreliable Transit Timing, Unclear Parking Rules, Fragmented Information" width="700"/>
</p>

Getting around Boston means juggling multiple disconnected apps and sources:

- **Unreliable Transit Timing** — Schedules change, delays happen, and you don't find out until you're already waiting.
- **Unclear Parking Rules** — Signs are confusing, rules overlap, and a wrong guess means a ticket.
- **Fragmented Information** — Bus routes on one app, bike stations on another, parking on a third. No single place compares them all.

---

## Our Solution

<p align="center">
  <img src="assets/page4_solutions.png" alt="Solutions: Route Planner, Parking + Sign Reader, Multi-Modal Urban Intelligence" width="700"/>
</p>

FlowBot addresses each problem with a specific capability:

**01 — Route Planner**
Compare time and cost across bus, train, bike, walking, and driving for any trip. One question, all options.

**02 — Parking + Sign Reader**
Upload a photo of a parking sign and get an instant, plain-English explanation — plus nearby alternatives if you can't park there.

**03 — Multi-Modal Urban Intelligence**
A unified conversational interface that combines transit, buses, biking, walking, and driving into a single answer grounded in real data.

---

## Demo

<p align="center">
  <img src="assets/ui_screenshot.jpeg" alt="FlowBot chat interface showing welcome message and suggestion chips" width="600"/>
</p>

<p align="center"><em>FlowBot's chat interface with quick-action suggestion chips</em></p>

**Try asking:**

| Question | What FlowBot Does |
|---|---|
| *"Fastest way to Boston Common"* | Compares bus, train, bike, walking, and driving with times and costs |
| *"What does this sign mean?"* | Reads an uploaded parking sign photo and explains the rules |
| *"Can I park here?"* | Checks parking regulations for your area and suggests alternatives |
| *"Is the Green Line running?"* | Pulls real-time MBTA service alerts and schedule updates |
| *"Nearest Bluebikes station"* | Shows live bike and dock availability at nearby stations |

<p align="center">
  <video src="https://github.com/ramihuunguyen/FlowBot/raw/main/FlowBotDemo.mp4" width="600" controls>
    Your browser does not support the video tag.
  </video>
</p>

---

## Architecture

FlowBot uses a **Retrieval-Augmented Generation (RAG)** pipeline — every answer is grounded in real data, not hallucinated.

```
User Question
     |
     v
Query Expansion ──── Topic-aware keywords added to query
     |
     v
Hybrid Retrieval
  ├── Vector Search ── Semantic similarity (sentence embeddings)
  └── BM25 Search ──── Exact keyword matching
     |
     v
Deduplication ──────── Merge results, remove duplicates
     |
     v
Cross-Encoder Reranking ── Re-score (query, passage) pairs
     |
     v
Context Builder ────── Format top passages + source URLs
     |
     v
LLM Generation ────── Structured answer with cited sources
     |
     v
Response ──────────── Concise answer + source links
```

**By the numbers:**

| Metric | Value |
|---|---|
| Documents scraped | Thousands across 11 public sources |
| Searchable passages | Thousands of chunked passages |
| Embedding model | Sentence-transformer (384 dimensions) |
| Reranker | Cross-encoder reranking |
| Query expansion | Multiple topic categories for improved recall |

---

## Data Sources

FlowBot pulls from **11 public data sources** — no paid APIs required.

| Source | What It Provides | Method |
|---|---|---|
| MBTA Routes API | Bus, subway, commuter rail, and ferry routes | API fetch |
| MBTA Stops API | Every stop and station across the network | API fetch |
| Bluebikes GBFS Feed | Bike-share stations with real-time availability | API fetch |
| MBTA Accessibility Pages | Accessibility info for stations and services | Web scrape |
| Boston Transportation Dept | City transportation policies and updates | Web scrape |
| Boston Parking Info | Parking regulations, meters, and resident permits | Web scrape |
| Parking/Road Sign Explanations | Plain-English explanations for common sign types | Curated |
| Mass511 Traffic Incidents | Real-time traffic incidents and road closures | API/Scrape |
| Overpass API (Walking Paths) | Pedestrian paths, sidewalks, and walking routes | API fetch |
| Boston Data Portal | Traffic signals, Vision Zero crash data | API fetch |
| MA Driver's Manual | Sign rules and driving regulations | PDF extraction |

---

## Prompt Design

FlowBot's system prompt enforces structured, grounded responses:

- **Step-by-step reasoning** — The LLM thinks through what the user is asking, which passages are relevant, and what key facts to include before generating an answer.
- **Structured output** — Every response follows the same format: a concise main answer followed by clickable source links.
- **Source citation required** — The LLM must cite the specific data sources backing each claim. No unsupported statements.
- **Scope enforcement** — Questions outside Boston transportation get a polite redirect rather than a hallucinated answer.

---

## Team

Built at **UMass Boston** — CS 438/638, Spring 2026.

| | |
|---|---|
| **HuuThanhVy Nguyen (Rami)** | **Justin J McMahon** |
| **Domenic B DiClemente** | **Igor Ten** |
| **Ajanee T Igharo** | **MeghSanjaykumar Patel** |
| **Felipe Mahecha** | **Syed Taswar Mahbub** |

---

<p align="center">
  <img src="assets/page6_curious.png" alt="Curious about FlowBot?" width="500"/>
</p>

<p align="center">
  <strong>Curious about the details?</strong><br>
  Open an issue or reach out to any team member.
</p>

---

<p align="center">MIT License</p>
