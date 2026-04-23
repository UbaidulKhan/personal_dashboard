# PCC v22 Build Plan

## Page 1

Personal Command Center v2.2 — Full Life Operating System




                  Personal Command Center
                                    Full Life Operating System
                      Architecture & Cursor Build Plan — Version 2.2 — April 2026


           Markets · Health · Spiritual Growth · Family · Productivity · Morning Routine

   💹 Markets          💚 Health        🕋 Spiritual      👪 Family       ☀ Morning        🎙 Entertainment
  Modules 01–11     Modules 12–15     Modules 16–19   Modules 20–22    Module 24       Module 23




1. Project Overview
Version 2.2 adds Module 24 — the Morning Routine Intelligence engine. Each morning, PCC reads last
night’s sleep data from Apple HealthKit, prompts you for a quick mood check-in (with your sleep score
as the baseline), and uses that combined signal to recommend the optimal music/audio type, breakfast,
and caffeine choice for your morning. Recommendations are explained, rateable, and improve over
time. All prior content from v2.1 is fully preserved.



What’s New in v2.2
    •   Module 24: Morning Routine Intelligence — sleep-aware, mood-aware daily recommendations
    •   Music rotation: Quran recitation, nasheeds, lo-fi, instrumental, classical/jazz, upbeat (pop/hip-
        hop), classic rock (80s & 90s)
    •   Caffeine logic: green tea (good sleep + calm), coffee 1 cup (moderate), coffee strong (poor
        sleep), with hydration reminders
    •   Breakfast logic: high-protein (eggs, Greek yogurt, protein shake) or traditional warm (oatmeal,
        toast, ful medames) based on energy need
    •   Delivery: Today dashboard card + full Morning Routine screen; no email
    •   Feedback loop: rate yesterday’s recommendation (thumbs up/down + note), Claude learns your
        preferences over time



2. Today Dashboard (Morning Home Screen)
The Today dashboard is the app’s home page. Prayer times remain the top card. The Morning Routine
card appears second, immediately after prayer times.


                         Today Dashboard — Card Order (top to bottom)

Confidential — Personal Use                                                               Page 1

## Page 2

Personal Command Center v2.2 — Full Life Operating System

   🕌 Prayer          ☀ Morning         🕋 Quran &         💧 Health          💹 Markets        👪 Family
        Times         Routine            Arabic        Calories, steps,   Top signal, P&L   Active project
   Next prayer +   Music, breakfast,   Today’s goal,        sleep
    countdown          caffeine           streak



    •    Morning Routine card shows: sleep score badge, mood selector (5 options), then
         recommendation summary (music genre, breakfast, caffeine) — all in one compact card
    •    Tap ‘See full routine’ to open the Morning Routine screen with full detail, reasoning, and audio
         playback
    •    Mood selector defaults to the AI-inferred mood from sleep data; you can tap to override in one
         tap
    •    On Fridays the Jumu’ah departure card replaces the Dhuhr entry as before



3. Module 24 — Morning Routine Intelligence
This is the primary new feature in v2.2. It combines Apple HealthKit sleep data, a lightweight mood check-in, a
rule-based decision engine, Claude API narrative reasoning, and a feedback/learning loop to recommend music,
breakfast, and caffeine each morning.



3.1 Inputs — How Energy & Mood Are Determined
Step 1: Sleep baseline (automatic, from HealthKit)
   • Total sleep duration pulled from the previous night’s HealthKit sleep analysis record
    •    Sleep quality score computed from: duration, time-in-bed vs. asleep ratio, wake events, and
         deviation from 10 PM–6 AM target window
    •    Sleep tiers: Excellent (≥ 7.5 hrs, within 30 min of target) — Good (6–7.5 hrs) — Poor (< 6 hrs)
         — Overslept (missed Fajr window)
    •    The sleep tier becomes the energy baseline and is shown on the morning card as a colored
         badge (green / amber / red / gray)


Step 2: Mood check-in (optional 1-tap override)
   • Mood selector appears on the Morning Routine card immediately after Fajr time
    •    5 mood options displayed as icon + label: 😄 Energized — 😐 Neutral — 😪 Tired — 😰 Stressed
         — 🧘 Calm
    •    Default selection is AI-inferred from sleep tier: Excellent → Energized, Good → Neutral, Poor →
         Tired, Overslept → Stressed
    •    You tap to override if the default doesn’t match how you actually feel — takes one tap, no typing
    •    Both the sleep tier and selected mood are stored and used together by the recommendation
         engine


3.2 Recommendation Engine — Decision Logic
The engine uses a two-layer approach: a fast rule-based layer for instant recommendations, and
Claude for the explanatory narrative.

Confidential — Personal Use                                                                      Page 2

## Page 3

Personal Command Center v2.2 — Full Life Operating System



