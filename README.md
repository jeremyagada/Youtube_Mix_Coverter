# YouTube Mix → Playlist Converter

Convert YouTube's auto-generated mixes into real, saveable playlists.

## What it does

YouTube creates personalized "Mix" playlists based on what you're listening to — but you can't save them. This tool extracts every song from a YouTube Mix and creates a proper playlist in your YouTube account.

![YouTube Mix](https://img.shields.io/badge/YouTube-Mix-red?style=flat&logo=youtube)
![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat&logo=jupyter)

---

## Features

- Extracts songs from any YouTube Mix URL (`&list=RD...`)
- Creates a new YouTube playlist via the Data API v3
- Searches and adds the best matching videos to your playlist
- Saves a JSON backup of extracted songs
- Runs entirely in a Jupyter Notebook with step-by-step cells

---

## Demo

| Step | Action | Result |
|------|--------|--------|
| 1 | Paste a YouTube Mix URL | Extracts song list |
| 2 | Authenticate with Google | One-time OAuth flow |
| 3 | Run the converter | Playlist created on YouTube |

---

## Tech Stack

- **Python 3.8+**
- **yt-dlp** — extracts mix metadata without downloading videos
- **Google OAuth 2.0** + **YouTube Data API v3** — creates playlists
- **Jupyter Notebook** — interactive, step-by-step execution

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/youtube-mix-converter.git
cd youtube-mix-converter
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

Or run the first cell in the Jupyter notebook:
```python
!pip install yt-dlp google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

### 3. Set up Google Cloud credentials

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or use an existing one)
3. Enable **YouTube Data API v3**
4. Go to **APIs & Services → Credentials**
5. Click **Configure consent screen**
   - Choose **External**
   - Fill in app name and email
6. Go back to **Credentials → Create Credentials → OAuth client ID**
   - Application type: **Desktop app**
   - Name: `YouTube Playlist Converter`
7. Download the JSON file and rename it to **`client_secret.json`**
8. Place `client_secret.json` in the same folder as the notebook

### 4. Add yourself as a test user

1. In Google Cloud Console, go to **APIs & Services → OAuth consent screen**
2. Scroll to **Test users**
3. Click **+ ADD USERS**
4. Add your Google email address
5. Wait 1-2 minutes for changes to propagate

---

## Usage

1. Open `youtube_mix_converter.ipynb` in Jupyter Lab, VS Code, or Google Colab
2. Run cells sequentially (Shift + Enter)
3. In **Cell 6**, paste your YouTube Mix URL:
   ```python
   MIX_URL = "https://www.youtube.com/watch?v=VIDEO_ID&list=RDVIDEO_ID"
   ```
4. Run **Cell 7** to create the playlist and add songs
5. Check your YouTube account — the playlist is live!

---

## How to find a YouTube Mix URL

1. Play any song on YouTube
2. Look in the right sidebar for **"Mix"**
3. Click the Mix to start playing it
4. Copy the URL from your browser's address bar
   - Must contain `&list=RD...` (e.g., `&list=RDsuRE1UX4Z8k`)

> ⚠️ **Not** a regular playlist (`&list=PL...`) or a single video (`youtu.be/...`)

---

## Project Structure

```
youtube-mix-converter/
├── youtube_mix_converter.ipynb   # Main Jupyter notebook
├── client_secret.json            # Your Google OAuth credentials (not tracked)
├── extracted_songs.json          # Backup of extracted songs
├── requirements.txt              # Python dependencies
└── README.md                     # This file
```

---

## Troubleshooting

| Error | Fix |
|-------|-----|
| `Access blocked: app not verified` | Add your email as a test user in OAuth consent screen |
| `No playlist entries found` | Make sure URL contains `&list=RD...` |
| `FileNotFoundError: client_secret.json` | Download OAuth credentials and place in project folder |
| `songs list is empty` | Check that the Mix URL is valid and publicly accessible |
| Rate limit / quota exceeded | Wait 24h or check quotas at Google Cloud Console |

---

## Roadmap

- [ ] Spotify integration (create matching Spotify playlist)
- [ ] Support for regular YouTube playlists (`&list=PL...`)
- [ ] Auto-convert "Liked Videos" into a playlist
- [ ] CLI version for terminal users
- [ ] Batch processing multiple mixes

---

## License

feel free to use, modify, and share.

---

## Acknowledgments

Built with [yt-dlp](https://github.com/yt-dlp/yt-dlp) and the [YouTube Data API](https://developers.google.com/youtube/v3).
