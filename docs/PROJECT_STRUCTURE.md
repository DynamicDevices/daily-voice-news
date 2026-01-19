# AudioNews - Project Structure & Current State

## 🎯 Mission
Create natural, human-quality AI-powered audio news digests specifically designed for blind and partially sighted users. This project transforms news headlines from multiple sources into accessible, professional-sounding audio content that can be consumed via web or podcast platforms.

## 📋 Current Project Status

### ✅ Active Services (3)
- **English (UK)** (`en_GB`): General UK news digest covering politics, economy, health, international affairs, climate, technology, and crime
- **Polish** (`pl_PL`): Polish news digest (excluding Radio Maria)
- **BellaNews** (`bella`): Personalized business and finance news for undergraduate students interested in investment banking, VC finance, and business strategy

### 🎙️ Podcast Distribution
- RSS 2.0 feeds generated automatically for each service
- Available at:
  - `https://audionews.uk/en_GB/podcast.rss`
  - `https://audionews.uk/pl_PL/podcast.rss`
  - `https://audionews.uk/bella/podcast.rss`
- Compatible with Spotify, Apple Podcasts, Google Podcasts, and other platforms
- Includes full transcripts, SEO-optimized metadata, and podcast artwork

### 🔧 Technical Features

#### AI Processing
- **Model**: Anthropic Claude 4.5 Sonnet
- **Analysis**: Categorizes stories by theme, identifies key facts, cross-references sources
- **Synthesis**: Creates original summaries with context-aware generation to avoid repetition
- **Prompts**: Configurable via `config/ai_prompts.json`

#### Text-to-Speech
- **Engine**: Microsoft Edge TTS (neural voices)
- **Voices**: 
  - English (UK): `en-IE-EmilyNeural` (Irish female)
  - Polish: `pl-PL-ZofiaNeural` (Polish female)
  - BellaNews: `en-GB-LibbyNeural` (UK female)
- **Speed Adjustment**: +10% rate for optimal speech rate (~120 WPM)
- **Quality**: Professional neural voices, not robotic TTS

#### Audio Quality Optimizations
- ✅ **Quote removal**: Eliminates quote marks that cause TTS pauses
- ✅ **Newline removal**: Replaces internal newlines with spaces
- ✅ **Transition fixes**: Replaces periods with semicolons/commas before section transitions
- ✅ **Em/en dash replacement**: Replaces dashes with commas for smoother flow
- ✅ **Long sentence breaking**: Splits sentences over 40 words at natural points
- ✅ **Double space cleanup**: Normalizes spacing throughout
- ✅ **Ampersand replacement**: Replaces `&` with "and" for better pronunciation

#### Accessibility
- **WCAG 2.1 AA compliant**: Full accessibility standards
- **Screen reader optimized**: Semantic HTML, ARIA labels, skip links
- **SEO tags**: Includes keywords for "blind", "partially sighted", "blind and partially sighted"
- **Multi-language support**: Language-specific terms in meta tags

## 📁 Project Structure

```
audio-transcription/
├── scripts/                      # Core Python scripts
│   ├── github_ai_news_digest.py  # Main AI digest generator
│   ├── generate_podcast_rss.py    # Podcast RSS feed generator
│   ├── update_language_website.py # Language page updater
│   ├── update_website.py          # Website updater
│   ├── create_all_language_pages.py # Page generator
│   └── add_language.py           # Add new language support
│
├── config/                       # Configuration files
│   ├── ai_prompts.json           # AI model settings, prompts, system messages
│   ├── voice_config.json         # TTS voices, retry logic, rate settings
│   └── README.md                 # Configuration documentation
│
├── docs/                         # GitHub Pages website (public)
│   ├── en_GB/                    # English (UK) service
│   │   ├── index.html            # Language-specific page
│   │   ├── podcast.rss           # RSS feed for podcast platforms
│   │   ├── audio/                # MP3 audio files (Git LFS)
│   │   └── news_digest_ai_*.txt  # Transcript files
│   ├── pl_PL/                    # Polish service
│   │   └── [same structure]
│   ├── bella/                    # BellaNews service
│   │   └── [same structure]
│   ├── images/                   # Podcast artwork (1400x1400px)
│   │   ├── podcast-cover-en-gb.png
│   │   ├── podcast-cover-pl-pl.png
│   │   └── podcast-cover-bella.png
│   ├── shared/                   # Shared CSS/JS assets
│   ├── index.html                 # Main landing page
│   ├── PODCAST_SETUP.md          # Podcast publishing guide
│   ├── PROJECT_STRUCTURE.md      # This file
│   └── COPYRIGHT_AND_ETHICS.md   # Legal framework
│
├── templates/                     # HTML templates
│   ├── base/                     # Base template
│   ├── components/               # Reusable components
│   └── languages/                # Language-specific templates
│
├── resources/                     # Source assets
│   └── images/                   # Original logo and artwork
│
├── .github/workflows/             # CI/CD automation
│   └── daily-news-digest.yml     # Daily generation workflow
│
├── archive/                       # Old/unused files
├── LICENSE                        # GPL v3 (source code)
├── CONTENT_LICENSE.md             # CC BY-NC 4.0 (generated content)
├── README.md                      # Main project documentation
└── requirements.txt               # Python dependencies
```

