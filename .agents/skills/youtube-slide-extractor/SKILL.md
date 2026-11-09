---
name: youtube-slide-extractor
description: Extracts presentation slides from YouTube videos or playlists, with optional webcam/bottom-bar masking, deduplicating slides, and generating a combined PDF with OCR.
---
# YouTube Slide Extractor Skill

Use this skill when the user wants to extract presentation slides from a YouTube video or playlist.

## Instructions
1. Execute the extraction CLI directly using `youtube-slide-extractor "<youtube_url>" --best` (or add `--lang <code>` to specify a transcript language; by default it extracts the transcript in the video's original default language).
2. The tool will automatically create a timestamped folder inside `outputs/` (or the directory passed via `--output-dir` / `-d`) and save the individual slide PDFs, `Combined_Slides.pdf`, and the `<video>_transcript.txt` file(s) there. Use `--transcript-only` to extract only the transcript or `--no-transcript` to skip it.
3. Notify the user when the extraction is complete and point them to the `outputs/` directory.

## Defaults
By default the extractor runs with **no masking** and **enhancement enabled**.
- Masking is opt-in. Use `--mask-webcam` to enable ensemble webcam masking, `--mask-bottom-bar` to enable temporal bottom-bar masking, `--best` to apply the best verified configuration (ensemble webcam + temporal bottom + enhancement), or `--quality` (alias for `--best`) to enable both plus enhancement.
- Enhancement is on by default; use `--no-enhance` to disable it.
- Use `--speed` for a fast preset: frequency webcam + fixed bottom bar + no enhancement.

## Features
- **Dynamic Masking**: Optionally detects circular/rectangular webcams and bottom control bars (like YouTube UI or presentation UI) when enabled.
- **Consensus Background Color**: Calculates the global background color of the presentation and seamlessly patches the masked areas so they disappear completely.
- **Robust Deduplication**: Tracks pixel motion to identify unique slide transitions and discards exact duplicates.
- **High Quality & OCR**: Downloads the highest available 1080p source and applies Tesseract OCR so the resulting PDFs have selectable text.
