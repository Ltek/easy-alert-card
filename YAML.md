# Easy Alert Card — YAML reference

Everything the card reads from YAML. You don't need any of it: the visual editor writes all of these for you (see the [README](README.md)). This file is for writing or checking a config by hand.

```yaml
type: custom:easy-alert-card
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    theme: door
    message: "Front door open"
```

## Contents

- [Card-level options](#card-level-options)
- [Alert-level options](#alert-level-options)
- [Action object](#action-object)
- [Custom themes & Alert Preset associations](#custom-themes--alert-preset-associations)
- [Rule sets](#rule-sets)
- [Notification rule sets](#notification-rule-sets)
- [Feature options](#feature-options) — TTS, push, music player
- [Feature snippets](#feature-snippets)
- [Examples](#examples)

## Card-level options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `cycle_interval` | `number` | `5` | Seconds between alerts when cycling |
| `cycle_animation` | `string` | `fold` | Transition animation |
| `show_when_clear` | `boolean` | `false` | Show card when no alerts are active |
| `clear_message` | `string` | `""` | Message shown in all-clear state (message mode) |
| `clear_theme` | `string` | `success` | Theme for all-clear (`success`, `check`, `confetti`, …) |
| `clear_display_mode` | `string` | `message` | All-clear widget: `message`, `clock`, `weather`, `weather_clock`, `forecast`, `weather_forecast` |
| `clear_clock_style` | `string` | — | Clock style: `aurora`, `gold`, `matrix` |
| `clear_weather_style` | `string` | — | Weather badge style: `stage`, `split`, `cinematic`, `wallpanel` |
| `clear_clock_show_date` | `boolean` | `true` | Show or hide the date in clock / weather+clock mode |
| `clear_clock_show_seconds` | `boolean` | `true` | **New in 1.3.9.9.6** — hide seconds from the clock display for a cleaner `15:58` look instead of `15:58:47` |
| `clear_clock_date_position` | `string` | `below` | Date position relative to time: `above` or `below` |
| `clear_weather_entity` | `string` | `null` | `weather.*` entity for weather/weather_clock modes |
| `clear_badge_label` | `string` | `"Resolved"` | Badge text on the all-clear card |
| `clear_tap_action` | `object` | — | Tap action for the all-clear card |
| `clear_hold_action` | `object` | — | Hold action for the all-clear card |
| `clear_double_tap_action` | `object` | — | Double-tap action for the all-clear card |
| `show_widget_in_cycle` | `boolean` | `false` | Insert the clear widget as a slide in the alert cycle |
| `snooze_default_duration` | `number` | *(menu)* | Fixed snooze duration in hours (`0.5`, `1`, `4`, `8`, `24`). Omit for menu. |
| `show_snooze_bar` | `boolean` | `true` | Set `false` to hide the amber snooze reactivation bar and pill |
| `large_buttons` | `boolean` | `false` | Always-visible pill-shaped 💤 and 📋 buttons |
| `swipe_to_snooze` | `boolean` | `false` | Left-swipe gesture to snooze on touch devices |
| `vertical` | `boolean` | `false` | Vertical layout — icon on top, message centered below |
| `text_align` | `string` | `left` | `center` to center message text (useful in wide Panel layouts) |
| `ha_theme` | `boolean` | `false` | Adapt card colors to the active HA global theme |
| `history_keep_mode` / `history_keep` | `string` / `number` | `count` / `50` | What this browser stores: `count` = up to N alerts (max 5000), `days` = N days (max 5). Replaces `history_max_events` (still read) |
| `custom_themes` | `object` | — | See [Custom themes](#custom-themes--alert-preset-associations). Your themes: `{ <id>: { base, name, …look } }`. Look keys: `icon`, `icon_color`, `icon_size`, `icon_image`, `use_ha_icon`, `use_entity_picture`, `message_size`, `message_color`, `entity_size`, `entity_color`, `show_badge`, `badge_label`, `pulse`, `flash_background`, `disable_animation`, `color` (accent), `card_background`, `card_height`, `card_height_fill`, `font_scale`, `text_align`, `card_border`, `severity_border` |
| `theme_associations` | `object` | — | Alert Preset associations per theme (built-in or custom): `{ <theme>: { items: ["domain:x", "class:y", "builtin:<preset>:<n>"], state } }` |
| `history_show_mode` / `history_show` | `string` / `number` | all | What the card's 📋 panel lists: `count` = the latest N (max 500), `hours` = the last N hours (1–120); omit = everything stored |
| `active_state_entity` | `string` | — | **Per-alert.** `input_boolean.*` entity to write `on`/`off` to when this specific alert becomes active or clears. Each alert can target a different boolean. Works only while the browser tab is open. |
| `card_height` | `number` | *(auto)* | Fixed card height in px — prevents layout shifts when cycling |
| `card_height_fill` | `boolean` | `false` | With `card_height`: stretch every alert block (background + severity border) to the full height instead of centering it, so short and long alerts are the same size. Horizontal layout only (vertical always fills). Also a custom-theme key |
| `font_scale` | `number` | `1` | **New in 1.3.9.9.7** — proportional zoom for HD / 4K / wall-panel displays. `1` = normal, `1.5` = 50% larger, `2` = double. May require bumping `grid_options.rows`. |
| `card_border` | `boolean` | `false` | Show the standard HA border around the card at all times |
| `severity_border` | `boolean` | `true` | Show the 1px severity-colored border around each alert block. Set `false` to keep badge/icon color coding without the border. Width themeable via `--atc-severity-border-width`. |
| `overlay_mode` | `boolean` | `false` | Show a floating banner when a new alert triggers — visible from any dashboard view |
| `overlay_position` | `string` | `top` | Banner position: `top`, `center`, or `bottom` |
| `overlay_duration` | `number` | `8` | Seconds before auto-dismiss (0 = manual close only) |
| `overlay_scale` | `number` | `1` | Banner zoom factor: `1`, `1.5`, `2`, or `3` |
| `tts_enabled` | `boolean` | `true` | Master toggle — set `false` to silence all TTS globally |
| `tts_entity` | `string` | — | Default `media_player.*` speaker entity |
| `tts_engine` | `string` | *(auto)* | TTS engine entity (auto-detected from first `tts.*` state if omitted) |
| `tts_notify_service` | `string` | — | Default notify service for Alexa / push (e.g. `alexa_media_echo_dot`) |
| `tts_language` | `string` | — | Language code passed to `tts.speak` (e.g. `it-IT`) |
| `push_notify_enabled` | `boolean` | `true` | Master toggle — set `false` to disable all push notifications globally |
| `clear_weather_temperature_entity` | `string` | — | Override weather temperature with a local sensor entity |
| `clear_weather_humidity_entity` | `string` | — | Override weather humidity with a local sensor entity |
| `clear_weather_temp_high_entity` | `string` | — | Override today's high temperature with a sensor |
| `clear_weather_temp_low_entity` | `string` | — | Override today's low temperature with a sensor |
| `clear_weather_aqi_entity` | `string` | — | Show air quality / PM2.5 from a sensor in the weather badge |
| `show_history_button` | `boolean` | `true` | Set `false` to hide the 📋 history button completely |
| `show_snooze_button` | `boolean` | `true` | Set `false` to hide the 💤 snooze button completely |
| `test_mode` | `boolean` | `false` | Show all alerts as active (ignore conditions). Only applies while this card's editor is open — the live card ignores it, so saving with it on is harmless |
| `disable_animation` | `boolean` | `false` | Stop all ambient animations (pulse, flash, icon motion, weather effects) on every alert |
| `card_background` | `boolean\|string` | — | `true` = the HA card background, or any CSS color (e.g. `rgba(20,20,30,0.7)`) instead of the theme's |
| `show_counter` | `boolean` | `true` | Set `false` to hide the 1/3 alert counter |
| `show_dismiss_bar` | `boolean` | `true` | Set `false` to hide the bar that restores dismissed (persistent) alerts |
| `overlay_dismissible` | `boolean` | `true` | `false` = the banner never auto-hides and has no close button; it stays until the condition clears |
| `overlay_rotation` / `overlay_rotation_interval` | `boolean` / `number` | `false` / `5` | Cycle the banner through all active alerts (1/N counter), N seconds each |
| `weather_forecast_interval` | `number` | `5` | Seconds between current weather and forecast in `weather_forecast` mode |
| `clear_icon` / `clear_icon_color` / `clear_icon_size` | `string` | — | All-clear icon (emoji or `mdi:`), its color and size |
| `clear_clock_12h` | `boolean` | `false` | 12-hour clock (AM/PM) |
| `clear_clock_color` / `clear_clock_date_color` / `clear_clock_background` | `string` | — | Custom clock digit, date and background colors |
| `clear_disable_animation` | `boolean` | `false` | Freeze sun, clouds, stars and weather effects in the all-clear widget |
| `history_max_events` | `number` | — | *Legacy* — read as `history_keep` (a count) |
| `theme_styles` | `object` | — | *Legacy (test builds)* — the editor turns it into `custom_themes` |
| `alerts` | `list` | `[]` | List of alert objects |
| `rule_sets` | `list` | — | Named [rule sets](#rule-sets) used by alerts' `rule_set:` |
| `notifications_retention` | `number` | `3600` | Seconds a sent (mobile / notify) notification stays an alert — see [Notification rule sets](#notification-rule-sets) |

## Alert-level options

| Option | Type | Required | Description |
|--------|------|----------|-------------|
| `name` | `string` | ❌ | Editor display label for this alert panel |
| `entity` | `string` | ✅* | Entity ID |
| `rule_set` | `string\|object` | ✅* | Id of a [rule set](#rule-sets) (one alert per match), or inline rules — on a single-entity alert, its extra conditions |
| `entity_filter` | `string` | ✅* | Text filter — supports `*` wildcard (replaces `entity`) |
| `entity_filter_exclude` | `list` | ❌ | Entity IDs to exclude from `entity_filter` or `device_class` match |
| `device_class` | `string` | ✅* | HA device class (e.g. `smoke`, `battery`, `motion`) — auto-discovers all matching entities |
| `show_filter_name` | `boolean` | `true` | Set `false` to hide the entity friendly name below the message |
| `attribute` | `string` | ❌ | Attribute to check instead of state — supports dot-notation (e.g. `activity.0.forecast`) |
| `operator` | `string` | ❌ | `=` `!=` `>` `<` `>=` `<=` `contains` `not_contains` (default: `=`) |
| `state` | `string` | ✅ | Trigger value — supports Jinja2 templates (e.g. `{{ states('input_number.threshold') }}`) |
| `on_change` | `boolean` | `false` | Trigger on any state change — ignores `operator`/`state` |
| `auto_dismiss_after` | `number` | ❌ | Auto-hide after N seconds. For `on_change`: starts on trigger. For condition alerts: starts when condition first becomes true. |
| `time_range` | `object` | ❌ | `{from: "HH:MM", to: "HH:MM"}` — restrict to a time window (midnight crossing supported) |
| `visible_to` | `string\|list` | ❌ | `admin`, `non_admin`, a display-name string, or a list of names |
| `message` | `string` | ✅ | Text shown when active — supports `{name}`, `{entity}`, `{state}`, `{timer}`, `{device}` |
| `secondary_text` | `string` | ❌ | Static second line below the message — supports `{state}`, `{name}`, `{entity}` |
| `theme` | `string` | ❌ | Built-in theme or a [custom theme](#custom-themes--alert-preset-associations) id (default: `emergency`) |
| `priority` | `number` | ❌ | *Legacy:* 1–4. Still sorts YAML that has it; the editor replaces it with the list order |
| `enabled` | `boolean` | `true` | `false` switches the alert off — nothing on the card, in the overlay, TTS or push (test mode still previews it) |
| `icon` | `string` | ❌ | Emoji or `mdi:` icon override |
| `use_ha_icon` | `boolean` | ❌ | Use HA native icon (auto-read from entity, or pick via icon picker) |
| `use_entity_picture` | `boolean` | ❌ | Use the entity's `entity_picture` attribute as the alert icon |
| `icon_image` | `string` | ❌ | Static image path (`/local/…`) or full URL — takes priority over `use_entity_picture` |
| `icon_size` | `string` | `2rem` | Size of the image icon — any CSS length (applies to `icon_image` and `use_entity_picture`) |
| `icon_color` | `string` | ❌ | CSS color for the MDI icon (requires `use_ha_icon: true`) |
| `show_badge` | `boolean` | `true` | Set `false` to hide the category badge |
| `badge_label` | `string` | ❌ | Custom text for the category badge |
| `message_size` / `message_color` | `number` / `string` | theme | Message text size (px, 10–40) and color (`var(--…)`, `#rrggbb` or any CSS color) |
| `entity_size` / `entity_color` | `number` / `string` | theme | Same for the entity info line(s) under the message (entity name / state, secondary value) |
| `pulse` | `boolean` | `false` | The whole card gently grows and glows in the theme (or accent) color |
| `flash_background` | `boolean` | on for `alarm` / `intruder`, else off | Flash the card's background in the theme (or accent) color; `false` keeps alarm / intruder steady. Pulse and flash stop with `disable_animation` |
| `secondary_entity` | `string` | ❌ | Entity whose live value appears below the message |
| `secondary_attribute` | `string` | ❌ | Attribute of `secondary_entity` to show — supports dot-notation |
| `show_secondary_name` | `boolean` | `false` | Show the entity friendly name next to the secondary value |
| `show_filter_state` | `boolean` | `false` | Show translated entity state next to the entity name (`entity_filter` only) |
| `snooze_duration` | `number\|null` | ❌ | Override global snooze: hours, `null` for menu, omit to use global |
| `sound` | `boolean` | `false` | Play a sound when this alert becomes active |
| `sound_url` | `string` | ❌ | Custom `.mp3`/`.wav` URL — omit for auto-generated tone |
| `tts` | `boolean` | `false` | Read the alert aloud when it becomes active |
| `tts_entity` | `string` | ❌ | Override the global `media_player.*` speaker for this alert |
| `tts_engine` | `string` | ❌ | Override the global TTS engine entity |
| `tts_notify_service` | `string` | ❌ | Override the global notify service (for Alexa / push) |
| `tts_notify_type` | `string` | `tts` | Notify type sent to the service — use `announce` for Alexa speaker groups |
| `tts_message` | `string` | ❌ | Custom spoken text — omit for auto-generated multilingual sentence |
| `push_notify` | `boolean` | `false` | Send a push notification when this alert becomes active |
| `push_notify_service` | `string` | ❌ | Target `notify.*` service (without prefix, e.g. `mobile_app_iphone`) |
| `push_notify_title` | `string` | ❌ | Notification title — supports `{name}`, `{state}`, `{entity}`, `{device}`, Jinja2 |
| `push_notify_message` | `string` | ❌ | Notification body — same placeholders; falls back to `message` if empty |
| `show_player_controls` | `boolean` | ❌ | Enable graphical music player UI for `media_player.*` entities (requires `theme: music`) |
| `music_player_color` | `string` | ❌ | Accent color for the music player UI — any CSS color (default `#e040fb`) |
| `music_show_art` | `boolean` | `true` | Show album artwork in the music player (background blur + thumbnail) |
| `music_show_title` | `boolean` | `true` | Show track title (with marquee for long titles) |
| `music_show_artist` | `boolean` | `true` | Show artist name |
| `music_show_controls` | `boolean` | `true` | Show previous / play-pause / next / mute buttons and volume slider |
| `music_show_power` | `boolean` | `false` | Add a power icon in the bottom-right corner — calls `media_player.turn_off` |
| `music_show_player_picker` | `boolean` | `false` | Add a cast icon in the bottom-right corner — dropdown to switch the active player for this session |
| `music_compact_layout` | `boolean` | `false` | Compact layout: track title + artist move to the top-right column, controls stay left — ideal for small displays |
| `battery_trim_name` | `boolean` | `false` | (`theme: battery` only) Strip the trailing word "Battery" from entity friendly names to shorten long labels |
| `camera_entity` | `string` | ❌ | Camera entity for overlay banner and card background |
| `camera_live` | `boolean` | `false` | Show a live HLS/WebRTC stream in the overlay banner instead of a static snapshot (requires `camera_entity`) |
| `camera_in_card` | `boolean` | `false` | Show the camera image as a background layer behind the alert card slide (requires `camera_entity`) |
| `history_message` | `string` | ❌ | Custom text recorded in the history log — overrides `message` for history entries; supports `{name}`, `{state}`, `{entity}` |
| `secondary_value_align` | `string` | `below` | Position of the secondary value: `below` (default, shown under the message) or `right` (shown on the same row as the title) |
| `conditions_logic` | `string` | ❌ | `and` or `or` for extra conditions |
| `conditions` | `list` | ❌ | Extra entity conditions |
| `color` | `string` | ❌ | Accent color (look key — see note below) |
| `disable_animation` | `boolean` | `false` | Stop this alert's ambient animations (look key) |
| `persistent` | `boolean` | `false` | Stays on the card after the condition clears, until dismissed with ✕ |
| `overlay` | `boolean` | `true` | `false` keeps this alert out of the overlay banner |
| `trigger_delay` | `number` | ❌ | Only alert if the condition holds for N seconds (like an automation's `for:`) |
| `label_filter` / `area_filter` | `string\|list` | ❌ | *Legacy filters* — HA label / area; the editor converts them into a rule set |
| `device_class_exclude` | `list` | ❌ | *Legacy* — entities excluded from a `device_class` match |
| `group` / `group_min` | `boolean` / `number` | `false` / `3` | Show matching entities as one summary slide once at least N are active |
| `group_message` / `group_secondary_text` | `string` | ❌ | Summary text — `{count}`, `{names}`, Jinja2 |
| `group_expanded_message` | `string` | ❌ | Message per entity when the group is expanded |
| `group_tap_action` / `group_hold_action` / `group_double_tap_action` | `object` | ❌ | Actions on the group summary slide |
| `card` | `object` | ❌ | Replace the theme with any HA card config (`this.entity_id` = the alert's entity) |
| `music_compact_show_badge` | `boolean` | ❌ | NOW PLAYING badge in the compact music layout |
| `tap_action` | `object` | ❌ | Action on tap |
| `hold_action` | `object` | ❌ | Action on hold (500 ms) |
| `double_tap_action` | `object` | ❌ | Action on double-tap (single tap waits 300 ms to distinguish) |
| `snooze_action` | `object` | ❌ | Action executed when 💤 is tapped |

*One of `entity`, `rule_set`, `entity_filter`, or `device_class` is required.

> **Look keys on an alert** (`icon`, `use_ha_icon`, `use_entity_picture`, `icon_image`, `icon_size`, `icon_color`, `color`, `show_badge`, `badge_label`, `message_size`, `message_color`, `entity_size`, `entity_color`, `pulse`, `flash_background`, `disable_animation`) still work when written by hand. The visual editor moves them into a [custom theme](#custom-themes--alert-preset-associations) the first time it opens the card, so every look setting lives on a theme.

## Action object

Used by `tap_action`, `hold_action`, `double_tap_action`, `snooze_action`, the `group_*_action`s and the `clear_*_action`s.

| Field | Description |
|-------|-------------|
| `action` | `call-service` · `navigate` · `more-info` · `url` · `none` |
| `service` | HA service in `domain.service` format |
| `target` | `{entity_id: "..."}` |
| `service_data` | Extra service parameters (object) |
| `navigation_path` | Path for `navigate` action |
| `url_path` | URL for `url` action |
| `entity_id` | Entity for `more-info` action |

## Custom themes & Alert Preset associations

Built-in themes are fixed. A custom theme copies one (`base`) and holds every look setting; alerts pick it by id like any theme. Associations (what makes a theme an Alert Preset) are stored separately and work on any theme, built-in or custom. See [Themes](README.md#-themes) in the README.

```yaml
custom_themes:
  flood_custom: { base: flood, name: "Flood (basement)", message_size: 20, pulse: true, show_badge: false }
theme_associations:
  flood_custom: { items: ["domain:valve"], state: open }   # own association → an Alert Preset
  door:   { items: ["builtin:doors_windows:0"] }            # Doors & Windows' door alert moved to the door theme
  caution: { items: [] }                                     # caution no longer holds Doors & Windows
alerts:
  - theme: flood_custom
```

**Custom theme keys:** `base` (built-in theme), `name`, and the look keys `icon`, `icon_color`, `icon_size`, `icon_image`, `use_ha_icon`, `use_entity_picture`, `message_size`, `message_color`, `entity_size`, `entity_color`, `show_badge`, `badge_label`, `pulse`, `flash_background`, `disable_animation`, `color` (accent), `card_background`, `card_height`, `card_height_fill`, `font_scale`, `text_align`, `card_border`, `severity_border`.

**Association items:** `domain:<domain>`, `class:<device class>` (your own — build one alert with that theme, when the state is `state`, otherwise on any change), and `builtin:<preset>:<n>` (an alert of a built-in preset, moved to this theme). `items: []` removes the theme's built-in associations.

## Rule sets

See [Rule Sets](README.md#-rule-sets) in the README for what they do.

```yaml
type: custom:easy-alert-card
rule_sets:
  - id: entry_open
    name: Entry open at night
    groups:
      - mode: include          # include = must match · exclude = drops what matches
        match: all             # all | any — how these rules combine
        rules:
          - { field: label, op: in, values: [security] }
          - { field: area,  op: eq, value: entry }
          - { field: state, op: in, values: ["on", open, unlocked] }
          - { field: time,  op: between, value: "21:00", value2: "06:00" }
      - mode: exclude
        match: any
        rules:
          - { field: label, op: in, values: [ignore_alerts] }
alerts:
  - rule_set: entry_open
    theme: intruder
    message: "{name} open"
```

```yaml
- id: open_locks
  rules:
    - { field: domain, op: eq, value: lock }
    - { field: state,  op: eq, value: unlocked }
```

```yaml
- entity: binary_sensor.front_door
  state: "on"
  rule_set:                      # inline: rules for this alert only
    groups:
      - mode: include
        match: all
        rules:
          - { field: other_entity, entity: alarm_control_panel.home, op: in, values: [armed_away, armed_night] }
          - { field: time, op: between, value: "22:00", value2: "07:00" }
```

`rules:` works as an alias for `groups:`, and a plain list of rules means "all of these":

| Field | Matches |
|---|---|
| `entity_id`, `name`, `domain` | The entity's id, friendly name, domain |
| `device_class`, `integration` | Its device class, the integration it comes from |
| `area`, `floor` | Its area (else its device's area) / that area's floor — by id or name |
| `label` | Its labels (any of them) |
| `state`, `attribute` | Its state, or an attribute (`attribute: battery_level`, dot paths and `[n]` work) |
| `last_changed_ago` | Seconds since it last changed — "unchanged for at least N seconds" |
| `other_entity` | **Another** entity's state or attribute (`entity:`, optional `attribute:`) — e.g. *only while the alarm is armed*. `{entity}` means the matched entity |
| `time` | Time of day, `"HH:MM"` — `between` crosses midnight |
| `weekday` | `mon` … `sun` (or 1–7) |
| `visibility` | `shown` / `hidden` — whether the entity is hidden in Settings → Entities |
| `sun` | `above_horizon` / `below_horizon` (from `sun.sun`) |

Operators: `eq`, `ne`, `in`, `not_in`, `contains`, `not_contains`, `regex`, `gt`, `lt`, `ge`, `le`, `between`, `older` / `newer` (age of a timestamp, in seconds). Text compares ignore upper/lower case unless the rule has `case_sensitive: true` (*Match upper / lower case* in the editor). Values may be `{{ templates }}`, e.g. `value: "{{ states('input_number.battery_threshold') }}"`.

## Notification rule sets

See [Notification alerts](README.md#-notification-alerts) in the README.

```yaml
rule_sets:
  - id: bypass_to_phones
    name: Bypass notifications
    watch: notifications
    notification_source: [automation.alarm_bypass_watchdog]        # omit = any sender
    notification_destination: [mobile_app, notify.parent_phones]    # omit = anywhere
    groups:                                                         # optional conditions
      - mode: include
        match: all
        rules:
          - { field: notification_text, op: contains, value: bypass }
alerts:
  - rule_set: bypass_to_phones
    theme: notification
    message: "{title}"
```

- Conditions: `notification_text` (title or message), `notification_title`, `notification_message`, `notification_tag`, `notification_sent_to`.
- Message placeholders: `{title}`, `{message}`, `{sent_by}`, `{sent_to}`.
- `merge_duplicates` (default `true`): the same notification sent to several destinations — related contexts (a notify group and its members), or the same title + message + tag within 10 s — is one alert with every destination; `false` = one alert per copy.
- Card option `notifications_retention` (seconds, default `3600`): how long a sent notification stays an alert.

## Feature options

### TTS — card-level options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `tts_enabled` | `boolean` | `true` | Master toggle — set `false` to silence all TTS globally |
| `tts_entity` | `string` | — | Default `media_player.*` speaker entity |
| `tts_engine` | `string` | *(auto)* | TTS engine entity (auto-detected from first `tts.*` state) |
| `tts_notify_service` | `string` | — | Default notify service for Alexa / push |
| `tts_language` | `string` | — | Language code passed to `tts.speak` (e.g. `it-IT`) |

### TTS — per-alert options

| Option | Type | Description |
|--------|------|-------------|
| `tts` | `boolean` | Enable TTS for this alert |
| `tts_entity` | `string` | Override the global speaker for this alert |
| `tts_engine` | `string` | Override the global TTS engine |
| `tts_notify_service` | `string` | Override the global notify service |
| `tts_message` | `string` | Custom spoken text (supports `{name}`, `{state}`, Jinja2) |

### Push notifications — per-alert options

| Option | Type | Description |
|--------|------|-------------|
| `push_notify` | `boolean` | Enable push notification for this alert |
| `push_notify_service` | `string` | `notify.*` service name (e.g. `mobile_app_my_phone`, `notify.telegram`) |
| `push_notify_title` | `string` | Notification title — Jinja2, defaults to badge label |
| `push_notify_message` | `string` | Notification message — Jinja2, defaults to alert message |
| `push_notify_data` | `object` | **New in 1.3.9.9.4** — arbitrary payload passed through to the `notify.*` service under the `data` key. Enables actionable notifications, critical alerts (bypass DND), custom push sounds, attachments, tag/group. String values are template-resolved (see example below). |

### Music player — options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `show_player_controls` | `boolean` | `false` | Enable the graphical player UI (requires `media_player.*` entity) |
| `music_player_color` | `string` | `#e040fb` | Accent color for all player UI elements — any CSS color |
| `music_show_art` | `boolean` | `true` | Show album artwork (background blur + thumbnail) |
| `music_show_title` | `boolean` | `true` | Show track title (with marquee scroll for long titles) |
| `music_show_artist` | `boolean` | `true` | Show artist name |
| `music_show_controls` | `boolean` | `true` | Show previous / play-pause / next / mute buttons and volume slider |
| `music_show_power` | `boolean` | `false` | Add a power icon (bottom-right corner) — calls `media_player.turn_off` |
| `music_show_player_picker` | `boolean` | `false` | Add a cast icon (bottom-right corner) — opens a dropdown to switch the active player for this session |
| `music_compact_layout` | `boolean` | `false` | Compact layout: track title and artist move to the top-right column, controls stay left — ideal for small/narrow displays |

## Feature snippets

YAML for the features described in the README, by section.

### Text-to-Speech Announcements

[← README: Text-to-Speech Announcements](README.md#-text-to-speech-announcements-new-in-122)

```yaml
# Standard HA TTS (media_player + TTS engine)
alerts:
  - entity: binary_sensor.smoke_detector
    state: "on"
    message: "Smoke detected!"
    theme: fire
    tts: true                            # enable TTS for this alert
    tts_entity: media_player.living_room # speaker to use
    # tts_engine: tts.google_en_com      # auto-detected if omitted
```

```yaml
# Alexa Echo (via notify service)
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    message: "Front door open"
    tts: true
    tts_notify_service: alexa_media_echo_dot_kitchen
    tts_message: "Attention — the front door is open"   # optional custom sentence
```

### Mobile Push Notifications

[← README: Mobile Push Notifications](README.md#-mobile-push-notifications-new-in-13)

```yaml
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    theme: door
    message: "Front door open"
    push_notify: true
    push_notify_service: mobile_app_my_phone         # required
    push_notify_title: "🚪 Door Alert"               # optional, Jinja2
    push_notify_message: "Door opened — {state}"     # optional, Jinja2
```

### Actionable & critical push notifications

[← README: Actionable & critical push notifications](README.md#actionable--critical-push-notifications-new-in-13994)

```yaml
- entity: switch.master_ensuite_fan
  state: 'on'
  push_notify: true
  push_notify_service: mobile_app_john
  push_notify_title: '💨 Master en-suite fan'
  push_notify_message: 'Fan left running in {area}'
  push_notify_data:
    push:
      sound:
        name: Bloom.caf
        volume: 1
      interruption-level: time-sensitive   # iOS: bypass focus modes
    actions:
      - action: TURN_OFF_MASTER_ENSUITE_FAN
        title: Turn Off Fan
        destructive: true
      - action: URI
        title: Open Camera
        uri: /lovelace/cameras
    tag: alert_master_ensuite_fan          # replace previous notification with same tag
    group: bathroom                        # Android: notification group
```

```yaml
- alias: 'Turn off master en-suite fan from push action'
  trigger:
    platform: event
    event_type: mobile_app_notification_action_received
    event_data:
      action: TURN_OFF_MASTER_ENSUITE_FAN
  action:
    service: switch.turn_off
    target: { entity_id: switch.master_ensuite_fan }
```

### Music Player Mode

[← README: Music Player Mode](README.md#-music-player-mode-new-in-126)

```yaml
alerts:
  - entity: media_player.spotify_davide
    theme: music
    show_player_controls: true
    music_player_color: "#e040fb"   # optional accent color
```

### Accent color

[← README: Accent color](README.md#accent-color)

```yaml
music_player_color: "#00e5ff"   # cyan
music_player_color: "#69f0ae"   # green
music_player_color: "#ff4081"   # pink
```

### Camera in Overlay Banner & Card Background

[← README: Camera in Overlay Banner & Card Background](README.md#-camera-in-overlay-banner--card-background-snapshot-122--live-stream--card-bg-131)

```yaml
alerts:
  - entity: binary_sensor.front_door_motion
    state: "on"
    message: "Motion at front door"
    theme: intruder
    camera_entity: camera.front_door     # required for all camera features
    overlay_mode: true                   # show overlay banner at card level
    camera_live: true                    # live stream in banner (default: false = snapshot)
    camera_in_card: true                 # camera background in the card slide
```

### Secondary entity value

[← README: Secondary entity value](README.md#secondary-entity-value)

```yaml
- entity: sensor.open_zones
  operator: "!="
  state: "0"
  message: "Zones open"
  secondary_entity: sensor.open_zones_list
  secondary_attribute: zone_names   # optional — read an attribute instead of state
```

### tap_action / hold_action / double_tap_action

[← README: tap_action / hold_action / double_tap_action](README.md#tap_action--hold_action--double_tap_action)

```yaml
- entity: binary_sensor.front_door
  state: "on"
  message: "Front door open"
  tap_action:
    action: more-info
    entity_id: binary_sensor.front_door
  hold_action:
    action: navigate
    navigation_path: /lovelace/security
  double_tap_action:
    action: call-service
    service: lock.lock
    target:
      entity_id: lock.front_door
```

### confirmation — ask before executing

[← README: confirmation — ask before executing](README.md#confirmation--ask-before-executing-new-in-13995)

```yaml
- entity: alarm_control_panel.home
  state: "triggered"
  message: "Disarm alarm"
  tap_action:
    action: call-service
    service: alarm_control_panel.alarm_disarm
    target:
      entity_id: alarm_control_panel.home
    confirmation:
      text: "Are you sure you want to disarm the alarm?"
```

```yaml
confirmation: true
```

```yaml
confirmation:
  text: "Are you sure you want to unlock the door?"
  exemptions:
    - user: "<HA_USER_ID>"   # Devs → Persons → Users → copy the User ID
```

### on_change — trigger on any state change

[← README: on_change — trigger on any state change](README.md#on_change--trigger-on-any-state-change)

```yaml
- entity: media_player.living_room
  on_change: true
  auto_dismiss_after: 15
  message: "Now playing: {state}"
  theme: notification
```

### time_range — restrict to a time window

[← README: time_range — restrict to a time window](README.md#time_range--restrict-to-a-time-window)

```yaml
- entity: binary_sensor.front_door
  state: "on"
  message: "Door open at night!"
  time_range:
    from: "22:00"
    to: "07:00"
  theme: intruder
```

### visible_to — per-alert user filter

[← README: visible_to — per-alert user filter](README.md#visible_to--per-alert-user-filter)

```yaml
- entity: sensor.server_load
  state: "high"
  message: "Server load critical"
  visible_to: admin          # admin | non_admin | "John" | ["John", "Maria"]
```

### device_class — auto-discover by device class

[← README: device_class — auto-discover by device class](README.md#device_class--auto-discover-by-device-class)

```yaml
- device_class: smoke
  state: "on"
  message: "Smoke detected: {name}"
  theme: fire
  priority: 1

- device_class: battery
  attribute: battery_level
  operator: "<="
  state: "15"
  message: "Low battery: {name} ({state}%)"
  theme: battery
  entity_filter_exclude:
    - sensor.battery_test_device
```

### Jinja2 in the state trigger field

[← README: Jinja2 in the state trigger field](README.md#jinja2-in-the-state-trigger-field)

```yaml
- entity: sensor.outdoor_temperature
  operator: ">"
  state: "{{ states('input_number.temp_alert_threshold') }}"
  message: "Temperature too high: {state}°"
```

### All-clear widget (clock / weather / forecast)

[← README: All-clear widget (clock / weather / forecast)](README.md#all-clear-widget-clock--weather--forecast)

```yaml
show_when_clear: true
clear_display_mode: weather_forecast   # see modes below
clear_weather_entity: weather.home
```

### Weather/time as a slide in the alert cycle

[← README: Weather/time as a slide in the alert cycle](README.md#weathertime-as-a-slide-in-the-alert-cycle)

```yaml
show_widget_in_cycle: true
clear_display_mode: weather_clock
clear_weather_entity: weather.home
```

### Overlay / toast notification

[← README: Overlay / toast notification](README.md#overlay--toast-notification)

```yaml
overlay_mode: true
overlay_position: top     # top | center | bottom
overlay_duration: 8       # seconds before auto-dismiss (0 = manual close only)
overlay_scale: 1.5        # 1 | 1.5 | 2 | 3 — enlarge for wall displays
```

### snooze_action

[← README: snooze_action](README.md#snooze_action)

```yaml
- entity: binary_sensor.mailbox
  state: "on"
  message: "Mail arrived"
  snooze_action:
    action: call-service
    service: input_boolean.turn_off
    target:
      entity_id: input_boolean.mailbox_flag
```

### entity_filter

[← README: entity_filter](README.md#entity_filter)

```yaml
- entity_filter: "battery"
  attribute: battery_level
  operator: "<="
  state: "20"
  message: "Low battery: {name} ({state}%)"
  theme: battery
  entity_filter_exclude:
    - sensor.battery_test_device
```

### HA template syntax in messages

[← README: HA template syntax in messages](README.md#ha-template-syntax-in-messages)

```yaml
# Simple sensor value
- entity: sensor.co2_ppm
  operator: ">"
  state: "1000"
  message: "CO₂: {{ states('sensor.co2_ppm') }} ppm"

# Attribute value
- entity: climate.hvac
  state: heating
  message: "Heating — room: {{ state_attr('climate.hvac', 'current_temperature') }}°"

# Conditional logic
- entity: sensor.battery_phone
  operator: "<"
  state: "20"
  message: >
    {% if states('sensor.battery_phone') | int < 10 %}
      Critical: {{ states('sensor.battery_phone') }}%
    {% else %}
      Low battery: {{ states('sensor.battery_phone') }}%
    {% endif %}

# Time / date
- entity: binary_sensor.night_mode
  state: "on"
  message: "Night mode active since {{ now().strftime('%H:%M') }}"

# Math / unit conversion
- entity: sensor.power_consumption
  operator: ">"
  state: "2000"
  message: "High consumption: {{ (states('sensor.power_consumption') | float / 1000) | round(2) }} kW"
```

### Timer themes

[← README: Timer themes](README.md#timer-themes)

```yaml
- entity: timer.ad_blocker_paused
  state: active
  message: "Ad blocking disabled for {timer}"
  theme: countdown
```

### Numeric / comparison conditions

[← README: Numeric / comparison conditions](README.md#numeric--comparison-conditions)

```yaml
- entity: sensor.co2_ppm
  operator: ">"
  state: "1000"
  message: "CO₂ level critical!"
```

### Attribute-based triggers

[← README: Attribute-based triggers](README.md#attribute-based-triggers)

```yaml
- entity: sensor.phone
  attribute: battery_level
  operator: "<"
  state: "20"
  message: "Phone battery critical"
  theme: battery
```

### AND / OR multi-entity conditions

[← README: AND / OR multi-entity conditions](README.md#and--or-multi-entity-conditions)

```yaml
- entity: binary_sensor.front_door
  state: "on"
  conditions_logic: "and"
  conditions:
    - entity: input_boolean.night_mode
      operator: "="
      state: "on"
  message: "Door open at night"
  theme: intruder
```

### Entity picture / custom image as icon

[← README: Entity picture / custom image as icon](README.md#entity-picture--custom-image-as-icon-new-in-1398)

```yaml
alerts:
  - entity: sensor.bin_collection
    state: "on"
    message: 🗑️ Bin day!
    use_entity_picture: true
    icon_size: 2rem   # optional, default 2rem
```

```yaml
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    message: Porta aperta
    icon_image: /local/immagini/porta.png
    icon_size: 3rem
```

### Message placeholders

[← README: Message placeholders](README.md#message-placeholders)

```yaml
- entity: sensor.meter_abe4
  operator: "<="
  state: "20"
  message: "Battery low: {state}%"
  secondary_text: "Device: {device}"
```

### secondary_text

[← README: secondary_text](README.md#secondary_text)

```yaml
secondary_text: "Zone: {name} — Current: {state}"
```

### Badge customization

[← README: Badge customization](README.md#badge-customization)

```yaml
show_badge: false        # hide completely
badge_label: "URGENT"   # or use a custom label
```

### Sound notifications

[← README: Sound notifications](README.md#sound-notifications)

```yaml
- entity: binary_sensor.smoke_detector
  state: "on"
  message: "Smoke detected!"
  sound: true
  sound_url: "https://example.com/alarm.mp3"  # optional custom sound
```

### Large buttons

[← README: Large buttons](README.md#large-buttons)

```yaml
large_buttons: true
```

### Swipe to snooze

[← README: Swipe to snooze](README.md#swipe-to-snooze)

```yaml
swipe_to_snooze: true
```

### Vertical layout

[← README: Vertical layout](README.md#vertical-layout)

```yaml
vertical: true
```

### HA theme adaptation

[← README: HA theme adaptation](README.md#ha-theme-adaptation)

```yaml
ha_theme: true
```

### Severity border

[← README: Severity border](README.md#severity-border)

```yaml
severity_border: false
```

```yaml
your-theme-name:
  atc-severity-border-width: "0px"
```

### Card border

[← README: Card border](README.md#card-border)

```yaml
card_border: true
```

### Test mode

[← README: Test mode](README.md#test-mode)

```yaml
test_mode: true
```

## Examples

### Battery monitor with entity filter

```yaml
type: custom:easy-alert-card
cycle_animation: slide
alerts:
  - entity_filter: "battery"
    attribute: battery_level
    operator: "<="
    state: "20"
    message: "Low battery: {name} ({state}%)"
    theme: battery
    priority: 2
    entity_filter_exclude:
      - sensor.battery_test_device
```

### Phone battery with charging status (`battery3d` theme)

```yaml
type: custom:easy-alert-card
show_when_clear: true
alerts:
  - entity: sensor.iphone_battery_level
    operator: "<="
    state: "100"                    # always active so the widget stays visible
    message: "iPhone"
    theme: battery3d
    charging_entity: binary_sensor.iphone_is_charging   # optional — enables ⚡ lightning + cyan colour while charging
```

The `battery3d` theme colours the CSS battery icon **and** the horizontal progress bar dynamically:

- **≤ 20%** red — low battery
- **21–60%** orange — medium
- **> 60%** green — healthy
- **Charging** cyan with an animated ⚡ inside the icon (overrides the level colour)

Works with any entity that reports a 0–100 numeric state (phones, tablets, laptops, robot vacuums, EVs, IoT sensors, HA Companion battery, etc.).

### Smoke detector with TTS + camera snapshot

```yaml
type: custom:easy-alert-card
overlay_mode: true
overlay_scale: 1.5
tts_entity: media_player.living_room
alerts:
  - entity: binary_sensor.smoke_detector
    state: "on"
    message: "Smoke detected!"
    theme: fire
    priority: 1
    tts: true
    camera_entity: camera.kitchen
```

### Alexa TTS announcement on door open

```yaml
type: custom:easy-alert-card
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    message: "Front door is open"
    theme: door
    tts: true
    tts_notify_service: alexa_media_echo_dot_hallway
    tts_message: "Attention — the front door has been opened"
```

### All smoke detectors via device_class

```yaml
type: custom:easy-alert-card
alerts:
  - device_class: smoke
    state: "on"
    message: "Smoke detected: {name}"
    theme: fire
    priority: 1
    tts: true
    tts_entity: media_player.all_speakers
```

### Dynamic threshold from helper entity

```yaml
type: custom:easy-alert-card
alerts:
  - entity: sensor.outdoor_temperature
    operator: ">"
    state: "{{ states('input_number.temp_alert_threshold') }}"
    message: "Temperature too high: {state}°"
    theme: temperature
```

### Timer with countdown

```yaml
type: custom:easy-alert-card
alerts:
  - entity: timer.ad_blocker_paused
    state: active
    message: "Ad blocking disabled for {timer}"
    theme: countdown
    priority: 2
```

### Alarm with tap_action

```yaml
type: custom:easy-alert-card
alerts:
  - entity: alarm_control_panel.home
    state: "triggered"
    message: "ALARM TRIGGERED"
    priority: 1
    theme: emergency
    tap_action:
      action: call-service
      service: alarm_control_panel.alarm_disarm
      target:
        entity_id: alarm_control_panel.home
      service_data:
        code: "1234"
```

### Smart snooze (resets the sensor)

```yaml
type: custom:easy-alert-card
alerts:
  - entity: binary_sensor.mailbox
    state: "on"
    message: "Mail arrived"
    theme: notification
    snooze_action:
      action: call-service
      service: input_boolean.turn_off
      target:
        entity_id: input_boolean.mailbox_flag
```

### Night-time door alert (AND condition + time_range)

```yaml
type: custom:easy-alert-card
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    time_range:
      from: "22:00"
      to: "07:00"
    message: "Front door open at night!"
    priority: 1
    theme: intruder
    hold_action:
      action: navigate
      navigation_path: /lovelace/security
```

### Alert visible only to admins

```yaml
type: custom:easy-alert-card
alerts:
  - entity: sensor.server_load
    operator: ">"
    state: "90"
    message: "Server CPU at {state}%"
    visible_to: admin
    theme: warning
```

### Push notification on door open

```yaml
type: custom:easy-alert-card
alerts:
  - entity: binary_sensor.front_door
    state: "on"
    message: "Front door open"
    theme: door
    notify_push: true
    notify_push_service: mobile_app_iphone_di_mario
    notify_push_title: "Door Alert"
    notify_push_message: "{name} opened at {{ now().strftime('%H:%M') }}"
```

### Music player with custom accent color

```yaml
type: custom:easy-alert-card
alerts:
  - entity: media_player.spotify_davide
    theme: music
    show_player_controls: true
    music_player_color: "#00e5ff"
    operator: "="
    state: playing
```

### Weather + 7-day forecast alternating

```yaml
type: custom:easy-alert-card
show_when_clear: true
clear_display_mode: weather_forecast
clear_weather_entity: weather.home
clear_weather_style: default
show_widget_in_cycle: true
alerts:
  - entity: binary_sensor.smoke_detector
    state: "on"
    message: "Smoke detected!"
    theme: fire
```

### All-clear with animated weather + widget in cycle

```yaml
type: custom:easy-alert-card
show_when_clear: true
clear_display_mode: weather_clock
clear_weather_entity: weather.home
show_widget_in_cycle: true
alerts:
  - entity: binary_sensor.smoke_detector
    state: "on"
    message: "Smoke detected!"
    theme: fire
```

### Multiple warnings cycling

```yaml
type: custom:easy-alert-card
cycle_interval: 8
cycle_animation: slide
show_when_clear: true
clear_message: "All systems normal"
clear_theme: success
alerts:
  - entity: binary_sensor.smoke_detector
    state: "on"
    message: "Smoke detected in kitchen!"
    priority: 1
    theme: fire
  - entity: binary_sensor.water_leak
    state: "on"
    message: "Water leak under sink"
    priority: 2
    theme: flood
  - entity: sensor.co2_ppm
    operator: ">"
    state: "1000"
    message: "CO₂ level too high — {state} ppm"
    priority: 2
    theme: toxic
  - entity: binary_sensor.window_contact
    state: "on"
    message: "Living room window open"
    priority: 3
    theme: window
    secondary_entity: sensor.outdoor_temperature
```
