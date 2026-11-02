# Changelog

## v2026.11.02.48

- **Fill the card height** (`card_height_fill`): with a fixed card height, every alert block stretches to the full height instead of sitting centered at its own size, so short and long alerts match and line up with neighbouring cards. In Global Defaults → Look (shown once a height is set) and per custom theme. Requested in AlertTicker Card [#237](https://github.com/djdevil/AlertTicker-Card/issues/237).

## v2026.11.02.47

**Easy Alert Card (Ltek)** — forked from [AlertTicker Card](https://github.com/djdevil/AlertTicker-Card) 1.3.17 by djdevil and now a separate card.

- New identity: card type `custom:easy-alert-card`, files `easy-alert-card.js` / `easy-alert-card-editor.js`, its own element names, shared-code object, browser storage keys (`eac-*`), events and overlay, so it can run next to AlertTicker Card without either affecting the other.
- Moving from AlertTicker Card: every AlertTicker option is read as is (change `type:`), **📥 Import from AlertTicker Card** in the editor, and AlertTicker's saved snoozes, dismissals, sticky alerts, trigger states and history are copied once on first load.

Changes since AlertTicker Card 1.3.17:

### Added

- Notification alerts: one alert per notification — copies sent through a notify group (child contexts) or by separate automations (same title, message and tag within 10 s) merge into one alert listing every destination; dismissing it clears all copies. `merge_duplicates: false` on a rule set keeps one alert per copy.
- Docs: README gets a short **What's new** section, the missing 3D / weather themes in the theme tables (64 in all) and a current alert-editor section list; every YAML option, snippet and example moved to **[YAML.md](YAML.md)** (with undocumented options added and the push keys corrected to `push_notify*`).
- **Rule Sets** — named, reusable filters (`rule_sets:`, `rule_set:` on alerts) with include and exclude rules on the fields `entity_id`, `name`, `domain`, `device_class`, `area`, `floor`, `label`, `integration`, `state`, `attribute`, `last_changed_ago`, `other_entity`, `time` and `weekday`; operators `eq` `ne` `in` `not_in` `contains` `not_contains` `regex` `gt` `lt` `ge` `le` `between` `older` `newer`; `{{ template }}` values. Editor: a 🧩 Rule Sets section with HA pickers, a live match list with Exclude / Include per entity, "used by" links and *Create alert from this rule set*.
- **Notification alerts** — `watch: notifications` rule sets raise alerts from Home Assistant notifications, by Notification Source (automation / script, via context ids), Notification Destination (phones, notify groups and entities, the bell) and text; placeholders `{title}` `{message}` `{sent_by}` `{sent_to}`; tap dismisses. Editor: a scan for automations that send notifications and a *Recent notifications* list. `notifications_retention` card option.
- **Inline rules on single-entity alerts** — extra conditions with other entities, time of day, weekday and "unchanged for".
- Editor: Add buttons per alert type, one panel per alert / rule set (settings open inside the row), collapsible sections with a "changed" marker on non-default ones, summary chips.
- **Duplicate** an alert or a rule set (#233); **switch an alert off** with `enabled: false` (#232).
- **Order instead of priority:** drag-and-drop or ▲▼ reorder; a **Show in overlay** switch on each alert row and an "Alerts shown in the overlay" list in the Overlay tab.
- Rule fields `visibility` (hidden in HA) and `sun`.
- History: keep by number of alerts (up to 5000) or days (up to 5), and choose separately how much the card's 📋 panel shows (up to 500 alerts, or 1 hour – 5 days); a stored-history viewer in the editor.
- Notification alerts ignore Companion app commands (`clear_notification`, `command_*`, …); `clear_notification` + tag clears the matching alert, and a repeated tag replaces the earlier notification.
- Editor reorganised: the main screen is a stack of full-width tiles (Alerts, Rule Sets, Themes, Global Defaults, History, Overlay, All Clear). **Global Defaults** merges General and Layout into collapsible groups — Look, Cycling & Animation, Card controls, Snooze, Voice & Push. **History** has its own page. Every toggle is now a checkbox; headings, text and icon sizes follow the design guide (uppercase accent subtitles).
- Theme panel: on/off settings are checkboxes with a "Default: On/Off" note (accent when changed); new **Severity label** group (show / hide the Critical / Warning… label, custom text) per theme.
- **Test mode only applies while the card editor is open** (it ends when the editor closes, even if the dashboard stays in edit mode), so saving with it on is harmless (the "remember to disable" warning is gone). Editor previews (🔍) no longer travel in the card config, so a Save during a preview can't store them.
- **💾 Save** in every editor page header: saves the card and keeps editing (through the HA edit dialog's save function; hidden when unavailable).
- Themes filters: Themes in Use / My Custom Themes / Alert Presets / Built-Ins, each showing only its themes, by category and name; Reset buttons ask for confirmation.
- **Custom themes** replace in-place theme edits and per-alert look settings: built-in themes are read-only templates; ✎+ duplicates one into *My themes* (`custom_themes`, marked "based on …"), where icon, text, severity label, effects, colors and layout are set. The alert editor no longer has look settings. The editor moves existing per-alert look settings (and test-build `theme_styles`) into shared custom themes; the card still honours per-alert look keys in YAML. Associations are separate (`theme_associations`) and work on any theme.
- Alert Presets are fully editable: built-in and own associations are the same chips on a theme — remove, add, or move a built-in association to another theme (that preset then uses it); Reset associations restores the defaults. Stored as `theme_styles.<theme>.preset_items`.
- Overlay tab: "Alerts shown in the overlay" rows use an eye icon (shown / hidden) instead of checkboxes; fixes the `[object Object]` that appeared before each name.
- Presets show their domain / device class as chips in every header (Alert Presets, theme list, theme panel); the Alert Preset group is first in a theme's panel; subtitles inside panels have a divider above them.
- **Themes** page: filter buttons (Used / Customized / Alert Presets / All), a ✎ pencil to edit each theme, and **Associated domains** that turn a theme into an Alert Preset (`preset_domains`, `preset_state`). Customize any theme in place (`theme_styles`) — text size/color, effects, colors and layout per theme, with preview and Reset to Default; settings layer card → theme → alert.
- Alert Presets: 🔍 previews a preset on the card in the editor's preview pane.
- Per-alert text style: size (slider) and color (default / theme color / custom / CSS) for the message and for the entity info line.
- Per-alert **Pulse the card** and **Flash the background** (on by default for alarm and intruder, which already flash; can be turned off there). Both follow Disable animations.
- New theme **`water`** ("Water"): Flood's look with a fluid water level — layered waves, swell and bubbles; fills to a `%` entity's value.
- **All Notifications** preset (listed first; the other presets are alphabetical); a **Quick Start** panel on the editor's main screen.
- Alert editor sections: **Options** (Persistent / Sticky, Show in overlay, snooze duration, trigger on any change), **Appearance** (theme, entity-name line, icon source — theme / emoji / entity's HA icon / custom `mdi:` / entity picture / image —, accent color, animations, custom card), **Condition**, **Alert Grouping** (tap / hold inside), **Tap Actions** (Single Tap, Double Tap, Hold, Snooze), **Set Entity Value**. Checkboxes instead of toggles; a pencil marks sections changed from the defaults.
- `rules:` as an alias for `groups:` on a rule set (a flat list = all must match); per-rule `enabled: false`; rule-set Export with per-rule match counts for troubleshooting.
- **Alert Presets panel** (was "Alert Templates") replaces the template dropdown: each preset shows what it can match here and what's active now, with Create / Create & edit; preset alerts are inserted by importance.
- **Can match N entities** inside an alert: every entity it can cover, independent of their current state.

### Changed

- The editor converts quick filters (`entity_filter`, `device_class`, `label_filter`, `area_filter`, exclusions), extra `conditions` and `time_range` into rules when a card is opened; the card shows the same alerts. All of them still work in YAML. The Quick filter mode, the extra-conditions list and the time-range section are replaced by rule sets / inline rules.
- One matching engine for the card, the overlay and the editor. The overlay now follows the card where they differed: an empty `state`, no state on an "off" entity, `attribute[n]` paths, missing attributes, `{{ }}` states, and filter alerts' extra conditions (the overlay ignored them).
- Faster matching: ~37% less work per card update and ~82% per overlay tick (2,000-entity benchmark); results are shared by the card, the overlay and the editor.
- `label_filter`- and `area_filter`-only alerts now show the matched entity's name under the message, like `entity_filter` / `device_class` alerts.
- The editor replaces `priority` with the list order (same order on the card) and `overlay_min_priority` with the per-alert **Show in overlay** switch. YAML with `priority` still sorts by it. The overlay follows the card's order.

### Fixed

- `auto_dismiss_after` never fired when the dashboard was reloaded, the view changed or the card re-rendered before it ran out: the timer lived in the browser and restarted each time. It now counts from when the condition became true (the entity's last change, like `trigger_delay`), so it also holds after a reload (#234).
- `conditions_logic: or` required the alert's own condition and applied OR only among the extra conditions; it now means own condition OR any extra condition (#231).
- `navigate` tap actions with `{{ }}` in the path threw a ReferenceError.

---

For AlertTicker Card's own history up to 1.3.17, see [its changelog](https://github.com/djdevil/AlertTicker-Card/blob/main/CHANGELOG.md).
