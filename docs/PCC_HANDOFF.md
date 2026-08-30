# PCC Implementation Handoff

This handoff translates the design and build-plan docs into implementation-ready guidance for frontend, backend, data, and QA work.

## 1. Source Documents

- `docs/DESIGN.md`: canonical UI design system and responsive behavior.
- `docs/DESIGN.md.claude`: design interview synthesis and naming updates.
- `docs/pcc_v2.4_build_plan.md`: most current build-plan source, including Entertainment naming.
- `docs/pcc_v2.3_build_plan.md` and `docs/pcc_v22_build_plan.md`: prior build-plan context.
- `docs/pcc_build_plan.docx`: earlier v1 markets/productivity build plan.

## 2. Product Direction

PCC is a dashboard-first personal operating system. The app should open to Today, not a marketing page. Prayer is the primary anchor, Morning Routine is the newest intelligence surface, and the remaining pillars, including Planning, Work, Health, Family, and Fun, supply concise daily summaries with deep links.

Use `Fun > Entertainment`, not top-level `Media`, in UI and new docs/code unless maintaining backward-compatible database names during migration.

## 3. Suggested Stack

- Frontend: Next.js 14, React, Tailwind CSS, shadcn/ui, Recharts, Zustand.
- Backend: FastAPI, APScheduler, Redis, PostgreSQL 15, TimescaleDB.
- Mobile companion: SwiftUI + HealthKit + APNs.
- Deployment: Docker Compose locally, optional Caddy HTTPS on VPS/GCP.
- LLM: Claude API for sparse narrative and weekly analysis calls.

## 4. Frontend Shell

### Desktop

- Fixed left sidebar, 240px.
- Main content max width around 1200px.
- Today hero layout: prayer card 60%, summary column 40%.
- Hover states and keyboard-accessible controls enabled.

### Tablet

- Collapsible left sidebar, 240px expanded or 60px rail.
- Two-column card grid.
- Centered modals for detail views.

### Mobile

- Bottom tab navigation.
- One-column stacked cards.
- Full-screen overlays or bottom sheets for details.
- Mood selector can use icon-only compact controls.

## 5. Visual Tokens

```css
:root {
  --bg-page: #F9F7F4;
  --bg-card: #FFFFFF;
  --bg-sidebar: #F4F1EE;
  --border-subtle: #E8E4DF;
  --text-primary: #1A1612;
  --text-secondary: #6B6560;
  --text-tertiary: #A09890;
  --markets: #2D6A4F;
  --work: #5B677A;
  --planning: #6F5A8D;
  --health: #C1440E;
  --spiritual: #B5862A;
  --family: #D4883A;
  --morning: #E09B3D;
  --fun: #4A5C7A;
  --radius-card: 10px;
}
```

Typography:
- UI/body: Inter.
- Data: JetBrains Mono.
- Arabic: Amiri with `dir="rtl"` and `lang="ar"`.

## 6. Primary Screens

### Today Dashboard

Required sections:
- Header with greeting, date, location, and customize control.
- Prayer hero with next prayer, Arabic label, countdown, animated ring, mute, and five prayer statuses.
- Summary column for Health and Markets on desktop.
- Morning Routine card directly below prayer/summary area.
- Summary cards for Planning, Work, Spiritual, Family, Fun.
- Right Now strip with urgent chips.

### Planning

Required sections:
- Today plan with focus items, calendar commitments, due reminders, and cross-pillar priorities.
- Week view for upcoming work, family, health, spiritual, hobby, and travel commitments.
- Calendar view with a Sunday-through-Saturday grid in desktop paper-calendar style.
- Google Keep event-note importer/parser for a single configured note.
- Parsed event review surface that shows the source text, parsed date/time/title/location, and parser confidence.
- Backlog for personal tasks and ideas not yet scheduled.
- Source attribution and deep links for items originating in other pillars.
- Promote-to-Today action for any item.

### Work

Required sections:
- Priority digest combining Gmail, Outlook, Teams mentions, TeamDynamix tickets, Keep reminders, and calendar obligations.
- Today focus list with reviewed, deferred, and promoted states.
- Source chips and direct open-in-source actions for each item.
- Deadline and meeting urgency surfaced into the Right Now strip.
- Quiet dense layout with table/list treatment, restrained accenting, and no marketing-style panels.

### Health

Required subareas:
- Exercise: workout plan, weekly targets, cardio/strength logs, rings/charts, recovery cues, and workout schedule exposed to Morning Routine.
- Diet: calorie budget, food search/logging, macro tracking, hydration prompts, and breakfast logging from Morning Routine.
- Left navigation: Health is expandable/collapsible with a `+` control. Exercise and Diet are hidden until expanded.

### Fun

