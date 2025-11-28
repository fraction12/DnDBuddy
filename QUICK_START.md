# DnD Buddy - Quick Start Guide

## 🎯 What You're Building

An immersive D&D companion app where:
- **ChatGPT** acts as your Dungeon Master
- **4 players** experience epic campaigns together in real-time
- **Strict stat tracking** ensures authentic D&D mechanics
- **Text-to-speech** narration brings the story to life
- **Deploy on Vercel** for easy hosting

---

## 📚 Planning Documents

You now have complete planning documentation:

1. **PLAN.md** - Complete project plan (features, architecture, phases)
2. **TECH_STACK_COMPARISON.md** - Technology choices and comparisons
3. **CHARACTER_DATA_EXAMPLES.md** - Real data structures from your ChatGPT session

---

## ⚡ Quick Decision Guide

### Choose Your Path:

#### 🚀 **Fast MVP** (Free/Cheap - Get started today!)
```bash
Tech Stack:
✅ Next.js 14 + TypeScript
✅ Supabase (free database + real-time + auth)
✅ GPT-3.5 Turbo (cheap AI)
✅ Web Speech API (free TTS)
✅ Deploy on Vercel Hobby (free)

Cost: ~$5-10/month (just OpenAI API)
Time: 2-3 weeks
```

#### ⭐ **Production Ready** (Best quality)
```bash
Tech Stack:
✅ Next.js 14 + TypeScript
✅ Vercel Postgres
✅ GPT-4 Turbo (best AI)
✅ OpenAI TTS
✅ Pusher (real-time)
✅ Deploy on Vercel Pro

Cost: ~$40-70/month
Time: 4-6 weeks
```

#### 🎨 **Premium Experience** (Best of everything)
```bash
Everything from Production +
✅ ElevenLabs TTS (amazing voices)
✅ Battle map visualization
✅ Custom animations

Cost: ~$100-150/month
Time: 8-10 weeks
```

**My Recommendation for You**: Start with **Fast MVP**, then upgrade features based on user feedback.

---

## 🛠️ Implementation Steps

### Phase 1: Project Setup (Week 1)

```bash
# 1. Create Next.js project
npx create-next-app@latest dndbuddy --typescript --tailwind --app

cd dndbuddy

# 2. Install core dependencies
npm install zustand @prisma/client prisma openai ai zod framer-motion lucide-react

# 3. Install shadcn/ui for components
npx shadcn-ui@latest init
npx shadcn-ui@latest add button card dialog input label progress select tabs avatar badge

# 4. Set up Supabase (for Fast MVP) OR Vercel Postgres
# Supabase: https://supabase.com/dashboard/project/_/settings/database
# Vercel Postgres: https://vercel.com/docs/storage/vercel-postgres

# 5. Initialize Prisma
npx prisma init

# 6. Set up environment variables
cp .env.example .env.local
```

**.env.local**:
```bash
# Database (choose one)
# Option A: Supabase
DATABASE_URL="postgresql://postgres:[YOUR-PASSWORD]@db.[YOUR-PROJECT-REF].supabase.co:5432/postgres"

# Option B: Vercel Postgres
# POSTGRES_URL="..."

# OpenAI
OPENAI_API_KEY="sk-..."

# Real-time (if using Pusher instead of Supabase)
# NEXT_PUBLIC_PUSHER_APP_KEY="..."
# PUSHER_APP_ID="..."
# PUSHER_SECRET="..."

# Auth
NEXTAUTH_SECRET="generate-random-secret-here"
NEXTAUTH_URL="http://localhost:3000"
```

