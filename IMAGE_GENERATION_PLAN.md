# 🎨 Image Generation Integration Plan

## Overview

Enhance the DnD Buddy experience with AI-generated images for:
- **Character portraits** - Visual representation of each character
- **Scene setting** - Dungeons, forests, taverns, battles
- **Enemy encounters** - Goblins, werewolves, dragons
- **Key moments** - Epic scenes from the campaign
- **Items & loot** - Weapons, artifacts, magical items

---

## 🎯 Use Cases

### 1. Character Portraits
**When**: Character creation
**Prompt Example**:
```
"Portrait of Lira, an 11-inch tall fairy with iridescent wings,
luminous skin, big expressive eyes, wearing nature-inspired clothing,
fantasy art style, D&D character portrait, digital art"
```

**Generated For**:
- Lira the Fairy (11 inches, iridescent wings, luminous)
- Rorek the Rune Knight (Dwarf, heavy armor, runic greatsword)
- Elliathel the Elf Ranger (Agile, bow, elven features)
- Veyrath the Dark High Mage (Dark robes, shadow aura, spellbook)

### 2. Scene Setting
**When**: New location or major scene change
**Prompt Example**:
```
"The town of Brightwick at sunrise, pale mist floating along cobbled streets,
old stone Council Hall with lanterns, frontier outpost at the edge of a dark forest,
fantasy landscape, D&D setting, atmospheric, moody lighting"
```

**Scenes to Generate**:
- Brightwick Town (starting location)
- East Storage Barn (goblin encounter)
- Secret Cellar (mysterious, glowing moonrunes)
- Ashenwild Forest (dark, corrupted)
- Dragon Lairs (volcano caverns, crystalline ruins)

### 3. Enemy Encounters
**When**: New enemy appears
**Prompt Example**:
```
"A massive barn werewolf, standing on two legs, torn ears, ragged claws,
enormous glowing yellow eyes, fur covered in hay and blood,
menacing pose, D&D monster, dark fantasy art, dramatic lighting"
```

**Enemies to Generate**:
- Goblins (various types: scout, sneak, pyro)
- Barn Werewolf (large, menacing)
- Troll Warlord (regenerating, brutal)
- Werewolf Pack (pack hunting under full moon)
- Mimics (disguised as chests, objects)
- Manticore (intelligent, cruel, winged)
- Vorathrax the Volcanic (fire dragon, molten scales)
- Sylestria the Dreaming Serpent (psychic dragon, crystalline)

### 4. Epic Moments
**When**: Critical hits, major victories, dramatic scenes
**Prompt Example**:
```
"An elf ranger throwing a glowing moon-blessed dagger at a werewolf's eye,
action shot, dynamic pose, magical energy trail, D&D combat scene,
epic fantasy art, cinematic lighting"
```

**Moments to Capture**:
- Elliathel's True Shot hitting werewolf's eye
- Veyrath's critical Dark Fire killing the werewolf
- Lira's Fairy Fuckery swarm of tiny swords
- Rorek creating Ropey the animated rope

### 5. Items & Loot
**When**: New item acquired
**Prompt Example**:
```
"Moon-Bitten Dagger, ornate silver blade glowing with faint moonlight,
runic engravings, fantasy weapon, item card art, D&D magic item,
clean white background"
```

**Items to Generate**:
- Moon-Bitten Dagger
- Runic Greatsword
- Werewolf Blood Vial
- Bloodmoon Pelt Fragment
- Magical Artifacts

---

## 🛠️ Image Generation APIs

### Option 1: **DALL-E 3** (OpenAI) ⭐ RECOMMENDED

**Pros**:
- Same API as ChatGPT (already integrated)
- Best prompt understanding
- High quality, consistent style
- Good at fantasy art
- Supports 1024x1024, 1024x1792, 1792x1024

**Cons**:
- More expensive ($0.040 - $0.080 per image)
- Slower (10-30 seconds)

