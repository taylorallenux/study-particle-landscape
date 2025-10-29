# particle-study-landscape-mask

Part of my ongoing particle studies exploring point cloud representations of natural forms.

**Study focus:** Heightmap masking, tiling, and atmospheric depth  
**Particle count:** ~450,000 per tile (configurable via density controls)  
**Technique:** GPU-driven point sprites sampling dynamic heightmaps with real-time masking

## Overview

An interactive WebGL visualization that transforms heightmap images into beautiful particle landscapes. Each pixel of the heightmap becomes a point sprite, creating a volumetric terrain representation with real-time masking, atmospheric fog, and dynamic tiling for infinite scrolling landscapes.

## Features

- **Heightmap Import**: Drag-and-drop or load heightmap images (PNG, JPEG, WebP)
- **Dynamic Tiling**: Configurable tile grid for seamless infinite scrolling
- **Circular Masking**: Real-time circular mask with adjustable radius and feathering
- **Mouse Hover Effects**: Interactive particle highlighting that follows mouse movement
- **Atmospheric Depth**: Configurable fog effects for depth perception
- **Particle Customization**: Adjust point size, density, jitter, and colors
- **Camera Controls**: Full camera manipulation (yaw, pitch, FOV, position)
- **Animated Scrolling**: Auto-scroll terrain based on camera direction
- **URL Parameters**: Configure scene via query string parameters

## Usage

### Running Locally

Simply open `index.html` in a modern web browser with WebGL support. The project uses ES modules and CDN imports, so no build step is required.

### Interactive Controls

The Tweakpane UI provides real-time control over:

- **Heightmap**: Load new heightmaps, adjust terrain scale, tile size, and grid dimensions
- **Particles**: Point size, jitter amount, hover effects, and density (columns/rows)
- **Mask**: Circular mask radius and feather controls
- **Animation**: Scroll speed and auto-animation toggle
- **Camera**: Yaw, pitch, FOV, height, position, and fog settings

### Drag & Drop

Drop a heightmap image directly onto the canvas to replace the current terrain. The heightmap will be automatically sampled and applied to all tiles.

### URL Parameters

Configure the scene via URL query parameters:

- `scale` - Heightmap scale (default: 1.4)
- `tileSize` - Size of each tile (default: 11)
- `tilesX` / `tilesZ` - Grid dimensions (default: 1x3)
- `psize` - Point size multiplier (default: 0.01)
- `mask` - Mask radius (default: 3.0)
- `feather` - Mask feather amount (default: 0.8)
- `jitter` - Particle position jitter (default: 0.02)
- `hR` / `hS` / `hSnap` - Hover effect controls
- `yaw` / `pitch` - Camera rotation in degrees
- `fov` - Camera field of view (default: 90)
- `height` / `z` - Camera position
- `scroll` - Scroll speed (default: 0.6)
- `animate` - Enable auto-scroll (0 or 1)
- `cols` / `rows` - Particle grid resolution
- `fog` - Enable fog (0 or 1)
- `terrain` - Terrain color (hex)
- `fogColor` - Fog color (hex)
- `ui` - Hide UI (set to 0)

Example: `index.html?scale=2.0&mask=5.0&animate=1&ui=0`

## Technical Details

### Rendering Pipeline

- **Geometry**: PlaneGeometry subdivided into configurable grid (default 256x256 segments)
- **Point Cloud**: Converted to non-indexed geometry for `THREE.Points` rendering
- **Shader-Based Sampling**: Vertex shader samples heightmap texture to displace Y position
- **Masking**: Fragment shader applies circular mask with smooth falloff
- **Tiling**: Multiple point cloud instances positioned dynamically for seamless scrolling

### Performance

- GPU-accelerated particle rendering
- Efficient frustum culling disabled for seamless tiling
- Configurable particle density for performance tuning
- Power-of-two texture handling for optimal GPU sampling

### Browser Compatibility

Requires a modern browser with:
- WebGL 2.0 support
- ES6 modules support
- File API (for drag-and-drop)

## Assets

- Default heightmap: `assets/heightmap_512x512.png`

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Credits

Project by [@Taylor](https://www.threads.com/@taylor)

Built with:
- [Three.js](https://threejs.org/) - 3D graphics library
- [Tweakpane](https://cocopon.github.io/tweakpane/) - UI controls