Layer 1: Rule-based recommendations (instant, zero API cost)
   • Music/audio: mapped from mood × sleep tier using the decision matrix below
   • Caffeine: green tea for good sleep + calm mood; standard coffee (1 cup) for moderate energy;
       strong coffee (1–2 cups) for poor sleep; always includes a hydration reminder if sleep was < 6
       hrs
   • Breakfast: high-protein options (eggs, Greek yogurt, protein shake) when energy is low or
       workout is scheduled; traditional warm options (oatmeal, toast, ful medames) when mood is
       calm or spiritual morning is planned; light options only when explicitly chosen or calorie budget
       is nearly met
   • Calorie awareness: breakfast suggestion cross-references the health module’s daily calorie goal
       and remaining budget
   • Workout awareness: if a workout is scheduled in the exercise tracker for today, the engine
       always favors high-protein breakfast


Decision matrix: sleep × mood → recommendation


  Sleep Score        Mood             Caffeine                  Breakfast                  Music / Audio
                    Override
Excellent (≥ 7.5   Energized   Green tea (light)         High protein — eggs,     Upbeat: classic rock 80s/90s,
hrs, on time)                                            Greek yogurt             pop
Excellent (≥ 7.5   Calm        Green tea or none         Traditional warm —       Quran recitation or nasheed
hrs, on time)                                            oatmeal, ful medames
Good (6–7.5        Energized   Coffee (1 cup)            High protein — protein   Classic rock or lo-fi
hrs)                                                     shake + toast
Good (6–7.5        Tired /     Coffee (1 cup)            Traditional warm —       Quran recitation or instrumental
hrs)               Stressed                              oatmeal, toast
Poor (< 6 hrs)     Any         Coffee (strong, 1–2       High protein — eggs +    Lo-fi / ambient or nasheed
                               cups)                     protein shake
Poor (< 6 hrs)     Stressed    Coffee + water reminder   Light protein — Greek    Quran recitation (calming)
                                                         yogurt, smoothie
Skipped Fajr       Any         Coffee immediately        Quick high protein —     Upbeat — classic rock or
(overslept)                                              shake or yogurt          energetic nasheed



Layer 2: Claude narrative (one call per morning, ~$0.002)
   • After the rule-based recommendation is generated, Claude receives: sleep duration, sleep
       quality score, mood selection, yesterday’s rating, and today’s calendar (prayer times, scheduled
       workout, any family activities)
   • Claude returns a 2–3 sentence personalized morning message explaining the recommendation,
       e.g.: ‘You got 5.5 hours last night and selected Tired — I’ve suggested a strong coffee and eggs
       to help you power through. Start with Quran recitation to center yourself before the day picks up.
       Your Asr prayer is at 4:30 PM — a good natural break point.’
    •   The narrative is displayed on the Morning Routine screen and on the Today card (collapsed to 1
        sentence on the card)
    •   Cost: ~1 Claude call per morning × 30 days ≈ $0.06/month additional on top of existing Claude
        usage


Confidential — Personal Use                                                                               Page 3

## Page 4

Personal Command Center v2.2 — Full Life Operating System

3.3 Music & Audio Recommendation
Full rotation available (user-configured, all enabled by default)
   • Quran recitation — Al Quran Cloud audio (same source as Spiritual pillar). Recommended for:
        calm mood, post-Fajr mornings, stressed state (grounding)
   • Arabic nasheeds (no instruments) — curated playlist links (YouTube or local files).
        Recommended for: spiritual mornings, calm or neutral mood
   • Lo-fi / ambient — YouTube playlist links (curated lofi channels). Recommended for: tired state,
        focus-needed mornings, poor sleep recovery
   • Instrumental / nature sounds — YouTube or Spotify-style links. Recommended for: calm + good
        sleep, meditation mornings
   • Classical / jazz — YouTube playlist links. Recommended for: good sleep + neutral mood, work-
        from-home mornings
   • Upbeat / energetic (pop, hip-hop) — YouTube playlist links. Recommended for: excellent sleep
        + energized mood, workout mornings
   • Classic rock — 80s & 90s (e.g. Bon Jovi, Queen, Eagles, Def Leppard). YouTube playlist links.
        Recommended for: good/excellent sleep + energized mood, overslept recovery boost


Music delivery
  • Morning Routine screen shows the recommended genre with a ‘Play’ button that opens a
      curated YouTube playlist in a new tab or the in-app YouTube embed
    •   You can tap any other genre tile to switch — all 7 options are shown as tappable cards
    •   Selected genre is logged for feedback tracking
⚠
   Quran recitation is always available regardless of recommendation — a dedicated ‘Listen to Quran’ shortcut
appears at the top of the music section.



