# Databases Directory

This folder is intended for local SQLite database files used by plugins for structured, persistent data storage.

## Use Cases

- **Caching**: Storing game map layout data, room configurations, and zone listings.
- **Logbooks & Trackers**: Keeping history databases for player statistics, loot drops, combat performance, or quest lines.
- **Large Data Sets**: Keeping bulky data structures out of standard plugin XML configuration files or saving states.

## Best Practices

1. **Clean Resource Management**: Always close SQLite database handles when they are no longer in use, specifically during the `OnPluginClose()` callback.
2. **Robust Error Handling**: Wrap all query executions in safe-calling methods (e.g., Lua's `pcall` or return code checks) to prevent unhandled database exceptions from crashing MUSHclient scripts.
3. **Indices**: Add proper database indexes on frequently queried columns to ensure fast search response times.
