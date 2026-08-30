# Personal Command Center PRD

Version: v2.4 synthesis from PCC design and build-plan docs
Date: August 30, 2026
Owner: Ubaidul Khan

## 1. Product Summary

Personal Command Center (PCC) is a self-hosted personal life operating system that consolidates daily signals across planning, work, markets, health, spiritual practice, family planning, fun, and morning routine intelligence. The product should feel calm, personal, and capable: a daily operating surface rather than a generic SaaS dashboard.

The primary experience is the Today dashboard. It surfaces the next prayer, current urgency, and the highest-value summary from each life pillar. The newest strategic feature is Module 24, Morning Routine Intelligence, which combines HealthKit sleep data, a one-tap mood check-in, rules, and Claude-generated narrative to recommend morning audio, caffeine, and breakfast.

## 2. Goals

- Reduce daily context switching across planning, work inboxes/tasks, finance, health, spiritual tracking, family planning, hobbies, and entertainment queues.
- Make the Today dashboard the trusted first screen for the day.
- Keep prayer times and salah tracking emotionally grounding and immediately actionable.
- Use sleep and mood to generate a practical morning briefing after Fajr.
- Support desktop, tablet, and iPhone layouts from the beginning.
- Keep costs low through local/self-hosted services, free data sources, and sparse LLM calls.
- Preserve user control through transparent rules, rating feedback, and dashboard customization.

## 3. Non-Goals

- Multi-user enterprise account management in the first release.
- Full App Store deployment for the iOS companion app.
- Real-time options chains unless Polygon.io is explicitly enabled.
- LLM-only recommendation logic. Rule-based behavior must remain the fast, explainable default.
- A marketing landing page. PCC opens directly into the usable command surface.

## 4. Target User

The target user is a single power user managing daily responsibilities across work, worship, family, markets, health, and learning. The product should reward repeated daily use, quick scanning, and one-tap logging.

## 5. Core Pillars

### Markets

Dense, Bloomberg-lite market view covering quotes, OHLCV, macro readings, news, portfolio P&L, target prices, movers, winners, losers, upgrades, downgrades, and signal narratives.

### Work

Focused command surface for professional obligations. Tracks Gmail, Outlook, Teams mentions, TeamDynamix tickets, Google Keep reminders, calendar commitments, priority tasks, and daily work focus. Work should feel quiet, utilitarian, and optimized for triage rather than project-management theater.

### Planning

Cross-pillar planning surface for today, this week, and longer-horizon commitments. Planning should unify tasks, calendar milestones, family commitments, work deadlines, habit targets, and personal projects without replacing the specialized pillar screens.

### Health

Apple Health-inspired but warmer. Tracks calories, steps, active calories, weight, sleep, workout targets, food logging, and daily/weekly trends.

Health subareas:
- Exercise: workout schedule, weekly targets, cardio/strength logs, heart-rate trends, VO2 estimate, and recovery context.
- Diet: calorie budget, food log, macros, USDA search, breakfast recommendations, hydration prompts, and goal progress.

### Spiritual

Prayer times, adhan, salah tracking, Jumu'ah handling, Quran reading, Arabic learning, hifz flashcards, and spiritual streaks. This pillar should be the most spacious and reverent.

### Family

Activity planning for family members and side hustle project management. Includes AI activity suggestions, Kanban lanes, project milestones, tasks, dependencies, and weekly project health summaries.

### Fun

Personal enjoyment and recovery area containing Hobby and Entertainment.

Fun subareas:
- Hobby: creative, learning, tinkering, reading, side interests, and personal projects done for enjoyment rather than obligation.
- Entertainment: queue-oriented YouTube and podcast surface with interest tags, playback position, in-app player controls, and morning queue generation.

### Morning Routine

Sleep-aware and mood-aware recommendations for audio, caffeine, and breakfast, delivered in the Today card and a full Morning Routine screen.

## 6. Primary User Journeys

### Start the Day

1. User opens PCC on phone, tablet, or laptop.
2. Today dashboard displays next prayer as the primary hero.
3. After Fajr, the Morning Routine card appears directly beneath the prayer hero.
4. User confirms or changes mood with one tap.
5. PCC shows audio, caffeine, and breakfast recommendations.
6. User opens full routine, plays audio, logs caffeine/breakfast, and optionally rates yesterday.

### Track Prayer

1. User sees next prayer countdown and all five prayer statuses.
2. User logs salah as On Time, Qada, or Missed with location.
3. On Fridays, Dhuhr is replaced by Jumu'ah with Adams Center details and departure countdown.
4. Prayer history updates daily rings and weekly summary.

### Scan Markets

1. User opens Markets or taps a Today signal chip.
2. PCC shows macro strip, watchlist, movers, portfolio P&L, signal score, and compact news.
3. User adjusts signal weights or reviews Claude market narrative.

### Triage Work

1. User opens Work or taps a Today work chip.
2. PCC shows the highest-priority inbox items, Teams mentions, open TDx tickets, Keep reminders, and calendar deadlines.
3. User marks an item reviewed, opens the source system, or promotes it into a Today focus item.
4. PCC updates the Right Now strip when hard work deadlines become urgent.

### Customize Dashboard

1. User enters Customize Dashboard mode.
2. Cards expose reorder, resize, hide/show, and pin controls.
3. User saves layout per device class.
4. Normal dashboard returns with editing controls hidden.

## 7. Functional Requirements

### Today Dashboard

- Must be the default route.
- Must show prayer hero first.
- Must show Morning Routine second after prayer card by default.
- Must show Health, Markets, Work, Planning, Family, Fun, and spiritual progress summaries.
- Must include a Right Now strip for urgent cross-pillar chips.
- Must auto-refresh urgency chips every 60 seconds.
- Must support customizable card pinning, ordering, hiding, and resizing.
- Must keep customization controls out of the normal browsing mode.