3.4 Caffeine Recommendation
    •   Green tea: recommended when sleep was Excellent + mood is Calm or Neutral. Displays:
        ‘Green tea — you’re well-rested, light caffeine is enough.’
    •   Coffee — 1 cup: recommended when sleep was Good or mood is Tired/Energized with Good
        sleep. Displays brew suggestion (e.g. drip, pour-over).
    •   Coffee — strong (1–2 cups): recommended when sleep was Poor (< 6 hrs). Displays: ‘Strong
        coffee — you need the boost today. Drink a glass of water first.’
    •   Hydration reminder: always shown when sleep < 6 hrs or mood is Stressed — ‘Drink 16 oz
        water before your coffee.’
    •   Skip caffeine option: always available with one tap — no judgment
    •   Logged to the food_log table as a zero-calorie entry for tracking consistency


3.5 Breakfast Recommendation
High-protein options (recommended for low energy, post-workout, poor sleep)
   • Eggs — scrambled, fried, or boiled. Shown with estimated prep time (5–8 min) and calorie count
      (~200–300 kcal depending on count)
    •   Greek yogurt — with honey or fruit. Shown with calorie count (~150–200 kcal)
Confidential — Personal Use                                                                  Page 4

## Page 5

Personal Command Center v2.2 — Full Life Operating System
    •   Protein shake — shown with suggested flavor/brand if user has configured a preference. (~200–
        350 kcal)
    •   Eggs + protein shake combo: suggested when sleep was Poor and a workout is scheduled
        today


Traditional / warm options (recommended for calm mornings, spiritual focus, good sleep)
   • Oatmeal — with dates, honey, or banana. Calorie estimate shown (~300–400 kcal). Prep time:
       5 min.
    •   Toast — whole grain with peanut butter or avocado. Calorie estimate (~250–350 kcal)
    •   Ful medames — Egyptian fava bean dish. Shown as ‘Weekend option’ (longer prep). Calorie
        estimate (~350–450 kcal)


Breakfast calorie integration
   • Suggested breakfast calorie count is automatically pre-filled into the food log as a pending entry
      — one tap to confirm and log it
   • If the remaining daily calorie budget is less than the suggested breakfast, the engine substitutes
      a lighter option and notes the reason
   • Breakfast skip option always available — skipping is logged and factored into calorie budget for
      the day



3.6 Morning Routine Screen
A dedicated full-screen view accessible from the Today dashboard card. Opens after Fajr. Contains:
    •   Sleep summary banner: last night’s duration, quality score, sleep tier badge, deviation from 10
        PM–6 AM target
    •   Mood selector: 5-option one-tap picker, defaulted to AI inference, overridable
    •   Recommended music genre card: genre name, description, Play button (opens YouTube
        playlist), all 7 genres shown as tappable alternates below
    •   Caffeine card: recommendation with brief reasoning, one-tap ‘Done’ to log it, ‘Skip’ option
    •   Breakfast card: recommended option with calorie estimate, prep time, one-tap log-to-food-diary,
        ‘Skip’ option
    •   Claude narrative: 2–3 sentence personalized morning message
    •   Yesterday’s rating: thumbs up / thumbs down + optional 1-line note. Appears at the bottom as a
        gentle prompt (‘How was yesterday’s morning routine?’)



3.7 Feedback & Learning Loop
    •   Each morning’s recommendation (music genre, caffeine, breakfast) is stored in the morning_log
        table with the sleep score and mood at the time
    •   Each evening (or next morning), a rating prompt appears: thumbs up (kept the
        recommendation) or thumbs down (overrode it), plus an optional note
    •   After 14 days of ratings, Claude analyzes the pattern: ‘You consistently override the lo-fi
        recommendation when your sleep is Good — switching your Good sleep default to Classic
        Rock.’

Confidential — Personal Use                                                             Page 5

## Page 6

Personal Command Center v2.2 — Full Life Operating System
    •   Preference adjustments are stored in morning_preferences table and override the default
        decision matrix going forward
    •   The learning loop runs as a weekly background job (APScheduler) — one Claude call per week
        analyzing the past 7 days of ratings (~$0.005/week)



3.8 Morning Routine Database Schema
    •   morning_log: id, date, sleep_duration_min, sleep_quality_score, sleep_tier, mood_inferred,
        mood_selected, music_genre_recommended, music_genre_used, caffeine_recommended,
        caffeine_used, breakfast_recommended, breakfast_used, claude_narrative, created_at
    •   morning_ratings: id, morning_log_id, rating (up/down), note, rated_at
    •   morning_preferences: id, sleep_tier, mood, music_genre_override, caffeine_override,
        breakfast_override, confidence_score, last_updated
    •   morning_music_playlists: id, genre, label, youtube_url, description, active


3.9 Morning Routine Backend Endpoints
    •   GET /api/morning/recommendation — returns today’s full recommendation (sleep data + mood
        default + all three suggestions + Claude narrative)
    •   POST /api/morning/mood — saves mood override {mood: ‘tired’}
    •   POST /api/morning/log — saves what was actually used {music_genre_used, caffeine_used,
        breakfast_used}
    •   POST /api/morning/rating — saves rating {morning_log_id, rating, note}
    •   GET /api/morning/history?days=30 — returns 30-day morning log with ratings
    •   POST /api/morning/preferences/recalculate — triggers the weekly Claude preference analysis
        job