**Cost**:
- Standard (1024x1024): **$0.040 per image**
- HD (1024x1024): **$0.080 per image**

**Best For**: Character portraits, key scenes, epic moments

```typescript
// Example implementation
import OpenAI from 'openai';

const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });

async function generateImage(prompt: string) {
  const response = await openai.images.generate({
    model: "dall-e-3",
    prompt: prompt,
    n: 1,
    size: "1024x1024",
    quality: "standard", // or "hd" for better quality
    style: "vivid" // or "natural"
  });

  return response.data[0].url;
}
```

---

### Option 2: **Stable Diffusion XL** (Stability AI)

**Pros**:
- Cheaper ($0.002 - $0.008 per image)
- Fast (3-5 seconds)
- Good quality
- More style control

**Cons**:
- Needs separate API account
- Less consistent with complex prompts
- Requires more prompt engineering

**Cost**:
- Standard: **$0.002 per image**
- HD: **$0.008 per image**

**Best For**: Scenes, backgrounds, environments

```typescript
import Replicate from 'replicate';

const replicate = new Replicate({
  auth: process.env.REPLICATE_API_TOKEN,
});

async function generateImage(prompt: string) {
  const output = await replicate.run(
    "stability-ai/sdxl:latest",
    {
      input: {
        prompt: prompt,
        width: 1024,
        height: 1024,
      }
    }
  );

  return output[0];
}
```

---

### Option 3: **Midjourney** (via API)

**Pros**:
- Best artistic quality
- Amazing fantasy art style
- Consistent aesthetics

**Cons**:
- No official API (need third-party)
- More expensive
- Slower
- Complex setup

**Cost**: ~$0.10 per image

**Best For**: Premium experience, promotional material

---

### Option 4: **Free/Local Options**

**For Friends-Only Budget Build**:

1. **Replicate (Free Credits)**
   - $5 free credits
   - Then pay-as-you-go

2. **Hugging Face Inference API**
   - Free tier available
   - Stable Diffusion models
   - Rate limited

3. **Local Stable Diffusion**
   - Completely free
   - Requires GPU (6GB+ VRAM)
   - Slower but unlimited

---

## 💰 Cost Analysis for Friends Group

### Conservative Estimate (Per Campaign)

**Using DALL-E 3 Standard ($0.040/image)**:

| Image Type | Quantity | Cost |
|------------|----------|------|
| Character Portraits (4) | 4 | $0.16 |
| Scene Setting (per session) | 2-3 | $0.08-0.12 |
| Enemy Encounters | 3-4 | $0.12-0.16 |
| Epic Moments | 2-3 | $0.08-0.12 |
| Items/Loot | 3-5 | $0.12-0.20 |
| **Per Session Total** | **14-19 images** | **$0.56-0.76** |

**Per Campaign (5 sessions)**:
- Total images: ~70-80 images
- **Total cost: ~$3-4**

### Budget-Friendly Option

**Using Stable Diffusion XL ($0.002/image)**:

| Period | Images | Cost |
|--------|--------|------|
| Per Session | 15-20 | **$0.03-0.04** |
| Per Campaign (5 sessions) | 75-100 | **$0.15-0.20** |

**Basically free!** 🎉

---

## 🎨 Implementation Strategy

### When to Generate Images

```typescript
// lib/ai/image-generation.ts

interface ImageGenerationTrigger {
  type: 'character' | 'scene' | 'enemy' | 'moment' | 'item';
  trigger: string;
  priority: 'high' | 'medium' | 'low';
  autoGenerate: boolean;
}

const triggers: ImageGenerationTrigger[] = [
  {
    type: 'character',
    trigger: 'character_created',
    priority: 'high',
    autoGenerate: true
  },
  {
    type: 'scene',
    trigger: 'location_changed',
    priority: 'medium',
    autoGenerate: true
  },
  {
    type: 'enemy',
    trigger: 'combat_started',
    priority: 'high',
    autoGenerate: true
  },
  {
    type: 'moment',
    trigger: 'critical_hit',
    priority: 'low',
    autoGenerate: false // Player can request
  },
  {
    type: 'item',
    trigger: 'rare_item_acquired',
    priority: 'low',
    autoGenerate: false
  }
];
```

