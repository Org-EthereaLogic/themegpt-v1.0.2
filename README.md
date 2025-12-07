<p align="center">
  <img src="asset/icons/logo-512.png" alt="ThemeGPT Logo" width="200">
</p>

<h1 align="center">ThemeGPT</h1>

<p align="center">
  <strong>Customize ChatGPT with friendly themes. No tracking.</strong>
</p>

<p align="center">
  <a href="https://chromewebstore.google.com/detail/dlphknialdlpmcgoknkcmapmclgckhba">
    <img src="https://img.shields.io/badge/Chrome%20Web%20Store-Install-blue?logo=googlechrome&logoColor=white" alt="Chrome Web Store">
  </a>
  <img src="https://img.shields.io/badge/version-1.0.2-green" alt="Version 1.0.2">
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/license-Apache%202.0-blue" alt="License">
  </a>
</p>

---

ThemeGPT instantly transforms ChatGPT's appearance with beautiful, curated themes—no coding, no CSS, no hassle. Just one click and your entire ChatGPT workspace reflects your personal style, reduces eye strain, and makes your most-used AI tool feel like yours.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

## Features

- **One-Click Theming** — Apply themes instantly without any technical knowledge
- **No CSS Required** — Beautiful pre-designed themes ready to use
- **Real-Time Preview** — See changes immediately as you browse themes
- **Eye Strain Reduction** — Dark modes and softer color palettes for extended sessions
- **Privacy-Focused** — No tracking, no data collection, just themes
- **Lightweight** — Minimal footprint, maximum impact

## Installation

### Chrome Web Store (Recommended)

Install ThemeGPT directly from the Chrome Web Store:

[![Install from Chrome Web Store](https://img.shields.io/badge/Chrome%20Web%20Store-Install%20Now-blue?style=for-the-badge&logo=googlechrome&logoColor=white)](https://chromewebstore.google.com/detail/dlphknialdlpmcgoknkcmapmclgckhba)

### Manual Installation (For Developers)

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/themegpt.git
   ```

2. Open Chrome and navigate to `chrome://extensions/`

3. Enable **Developer mode** (toggle in the top right)

4. Click **Load unpacked** and select the cloned directory

5. The ThemeGPT icon will appear in your browser toolbar

## Usage

1. **Open ChatGPT** — Navigate to [chat.openai.com](https://chat.openai.com) or [chatgpt.com](https://chatgpt.com)

2. **Click the ThemeGPT icon** — Find it in your browser's extension toolbar

3. **Browse themes** — Scroll through the available theme gallery

4. **Apply with one click** — Click any theme to instantly transform ChatGPT

5. **Enjoy!** — Your theme preference is saved automatically

## Development

### Prerequisites

- Google Chrome or any Chromium-based browser (Edge, Brave, etc.)
- Basic knowledge of Chrome extension development

### Project Structure

```
themegpt/
├── manifest.json      # Extension configuration
├── popup.html         # Extension popup UI
├── popup.js           # Popup functionality
├── contentScript.js   # Theme injection logic
├── themes.css         # Theme stylesheets
├── asset/             # Icons and images
└── app_docs/          # Documentation
```

### Local Development

1. Make your changes to the source files

2. Go to `chrome://extensions/` and click the refresh icon on ThemeGPT

3. Test your changes on ChatGPT

## Contributing

We welcome contributions from the community! Whether it's bug fixes, new themes, or feature improvements, your help makes ThemeGPT better for everyone.

Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the Apache License 2.0 — see the [LICENSE](LICENSE) file for details.

## Support

Having issues or questions?

- **Bug Reports & Feature Requests** — [Open an issue](../../issues) on GitHub
- **Discussions** — Join the conversation in [GitHub Discussions](../../discussions)

---

<p align="center">
  Made with care for the ChatGPT community
</p>
