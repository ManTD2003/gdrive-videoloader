# GDrive VideoLoader

**GDrive VideoLoader** is a Python-based tool to download videos from Google Drive effortlessly, **including those marked as _view-only_** (no download option). It supports resumable downloads, progress bars, parallel downloading, and various customization options for video fetching and downloading.

## Features

- Download videos even if marked as *view-only* (without a download button)
- Supports resumable downloads (continue from where it stopped)
- Supports parallel downloading of a single file (multithreading)
- Displays a progress bar for ongoing downloads
- Allows custom chunk sizes for downloading
- Optionally specify a custom output file name
- Verbose mode for detailed logs during execution

## Installation

### Prerequisites

- Python 3.7+
- Pip (Python package manager)

### Dependencies

Install the required Python packages using the following command:

```bash
pip install -r requirements.txt
```

## Usage

### Basic Command

To download a video, you can provide either the Google Drive file ID or a full Google Drive URL:

**Using a file ID:**
```bash
python gdrive_videoloader.py <video_id>
```

**Using a full Google Drive URL:**
```bash
python gdrive_videoloader.py https://drive.google.com/file/d/<video_id>/view
```

The script will automatically extract the file ID from the URL if you provide a full link.

### Options

| Parameter                | Description                                                       | Default Value         |
|--------------------------|-------------------------------------------------------------------|-----------------------|
| `<video_id>`             | The video ID from Google Drive or a full Google Drive URL (required). The script automatically extracts the ID from URLs like `https://drive.google.com/file/d/ID/view`. | N/A                   |
| `-o`, `--output`         | Custom output file name for the downloaded video.                | Video name in GDrive  |
| `-c`, `--chunk_size`     | Chunk size (in bytes) for downloading the video.                 | 1024 bytes            |
| `-t`, `--threads`        | Number of threads for parallel downloading, improves speed       | 4                     |
| `-v`, `--verbose`        | Enable verbose mode for detailed logs.                           | Disabled              |
| `--version`              | Display the script version.                                      | N/A                   |
| `-h`, `--help`           | Display the help message.                                        | N/A                   |
### Downloading Private / Restricted Videos (Using Cookies)

If the video requires you to be logged into your Google account to view it, you need to extract your session cookies and pass them to the script using the `--cookies` parameter.

**How to extract cookies:**

**Method 1: Using Netscape format (Recommended)**
1. Install the **Get cookies.txt LOCALLY** extension (available for Chrome/Edge).
2. Log into [Google Drive](https://drive.google.com) and ensure you can access the target video.
3. Click the extension icon and click **Export**.
4. Rename the downloaded file to `cookies.txt` and place it in the same directory as the script.

**Method 2: Using JSON format**
1. Install the **Cookie-Editor** extension (available for Chrome/Firefox/Edge).
2. Log into Google Drive.
3. Click the extension icon, click **Export**, and select **Export as JSON**.
4. Create a new text file named `cookies.json`, paste the copied clipboard content into it, and save.

**Usage with cookies:**
```bash
python gdrive_videoloader.py <video_id> --cookies cookies.txt
```