Required subareas:
- Hobby: lightweight tracker for creative interests, learning, reading, tinkering, and recreational projects.
- Music: playlists, listening preferences, mood/energy tags, and listening history.
- Entertainment: YouTube and podcast queue, interest tags, playback progress, in-app player, and external app handoff.
- YouTube Shorts: separate short-form queue, saved topics, time-boxing controls, and watch-history reflection.
- Fun Today card should summarize Hobby, Music, Entertainment, and YouTube Shorts without making them separate top-level left-nav items.
- Left navigation: Fun is expandable/collapsible with a `+` control.
- Hobby, Music, Entertainment, and YouTube Shorts each expose their own expandable `+` affordance so nested filters, saved lists, channels, playlists, or collections can be revealed later.

### Spiritual

Required subareas:
- Growth: reflection, goals, streaks, and progress insights across prayer consistency, Quran, Arabic, hifz, and character development.
- Left navigation: Spiritual is expandable/collapsible with a `+` control. Growth is hidden until expanded.

### Morning Routine Screen

Required sections:
- Sleep summary banner with duration, score, tier, and target-window deviation.
- Mood picker with five options.
- Claude narrative.
- Recommended music/audio card with play action.
- Quran shortcut always visible.
- Alternate genre tiles.
- Caffeine recommendation with Log and Skip.
- Breakfast recommendation with calorie/prep metadata and Log/Skip.
- Yesterday rating prompt.

### Dashboard Customize Mode

Required behaviors:
- Enter explicit edit mode.
- Show reorder, resize, hide/show, and pin controls only in edit mode.
- Save layout.
- Preserve sane defaults if no custom layout exists.

## 7. Backend Contracts

### Morning Routine

`GET /api/morning/recommendation`

Returns today's generated recommendation. Must respond quickly with rule-based output; Claude narrative may be cached or returned when available.

```json
{
  "date": "2026-08-30",
  "sleep": {
    "duration_min": 392,
    "quality_score": 82,
    "tier": "good",
    "target_window_deviation_min": 42
  },
  "mood": {
    "inferred": "neutral",
    "selected": "neutral"
  },
  "recommendation": {
    "music_genre": "classic_rock",
    "music_label": "Classic rock",
    "caffeine": "coffee_1_cup",
    "breakfast": "protein_shake_toast",
    "hydration_reminder": false
  },
  "narrative": "You slept well enough to keep the morning steady. A single coffee, protein-forward breakfast, and classic rock gives you momentum without overcorrecting.",
  "actions": {
    "can_log": true,
    "can_rate_yesterday": true
  }
}
```

`POST /api/morning/mood`

```json
{ "mood": "tired" }
```

`POST /api/morning/log`

```json
{
  "music_genre_used": "quran",
  "caffeine_used": "coffee_1_cup",
  "breakfast_used": "eggs"
}
```

`POST /api/morning/rating`

```json
{
  "morning_log_id": "uuid",
  "rating": "up",
  "note": "Classic rock worked better than lo-fi."
}
```

`GET /api/morning/history?days=30`

Returns logs and ratings for trend display.

`POST /api/morning/preferences/recalculate`

Triggers weekly Claude preference analysis.

### Prayer

`GET /api/prayer/today`

Returns all prayer times, next prayer, countdown metadata, status list, Jumu'ah replacement data when applicable, and mute state.

`POST /api/prayer/log`

```json
{
  "prayer": "asr",
  "status": "on_time",
  "location": "masjid",
  "notes": ""
}
```

### Dashboard

`GET /api/dashboard/today`

Aggregates prayer, morning, health, markets, work, planning, family, fun, spiritual progress, and Right Now chips.

`GET /api/dashboard/layout`

Returns layout config by device class.

`PUT /api/dashboard/layout`

Persists card order, size, visibility, and pinned state.

### Planning

`GET /api/planning/events?start=2026-08-30&end=2026-09-05`

Returns parsed planning events from the configured Keep note and other PCC sources.

```json
{
  "week_starts_on": "sunday",
  "source": "google_keep",
  "events": [
    {
      "id": "evt_2026_09_03_flight_tx",
      "date": "2026-09-03",
      "start_time": "19:27",
      "end_time": "22:01",
      "title": "Flight 4559 to TX",
      "location": null,
      "category": "travel",
      "status": "confirmed",
      "raw_text": "7:27 PM FLIGHT 4559 / Arrival 10:01 PM"
    }
  ]
}
```

`POST /api/planning/keep/sync`

Syncs the configured Google Keep note, stores the raw text, parses event sections, and returns parse warnings.

`GET /api/planning/calendar/week?date=2026-09-03`

Returns the Sunday-through-Saturday week containing the requested date, grouped by day for the paper-calendar UI.

## 8. Database Schema

### Morning Routine

