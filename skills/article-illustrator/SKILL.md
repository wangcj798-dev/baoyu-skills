---
name: article-illustrator
description: Smart article illustration skill. Analyzes article content and generates illustrations at positions requiring visual aids. Illustrations can supplement information, visualize concepts, or guide reader imagination. Use when user asks to "add illustrations to article", "generate images for article", or "illustrate article".
---

# Smart Article Illustration Skill

Analyze article structure and content, identify positions requiring visual aids, and generate flexible-style illustrations.

## Usage

```bash
# Option 1: Specify article path
/article-illustrator vibe-coding-guide/final.md

# Option 2: Specify article URL (auto-download to local)
/article-illustrator https://example.com/article.md
```

## File Management

Save illustrations to `imgs/` subdirectory in the same folder as the article:

```
vibe-coding-guide/
├── final.md
└── imgs/
    ├── prompts/
    │   ├── illustration-evolution.md
    │   ├── illustration-comparison.md
    │   └── ...
    ├── illustration-evolution.png
    ├── illustration-comparison.png
    └── ...
```

## Workflow

### Step 1: Retrieve Article Content

1. **Local path**: Read file directly
2. **URL**: Download Markdown content to temporary location

### Step 2: Analyze Illustration Requirements

Analyze article paragraph by paragraph, identify positions requiring illustrations.

**Three Purposes of Illustrations**:
1. **Information Supplement**: Help understand abstract concepts (e.g., "iterative development" shown as skateboard → bicycle → car evolution)
2. **Concept Visualization**: Transform abstract ideas into concrete visuals for instant comprehension
3. **Imagination Guidance**: Create atmosphere, spark associations, enhance reading experience

**Content Suitable for Illustrations**:
- Abstract concepts needing visualization
- Processes/steps needing diagrams
- Comparisons needing visual representation
- Core arguments needing reinforcement
- Scenarios needing imagination guidance
- Emotions/atmosphere needing enhancement

**Content NOT Needing Illustrations**:
- Already intuitive descriptions (e.g., code examples, specific numbers)
- Simple list enumerations
- Direct quotes

**Illustration Count**:
- Consider at least 1 image per major section, prioritize core arguments and abstract concepts
- Opening/ending may add 1 image (for atmosphere)
- **Principle: More is better than fewer** - visual content significantly enhances reading experience

### Step 3: Generate Illustration Plan

Create plan for each illustration position:

```markdown
# Illustration Plan

**Article**: [article path]
**Illustration Count**: N images

---

## Illustration 1

**Insert Position**: [section name] / [paragraph description]
**Purpose**: [why illustration needed here]
**Visual Content**: [what the image should show]
**Filename**: illustration-[slug].png (slug convention: lowercase letters, numbers, hyphens)

---

## Illustration 2
...
```

### Step 4: Generate Prompts and Save

Create detailed prompt for each illustration, save to `prompts/` directory.

**Slug Naming Rules**:
- Use meaningful English description, following slug convention (lowercase letters, numbers, hyphens)
- Examples: `product-evolution`, `ai-vs-human-comparison`, `step-by-step-workflow`
- If file exists, generate a different slug; never overwrite

**Prompt File Format** (each prompts/illustration-[slug].md):

```markdown
[Specific content description including:]
- Main visual elements
- Element layout and positioning
- Text content (if any)
- Decorative elements

[System prompt style specifications auto-appended]
```

### Step 5: Generate Images Using `/gemini-web`

For each illustration, call:

```
/gemini-web --promptfiles [SKILL_ROOT]/skills/article-illustrator/prompts/system.md [ARTICLE_DIR]/imgs/prompts/illustration-[slug].md --image [ARTICLE_DIR]/imgs/illustration-[slug].png
```

- `[SKILL_ROOT]`: The baoyu-skills root directory
- `--promptfiles`: Concatenates system.md (style guidelines) + image-specific prompt
- `--image`: Output path for generated image

Generation flow:
1. Generate images sequentially
2. After each image, output progress: "Generated X/N"
3. On failure, auto-retry once
4. If retry fails, log reason, continue to next

### Step 6: Update Article

Insert generated images at corresponding positions:

```markdown
![illustration description](imgs/illustration-evolution.png)
```

**Insertion Rules**:
- Insert image after corresponding paragraph
- Leave one blank line before and after image
- Alt text uses concise description in article's language

**Infographic Handling**:
- Check if `imgs/` directory contains `infographic.png`
- If exists, insert infographic at appropriate position near article end (before summary or at very end)
- Format: `![Infographic](imgs/infographic.png)`

### Step 7: Output Summary

```
Article Illustration Complete!

Article: [article path]
Generated: X/N images successful

Illustration Positions:
- illustration-failure-trap.png → After section "Common Pitfalls"
- illustration-iteration.png → After section "Iterative Development"
...

[If any failures]
Failed:
- illustration-workflow.png: [failure reason]
```

## Visual Style Guidelines

See `prompts/system.md` for details. Style can be flexibly chosen based on content.

### Default Style (Cartoon Hand-drawn)

- **Minimalist**: Clean composition, ample whitespace
- **Hand-drawn illustration**: Cartoon style, warm and approachable
- **Retro-tech aesthetic**: Warm, soft color tones

### Optional Style Variants

Choose most appropriate style based on content:
- **Sci-fi futuristic**: Suitable for AI, cutting-edge technology topics
- **Sketch doodle**: Suitable for casual, contemplative content
- **Infographic**: Suitable for processes, comparisons, data content
- **Scene illustration**: Suitable for narrative, imaginative content

### Visual Elements

- **Aspect Ratio**: 16:9 landscape
- **Background**: Based on style, default cream/off-white
- **Elements**: Graphics matching content
- **Watermark**: "宝玉" in bottom-right corner

### Default Color Scheme

- Primary: Warm orange, coral
- Accent: Mint green, sky blue, light purple
- Background: Cream, off-white
- Outline: Dark gray line work

(Colors may adjust based on style variant)

## Terminology

| English | Chinese |
|---------|---------|
| Token | Token |
| AI Agent | AI 智能体 |
| Vibe Coding | 凭感觉编程 |
| AI Wrapper | AI 套壳 |

## Notes

- Illustrations serve the content: supplement information, visualize concepts, guide imagination
- Avoid duplicating information already intuitive in article
- Image generation typically takes 10-30 seconds per image
- Sensitive figures should use cartoon alternatives
- Maintain style consistency within same article
- Prompt and illustration text language should match article language
