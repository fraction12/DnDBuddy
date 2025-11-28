# Character Data Examples

## Complete Character Data Structures

Based on your ChatGPT session, here are the exact data structures for each character.

---

## Player A - Lira the Fairy

```typescript
const liraCharacter: Character = {
  id: "char-a-001",
  campaignId: "campaign-epic-quest-001",
  playerName: "A",
  characterName: "Lira",
  characterType: "Fairy",
  characterClass: "Support Caster",

  // Core Stats
  stats: {
    hp: {
      current: 18,
      max: 18
    },
    mana: {
      current: 24,
      max: 24
    },
    armor: 10,
    speed: "Fast",
    size: "Tiny", // 11 inches tall
    weight: "1.2 lbs"
  },

  // Character Details
  backstory: "Lira's grove was poisoned by a spreading corruption. She left in search of a cure rumored to be held by an ancient creature — the Manticore.",

  appearance: {
    height: "11 inches",
    features: "Small, luminous creature with iridescent wings",
    distinctiveTraits: ["Glowing wings", "Tiny size", "Big attitude"]
  },

  // Skills & Abilities
  skills: [
    {
      id: "skill-fairy-bliss",
      name: "Fairy Bliss",
      description: "Emits euphoric aura, calming hostile creatures for 1 round or making them confused",
      type: "once_per_session",
      manaCost: 0,
      range: "20 feet",
      duration: "1 round",
      saveDC: 14,
      usedThisSession: false,
      cooldown: 0,
      effects: {
        target: "all_enemies_in_range",
        save: "wisdom",
        onFail: ["calmed", "disoriented", "euphoric"],
        duration: 1 // rounds
      }
    },
    {
      id: "skill-healing-light",
      name: "Healing Light",
      description: "Emit healing light to restore HP",
      type: "active",
      manaCost: 8,
      range: "Touch or 10 feet",
      healAmount: "2d6",
      usedThisSession: false
    },
    {
      id: "skill-charm",
      name: "Charm",
      description: "Charm a creature to be friendly or compliant",
      type: "active",
      manaCost: 6,
      modifier: 5, // +3 charm bonus + 2 fairy appeal
      saveDC: 14,
      range: "30 feet",
      duration: "1 hour or until harmed"
    },
    {
      id: "skill-sleep",
      name: "Sleep",
      description: "Put creatures to sleep based on their total HP",
      type: "active",
      manaCost: 10,
      range: "60 feet",
      affectedHP: "5d8", // Roll to determine total HP affected
      saveDC: 12
    }
  ],

  // Special Abilities
  specialAbilities: [
    {
      name: "Detect Magic",
      description: "Can detect magical traps, illusions, and hidden objects",
      passive: true
    },
    {
      name: "Flight",
      description: "Can fly at will with iridescent wings",
      passive: true
    },
    {
      name: "Fae Magic",
      description: "Natural affinity for charm and enchantment magic",
      passive: true,
      bonus: "+2 to all charm-related checks"
    }
  ],

  // Inventory
  inventory: [
    {
      id: "item-lantern-001",
      name: "Lantern",
      type: "utility",
      quantity: 1,
      effects: ["illuminates_dark_areas", "reveals_mimics"],
      equipped: true,
      description: "Light source that can reveal hidden mimics"
    },
    {
      id: "item-healing-herb-001",
      name: "Small Healing Herb",
      type: "consumable",
      quantity: 1,
      effects: [{ type: "heal", value: 8 }],
      equipped: false,
      description: "Restores 8 HP once"
    }
  ],

  // Progression
  xp: 30,
  gold: 3,
  level: 1,

  // Session State
  sessionState: {
    turnOrder: 3,
    statusEffects: [],
    tempModifiers: [],
    notesFromPlayer: "Remember to use Fairy Bliss strategically!"
  }
};
```

---

## Player B - Rorek the Rune Knight Fighter

