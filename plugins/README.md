# MUSHclient Plugins Directory

This is the primary directory where all MUSHclient XML plugin definition files reside.

## Structure of a MUSHclient Plugin

All plugins must follow a structured schema compatible with MUSHclient:

- **XML Validation**: All MUSHclient plugins must be valid XML files with the `.xml` extension.
- **Root Element**: Must start with `<muclient>` and contain `<plugin>`.
- **Name**: Must be set to the plugin name.
- **Author**: Must contain FesterHead, appending if necessary.
- **Unique Plugin IDs**: Every plugin must have a unique 24-character hexadecimal `id` attribute. Do not copy-paste or reuse plugin IDs.
- **Language**: Must be set to "Lua".
- **Purpose**: Must be set to the plugin purpose.
- **Save State**: Set `save_state="y"` if you need plugin variables to persist across reloads or client sessions.
- **Date Written**: Must be set to the current date.
- **Version**: Must be set to a single decimal number like "1.0" or "1.00" for the first version (since MUSHclient does not support multi-decimal version numbers).
- **Requires**: Must be set to "5.06".
- **CDATA Wrap**: Always wrap Lua code blocks inside `<![CDATA[ ... ]]>` tags to prevent XML parser errors from Lua comparison operators (e.g., `<`, `>`, `&`).

Example Template:

```xml
<muclient>
  <plugin
    name="MyPlugin"
    author="FesterHead"
    id="abc123abc123abc123abc123"
    language="Lua"
    purpose="Description of the plugin"
    save_state="y"
    date_written="2026-06-26 12:00:00"
    version="1.0"
    requires="5.06"
  >
  </plugin>
  <script>
    <![CDATA[
      -- Lua logic goes here
    ]]>
  </script>
</muclient>
```

## Best Practices

1. **Callback Handlers**: Implement standard MUSHclient callbacks such as `OnPluginInstall` for initialization and `OnPluginClose` for resource deallocation.
2. **Minimize Triggers**: Use GMCP events (e.g. `char.vitals`, `char.status`) instead of parsing text trigger outputs.
3. **Miniwindow Repositioning**: Use standard helper modules such as `movewindow` to support window drag-to-reposition actions and window state persistence.
