# PCC v22 UI/UX Design Specification

## Overview
This document captures the UI/UX direction for the Personal Command Center (PCC) v2.2 application based on the interactive design interview. It is intended to guide design, frontend implementation, and future iteration across web and mobile experiences.

## Product Context
PCC is a personal life operating system spanning multiple pillars:
- Markets
- Health
- Spiritual
- Family
- Entertainment
- Morning Routine

The design must support:
- desktop/laptop use
- iPad/tablet use
- iPhone/mobile use
- adaptive light/dark mode
- a highly customizable dashboard experience

## Core Design Principles
1. Clean and calm, not sterile
2. Friendly and personal, not playful to the point of distraction
3. Information-rich, but adaptable by screen size
4. Strong daily dashboard orientation
5. Modular, customizable, and scalable
6. Morning-focused intelligence without dominating the whole app all day
7. Spiritual and personal tone should feel grounded and respectful

## Visual Style Direction
The selected visual direction is a blend of:
- Minimalist
- Friendly / colorful

### Interpretation
- minimalist layout foundation
- generous whitespace
- soft color accents
- icon-forward UI where helpful
- clean card structure
- approachable, modern surfaces
- avoid overly loud gradients or overly enterprise-like severity

## Theme System
### Selected Direction
Adaptive theme with:
- Light mode default
- Dark mode available via user selection

### Requirements
- support both light and dark themes from the start
- respect system theme where appropriate
- allow explicit user override in settings
- retain hierarchy and visual consistency across both themes

### Theme Guidance
#### Light mode
- primary default experience
- bright background
- soft card surfaces
- subtle shadows or borders
- pastel/pillar accent colors used lightly

#### Dark mode
- reduced glare, calm dark surfaces
- muted accent tones rather than neon
- maintain readability and hierarchy
- preserve emotional warmth, especially for spiritual and morning features

## Navigation
### Primary Navigation
- Left sidebar navigation
- customizable ordering/visibility
- icon + label presentation

### Sidebar Sections
Recommended top-level items:
- Today
- Markets
- Health
- Spiritual
- Family
- Entertainment
- Settings

### Sidebar Style
- icon + label
- clean and scan-friendly
- lightweight, not oversized
- consistent icon treatment
- support future customization or reordering

## Dashboard / Landing Page
### Primary Role
The landing page should act as a high-level personal command dashboard.

It should show:
- summary
- urgency
- highest-priority item
- quick status by pillar

### Dashboard Philosophy
The user explicitly wanted:
- a landing page showing summary/high-priority item from each category
- a customizable experience
- adaptability across iPhone, iPad, and laptop

### Dashboard Organization
Selected direction:
- fully customizable dashboard

Supported behaviors:
- pin cards
- reorder cards
- hide cards
- resize cards
- establish user-specific priority

### Customization Entry
Selected direction:
- dedicated "Customize Dashboard" mode

This means:
- customization should not clutter the normal dashboard
- user enters a clear edit mode
- cards expose drag/reorder/resize/hide controls inside edit mode

## Card System
### Layout Style
Selected direction:
- mixed priority cards

### Meaning
- large cards for important/high-priority content
- smaller cards for secondary information
- daily rhythm should influence prominence
- not all modules deserve equal space every day

### Recommended Dashboard Hierarchy
Likely card hierarchy:
1. Prayer Times
2. Morning Routine
3. Health summary
4. Markets summary
5. Family summary
6. Entertainment summary
7. Spiritual progress summary if not already represented elsewhere

### Density
Selected direction:
- adaptive density by device/screen size

#### Implementation guidance
- default density: balanced
- laptop/desktop: can show more cards and denser layout
- tablet: balanced with moderate spacing
- phone: prioritize readability, stacked cards, fewer columns
- optional compact mode may be introduced later if desired

## Morning Routine Card
### Importance
Selected direction:
- blend of "slightly emphasized" and "time-based prominence"

### Behavior
- Prayer Times remains above Morning Routine
- Morning Routine is one of the larger dashboard cards
- Morning Routine is more visually prominent in the morning
- later in the day it should compress into a smaller summary card

### Morning card content
Collapsed dashboard version should likely show:
- sleep score/tier badge
- mood selector or selected mood
- summary recommendation:
  - music
  - breakfast
  - caffeine
