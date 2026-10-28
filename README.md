# GDM Downloader

A small interactive Python downloader built with `yt-dlp`. It can download video at a selected available resolution or extract music as M4A. Download progress is shown in the terminal with a Rich bar, percentage when the total is known, downloaded size, speed, and ETA.

## What you need

- Python 3.10 or newer
- The packages listed in `requirements.txt`
- FFmpeg available on your `PATH` for video/audio merging, metadata, and thumbnail embedding
- An internet connection and a supported media URL

The script asks for a URL, then whether you want video or music. For video it lists detected resolutions. Files are saved to the current working directory.

## Windows

1. Install Python from [python.org](https://www.python.org/downloads/windows/) and enable the option to add Python to `PATH`.
2. Install FFmpeg and make sure `ffmpeg` and `ffprobe` are available in PowerShell. Open a new PowerShell window after changing `PATH`.
3. Open PowerShell in the folder containing `gdm.py` and `requirements.txt`, then run:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe gdm.py
```

Downloads go into that folder. If you prefer to activate the environment first, run `.\.venv\Scripts\Activate.ps1`, then `python -m pip install -r requirements.txt` and `python gdm.py`.

## macOS

Install Python 3 from [python.org](https://www.python.org/downloads/macos/) or your preferred package manager. Install FFmpeg with Homebrew if available:

```sh
brew install ffmpeg
```

In Terminal, change to the folder containing the two project files and run:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python gdm.py
```

## Linux

On Debian or Ubuntu, install Python, its virtual environment support, and FFmpeg:

```sh
sudo apt update
sudo apt install python3 python3-venv ffmpeg
```

Then, from the project folder, run:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python gdm.py
```

For other distributions, install Python 3, `venv` support, and FFmpeg using that distribution's package manager.

## Android

Use [Termux](https://github.com/termux/termux-app), installed from its official F-Droid or GitHub release source. Avoid mixing Termux installs from different sources because Android treats them as different app signatures.

Open Termux and install the runtime tools:

```sh
pkg update
pkg install python ffmpeg
termux-setup-storage
```

Allow storage access when Android asks. Copy `gdm.py` and `requirements.txt` into a folder under `Download`, then in Termux run:

```sh
cd ~/storage/downloads/GSD-py
python -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python gdm.py
```

Change `GSD-py` in the `cd` command to the folder name you copied. Downloads are saved in that folder. Android may pause background terminals to save battery; keep Termux open during a download. Android/Termux use has not been separately tested for this project.

## iPhone (iOS)

This project is a command-line Python program and is not a native iPhone app. Standard iOS Python environments are sandboxed; in Pythonista, for example, launching subprocesses is restricted. This downloader relies on external FFmpeg for merging and post-processing, so running the full workflow locally on iPhone is not a supported setup.

The practical option is to run the project on a Mac, Linux, or Windows computer and connect to that computer from an iPhone using an SSH terminal app. Start `gdm.py` in the remote shell; progress appears in that terminal, and downloaded files remain on the computer. Use a computer you control and a secure SSH connection.

## Progress bar notes

- Separate audio and video streams may appear as separate progress rows.
- When yt-dlp cannot determine a total size, the bar stays indeterminate and does not show a fabricated percentage.
- After transfer finishes, yt-dlp may continue merging streams or embedding metadata and artwork. The progress row then shows that the transfer finished while post-processing continues.
- Some sites, formats, or protected media may not be supported by yt-dlp.

## Troubleshooting

- **`ModuleNotFoundError`**: Activate the virtual environment or run the Python executable inside `.venv`, then install dependencies with `python -m pip install -r requirements.txt`.
- **FFmpeg not found / post-processing failed**: Install FFmpeg for your OS, ensure both `ffmpeg` and `ffprobe` are on `PATH`, and reopen the terminal.
- **No resolutions found or download fails**: Check that the URL is accessible and supported by yt-dlp. Some sites require authentication or block automated downloads.