**prisma/schema.prisma**:
```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Campaign {
  id              String    @id @default(uuid())
  name            String
  totalDuration   Int       // hours
  sessionDuration Int       // hours
  currentSession  Int       @default(1)
  gameState       Json?     // Flexible storage for complex state
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
  characters      Character[]
  sessions        Session[]
  enemies         Enemy[]
  chatHistory     ChatMessage[]
}

model Character {
  id            String   @id @default(uuid())
  campaignId    String
  playerName    String   // A, B, P, D
  characterName String
  characterType String
  hpCurrent     Int
  hpMax         Int
  manaCurrent   Int
  manaMax       Int
  armor         Int
  speed         String
  xp            Int      @default(0)
  gold          Int      @default(0)
  level         Int      @default(1)
  backstory     String?
  stats         Json     // Flexible stats storage
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  campaign      Campaign @relation(fields: [campaignId], references: [id])
  skills        Skill[]
  inventory     InventoryItem[]
}

model Skill {
  id             String   @id @default(uuid())
  characterId    String
  name           String
  description    String
  type           String   // active, passive, once_per_session
  manaCost       Int      @default(0)
  usedThisSession Boolean @default(false)
  metadata       Json?    // damage, range, effects, etc.
  character      Character @relation(fields: [characterId], references: [id])
}

model InventoryItem {
  id          String   @id @default(uuid())
  characterId String
  itemName    String
  itemType    String   // weapon, armor, utility, magical
  quantity    Int      @default(1)
  equipped    Boolean  @default(false)
  effects     Json?
  description String?
  character   Character @relation(fields: [characterId], references: [id])
}

model Enemy {
  id         String   @id @default(uuid())
  campaignId String
  name       String
  type       String
  hpCurrent  Int
  hpMax      Int
  armor      Int
  abilities  Json
  statusEffects Json?
  isAlive    Boolean  @default(true)
  loot       Json?
  campaign   Campaign @relation(fields: [campaignId], references: [id])
}

model Session {
  id            String   @id @default(uuid())
  campaignId    String
  sessionNumber Int
  startTime     DateTime @default(now())
  endTime       DateTime?
  dmSummary     String?
  majorEvents   Json?
  lootGained    Json?
  xpGained      Int      @default(0)
  campaign      Campaign @relation(fields: [campaignId], references: [id])
}

model ChatMessage {
  id            String   @id @default(uuid())
  campaignId    String
  sessionNumber Int
  role          String   // user, assistant, system
  content       String
  metadata      Json?
  timestamp     DateTime @default(now())
  campaign      Campaign @relation(fields: [campaignId], references: [id])
}
```

```bash
# Run migrations
npx prisma migrate dev --name init

# Generate Prisma client
npx prisma generate

# Start development server
npm run dev
```

---

### Phase 2: Core Features (Week 2-4)

Build in this order:

#### Week 2: Character System
- [ ] Character creation form
- [ ] Character sheet display
- [ ] HP/Mana tracking components
- [ ] Basic inventory display

#### Week 3: Dice & Combat
- [ ] Dice roller component with animations
- [ ] Initiative tracker
- [ ] Turn-based combat flow
- [ ] Combat log display

#### Week 4: ChatGPT DM
- [ ] OpenAI API integration
- [ ] Context management
- [ ] Narration streaming display
- [ ] Text-to-speech integration

---

## 📁 Suggested File Structure

