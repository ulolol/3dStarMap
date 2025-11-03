# 🌌 3D Cosmos Visualizer

An interactive, portable 3D star catalog visualizer that works on any device—PC, tablet, or mobile phone. No installation, no dependencies, just open and explore.

## Features

✨ **Interactive 3D Universe**
- Real-time rendering of star positions from the Bright Star Catalog (BSC-5P)
- Accurate 3D coordinates centered at Earth (0,0,0)
- Star distances expressed in parsecs (3.26 light-years per parsec)
- True-color star rendering with full spectral data
- **Realistic glowing stars** with radial gradient texture
- **Luminosity-based glow intensity** - brighter stars shine more brilliantly
- **Additive blending** for natural cosmic appearance

🎮 **Multi-Input Support**
- **Mouse**: Drag to rotate, scroll to zoom, click to select stars
  - Orbit mode: Rotate around scene center
  - Free mode: First-person FPS-style camera control
- **Keyboard**: Arrow keys/WASD for panning, +/- for zoom
- **Touch**: Drag to rotate, pinch to zoom, tap to select
- **Responsive**: Automatically adapts to desktop and mobile screens

🔧 **Customizable Visualization**
- Adjustable star scale (0.1x - 5x)
- Brightness/opacity control (0.1x - 3x)
- Two camera modes:
  - **Orbit Mode**: Rotate around the cosmos
  - **Free Mode**: First-person exploration
- Auto-rotating view (toggle on/off)
- Reset view button for quick navigation

📊 **Star Information Display**
- Real-time FPS and zoom level
- Click any star to see:
  - Catalog name (HD designation)
  - Apparent magnitude (brightness)
  - Distance in parsecs and light-years
  - 3D coordinates
  - Spectral color swatch

## Getting Started

### Quick Start

1. Download or clone this repository
2. Ensure you have `cosmos-visualizer.html` and `bsc5p_3d.json` in the same directory
3. Open `cosmos-visualizer.html` in any modern web browser
   - The visualizer will automatically load the star catalog
   - Or use the file picker in the interface to manually load a JSON file

### Supported Browsers

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Any WebGL-capable browser

### Requirements

- Modern web browser with WebGL support
- `bsc5p_3d.json` star catalog file
- Display with minimum 320x480 resolution (mobile)

## Usage Guide

### Desktop Controls

**Orbit Mode (Default)**
| Action | Control |
|--------|---------|
| Rotate around center | Click and drag with mouse |
| Zoom in/out | Mouse wheel or +/- keys |
| Select star | Click on a star |
| Reset view | Click "Reset View" button |

**Free Mode (First-Person)**
| Action | Control |
|--------|---------|
| Look around | Click and drag with mouse |
| Move forward | W key or Up arrow |
| Move backward | S key or Down arrow |
| Move left | A key or Left arrow |
| Move right | D key or Right arrow |
| Zoom in/out | Mouse wheel or +/- keys |
| Select star | Click on a star |
| Reset view | Click "Reset View" button |

**General Controls**
| Action | Control |
|--------|---------|
| Switch mode | Click "Orbit" or "Free" button |
| Toggle auto-rotate | Click "Pause Auto-Rotate" button |
| Adjust star size | Use "Star Scale" slider |
| Adjust brightness | Use "Brightness" slider |

### Mobile/Touch Controls

| Action | Control |
|--------|---------|
| Rotate view | Single finger drag |
| Zoom in/out | Two-finger pinch |
| Select star | Tap on a star |

### UI Panels

**Controls Panel** (top-left)
- File input for loading custom catalogs
- Star scale adjustment (affects star size)
- Brightness control
- View mode selector (Orbit/Free)
- Reset and pause buttons

**Info Panel** (bottom-left)
- Current catalog status
- Number of stars loaded
- FPS counter
- Current zoom level
- Selected star details (when clicked)

**Help Panel** (bottom-right)
- Quick reference for controls
- Platform-specific instructions
- Unit information

## Data Format

The visualizer expects a JSON file with an array of star objects:

```json
[
  {
    "i": 1,                    // Index
    "n": "HD3",               // Star name/designation
    "x": 112.44,              // X coordinate (parsecs)
    "y": -2.51,               // Y coordinate (parsecs)
    "z": 111.52,              // Z coordinate (parsecs)
    "p": 158.39,              // Parallax distance
    "N": 41.38,               // Apparent magnitude (brightness)
    "K": {                    // RGB color (normalized 0-1)
      "r": 0.349,
      "g": 0.493,
      "b": 1.0
    }
  }
]
```

### Coordinate System

- **Origin**: (0, 0, 0) represents Earth's position at the center of the ecliptic
- **Units**: Parsecs (1 pc = 3.26156 light-years = 3.086 × 10¹⁶ meters)
- **Axes**: Standard Cartesian coordinate system (X, Y, Z)
- **Range**: Typically ±500 parsecs for visible stars

