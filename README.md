# Bulk Blog Generator

AI-powered bulk blog generator. Upload an Excel sheet with keywords and topics — get individual `.docx` blog files downloaded as a ZIP. Powered by Claude (Anthropic).

---

## Files in this repo

```
bulk-blog-generator/
├── index.html          ← The app (rename bulk-blog-generator.html to this)
├── server.js           ← Proxy server — deploy to Render to keep API key secure
├── package.json        ← Node dependencies for the proxy
├── .env.example        ← Copy to .env and add your API key
├── .gitignore          ← Keeps .env out of GitHub
├── netlify.toml        ← Fixes Netlify content security policy
└── README.md
```

---

## Deploy in 3 steps

### Step 1 — Backend proxy on Render (free)
Keeps your Anthropic API key secure — never exposed in the browser.

1. Go to [render.com](https://render.com) → New Web Service → connect this repo
2. Set:
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
   - **Instance Type:** Free
3. Add environment variables:
   - `ANTHROPIC_API_KEY` = your key from [console.anthropic.com](https://console.anthropic.com)
   - `ALLOWED_ORIGIN` = your Netlify URL (set after Step 2)
4. Deploy → note your Render URL e.g. `https://bulk-blog-proxy.onrender.com`

### Step 2 — Frontend on Netlify (free)

1. Go to [netlify.com](https://netlify.com) → Add new site → Import from Git
2. Connect this repo
3. Netlify auto-deploys → your app is live at `https://your-site.netlify.app`

### Step 3 — Connect them

1. Open your Netlify URL
2. Click **API Settings** → select **Backend Proxy**
3. Paste: `https://bulk-blog-proxy.onrender.com/api/generate`
4. Click **Save & Connect** — green dot = connected

---

## How to use

1. Click **Download Template** inside the app to get the Excel input file
2. Fill in one row per blog (Primary Keyword + Topic are required)
3. Set **Product Context** once — brand name, USPs, voice, things to avoid
4. Upload the filled Excel file
5. Click **Generate All Blog Posts** — live progress tracker per blog
6. Click **Download All .docx Files as ZIP**

### Excel columns

| Column | Required | Notes |
|--------|----------|-------|
| Primary Keyword | ✅ | Use 3-5 word long-tail phrases |
| Blog Topic / Angle | ✅ | Opinionated headline, not just a subject |
| Target Audience | Optional | Specific role + situation |
| Product Page URL | Optional | Linked naturally inside the article |
| Secondary Keywords | Optional | Comma-separated, 4-6 recommended |
| Word Count | Optional | 800 / 1200 / 1800 / 2500 (default: 1200) |
| Tone | Optional | conversational / professional / authoritative / educational |

---

## Local development

```bash
git clone https://github.com/YOUR-USERNAME/bulk-blog-generator.git
cd bulk-blog-generator
npm install
cp .env.example .env
# Add ANTHROPIC_API_KEY to .env
node server.js
# Open index.html in browser
# API Settings → Backend Proxy → http://localhost:3000/api/generate
```

---

## Tech stack

- **Frontend:** Vanilla HTML/CSS/JS — no build step
- **Backend:** Node.js + Express proxy
- **AI:** Anthropic Claude Sonnet (`claude-sonnet-4-20250514`)
- **Libraries:** SheetJS, docx.js, JSZip, FileSaver.js
- **Hosting:** Netlify + Render (both free tier)