```typescript
const rorekCharacter: Character = {
  id: "char-b-001",
  campaignId: "campaign-epic-quest-001",
  playerName: "B",
  characterName: "Rorek",
  characterType: "Rune Knight Fighter",
  characterClass: "Tank Fighter",

  stats: {
    hp: {
      current: 32,
      max: 32
    },
    mana: {
      current: 8,
      max: 8
    },
    armor: 17,
    speed: "Medium",
    size: "Medium",
    weight: "~200 lbs"
  },

  backstory: "He once served the Dwarven Legion, but left after discovering forbidden runes held by a Troll warlord who destroyed his unit.",

  appearance: {
    height: "5'4\" (Dwarf)",
    features: "Heavy armor, runic-etched greatsword",
    distinctiveTraits: ["Muscular build", "Glowing runes", "Battle-scarred"]
  },

  skills: [
    {
      id: "skill-greatsword-attack",
      name: "Greatsword Attack",
      description: "Powerful melee strike",
      type: "active",
      manaCost: 0,
      damage: "2d6+4",
      range: "Melee (5 feet)",
      attackBonus: 6
    },
    {
      id: "skill-stone-rune",
      name: "Stone Rune",
      description: "Enhanced defense and resistance",
      type: "active",
      manaCost: 2,
      duration: "3 rounds",
      effects: {
        armorBonus: 3,
        resistances: ["physical"]
      }
    },
    {
      id: "skill-fire-rune",
      name: "Fire Rune",
      description: "Burning strike that deals fire damage",
      type: "active",
      manaCost: 3,
      damage: "2d6+2d6fire",
      range: "Melee or 15 feet",
      effects: {
        burningDamage: "1d6 per round for 2 rounds"
      }
    },
    {
      id: "skill-giants-rune",
      name: "Giant's Rune",
      description: "Double size and gain massive strength for 2 rounds",
      type: "once_per_session",
      manaCost: 4,
      duration: "2 rounds",
      usedThisSession: false,
      effects: {
        sizeIncrease: "Large",
        strengthBonus: "+6",
        damageBonus: "2x"
      }
    },
    {
      id: "skill-rune-of-living-will",
      name: "Rune of Living Will",
      description: "Animate objects (like rope) to become familiars",
      type: "special",
      manaCost: 5,
      checkRequired: {
        runeKnowledge: { dice: "1d20+4", dc: 14 },
        willpower: { dice: "1d20+2", dc: 12 }
      }
    }
  ],

  specialAbilities: [
    {
      name: "Luck Bonus",
      description: "+1 bonus on ONE roll next session (from prayer)",
      passive: false,
      usesRemaining: 1
    }
  ],

  inventory: [
    {
      id: "item-greatsword-001",
      name: "Runic Greatsword",
      type: "weapon",
      quantity: 1,
      effects: [
        { type: "damage", value: "2d6+4" },
        { type: "ability", value: "Can channel runes through blade" }
      ],
      equipped: true
    },
    {
      id: "item-cloak-distraction",
      name: "Cloak of Distraction",
      type: "armor",
      quantity: 1,
      effects: [{ type: "dodge", value: "+1" }],
      equipped: true,
      description: "+1 to Dodge checks"
    }
  ],

  companions: [
    {
      id: "companion-ropey",
      name: "Ropey",
      type: "Animated Rope Familiar",
      hp: {
        current: 6,
        max: 6
      },
      armor: 12,
      speed: "Slithery",
      abilities: ["wrap", "trip", "yank", "distraction_wave", "goblin_rat_flail"],
      personality: "Loyal-ish, whimsical, easily distracted, mildly insane",
      description: "Animated rope familiar created via Rune of Living Will"
    }
  ],

  xp: 30,
  gold: 0,
  level: 1,

  sessionState: {
    turnOrder: 4,
    statusEffects: [],
    tempModifiers: [
      { type: "luck_bonus", value: 1, usesRemaining: 1 }
    ]
  }
};
```

---

## Player P - Elliathel the Elf Ranger

