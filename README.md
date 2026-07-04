# 🎃 Pumpkin Upload It v7.5.8

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)
![Built%20For-bitporn.eu-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

> ☕ **Support the project:** [Buy Me a Coffee](https://buymeacoffee.com/pumpkinpounder)
>
> I will genuinely buy coffee. Like, a lot of coffee. Probably an unhealthy amount of coffee.

---

> ⚠ **Originally built for bitporn.eu**
>
> Pumpkin Upload It was built for the **BitPorn** upload workflow.
>
> It creates torrent files, prepares BitPorn BBCode descriptions, adds cover/banner/description images, generates a release-info image, and uploads directly through the BitPorn API.

---

# 📌 Overview

Pumpkin Upload It is a Windows Python GUI app for preparing and uploading torrent packs.

It is designed for uploaders who already have a folder prepared with videos and a `scr` folder containing preview images or animated WEBP previews.

The app can:

- Create private `.torrent` files from folders or selected files
- Load existing `.torrent` files
- Auto-fill the torrent name from the torrent or folder
- Upload directly to the BitPorn API
- Force anonymous uploads
- Opt in to the moderation queue
- Auto-build a clean BBCode description
- Auto-load cover, banner, and screenshots from a `scr` folder
- Work alongside **Pumpkin Thumb It** by using its generated screenshots and WEBP previews
- Generate a transparent release-info PNG
- Scan media resolution, codec, runtime, size, and video count
- Scrape Pornolab pages for keywords and time-period information

---

# ✨ Main Features

## 🚀 Direct BitPorn Upload

The app uploads directly to:

```text
https://bitporn.eu/api/torrents/upload
```

It sends:

- Torrent file
- Torrent name
- BBCode description
- Category
- Resolution
- Keywords
- Cover image
- Banner image
- Description images
- Mod queue option
- Anonymous upload flag

Anonymous upload is forced on by default.

---

## 🧲 Built-in Torrent Creator

Pumpkin Upload It can create a `.torrent` file from:

- A full folder
- Selected files

The torrent creator:

- Sets the private flag
- Uses the configured announce URL
- Picks sensible piece sizes based on total data size
- Ignores junk files such as `Thumbs.db`, `.DS_Store`, and desktop metadata
- Ignores development folders such as `.git`, `.svn`, and `.hg`
- Counts video files for the upload description
- Shows progress while hashing pieces

---

## 📁 SCR Folder Auto-Loading

When a folder contains a `scr` folder, Pumpkin Upload It can automatically load upload images.

Expected example:

```text
Performer Name/
├── video1.mp4
├── video2.mkv
└── scr/
    ├── centerlongest_Performer Name.webp
    ├── center1.webp
    ├── center2.webp
    ├── center3.webp
    ├── center4.webp
    └── center5.webp
```

The app uses:

- `centerlongest_*.webp` as the cover/banner preview
- `center1.webp` to `center5.webp` as screenshots
- The parent folder name as the upload name


## 🎬 Works with Pumpkin Thumb It

Pumpkin Upload It is designed to work alongside **Pumpkin Thumb It**.

Pumpkin Thumb It can generate the screenshot images and WEBP previews, then Pumpkin Upload It can pick them up from the `scr` folder and place them into the BitPorn upload layout.

Typical workflow:

```text
Pumpkin Thumb It
        ↓
Creates screenshots / WEBP previews
        ↓
Saved into the scr folder
        ↓
Pumpkin Upload It loads them into the upload description
```

This keeps the thumbnail/screenshot creation separate from the torrent upload process, while still making both tools work together cleanly.

---

## 🖼 Automatic Release Info Image

Pumpkin Upload It generates a transparent PNG release-info image before upload.

The image includes:

- Category
- Genre / keywords
- Time period covered
- Resolution
- Video codec
- Audio codec
- Total runtime
- Total size
- Total video count

The generated image is inserted into the BBCode description as a description image.

---

## 🧡 Pumpkin BBCode Layout

The app builds a BitPorn-ready BBCode layout with:

- Header image
- Torrent title
- Cover image
- Release-info image
- Centred screenshots spoiler
- Layout notice footer

The layout is built to avoid broken BBCode nesting and stray closing tags.

---


## 🔎 Pornolab Search and Scraping

Pumpkin Upload It can search and scrape Pornolab pages.

It can pull:

- Genre / tags / keywords
- Time period covered
- Search result titles
- Topic URLs

It supports Pornolab cookie files placed beside the script.

Supported cookie filenames:

```text
pornolab.net_cookies.txt
pornolab_cookies.txt
pornolab_cookie.txt
cookies.txt
```

Supported cookie formats include:

- Raw browser cookie header
- Netscape `cookies.txt`
- JSON cookie exports

---

## 🌍 Russian Tag Cleaner

The script includes a Russian-to-English tag cleaner for scraped Pornolab data.

This helps keep BitPorn upload keywords readable by translating common Pornolab labels and dropping unwanted navigation words.

---

## 🎞 Media Scanning

Pumpkin Upload It can scan video files for:

- Resolution group
- Exact resolution
- Video codec
- Audio codec
- Runtime
- Total size
- Total video count
- Resolution breakdown

This uses `ffprobe`, so FFmpeg needs to be installed and available in your system PATH.

---

# 🧰 Requirements

## Required

- Windows
- Python 3.10+
- Tkinter
- Internet access for API upload and scraping

Tkinter is normally included with the official Windows Python installer.

## Python packages

Install the required packages with:

```bash
pip install requests bencodepy urllib3 pillow
```

## Optional but recommended

Install FFmpeg and make sure `ffprobe` is available in PATH.

FFmpeg is needed for resolution scanning and media information.

Check it works with:

```bash
ffprobe -version
```

---

# ▶️ How to Run

Clone or download the repo, then run the Python file:

```bash
python "Pumpkin_Upload_It.py"
```

---

# ⚙️ Configuration

Open the Python file and edit the configuration section near the top.

Important values:

```python
BITPORN_UPLOAD_URL = "https://bitporn.eu/api/torrents/upload"
BITPORN_ANNOUNCE_URL = "https://bitporn.eu/announce"
TYPE_ID = 1
```

You will also need your own API token.

```python
BITPORN_API_TOKEN = "PUT_YOUR_TOKEN_HERE"
```

---

---

# 📦 Suggested Folder Workflow

A clean upload folder should look like this:

```text
Performer Name/
├── video1.mp4
├── video2.mp4
├── video3.mkv
└── scr/
    ├── centerlongest_Performer Name.webp
    ├── center1.webp
    ├── center2.webp
    ├── center3.webp
    ├── center4.webp
    └── center5.webp
```

Then in Pumpkin Upload It:

1. Click **Create Folder**
2. Select the performer folder
3. Save the `.torrent`
4. Let the app auto-load the `scr` images
5. Let it scan media information
6. Check the title, category, resolution, and keywords
7. Click **Upload with Pumpkin Upload It**

---

# 🧪 Upload Layout Order

Description image order is handled like this:

```text
upimg1 = cover image
upimg2 = generated release-info image
upimg3+ = screenshots / WEBP previews
```

The app strips `[img=width]` wrappers before API upload and sends the widths separately so BitPorn can render them correctly.

---

# 🏷 Categories and Resolutions

The app includes BitPorn category and resolution mappings inside the script.

Default category:

```text
collection
```

Default resolution:

```text
Other
```

Resolution options include:

```text
SD
720p
1080p
2K/2048p
4K/2160p
6K/3160p
8K/4320p
Other
```

---


---

# ⚠ Notes

This tool is made for a specific upload workflow.

Before using it on another tracker or UNIT3D site, check:

- API endpoint
- Required API fields
- Category IDs
- Resolution IDs
- Type IDs
- Announce URL
- Image upload handling
- BBCode support

---

# 📜 Licence

Add your preferred licence here.

For example:

```text
MIT Licence
```

---

# 👤 Author

Made by **PumpkinPounder**.

GitHub:

```text
https://github.com/PumpkinPounder
```
