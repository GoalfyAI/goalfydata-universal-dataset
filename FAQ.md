# FAQ

### 1. What is GoalfyData?

GoalfyData provides governed datasets for AI agents. It helps you persist business data, field definitions, table relationships, metric definitions, processing rules, and usage guidelines — so different agents don't need to re-understand the data every time, and can continuously query, update, and reuse it.

### 2. Is GoalfyData a database?

Not a traditional database, and not a replacement for MySQL, Excel, Airtable, or spreadsheets. GoalfyData is more like a data context layer for agents — helping them understand where data lives, what fields mean, how tables relate, how metrics should be calculated, and which data can be safely accessed.

### 3. How is GoalfyData different from spreadsheets, databases, or BI dashboards?

Spreadsheets and databases mainly store data. BI dashboards mainly display results. GoalfyData focuses on enabling agents to continuously understand and use data — including data structure, primary keys, table relationships, metric definitions, update methods, governance rules, and Agent Skills.

So it's not just about displaying results — it's about turning data into assets that agents can call, update, and reuse.

### 4. Which agents does GoalfyData work with?

Currently focused on ChatGPT, Codex, Claude Code, Manus, and MCP / CLI agent workflows. You can let agents query datasets, update data, generate reports, or build dashboards / apps from datasets — without repeatedly uploading files and explaining data rules.

### 5. What's stored in a dataset?

GoalfyData stores more than just table data, including:

- Data tables, field definitions, and primary keys
- Table relationships and field mappings
- Metric definitions and processing rules
- Data update methods: full replace, append, upsert, and scheduled sync
- Agent Skills and recommended usage patterns
- Permission policies and sharing authorizations

This way, when agents access data, they don't just read it — they understand how it should be used.

### 6. What does "data updates" mean in pricing?

"Data updates" refers to the number of tasks available for dataset updates within each 30-day period. This includes dataset updates, sync tasks, script runs, and agent-triggered data refreshes. Different plans offer different data update quotas, storage limits, and active app limits.

### 7. What does "active apps" mean?

Active apps refers to the number of applications currently in online status, including dashboards or lightweight apps built from datasets. Apps that are in draft, building, or offline status don't count toward the active app limit.

### 8. How do plan quotas and add-on packs work?

Plan quotas reset automatically every 30 days. Add-on pack quotas are valid for 30 days from purchase date and expire without auto-renewal. The system uses plan quotas first; once depleted, it consumes the corresponding add-on pack quota.

### 9. Is my data secure?

GoalfyData does not publicly expose your private data by default. You can control access to datasets, apps, and agents through permission policies and sharing authorizations. Only authorized members, apps, links, or agents can access the corresponding data — private workspace data is never publicly displayed.