3.10 Cursor Prompt for Module 24
Build the Morning Routine Intelligence module for PCC. Stack: FastAPI + PostgreSQL +
Redis + Claude API. Inputs: (1) last night's HealthKit sleep data from the
health_metrics TimescaleDB table, (2) mood selected by user (fajr/dhuhr/asr/maghrib/isha
enum). Sleep tiers: Excellent >=7.5hrs, Good 6-7.5hrs, Poor <6hrs. Decision matrix: Poor
sleep -> strong coffee + high protein breakfast + lofi/quran. Good sleep + tired mood ->
1 cup coffee + warm breakfast + lofi. Good sleep + energized -> green tea or 1 cup
coffee + high protein + classic rock or upbeat. Excellent sleep + calm -> green tea +
traditional warm + quran or nasheed. Music genres stored in morning_music_playlists
table. After rule-based recommendation, call Claude API with: sleep_duration,
sleep_tier, mood, yesterday_rating, today_prayer_times, today_workout_scheduled. Claude
returns 2-3 sentence narrative. Weekly APScheduler job calls Claude to analyze 7 days of
ratings and update morning_preferences table. Endpoints: GET
/api/morning/recommendation, POST /api/morning/mood, POST /api/morning/log, POST
/api/morning/rating, GET /api/morning/history. Write all 4 DB tables and pytest tests
for all endpoints.




4. Pillar A — Markets & Productivity

Confidential — Personal Use                                                           Page 6

## Page 7

Personal Command Center v2.2 — Full Life Operating System
Unchanged from v2.1. Modules 01–11 cover market data, macro indicators, news aggregation, portfolio
management, the signal engine, Gmail/Outlook/Teams/TDx inbox digest, Google Keep, Charles
Schwab sync, markets frontend, and Docker/Caddy deployment.


                                     Markets Pillar — Key Screens
    Market            Portfolio        News Feed        Macro Strip   Signal Config     Inbox Digest
   Dashboard          Manager         Energy, metals,    CPI, PCE,       Weights +      Gmail, Outlook,
   Quotes, VIX,      P&L, targets,       sectors        employment       narrative           TDx
    heatmap            margins
Modules 01–11: scaffold, market data, macro (FRED), news, portfolio, signal engine (rule-based scorer + Claude
narrative), inbox digest (Gmail OAuth + Graph API + TeamDynamix REST), Google Keep, Charles Schwab
OAuth sync, markets frontend (Next.js + Recharts), Docker Compose + Caddy HTTPS deployment.




5. Pillar B — Physical Health
Unchanged from v2.1. Modules 12–15.



Module 12 — iOS HealthKit Companion
    •   SwiftUI app: reads HealthKit (calories, steps, swim, walk, HR, weight, sleep analysis), POSTs to
        PCC backend every 15 min (foreground) / hourly (background)
    •   Also delivers prayer reminder APNs push notifications (time-sensitive, breaks through iOS
        Focus)
    •   Also delivers Morning Routine push at wake time (6:00 AM) with sleep score badge and mood
        selector deep-link


Module 13 — Health Data Service
    •   HealthKit ingest endpoint, TimescaleDB hypertable for health_metrics, daily rollup table
    •   USDA FoodData Central API for calorie logging food search
    •   Calorie budget and TDEE computation; macros ring chart data


Module 14 — Exercise Tracker
    •   Weekly targets per type (swimming, walking, weight training), AI weekly plan via Claude API
    •   HealthKit auto-import for cardio; manual log for resistance training
    •   Cardio health: resting HR trend, VO2 max estimate, heart rate zones
    •   Today’s workout schedule exposed to Morning Routine engine (Module 24) for breakfast logic


Module 15 — Health Frontend
    •   Today health card: calorie ring, steps, sleep score badge, active calories
    •   Sleep chart: 30-day rolling average, sleep score trend, deviation from 10 PM/6 AM target
    •   Exercise rings: weekly completion per type, HR zone chart
Confidential — Personal Use                                                                  Page 7

## Page 8

Personal Command Center v2.2 — Full Life Operating System
    •      Weight chart: actual vs. goal trajectory



6. Pillar C — Spiritual Development
Unchanged from v2.1. Modules 16–19.