### Smart Prompt Building

```typescript
// lib/ai/prompts.ts

function buildCharacterPrompt(character: Character): string {
  const baseStyle = "D&D character portrait, fantasy art, digital painting, detailed, high quality";

  const characterDetails = {
    name: character.characterName,
    race: character.characterType,
    class: character.characterClass,
    appearance: character.appearance.features,
    distinctive: character.appearance.distinctiveTraits.join(", ")
  };

  return `Portrait of ${characterDetails.name}, a ${characterDetails.race} ${characterDetails.class}.
    ${characterDetails.appearance}.
    Distinctive features: ${characterDetails.distinctive}.
    ${baseStyle}`;
}

function buildScenePrompt(location: string, context: GameContext): string {
  const baseStyle = "D&D fantasy setting, atmospheric, cinematic lighting, detailed environment";

  const moodMap = {
    "dangerous": "dark, ominous, threatening atmosphere",
    "peaceful": "warm, inviting, safe atmosphere",
    "mysterious": "foggy, ethereal, mysterious atmosphere",
    "epic": "grand, majestic, awe-inspiring atmosphere"
  };

  const mood = context.mood || "mysterious";

  return `${location}, ${moodMap[mood]}, ${baseStyle}`;
}

function buildEnemyPrompt(enemy: Enemy): string {
  const baseStyle = "D&D monster, creature design, menacing, detailed, fantasy art";

  return `${enemy.name}, ${enemy.type}.
    ${enemy.appearance || enemy.description}.
    ${baseStyle}`;
}
```

### Caching & Storage

```typescript
// lib/image/cache.ts

interface CachedImage {
  id: string;
  prompt: string;
  url: string;
  type: string;
  generatedAt: Date;
  campaignId: string;
}

// Store in database
model GeneratedImage {
  id          String   @id @default(uuid())
  campaignId  String
  type        String   // character, scene, enemy, etc.
  prompt      String
  imageUrl    String   // Uploaded to storage
  metadata    Json?
  generatedAt DateTime @default(now())
  campaign    Campaign @relation(fields: [campaignId], references: [id])
}

// Check cache before generating
async function getOrGenerateImage(
  prompt: string,
  type: string,
  campaignId: string
): Promise<string> {
  // Check if already generated
  const cached = await prisma.generatedImage.findFirst({
    where: {
      campaignId,
      type,
      prompt
    }
  });

  if (cached) {
    return cached.imageUrl;
  }

  // Generate new image
  const imageUrl = await generateImage(prompt);

  // Upload to storage (Vercel Blob or Cloudinary)
  const uploadedUrl = await uploadImage(imageUrl);

  // Cache in database
  await prisma.generatedImage.create({
    data: {
      campaignId,
      type,
      prompt,
      imageUrl: uploadedUrl
    }
  });

  return uploadedUrl;
}
```

---

## 🖼️ UI Integration

### Character Sheet with Portrait

```typescript
// components/character/CharacterSheet.tsx

export default function CharacterSheet({ character }: { character: Character }) {
  const [portrait, setPortrait] = useState<string | null>(character.portraitUrl);
  const [generating, setGenerating] = useState(false);

  const generatePortrait = async () => {
    setGenerating(true);

    const response = await fetch('/api/images/generate', {
      method: 'POST',
      body: JSON.stringify({
        type: 'character',
        characterId: character.id
      })
    });

    const data = await response.json();
    setPortrait(data.imageUrl);
    setGenerating(false);
  };

  return (
    <div className="character-sheet">
      <div className="portrait-section">
        {portrait ? (
          <img
            src={portrait}
            alt={character.characterName}
            className="character-portrait rounded-lg shadow-lg"
          />
        ) : (
          <div className="portrait-placeholder">
            {generating ? (
              <div className="animate-pulse">Generating portrait...</div>
            ) : (
              <button onClick={generatePortrait}>
                Generate Portrait
              </button>
            )}
          </div>
        )}
      </div>

      {/* Rest of character sheet */}
    </div>
  );
}
```

