# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Calgary Property Partners is a real estate investment company website built as a **macOS-inspired desktop UI** running entirely in the browser. The entire application lives in a single file: `index.html`.

## Development

No build process, package manager, or toolchain. To view the site, open `index.html` directly in a browser. No installation or compilation required.

## Architecture

Everything — HTML structure, CSS styles, and JavaScript logic — is embedded in `index.html`:

- `<style>` block: All styling (dark theme, gold accents via `--color-gold: #C9A84C`, glassmorphism, macOS-like window chrome)
- `<script>` block: All application logic

### Window Management System

A custom window manager simulates a desktop OS. Each "app" is a draggable, closeable window. Windows stack via z-index management, support minimize/maximize, and are launched from a dock or icon grid.

### Applications

| App | Key Detail |
|-----|-----------|
| **BRH Calculator** | Real estate Buy/Rent/Hold analysis — ~25 inputs, calculates Cap Rate, Cash-on-Cash, DCR, LTV, ROI |
| **Contact** | EmailJS integration (`service_rjkml9p`, template `template_sxkmljd`, public key `gejvTBGYYCcVWWuJi`) |
| **Weather** | Open-Meteo API, Calgary hardcoded at `(51.0447, -114.0719)` |
| **Bitcoin** | CoinCap v2 API + ExchangeRate-API for USD→CAD, auto-refreshes every 60s |
| **Wordle** | Full game with 600+ word list, stats persisted in `localStorage` |
| **Market / FAQ / Blog / Testimonials / About** | Static content windows |

### External Dependencies (CDN only)

- EmailJS v4 (`email.min.js`)
- Google Fonts: Playfair Display, DM Sans, DM Mono

No npm packages. No module bundler.

## Key Conventions

- All new UI components should follow the macOS window pattern already in use (title bar with red/yellow/green buttons, draggable header, content area).
- Color scheme uses CSS custom properties defined at the top of the `<style>` block — prefer these variables over hardcoded colors.
- `localStorage` is used only for Wordle game statistics; avoid expanding its use without good reason.
- The EmailJS public key and service/template IDs are intentionally exposed client-side (this is normal for EmailJS).
