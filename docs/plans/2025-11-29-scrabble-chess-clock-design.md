# Scrabble Chess Clock - Design Document

**Date:** 2025-11-29
**Purpose:** Multi-player Fischer chess clock for family Scrabble games on iPad

## Overview

A single-file HTML web app that provides a chess clock for 2-4 players with Fischer increment support. Optimized for iPad use with large touch targets and simple controls.

## Architecture

**Technology:** Single HTML file containing all HTML, CSS, and JavaScript. No external dependencies or build process.

**Deployment:** Open directly in Safari on iPad - no server required.

## Layout & Interface

### Main Clock Display
- **Player Sections:** 2-4 sections stacked vertically (equal height)
- Each section shows:
  - Player name (custom entered)
  - Current time in MM:SS format (large monospace font, 5-6em)
  - Entire section is a tap target to end turn
- **Active player:** Bright green background (#27ae60), subtle pulse animation
- **Inactive players:** Dark gray background (#2c3e50)
- **Warning state (<1 min):** Orange background (#e67e22)
- **Time's up:** Red background (#e74c3c), "TIME'S UP!" message

### Control Bar
- Located at bottom of screen
- **Start/Pause button:** Green when ready, orange when paused
- **Reset button:** Red, with confirmation dialog
- **Settings icon (gear):** Top-right corner
- Optional: Total elapsed game time display

### Settings Panel
- Slides in from right side
- Semi-transparent overlay behind
- Close by tapping outside or X button

**Configuration Options:**
- **Player Names:** 4 text inputs (Player 1-4)
  - Blank = player not used
  - Minimum 2 players required
- **Initial Time:** Input in minutes (default: 25)
  - Range: 1-999 minutes
- **Increment:** Input in seconds (default: 0)
  - Range: 0-999 seconds
- **Optional tick sound:** Toggle

**Settings Behavior:**
- Only editable when game not active
- If game paused: "Reset game to change settings?" warning
- All settings persist in localStorage

## Game Flow

### Setup
1. App loads with settings panel open
2. User enters player names (at least 2)
3. Configures initial time and increment
4. Tap "Start Game" to begin

### Clock Mechanics (Fischer-style)
1. All clocks start at initial time, paused
2. Tap Start - first active player's clock begins
3. Player taps their own section when turn ends
4. This triggers:
   - Stop their clock
   - Add increment to their time
   - Start next player's clock
5. Rotation: Player order based on non-blank name slots (1→2→3→4→1...)

### Time Runs Out
- At 0:00: Play beep sound, show "TIME'S UP!", red background
- Clock stops for that player
- Other players continue

### Pause/Resume
- Pause stops active clock (for breaks)
- Resume continues from paused state

### Reset
- Shows confirmation: "Are you sure? This will reset all clocks"
- Returns all clocks to initial time
- Returns to pre-game state

## Visual Design

### Color Scheme
- Inactive: #2c3e50 (dark gray)
- Active: #27ae60 (green)
- Warning: #e67e22 (orange)
- Time's up: #e74c3c (red)
- Control bar: #34495e (dark blue-gray)
- Text: White throughout

### Typography
- Player names: 2-3em, bold
- Time display: 5-6em, monospace
- Buttons: Medium, clear labels
- All fonts scale responsively

### Responsive Design
- Optimized for landscape, works in portrait
- Player sections scale equally to fill viewport
- Font sizes scale based on screen size

## Technical Features

### Error Handling
- Validate minimum 2 players before start
- Validate time range (1-999 minutes)
- Validate increment range (0-999 seconds)
- Debounce player button taps
- Show clear error messages

### Audio
- **Time's up beep:** Web Audio API generated tone
- **Optional tick sound:** Quiet, toggleable
- Respects device volume

### Screen Wake Lock
- Prevent iPad sleep during active game
- Use Screen Wake Lock API
- Release on pause/reset
- Graceful fallback if unsupported

### Polish
- Smooth transitions between player turns
- Haptic feedback on taps (if supported)
- Minimal, clean interface
- No text selection, no zoom (touch optimized)

### Data Persistence
- Settings stored in localStorage
- Remembered on next app open

## Browser Compatibility

**Primary Target:** Safari on iPad
**Fallbacks:** Graceful degradation for Wake Lock API

## Implementation Notes

- Single `index.html` file
- Vanilla JavaScript (no frameworks)
- CSS animations for pulse effect
- Web Audio API for sound
- Screen Wake Lock API for screen control
- localStorage for persistence
