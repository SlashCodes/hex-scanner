# Hex Scanner

A mobile-friendly barcode and QR code scanner that converts device codes between hex and decimal formats.

![Hex Scanner](assets/favicon.svg)

## Features

- 📷 **Camera Scanner** - Real-time barcode/QR code scanning using device camera
- 📁 **Image Upload** - Scan codes from uploaded images
- ⌨️ **Manual Input** - Enter codes manually (7-8 digit decimal or hex)
- 🔄 **Auto-Conversion** - Automatically converts between formats
- 📤 **Easy Sharing** - Share via SMS, Email, or native share sheet
- 📋 **Copy to Clipboard** - One-tap copy for each format

## Supported Input Formats

| Input | Description |
|-------|-------------|
| `2148004` | 7-digit decimal |
| `02148004` | 8-digit decimal (zero-padded) |
| `B220C6A4` | 8-character hex |
| `B2 20 C6 A4` | Hex with spaces |

## Output Formats

For any input, the app outputs:

- **Normalized Hex**: `B220C6A4`
- **Spaced Format**: `B2 20 C6 A4`
- **Decimal (8-digit)**: `02148004`

## Conversion Logic

```
Hex:     B2 20 C6 A4
         │  └──┬──┘
         │     │
Prefix───┘     └─── Last 3 bytes → 20C6A4 (hex) → 2148004 (decimal)
                                                  → 02148004 (zero-padded)
```

- The first byte (`B2`) is the model prefix
- The last 3 bytes are converted to decimal
- Decimal is zero-padded to 8 digits

## Installation

### Option 1: Direct Use
1. Download or clone the project
2. Open `index.html` in a web browser
3. For camera access, serve via HTTPS or localhost

### Option 2: Local Server
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .

# Using PHP
php -S localhost:8000
```

Then open `http://localhost:8000` in your browser.

### Option 3: Deploy
Upload the entire folder to any static web host:
- GitHub Pages
- Netlify
- Vercel
- Any web server

## Project Structure

```
hex-scanner/
├── index.html          # Main HTML file
├── css/
│   └── styles.css      # All styles
├── js/
│   ├── converter.js    # Hex/decimal conversion logic
│   ├── scanner.js      # Camera & barcode detection
│   ├── ui.js           # UI updates & interactions
│   └── app.js          # Main app initialization
├── assets/
│   └── favicon.svg     # App icon
└── README.md           # This file
```

## Browser Support

- **Camera Scanner**: Chrome, Edge, Safari (requires HTTPS)
- **Image Upload**: All modern browsers
- **Manual Input**: All browsers

### Camera Permissions

Camera access requires:
- HTTPS connection (or localhost)
- User permission granted

If camera doesn't work, use the **Upload Image** or **Manual Input** options.

## Sharing Options

- **💬 Text** - Opens SMS/Messages app
- **✉️ Email** - Opens default email client (Mail, Outlook, Gmail)
- **📤 Share** - Native share sheet (all available apps)

## Development

### Modules

- **Converter** - Handles all hex/decimal conversion logic
- **Scanner** - Manages camera and BarcodeDetector API
- **UI** - Handles DOM updates and user interactions
- **App** - Main controller connecting all modules

### Customization

To change the model prefix (default `B2`):
```javascript
// In js/converter.js
const Converter = {
  PREFIX: 'B2',  // Change this
  // ...
};
```

## License

MIT License - Feel free to use and modify.

## Troubleshooting

### Camera not working
1. Check browser permissions (Settings → Site Settings → Camera)
2. Ensure HTTPS or localhost
3. Try a different browser

### Barcode not detected
1. Ensure good lighting
2. Hold steady, fill frame with barcode
3. Try uploading a photo instead

### Share not working
- SMS requires a mobile device
- Email requires a configured mail client
- Native share requires browser support (Chrome, Safari)