```
app/
├── (auth)/
│   ├── login/page.tsx
│   └── signup/page.tsx
├── (game)/
│   ├── campaign/
│   │   ├── [id]/page.tsx          # Main game screen
│   │   └── create/page.tsx
│   ├── character/
│   │   └── create/page.tsx
│   └── lobby/page.tsx
├── api/
│   ├── campaigns/route.ts
│   ├── characters/route.ts
│   ├── dm/route.ts                 # ChatGPT DM endpoint
│   ├── dice/route.ts
│   └── combat/route.ts
├── layout.tsx
└── page.tsx                        # Landing page

components/
├── character/
│   ├── CharacterSheet.tsx          # Full character display
│   ├── StatBar.tsx                 # HP/Mana bars
│   ├── AbilityCard.tsx             # Skill cards
│   └── InventoryGrid.tsx
├── combat/
│   ├── InitiativeTracker.tsx       # Turn order
│   ├── CombatLog.tsx
│   └── StatusEffects.tsx
├── dice/
│   ├── DiceRoller.tsx              # Main dice interface
│   ├── DiceAnimation.tsx           # 3D dice animation
│   └── RollHistory.tsx
├── dm/
│   ├── NarrationPanel.tsx          # ChatGPT narration display
│   ├── TTSControls.tsx             # Text-to-speech controls
│   └── DMPromptBuilder.tsx
└── ui/                              # shadcn/ui components

lib/
├── db/
│   ├── client.ts                   # Prisma client
│   ├── queries.ts                  # Read operations
│   └── mutations.ts                # Write operations
├── ai/
│   ├── chatgpt.ts                  # OpenAI integration
│   ├── prompts.ts                  # System prompts
│   └── context.ts                  # Context management
├── game/
│   ├── combat.ts                   # Combat logic
│   ├── dice.ts                     # Dice mechanics
│   └── abilities.ts                # Ability system
└── utils/
    ├── dice.ts                     # Roll calculation
    └── formatting.ts

hooks/
├── useGameState.ts                 # Global game state (Zustand)
├── useCombat.ts                    # Combat state & actions
├── useDiceRoll.ts                  # Dice rolling logic
├── useCharacter.ts                 # Character operations
└── useRealtime.ts                  # Real-time synchronization
```

---

## 🎨 Key Components to Build

### 1. Character Sheet Component

```typescript
// components/character/CharacterSheet.tsx
'use client';

import { Character } from '@/types';
import StatBar from './StatBar';
import AbilityCard from './AbilityCard';

interface CharacterSheetProps {
  character: Character;
  isActive?: boolean; // Current turn
}

export default function CharacterSheet({ character, isActive }: CharacterSheetProps) {
  return (
    <div className={`character-sheet ${isActive ? 'ring-2 ring-yellow-500' : ''}`}>
      <div className="character-header">
        <h2>{character.characterName}</h2>
        <p className="text-sm text-gray-400">{character.characterType}</p>
      </div>

      <StatBar
        label="HP"
        current={character.stats.hp.current}
        max={character.stats.hp.max}
        color="red"
      />

      <StatBar
        label="Mana"
        current={character.stats.mana.current}
        max={character.stats.mana.max}
        color="blue"
      />

      <div className="stats-grid">
        <div>Armor: {character.stats.armor}</div>
        <div>Speed: {character.stats.speed}</div>
        <div>XP: {character.xp}</div>
        <div>Gold: {character.gold}</div>
      </div>

      <div className="abilities">
        {character.skills.map((skill) => (
          <AbilityCard key={skill.id} skill={skill} />
        ))}
      </div>

      <div className="inventory">
        {/* Inventory items */}
      </div>
    </div>
  );
}
```

### 2. Dice Roller Component

```typescript
// components/dice/DiceRoller.tsx
'use client';

import { useState } from 'react';

type DieType = 'd4' | 'd6' | 'd8' | 'd10' | 'd12' | 'd20' | 'd100';

export default function DiceRoller() {
  const [result, setResult] = useState<number | null>(null);
  const [rolling, setRolling] = useState(false);

  const rollDice = async (die: DieType, modifier = 0) => {
    setRolling(true);

    // Server-side roll (to prevent cheating)
    const res = await fetch('/api/dice/roll', {
      method: 'POST',
      body: JSON.stringify({ die, modifier }),
    });

    const data = await res.json();

    // Animate for 1 second
    setTimeout(() => {
      setResult(data.total);
      setRolling(false);
    }, 1000);
  };

  return (
    <div className="dice-roller">
      <div className="dice-buttons">
        {['d4', 'd6', 'd8', 'd10', 'd12', 'd20', 'd100'].map((die) => (
          <button
            key={die}
            onClick={() => rollDice(die as DieType)}
            disabled={rolling}
            className="dice-button"
          >
            {die}
          </button>
        ))}
      </div>

      {result !== null && (
        <div className="result-display text-4xl font-bold">
          {result}
        </div>
      )}
    </div>
  );
}
```