## 🔄 Daily Workflow

### Automated Generation (GitHub Actions)
1. **Trigger**: Daily at 5:00 UTC (6:00 AM UK time)
2. **Process**:
   - Fetch news headlines from configured sources
   - AI analysis: Categorize stories by theme
   - AI synthesis: Generate original summaries
   - Text processing: Apply all audio quality fixes
   - TTS generation: Convert to MP3 with Edge TTS (+10% rate)
   - Website update: Update HTML pages with new content
   - RSS generation: Regenerate podcast feeds
   - Git commit: Commit and push to repository
   - GitHub Pages: Auto-deploy to audionews.uk

### Manual Generation
```bash
# Remove today's content first (if regenerating)
rm docs/{lang}/news_digest_ai_{today}.txt
rm docs/{lang}/audio/news_digest_ai_{today}.mp3

# Generate for specific language
python scripts/github_ai_news_digest.py --language en_GB
python scripts/github_ai_news_digest.py --language pl_PL
python scripts/github_ai_news_digest.py --language bella

# Update website
python scripts/update_language_website.py --language en_GB

# Generate RSS feeds
python scripts/generate_podcast_rss.py
```

## 🎯 Key Features & Capabilities

### Content Generation
- **Multi-source aggregation**: Combines headlines from multiple news sources
- **Theme-based organization**: Stories grouped by politics, economy, health, etc.
- **Context-aware synthesis**: AI avoids repetition across themes
- **Original content**: Synthesizes summaries, never copies articles verbatim
- **Copyright compliant**: Fair use for accessibility purposes

### Audio Quality
- **Natural speech flow**: No artificial pauses or robotic breaks
- **Professional pacing**: ~120 WPM speech rate
- **Smooth transitions**: Optimized section transitions
- **Clean text processing**: All TTS-disrupting characters removed/replaced
- **Sentence optimization**: Long sentences broken at natural points

### Distribution Channels
- **Web**: Accessible HTML pages at audionews.uk
- **Podcast**: RSS feeds for major platforms
- **Direct download**: MP3 files available for offline use
- **WhatsApp sharing**: Easy sharing for community distribution

### SEO & Discoverability
- **Accessibility keywords**: "blind", "partially sighted", "blind and partially sighted"
- **Language-specific terms**: Polish, French, German, Spanish, Italian, Dutch keywords
- **Open Graph tags**: Optimized for social media sharing
- **Structured data**: JSON-LD for search engines

## 📊 Technical Stack

- **AI**: Anthropic Claude 4.5 Sonnet
- **TTS**: Microsoft Edge TTS (neural voices)
- **CI/CD**: GitHub Actions
- **Hosting**: GitHub Pages
- **Storage**: Git LFS for audio files
- **Podcasts**: RSS 2.0 with iTunes extensions
- **PWA**: Service Worker + manifest.json

## 🔐 Repository Information

- **Repository**: `git@github.com:DynamicDevices/audionews.git`
- **Website**: https://audionews.uk
- **License**: GPL v3 (source code), CC BY-NC 4.0 (generated content)
- **Organization**: Dynamic Devices

## 📚 Documentation

- **Main README**: [`README.md`](../README.md) - Overview and quick start
- **Podcast Setup**: [`docs/PODCAST_SETUP.md`](PODCAST_SETUP.md) - Publishing guide
- **Configuration**: [`config/README.md`](../config/README.md) - Config documentation
- **GitHub Actions**: [`docs/GITHUB_ACTIONS_SETUP.md`](GITHUB_ACTIONS_SETUP.md) - CI/CD setup
- **Copyright**: [`docs/COPYRIGHT_AND_ETHICS.md`](COPYRIGHT_AND_ETHICS.md) - Legal framework

## 🚀 Future Enhancements

- Additional languages (currently disabled for cost optimization)
- Enhanced AI analysis with more sophisticated categorization
- User feedback integration
- Analytics and usage tracking
- Mobile app development

---

**Last Updated**: January 2026  
**Project Status**: Active and maintained  
**Daily Updates**: 6 AM UK time
