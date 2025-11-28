# 🎲 DnD Buddy

An immersive D&D companion app where ChatGPT acts as your Dungeon Master, bringing epic campaigns to life for 4 players with real-time stat tracking, dice rolling, and AI-powered storytelling.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)

---

## ✨ Features

- 🤖 **AI Dungeon Master** - ChatGPT narrates your adventure with dramatic, immersive storytelling
- 🎭 **4-Player Co-op** - Real-time multiplayer synchronization
- 📊 **Strict Stat Tracking** - HP, Mana, Armor, XP, Inventory, and more
- 🎲 **Dice Roller** - Server-side dice rolls with beautiful animations
- ⚔️ **Combat System** - Initiative tracking, turn-based combat, status effects
- 🔊 **Text-to-Speech** - AI narration comes alive with voice
- 🎨 **AI Image Generation** - Character portraits, scene images, enemy visuals (DALL-E 3 + Stable Diffusion)
- 💾 **Session Management** - Save/load campaigns, session history
- 📱 **Mobile Responsive** - Play on any device

---

## 🎯 Based on Your ChatGPT Session

This app is specifically designed around your epic campaign featuring:

### Characters
- **Lira the Fairy** (Player A) - 11-inch magical support with Fairy Bliss
- **Rorek the Rune Knight** (Player B) - Dwarven tank with rune magic and Ropey the rope familiar
- **Elliathel the Elf Ranger** (Player P) - Agile archer with True Shot and moon-blessed dagger
- **Veyrath the Dark High Mage** (Player D) - Powerful spellcaster with shadow magic

### Campaign
- **5-hour epic quest** divided into 1-hour sessions
- Enemies: Goblins, Werewolves, Trolls, Mimics, Manticore, and 2 Dragons
- **Heroic tone** with moments of chaotic humor
- **STRICT mode** - Real D&D stat tracking

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| **[PLAN.md](./PLAN.md)** | Complete project plan, architecture, features, and development phases |
| **[TECH_STACK_COMPARISON.md](./TECH_STACK_COMPARISON.md)** | Technology choices, cost analysis, and recommendations |
| **[CHARACTER_DATA_EXAMPLES.md](./CHARACTER_DATA_EXAMPLES.md)** | Real data structures from your ChatGPT session |
| **[IMAGE_GENERATION_PLAN.md](./IMAGE_GENERATION_PLAN.md)** | 🎨 AI image generation guide (characters, scenes, enemies) |
| **[QUICK_START.md](./QUICK_START.md)** | Step-by-step guide to start building |

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- npm or yarn
- OpenAI API key
- Database (Supabase or Vercel Postgres)

### Installation

```bash
# 1. Clone repository
git clone https://github.com/your-username/dndbuddy.git
cd dndbuddy

# 2. Install dependencies
npm install

# 3. Set up environment variables
cp .env.example .env.local
# Edit .env.local with your API keys

# 4. Set up database
npx prisma migrate dev --name init
npx prisma generate

# 5. Seed with sample data (optional)
npm run seed

# 6. Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## 🏗️ Tech Stack

### Recommended (Production Ready)
- **Frontend**: Next.js 14 (App Router), TypeScript, Tailwind CSS, shadcn/ui
- **Backend**: Next.js API Routes, Vercel Postgres, Prisma ORM
- **AI**: OpenAI GPT-4 Turbo, OpenAI TTS
- **Real-time**: Pusher or Supabase Realtime
- **State**: Zustand
- **Deployment**: Vercel

### Budget-Friendly Alternative
- **Database**: Supabase (free tier)
- **AI**: GPT-3.5 Turbo (cheaper)
- **TTS**: Web Speech API (free)
- **Real-time**: Supabase Realtime (included)

**Cost**: ~$5-10/month vs ~$40-70/month

See [TECH_STACK_COMPARISON.md](./TECH_STACK_COMPARISON.md) for detailed analysis.

---

## 📂 Project Structure

```
dndbuddy/
├── app/                    # Next.js App Router
│   ├── (auth)/            # Authentication pages
│   ├── (game)/            # Main game interface
│   └── api/               # API routes
├── components/            # React components
│   ├── character/         # Character sheets, stats
│   ├── combat/            # Initiative, combat log
│   ├── dice/              # Dice roller
│   ├── dm/                # DM narration panel
│   └── ui/                # shadcn/ui components
├── lib/
│   ├── db/                # Database client & queries
│   ├── ai/                # ChatGPT integration
│   ├── game/              # Game logic (combat, dice)
│   └── utils/             # Utilities
├── hooks/                 # Custom React hooks
├── types/                 # TypeScript types
└── prisma/                # Database schema
```

---

## 🎮 How It Works

### 1. Campaign Setup
- Create campaign with 4 player slots
- Each player creates their character
- ChatGPT generates opening narration

### 2. Gameplay Loop
```
Player Action → API Request → ChatGPT Processes
                                     ↓
                            Game State Updates
                                     ↓
                         Real-time Sync to All Players
                                     ↓
                            DM Narrates Outcome
                                     ↓
                        Next Player's Turn → Repeat
```

### 3. Combat Flow
```
Encounter Triggers → Initiative Rolls → Turn Order
                                             ↓
Player Turn → Choose Action → Roll Dice → Apply Effects
                                             ↓
                           DM Narrates Result
                                             ↓
                         Enemy Turn (AI controlled)
                                             ↓
                             Repeat Until Victory
