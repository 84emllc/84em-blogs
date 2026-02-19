---
title: "Using FFmpeg to Let Claude Code See a Client's Bug"
date: 2026-02-18
description: "How to convert a client's screen recording into sequential image frames so Claude Code can visually analyze the bug being demonstrated."
tags:
  - claude-code
  - workflow
  - ai
  - debugging
---

A client sent me a screen recording of a bug. I needed Claude Code to help diagnose it, but Claude Code can't watch videos. It can read files and look at images, but a `.mp4` is a black box.

So I converted the video into a series of still frames and let Claude Code step through them visually.

## The Command

[FFmpeg ↗](https://www.ffmpeg.org/) handles the conversion. It's free, open-source, and available on every platform.

```bash
mkdir -p frames
ffmpeg -i client-bug-recording.mp4 -vf fps=1 -q:v 2 frames/frame_%04d.jpg
```

Breaking that down:

- `-i client-bug-recording.mp4`: the input video
- `-vf fps=1`: extract one frame per second
- `-q:v 2`: JPEG quality (scale of 1-31, lower is better, 2 is near-lossless)
- `frames/frame_%04d.jpg`: output with zero-padded numbering (`frame_0001.jpg`, `frame_0002.jpg`, etc.)

A 45-second recording at one frame per second gives you 45 sequential, well-labeled images.

## Feeding Frames to Claude Code

With the frames extracted, I pointed Claude Code at the directory:

> Look at the frames in the `frames/` directory. These are sequential screenshots from a screen recording of a bug. Walk through them in order and describe what's happening, then identify where the bug occurs.

Claude Code examined the images in sequence, described the UI state changes frame by frame, identified where the unexpected behavior started, and pointed to the component likely responsible based on what it could see.

What would have taken me 15 minutes of pause-play-rewatch took about 30 seconds. Its description was more precise than mine would have been.

## Tuning the Frame Rate

One frame per second works for most UI bug recordings. Adjust based on the situation:

- **Slow, page-level bugs** (wrong layout, missing content): `fps=0.5` is plenty
- **Fast interactions** (dropdown flickers, animation glitches): `fps=5` or higher
- **Specific time range**: add `-ss 00:00:12 -to 00:00:18` to extract only the relevant section

For a quick animation glitch in a 6-second window:

```bash
ffmpeg -i client-bug-recording.mp4 -ss 00:00:12 -to 00:00:18 -vf fps=5 -q:v 2 frames/frame_%04d.jpg
```

That gives you 30 frames. Enough to catch timing issues without flooding Claude with hundreds of images.

## Scaling Down Large Recordings

If the client recorded at full resolution, you can scale the frames down to save tokens without losing meaningful detail:

```bash
ffmpeg -i video.mp4 -vf "fps=1,scale=1280:-1" -q:v 2 frames/frame_%04d.jpg
```

The `-1` preserves the aspect ratio.

## Quick Reference

```bash
# Install FFmpeg
brew install ffmpeg          # macOS
sudo apt install ffmpeg      # Ubuntu/Debian
choco install ffmpeg         # Windows (Chocolatey)

# Basic: 1 frame/second
mkdir -p frames
ffmpeg -i video.mp4 -vf fps=1 -q:v 2 frames/frame_%04d.jpg

# Fast UI bugs: 5 frames/second
ffmpeg -i video.mp4 -vf fps=5 -q:v 2 frames/frame_%04d.jpg

# Specific time range
ffmpeg -i video.mp4 -ss 00:00:10 -to 00:00:20 -vf fps=2 -q:v 2 frames/frame_%04d.jpg

# Scale down large recordings
ffmpeg -i video.mp4 -vf "fps=1,scale=1280:-1" -q:v 2 frames/frame_%04d.jpg
```

## Tools Used

- **[FFmpeg ↗](https://www.ffmpeg.org/)** (free, open-source media processing)
- **Claude Code** (Anthropic's CLI tool for agentic coding)