### Scene Display

```typescript
// components/dm/SceneDisplay.tsx

export default function SceneDisplay({ scene }: { scene: string }) {
  const [sceneImage, setSceneImage] = useState<string | null>(null);

  useEffect(() => {
    // Auto-generate scene image when location changes
    async function generateSceneImage() {
      const response = await fetch('/api/images/generate', {
        method: 'POST',
        body: JSON.stringify({
          type: 'scene',
          location: scene
        })
      });

      const data = await response.json();
      setSceneImage(data.imageUrl);
    }

    generateSceneImage();
  }, [scene]);

  return (
    <div className="scene-display">
      {sceneImage && (
        <div className="scene-image-container relative">
          <img
            src={sceneImage}
            alt={scene}
            className="w-full h-64 object-cover rounded-lg"
          />
          <div className="scene-overlay absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-4">
            <h2 className="text-2xl font-bold text-white">{scene}</h2>
          </div>
        </div>
      )}
    </div>
  );
}
```

### Enemy Card with Image

```typescript
// components/combat/EnemyCard.tsx

export default function EnemyCard({ enemy }: { enemy: Enemy }) {
  const [enemyImage, setEnemyImage] = useState<string | null>(null);

  useEffect(() => {
    async function loadEnemyImage() {
      const response = await fetch(`/api/images/enemy/${enemy.id}`);
      const data = await response.json();
      setEnemyImage(data.imageUrl);
    }

    loadEnemyImage();
  }, [enemy.id]);

  return (
    <div className="enemy-card border-2 border-red-600 rounded-lg p-4">
      {enemyImage && (
        <img
          src={enemyImage}
          alt={enemy.name}
          className="w-full h-48 object-cover rounded-t-lg"
        />
      )}

      <h3 className="text-xl font-bold mt-2">{enemy.name}</h3>
      <div className="hp-bar">
        HP: {enemy.stats.hp.current} / {enemy.stats.hp.max}
      </div>
    </div>
  );
}
```

---

## 📁 Updated Project Structure

```
lib/
├── ai/
│   ├── chatgpt.ts
│   ├── image-generation.ts      # NEW: Image generation logic
│   ├── prompt-builder.ts        # NEW: Smart prompt building
│   └── image-cache.ts           # NEW: Image caching
├── storage/
│   └── upload.ts                # NEW: Image upload to storage

app/api/
├── images/
│   ├── generate/route.ts        # NEW: Generate images
│   ├── character/[id]/route.ts  # NEW: Get character portrait
│   ├── scene/route.ts           # NEW: Get scene image
│   └── enemy/[id]/route.ts      # NEW: Get enemy image

components/
├── images/
│   ├── ImageGenerator.tsx       # NEW: Manual image generation UI
│   ├── ImageGallery.tsx         # NEW: Campaign image gallery
│   └── ImagePreview.tsx         # NEW: Image preview modal
```

---

## 🔑 API Routes

### Generate Image Endpoint

