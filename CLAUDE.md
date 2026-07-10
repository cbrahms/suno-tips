# Suno Tips + Nano Banana 2 Skill

This repository integrates the **nano-banana-2-skill** - an AI image generation CLI powered by Google's Gemini models.

## Nano Banana 2 Skill Overview

Generate high-quality AI images using Gemini 3.1 Flash (default) or Gemini 3 Pro. Supports multi-resolution outputs (512px to 4K), aspect ratio control, reference image editing, transparent background generation, and cost tracking.

**Repository:** https://github.com/kingbootoshi/nano-banana-2-skill

## Getting Started

### 1. Install Prerequisites

```bash
# Install Bun (if not already installed)
curl -fsSL https://bun.sh/install | bash
source ~/.bashrc  # or ~/.zshrc
```

For transparent image generation, also install FFmpeg and ImageMagick:
```bash
brew install ffmpeg imagemagick  # macOS
# or on Linux:
sudo apt-get install ffmpeg imagemagick
```

### 2. Initialize Nano Banana

```bash
cd nano-banana-2-skill
bun install
bun link
```

### 3. Set Up Gemini API Key

Get your free API key from: https://aistudio.google.com/apikey

Then set it in one of these ways:

**Option A: Home directory config (recommended)**
```bash
mkdir -p ~/.nano-banana
echo "GEMINI_API_KEY=your_key_here" > ~/.nano-banana/.env
```

**Option B: Local .env file**
```bash
echo "GEMINI_API_KEY=your_key_here" > .env
```

**Option C: Environment variable**
```bash
export GEMINI_API_KEY=your_key_here
```

## Usage

After setup, use `nano-banana` from anywhere:

```bash
# Basic image generation
nano-banana "a serene landscape at sunset"

# Specify size and aspect ratio
nano-banana "cyberpunk city" -s 2K -a 16:9

# Use Pro model for higher quality
nano-banana "detailed portrait" --model pro

# Generate with transparent background
nano-banana "mascot character" -t -o mascot

# Reference image for style transfer
nano-banana "apply this style to a new scene" -r reference.png

# Show cost summary
nano-banana --costs
```

## Common Options

| Option | Values | Example |
|--------|--------|---------|
| `-s, --size` | 512, 1K (default), 2K, 4K | `-s 2K` |
| `-a, --aspect` | 1:1, 16:9, 9:16, 4:3, 3:4, etc. | `-a 16:9` |
| `-m, --model` | flash/nb2 (default), pro/nb-pro | `--model pro` |
| `-o, --output` | filename (no extension) | `-o my-image` |
| `-r, --ref` | image file (use multiple times) | `-r style.png` |
| `-t, --transparent` | flag for green screen removal | `-t` |

## Use Cases for Suno Tips

- **Music video assets** - Generate visual elements to accompany Suno AI songs
- **Album artwork** - Create cover art and promotional images
- **Metadata visuals** - Generate mood boards and inspiration images
- **Tutorials** - Create step-by-step visual guides
- **Marketing materials** - Promotional graphics for music projects

## Pricing

All prices are approximate and based on Gemini's current pricing:

| Size | Flash Model | Pro Model |
|------|------------|-----------|
| 512px | ~$0.045 | Flash only |
| 1K | ~$0.067 | ~$0.134 |
| 2K | ~$0.101 | ~$0.201 |
| 4K | ~$0.151 | ~$0.302 |

## Cost Tracking

All generations are logged to `~/.nano-banana/costs.json`. View your cost summary:

```bash
nano-banana --costs
```

## Troubleshooting

**Command not found after `bun link`:**
```bash
mkdir -p ~/.local/bin
ln -sf ~/tools/nano-banana-2/src/cli.ts ~/.local/bin/nano-banana
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**API Key not found:**
Check that your API key is set in one of these locations (checked in order):
1. `--api-key` flag
2. `GEMINI_API_KEY` environment variable
3. `.env` file in current directory
4. `.env` file in nano-banana-2-skill root
5. `~/.nano-banana/.env`

**Transparent generation issues:**
- Ensure FFmpeg is installed: `which ffmpeg`
- Ensure ImageMagick is installed: `which convert`
- Ensure the `-t` flag is used in the command

## More Information

For detailed documentation and advanced features, see:
- Main CLI README: `nano-banana-2-skill/README.md`
- Skill definition: `nano-banana-2-skill/plugins/nano-banana/skills/nano-banana/SKILL.md`
- Marketplace info: `nano-banana-2-skill/.claude-plugin/marketplace.json`

## API Key Disclaimer

Your Gemini API key is sensitive. Keep it secure and never commit `.env` files to version control. The `.env` file is already in `.gitignore`.