Module 16 — Prayer, Adhan & Salah Tracker
    •      Prayer times: adhan-py library, ISNA method, Sterling VA coordinates (38.9898° N, 77.3897°
           W)
    •      Adhan audio: Mishary Rashid Al-Afasy from cdn.islamic.network. Fajr version includes al-salatu
           khayrun min al-nawm.
    •      Tri-channel reminders: iPhone APNs push 20 min before + in-app WebSocket banner + adhan
           plays at prayer time
    •      Salah log: On Time / Qada / Missed × Masjid / Home / Work / Traveling, one-tap from Today
           dashboard
    •      Jumu’ah: Dhuhr replaced on Fridays. Adams Center (46903 Sugarland Rd, Sterling VA). Imam
           Majed / Imam Ouertani. Departure reminder (default 60 min early). Khutba notes.
    •      History: 5-segment daily prayer ring (green/amber/red/gray), 7-ring weekly row, monthly stats,
           location pie chart


        Prayer           Arabic       Typical         Adhan           20-min        Reminder      Track Status
                                       Time*                           Alert
 Fajr              ‫ﻓﺟر‬               5:15 AM            ✅               ✅          iPhone push   On time / Qada /
                                                                                                      Missed
 Dhuhr             ‫ظﮭر‬               1:00 PM            ✅               ✅             Push +     On time / Qada /
                                                                                      banner          Missed
 Asr               ‫ﻋﺻر‬               4:30 PM            ✅               ✅             Push +     On time / Qada /
                                                                                      banner          Missed
 Maghrib           ‫ﻣﻐرب‬              8:10 PM            ✅               ✅             Push +     On time / Qada /
                                                                                      banner          Missed
 Isha              ‫ﻋﺷﺎء‬              9:40 PM            ✅               ✅             Push +     On time / Qada /
                                                                                      banner          Missed
* Approximate for Sterling, VA in April. Calculated daily by adhan-py using ISNA method.




Module 17 — Quran & Arabic Backend
    •      Al Quran Cloud API + Quran.com API: verse text, word-level data, translations, audio
    •      SM-2 spaced repetition for hifz scheduling; streak logic across prayer + Quran + Arabic activity


Module 18 — Arabic Learning UI
    •      Phase 1: 28-letter guide with forms, audio (Web Speech API), canvas tracing
    •      Phase 2: verse-by-verse reader with transliteration and tap-to-hear audio


Confidential — Personal Use                                                                              Page 8

## Page 9

Personal Command Center v2.2 — Full Life Operating System

Module 19 — Hifz Tracker UI
    •   Flashcard quiz with SM-2 queue, progress bars (X/28 letters, X/6,236 ayahs), streak display



7. Pillar D — Family
Unchanged from v2.1. Modules 20–22.



Module 20 — Family Data Service
    •   Activity DB, project/milestone/task/dependency schema, Claude API suggestion endpoint
    •   Family members: daughter (10, interests: STEM, Art, Soccer) + wife (interests: business, side
        hustle, personal development)



Module 21 — Activity Planner UI
    •   AI suggests 3 activities/week per family member based on age + interests; you approve or skip
    •   Kanban activity board: Planned / In Progress / Done. Photo upload per completed activity.



Module 22 — Side Hustle PM UI
    •   Full PM: projects, milestones, tasks, dependencies. Board view (Trello-style) + Timeline view
        (Gantt).
    •   Weekly Claude project health summary (‘You have 3 overdue tasks and 2 milestones at risk’)



8. Pillar E — Entertainment
Unchanged from v2.1. Module 23.



Module 23 — Entertainment Queue Service
    •   YouTube Data API v3: subscription-based, interest-tagged, 30-min daily playlist via Claude
        curation
    •   Podcast RSS + iTunes Search API: episode library, in-app player (speed control, 15s skip,
        sleep timer)
    •   Apple Podcasts handoff via podcast:// URL deep link
    •   Unified queue view rebuilt each morning alongside Today dashboard refresh



9. Complete Module List — v2.2 (24 Modules)


Confidential — Personal Use                                                            Page 9

## Page 10

Personal Command Center v2.2 — Full Life Operating System

  #      Pillar            Module                        Description                           Key Tech
01     Markets    Project Scaffold          Monorepo, Docker Compose,.env,            Docker, Caddy, Python,
                                            Caddy config                               Node
02     Markets    Market Data Service       Yahoo Finance + Alpha Vantage +            yfinance, FastAPI, Redis
                                            Finnhub. Redis cache. TimescaleDB
                                            OHLCV.
03     Markets    Macro Data Service        FRED: CPI, PCE, unemployment,              FRED API, FastAPI
                                            payrolls. 6hr cache.
04     Markets    News Aggregation          NewsAPI by topic + symbol. URL             NewsAPI, Redis SET
                                            dedup. Keyword sentiment.
05     Markets    Portfolio Manager         CRUD positions. Live P&L. Target sell      PostgreSQL, FastAPI
                                            price + margin.
06     Markets    Signal Engine             Plugin scorer + weight store + hourly      Claude API, PostgreSQL
                                            Claude narrative.
07     Markets    Unified Inbox Digest      Gmail OAuth + Graph API + TDx              Google API, Graph API
                                            tickets. AI priority summary.
08     Markets    Google Keep Integration   gkeepapi reader. Date regex.               gkeepapi, Python
                                            Upcoming reminders endpoint.
