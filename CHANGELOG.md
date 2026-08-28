# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Added flight potion auto-quaffing to `Aardwolf_Potion_Quaffer.xml` when encountering "You can only fly there." movement barriers.
- Added `Fly:` counter line to `Aardwolf_Potion_Quaffer.xml` miniwindow.
- Added configurable `FLY_POTION_KEYWORDS` (`pquaff fly_keys`) and `FLY_POTION_CMD` (`pquaff fly_cmd`) for flight potion scanning and quaffing.
- Added manual quaff command alias `pquaff fly` (`pquaff f`).
- Added workspace settings in `.vscode/settings.json` configuring `DotJoshJohnson.xml` (XML Tools) as default XML formatter with automatic attribute splitting on save.

### Changed

- Updated Potion Quaffer miniwindow button layout to condensed side-by-side action buttons (`[ Heal ]`, `[ Mana ]`, `[ Fly ]`).
- Expanded Potion Quaffer miniwindow height to 190px to accommodate the extra counter line cleanly.
- Formatted plugin XML files (`Aardwolf_Auto_Open.xml`, `l33t_aarch_reporter.xml`) to split tag attributes across individual lines for readability.

### Fixed

- Fixed color code display formatting in `l33t_aarch_reporter.xml`.
- Fixed report output formatting in `l33t_aarch_reporter.xml` to display with proper line breaks instead of a single giant line.

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