### 3. ChatGPT DM Integration

```typescript
// lib/ai/chatgpt.ts
import OpenAI from 'openai';
import { Character, Enemy, GameContext } from '@/types';

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

export async function getDMResponse(
  gameContext: GameContext,
  playerAction: string
) {
  const systemPrompt = buildSystemPrompt(gameContext);

  const response = await openai.chat.completions.create({
    model: 'gpt-4-turbo-preview',
    messages: [
      { role: 'system', content: systemPrompt },
      { role: 'user', content: playerAction },
    ],
    stream: true, // Stream for real-time narration
  });

  return response;
}

function buildSystemPrompt(context: GameContext): string {
  return `You are an expert Dungeon Master running a D&D campaign.

CURRENT GAME STATE:
${JSON.stringify(context, null, 2)}

RULES:
- Speak with dramatic, immersive narration suitable for text-to-speech
- Track HP, mana, and status effects strictly
- Apply D&D 5e rules for combat
- Request dice rolls when needed (format: "ROLL: 1d20+5 for attack")
- Describe outcomes based on roll results

TONE: Heroic and adventurous with moments of chaotic humor

Your narration should be:
- Descriptive and atmospheric
- Clear and well-paced for TTS
- Engaging for all 4 players
- Respectful of player agency`;
}
```

### 4. Game State Management (Zustand)

```typescript
// hooks/useGameState.ts
import { create } from 'zustand';
import { Character, Enemy } from '@/types';

interface GameState {
  // Characters
  characters: Character[];
  activeCharacterId: string | null;

  // Combat
  inCombat: boolean;
  turnOrder: string[];
  currentTurn: number;

  // Enemies
  enemies: Enemy[];

  // Actions
  setCharacters: (characters: Character[]) => void;
  updateCharacterHP: (id: string, hp: number) => void;
  updateCharacterMana: (id: string, mana: number) => void;
  startCombat: (turnOrder: string[]) => void;
  endCombat: () => void;
  nextTurn: () => void;
  addEnemy: (enemy: Enemy) => void;
  updateEnemyHP: (id: string, hp: number) => void;
}

export const useGameState = create<GameState>((set) => ({
  characters: [],
  activeCharacterId: null,
  inCombat: false,
  turnOrder: [],
  currentTurn: 0,
  enemies: [],

  setCharacters: (characters) => set({ characters }),

  updateCharacterHP: (id, hp) =>
    set((state) => ({
      characters: state.characters.map((char) =>
        char.id === id
          ? { ...char, stats: { ...char.stats, hp: { ...char.stats.hp, current: hp } } }
          : char
      ),
    })),

  updateCharacterMana: (id, mana) =>
    set((state) => ({
      characters: state.characters.map((char) =>
        char.id === id
          ? { ...char, stats: { ...char.stats, mana: { ...char.stats.mana, current: mana } } }
          : char
      ),
    })),

  startCombat: (turnOrder) =>
    set({ inCombat: true, turnOrder, currentTurn: 0 }),

  endCombat: () =>
    set({ inCombat: false, turnOrder: [], currentTurn: 0 }),

  nextTurn: () =>
    set((state) => ({
      currentTurn: (state.currentTurn + 1) % state.turnOrder.length,
    })),

  addEnemy: (enemy) =>
    set((state) => ({ enemies: [...state.enemies, enemy] })),

  updateEnemyHP: (id, hp) =>
    set((state) => ({
      enemies: state.enemies.map((enemy) =>
        enemy.id === id
          ? { ...enemy, stats: { ...enemy.stats, hp: { ...enemy.stats.hp, current: hp } } }
          : enemy
      ),
    })),
}));
```

---

## 🚀 Deployment to Vercel

