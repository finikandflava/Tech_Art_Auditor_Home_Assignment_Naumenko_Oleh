# 🐟 Lane Runner Game

> Modern HTML5 game with progressive level system, animations, and responsive design

## 📋 Description

**Lane Runner** is a dynamic arcade game where the player controls a character, moving between lanes and collecting coins while avoiding obstacles. The game features 5 levels of increasing difficulty with a unique balance and progression system.

### ✨ Key Features

- 🎮 **5 Difficulty Levels** with progressive balance
- 💎 **Collection System**: Coins (+1), Gems (+10), Hearts (health restore)
- 🎨 **Modern UI** with glassmorphism effects and gradients
- ✨ **Advanced Animations**: 
  - Smooth player movement with interpolation
  - Character rotation and bobbing
  - Particle system for collecting items
  - Screen shake effect on damage
  - Coin flight animation to counter
- 📊 **Player Statistics**: nickname, best time, total games, wins, win rate, max level
- 💾 **LocalStorage**: progress and statistics persistence
- 📱 **Responsive Design**: 100vh approach, works on mobile and desktop
- 🖼️ **Sprite System**: all objects rendered via images with fallbacks

## 🎯 Game Mechanics

### Controls
- **Keyboard**: `A` / `←` - move left, `D` / `→` - move right
- **Goal**: collect the required number of coins at each level

### Game Objects

| Object | Value | Features |
|--------|-------|----------|
| 🪙 Coin | +1 coin | Main currency |
| 💎 Gem | +10 coins | Rare item |
| ❤️ Heart | +1 life | Restores health (max 3) |
| 🚧 Obstacle | -1 life | Damage and screen shake effect |

### Level System

Each level becomes harder through:
- 📈 Increased object speed
- 🎲 Higher spawn rate
- ⚠️ Increased obstacle percentage
- 💰 Higher coin target

| Level | Target | Speed | Coins | Gems | Hearts | Obstacles |
|-------|--------|-------|-------|------|--------|-----------|
| 1️⃣ | 20 | 2.0-3.5 | 45% | 18% | 12% | 25% |
| 2️⃣ | 40 | 2.5-4.2 | 42% | 16% | 10% | 32% |
| 3️⃣ | 60 | 3.0-5.0 | 38% | 15% | 9% | 38% |
| 4️⃣ | 80 | 3.5-5.8 | 35% | 13% | 8% | 44% |
| 5️⃣ | 100 | 4.0-6.5 | 32% | 12% | 6% | 50% |

**Progression**: Coins accumulate between levels, players receive a bonus life when advancing to the next level.

## 🛠️ Technologies

### Frontend
- **HTML5** - game structure
- **CSS3** - glassmorphism UI, animations, responsiveness
- **JavaScript ES6+** - modules, classes, async/await

### Architecture
- **OOP Approach**: separated into classes (Game, Player, GameObject, ImageLoader, StorageManager)
- **ES6 Modules**: modular structure with import/export
- **Canvas API**: 2D rendering using sprites
- **LocalStorage API**: data persistence

### Patterns & Approaches
- **MVC-like Structure**: separation of logic, data, and display
- **Observer Pattern**: event-driven architecture
- **Strategy Pattern**: different strategies for object types
- **Singleton**: StorageManager, ImageLoader

## 📁 Project Structure

```
FishGame/
├── index.html                          # Main HTML file
├── static/
│   ├── css/
│   │   └── style.css                   # Styles with glassmorphism UI
│   ├── js/
│   │   ├── main.js                     # Entry point
│   │   ├── Game.js                     # Main game class (638 lines)
│   │   ├── Player.js                   # Player class with animations
│   │   ├── GameObject.js               # Falling objects
│   │   ├── ImageLoader.js              # Async sprite loading
│   │   └── StorageManager.js           # LocalStorage wrapper
│   ├── config/
│   │   └── config.js                   # Centralized configuration
│   └── img/
│       ├── Player.png                  # Player sprite
│       ├── Coin.png                    # Coin sprite
│       ├── Gem.png                     # Gem sprite
│       ├── Heart.png                   # Heart sprite
│       ├── Obstenence.png              # Obstacle sprite
│       ├── Settings.png                # Settings icon
│       └── BackGrounds/                # Level backgrounds
└── README.md
```

## 🎨 UI/UX Features

