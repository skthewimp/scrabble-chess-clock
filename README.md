# Scrabble Chess Clock

A multi-player Fischer chess clock designed for family Scrabble games on iPad. Simple, clean interface with large touch targets optimized for tablet use.

## Features

- **2-4 Player Support** - Configurable number of players by entering names
- **Fischer Clock** - Adds configurable increment after each move
- **Large Touch Interface** - Giant "NEXT PLAYER" button for easy tapping
- **Visual Feedback** - Active player highlighted in green with pulse animation
- **Time Warnings** - Orange background when under 1 minute remaining
- **Audio Alert** - Beep sound when time runs out
- **Screen Wake Lock** - Keeps iPad screen on during games
- **Settings Persistence** - Remembers player names and time settings
- **Elapsed Time Display** - Shows total game duration

## How to Use

### Setup

1. **Transfer to iPad**: Send `scrabble_clock.html` to your iPad via AirDrop, email, or cloud storage
2. **Open in Safari**: Double-tap the file to open it in Safari
3. **Optional**: Add to Home Screen for app-like experience
   - Tap the Share button in Safari
   - Select "Add to Home Screen"

### Configuration

1. When you first open the app, the settings panel appears
2. **Enter Player Names**: Fill in 2-4 player names (leave blank to exclude)
3. **Set Initial Time**: Time per player in minutes (default: 25)
4. **Set Increment**: Seconds added after each move (default: 0)
5. Tap **Start Game**

### Playing

1. Tap **Start** to begin the first player's clock
2. When a player finishes their turn, tap the large **NEXT PLAYER** button
3. This adds the increment to their time and starts the next player's clock
4. Use **Pause** for breaks (restarts with Resume)
5. Use **Reset** to restart all clocks

### Controls

- **NEXT PLAYER** (large blue button) - End current turn, start next player
- **Start/Pause** - Begin game or pause all clocks
- **Reset** - Reset all clocks to initial time (with confirmation)
- **⚙️** (gear icon) - Open settings panel

## Visual States

- **Gray** - Inactive player
- **Green (pulsing)** - Active player's turn
- **Orange** - Less than 1 minute remaining
- **Red** - Time's up! (with "TIME'S UP!" message)

## Technical Details

### Technology

- Single HTML file - no dependencies or build process
- Vanilla JavaScript (ES6+)
- CSS3 animations
- Web Audio API for sound
- Screen Wake Lock API for keeping screen on
- LocalStorage for settings persistence

### Browser Compatibility

- **Primary Target**: Safari on iPad
- **Also Works**: Modern desktop browsers (Chrome, Firefox, Edge, Safari)
- Screen Wake Lock may not be supported on all browsers (degrades gracefully)

### File Structure

```
scrabble/
├── scrabble_clock.html    # Main application file
├── README.md              # This file
└── docs/
    └── plans/
        └── 2025-11-29-scrabble-chess-clock-design.md  # Design document
```

## Customization

All settings are in the HTML file and can be modified:

- **Colors**: Search for color codes (e.g., `#3498db`) in the `<style>` section
- **Default Time**: Change `value="25"` in the initial-time input
- **Default Increment**: Change `value="0"` in the increment input
- **Font Sizes**: Adjust `clamp()` values in CSS for responsive sizing

## Fischer Clock Explained

A Fischer clock adds time after each move:
- **Initial Time**: Starting time for each player (e.g., 25 minutes)
- **Increment**: Bonus time added after completing a turn (e.g., 15 seconds)

Example with 25 minutes + 15 second increment:
1. Player starts with 25:00
2. Player takes 2 minutes for their turn (23:00 remaining)
3. Player taps NEXT PLAYER
4. 15 seconds added → 23:15 remaining
5. Next player's turn begins

## Tips for Scrabble

Recommended settings for different game types:

### Casual Family Game
- Initial Time: 25 minutes
- Increment: 0 seconds
- Simple countdown, no bonus time

### Speed Scrabble
- Initial Time: 10 minutes
- Increment: 5 seconds
- Fast-paced with small bonus

### Tournament Style
- Initial Time: 25 minutes
- Increment: 15 seconds
- Rewards quick thinking

## Troubleshooting

**Screen goes to sleep during game**
- Screen Wake Lock API may not be supported
- Manually adjust iPad settings: Settings → Display & Brightness → Auto-Lock → Never

**Sound doesn't play**
- Check iPad is not in silent mode
- Check volume is turned up
- Some browsers require user interaction before playing audio

**Settings don't save**
- Browser may be in Private/Incognito mode
- LocalStorage disabled in browser settings

**Player clicks not working**
- Use the large NEXT PLAYER button instead
- Reload the page if issues persist

## License

Free to use and modify for personal and family use.

## Credits

Built with Claude Code for family Scrabble games.