09     Markets    Schwab Sync               OAuth 2.0 position sync to portfolio       Schwab API, OAuth 2
                                            table. Daily P&L.
10     Markets    Markets Frontend          Market, Portfolio, News, Deep Dive,        Next.js, Tailwind,
                                            Signal Config pages. Responsive.           Recharts
11     Markets    Docker + Deployment       Final compose.yml, Caddyfile HTTPS,        Docker Compose, Caddy
                                            deploy.sh zero-downtime.
12     Health     iOS HealthKit Companion   SwiftUI: HealthKit read, POST to           SwiftUI, HealthKit, APNs
                                            backend, APNs prayer + morning push
                                            notifications.
13     Health     Health Data Service       HealthKit ingest, TimescaleDB,             FastAPI, TimescaleDB,
                                            calorie/macro endpoints, USDA food         USDA
                                            search.
14     Health     Exercise Tracker          Weekly targets, workout log, AI plan,      FastAPI, Claude API
                                            VO2/HR zones. Exposes today's
                                            workout to Module 24.
15     Health     Health Frontend           Today health card, calorie ring, sleep     Next.js, Recharts
                                            chart, exercise rings, weight chart.
16     Spirit.    Prayer, Adhan & Salah     adhan-py ISNA calc, Mishary Al-Afasy       adhan-py, FastAPI, APNs
                                            audio, tri-channel reminders, salah log,
                                            Jumu'ah, rings.
17     Spirit.    Quran & Arabic Backend    Al Quran Cloud + Quran.com APIs.           FastAPI, PostgreSQL,
                                            SM-2 spaced repetition. Streaks.           Redis
18     Spirit.    Arabic Learning UI        Letter guide, canvas tracing,              Next.js, Canvas API,
                                            pronunciation audio, verse reader.         Web Speech
19     Spirit.    Hifz Tracker UI           Flashcard quiz, spaced repetition          Next.js, shadcn/ui
                                            queue, progress bars, streak display.
20     Family     Family Data Service       Activity DB, project/milestone/task        FastAPI, PostgreSQL,
                                            schema. Claude AI suggestion               Claude API
                                            endpoint.
21     Family     Activity Planner UI       Daughter + wife boards. AI suggestion      Next.js, DnD, shadcn/ui
                                            inbox. Kanban completion + photo log.
22     Family     Side Hustle PM UI         Project board, Gantt milestones, task      Next.js, Recharts, Claude
                                            dependencies, weekly AI health             API
                                            summary.

Confidential — Personal Use                                                                           Page 10

## Page 11

Personal Command Center v2.2 — Full Life Operating System

23 Entertainment Entertainment Queue       YouTube Data API + Podcast RSS. 30-       YouTube API, iTunes
                 Service                   min queue builder. In-app audio player.   API, FastAPI
24       Morning Morning Routine          Sleep-aware + mood-aware daily            FastAPI, Claude API,
                 Intelligence             music/caffeine/breakfast                  adhan-py
                                          recommendations. Claude narrative.
                                          Feedback learning loop.




10. Complete Database Schema (v2.2)
Markets
     •   positions: id, symbol, shares, purchase_price, purchase_date, target_sell_price,
         profit_margin_pct, notes
     •   transactions: id, symbol, type, shares, price, date
     •   signal_weights: id, plugin_name, weight, updated_at
     •   signal_history (TimescaleDB): time, symbol, score, breakdown_json, narrative
     •   news_articles: id, url_hash, title, source, published_at, topics_json, sentiment_score



Health
     •   health_metrics (TimescaleDB hypertable): time, metric_type, value, source
     •   daily_health_rollup: date, steps, active_cal, resting_cal, swim_min, walk_min, weight_kg,
         sleep_min, sleep_quality
     •   food_log: id, date, food_name, calories, protein_g, carbs_g, fat_g, created_at
     •   exercise_log: id, date, type, duration_min, sets_json, notes
     •   health_goals: metric, target_value, target_date, created_at



Prayer
     •   prayer_times: id, date, fajr, dhuhr, asr, maghrib, isha, calculation_method, latitude, longitude,
         created_at
     •   prayer_log: id, date, prayer, status (on_time/qada/missed), location (masjid/home/work/travel),
         notes, logged_at
     •   jumuah_log: id, date, location, imam, confirmed_time, khutba_notes, logged_at
     •   prayer_settings: id, calculation_method, asr_method, latitude, longitude, adhan_volume,
         muted_prayers_json, leave_early_minutes



Spiritual
     •   arabic_letters: id, letter, name, forms_json, audio_url, mastered_at
     •   letter_practice_log: id, letter_id, date, score, duration_sec
     •   quran_progress: id, surah, ayah, status, next_review_date, interval_days, ease_factor
     •   spiritual_streaks: date, activity_type, minutes_logged



Confidential — Personal Use                                                                      Page 11

## Page 12

Personal Command Center v2.2 — Full Life Operating System