### Prayer Hero

- Show next prayer name in transliteration and Arabic.
- Show animated countdown ring and HH:MM:SS countdown.
- Update countdown every second.
- Show five daily prayers with status badges.
- Support urgency states: steady, slow pulse, medium pulse, fast pulse, near-time strobe/glow, and prayer-time burst.
- Play adhan at prayer time when not muted.
- Provide visible mute control.
- Replace Dhuhr with Jumu'ah on Fridays.

### Morning Routine Intelligence

- Pull previous night sleep data from HealthKit-ingested health metrics.
- Compute sleep duration, sleep quality score, and tier.
- Infer default mood from sleep tier.
- Allow one-tap mood override: Energized, Neutral, Tired, Stressed, Calm.
- Generate recommendations using rule-based matrix before any LLM call.
- Recommend one music/audio genre, one caffeine option, and one breakfast option.
- Consider calorie budget and scheduled workout when recommending breakfast.
- Always provide a Quran shortcut in the music section.
- Generate a 2-3 sentence Claude narrative once per morning.
- Save recommendation, selected mood, actual choices, and narrative to morning log.
- Ask for thumbs up/down rating and optional note.
- Run weekly preference analysis after enough ratings and update overrides.

### Health

- Ingest calories, steps, swim, walk, HR, weight, and sleep from iOS HealthKit companion.
- Compute daily rollups, calorie budget, TDEE, sleep score, and trend data.
- Expose today's workout schedule to Morning Routine.

### Markets

- Fetch market data from Yahoo Finance, Alpha Vantage, Finnhub, FRED, and NewsAPI.
- Cache frequently requested data in Redis.
- Store time-series data in TimescaleDB.
- Compute transparent rule-based signal scores.
- Generate hourly Claude narrative from top readings and news.

### Work

- Fetch unread or priority Gmail threads through Google OAuth.
- Fetch Outlook mail, calendar items, and Teams mentions through Microsoft Graph.
- Fetch open or assigned TeamDynamix tickets.
- Parse Google Keep notes for dated reminders and upcoming obligations.
- Generate a daily work digest with source, urgency, due time, owner, and recommended next action.
- Let users mark digest items reviewed, deferred, or promoted to Today.
- Keep source-system links available so PCC does not become the system of record for enterprise data.

### Planning

- Aggregate dated tasks, calendar events, milestones, reminders, work deadlines, family commitments, and habit targets.
- Support Today, Week, and Backlog views.
- Let users promote planning items into Today focus.
- Preserve source attribution for items created by other pillars.
- Surface time-sensitive plan items in the Right Now strip.

### Family

- Store family members, interests, activity ideas, activity logs, projects, milestones, tasks, and dependencies.
- Generate weekly activity suggestions and project health summaries.
- Support board and timeline views.

### Fun

- Store hobbies and recreational projects with lightweight progress, next action, and optional streaks.
- Fetch YouTube subscription items and podcast RSS episodes.
- Build a daily queue with interest tags.
- Support in-app podcast playback and podcast app handoff.
- Keep Hobby and Entertainment available as subareas under Fun.

## 8. UX Requirements

- Light mode is default; dark mode must be supported.
- Use a warm off-white base, white cards, subtle borders, and restrained pillar accents.
- Use Inter for UI, JetBrains Mono for data, and Amiri for Arabic.
- Desktop uses a fixed left sidebar.
- Tablet uses a collapsible left sidebar.
- Mobile uses bottom tab navigation.
- Cards should be softly rounded and information-dense only where the pillar demands it.
- Markets and Work can be dense; Planning should be structured and scan-friendly; Spiritual must be spacious; Morning should feel warm and motivating; Fun should feel relaxed without becoming noisy.
- Do not rely on color alone for status.
- All interactive elements need visible focus states.

## 9. Data Sources

- Yahoo Finance via yfinance: quotes and OHLCV.
- Alpha Vantage: technical indicators.
- FRED: CPI, PCE, jobs, macro readings.
- NewsAPI: market and global news.
- Finnhub: VIX, earnings, sentiment.
- Polygon.io: optional options/futures data.
- Gmail, Microsoft Graph, TeamDynamix, and Google Keep: work inbox, calendar, mentions, ticket, and reminder signals.
- Apple HealthKit: health and sleep inputs.
- USDA FoodData Central: food/macros.
- adhan-py: local prayer time calculation.
- cdn.islamic.network: adhan audio.
- Al Quran Cloud API and Quran.com API: Quran text, audio, and word-level data.
- YouTube Data API v3: videos, channels, music playlists.
- iTunes Search API and podcast RSS: podcast metadata/audio.
- Claude API: narratives, suggestions, and preference learning.

## 10. Success Metrics

- User can understand the next important action within 5 seconds of opening Today.
- User can log prayer status in 2 taps or fewer from Today.
- User can complete morning mood check-in in 1 tap.
- Morning recommendation renders without waiting on Claude.
- Claude narrative appears after recommendation without blocking the rest of the UI.
- Dashboard customization can be entered, changed, saved, and exited without losing layout.
- Mobile Today remains readable without horizontal scrolling except dense Markets tables.

## 11. Open Questions

- Should the tablet sidebar collapse to an icon rail or hide fully behind a gesture?
- Should adhan interrupt morning audio or duck its volume?
- Should Markets charts always use a dark chart panel even in light mode?
- Should PCC use a custom logo or text-only wordmark?
- Should Jumu'ah have a distinct visual treatment beyond replacing Dhuhr?
