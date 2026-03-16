# 📡 Content Distribution Engine

A multi-platform content publishing pipeline that transforms a single source document into 30+ platform-specific formats with editorial guidelines, voice rules, and paste-ready output.

![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js)
![Markdown](https://img.shields.io/badge/Markdown-Templates-000000?style=flat-square&logo=markdown)
![Platforms](https://img.shields.io/badge/Platforms-30+-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

---

## The Problem

A single piece of long-form content needs to be adapted and published across 30+ platforms — each with different formatting rules, character limits, voice expectations, and media requirements. Doing this manually is slow and error-prone.

## The Solution

An engine that takes raw source content and runs it through platform-specific adapters, producing paste-ready output for each channel with formatting applied, editorial voice adjusted, and media specs met.

---

## Supported Platforms

### v1 — Full Source (Published As-Is)
WordPress, Medium, Buttondown, LinkedIn Article, Notion Archive, Physical Letter (Lob.com)

### v2 — Adapted Per Medium
| Platform | Format | Specs |
|----------|--------|-------|
| Email Newsletter | Markdown → HTML | 400–900 words, letter voice, CTA footer |
| LinkedIn Article | Rich text | 600–1,000 words, subheads every 200 words |
| Twitter/X Thread | Plain text | 8–15 tweets, standalone hooks |
| Threads / Bluesky | Plain text | 3–8 posts, casual tone |
| Facebook | Rich text | 300–500 words, emotional arc |
| Reddit | Markdown | Anti-promotional framing, question-led |
| WhatsApp Business | Plain text | 160–300 words, hook + CTA |
| Carousel / Slides | Copy blocks | 8–12 slides, 1 idea per slide |
| Short Video Script | Timestamped | 60-sec max, hook-in-2-seconds |
| YouTube (Long) | Chapters | 5–15 min, chapter markers, SEO metadata |
| Podcast (NotebookLM) | Full text input | AI dialogue generation |
| Quote Graphics | Isolated quotes | 3–5 standalone pull quotes |
| Pinterest Idea Pins | Visual + copy | Vertical format, keyword-rich |
| Audiograms | Audio + waveform | 30–60 sec clips with captions |
| Donor Email | Personalized | Via Gmail, formal tone |
| Physical Letter | Print-ready | Via Lob.com API |

### v3 — Micro Content (Drip)
Individual quote graphics, story snippets, single-stat graphics, teaser posts.

---

## Architecture

```
source-content/
├── raw/                    # Original long-form content
│   └── log-001.md
├── adapters/               # Platform-specific transformers
│   ├── medium.js
│   ├── twitter-thread.js
│   ├── linkedin-article.js
│   ├── buttondown.js
│   ├── reddit.js
│   ├── carousel.js
│   ├── video-script.js
│   ├── whatsapp.js
│   └── ... (30+ adapters)
├── templates/              # Output templates per platform
├── guidelines/             # Editorial rules per channel
│   ├── voice-rules.md      # First-person "I" vs institutional "We"
│   └── formatting-specs.md
├── output/                 # Generated paste-ready content
└── engine.js               # Main pipeline runner
```

### Editorial Rules

The engine enforces key editorial principles:

- **Source integrity** — Content stays as a single piece (never auto-split into series)
- **Voice preservation** — Edits for pacing only, never rewriting the author's voice
- **Dual voice support** — LinkedIn uses two distinct voices: personal first-person ("I") for the founder's profile and institutional ("We") for the organization page
- **Paste-ready output** — Every adapter produces content ready to copy-paste, not advisory notes

---

## Usage

```bash
# Process a single content piece across all platforms
node engine.js --input raw/log-001.md --output output/log-001/

# Process for specific platforms only
node engine.js --input raw/log-001.md --platforms twitter,linkedin,medium

# Generate with custom voice rules
node engine.js --input raw/log-001.md --voice institutional
```

### Output Example

```
output/log-001/
├── medium.md                 # Full article with pull quotes, image suggestions
├── buttondown.md             # Markdown preview driving to Medium
├── wordpress.html            # Brand-matched HTML/CSS
├── linkedin-personal.md      # First-person voice
├── linkedin-org.md           # Institutional voice
├── twitter-thread.txt        # 12 standalone tweets
├── threads.txt               # 5 casual posts
├── reddit-education.md       # r/education framing
├── reddit-nonprofit.md       # r/nonprofit framing
├── carousel-slides.md        # 10 slides, 1 idea each
├── video-script-60s.md       # Timestamped 60-sec script
├── youtube-chapters.md       # Long video with markers
├── whatsapp-broadcast.txt    # 200-word hook
├── quote-graphics.json       # 5 isolated quotes with metadata
└── donor-email.html          # Personalized template
```

---

## What I Learned

- Designing adapter patterns that scale to 30+ output formats
- Maintaining editorial voice consistency across drastically different platforms
- Building content pipelines that produce paste-ready output, not advisory notes
- Structuring anti-promotional content for community platforms (Reddit)

---

## License

MIT — see [LICENSE](LICENSE) for details.