```bash
# 1. Install Vercel CLI
npm install -g vercel

# 2. Login to Vercel
vercel login

# 3. Link project
vercel link

# 4. Set environment variables on Vercel dashboard
# Go to: https://vercel.com/your-username/dndbuddy/settings/environment-variables

# Add:
# - OPENAI_API_KEY
# - DATABASE_URL (or POSTGRES_URL)
# - NEXTAUTH_SECRET
# - NEXTAUTH_URL (https://your-domain.vercel.app)

# 5. Deploy
vercel --prod
```

---

## 📝 Development Checklist

### Minimum Viable Product (MVP)

**Week 1: Setup**
- [ ] Next.js project initialized
- [ ] Database schema created
- [ ] Environment variables configured
- [ ] Basic UI components (shadcn/ui)
- [ ] Git repository set up

**Week 2: Characters**
- [ ] Character creation form
- [ ] Character sheet display
- [ ] HP/Mana tracking
- [ ] Basic inventory system
- [ ] Database CRUD operations

**Week 3: Dice & Combat**
- [ ] Dice roller (server-side)
- [ ] Initiative tracker
- [ ] Turn-based system
- [ ] Combat state management
- [ ] Basic combat flow

**Week 4: AI DM**
- [ ] OpenAI API integration
- [ ] Context building
- [ ] Narration display
- [ ] Streaming responses
- [ ] Text-to-speech (basic)

**Week 5: Multi-Player**
- [ ] Real-time sync (Supabase or Pusher)
- [ ] Session management
- [ ] Save/load game state
- [ ] Player authentication
- [ ] Concurrent player handling

**Week 6: Polish & Deploy**
- [ ] Mobile responsive
- [ ] Error handling
- [ ] Loading states
- [ ] Testing
- [ ] Vercel deployment
- [ ] Production testing

---

## 💡 Pro Tips

1. **Start Small**: Build character sheets first, then add complexity
2. **Use Real Data**: Test with the character data from CHARACTER_DATA_EXAMPLES.md
3. **Server-Side Rolls**: Always roll dice server-side to prevent cheating
4. **Context Limits**: Keep only last 20 ChatGPT messages to avoid token limits
5. **Optimistic UI**: Update UI immediately, then sync with server
6. **Error Boundaries**: Wrap components in error boundaries for better UX
7. **Type Safety**: Use TypeScript everywhere for fewer bugs
8. **Test with Friends**: Get 4 people to test multi-player ASAP

---

## 🐛 Common Issues & Solutions

### Issue: ChatGPT responses too slow
**Solution**: Use streaming + show partial responses + loading indicators

### Issue: Real-time sync conflicts
**Solution**: Server is source of truth, client shows optimistic updates

### Issue: Database queries slow
**Solution**: Add indexes, use connection pooling, cache frequent queries

### Issue: Dice rolls feel unfair
**Solution**: Server-side randomness + show dice animation for transparency

### Issue: Token limits exceeded
**Solution**: Summarize old messages, keep only recent context

---

## 📞 Need Help?

- **Next.js Docs**: https://nextjs.org/docs
- **OpenAI API**: https://platform.openai.com/docs
- **Vercel Support**: https://vercel.com/support
- **Prisma Guides**: https://www.prisma.io/docs

---

## 🎉 Ready to Start?

```bash
# Your first command
npx create-next-app@latest dndbuddy --typescript --tailwind --app

cd dndbuddy

# Install core dependencies
npm install zustand @prisma/client prisma openai ai

# Initialize Prisma
npx prisma init

# Start building! 🚀
npm run dev
```

---

## Next Steps After MVP

Once your MVP is working, consider adding:

1. **Battle Map** - Visual grid for positioning
2. **Character Portraits** - AI-generated or uploaded
3. **Sound Effects** - Dice rolls, combat sounds
4. **Campaign Builder** - Pre-made adventures
5. **Mobile App** - React Native version
6. **Spectator Mode** - Watch campaigns live
7. **Session Recording** - Replay past sessions
8. **Achievement System** - Track epic moments

---

**You have everything you need to build this!**

The planning is done. The architecture is defined. The data structures are ready.

Now it's time to code. 🎲✨

Good luck, and may your rolls be ever in your favor!