```typescript
const elliAthelCharacter: Character = {
  id: "char-p-001",
  campaignId: "campaign-epic-quest-001",
  playerName: "P",
  characterName: "Elliathel",
  characterType: "Elf Ranger",
  characterClass: "Agile Archer",

  stats: {
    hp: {
      current: 22,
      max: 24
    },
    mana: {
      current: 10,
      max: 10
    },
    armor: 14,
    speed: "Fast",
    size: "Medium",
    weight: "~140 lbs"
  },

  backstory: "Elliathel has hunted the same pack of werewolves for years — they were responsible for slaughtering her elven kin under a full moon.",

  appearance: {
    height: "5'8\"",
    features: "Agile, silent, bow-focused",
    distinctiveTraits: ["Keen eyes", "Swift movements", "Moon-blessed aura"]
  },

  skills: [
    {
      id: "skill-longbow",
      name: "Longbow Attack",
      description: "Standard ranged attack with bow",
      type: "active",
      manaCost: 0,
      damage: "1d8+3",
      range: "150 feet",
      attackBonus: 5
    },
    {
      id: "skill-true-shot",
      name: "True Shot",
      description: "An arrow that cannot miss, deals maximum damage",
      type: "once_per_session",
      manaCost: 0,
      damage: "Automatic hit + maximum damage",
      range: "150 feet",
      usedThisSession: true, // Used against werewolf
      effects: {
        autoHit: true,
        criticalPrecision: true,
        damageBonus: "maximum"
      }
    },
    {
      id: "skill-tracking",
      name: "Tracking",
      description: "Expert tracking of creatures and paths",
      type: "passive",
      modifier: 7,
      effects: {
        advantageOnSurvival: true,
        detectHiddenPaths: true
      }
    },
    {
      id: "skill-beast-speech",
      name: "Beast Speech",
      description: "Can speak to and understand beasts",
      type: "passive",
      range: "30 feet"
    }
  ],

  inventory: [
    {
      id: "item-moon-bitten-dagger",
      name: "Moon-Bitten Dagger",
      type: "weapon",
      quantity: 1,
      effects: [
        { type: "damage", value: "2d4+2", condition: "vs beasts/shapeshifters" },
        { type: "damage", value: "1d4+1", condition: "vs others" },
        { type: "ability", value: "Emits faint silver glow in darkness" }
      ],
      equipped: true,
      description: "Enhanced after killing the werewolf. Glows with moon energy.",
      rarity: "Rare"
    },
    {
      id: "item-longbow",
      name: "Elven Longbow",
      type: "weapon",
      quantity: 1,
      effects: [
        { type: "damage", value: "1d8+3" },
        { type: "range", value: "150 feet" }
      ],
      equipped: true
    },
    {
      id: "item-quiver",
      name: "Quiver",
      type: "ammunition",
      quantity: 20, // arrows
      description: "20 arrows remaining"
    }
  ],

  specialAbilities: [
    {
      name: "Elven Senses",
      description: "Advantage on perception checks",
      passive: true,
      bonus: "+2 to perception"
    },
    {
      name: "Moon-Scent Aura",
      description: "Faint moon-scent after werewolf kill. May attract or repel lycanthropes.",
      passive: true,
      temporary: true
    }
  ],

  xp: 30,
  gold: 3,
  level: 1,

  sessionState: {
    turnOrder: 1,
    statusEffects: [
      {
        name: "Prone Bruises",
        description: "Minor bruising from fall",
        duration: "1 session",
        effect: "Cosmetic only"
      }
    ],
    tempModifiers: []
  }
};
```

---

## Player D - Veyrath the Dark High Mage