```typescript
// app/api/images/generate/route.ts

import { NextRequest, NextResponse } from 'next/server';
import OpenAI from 'openai';
import { prisma } from '@/lib/db/client';

const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });

export async function POST(req: NextRequest) {
  const { type, characterId, sceneDescription, enemyId } = await req.json();

  let prompt = '';

  // Build prompt based on type
  if (type === 'character' && characterId) {
    const character = await prisma.character.findUnique({
      where: { id: characterId }
    });
    prompt = buildCharacterPrompt(character);
  } else if (type === 'scene') {
    prompt = buildScenePrompt(sceneDescription);
  } else if (type === 'enemy' && enemyId) {
    const enemy = await prisma.enemy.findUnique({
      where: { id: enemyId }
    });
    prompt = buildEnemyPrompt(enemy);
  }

  // Check cache
  const cached = await prisma.generatedImage.findFirst({
    where: { prompt }
  });

  if (cached) {
    return NextResponse.json({ imageUrl: cached.imageUrl, cached: true });
  }

  // Generate image
  const response = await openai.images.generate({
    model: "dall-e-3",
    prompt: prompt,
    n: 1,
    size: "1024x1024",
    quality: "standard"
  });

  const imageUrl = response.data[0].url;

  // Upload to permanent storage (Vercel Blob Storage)
  const uploadedUrl = await uploadToStorage(imageUrl);

  // Save to database
  await prisma.generatedImage.create({
    data: {
      type,
      prompt,
      imageUrl: uploadedUrl,
      metadata: { characterId, enemyId }
    }
  });

  return NextResponse.json({ imageUrl: uploadedUrl, cached: false });
}
```

---

## 💾 Image Storage Options

### Option 1: **Vercel Blob Storage** ⭐ RECOMMENDED

**Pros**:
- Integrated with Vercel
- Simple API
- Automatic CDN
- Fast uploads

**Cost**:
- Free tier: 500GB bandwidth/month
- Storage: $0.15/GB/month
- Bandwidth: $0.40/GB

**For Friends**:
- ~80 images × 1MB = 80MB storage
- Cost: **~$0.01/month** (basically free)

```typescript
import { put } from '@vercel/blob';

async function uploadToStorage(imageUrl: string): Promise<string> {
  // Download image
  const response = await fetch(imageUrl);
  const blob = await response.blob();

  // Upload to Vercel Blob
  const { url } = await put(`campaign-images/${Date.now()}.png`, blob, {
    access: 'public',
  });

  return url;
}
```

### Option 2: **Cloudinary**

**Pros**:
- Generous free tier
- Image transformations
- Optimization

**Cost**:
- Free tier: 25GB storage, 25GB bandwidth
- **Free for your use case**

---

## 🎬 User Flow with Images

### Example: Combat Encounter

1. **DM Narration**: "A massive werewolf bursts from the tarp!"
2. **Trigger**: `combat_started` event
3. **Auto-Generate**: Enemy image (werewolf)
4. **Display**: Image appears above combat tracker
5. **Player Action**: "I use True Shot!"
6. **Roll**: Player rolls critical hit
7. **Optional**: Generate epic moment image
8. **Result**: "The dagger sinks into its eye!" + image updates

### Example: Character Creation

1. **Player**: Creates character (Lira the Fairy)
2. **Auto-Generate**: Character portrait from stats
3. **Preview**: Show generated portrait
4. **Option**: "Regenerate" if not satisfied
5. **Save**: Store portrait URL with character

---

## 🎨 Example Prompts for Your Characters

### Lira the Fairy
```
Portrait of Lira, an 11-inch tall fairy with iridescent shimmering wings,
luminous glowing skin, large expressive eyes, wearing delicate nature-inspired
clothing made of leaves and flowers, magical glow around her, cheerful but
fierce expression, holding a tiny lantern, fantasy character art, D&D portrait,
digital painting, detailed, high quality, magical atmosphere
```

### Rorek the Rune Knight
```
Portrait of Rorek, a stout muscular dwarf warrior wearing heavy ornate armor
covered in glowing runic etchings, holding a massive greatsword with fire runes,
battle-scarred face with braided beard, determined expression, fantasy character
art, D&D portrait, digital painting, heroic pose, dramatic lighting
```

