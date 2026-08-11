# Aardwolf MUD MUSHclient Project

A workspace for developing custom plugins, scripts, and utilities for the **Aardwolf MUD**, designed specifically for MUSHclient version r2332 and higher.

## Repository Directory Structure

This repository is structured into specific folders to separate concerns and ensure a clean environment:

| Directory | Purpose |
| :--- | :--- |
| [`assets/`](assets) | External media assets, soundscapes, images, and audio files used by plugins. |
| [`db/`](db) | SQLite database files used for persistent storage, caching, and logs. |
| [`lua/`](lua) | Shared external Lua libraries, helper modules, and custom script dependencies. |
| [`plugins/`](plugins) | Main repository for all MUSHclient plugin XML definition files. |

---

## Getting Started

To use the plugins in this repository:

1. Clone or download this repository.
2. In MUSHclient, open the File menu -> Plugins -> Add.
3. Browse and select the plugin XML files from the [`plugins/`](plugins) directory.

---

## Development Guidelines

When developing plugins for this repository, please adhere to the following best practices:

* **XML Schema & Validation**: All plugins must be valid XML with a `.xml` extension. Always wrap Lua code blocks inside `<![CDATA[ ... ]]>` tags.
* **Unique Plugin IDs**: Ensure every plugin has a unique 24-character hexadecimal ID. Never duplicate plugin IDs.
* **Scope & Namespace Safety**: Declare all variables, functions, and imports as `local` in Lua scripts to avoid polluting the global scope or conflicting with other plugins.
* **GMCP Integration**: Prefer GMCP for character details, status, room, and targeting data using `require "gmcphelper"` rather than scraping text output via triggers.
* **UI & Miniwindows**: Optimize redraws to minimize CPU usage, support clean window resizing, and leverage `require "movewindow"` for repositioning. Ensure window memory is freed using `WindowDelete()` inside the `OnPluginClose()` callback.
* **Database Management**: For tracking history or persistent state, load SQLite databases using `require "sqlite3"` and wrap queries in error-handling (`pcall`) blocks to prevent client crashes.

---

## License

This project is licensed under the MIT License - see the [`LICENSE`](LICENSE) file for details.