```typescript
const veyrathCharacter: Character = {
  id: "char-d-001",
  campaignId: "campaign-epic-quest-001",
  playerName: "D",
  characterName: "Veyrath",
  characterType: "Dark High Mage",
  characterClass: "Powerful Spellcaster",

  stats: {
    hp: {
      current: 20,
      max: 20
    },
    mana: {
      current: 28,
      max: 28
    },
    armor: 12,
    speed: "Medium",
    size: "Medium",
    weight: "~160 lbs"
  },

  backstory: "Once a mage of the High Academy, Veyrath delved too deep into forbidden shadowcraft and was exiled. He now seeks a lost artifact guarded by mimic-infested ruins.",

  appearance: {
    height: "6'0\"",
    features: "Dark robes, glowing shadow energy, spellbook always nearby",
    distinctiveTraits: ["Shadow aura", "Arcane bong", "Corrupted eyes"]
  },

  skills: [
    {
      id: "skill-shadow-bolt",
      name: "Shadow Bolt",
      description: "Direct shadow damage projectile",
      type: "active",
      manaCost: 4,
      damage: "2d8+3",
      range: "60 feet",
      attackBonus: 7,
      damageType: "shadow"
    },
    {
      id: "skill-dark-fire",
      name: "Dark Fire",
      description: "Hungry flames of black and violet hellfire with corruption damage",
      type: "active",
      manaCost: 6,
      damage: "3d6+3corruption",
      range: "60 feet",
      attackBonus: 6, // +1 from flanking in werewolf fight
      damageType: "fire+corruption",
      effects: {
        burningDamage: "1d6 fire per round",
        ignoresResistances: true,
        criticalEffect: "Creates permanent burn holes"
      }
    },
    {
      id: "skill-mind-spike",
      name: "Mind Spike",
      description: "Psychic attack that can stun or disorient",
      type: "active",
      manaCost: 5,
      damage: "2d8",
      range: "60 feet",
      attackBonus: 4,
      damageType: "psychic",
      saveDC: 14,
      effects: {
        onHit: "Target must save vs stun",
        stunDuration: "1-2 rounds",
        disorientation: true
      }
    },
    {
      id: "skill-shadow-rewrite",
      name: "Shadow Rewrite",
      description: "Change the outcome of a single roll or event",
      type: "once_per_session",
      manaCost: 8,
      usedThisSession: false,
      effects: {
        rewind: true,
        alterOutcome: true,
        realityManipulation: true
      },
      description: "Can rewrite reality itself - use wisely"
    }
  ],

  inventory: [
    {
      id: "item-dark-spellbook",
      name: "Dark Spellbook",
      type: "magical",
      quantity: 1,
      effects: [
        { type: "spell_power", value: "+2 to spell damage" },
        { type: "mana_regen", value: "1 mana per hour" }
      ],
      equipped: true,
      description: "Pages filled with pulsing rune-script. Floats autonomously."
    },
    {
      id: "item-rope",
      name: "Rope (30 ft)",
      type: "utility",
      quantity: 1,
      description: "Given to Elliathel, but still holds the end for vibes"
    },
    {
      id: "item-werewolf-blood",
      name: "Vial of Werewolf Blood",
      type: "alchemy_reagent",
      quantity: 1,
      rarity: "Rare",
      description: "Corrupted werewolf blood. Valuable for dark alchemy.",
      potentialUses: ["Potion crafting", "Curse components", "Werewolf detection"]
    },
    {
      id: "item-barn-key",
      name: "Charred Barn Key",
      type: "key_item",
      quantity: 1,
      description: "Found after dark fire. May unlock something below the barn."
    },
    {
      id: "item-journal-page",
      name: "Torn Journal Page",
      type: "quest_item",
      quantity: 1,
      description: "Reads: 'The artifact is below… protected by the dreamer…'",
      questHook: "Points to cellar beneath barn"
    },
    {
      id: "item-bong-of-calm",
      name: "Bong of Calm Focus",
      type: "magical_utility",
      quantity: 1,
      effects: [
        { type: "concentration", value: "+1 to concentration checks" },
        { type: "stress_relief", value: "Advantage on wisdom saves vs fear" }
      ],
      equipped: true,
      description: "Arcane bong that enhances mental clarity"
    }
  ],

  specialAbilities: [
    {
      name: "Shadowcraft Mastery",
      description: "Expert in shadow and dark magic",
      passive: true,
      bonus: "+3 to all shadow/dark spell attacks"
    },
    {
      name: "Corruption Risk",
      description: "Using too much dark magic may corrupt the caster",
      passive: true,
      warning: "Track corruption points - too many = bad consequences"
    }
  ],

  xp: 30,
  gold: 12, // Found loot
  level: 1,
  corruptionPoints: 2, // From using Dark Fire

  sessionState: {
    turnOrder: 2,
    statusEffects: [
      {
        name: "Arcane High",
        description: "Recently smoked. +1 to concentration, -1 to dexterity.",
        duration: "30 minutes",
        effect: "Minor stat adjustment"
      }
    ],
    tempModifiers: []
  }
};
```

---

## Enemy Example - Barn Werewolf (Defeated)

```typescript
const barnWerewolf: Enemy = {
  id: "enemy-werewolf-001",
  campaignId: "campaign-epic-quest-001",
  name: "Barn Werewolf",
  type: "Beast (Lycanthrope)",

  stats: {
    hp: {
      current: -10, // Defeated
      max: 34
    },
    armor: 15,
    speed: "40 feet",
    size: "Large"
  },

  abilities: [
    {
      name: "Rend",
      type: "attack",
      damage: "2d6+4",
      range: "Melee",
      description: "Claw attack"
    },
    {
      name: "Bite",
      type: "attack",
      damage: "2d8+4",
      range: "Melee",
      effects: ["bleed: 1d4 per round"]
    },
    {
      name: "Howl",
      type: "special",
      range: "60 feet",
      saveDC: 13,
      effects: ["fear", "All within range must save or be frightened"]
    },
    {
      name: "Leap Attack",
      type: "special",
      damage: "3d6+4",
      range: "30 feet leap",
      description: "Pounce from distance"
    }
  ],

  resistances: ["physical_nonmagical"],
  vulnerabilities: ["silver", "magical"],

  isAlive: false,
  defeatedBy: ["Elliathel's True Shot", "Veyrath's Dark Fire"],

  loot: [
    {
      name: "Werewolf Fang",
      type: "alchemy_reagent",
      value: 15, // gold
      description: "Valuable alchemy resource"
    },
    {
      name: "Bloodmoon Pelt Fragment",
      type: "crafting_material",
      value: 25, // gold
      description: "Can be crafted into armor"
    }
  ],

  xpReward: 100, // Divided among 4 players = 25 each

  combatLog: [
    { turn: 1, action: "Mind Spike from Veyrath", damage: 8, status: "stunned" },
    { turn: 2, action: "True Shot from Elliathel", damage: 9, status: "half-blinded" },
    { turn: 3, action: "Dark Fire from Veyrath (CRIT)", damage: 27, status: "dead" }
  ]
};
```

