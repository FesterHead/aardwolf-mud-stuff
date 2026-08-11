# Agent Guidelines - Aardwolf MUD MUSHclient Project

This document (`AGENTS.md`) provides guidelines and rules for AI coding assistants working in this workspace. This repository contains Aardwolf MUD scripts, plugins, and utilities designed for MUSHclient version r2332 and higher (`requires="5.06"`).

Follow these rules to maintain high code quality, client compatibility, performance, and repository organization across all AI interactions.

---

## 1. MUSHclient Plugin XML Schema & Structure

- **XML Validation & Formatting**: All MUSHclient plugins must be valid XML files with the `.xml` extension, starting with `<?xml version="1.0" encoding="iso-8859-1"?>` (or `UTF-8`) and `<!DOCTYPE muclient>`.
- **Root Element**: Must start with `<muclient>` and contain `<plugin>`.
- **Name**: Must match the plugin's functional name (e.g., `Aardwolf_Auto_Open`).
- **Author**: Must contain `FesterHead`, appending additional authors if necessary.
- **Unique Plugin IDs**: Every plugin must have a unique 24-character hexadecimal `id` attribute. Never duplicate or reuse plugin IDs.
- **Language**: Must be set to `"Lua"`.
- **Purpose**: A concise description of the plugin's functionality.
- **Save State**: Set `save_state="y"` if plugin variables or configurations persist across client reloads.
- **Date Written**: Format as `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS`.
- **Version Attribute**: Must be set to a single-decimal float string such as `"1.0"` or `"1.00"`. **Do not use multi-decimal semver strings (e.g. "1.0.0")**, as MUSHclient fails to parse multi-decimal version numbers. Do not increment the version when making changes unless explicitly instructed by the user.
- **Requires**: Must be set to `"5.06"`.
- **CDATA Wrap**: Always wrap Lua script blocks inside `<![CDATA[ ... ]]>` tags to prevent XML parsing errors caused by Lua comparison operators (`<`, `>`, `&`).
- **Description Block**: Optional `<description trim="y">` child element inside `<plugin>` to provide extended usage documentation.

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE muclient>

<muclient>
  <plugin
    name="PluginName"
    author="FesterHead"
    id="1234567890abcdef12345678"
    language="Lua"
    purpose="Plugin purpose summary..."
    save_state="y"
    date_written="2026-06-26"
    version="1.0"
    requires="5.06"
  >
    <description trim="y">
      Detailed plugin description and usage instructions...
    </description>
  </plugin>

  <script>
    <![CDATA[
      -- Lua code goes here
    ]]>
  </script>
</muclient>
```

---

## 2. Lua Scripting Guidelines & Namespace Safety

- **Local Scope**: Declare all functions, variables, and imported modules as `local` to prevent polluting the global Lua table or clashing with other loaded plugins.
- **Lifecycle Callbacks**: Correctly implement common MUSHclient callbacks when required:
  - `OnPluginInstall()`: Startup checks, configuration loading, initial window creation.
  - `OnPluginClose()`: Resource cleanup, window deletion, and final variable persistence.
  - `OnPluginSaveState()`: Triggered when MUSHclient saves plugin state; save state variables here.
  - `OnPluginConnect()` / `OnPluginDisconnect()`: Handle connection state changes.
- **Resource Cleanup**: Always invoke `WindowDelete(win_id)` inside `OnPluginClose()` to free memory and avoid duplicate window handles upon plugin reloads.
- **Defensive Execution & Error Handling**: Wrap fragile external calls, database queries, and table deserialization in `pcall` or `xpcall` to prevent uncaught script errors from crashing client execution.

---

## 3. Aardwolf MUD & GMCP Integration

- **Prefer GMCP over Triggers**: Avoid text-scraping triggers for information available via Aardwolf GMCP (e.g., character vitals, status, inventory, room details, target stats).
- **GMCP Helpers**: Use `require "gmcphelper"` to access GMCP data.
  - Query data using helper functions: e.g., `gmcp("char.status")`, `gmcp("char.vitals")`, `gmcp("room.info")`.
  - Handle cases where GMCP data is `nil` or incomplete prior to character login or server initialization.
- **GMCP Broadcast Handler**: Listen for GMCP updates via `OnPluginBroadcast(msg, id, name, text)` checking for `msg == 1` (the standard `gmcphelper` broadcast message ID).

---

## 4. Miniwindows & UI Development

- **Layout & Positioning**: MUSHclient miniwindows are blank canvases:
  - Leverage `require "movewindow"` to enable user drag-to-reposition and coordinate persistence.
  - Support font scaling gracefully when window font sizes change.
- **Visibility & Rendering**: Call `WindowShow(win_id, true)` explicitly to ensure created miniwindows render on screen. Use standard fail-safe fonts (e.g., `Consolas`, `Dina`, `Courier New`).
- **Redraw Optimization**: Redraw miniwindows only when displayed data changes; avoid redrawing on every line or packet update to minimize CPU usage.
- **Visual Consistency**: Match the dark-mode aesthetic of the default Aardwolf Client Package (dark backgrounds, high-contrast status text, clean borders). Use `WindowText`, `WindowRectOp`, and color utilities appropriately.

---

## 5. Triggers, Aliases, and Timers

- **Trigger Efficiency**:
  - Make trigger match patterns as specific as possible.
  - Set `keep_evaluating="n"` if matching lines do not require subsequent trigger evaluation.
  - Use regex (`regexp="y"`) for dynamic matching, taking care to escape special symbols and validate capture groups.
- **Script Callbacks**: Use `send_to="12"` (send to script) or explicit script attributes when delegating trigger/alias execution to Lua functions.
- **Clean Command Aliases**: Ensure alias patterns do not collide with default Aardwolf commands unless intentionally overriding or wrapping them.

---

## 6. SQLite Databases

- **Database Engine**: For plugins needing structured, persistent storage (e.g., trackers, query logs, stats), use MUSHclient's built-in SQLite3 module:
  - Load via `local sqlite3 = require "sqlite3"`.
  - Resolve database file paths dynamically (e.g., relative to `GetPluginInfo(7, 1)` or inside `db/`).
  - Always finalize prepared statements and close database handles cleanly.
  - Wrap database opening, schema migrations, and queries in `pcall` error-handling blocks.

---

## 7. Directory & Project Structure

Maintain strict directory separation for repo organization:

- **`plugins/`**: All MUSHclient XML plugin files (e.g., `plugins/Aardwolf_Auto_Open.xml`) must reside here.
- **`lua/`**: Shared external Lua modules or standalone helper libraries.
- **`assets/`**: Media files, soundscapes, images, or static data assets.
- **`db/`**: SQLite database files used for local storage, caching, or logs.

Use `GetPluginInfo(7, 1)` to dynamically locate the plugin directory when referencing relative paths in scripts.

---

## 8. Versioning, Changelog, & Rules Policy

- **Changelog Versioning**:
  - Never increment the `CHANGELOG.md` version unless explicitly instructed by the user.
  - Do NOT ask the user if you should increment the changelog version.
- **Plugin Versioning**:
  - Do NOT increment plugin versions in XML files unless explicitly instructed by the user.
  - It is acceptable to ask the user if a plugin version should be incremented when making edits to that plugin.
- **Cross-AI Rules Standard**:
  - Maintain `AGENTS.md` as the primary cross-AI rules file. Do not duplicate rules across tool-specific configuration files (such as `.antigravityrules`, `.cursorrules`, `.clauderules`) unless explicitly requested by the user.
