# Christian Marriage Counseling App — Complete Architecture & Design Document

> **Status:** Design v1.0 — Ready for implementation
> **Target:** Single-file PWA, fully offline, zero-dependency
> **Primary Framework:** Gottman Method + Love & Respect + Scripture Synthesis

---

## 1. APP NAME & BRANDING (3 Proposals)

### Option A — **"One Flesh"** (Recommended)
- **Scripture:** *"They two shall be one flesh"* — Ephesians 5:31
- **Rationale:** Captures the biblical vision of marriage as unity. Short, memorable, domain-friendly (oneflesh.app). Evokes the goal of the app — restoring oneness.
- **Tagline:** *Restoring Unity, One Conversation at a Time*
- **Color Palette:** Deep teal (#0B4F5C) + warm gold (#C9A84C) — calm wisdom meeting sacred union

### Option B — **"Cana"**
- **Scripture:** The wedding at Cana (John 2)
- **Tagline:** *Where Christ Meets the Conversation*
- **Vibe:** Minimalist, liturgical, warm

### Option C — **"The Peace Table"**
- **Scripture:** *"Blessed are the peacemakers"* (Matthew 5:9)
- **Tagline:** *Sit. Speak. Heal.*
- **Vibe:** Inviting, grounded, active

> **Decision: "One Flesh"** — strongest biblical grounding, memorable, communicates the mission in two words.

---

## 2. COUNSELING METHODOLOGY

### Recommended Synthesis: Gottman + Love & Respect + Biblical Wisdom

No single framework is sufficient. The app synthesizes three complementary methodologies:

### 2A. Foundation: Gottman's Sound Relationship House
**Why base:** Most empirically validated marriage research (40+ years, 3,000+ couples, 94% prediction accuracy).

**The 7 Levels:**
1. **Build Love Maps** — Know your spouse's inner world
2. **Share Fondness & Admiration** — Express genuine appreciation
3. **Turn Towards** — Respond to bids for connection
4. **Positive Perspective** — Positive sentiment override
5. **Manage Conflict** — Soft startup, accept influence, self-soothe (core engine)
6. **Make Life Dreams Come True** — Support each other's aspirations
7. **Create Shared Meaning** — Rituals, values, mission

**Two weight-bearing walls:** Trust & Commitment

### 2B. Gender-Communication Layer: Love & Respect (Eggerichs)
The "Crazy Cycle": *Without love, she reacts without respect → Without respect, he reacts without love → (repeat)*

**App use:** When complaint is "I feel unloved" → app validates need for love, then asks: "Could he have felt disrespected?" When complaint is "I feel disrespected" → app validates need for respect, then asks: "Could she have felt unloved?" Never takes sides — surfaces the cycle.

### 2C. Spiritual Anchor: Biblical Marriage Wisdom
**Core passages:**
| Passage | Principle | Tags |
|---------|-----------|------|
| Ephesians 5:21-33 | Mutual submission, one flesh | `unity`, `one-flesh` |
| 1 Corinthians 13:4-7 | Love is patient, kind | `patience`, `kindness` |
| Proverbs 15:1 | "A gentle answer turns away wrath" | `gentleness`, `deescalation` |
| Proverbs 31:10-31 | Partnership, not pedestal | `partnership`, `respect` |
| 1 Peter 3:7 | "Husbands, treat your wife with respect" | `husband-duty` |
| James 1:19 | "Quick to listen, slow to speak" | `listening`, `anger` |
| Matthew 5:9 | Peacemakers | `reconciliation` |
| Ecclesiastes 4:9-12 | Two better than one | `partnership`, `support` |

### 2D. Three-Pass Analysis
1. **Gottman Pass** — categorize conflict (solvable/perpetual/values), detect Four Horsemen (criticism, contempt, defensiveness, stonewalling)
2. **Love & Respect Pass** — identify Crazy Cycle dynamics
3. **Biblical Pass** — match underlying need to Scripture + counselor guidance

---

## 3. USER FLOW

```
[Open App] → Welcome Screen
  → [Start New Session]
    → Step 1: "What's the issue today?" [Type or 🎤 Speak]
    → Step 2: Spouse A speaks → Spouse B speaks
    → Step 3: App analyzes (2-5s reflecting animation)
    → Step 4: Wisdom Screen
      ├── Neutral restatement of both sides
      ├── Where each may be stuck (non-judgmental patterns)
      ├── Wisdom: Scripture + Counselor Insight + Practical Step
      ├── Prayer (issue-specific)
      └── Reconciliation Prompt
  → [Past Sessions] [Love Languages Quiz] [About]
```

**Step 1 — Issue Naming:** "What's the issue today?" Type or voice. App rephrases neutrally.

**Step 2 — Two-Sided Listening:** Spouse A speaks first (uninterrupted), then Spouse B. Device passed between them.

**Step 3 — Analysis:** Rule engine processes text for topics, sentiment, patterns, Crazy Cycle. Shows "reflecting" animation with rotating Scripture.

**Step 4 — Wisdom:** Neutral restatement → "I notice..." observations for each → Scripture + insight + action → prayer → "Would you be willing to..." reconciliation prompt.

---

## 4. UI/UX DESIGN

### Design Principles
- Calm, not clinical. Warm colors, soft curves, generous whitespace.
- Sacred pacing — soft pulsing, deliberate transitions.
- Shared device — designed for passing a phone/tablet between spouses.
- Accessible — min 18px body, high contrast, screen-reader friendly.

### Screen Descriptions

**Welcome/Home:** Warm gradient (teal→ivory). Interlocking rings logo. "Restoring Unity, One Conversation at a Time." Single CTA: "Begin a Session." Bottom nav: Past Sessions, About, Love Languages Quiz. First-run overlay: 3-card intro.

**Issue Input:** "What's the issue today?" Large text area, mic button. Helper: "Just describe it as you would to a friend."

**Spouse Speaks:** "[Spouse A], share your side." Same large text area. Button: "✓ I'm done — pass to my spouse." Transition: "Thank you. Now let me hear from you, [B]."

**Reflecting:** Centered pulsing warm light. Rotating Scripture. Auto-advances 2-5s.

**Wisdom (core, scrollable):** Color-coded cards — 📖 Scripture (gold), 💡 Insight (teal), 🛠️ Practical Step (sage), 🙏 Prayer (lavender). Sticky reconciliation prompt bottom.

**Prayer:** Full-screen prayer text. "Amen" button. "← Back to Wisdom."

**Session History:** List with date, topic, reconciliation status. Tap for full detail.

### Colors & Typography
- Primary: Deep Teal (#0B4F5C)
- Secondary: Warm Gold (#C9A84C)
- Background: Soft ivory (#F9F5F0)
- Accent: Muted sage (#7A9B6B)
- No red (anger association) → soft amber (#D4A34A)
- Headings: Georgia serif. Body: Atkinson Hyperlegible or system sans. Scripture: italic Georgia. Min body: 18px.

---

## 5. TECHNICAL ARCHITECTURE

### 5A. PWA Strategy

```
Browser → Single index.html + CSS + JS
            ├── manifest.json (PWA manifest)
            ├── service-worker.js (offline support)
            └── app.html (everything)
         → Local Storage: IndexedDB (sessions) + localStorage (settings)
         → Speech-to-Text: Web Speech API (browser-native)
```

**No server. Zero cloud. Everything on-device.**

### 5B. Tech Stack (MVP)
| Layer | Technology | Why |
|-------|-----------|-----|
| Runtime | Single `index.html` | Zero deps, no build step |
| CSS | Pure CSS3 (custom properties, grid, flexbox, animations) | Instant, no framework overhead |
| JS | Vanilla JavaScript ES6+ | No npm, no transpilation |
| PWA | manifest.json + service-worker.js | Offline-first, installable |
| Storage | IndexedDB + localStorage | Structured, persists cache clear |
| Speech | Web Speech API (SpeechRecognition) | No API keys, works offline |
| Font | System fonts + optional preloaded Google Font | Zero network after install |

### 5C. Offline-First
- First load: app renders instantly, PWA registers, SW caches assets
- Subsequent: opens from home screen, IndexedDB provides data — instant
- Speech recognition uses offline browser language model
- Entire app works with zero connectivity

### 5D. Speech-to-Text
```javascript
function startListening(targetField) {
  const recognition = new SpeechRecognition();
  recognition.lang = 'en-US';
  recognition.continuous = true;
  recognition.interim = true;
  recognition.onresult = (event) => {
    let transcript = '';
    for (let i = event.resultIndex; i < event.results.length; i++) {
      transcript += event.results[i][0].transcript;
    }
    targetField.value += transcript;
  };
  recognition.start();
}
```
Falls back gracefully to text input when speech unavailable.

### 5E. Rule Engine Architecture
```javascript
const RuleEngine = {
  extractTopics(text) { /* matches against 20 topic keyword sets */ },
  detectPatterns(text) { /* counts: criticism, contempt, defensiveness, stonewalling */ },
  detectCrazyCycle(textA, textB) { /* checks love/respect need markers */ },
  matchWisdom(topics, patterns, cycle) {
    return WisdomDB.query({ topics, patterns, cycleType });
  },
  generatePrayer(topics, spouseAName, spouseBName) {
    return PrayerTemplate.render(topics, { spouseAName, spouseBName });
  },
  generateReconciliationPrompt(topics) { return PromptDB.bestMatch(topics); }
};
```

---

## 6. WISDOM DATABASE

### 6A. Schema
```javascript
{
  "id": "wisdom-001",
  "type": "scripture",          // "scripture" | "insight" | "practical_step"
  "topics": ["money", "conflict", "trust"],
  "patterns": ["criticism", "defensiveness"],
  "cycle_types": ["crazy-cycle"],
  "gender_perspective": null,   // null (both) | "husband" | "wife"
  "severity": "moderate",       // "mild" | "moderate" | "severe"
  "text": {
    "scripture": { "reference": "Proverbs 15:1", "text": "A gentle answer turns away wrath..." },
    "explanation": "When arguments escalate, tone determines resolution...",
    "application": "Take three slow breaths before responding."
  },
  "tags": ["gentleness", "conflict-deescalation"],
  "priority": 85
}
```

### 6B. Topic Map (20 Base Categories)
1. Money/Finances → Security, Trust
2. Chores/Housework → Respect, Partnership
3. Children/Parenting → Shared Values, Unity
4. In-Laws/Family → Boundaries, Loyalty
5. Intimacy/Sex → Connection, Desire
6. Communication → Being Heard
7. Trust/Honesty → Safety
8. Time/Priority → Value, Priority
9. Respect → Honor, Esteem
10. Faith/Church → Spiritual Unity
11. Jealousy/Insecurity → Reassurance
12. Addiction/Habits → Healing, Recovery
13. Anger/Temper → Self-Control
14. Decision Making → Partnership
15. Past Hurts → Healing, Forgiveness
16. Gratitude/Appreciation → Recognition
17. Future/Goals → Alignment
18. Health/Self-Care → Support
19. Extended Family/Blended → Unity
20. General/Unspecified → Core Healing

### 6C. Scripture Database (MVP: 40 verses)
Organized by topic + pattern. Each with reference, full text (consistent translation), 1-2 sentence application, practical action step.

### 6D. Counselor Insight Database (MVP: 30 entries)
Plain-language, pastor-quality observations. Examples:
- Criticism detected: "Criticism attacks the person, not the problem. Try 'I feel...' instead of 'You always...'"
- Contempt detected: "Contempt is the single best predictor of divorce."
- Crazy Cycle: "She needs love, he needs respect. Neither is wrong — you're speaking past each other."
- Money conflict: "Money arguments are never about money. They're about security, control, or trust."

### 6E. Prayer Generator
Templates per topic with slots for spouse names and issue details. Example for conflict topic:
> "Lord Jesus, You who are the Prince of Peace, help [A] and [B] to set down their weapons and pick up understanding. When anger rises, remind them of Your gentleness. When pride blocks forgiveness, remind them Your love is stronger than any argument..."

---

## 7. DATA MODEL

### 7A. IndexedDB Schema
- **Database:** oneflesh_db, version 1
- **Store: sessions** — keyPath: id, indexes: by_date, by_topic
- **Store: settings** — key: 'app-settings' (single-row)
- **Store: wisdom_cache** — keyPath: id

### 7B. Session Document
```javascript
{
  "id": "session-20261009-193042-a1b2c3",
  "createdAt": "2026-10-09T19:30:42Z",
  "title": "Argument about dishes",
  "titleNeutral": "Conflict about household responsibilities",
  "spouseA": { "name": "", "statement": "...", "wordCount": 147, "spokenFirst": true },
  "spouseB": { "name": "", "statement": "...", "wordCount": 112, "spokenFirst": false },
  "analysis": {
    "topics": [{ "topic": "chores", "confidence": 0.91 }],
    "patterns": { "a": { "criticism": 2, "contempt": 0, "defensiveness": 1, "stonewalling": 0 },
                  "b": { "criticism": 1, "contempt": 0, "defensiveness": 3, "stonewalling": 0 } },
    "crazyCycle": { "detected": false, "aFeelsUnloved": false, "bFeelsDisrespected": false },
    "severity": "moderate", "conflictType": "perpetual"
  },
  "wisdom": {
    "scriptures": [{ "reference": "Proverbs 15:1", "text": "...", "explanation": "..." }],
    "insights": ["This isn't about dishes. It's about feeling seen."],
    "practicalSteps": ["Before bed, each say one specific thing you appreciate."],
    "prayer": "Lord Jesus, help [A] and [B] to see each other's labor...",
    "prayerPrayedAt": null,
    "reconciliationPrompt": "Would you be willing to forgive each other and start over?"
  },
  "reconciled": false,
  "loveLanguages": { "a": { "primary": null }, "b": { "primary": null } }
}
```

### 7C. Privacy & Security
| Concern | Decision |
|---------|----------|
| No cloud | Zero data leaves the device. No account, no sync, no analytics. |
| No crash reports | No network calls at all unless user explicitly exports data. |
| No audio storage | Speech recognition is browser-local. Audio never stored or transmitted. |
| Export only | "Export All Sessions" generates a JSON file for user to save manually. |
| Clear data | "Delete All Data" wipes IndexedDB. |
| No ads/trackers | None. Zero third-party embeds. |

---

## 8. MVP VS FUTURE ENHANCEMENTS

### 8A. MVP (Build This First — ~16 days)
- Single index.html PWA (2d)
- IndexedDB session storage (1d)
- PWA manifest + service worker (0.5d)
- Welcome/home screen (0.5d)
- Issue input screen (0.5d)
- Two-sided listening flow (1d)
- Rule-based analysis engine (3d) — **the core**
- Wisdom database — 40 verses, 30 insights, 20 prayers (2d)
- Wisdom display screen (1d)
- Reconciliation prompt (0.5d)
- Session history list + detail (1d)
- Prayer screen (0.5d)
- Reflecting animation (0.5d)
- Settings: names, theme, font size (0.5d)
- Browser speech-to-text (1d)
- Love Languages quick quiz (1d)
- Data export JSON (0.5d)

### 8B. Future (Phase 2+)
- Multi-language support (Spanish, French, Portuguese)
- Audio playback of prayer (browser TTS)
- Shared journal (local notes per session)
- Full love languages quiz (25 questions, scored)
- Conflict trend dashboard ("You've argued about money 4 times")
- Daily devotional (verse + prayer based on recent topics)
- Couples reading plan (Bible + reflection questions)
- Themed tracks (e.g., "40 Days of Marriage Renewal")
- Couples daily check-in (1-tap mood)
- PDF export (beautifully formatted session summaries)
- Dark mode (CSS custom properties toggle)
- Encrypted local storage (browser crypto API)
- P2P sync between two phones (WebRTC, no cloud)

### 8C. Deliberate Non-Features (What We WILL NOT Build)

| Feature | Reason |
|---------|--------|
| AI chatbot / LLM | Hallucinates verses, inconsistent advice, requires internet, adds cost. Rule engine is predictable, private, and free. |
| Cloud sync | Violates core privacy promise. P2P sync may come later. |
| Social/community | Marriage counseling is intimate. No friend lists, sharing, or leaderboards. |
| Therapist directory | Separate product requiring medical licensing compliance. |
| Payment/subscription | Ministry tool, not SaaS. Free forever. |
| Email/notifications | App is offline-first. Notifications require servers. |

---

## 9. FILE STRUCTURE (MVP)

```
one-flesh/
├── index.html              # Single-page PWA — all HTML, CSS, JS
├── manifest.json           # PWA manifest
├── service-worker.js       # Offline cache handler
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── icon.svg
└── README.md
```

Everything lives in `index.html`. manifest.json and service-worker.js are separate because PWA registration requires them at root, but all app logic — HTML structure, CSS styles, JS engine, wisdom database — is one file.

---

## 10. IMPLEMENTATION ORDER (Build Sequence)

| Phase | Tasks | Days |
|-------|-------|------|
| **Phase 1: Shell** | index.html skeleton, CSS theme, PWA manifest, service worker, basic screen scaffolding | 2 |
| **Phase 2: Storage** | IndexedDB setup, session CRUD, settings store | 1 |
| **Phase 3: Input** | Issue input screen, spouse speaking screens, speech-to-text, session flow | 2 |
| **Phase 4: Engine** | Topic extraction, pattern detection, Crazy Cycle detection, wisdom matching | 4 |
| **Phase 5: Content** | Write 40 Scripture entries, 30 insights, 20 prayer templates, reconciliation prompts | 3 |
| **Phase 6: Output** | Wisdom display screen, prayer screen, reflecting animation, reconciliation prompt | 2 |
| **Phase 7: Polish** | Session history, settings, love languages quiz, data export, accessibility audit | 2 |

**Total: ~16 days for MVP**

---

*Document prepared for implementation. Ready for the single-file PWA build phase.*