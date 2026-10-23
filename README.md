# Video Frame Grabber

Save clean, full-resolution still images from a video, right in the browser. No upload, no server, no install.

**Live demo:** [downloaders.co/video-frame-grabber](https://www.downloaders.co/video-frame-grabber)

Pausing a video and taking a screenshot gives you player controls, a scaled-down picture and whatever your screen resolution happens to be. This tool reads the video file directly and draws the exact frame you choose at the video's own resolution, so a 1080p video gives you a 1920 × 1080 image.

## Features

- **Capture the current frame** with one click
- **Capture a frame every N seconds** to build a storyboard or find the best thumbnail
- **PNG, JPG or WebP** output. PNG keeps every detail, JPG and WebP make smaller files
- **Original resolution**, no scaling
- **MP4, MOV and WebM** input (whatever your browser can play)
- **Drag and drop** or file picker
- **100% client-side**: the video never leaves your device

## How it works

There is no backend. The whole tool is a few hundred lines of plain JavaScript built on standard browser APIs:

1. The selected file is turned into an object URL with `URL.createObjectURL()` and loaded into a `<video>` element.
2. To capture a frame, the video is paused at the chosen time and drawn onto a `<canvas>` sized to `video.videoWidth × video.videoHeight`.
3. `canvas.toBlob()` encodes the frame as PNG, JPEG or WebP, and the blob is offered as a download.
4. For interval capture, the tool seeks to each timestamp, waits for the `seeked` event, then repeats step 2 and 3.

Because nothing is uploaded, processing speed depends only on your device, and large files work as long as your browser can play them.

## Browser support

Works in current versions of Chrome, Edge, Firefox and Safari, on desktop and mobile. Supported input formats depend on the browser: MP4 (H.264) works everywhere, WebM is not supported by older Safari versions, and MOV files play where the codec inside them is supported.

## Run locally

```bash
git clone https://github.com/YOUR-USERNAME/video-frame-grabber.git
cd video-frame-grabber
# any static server works, for example:
npx serve .
```

Then open the address it prints. Opening `index.html` directly from disk also works in most browsers.

## Project structure

```
index.html        UI
frame-grabber.js  capture logic
style.css         styles
```

## Part of Pullo

This tool is one of the free browser utilities on [Pullo](https://www.downloaders.co), alongside a [video to MP3 converter](https://www.downloaders.co/video-to-mp3-converter), an [audio cutter](https://www.downloaders.co/audio-cutter) and an [image converter](https://www.downloaders.co/image-converter). All of them process files locally.

## Contributing

Issues and pull requests are welcome. If a video file doesn't load or a frame comes out wrong, please open an issue with your browser, operating system and the file's format.

## License

MIT