### Visual Style
- **Color Scheme**: 
  - Primary: `#00edd5` (Cyan) - coins, gem glow
  - Secondary: `#ffce38` (Gold) - accents, level number
  - Background: dark blue gradients with transparency
- **Glassmorphism**: `backdrop-filter: blur(20px)` on modal windows
- **Shadows & Glow**: `box-shadow` with cyan/gold tints
- **Animations**: smooth transitions `transition: all 0.3s ease`

### Responsiveness
- **Viewport**: 100vh height, 2:3 aspect ratio
- **Responsive Canvas**: dynamic size calculation
- **Mobile-friendly**: meta tags for mobile devices
- **Touch-ready**: prepared for touch controls

### Modal Windows
1. **Nickname Modal** - name input on first launch
2. **Game Over** - loss screen
3. **Game Win** - victory/level transition screen
4. **Player Stats** - player statistics (⚙️ button)

## 🚀 Getting Started

### Requirements
- Modern browser with ES6 modules support
- Local web server (for ES6 imports to work)

### Installation & Launch

#### Option 1: Python HTTP Server
```bash
# Python 3
python -m http.server 8000

# Open http://localhost:8000
```

#### Option 2: Node.js HTTP Server
```bash
npx http-server -p 8000

# Open http://localhost:8000
```

#### Option 3: VS Code Live Server
1. Install "Live Server" extension
2. Open `index.html`
3. Click "Go Live"

## 📊 Statistics & Progress

The game saves to LocalStorage:
- `fishgame_nickname` - player name
- `fishgame_best_time` - best completion time
- `fishgame_total_games` - total games played
- `fishgame_total_coins` - total coins collected
- `fishgame_wins` - number of wins
- `fishgame_max_level` - maximum level reached

**Win Rate** is calculated automatically: `(wins / totalGames) * 100%`

## 🎮 Animation System

### Player Animations
```javascript
- Smooth movement (lerp with 0.25 coefficient)
- Rotation on turns (±0.2 radians)
- Vertical bobbing (bobOffset)
- Scale pulsing during movement
```

### Interaction Effects
```javascript
- Particles on coin/gem collection (8 particles, radial spread)
- Pink particles on heart collection (12 particles)
- Red particles on damage
- Screen shake with exponential decay
- Red flash on damage (alpha fade)
- Object flight animation to UI counter
```

## 🔧 Configuration

All game settings are in `static/config/config.js`:

```javascript
CONFIG = {
    CANVAS: { dimensions, aspect ratio },
    LANES: { lane count },
    PLAYER: { size, lives, sprite },
    GAME_OBJECT: { base speed, spawn rate },
    OBJECT_TYPES: { object types with spawn weights },
    LEVELS: [ 5 levels with difficulty balance ]
}
```

## 🐛 Known Fixes

### Optimizations
- ✅ Fixed memory leak (removed `innerHTML` from `endGame()`)
- ✅ Smooth player movement instead of jerky motion
- ✅ Optimized particle system with lifetime limits
- ✅ Removed Pause button (replaced with auto-pause on settings open)

### UX Improvements
- ✅ Icons instead of text (Hearts, Coins, Settings)
- ✅ Dynamic button text ("Next Level" / "Play Again")
- ✅ Coin progress shown as `totalCoins/target`
- ✅ Bonus life when advancing to new level

## 📝 Development History

1. **Modular Architecture** - separated CSS/JS into individual files
2. **OOP Refactoring** - created classes for all entities
3. **Sprite System** - ImageLoader with async loading
4. **Responsive Design** - 100vh approach for mobile
5. **Glassmorphism UI** - modern design with blur effects
6. **Animation System** - particles, shake, smooth transitions
7. **UI Icons** - replaced text with images
8. **HEART Pickup** - healing objects
9. **Player Statistics** - modal window with data
10. **Level System** - 5 levels with progressive difficulty

## 🎯 Future Improvements

- [ ] Touch controls for mobile devices
- [ ] Sound effects and background music
- [ ] Leaderboard
- [ ] Bonus levels and achievements
- [ ] Character skin system
- [ ] Powerups (shield, slow-motion, coin magnet)
- [ ] Multiplayer mode

## 👨‍💻 Development

Project developed using modern web technologies and best practices:
- ES6+ syntax
- Modular architecture
- Clean code with comments
- Performance optimization
- Responsive and accessible UI

## 📄 License

MIT License - free to use for personal and commercial projects.

---

**Made with ❤️ and ☕**

Enjoy the game! 🎮✨

All in all (+-6 hours)
