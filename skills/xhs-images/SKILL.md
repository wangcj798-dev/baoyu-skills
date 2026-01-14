---
name: xhs-images
description: Xiaohongshu (Little Red Book) infographic series generator with multiple style options. Breaks down content into 1-10 cartoon-style infographics. Use when user asks to create "小红书图片", "XHS images", or "RedNote infographics".
---

# Xiaohongshu Infographic Series Generator

Break down complex content into eye-catching infographic series for Xiaohongshu with multiple style options.

## Usage

```bash
# Auto-select style based on content
/xhs-images posts/ai-future/article.md

# Specify a style
/xhs-images posts/ai-future/article.md --style cute
/xhs-images posts/ai-future/article.md --style tech
/xhs-images posts/ai-future/article.md --style minimal

# Direct content input
/xhs-images
[paste content]

# Direct input with style
/xhs-images --style bold
[paste content]
```

## Options

| Option | Description |
|--------|-------------|
| `--style <name>` | Specify infographic style (see Style Gallery below) |

## Style Gallery

### 1. `cute` (Default)
Sweet, adorable, girly - classic Xiaohongshu aesthetic
- **Colors**: Pink, peach, mint, lavender, cream background
- **Elements**: Cute stickers, emoji icons, hearts, stars, sparkles
- **Best for**: Lifestyle, beauty, fashion, daily tips

### 2. `fresh`
Clean, refreshing, natural
- **Colors**: Mint green, sky blue, white, light yellow
- **Elements**: Plant icons, clouds, simple shapes, breathing room
- **Best for**: Health, wellness, minimalist lifestyle, self-care

### 3. `tech`
Modern, smart, digital
- **Colors**: Deep blue, purple, cyan, dark backgrounds with neon accents
- **Elements**: Geometric shapes, data icons, circuit patterns, glowing effects
- **Best for**: Tech tutorials, AI content, digital tools, productivity

### 4. `warm`
Cozy, friendly, approachable
- **Colors**: Warm orange, golden yellow, brown, cream
- **Elements**: Sun motifs, coffee cups, cozy illustrations, warm lighting
- **Best for**: Personal stories, life lessons, emotional content

### 5. `bold`
High impact, attention-grabbing
- **Colors**: Red, orange, black, yellow accents
- **Elements**: Strong typography, exclamation marks, arrows, contrast
- **Best for**: Important tips, warnings, must-know content

### 6. `minimal`
Ultra-clean, sophisticated
- **Colors**: Black, white, single accent color
- **Elements**: Maximum whitespace, simple icons, clean lines
- **Best for**: Professional content, serious topics, elegant presentations

### 7. `retro`
Vintage, nostalgic, trendy
- **Colors**: Muted pastels, sepia, faded tones
- **Elements**: Vintage badges, halftone dots, classic typography
- **Best for**: Throwback content, classic tips, timeless advice

### 8. `pop`
Vibrant, energetic, eye-catching
- **Colors**: Bright primary colors, neon accents, white
- **Elements**: Bold shapes, comic-style elements, dynamic compositions
- **Best for**: Exciting announcements, fun facts, engaging tutorials

### 9. `notion`
Minimalist hand-drawn line art, intellectual
- **Colors**: Black outlines, white background, 1-2 pastel accents
- **Elements**: Simple line doodles, geometric shapes, hand-drawn wobble, maximum whitespace
- **Best for**: Knowledge sharing, concept explanations, SaaS content, productivity tips

## Auto Style Selection

When no `--style` is specified, analyze content to select:

| Content Signals | Selected Style |
|----------------|----------------|
| Beauty, fashion, cute, girl, pink | `cute` |
| Health, nature, clean, fresh, organic | `fresh` |
| Tech, AI, code, digital, app, tool | `tech` |
| Life, story, emotion, feeling, warm | `warm` |
| Warning, important, must, critical | `bold` |
| Professional, business, elegant, simple | `minimal` |
| Classic, vintage, old, traditional | `retro` |
| Fun, exciting, wow, amazing | `pop` |
| Knowledge, concept, productivity, SaaS, notion | `notion` |

## File Management

### With Article Path

Save to `xhs-images/` subdirectory in the same folder as the article:

```
posts/ai-future/
├── article.md
└── xhs-images/
    ├── outline.md
    ├── prompts/
    │   ├── 01-cover.md
    │   ├── 02-content-1.md
    │   └── ...
    ├── 01-cover.png
    ├── 02-content-1.png
    └── 03-ending.png
```

### Without Article Path

Save to `xhs-outputs/YYYY-MM-DD/[topic-slug]/`:

```
xhs-outputs/
└── 2026-01-13/
    └── ai-agent-guide/
        ├── outline.md
        ├── prompts/
        │   ├── 01-cover.md
        │   └── ...
        ├── 01-cover.png
        └── 02-ending.png
```

## Workflow

### Step 1: Analyze Content & Select Style

1. Read content
2. If `--style` specified, use that style
3. Otherwise, scan for style signals and auto-select
4. Determine image count based on content complexity:

| Content Type | Image Count |
|-------------|-------------|
| Simple opinion / single topic | 2-3 |
| Medium complexity / tutorial | 4-6 |
| Deep dive / multi-dimensional | 7-10 |

### Step 2: Generate Outline

Plan for each image with style-specific approach:

```markdown
# Xiaohongshu Infographic Series Outline

**Topic**: [topic description]
**Style**: [selected style]
**Image Count**: N
**Generated**: YYYY-MM-DD HH:mm

---

## Image 1 of N

**Position**: Cover
**Core Message**: [one-liner]
**Filename**: 01-cover.png

**Text Content**:
- Title: xxx
- Subtitle: xxx

**Visual Concept**: [style-appropriate description]

---

## Image 2 of N
...
```

### Step 3: Save Outline

Save outline as `outline.md`.

### Step 4: Generate Images One by One

For each image, create a style-specific prompt file.

**Prompt Format**:

```markdown
Infographic theme: [topic]
Style: [style name]
Position: [cover/content/ending]

Visual composition:
- Main visual: [style-appropriate description]
- Layout: [element positioning for 3:4 vertical format]
- Decorative elements: [style-specific decorations]

Color scheme:
- Primary: [style primary color]
- Background: [style background color]
- Accent: [style accent color]

Text content:
- Title: 「xxx」(large, prominent)
- Key points: 「xxx」「xxx」

Style notes: [specific style characteristics]
```

Then generate using:

```bash
/gemini-web --promptfiles [SKILL_ROOT]/skills/xhs-images/prompts/system.md [TARGET_DIR]/prompts/01-cover.md --image [TARGET_DIR]/01-cover.png
```

After each image:
1. Confirm generation success
2. Report progress: "Generated X/N"
3. Continue to next

### Step 5: Completion Report

```
Xiaohongshu Infographic Series Complete!

Topic: [topic]
Style: [style name]
Location: [directory path]
Images: N total

- 01-cover.png ✓ Cover
- 02-content-1.png ✓ Content
- 03-content-2.png ✓ Content
- 04-ending.png ✓ Ending

Outline: outline.md
```

## Style Reference Details

### cute
```
Colors: Pink (#FED7E2), peach (#FEEBC8), mint (#C6F6D5), lavender (#E9D8FD)
Background: Cream (#FFFAF0), soft pink (#FFF5F7)
Accents: Hot pink, coral
Elements: Hearts, stars, sparkles, cute faces, ribbon decorations, sticker-style
Typography: Rounded, bubbly hand lettering
```

### fresh
```
Colors: Mint green (#9AE6B4), sky blue (#90CDF4), light yellow (#FAF089)
Background: Pure white (#FFFFFF), soft mint (#F0FFF4)
Accents: Leaf green, water blue
Elements: Plant leaves, clouds, water drops, simple geometric shapes
Typography: Clean, light hand lettering with breathing room
```

### tech
```
Colors: Deep blue (#1A365D), purple (#6B46C1), cyan (#00D4FF)
Background: Dark gray (#1A202C), near-black (#0D1117)
Accents: Neon green (#00FF88), electric blue
Elements: Circuit patterns, data icons, geometric grids, glowing effects
Typography: Monospace-style hand lettering, subtle glow
```

### warm
```
Colors: Warm orange (#ED8936), golden yellow (#F6AD55), terracotta (#C05621)
Background: Cream (#FFFAF0), soft peach (#FED7AA)
Accents: Deep brown (#744210), soft red
Elements: Sun rays, coffee cups, cozy items, warm lighting effects
Typography: Friendly, rounded hand lettering
```

### bold
```
Colors: Vibrant red (#E53E3E), orange (#DD6B20), yellow (#F6E05E)
Background: Deep black (#000000), dark charcoal
Accents: White, neon yellow
Elements: Exclamation marks, arrows, warning icons, strong shapes
Typography: Bold, impactful hand lettering with shadows
```

### minimal
```
Colors: Black (#000000), white (#FFFFFF)
Background: Off-white (#FAFAFA), pure white
Accents: Single color (content-derived - blue, green, or coral)
Elements: Single focal point, thin lines, maximum whitespace
Typography: Clean, simple hand lettering
```

### retro
```
Colors: Muted orange, dusty pink (#FED7E2 at 70%), faded teal
Background: Aged paper (#F5E6D3), sepia tones
Accents: Faded red, vintage gold
Elements: Halftone dots, vintage badges, classic icons, tape effects
Typography: Vintage-style hand lettering, classic feel
```

### pop
```
Colors: Bright red (#F56565), yellow (#ECC94B), blue (#4299E1), green (#48BB78)
Background: White (#FFFFFF), light gray
Accents: Neon pink, electric purple
Elements: Bold shapes, speech bubbles, comic-style effects, starburst
Typography: Dynamic, energetic hand lettering with outlines
```

### notion
```
Colors: Black (#1A1A1A), dark gray (#4A4A4A)
Background: Pure white (#FFFFFF), off-white (#FAFAFA)
Accents: Pastel blue (#A8D4F0), pastel yellow (#F9E79F), pastel pink (#FADBD8)
Elements: Simple line doodles, hand-drawn wobble effect, geometric shapes, stick figures, maximum whitespace
Typography: Clean hand-drawn lettering, simple sans-serif labels
```

## Content Breakdown Principles

1. **Cover (Image 1)**: Strong visual impact, core title, attention hook
2. **Content (Middle)**: One core point per image, moderate information density
3. **Ending (Last)**: Summary / call-to-action / memorable quote

## Notes

- Image generation typically takes 10-30 seconds per image
- Auto-retry once on generation failure
- Use cartoon alternatives for sensitive public figures
- Output language matches input content language
- Maintain selected style consistency across all images in series