Morning Routine (NEW in v2.2)
    •    morning_log: id, date, sleep_duration_min, sleep_quality_score, sleep_tier, mood_inferred,
         mood_selected, music_genre_recommended, music_genre_used, caffeine_recommended,
         caffeine_used, breakfast_recommended, breakfast_used, claude_narrative, created_at
    •    morning_ratings: id, morning_log_id, rating (up/down), note, rated_at
    •    morning_preferences: id, sleep_tier, mood, music_genre_override, caffeine_override,
         breakfast_override, confidence_score, last_updated
    •    morning_music_playlists: id, genre, label, youtube_url, description, active


Family
    •    family_members: id, name, relationship, interests_json, birth_date
    •    activity_ideas: id, member_id, title, description, category, materials, duration_min, ai_generated,
         approved, created_at
    •    activity_log: id, idea_id, completed_date, notes, photo_url
    •    projects: id, name, description, goal, target_date, status
    •    milestones: id, project_id, title, target_date, completed_at
    •    tasks: id, milestone_id, title, owner, due_date, status, priority, blocking_task_ids_json



Entertainment
    •    podcast_feeds: id, title, rss_url, interest_tags_json, last_fetched
    •    podcast_episodes: id, feed_id, title, audio_url, duration_sec, published_at,
         playback_position_sec, completed
    •    youtube_channels: id, channel_id, title, interest_tags_json
    •    entertainment_queue: id, date, item_type, item_id, order, completed



11. Complete Data Source Registry

        Source              Cost              Data                  Limit             Use Case
Yahoo Finance        Free           Quotes, OHLCV          Unlimited         Primary market data
(yfinance)
Alpha Vantage        Free           RSI, MACD, OHLCV       25/day            Technical indicators
FRED API             Free           CPI, PCE, jobs         Unlimited         Macro data
NewsAPI              Free           Global news            100/day           Market & sector news
Finnhub              Free           VIX, earnings          60/min            Volatility data
Polygon.io           ~$29           Options, futures       Unlimited         Options deep dive
Apple HealthKit      Free           Activity, sleep, HR,   Device-local      All health + morning sleep
                                    weight                                   input
USDA FoodData        Free           600k+ foods with       3,600/hr          Calorie logging
Central                             macros



Confidential — Personal Use                                                                    Page 12

## Page 13

Personal Command Center v2.2 — Full Life Operating System

adhan-py (local       Free             Prayer time calc (ISNA)    Local, no API         Prayer times for all 5
library)                                                                                prayers
cdn.islamic.network   Free             Mishary Al-Afasy adhan     CDN                   Adhan playback for 5
                                       MP3s                                             prayers
Al Quran Cloud API    Free             Quran text + audio         Unlimited             Quran recitation + morning
                                                                                        audio
Quran.com API         Free             Word-level data            Generous              Word-by-word reading
YouTube Data API      Free             Subscriptions, videos      10k units/day         Entertainment queue + music
v3                                                                                      playlists
iTunes Search API     Free             Podcast directory          Unlimited             Podcast search
Claude API (Sonnet    ~$3/mo           LLM inference              Per token             Signal narrative, activity
4)                                                                                      suggestions, morning
                                                                                        routine reasoning, learning
                                                                                        loop




12. Updated Monthly Cost Estimate (v2.2)

Item                                     Cost/mo                 Notes
Yahoo Finance / FRED / Finnhub /        Free                     Core data — zero cost
Quran / iTunes / adhan audio / adhan-py
Alpha Vantage                            Free                    25 calls/day covers indicators
NewsAPI                                  Free                    100 calls/day sufficient
USDA FoodData Central                    Free                    3,600 req/hr — far more than needed
YouTube Data API v3                      Free                    10k units/day covers subscription reads + music
                                                                 playlists
Claude API — market signal narrative     ~$1.50/mo               ~1,000 calls/mo at Sonnet pricing
(hourly)
Claude API — morning routine (1          ~$0.10/mo               30 morning calls + 4 weekly analysis calls
call/morning + weekly learning)
Claude API — activity suggestions +      ~$1.40/mo               Family + side hustle weekly summaries
project health
Claude API — total                       ~$3/mo                  All pillars combined
Polygon.io (optional — options data)     ~$29/mo                 Only if real-time options chain needed
VPS hosting (Phase 2, optional)          $0–$5/mo                GCP free tier or Hetzner CX11
TOTAL — Phase 1 baseline (no             ~$3/mo                  All 6 pillars + 24 modules running
options, no VPS)
TOTAL — Phase 2 full (options data + ~$37/mo                     Full feature set, self-hosted HTTPS
VPS)




13. Recommended Build Order for Cursor

Group 1 — Foundation

Confidential — Personal Use                                                                               Page 13

## Page 14

