# 🔐 GitHub Actions Setup Guide

## Required Repository Secrets

To enable AI-powered daily news digests, you need to add these secrets to your GitHub repository:

### 🚀 **How to Add Secrets**

1. Go to your repository on GitHub
2. Click **Settings** → **Secrets and variables** → **Actions**  
3. Click **New repository secret**
4. Add each secret below:

### 🤖 **AI Provider Secret (Required)**

#### **Anthropic Claude (Currently Used)**
- **Secret Name**: `ANTHROPIC_API_KEY`  
- **Secret Value**: Your Anthropic API key
- **Get it from**: https://console.anthropic.com/
- **Cost**: ~$0.50-$2.00 per digest (varies by language count)
- **Note**: Currently generating 3 services (English, Polish, BellaNews) for cost optimization

### 🔧 **GitHub Token (Automatic)**
- **Secret Name**: `GITHUB_TOKEN`
- **Status**: ✅ **Already available** (GitHub provides this automatically)
- **Purpose**: Allows the action to commit files and create releases

## 📅 **Automatic Schedule**

Once secrets are configured, the workflow will:
- ✅ **Run daily at 5:00 AM UTC** (6:00 AM UK time)
- ✅ **Generate AI-enhanced news digests** for English, Polish, and BellaNews
- ✅ **Commit MP3 and text files to repository** (stored in Git LFS)
- ✅ **Deploy to GitHub Pages** automatically
- ✅ **Upload artifacts for 90-day retention**

## 🎯 **Manual Triggering**

You can also run the digest manually:
1. Go to **Actions** tab in your repository
2. Click **🤖 AI-Powered Daily News Digest**
3. Click **Run workflow**
4. Optionally enable debug mode
5. Click **Run workflow**

## 📊 **What Gets Generated**

### **Files Created (per language):**
- `docs/{language}/audio/news_digest_ai_YYYY_MM_DD.mp3` - Audio file
- `docs/{language}/news_digest_ai_YYYY_MM_DD.txt` - Full transcript

### **Active Languages:**
- `en_GB`: English (UK) news digest
- `pl_PL`: Polish news digest (excluding Radio Maria)
- `bella`: Personalized business/finance news for investment banking & VC interests

### **GitHub Features:**
- **Releases**: Each digest gets its own release with download links
- **Artifacts**: 90-day backup of all generated files  
- **Issues**: Automatic issue creation if generation fails
- **Commits**: Detailed commit messages with file stats

## 🚨 **Error Handling**

If the workflow fails:
- ✅ **Automatic issue created** with failure details
- ✅ **Email notification** (if GitHub notifications enabled)
- ✅ **Fallback to non-AI mode** if API fails
- ✅ **Detailed logs** available in Actions tab

## 💰 **Cost Estimation**

**Anthropic Claude API Usage:**
- Daily digest per language: ~5,000-15,000 tokens (analysis + synthesis)
- Cost per digest: ~$0.15-0.70 per language
- Current setup (3 languages): ~$0.50-$2.00 per day
- Monthly cost: ~$15-60
- **Cost optimized**: Other languages disabled to minimize API costs

## 🎧 **Usage for Visually Impaired Users**

### **Daily Routine:**
1. **5:00 AM UTC (6:00 AM UK)**: Digests automatically generated
2. **5:05 AM UTC**: Available on GitHub Pages
3. **Visit**: https://audionews.uk (or your custom domain)
4. **Select language**: English, Polish, or BellaNews
5. **Play audio** directly in browser or download MP3
6. **Natural neural voices** - professional and clear

### **Access Methods:**
- **Live Website**: https://audionews.uk (GitHub Pages)
- **Direct download**: Audio files available in language-specific folders
- **PWA Support**: Can be installed as a Progressive Web App
- **Offline Access**: Service worker caches content for offline use

## 🔧 **Troubleshooting**

### **No AI Analysis:**
- Check API key is correctly set in repository secrets
- Verify key has sufficient credits/usage limits
- System will fallback to keyword-based analysis

### **No Audio Generated:**
- Check if `edge-tts` is working (should work on GitHub runners)
- Verify text content was created successfully
- Check workflow logs for specific error messages

### **Files Not Committed:**
- Ensure `GITHUB_TOKEN` has write permissions (should be automatic)
- Check if repository has branch protection rules
- Verify workflow has `contents: write` permission

## ✅ **Testing Setup**

After adding secrets, test the setup:

1. **Manual trigger**: Run workflow manually to test
2. **Check outputs**: Verify MP3 and TXT files are created
3. **Test download**: Download from GitHub release
4. **Verify quality**: Listen to audio for quality and content
5. **WhatsApp test**: Send MP3 to phone and test playback

**Perfect for providing daily, professional news access to visually impaired users! 🎧♿**
