# Assets Directory

This folder is designated for storing all external visual and audio resources used by the MUSHclient plugins.

## Supported Content Types

- **Audio Assets**: Sound files, music tracks, or soundscapes (typically in `.wav` or `.mp3` format) used for alerts, notification triggers, or background atmosphere.
- **Visual Assets**: Custom miniwindow UI textures, icons, map tiles, and custom status indicators (such as `.png`, `.bmp`, or `.gif`).

## Best Practices

1. **Optimization**: Optimize image and audio sizes to minimize client-side load times and memory footprint.
2. **Relative Paths**: Always resolve asset paths dynamically or relatively within plugins to ensure compatibility across different user installations.
3. **Clean Naming**: Use lowercase alphanumeric names and underscores for asset filenames to avoid operating system compatibility issues.