Personal Command Center v2.2 — Full Life Operating System
    1. Module 01: Scaffold — Docker Compose, folder structure,.env
    2. Module 02 + 03: Market data + Macro data
    3. Module 13: Health data service + TimescaleDB schema (morning routine reads from this)


Group 2 — Core backends (parallelize freely)
    4. Module 05: Portfolio Manager
    5. Module 04: News Aggregation
    6. Module 16: Prayer, Adhan & Salah — build early so prayer times feed Today dashboard
    7. Module 17: Quran & Arabic backend
    8. Module 20: Family data service
    9. Module 23: Entertainment queue service
    10. Module 24: Morning Routine Intelligence — depends on Module 13 (sleep data) and Module 14
        (workout schedule)



Group 3 — Intelligence layer
    11. Module 06: Signal Engine (depends on 02, 03, 04)
    12. Module 14: Exercise Tracker + AI weekly plan (depends on 13; exposes workout schedule to
        Module 24)



Group 4 — Integrations
    13. Module 07: Gmail + Outlook + TDx digest
    14. Module 08: Google Keep
    15. Module 09: Charles Schwab sync
    16. Module 12: iOS companion app (SwiftUI — separate Xcode project; delivers HealthKit data,
        prayer APNs, and 6 AM morning push)



Group 5 — Frontend (build last)
    17. Module 10: Markets frontend
    18. Module 15: Health frontend
    19. Module 18 + 19: Arabic learning + Hifz tracker UI
    20. Module 21 + 22: Family activity planner + Side hustle PM
    21. Morning Routine screen UI (part of Module 24): sleep banner, mood picker,
        music/caffeine/breakfast cards, Claude narrative, rating prompt
    22. Today Dashboard: build last — aggregates prayer times, morning routine card, and all pillar
        summaries


Group 6 — Deployment
    23. Module 11: Final Docker Compose, Caddy, deploy.sh zero-downtime script

Confidential — Personal Use                                                           Page 14

## Page 15

Personal Command Center v2.2 — Full Life Operating System




14. Cursor Session Templates
Standard session header (all modules)
Stack: Next.js 14 / FastAPI / PostgreSQL+TimescaleDB / Redis / Docker Compose. This is a
personal life OS called PCC with 6 pillars: Markets, Health, Spiritual, Family, Entertainment,
Morning Routine. We are on Module [N]: [Name]. Here is the DB schema: [paste]. Here are
prior API contracts: [paste]. Build only this module. Write pytest tests for all
endpoints. Do not modify other modules.



Module 16 — Prayer Cursor prompt
Build the Prayer, Adhan & Salah module. Use adhan-py (pip install adhan) with ISNA
method, coordinates 38.9898,-77.3897 (Sterling VA). Adhan: Mishary Al-Afasy from
cdn.islamic.network; Fajr version includes al-salatu khayrun min al-nawm. APScheduler:
schedule WebSocket pushes 20 min before each prayer and at prayer time. POST
/api/prayer/log: {prayer, status (on_time/qada/missed), location
(masjid/home/work/travel), notes}. Fridays: replace dhuhr with jumuah (Adams Center,
46903 Sugarland Rd Sterling VA, imams: Mohammed Majed / Abd Ar-Rafa Ouertani,
configurable leave_early_minutes default 60). 4 DB tables: prayer_times, prayer_log,
jumuah_log, prayer_settings.



Module 24 — Morning Routine Cursor prompt
Build the Morning Routine Intelligence module. Inputs: (1) prior night HealthKit sleep
from health_metrics TimescaleDB table, (2) user mood
(energized/neutral/tired/stressed/calm). Sleep tiers: Excellent >=7.5hrs, Good 6-7.5hrs,
Poor <6hrs. Decision matrix: Poor -> strong coffee + high protein + lofi/quran.
Good+tired -> 1 cup coffee + warm breakfast + lofi. Good+energized -> green tea or
coffee + protein + classic rock or upbeat. Excellent+calm -> green tea + warm
traditional + quran or nasheed. After rule engine, call Claude API (sleep_duration,
sleep_tier, mood, yesterday_rating, today_prayer_times, today_workout_scheduled) for 2-3
sentence narrative. Weekly APScheduler job: Claude analyzes 7 days of ratings, updates
morning_preferences table. Endpoints: GET /api/morning/recommendation, POST
/api/morning/mood, POST /api/morning/log, POST /api/morning/rating, GET
/api/morning/history. 4 DB tables: morning_log, morning_ratings, morning_preferences,
morning_music_playlists.


Module 12 iOS note: open a separate Xcode project. App reads HealthKit and POSTs to http://[local-
ip]:8000/api/health/ingest. Register for APNs: deliver prayer 20-min alerts as time-sensitive notifications, and
deliver the 6:00 AM morning routine push with a deep link to the Morning Routine screen. No App Store
submission required — install via Xcode direct device install.




                              Personal Command Center v2.2 — Full Life OS — April 2026




Confidential — Personal Use                                                                      Page 15