```sql
CREATE TABLE morning_log (
  id UUID PRIMARY KEY,
  date DATE NOT NULL UNIQUE,
  sleep_duration_min INT,
  sleep_quality_score INT,
  sleep_tier TEXT NOT NULL,
  mood_inferred TEXT,
  mood_selected TEXT,
  music_genre_recommended TEXT,
  music_genre_used TEXT,
  caffeine_recommended TEXT,
  caffeine_used TEXT,
  breakfast_recommended TEXT,
  breakfast_used TEXT,
  claude_narrative TEXT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE morning_ratings (
  id UUID PRIMARY KEY,
  morning_log_id UUID NOT NULL REFERENCES morning_log(id),
  rating TEXT NOT NULL CHECK (rating IN ('up', 'down')),
  note TEXT,
  rated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE morning_preferences (
  id UUID PRIMARY KEY,
  sleep_tier TEXT NOT NULL,
  mood TEXT NOT NULL,
  music_genre_override TEXT,
  caffeine_override TEXT,
  breakfast_override TEXT,
  confidence_score NUMERIC(4, 3),
  last_updated TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE morning_music_playlists (
  id UUID PRIMARY KEY,
  genre TEXT NOT NULL UNIQUE,
  label TEXT NOT NULL,
  youtube_url TEXT,
  description TEXT,
  active BOOLEAN NOT NULL DEFAULT true
);
```

### Related Existing Tables

- `health_metrics` and `daily_health_rollup` feed sleep data.
- `exercise_log` feeds workout-aware breakfast logic.
- `food_log` receives confirmed breakfast/caffeine entries.
- `prayer_times`, `prayer_log`, `jumuah_log`, and `prayer_settings` feed prayer card and narrative context.
- Work digest tables should normalize source, external id, title, due time, priority, review state, and source URL across Gmail, Outlook, Teams, TeamDynamix, and Keep.
- Planning tables should support source attribution, due date, status, priority, pillar, and promoted-to-Today state.
- `planning_sources`: id, source_type, external_id, title, source_url, active, last_synced_at.
- `planning_raw_notes`: id, source_id, raw_text, content_hash, captured_at.
- `planning_events`: id, source_id, raw_note_id, event_date, start_time, end_time, title, location_name, address, category, status, raw_text, parser_confidence, promoted_to_today, created_at, updated_at.
- Fun tables should separate hobby tracking from the existing entertainment queue.
- `fun_entertainment_queue` or `entertainment_queue` should replace older `media_queue` naming in new work.

## 9. Recommendation Logic

Implement as deterministic rules first:

- Excellent + Energized: green tea, high protein, upbeat/classic rock.
- Excellent + Calm: green tea or none, warm traditional breakfast, Quran/nasheed.
- Good + Energized: one coffee, high protein, classic rock or lo-fi.
- Good + Tired/Stressed: one coffee, warm breakfast, Quran or instrumental.
- Poor: strong coffee, high protein, lo-fi/ambient or nasheed.
- Poor + Stressed: coffee plus water reminder, light protein, Quran.
- Overslept/skipped Fajr: immediate coffee, quick high protein, upbeat or energetic nasheed.

Then apply overrides from `morning_preferences`. Then request Claude narrative using sleep, mood, yesterday rating, prayer times, workout schedule, and final recommendation.

## 10. QA Checklist

- Today dashboard loads without requiring external paid services.
- Prayer countdown updates every second and never communicates urgency by color alone.
- Jumu'ah replaces Dhuhr on Fridays.
- Morning recommendation returns when Claude is unavailable.
- Work appears in desktop/tablet left navigation and has a Today summary card.
- Planning and Fun appear in desktop/tablet left navigation and have Today summary cards.
- Hobby, Music, Entertainment, and YouTube Shorts appear as Fun subareas, not separate top-level left-nav peers.
- Growth appears as a Spiritual subarea.
- Exercise and Diet appear as Health subareas.
- All left-nav sections with subareas can expand/collapse from a visible `+` control and remain keyboard accessible.
- Google Keep event note parses date-section formats with dashes, slashes, weekday labels, indented event lines, addresses, travel entries, arrivals, and cancellation markers.
- Planning Calendar view starts on Sunday, ends on Saturday, and visually matches a desktop paper calendar.
- Work digest items preserve source links and can be reviewed without deleting source data.
- Mood override updates recommendation and persists.
- Breakfast log updates food log with calories/macros when confirmed.
- Caffeine skip is stored without judgment copy or failure state.
- Dashboard customization controls are hidden outside edit mode.
- Mobile bottom tab does not overlap content or mini-player.
- Arabic text uses correct font, language, and direction attributes.
- Reduced motion preference disables decorative animations.

## 11. Build Order

1. Scaffold monorepo, Docker Compose, env templates, database, Redis.
2. Market and macro data services.
3. Health data service and HealthKit ingest schema.
4. Prayer, Adhan, and Salah module.
5. Core family and entertainment services.
6. Morning Routine backend after health/prayer contracts exist.
7. Intelligence layer for market signal and morning preference learning.
8. iOS companion app for HealthKit and push notifications.
9. Pillar frontends.
10. Today dashboard aggregator and customization mode.
11. Deployment hardening with Caddy and zero-downtime scripts.
