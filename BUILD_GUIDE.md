# Build Guide - Modak Maker Challenge

A complete step-by-step guide to build and deploy your Vinaya Chavathi-themed match-3 puzzle game.

## 📋 Table of Contents
1. [Prerequisites](#prerequisites)
2. [Project Setup](#project-setup)
3. [Development](#development)
4. [Asset Creation](#asset-creation)
5. [Configuration](#configuration)
6. [Testing](#testing)
7. [Building for Production](#building-for-production)
8. [Deployment](#deployment)

---

## Prerequisites

### Required Software
- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js) or **yarn**
- **Git** - [Download](https://git-scm.com/)
- **Code Editor** - VS Code recommended

### Recommended Tools
- **Visual Studio Code** with extensions:
  - ES7+ React/Redux/React-Native snippets
  - Prettier - Code formatter
  - ESLint
  - Live Server
  
### System Requirements
- **RAM:** 4GB minimum (8GB recommended)
- **Storage:** 2GB free space
- **Browser:** Chrome, Firefox, Safari, or Edge (latest versions)

---

## Project Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/Bhavitha-sekhar/vinaya-chavathi-game.git
cd vinaya-chavathi-game
```

### Step 2: Install Dependencies

```bash
npm install
# or
yarn install
```

This installs:
- Phaser 3 (game framework)
- Webpack (bundler)
- Babel (transpiler)
- Development dependencies

**Installation time:** ~2-3 minutes

### Step 3: Verify Installation

```bash
npm --version
node --version
```

Expected output:
```
v8.x.x or higher (npm)
v14.x.x or higher (node)
```

---

## Development

### Running the Development Server

```bash
npm run dev
```

This will:
1. Start Webpack dev server on `http://localhost:8080`
2. Hot-reload on file changes
3. Display errors in browser console

### Project Structure

```
vinaya-chavathi-game/
│
├── src/
│   ├── main.js                 # Game entry point
│   ├── scenes/
│   │   ├── BootScene.js       # Asset loading
│   │   ├── MenuScene.js       # Main menu
│   │   ├── GameScene.js       # Gameplay
│   │   ├── WinScene.js        # Level complete
│   │   └── LoseScene.js       # Game over
│   │
│   ├── objects/               # Game objects (to create)
│   │   ├── Tile.js
│   │   ├── Modak.js
│   │   └── Ingredient.js
│   │
│   └── utils/                 # Utilities (to create)
│       ├── ScoreManager.js
│       ├── LevelManager.js
│       └── SoundManager.js
│
├── assets/                    # Game assets (to create)
│   ├── images/
│   │   ├── backgrounds/       # BG images
│   │   ├── tiles/            # Ingredient tiles
│   │   ├── modaks/           # Modak images
│   │   ├── characters/       # Ganesha image
│   │   ├── ui/               # Buttons, icons
│   │   └── effects/          # Particle effects
│   │
│   ├── audio/
│   │   ├── music/            # Background music
│   │   └── sfx/              # Sound effects
│   │
│   └── fonts/                # Custom fonts
│
├── index.html               # HTML entry point
├── style.css               # Global styles
├── package.json            # Dependencies
├── webpack.config.js       # Webpack config (to create)
├── .gitignore
├── README.md
└── CONTRIBUTING.md
```

---

## Asset Creation

### Step 1: Create Asset Directories

```bash
mkdir -p assets/images/backgrounds
mkdir -p assets/images/tiles
mkdir -p assets/images/modaks
mkdir -p assets/images/characters
mkdir -p assets/images/ui
mkdir -p assets/images/effects
mkdir -p assets/audio/music
mkdir -p assets/audio/sfx
mkdir -p assets/fonts
```

### Step 2: Required Assets

#### A. Background Images (1024x768 each)
- `assets/images/backgrounds/menu-bg.png` - Menu background
- `assets/images/backgrounds/game-bg.png` - Game background

**Create using:**
- Photoshop, GIMP, or Canva
- Online tools: pixlr.com, photopea.com

#### B. Ingredient Tiles (50x50 each)
Create 5 colored circles representing ingredients:

- `assets/images/tiles/jaggery.png` - Brown (#8B4513)
- `assets/images/tiles/rice-flour.png` - Yellow (#FFD700)
- `assets/images/tiles/coconut.png` - White (#FFFFFF)
- `assets/images/tiles/cardamom.png` - Green (#228B22)
- `assets/images/tiles/ghee.png` - Orange (#FFA500)

**Quick Create Script:**
```javascript
// Use this in browser console to generate placeholder images
// Save as PNG using screenshot tools

const canvas = document.createElement('canvas');
canvas.width = 50;
canvas.height = 50;
const ctx = canvas.getContext('2d');

// Draw circle
ctx.fillStyle = '#8B4513'; // Change color for each
ctx.beginPath();
ctx.arc(25, 25, 22, 0, Math.PI * 2);
ctx.fill();

// Add text
ctx.fillStyle = '#FFF';
ctx.font = 'bold 20px Arial';
ctx.textAlign = 'center';
ctx.fillText('J', 25, 32); // Change letter for each

// Download
canvas.toBlob(blob => {
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'jaggery.png';
    a.click();
});
```

#### C. Modak Image (100x100)
- `assets/images/modaks/modak.png` - Modak sweet
- `assets/images/modaks/modak-icon.png` - Icon version (32x32)

#### D. Character
- `assets/images/characters/ganesha.png` - Ganesha statue (100x100)

#### E. UI Elements
- `assets/images/ui/button-play.png` - Play button
- `assets/images/ui/button-restart.png` - Restart button
- `assets/images/ui/button-menu.png` - Menu button

#### F. Audio Files
Create or download:
- `assets/audio/music/menu-music.mp3` - Royalty-free Indian classical
- `assets/audio/music/game-music.mp3` - Background game music
- `assets/audio/sfx/match.mp3` - Match sound effect
- `assets/audio/sfx/level-complete.mp3` - Victory sound
- `assets/audio/sfx/game-over.mp3` - Game over sound
- `assets/audio/sfx/powerup.mp3` - Powerup sound
- `assets/audio/sfx/click.mp3` - Click sound

**Free Resources:**
- **Images:** Pixabay, Unsplash, OpenGameArt.org
- **Audio:** Freesound.org, ZapSplat, BensoundXVXVX.com

---

## Configuration

### Step 1: Create Webpack Config

Create `webpack.config.js`:

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    mode: process.env.NODE_ENV || 'development',
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: '[name].[contenthash].js',
        clean: true,
    },
    devServer: {
        static: {
            directory: path.join(__dirname, '.'),
        },
        compress: true,
        port: 8080,
        hot: true,
        open: true,
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env'],
                    },
                },
            },
            {
                test: /\.css$/i,
                use: ['style-loader', 'css-loader'],
            },
            {
                test: /\.(png|jpg|gif|mp3|wav)$/,
                type: 'asset/resource',
            },
        ],
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './index.html',
        }),
    ],
};
```

### Step 2: Update package.json Scripts

```json
{
  "scripts": {
    "dev": "webpack serve --mode development",
    "build": "webpack --mode production",
    "start": "npm run dev",
    "analyze": "webpack-bundle-analyzer dist/stats.json"
  }
}
```

---

## Testing

### Manual Testing

```bash
# Run development server
npm run dev

# Test in different browsers
# - Chrome DevTools (F12)
# - Firefox Developer (F12)
# - Safari Develop menu

# Test on mobile
# Use Chrome DevTools > Device Toggle (Ctrl+Shift+M)
```

### Test Checklist

- [ ] **Gameplay**
  - [ ] Tiles match correctly
  - [ ] Score updates properly
  - [ ] Timer counts down
  - [ ] Level progression works

- [ ] **Audio**
  - [ ] Background music plays
  - [ ] Sound effects trigger
  - [ ] No audio distortion

- [ ] **UI/UX**
  - [ ] Menu displays properly
  - [ ] Buttons are clickable
  - [ ] Text is readable
  - [ ] Layout responsive on mobile

- [ ] **Performance**
  - [ ] No lag during gameplay
  - [ ] Smooth animations
  - [ ] FPS stable (60 FPS target)

### Browser Testing

```bash
# Test on different browsers
Chrome     ✅ Recommended
Firefox    ✅ Good
Safari     ✅ Works
Edge       ✅ Works
```

---

## Building for Production

### Step 1: Build the Game

```bash
npm run build
```

This will:
- Minify JavaScript
- Optimize assets
- Generate `dist/` folder
- Create production-ready files

**Output structure:**
```
dist/
├── index.html
├── main.[hash].js      # Bundled game code
└── assets/             # Compressed images/audio
```

### Step 2: Optimize Assets

#### Image Optimization
```bash
# Install image optimizer
npm install --save-dev imagemin-webpack-plugin

# Compress images
npx imagemin assets/images --out-dir=dist/assets/images
```

#### File Sizes Target
- **Total bundle:** < 5MB
- **JavaScript:** < 1MB
- **Images:** < 3MB
- **Audio:** < 1MB

### Step 3: Test Production Build

```bash
# Serve production build locally
npx http-server dist/

# Visit http://localhost:8080
```

---

## Deployment

### Option 1: GitHub Pages (Free, Recommended for Beginners)

1. **Enable GitHub Pages:**
   - Go to repository Settings
   - Scroll to "Pages"
   - Set source to `main` branch
   - Set folder to `/root` or `/docs`

2. **Update package.json:**
   ```json
   {
     "homepage": "https://Bhavitha-sekhar.github.io/vinaya-chavathi-game",
     "scripts": {
       "predeploy": "npm run build",
       "deploy": "gh-pages -d dist"
     }
   }
   ```

3. **Deploy:**
   ```bash
   npm install --save-dev gh-pages
   npm run deploy
   ```

4. **Access:** `https://Bhavitha-sekhar.github.io/vinaya-chavathi-game`

### Option 2: Netlify (Free, Easiest)

1. **Connect repository:**
   - Go to [netlify.com](https://netlify.com)
   - Sign up with GitHub
   - Click "New site from Git"
   - Select your repository

2. **Configure build:**
   - Build command: `npm run build`
   - Publish directory: `dist`

3. **Deploy:**
   - Netlify auto-deploys on push
   - Custom domain available

### Option 3: Vercel (Free)

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Deploy:**
   ```bash
   vercel
   ```

3. **Follow prompts and done!**

### Option 4: Traditional Hosting (Paid)

Upload `dist/` folder to:
- **Bluehost, GoDaddy, HostGator** (cPanel FTP)
- **AWS S3** (Cloud hosting)
- **DigitalOcean** (VPS)

---

## Advanced Setup (Optional)

### Add Analytics

```bash
npm install --save-dev google-analytics-webpack-plugin
```

### Add Firebase (Leaderboard)

```bash
npm install firebase
```

### PWA (Progressive Web App)

```bash
npm install --save-dev workbox-webpack-plugin
```

---

## Troubleshooting

### Issue: `Module not found`
```bash
# Clear node_modules and reinstall
rm -rf node_modules
npm install
```

### Issue: `Port 8080 already in use`
```bash
# Use different port
npm run dev -- --port 3000
```

### Issue: Images not loading
- Check file paths (case-sensitive on Linux)
- Ensure files in `assets/` directory
- Use relative paths: `assets/images/bg.png`

### Issue: Audio not playing
- Check browser autoplay policy
- Test in incognito mode
- Ensure audio files are compressed

---

## Performance Optimization

### 1. Lazy Load Assets
```javascript
// Only load assets when needed
scene.load.audio('music', 'path/to/music.mp3');
```

### 2. Reduce File Sizes
- Compress images (TinyPNG)
- Use WebP format
- Optimize audio bitrate (128kbps)

### 3. Caching
- Browser cache headers
- Service Workers (PWA)
- CDN integration

### 4. Monitor Performance
```bash
# Analyze bundle size
npm run analyze
```

---

## CI/CD Setup (Optional)

### GitHub Actions Workflow

Create `.github/workflows/build.yml`:

```yaml
name: Build and Deploy

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'
      
      - run: npm install
      - run: npm run build
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## Next Steps

1. ✅ Install dependencies
2. ✅ Create asset directories
3. ✅ Add game images and audio
4. ✅ Run `npm run dev`
5. ✅ Test gameplay
6. ✅ Build with `npm run build`
7. ✅ Deploy to hosting

---

## Resources

- **Phaser 3 Docs:** https://photonstorm.github.io/phaser3-docs/
- **Game Assets:** https://opengameart.org/
- **Audio:** https://freesound.org/
- **Hosting:** https://netlify.com, https://vercel.com

---

**🎮 Happy Building! May Ganesha guide your development journey! 🙏**