### Elliathel the Elf Ranger
```
Portrait of Elliathel, an agile female elf ranger with long flowing hair,
keen sharp eyes, wearing leather armor, holding an elegant longbow and a
glowing moon-blessed silver dagger, graceful pose, surrounded by faint
moonlight aura, fantasy character art, D&D portrait, digital painting,
mystical atmosphere
```

### Veyrath the Dark High Mage
```
Portrait of Veyrath, a tall male mage with dark flowing robes covered in
shadow patterns, glowing eyes with purple and black energy, holding an ancient
floating spellbook surrounded by dark magic, mysterious and powerful aura,
fantasy character art, D&D portrait, digital painting, dramatic lighting,
arcane atmosphere
```

---

## 📊 Recommended Setup for Friends Group

### Budget-Conscious (Recommended)

```typescript
{
  "characterPortraits": "DALL-E 3 Standard ($0.16 total)",
  "sceneImages": "Stable Diffusion XL ($0.04 per session)",
  "enemies": "Stable Diffusion XL ($0.01 per enemy)",
  "epicMoments": "Manual generation (player request)",
  "storage": "Vercel Blob (free tier)",

  "totalPerCampaign": "~$1-2",
  "generateOnDemand": true, // Don't pre-generate everything
  "cacheAggressively": true // Reuse when possible
}
```

---

## 🚀 Implementation Priority

### Phase 1: Core Images (Week 1)
- [ ] Character portrait generation
- [ ] Basic image display in character sheet
- [ ] Image caching in database

### Phase 2: Scene Images (Week 2)
- [ ] Scene generation on location change
- [ ] Scene display component
- [ ] Storage integration (Vercel Blob)

### Phase 3: Enemy & Items (Week 3)
- [ ] Enemy image generation
- [ ] Item card images
- [ ] Image gallery view

### Phase 4: Epic Moments (Week 4)
- [ ] Manual generation UI
- [ ] Critical hit image generation
- [ ] Campaign highlight reel

---

## 🎉 Final Recommendation

**For your friends group, I recommend**:

1. **DALL-E 3 for character portraits** ($0.16 one-time) - High quality, worth it
2. **Stable Diffusion XL for everything else** (~$0.50 total) - Cheap and good enough
3. **Vercel Blob Storage** (free) - Simple and integrated
4. **On-demand generation** - Generate only what you need
5. **Manual epic moments** - Let players request special images

**Total cost per 5-hour campaign**: **~$0.70-1.00** 🎉

Basically the cost of a coffee for an entire epic campaign with stunning visuals!

---

## 📝 Environment Variables to Add

```bash
# .env.local

# Image Generation
OPENAI_API_KEY=sk-...              # For DALL-E 3 (already have)
REPLICATE_API_TOKEN=r8_...         # For Stable Diffusion XL (optional)

# Image Storage
BLOB_READ_WRITE_TOKEN=vercel_...   # Vercel Blob Storage
```

---

## 🎨 Example Implementation

Ready-to-use code:

```typescript
// lib/ai/image-generation.ts
import OpenAI from 'openai';
import Replicate from 'replicate';

const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });
const replicate = new Replicate({ auth: process.env.REPLICATE_API_TOKEN });

export async function generateCharacterImage(character: Character): Promise<string> {
  const prompt = buildCharacterPrompt(character);

  // Use DALL-E 3 for high quality
  const response = await openai.images.generate({
    model: "dall-e-3",
    prompt,
    size: "1024x1024",
    quality: "standard"
  });

  return response.data[0].url;
}

export async function generateSceneImage(scene: string): Promise<string> {
  const prompt = buildScenePrompt(scene);

  // Use Stable Diffusion for cost savings
  const output = await replicate.run(
    "stability-ai/sdxl:latest",
    { input: { prompt, width: 1024, height: 1024 } }
  ) as string[];

  return output[0];
}
```

This will make your DnD sessions **incredibly immersive**! 🎨✨
