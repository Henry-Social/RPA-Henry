# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Ui.Vision RPA - a browser extension for robotic process automation that supports Chrome, Edge, and Firefox. The project includes:
- Selenium IDE import/export functionality
- Computer vision capabilities for UI automation
- AI integration with Anthropic Claude for computer use and vision tasks
- Desktop screenshot editing and OCR functionality
- Side panel interface for macro management and AI chat

## Build & Development Commands

**Development:**
```bash
npm i -f
npm run ext          # Start development build (Chrome)
npm run start-ff     # Start development build (Firefox)
```

**Production builds:**
```bash
npm run build        # Build for Chrome
npm run build-ff     # Build for Firefox
```

Build outputs go to `dist/` (Chrome) and `dist_ff/` (Firefox) directories.

## Architecture

### Core Services
- **AnthropicService** (`src/services/ai/anthropic/anthropic.service.ts`): Handles Claude API integration for computer use, vision tasks, and AI chat
- **ComputerUseService** (`src/services/ai/computer_use/service.ts`): Manages computer use automation with coordinate parsing and screenshot processing
- **StorageManager** (`src/services/storage/`): Manages different storage strategies (browser filesystem, native filesystem, IndexedDB)
- **XModules** (`src/services/xmodules/`): Native host communication for desktop automation (xfile, xdesktop, xy)

### Extension Architecture
- **Background Script** (`src/ext/bg.js`): Main extension orchestrator handling IPC, storage, downloads, and tab management
- **Content Scripts** (`src/ext/content_script/`): Injected into web pages for DOM manipulation and command execution
- **Side Panel** (`src/containers/sidepanel/`): Main UI including macro editor, file management, logs, and AI chat
- **Vision Editor** (`src/vision_editor/`): Image annotation and computer vision task editor

### Key Components
- **Command System**: Commands defined in `src/actions/` with TypeScript types and execution logic
- **Storage Abstraction**: Multiple storage backends with consistent API in `src/services/storage/`
- **IPC System**: Inter-process communication between background, content scripts, and UI panels
- **Player System**: Macro execution engine with call stack and monitoring in `src/services/player/`

### AI Integration
- Anthropic Claude integration for computer use tasks
- Image processing with automatic scaling for API limits
- Coordinate parsing and scaling for different screen resolutions
- AI chat interface in side panel for interactive automation

### File Structure
- `extension/`: Static extension files (manifest, HTML, icons)
- `src/`: TypeScript/JavaScript source code
- `build/`: Build outputs and webpack configuration
- `command-line/`: Automation scripts for various platforms

## Technology Stack
- React + Redux for UI state management
- TypeScript for type safety
- Webpack for bundling
- Ant Design for UI components
- Anthropic SDK for AI integration
- Tesseract.js for OCR functionality