```

---

## 🎯 Development Roadmap

### Phase 1: MVP (Week 1-6) ✅ PLANNING COMPLETE
- [x] Complete planning documentation
- [ ] Project setup
- [ ] Character creation & display
- [ ] Dice rolling system
- [ ] ChatGPT DM integration
- [ ] Basic combat system
- [ ] Multi-player sync
- [ ] Deploy to Vercel

### Phase 2: Polish (Week 7-8)
- [ ] Animations & effects
- [ ] Mobile responsive
- [ ] Session save/load
- [ ] Inventory management
- [ ] Quest log

### Phase 3: Advanced Features (Week 9-12)
- [ ] Battle map visualization
- [ ] Enhanced TTS (ElevenLabs)
- [ ] Character portraits
- [ ] Session recording
- [ ] Statistics dashboard

---

## 💰 Cost Breakdown

### Per Session (1 hour, 4 players)
| Service | Cost |
|---------|------|
| OpenAI GPT-4 Turbo | ~$2.80 |
| OpenAI TTS | ~$0.15 |
| Real-time (Pusher) | $0 (free tier) |
| **Total** | **~$3.00** |

### Monthly (100 sessions)
| Service | Tier | Cost |
|---------|------|------|
| Vercel Pro | Required | $20 |
| Vercel Postgres | Starter | $20 |
| OpenAI API | Pay-as-you-go | ~$280 |
| Pusher | Free tier | $0 |
| **Total** | | **~$320** |

**Budget Option**: Use Supabase + GPT-3.5 for ~$5-10/month during development.

---

## 🧪 Example Character Data

All character data from your ChatGPT session is documented in [CHARACTER_DATA_EXAMPLES.md](./CHARACTER_DATA_EXAMPLES.md).

Example:
```typescript
const liraCharacter = {
  characterName: "Lira",
  characterType: "Fairy",
  stats: {
    hp: { current: 18, max: 18 },
    mana: { current: 24, max: 24 },
    armor: 10,
    speed: "Fast",
    size: "11 inches"
  },
  skills: [
    {
      name: "Fairy Bliss",
      type: "once_per_session",
      description: "Calm hostile creatures in 20ft radius",
      saveDC: 14
    }
  ]
};
```

---

## 🔧 Configuration

### Environment Variables

```bash
# OpenAI API
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4-turbo-preview

# Database
DATABASE_URL=postgresql://...

# Real-time (Pusher)
NEXT_PUBLIC_PUSHER_APP_KEY=...
PUSHER_APP_ID=...
PUSHER_SECRET=...

# Authentication
NEXTAUTH_SECRET=...
NEXTAUTH_URL=http://localhost:3000

# Text-to-Speech (Optional)
ELEVENLABS_API_KEY=...
```

---

## 📖 API Examples

### Roll Dice
```typescript
POST /api/dice/roll
{
  "dieType": "d20",
  "modifier": 5,
  "advantage": false
}

Response:
{
  "rolls": [17],
  "modifier": 5,
  "total": 22,
  "isCritical": false
}
```

### Get DM Narration
```typescript
POST /api/dm/narrate
{
  "campaignId": "...",
  "playerAction": "I attack the werewolf with my dagger",
  "gameContext": { ... }
}

Response (streamed):
{
  "narration": "Elliathel raises her dagger...",
  "requiresRoll": {
    "player": "P",
    "type": "d20",
    "modifier": 3,
    "dc": 15
  }
}
```

### Update Character HP
```typescript
PATCH /api/characters/:id/hp
{
  "currentHP": 15
}
```

---

## 🐛 Troubleshooting

### ChatGPT responses are slow
- Use streaming responses
- Show loading states
- Consider GPT-3.5 for faster (but lower quality) responses

### Real-time sync not working
- Check Pusher/Supabase configuration
- Verify environment variables
- Test with multiple browser tabs

### Database queries failing
- Run `npx prisma generate`
- Check DATABASE_URL
- Verify migrations: `npx prisma migrate dev`

---

## 🤝 Contributing

This is a personal project, but suggestions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📝 License

MIT License - feel free to use this for your own campaigns!

---

## 🎉 Credits

- **ChatGPT** - Your amazing DM
- **OpenAI** - GPT-4 and TTS
- **Vercel** - Hosting platform
- **Shadcn** - UI components
- **You** - The adventurers!

---

## 🔗 Links

- [Live Demo](#) - Coming soon
- [Documentation](./PLAN.md)
- [Tech Stack Guide](./TECH_STACK_COMPARISON.md)
- [Quick Start](./QUICK_START.md)

---

## 📬 Contact

Have questions? Found a bug? Want to collaborate?

- **GitHub Issues**: [Create an issue](https://github.com/your-username/dndbuddy/issues)
- **Email**: your-email@example.com

---

## 🎲 May Your Rolls Be Ever in Your Favor!

Built with ❤️ for epic adventures.

**Status**: 📋 Planning Complete → 🏗️ Ready to Build

---

## Quick Commands

```bash
# Development
npm run dev          # Start dev server
npm run build        # Build for production
npm run start        # Start production server

# Database
npx prisma studio    # Open database GUI
npx prisma migrate dev  # Run migrations
npx prisma generate  # Generate client

# Deployment
vercel               # Deploy to Vercel
vercel --prod        # Deploy to production
```

---

**Last Updated**: November 28, 2025

**Next Steps**: Read [QUICK_START.md](./QUICK_START.md) to begin building! 🚀
