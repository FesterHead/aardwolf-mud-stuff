# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-08-26

### Added

- Manual potion quaffing command aliases: `pquaff heal` (`pquaff h`) and `pquaff mana` (`pquaff m`).
- Interactive Monokai spectrum miniwindow buttons for manually quaffing heal and mana potions.
- Smart potion keyword extraction during container scanning to automatically detect MUD command keywords (`lotus`, `refresh`, `relief`, `honey`).
- Automatic silent potion bag scanning on connection, character login, and plugin initialization.
- New plugin `Aardwolf_Hunt_Trick.xml` (`phunt` / `phtrick`) for automated hunt-stepping and campaign hunt-trick target scanning.

### Changed

- Replaced base command prefix `quaff` with `pquaff` in `Aardwolf_Potion_Quaffer.xml` to prevent collisions with MUD commands.
- Expanded Potion Quaffer miniwindow size to 270x165px for better layout and button spacing.

### Fixed

- Fixed miniwindow drag handler overlay intercepting mouse click events on action buttons.
- Fixed hotspot lifecycle management to prevent client crashes during mouseover event callbacks.

## [1.0.0] - 2026-08-11

Initial version.