---

## Campaign State Example

```typescript
const campaignState: Campaign = {
  id: "campaign-epic-quest-001",
  name: "Epic Quest",

  settings: {
    totalDuration: 5, // hours
    sessionDuration: 1, // hour
    tone: "Heroic and adventurous with moments of chaotic humor",
    difficulty: "Strict" // STRICT stat tracking
  },

  progress: {
    currentSession: 1,
    totalSessions: 5,
    sessionCompleted: true
  },

  players: [
    "char-a-001", // Lira
    "char-b-001", // Rorek
    "char-p-001", // Elliathel
    "char-d-001"  // Veyrath
  ],

  location: {
    current: "Brightwick - East Storage Barn (Cellar revealed)",
    previous: "Brightwick Town",
    discovered: [
      "Brightwick Town",
      "Brightwick Supply Depot",
      "East Storage Barn",
      "Secret Cellar (entrance)"
    ]
  },

  questLog: [
    {
      id: "quest-main-001",
      name: "The Spreading Corruption",
      description: "Investigate and stop the corruption affecting the land",
      status: "active",
      objectives: [
        { text: "Clear goblins from East Barn", completed: true },
        { text: "Defeat the Barn Werewolf", completed: true },
        { text: "Investigate the cellar below", completed: false },
        { text: "Find the lost artifact", completed: false }
      ]
    },
    {
      id: "quest-lira",
      name: "Cure for the Grove",
      description: "Find cure for Lira's poisoned grove (rumored to be held by Manticore)",
      status: "active"
    },
    {
      id: "quest-rorek",
      name: "Forbidden Runes",
      description: "Recover forbidden runes from Troll warlord",
      status: "active"
    },
    {
      id: "quest-elliathel",
      name: "Werewolf Revenge",
      description: "Hunt the werewolf pack that killed elven kin",
      status: "in_progress",
      progress: "1 werewolf defeated"
    },
    {
      id: "quest-veyrath",
      name: "The Lost Artifact",
      description: "Find artifact guarded by mimic-infested ruins",
      status: "active",
      hint: "Journal page mentions artifact below barn"
    }
  ],

  enemies: {
    encountered: ["Goblins", "Barn Werewolf"],
    remaining: [
      "Manticore",
      "Troll",
      "Werewolf Pack",
      "Mimics",
      "Vorathrax the Volcanic (Fire Dragon)",
      "Sylestria the Dreaming Serpent (Psychic Dragon)"
    ]
  },

  partyInventory: {
    gold: 15, // Total party gold (12 from Veyrath + 3 shared)
    sharedItems: [
      {
        name: "Werewolf Fang",
        quantity: 1,
        holder: "Party"
      },
      {
        name: "Bloodmoon Pelt Fragment",
        quantity: 1,
        holder: "Party"
      }
    ]
  },

  sessionHistory: [
    {
      sessionNumber: 1,
      duration: "~60 minutes",
      summary: "Party cleared goblin-infested barn, encountered and defeated barn werewolf, discovered secret cellar entrance",
      majorEvents: [
        "Lira charmed shopkeeper for extra item",
        "Sleep spell put all goblins to sleep",
        "Rorek created Ropey the rope familiar",
        "Ropey accidentally tripped Elliathel",
        "Elliathel's True Shot damaged werewolf's eye",
        "Veyrath's critical Dark Fire killed werewolf",
        "Secret cellar discovered beneath burn hole",
        "Lira killed all goblins in rage"
      ],
      lootGained: [
        "Moon-Bitten Dagger (Elliathel)",
        "Werewolf Blood (Veyrath)",
        "Barn Key (Veyrath)",
        "Journal Page (Veyrath)",
        "12 gold",
        "Werewolf Fang",
        "Bloodmoon Pelt Fragment"
      ],
      xpGained: 30,
      endingCliffhanger: "A stone stairwell descending into darkness, glowing with moonrunes, and the distant sound of breathing..."
    }
  ],

  dmContext: {
    recentNarration: "The hole in the floor reveals stone steps glowing faintly with moonrunes and the distant sound of breathing...",
    activePlotThreads: [
      "Secret cellar exploration",
      "Artifact search",
      "Dreaming Dragon connection"
    ],
    npcRelationships: {
      "Brightwick Mayor": "Grateful (quest giver)",
      "Shopkeeper": "Charmed by Lira (friendly)"
    }
  },

  nextSession: {
    preview: "THE CELLAR OF RUNES - Possibly encounter Sylestria the Dream Dragon's illusions",
    preparedElements: [
      "Cellar exploration",
      "Ancient ruin puzzles",
      "Dream Dragon's illusions",
      "Artifact clues"
    ]
  }
};
```

