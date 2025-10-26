# Esports Insight Dashboard (Educational / Non-Commercial)

## Overview
Esports Insight Dashboard is an educational data engineering project focused on analyzing publicly available performance data from professional League of Legends esports.

The objective is to help fans, students, and analysts understand competitive trends (team form, player performance, matchup history, etc.) through clean, aggregated, historical data.

This project:
- is **non-commercial**
- does **not** provide betting, gambling, odds, or wagering
- does **not** run or manage tournaments
- does **not** attempt to influence in-game behavior
- does **not** expose private player data
- does **not** use undocumented or internal Riot endpoints

It is built as part of a data engineering curriculum and is intended for learning, research, and fan insights.  
It is not a production betting tool, coaching tool, or competitive integrity tool.


## Goals
1. Collect and store **publicly available competitive results** (match outcomes, rosters, schedules).
2. Build a data pipeline / data lake to demonstrate good engineering practices:
   - ingestion
   - normalization
   - historical storage
   - analytics-ready views
3. Provide aggregated insights such as:
   - team win rates over a period
   - player consistency metrics over multiple stages/splits
   - matchup history between two specific teams
4. Showcase data engineering skills (ETL, data modeling, partitioning, historization) in a transparent and compliant way.


## Scope and Non-Goals
### In Scope
- Historical and descriptive analytics about pro play.
- Dashboards that summarize past performance of professional teams and players.
- Educational demonstration of data ingestion, transformation, and warehousing.

### Explicitly Out of Scope
To comply with Riot policies:
- ❌ No tournament hosting, lobby generation, matchmaking, or bracket management.
- ❌ No use of the Tournaments API.
- ❌ No alternative MMR, no hidden skill rating, no performance “shaming”.
- ❌ No betting, odds calculation, gambling, or payout system.
- ❌ No monetization, premium tiers, or paywalled features.
- ❌ No automation that interacts with the League of Legends game client, chat, or any protected system.

This project is read-only analytics over already played matches.  
It does not give a player any unfair in-game advantage.


## Data Sources
This project aggregates data from:
- **Riot's documented public APIs** (e.g. Match V5 / Summoner V4 / League V4) strictly within rate limits and terms.
- **Publicly available esports match information** (e.g. published results, team rosters, tournament stages).
- **Open community resources / wikis** that publish historical esports data.

Important compliance notes:
- We do **not** scrape internal or undocumented Riot esports endpoints.
- We do **not** attempt to access data that is not already publicly available.
- We do **not** re-host Riot assets, logos, or branding.


## Technical Architecture (High-Level)
1. **Ingestion Layer (Extract)**
   - Small Python services fetch allowed, documented data sources.
   - API keys are stored securely (environment variables / secrets).
   - Raw responses are stored in a `bronze` zone (append-only, timestamped).

2. **Processing Layer (Transform)**
   - Spark / PySpark jobs clean and normalize entities such as:
     - leagues
     - teams
     - players
     - matches
     - individual games / maps
     - per-player performance stats
   - Each dataset is enriched with metadata like ingestion timestamp and source.

3. **Storage Layer**
   - Normalized (curated) data is stored in Parquet, partitioned for analytics at scale.
   - Historical snapshots are preserved for longitudinal analysis.

4. **Analytics Layer**
   - Aggregated views power questions like:
     - “Which team has the highest match win rate in the last X days?”
     - “Which player has the best KDA in role ‘mid’ during a given split?”
   - These are descriptive / historical statistics only.

5. **Presentation Layer**
   - A simple dashboard / API to expose summaries to fans and students.
   - No betting lines, no gambling suggestions, no predictive odds.


## Compliance with Riot Developer Policies
This project is intentionally designed to respect Riot's Third Party Developer Tools policies:

- We acknowledge that access to the Riot Games API is a privilege and can be revoked at any time.
- We do not claim partnership, endorsement, or approval from Riot Games.
- We do not use Riot Games logos, trademarks, or branding.
- We do not expose, bundle, resell, or redistribute Riot API keys.
- We do not use Development keys or Interim keys in public-facing environments.
- We do not provide (or imply) any competitive advantage in-game.
- We do not create any experience that could harm player experience, integrity, or safety.
- We are not organizing tournaments and we do not use the Tournaments API.
- We do not handle buy-ins, entry fees, payouts, or any gambling-related mechanic.
- We do not create any matchmaking / ladder / elo / hidden-MMR system.
- All features are intended to remain freely accessible and non-commercial.

If a future feature request could fall into a grey area (for example: money, skill ranking, predictive win probability for gambling use, etc.), the intent is to request guidance from Riot **before** implementing it.


## Security & Key Management
- API keys are stored in environment variables or a secret manager.
- Keys are never committed to source control.
- Keys are never exposed client-side.
- Access to the data pipeline is limited to contributors to this repository for educational purposes.
- If this repository is ever deployed publicly, it will not ship any Riot API key.


## Project Status
This is an in-progress educational build:
- It is not commercial.
- It is not sold or paywalled.
- It is used for data engineering learning, portfolio demonstration, and esports insights for fans.


## Contact / Ownership
This repository is maintained by a student / independent developer for educational and community insight purposes.

This project is not affiliated with, sponsored by, or approved by Riot Games.
All League of Legends related data and assets are property of Riot Games, Inc.