### Star Properties

- **Magnitude (N)**: Apparent brightness scale (lower = brighter)
  - Scale: -2 to +6 visible range
  - Used to determine star size in visualization

- **Color (K)**: RGB values (0-1 normalized)
  - Determined by star's spectral class
  - Indicates surface temperature and composition

## Visualization Features

### Rendering

- **Point cloud rendering**: Efficiently displays thousands of stars
- **Glowing star texture**: Radial gradient texture creates realistic cosmic glow
- **Full spectral colors**: Blue, red, yellow, and white stars with accurate colors
- **Additive blending**: Natural light blending when stars overlap
- **Depth fogging**: Distant stars fade out for depth perception
- **Vertex coloring**: Each star rendered with accurate spectral color
- **Luminosity-based sizing**: Star glow intensity matches apparent brightness
  - Brighter stars (lower magnitude) = larger, more intense glows
  - Dimmer stars (higher magnitude) = smaller, subtler glows
- **Adaptive sizing**: Star size based on magnitude (brightness)
- **Antialiasing**: Smooth, anti-aliased rendering on all platforms

### Performance Optimization

- Limits to 10,000 stars by default (configurable)
- Hardware-accelerated WebGL rendering
- Efficient buffer geometry for millions of vertices
- Responsive resize handling
- Mobile-optimized touch input

### Camera Modes

**Orbit Mode** (default)
- Circular rotation around scene center
- Mouse/touch drag rotates around scene
- Maintains intuitive star exploration
- Auto-rotate available

**Free Mode**
- First-person perspective
- Keyboard navigation (WASD/Arrows)
- Full 6-degrees-of-freedom movement
- Useful for manual exploration

## Customization

### Modifying Star Scale

Edit line in `cosmos-visualizer.html`:
```javascript
const magnitude = Math.max(0, 6 - star.N) / 6;
sizes[i] = Math.max(0.5, magnitude * 3);  // Adjust the multiplier (3)
```

### Changing Background Color

Edit the `THREE.Color()` value:
```javascript
state.scene.background = new THREE.Color(0x000005);  // Change hex color
```

### Adjusting Fog Depth

Edit the fog parameters:
```javascript
state.scene.fog = new THREE.Fog(0x000005, 5000, 10000);  // (color, near, far)
```

## Troubleshooting

### Visualizer Won't Load
- Ensure `bsc5p_3d.json` is in the same directory as the HTML file
- Check browser console for errors (F12)
- Try a different browser

### Stars Not Visible
- Check zoom level (might be too far away)
- Click "Reset View" to return to default camera position
- Verify JSON file contains star data

### Performance Issues on Mobile
- Reduce star scale for smaller geometry
- Close other browser tabs
- Try landscape orientation
- Update your browser

### File Input Not Working
- Verify the JSON file is valid
- Try a smaller test catalog first
- Check browser permissions for file access

## Technical Details

### Dependencies

- **Three.js** (CDN-loaded, v128)
- No other external dependencies
- Pure JavaScript (no frameworks)

### Browser Compatibility

| Browser | Version | WebGL 2.0 | Status |
|---------|---------|-----------|--------|
| Chrome | 90+ | ✓ | Fully supported |
| Firefox | 88+ | ✓ | Fully supported |
| Safari | 14+ | ✓ | Fully supported |
| Edge | 90+ | ✓ | Fully supported |
| Mobile Chrome | 90+ | ✓ | Fully supported |
| Mobile Safari | 14+ | ✓ | Fully supported |

### File Size

- HTML file: ~32 KB (minified, no gzip)
- Data file: Variable (depends on star count)
- Total with 10,000 stars: ~500 KB

### Performance Metrics

- **10,000 stars**: 30-60 FPS on modern hardware
- **Mobile**: 20-60 FPS depending on device
- **Memory**: ~50 MB typical usage
- **GPU**: Most integrated GPUs supported

## License

This project uses publicly available star catalog data (Bright Star Catalog - BSC-5P).

## Credits

- **Star Data**: Yale Bright Star Catalog (BSC-5P)
- **3D Rendering**: Three.js WebGL Library
- **Color Data**: UBV Photometric System

## Version

**1.1.0** - Current Release

### What's New in v1.1.0
- ✨ **Glowing star texture** - Realistic cosmic glow effect with radial gradients
- 🎮 **Free-flight camera mode** - First-person FPS-style exploration
- 🐛 **Fixed mouse drag controls** - Smooth rotation in both camera modes
- 🎨 **Enhanced star rendering** - Full spectral colors with additive blending
- 💫 **Luminosity-based glow** - Brighter stars glow more intensely
- ✅ **Improved data validation** - Handles malformed catalog data gracefully

### Previous Releases
- **1.0.0** - Initial Release with basic 3D star rendering and multi-input support

---


For questions, issues, or improvements, refer to the included help panel in the visualizer.