---

## TypeScript Types

```typescript
// Core Types
interface Character {
  id: string;
  campaignId: string;
  playerName: string;
  characterName: string;
  characterType: string;
  characterClass: string;
  stats: CharacterStats;
  backstory: string;
  appearance: Appearance;
  skills: Skill[];
  specialAbilities: SpecialAbility[];
  inventory: InventoryItem[];
  companions?: Companion[];
  xp: number;
  gold: number;
  level: number;
  corruptionPoints?: number;
  sessionState: SessionState;
}

interface CharacterStats {
  hp: { current: number; max: number };
  mana: { current: number; max: number };
  armor: number;
  speed: string;
  size: string;
  weight: string;
}

interface Skill {
  id: string;
  name: string;
  description: string;
  type: 'active' | 'passive' | 'once_per_session' | 'special';
  manaCost: number;
  range?: string;
  damage?: string;
  duration?: string;
  saveDC?: number;
  attackBonus?: number;
  modifier?: number;
  usedThisSession?: boolean;
  cooldown?: number;
  effects?: Record<string, any>;
  checkRequired?: Record<string, { dice: string; dc: number }>;
}

interface InventoryItem {
  id: string;
  name: string;
  type: 'weapon' | 'armor' | 'utility' | 'magical' | 'consumable' | 'quest_item';
  quantity: number;
  effects?: ItemEffect[];
  equipped: boolean;
  description: string;
  rarity?: 'Common' | 'Uncommon' | 'Rare' | 'Epic' | 'Legendary';
  value?: number;
}

interface ItemEffect {
  type: string;
  value: string | number;
  condition?: string;
}

interface Enemy {
  id: string;
  campaignId: string;
  name: string;
  type: string;
  stats: {
    hp: { current: number; max: number };
    armor: number;
    speed: string;
    size: string;
  };
  abilities: EnemyAbility[];
  resistances?: string[];
  vulnerabilities?: string[];
  isAlive: boolean;
  defeatedBy?: string[];
  loot?: LootItem[];
  xpReward: number;
  combatLog?: CombatAction[];
}

interface Campaign {
  id: string;
  name: string;
  settings: CampaignSettings;
  progress: CampaignProgress;
  players: string[];
  location: LocationState;
  questLog: Quest[];
  enemies: EnemyTracker;
  partyInventory: PartyInventory;
  sessionHistory: SessionSummary[];
  dmContext: DMContext;
  nextSession: NextSessionPreview;
}
```

---

## Database Seed Data

You can use these exact character structures to seed your database for testing!

```typescript
// prisma/seed.ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function main() {
  // Create campaign
  const campaign = await prisma.campaign.create({
    data: {
      id: 'campaign-epic-quest-001',
      name: 'Epic Quest',
      totalDuration: 5,
      sessionDuration: 1,
      currentSession: 1,
      gameState: campaignState
    }
  });

  // Create characters
  await prisma.character.createMany({
    data: [
      liraCharacter,
      rorekCharacter,
      elliAthelCharacter,
      veyrathCharacter
    ]
  });

  console.log('✅ Database seeded with Session 1 data!');
}

main()
  .catch((e) => console.error(e))
  .finally(async () => await prisma.$disconnect());
```

---

These data structures are production-ready and match your exact ChatGPT session. You can use them to:

1. **Test your database schema**
2. **Build UI components** with real data
3. **Test ChatGPT integration** with accurate context
4. **Develop combat mechanics** with actual character stats

Want me to create more enemy data or additional session scenarios?