- short narrative line
- entry point to full screen

## Interaction Model
### Device-specific interaction rules
#### Mobile and tablet
- gestures/swipes are encouraged
- long-press can reveal secondary actions where appropriate
- use bottom sheets, contextual reveals, and touch-friendly controls

#### Desktop
- buttons + icon chips
- clearer visible affordances for primary actions
- contextual secondary controls may still exist

### Design principle
Critical actions should remain obvious:
- log prayer
- select mood
- play recommendation
- log breakfast
- log caffeine
- open detail screens

Less critical actions can be contextual.

## Mood Selector
### Selected direction
Adaptive by screen size.

#### Mobile
- compact icon row

Example:
- Energized
- Neutral
- Tired
- Stressed
- Calm

#### Tablet/Desktop
- icon + label chips

This improves:
- speed on smaller devices
- clarity on larger screens

## Color System
### Selected direction
Hybrid system:
- neutral base
- subtle pillar colors only where helpful

### Guidance
Base UI:
- neutral background
- white/light cards in light mode
- dark muted cards in dark mode

Pillar color use:
- icon accents
- badges
- section markers
- chart highlights
- small emphasis UI
- avoid making every card a solid color block

### Suggested pillar accent approach
- Markets: muted blue
- Health: soft green
- Spiritual: subdued olive/gold
- Family: warm coral or terracotta accent
- Entertainment: restrained purple
- Morning Routine: sunrise amber / warm yellow accent

## Shape Language
### Selected direction
Hybrid softness:
- cards softly rounded
- chips/buttons more rounded than cards

### Guidance
- main cards: rounded rectangle
- controls: pill or capsule where appropriate
- avoid harsh corners
- avoid excessive bubble/pill styling across everything

## Typography
### Selected direction
Hybrid typography:
- clean, readable modern UI font
- slightly more character in headings
- restrained body text

### Guidance
- body text should optimize for dashboard readability
- heading style should add warmth/personality without becoming decorative
- maintain accessibility and strong hierarchy

## Responsive Design Rules
### iPhone
- stacked cards
- compact summary
- gesture-friendly controls
- mood selector in icon-only form
- bottom sheets for details where appropriate

### iPad / tablet
- more spacious than phone
- can support 2-column dashboard layouts
- gesture-friendly but more visible controls than phone
- mood selector can shift toward icon + label

### Laptop / desktop
- left sidebar visible
- mixed-size dashboard grid
- buttons + icon chips
- more persistent summary information visible
- larger customization surface in dashboard edit mode

## Terminology Update
The project naming should be updated from:
- Media

to:
- Entertainment

This applies to:
- sidebar label
- dashboard card label
- documentation
- future UI copy unless a later naming decision overrides it

## Default Dashboard Behavior
Even though the dashboard is customizable, the default layout should emphasize:
1. Prayer Times
2. Morning Routine
3. Health
4. Markets
5. Family
6. Entertainment
7. Secondary spiritual or progress widgets

## Accessibility Guidance
- maintain adequate color contrast in light and dark modes
- do not rely on color alone for status
- support labels with icons
- ensure touch targets are large enough on mobile/tablet
- preserve clarity in compact dashboard states
- allow keyboard access for dashboard editing on desktop

## Implementation Notes for Frontend
### Recommended UX patterns
- responsive card grid
- dedicated dashboard customization mode
- drag-and-drop reordering
- hide/show controls in edit mode
- per-device interaction tuning
- time-aware Morning Routine prominence
- sidebar icon + label
- theme toggle in settings and/or header menu

### Risks to avoid
- too many accent colors competing visually
- overloading cards with excessive detail
- treating phone like shrunken desktop
- hiding critical actions behind too many gestures
- making customization always visible and cluttered

## Design Summary
PCC should feel like:
- a calm but capable personal operating system
- respectful of spiritual rhythm
- practical for daily life management
- adaptable across devices
- customizable without becoming chaotic

The final aesthetic direction is:
- minimalist foundation
- friendly visual accents
- neutral base with subtle pillar colors
- adaptive layout and density
- dashboard-first architecture
- device-appropriate interactions
