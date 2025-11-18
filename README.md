# 🧠 NeuralZero Chess

**A self-learning chess AI powered by collective intelligence**

Play chess against an AI that learns from every player worldwide. Every 16 games played globally, the AI automatically retrains on community data, becoming smarter for everyone simultaneously.

---

## ✨ Features

- 🎮 Full chess implementation with move validation
- 🧠 Neural network AI (TensorFlow.js) that improves over time
- 🌐 "Hive mind" - AI learns from all players globally
- 📊 Real-time global stats and training progress
- 🎨 Beautiful dark-themed responsive UI
- 🔒 Privacy-friendly (anonymous auth, no tracking)

---

## 🚀 Quick Start

**Play Now**: Simply open `index.html` in any modern browser. No installation needed!

```bash
# Clone and run locally
git clone https://github.com/Open-Deep-ML/NeuralZero-Chess.git
cd NeuralZero-Chess
# Open index.html in your browser
```

**Deploy to GitHub Pages**: Fork repo → Enable Pages → Push to main → Done!

---

## 🧮 How It Works

### The AI
- **Hybrid evaluation**: 70% material heuristics + 30% neural network
- **Search**: Minimax algorithm with alpha-beta pruning (2-ply depth)
- **Network**: 768 → 128 → 64 → 1 (input: board state, output: position score)

### The Hive Mind
1. **You play** → Game data uploaded to Firebase (20 shared slots)
2. **16 games complete globally** → Training triggered for all users
3. **AI downloads** all community data and retrains (3 epochs, ~500 positions)
4. **Everyone benefits** → Smarter AI for all players simultaneously

```
Player 1 plays → Firebase
Player 2 plays → Firebase  
...
Player 16 plays → Firebase
                     ↓
         🧠 Global Training Event 🧠
                     ↓
    All users download & retrain
                     ↓
         Everyone has smarter AI!
```

---

## 🛠️ Technology Stack

- **chess.js** - Game logic
- **TensorFlow.js** - Neural network
- **Firebase** - Cloud database & auth
- **Tailwind CSS** - Styling

**No build tools required** - Single HTML file with everything!

---

## 🔧 Configuration

### Deploy Your Own Instance

1. Create Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable Firestore + Anonymous Auth
3. Update `firebaseConfig` in `index.html`
4. Set Firestore rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function isSignedIn() {
      return request.auth != null;
    }
    
    match /artifacts/{appId}/public/data/hive_memory/{slotId} {
      allow read: if true;
      allow write: if isSignedIn();
    }
    
    match /artifacts/{appId}/public/data/chess_stats/global {
      allow read: if true;
      allow write: if isSignedIn();
    }
    
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

### Customize Settings

```javascript
const GAMES_PER_TRAINING = 16;  // Training frequency
const HIVE_SLOTS = 20;          // Number of cloud slots
const move = await getBestMove(2); // AI search depth
```

---

## 📊 Performance

**Strengths**:
- ✅ Runs in browser (no server costs)
- ✅ Privacy-friendly
- ✅ Improves automatically
- ✅ Fast inference (~100ms)

**Limitations**:
- ⚠️ Weak when untrained
- ⚠️ Limited depth (browser constraints)
- ⚠️ Can't compete with Stockfish

---

## 🤝 Contributing

Ideas welcome! Consider adding:
- Difficulty levels
- Opening book
- Time controls
- Game replay
- Sound effects

1. Fork the repo
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📝 License

MIT License - See [LICENSE](LICENSE) file

---

## 🙏 Credits

Built with [chess.js](https://github.com/jhlywa/chess.js), [TensorFlow.js](https://www.tensorflow.org/js), [Firebase](https://firebase.google.com), and [Tailwind CSS](https://tailwindcss.com)

**Made by [Deep-ML](https://www.deep-ml.com/problems)** for the AI learning community

---

⭐ Star this repo if you find it interesting • 🎮 Play and contribute to the hive mind!
