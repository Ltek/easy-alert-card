<h1 align="center">Easy Alert Card (Ltek)</h1>

<p align="center">
  <strong>An alert & notification card for Home Assistant dashboards</strong><br>
  64 visual themes and your own custom themes, rule sets, notification alerts, TTS, push notifications, a global overlay banner, media player mode, a weather widget, and a full visual editor. No YAML required.
</p>

<p align="center">
  <a href="https://my.home-assistant.io/redirect/hacs_repository/?owner=Ltek&repository=easy-alert-card&category=plugin"><img src="https://my.home-assistant.io/badges/hacs_repository.svg" alt="Open your Home Assistant instance and open this repository in HACS."></a>
</p>

Current build: **v2026.11.02.2** · full history in [CHANGELOG.md](CHANGELOG.md)

 Migrating from [AlertTicker Card 1.3.17](https://github.com/djdevil/AlertTicker-Card) ... See [Moving from AlertTicker Card](#-moving-from-alertticker-card). 
 
 Huge thank you to djdevil for which my card is based on. its own card type (`custom:easy-alert-card`), so the two can be installed side by side.


---

### ✨ Highlights

- 🎨 **64 visual themes** — from subtle `info` to cinematic 3D, timer countdowns, weather badges, and a full music-player mode with album art
- ⚡ **Trigger on anything** — entity state, attribute, template, device class, entity filter with wildcards, AND/OR logic
- 🧩 **Rule Sets** — reusable, named filters by label, area, floor, device class, integration, state, other entities, time of day and weekday; edit once, every alert using it follows
- 📨 **Notification alerts** — raise an alert when Home Assistant sends a notification: by sender (automation / script), destination (phone, notify group, the 🔔 bell) and text
- 📢 **Notify everywhere** — in-dashboard cycling ticker, **global overlay banner** visible from any view, **TTS** (Alexa / Google / any speaker), **push notifications**, **camera snapshots & live streams**
- 🌍 **12 languages** — IT, EN, FR, DE, NL, VI, RU, DA, CS, PT-BR, ES, TR
- 🎯 **Per-alert control** — themes, time windows, user visibility, snooze, order, actions, group/collapse, `active_state_entity` for HA automations
- 🖼️ **Full visual editor** — configure every option in the GUI, no YAML needed
- 📱 **Mobile-first UX** — swipe to snooze, invisible touch zones, HA Companion push support

---

## 📚 Table of Contents

- [Moving from AlertTicker Card](#-moving-from-alertticker-card)
- [What's new](#-whats-new) — the main improvements, briefly
- [Translators](#translators)
- [Features at a Glance](#features-at-a-glance)
- [Text-to-Speech (TTS) Announcements](#-text-to-speech-announcements-new-in-122) — Alexa, Google Home, HA speakers
- [Mobile Push Notifications](#-mobile-push-notifications-new-in-13)
- [Music Player Mode](#-music-player-mode-new-in-126) — album art, playback controls, vinyl mode
- [Camera in Overlay & Card Background](#-camera-in-overlay-banner--card-background-snapshot-122--live-stream--card-bg-131) — snapshots & live streams
- [Rule Sets](#-rule-sets) — reusable entity filters and conditions
- [Notification alerts](#-notification-alerts) — alerts from Home Assistant notifications
- [Upgrading: filters & conditions become rules](#upgrading-filters--conditions-become-rules)
- [Themes](#themes) — all 64 themes explained
- [How It Works](#how-it-works)
- [Installation](#install-via-hacs) — HACS + manual
- [Visual Editor](#visual-editor)
- [YAML reference](YAML.md) — every option, snippets and real-world examples (separate file)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Languages](#languages) — 12 supported languages

---

## 🚚 Moving from AlertTicker Card

Easy Alert Card reads every AlertTicker Card option, so your existing config works as it is.

1. **Install** Easy Alert Card from HACS (see [Installation](#install-via-hacs)). You can keep AlertTicker Card installed — the two use different card types, storage and events, so they don't interfere.
2. **Switch a card** — either:
   - edit the card's YAML and change `type: custom:easy-alert-card` to `type: custom:easy-alert-card`, or
   - add an Easy Alert Card, open **📥 Import from AlertTicker Card** on its main screen, paste the old card's YAML (the card alone, or a whole view / dashboard that contains it) and click **Import**.
3. **Open the editor once and Save.** It converts the old setup the same way every time: filters and extra conditions become [rule sets](#-rule-sets), priority becomes the list order, and per-alert look settings (icon, colors, badge…) move into [custom themes](#-themes).

Snoozes, dismissed alerts, sticky alerts and history saved in your browser by AlertTicker Card are copied over the first time Easy Alert Card loads; AlertTicker's own data isn't changed. When all your cards are moved, you can remove AlertTicker Card.

---

## 🆕 What's new

What Easy Alert Card adds to AlertTicker Card 1.3.17, briefly — full details in the [CHANGELOG](CHANGELOG.md).

- 🧩 **Rule Sets** — one rule engine for every filter and condition: named, reusable sets of include / exclude rules on entity id, name, domain, device class, integration, area, floor, label, state, attribute, age, another entity, time, weekday, sun and visibility, with a live "can match N entities" list. Old filters and conditions convert automatically.
- 📨 **Notification alerts** — alert on Home Assistant notifications by sender, destination and text; Companion app commands are ignored and `clear_notification` clears the alert.
- 🎨 **Themes page & custom themes** — built-in themes are templates; duplicate one to set its icon, text size and color, severity label, pulse / flash effects, colors and layout. Every alert using it looks the same, and the preview matches the live card.
- 📚 **Alert Presets** — ready-made alerts by domain or device class (batteries, doors, leaks, all notifications…), with match counts, a 🔍 preview, and editable associations on any theme.
- ⚙️ **Reorganized editor** — full-width page tiles (Alerts, Rule Sets, Themes, Global Defaults, History, Overlay, All Clear), collapsible sections, checkboxes instead of toggles, drag to reorder, duplicate / enable / disable alerts, and a 💾 **Save** that keeps the editor open.
- ↕ **Order replaces priority** — the list order decides which alert shows first; **Show in overlay** is per alert.
- 📋 **History** — keep up to 5000 alerts or 5 days; choose separately what the card's 📋 panel shows.
- 🌊 **New `water` theme**, **pulse** and **background flash** for any theme.
- 🧪 **Safer test mode & previews** — they only apply while the editor is open, so nothing leaks onto the live dashboard.
- ⚡ **Faster** — card updates take about 40% less time.
- 📥 **Import from AlertTicker Card** and automatic carry-over of its saved state.
- 📄 **YAML reference** in its own file, [YAML.md](YAML.md).


---

## Features at a Glance

| Feature | Details |
|---------|---------|
| **Themes** | **64** visual themes in 6 categories (including 4 timer themes and the 3D spectacular themes), plus your own **custom themes** |
| **Animations** | **12** selectable transition animations between alerts |
| **Per-alert theme** | Each alert picks a theme — built-in or your own custom theme, where all look settings live |
| **Multiple entities** | Unlimited alerts per card |
| **Order** | The list order decides which active alert shows first — drag to reorder (replaces the old 4-level priority) |
| **tap / hold / double-tap** | Standard Lovelace card interactions per alert |
| **Attribute triggers** | Trigger on any entity attribute (e.g. `battery_level`) |
| **AND / OR conditions** | Multiple entities must match (all or at least one) |
| **Numeric conditions** | Trigger on `>`, `<`, `>=`, `<=`, `!=` for sensor values |
| **on_change** | Trigger on any state change regardless of condition — with optional auto-dismiss |
| **time_range** | Restrict any alert to a specific time window (e.g. 22:00–07:00, midnight crossing supported) |
| **visible_to** | Restrict alert visibility to specific HA users (`admin`, `non_admin`, or by display name) |
| **secondary_entity** | Live entity value shown below the message |
| **Jinja2 templates** | Full HA template syntax in messages — rendered server-side with live updates |
| **Jinja2 in `state`** | Trigger threshold driven by a helper entity via `{{ states(...) }}` template |
| **entity_filter** | Text filter — one alert per matched entity, with exclude list and wildcard `*` support |
| **device_class** | Auto-discover all entities with a given HA device class (e.g. `smoke`, `battery`, `motion`) |
| **Auto-icon** | Automatically uses the entity's HA icon when no icon is set |
| **Custom icon namespaces** | Any icon namespace works: `mdi:`, `hass:`, `hue:`, `phu:`, `cil:` and more |
| **Alert navigation** | ◀ ▶ buttons + left/right swipe to jump between active alerts |
| **Snooze** | Suspend any alert — fixed duration or menu — persisted in localStorage |
| **snooze_action** | Execute a Lovelace action when the 💤 button is tapped |
| **Alert history** | 📋 button flips the card to a timestamped event log |
| **Timer themes** | 4 animated themes for `timer.*` entities with live countdown |
| **HA icons** | Use any `mdi:` icon per alert via native icon picker |
| **Entity picture / custom image** | Use the entity's `entity_picture` attribute or a static `/local/` path as the alert icon |
| **Sound notifications** | Per-alert audio — auto-generated tones or custom URL |
| **🔊 TTS announcements** | Read alerts aloud via HA TTS, Alexa, or any notify service. Multilingual fallback messages auto-generated from alert theme (12 languages) |
| **📱 Push notifications** | Send a push notification to any `notify.*` service when an alert fires. Full Jinja2 support for title and message. Global master toggle. |
| **📷 Camera snapshot** | Attach a live camera frame to the overlay banner, scaled proportionally with overlay zoom |
| **📹 Camera live stream** | **NEW** — `camera_live: true` shows a live HLS/WebRTC stream in the overlay banner instead of a static snapshot |
| **🖼️ Camera card background** | **NEW** — `camera_in_card: true` uses the camera image as a full-bleed background layer behind any alert card slide |
| **Overlay scale** | Enlarge the overlay banner up to 3× for wall-mounted displays |
| **🎵 Music player mode** | **NEW** — `media_player` entity shown as a cinematic player card with album art, equalizer, and controls |
| **🌤 7-day forecast widget** | **NEW** — full forecast grid or alternating weather+forecast display mode |
| **Weather/time in cycle** | Insert the clock/weather widget as a slide in the alert rotation |
| **Large buttons** | Always-visible pill-shaped 💤 and 📋 buttons |
| **Persistent alerts** | `persistent: true` — alert stays visible after sensor clears, requires manual ✕ dismiss |
| **Swipe to snooze** | Swipe left on the card to snooze (or dismiss if `persistent: true`) — no conflict with `tap_action` |
| **Invisible touch zone** | Right-side tap zone shows action buttons on mobile without interfering with `tap_action` |
| **Vertical layout** | Stack icon on top, message below, centered — all themes |
| **HA theme adaptation** | `ha_theme: true` adapts colors to any active HA global theme |
| **Overlay notification** | Global floating banner — fires from any dashboard view, with top / center / bottom position and auto-dismiss |
| **Clear widget** | Animated clock or weather display (condition + temp + wind + humidity) when no alerts are active |
| **6 new clear styles** | Clock: `aurora`, `gold`, `matrix` — Weather badge: `stage`, `split`, `cinematic` |
| **Card border** | Toggle to show the standard HA border around the card — always visible, off by default |
| **Test mode** | Force-preview all alerts while the editor is open, regardless of conditions (the live card ignores it) |
| **Visual editor** | Full GUI — no YAML required |
| **Languages** | Italian, English, French, German, Dutch, Vietnamese, Russian, Danish, Czech, Portuguese (pt-BR), Spanish, Turkish — **12 languages** |
| **🔗 active_state_entity** | Per-alert option — write `on`/`off` to any `input_boolean` when that specific alert becomes active or clears. Each alert can target a different boolean, wiring them to independent HA automations (lamp, script, push notification…) |
| **Performance** | Signature-based dirty check — no unnecessary re-renders |

---

## 🔊 Text-to-Speech Announcements *(new in 1.2.2)*

Make Home Assistant read your alerts aloud the moment they trigger — on any speaker, Alexa Echo device, or Google Home.

> ⚠️ **Client-side limitation:** TTS is fired by the card itself, which runs in the browser. It works **only while at least one browser tab has Home Assistant open** (desktop, wall tablet, or the HA Companion app running in the foreground). For 24/7 unattended TTS announcements on critical events, use a **server-side HA automation** with the same `notify.alexa_media_*` / `tts.speak` service call.

> 📄 YAML: [Text-to-Speech Announcements](YAML.md#text-to-speech-announcements)

### How it works

- Enable `tts: true` on any individual alert.
- If no `tts_message` is set, the card **auto-generates a natural sentence** from a built-in dictionary in 10 languages, based on the alert's theme category. For example, a `critical` theme in Italian produces *"Allarme critico: Sensore fumo cucina"*.
- The spoken language is read from `hass.language` and falls back to English automatically.
- Set a global **master toggle** (`tts_enabled: false`) in Global Defaults → Voice & Push to disable all TTS at once without losing per-alert settings.

### TTS service options

| Method | When to use | Config |
|--------|-------------|--------|
| **Standard TTS** | HA media players, Sonos, Chromecast | `tts_entity` (speaker) + optional `tts_engine` |
| **notify service** | Alexa, Google Home via notify, mobile push | `tts_notify_service` (any `notify.*` service) |

Per-alert fields override global card-level defaults, so you can have one speaker for most alerts and a different one for critical alerts.

## 📱 Mobile Push Notifications *(new in 1.3)*

Send a push notification to any Home Assistant `notify.*` service the moment an alert fires — works with the HA Companion App, Telegram, Pushover, and any other notify integration.

> ⚠️ **Client-side limitation:** push notifications are fired by the card, which runs in the browser. They work **only while at least one browser tab has Home Assistant open** (desktop, wall tablet, or the HA Companion app running in the foreground). If nobody is looking at HA at 3 am, no push will be sent even if a sensor triggers. For 24/7 critical alerts (smoke, security, water leak, …), always create a **server-side HA automation** that calls the same `notify.*` service — the card push is best used as a convenience layer on top.

> 📄 YAML: [Mobile Push Notifications](YAML.md#mobile-push-notifications)

### How it works

- Enable `push_notify: true` on any individual alert.
- If no `push_notify_title` is set, the card uses the alert's **badge label** (or `name` if set).
- If no `push_notify_message` is set, the card uses the alert's **display message** (same text shown in the ticker).
- Both fields support `{state}`, `{name}`, `{entity}`, `{device}` placeholders and full Jinja2 templates.
- Set a global **master toggle** (`push_notify_enabled: false`) in Global Defaults → Voice & Push to disable all push notifications at once without touching individual alerts.

### Actionable & critical push notifications *(new in 1.3.9.9.4)*

Use `push_notify_data` to unlock every feature the HA Companion apps and other notify integrations support:

> 📄 YAML: [Actionable & critical push notifications](YAML.md#actionable--critical-push-notifications)

String values inside `push_notify_data` are template-resolved by the card's usual renderer, so `{state}`, `{name}`, `{area}`, `{trigger_state}` and full Jinja2 `{{ ... }}` work inside actions/titles/URIs.

Handle the `action` returned by the user in a server-side automation:

---

## 🎵 Music Player Mode *(new in 1.2.6)*

Turn any `media_player.*` entity into a full graphical player card. When `show_player_controls: true` is set and the entity is a media player, the `music` theme renders a cinematic player UI instead of the default floating notes.

> 📄 YAML: [Music Player Mode](YAML.md#music-player-mode)

### What the player shows

| Element | Description |
|---------|-------------|
| **Album art background** | Blurred, saturated backdrop pulled from `entity_picture` |
| **Spinning vinyl** | Circular album art thumbnail on the right — spins while playing, stops on pause |
| **Equalizer bars** | 3 animated bars pulse next to "NOW PLAYING" when playing; ◼ pause dot when paused |
| **Track info** | `media_title` as title, `media_artist` below |
| **Playback controls** | ⏮ previous · ⏸/▶ play-pause · ⏭ next |
| **Mute toggle** | 🔇/🔊 — highlights in accent color when muted |
| **Volume slider** | Live range slider — gradient fills to current level, updates in real time while dragging |
| **Accent line** | Animated gradient line at the bottom, pulses in the accent color |

### Accent color

All colors in the player UI (buttons, glow, equalizer, vinyl ring, accent line) are driven by a single **`--mu-accent` CSS custom property**, set from `music_player_color`. Change it from the editor's color picker to instantly retheme the entire player:

> 📄 YAML: [Accent color](YAML.md#accent-color)

### Auto-setup in the editor

Selecting a `media_player.*` entity in the visual editor automatically:
- Sets theme to `music`
- Enables `show_player_controls`
- Sets `state: playing` and `operator: =`

Switching back to a non-media-player entity reverts to `emergency`.

## 📷 Camera in Overlay Banner & Card Background *(snapshot: 1.2.2 · live stream + card bg: 1.3.1)*

Attach a **camera image** to an alert — either as a snapshot in the overlay banner, a live stream in the banner, or a background layer behind the alert card slide.

> 📄 YAML: [Camera in Overlay Banner & Card Background](YAML.md#camera-in-overlay-banner--card-background)

| Option | Description |
|--------|-------------|
| `camera_entity` | Camera entity whose image is used |
| `camera_live` | `true` = live HLS/WebRTC stream in the overlay banner; `false` (default) = static snapshot |
| `camera_in_card` | `true` = camera image shown as a background layer behind the alert card slide on every rotation |

- The snapshot/stream appears **below the alert header row** inside the overlay toast. Its height scales proportionally with `overlay_scale`.
- `camera_in_card` uses the entity's `entity_picture` attribute as a CSS background image, visible across the full card behind a semi-transparent overlay. Works with all themes.
- If a snapshot fails to load, the image is silently removed and the banner stays intact.
- `camera_live` requires a camera entity with HLS or WebRTC stream support. Falls back to static snapshot when the `<ha-camera-stream>` component is not yet loaded.

---

## 🧩 Rule Sets

A **rule set** is a named, reusable filter. Define it once in the editor's **🧩 Rule Sets** section (or under `rule_sets:` in YAML) and use it in any number of alerts: an alert that uses a rule set shows once for every entity that matches. Edit the set and every alert using it follows.

> 📄 YAML: [Rule Sets](YAML.md#rule-sets)

An entity matches when **all its include rules** hold and **no exclude rule** does. Each `groups:` entry is a list of rules that are either included or excluded, matching **all** or **any** of them. A set with no include rule matches nothing — never "every entity in Home Assistant".

Any rule can be switched off with `enabled: false` (the eye icon in the editor) — it's ignored without deleting it.

In the editor, **Can match N entities · M active now** sits under every set's ID: every entity the set can cover, whatever its state right now (a green state = matching now). **Exclude** leaves an entity out, **Include** brings it back. **Export** (on the set's row) gives the set as JSON with how many entities each rule matches on its own — handy for troubleshooting. **+ Create alert from this rule set** adds an alert that uses it, and *Alerts using this rule set* links to each one.

**Single-entity alerts** have a **Condition** section: *When this entity…* (an operator + value, or *changes (any value)*), *…and also* optional rules on the alert itself — the same rule editor, with *Another entity*, *Time of day*, *Day of week*, *Sun* and *Unchanged for*:

---

## 📨 Notification alerts

A **notification rule set** (`watch: notifications`) raises an alert for each Home Assistant notification that matches — mobile app pushes, persistent notifications (the 🔔 bell) and any other notify service.

> 📄 YAML: [Notification alerts](YAML.md#notification-rule-sets)

- **Notification Source** — which automation or script sent it, traced through Home Assistant's context ids (a script called by an automation counts for both). Notifications from no automation (integrations, Developer Tools) match only *any sender*.
- **Notification Destination** — `mobile_app` (any phone), `persistent` (the bell), a phone (`notify.mobile_app_pixel_7` or its notify entity), a notify service or group (`notify.parent_phones`), or a notify entity. A phone also matches notifications sent to a group it belongs to; a group send counts as **one** notification.
- **Conditions** — `notification_text` (title or message), `notification_title`, `notification_message`, `notification_tag`, `notification_sent_to`.
- **Message placeholders** — `{title}`, `{message}`, `{sent_by}`, `{sent_to}`. Notification text is shown as written, never run as a template.
- **Tap** dismisses the notification (a persistent one is dismissed in Home Assistant). In **test mode** an alert with nothing matching shows a sample notification.
- In the editor: **Scan automations for notifications** lists which automations and scripts send them (read-only, adapted from [Notification Manager Card](https://github.com/Ltek/notification-manager-card)); **Recent notifications** lists what arrived, with **Use** to build a rule from one.

- **One alert per notification.** The same notification sent to several destinations — by one automation, through a notify group, or by separate automations within 10 seconds with the same title, message and tag — is one alert listing every destination (`{sent_to}`). Dismissing it clears every copy. Untick *One alert per notification* on the rule set (`merge_duplicates: false`) for one alert per copy.
- **Companion app commands are ignored.** Messages like `clear_notification`, `remove_channel`, `request_location_update`, `clear_badge`, `update_complications`, `TTS` and `command_*` control the phone and show nothing, so they never become alerts. `clear_notification` with a `tag` also clears the matching notification's alert, and a new notification with a tag already shown replaces the old one — the same as on the phone.

> ⚠️ Like TTS and push, this runs in the browser: only notifications that arrive while a dashboard is open are seen. Who sent a notification, and notifications other than the bell, are visible to **admin users only** — Home Assistant restricts those events. A sent notification has no "dismissed" event, so its alert is kept for `notifications_retention` seconds (default 3600).

---

## Upgrading: filters & conditions become rules

Alerts written with `entity_filter`, `device_class`, `label_filter`, `area_filter`, `entity_filter_exclude`, `conditions` / `conditions_logic` or `time_range` **keep working unchanged**. When you open such a card in the visual editor, it converts them — the card shows exactly the same alerts — and saves the result on your next save:

- multi-entity alerts → a shared rule set (their filters, own condition, extra conditions and time range; identical ones share one set)
- single-entity alerts → their extra conditions and time range become inline rules

`trigger_delay`, `on_change`, `visible_to` and all display and action options stay on the alert. The sections below that describe the old fields still apply to YAML.

**Priority → order.** The editor also replaces the 1–4 `priority` with the list order: alerts are listed in the order they showed on the card, and `overlay_min_priority` becomes the per-alert **Show in overlay** switch (`overlay: false`) on the alerts it used to filter out. The card shows the same order as before; the overlay now follows the same order as the card.

---

## Themes

### 🚨 Critical

| Theme | Icon | Visual style |
|-------|------|-------------|
| `emergency` | 🚨 | Dark red card with pulsing red glow and flashing siren icon |
| `fire` | 🔥 | Deep orange card with flame flicker animation |
| `alarm` | 🔴 | Black card with rapid red strobe effect |
| `lightning` | 🌩️ | Dark purple card with electric glow and lightning flash |
| `nuclear` | ☢️ | Dark amber card with slowly rotating radiation symbol and radial glow pulse |
| `flood` | 🌊 | Deep blue card with animated horizontal water waves |
| `water` | 🌊 | Flood's colors with a fluid water level: two wave layers moving in opposite directions, a gentle swell and rising bubbles. With a `%` entity (e.g. a tank level) the water fills to its value; otherwise about half. Look inspired by [lovelace-fluid-level-background-card](https://github.com/swingerman/lovelace-fluid-level-background-card) (MIT), redrawn in CSS |
| `motion` | 👁️ | Dark green night-vision infrared scan effect |
| `intruder` | 🚷 | Black card with red siren flash and rotating warning icon |
| `toxic` | ☠️ | Black/green card with rising poison bubbles |
| `portal` | 🌀 | 3D spinning crimson vortex |
| `void` | ⚫ | 3D black hole |

### ⚠️ Warning

| Theme | Icon | Visual style |
|-------|------|-------------|
| `warning` | ⚠️ | Dark amber card with orange left border and pulsing dot |
| `caution` | 🟡 | Black/yellow card with diagonal stripe bar and blinking dot |
| `radar` | 🎯 | Dark green card with circular sonar display, sweeping cone and concentric rings |
| `temperature` | 🌡️ | Dark orange card with shaking thermometer and animated fill bar |
| `battery` | 🔋 | Dark card with blinking battery drain animation |
| `battery3d` | 🔋 | **New in 1.3.9.9.6** — CSS battery icon that fills based on the entity value, horizontal progress bar, dynamic colour (green > 60% / orange 21–60% / red ≤ 20%). Optional `charging_entity` shows ⚡ lightning bolt and switches to cyan while charging |
| `door` | 🚪 | Dark card with animated `mdi:door-open` icon that pivots on its hinge (CSS perspective rotateY) |
| `window` | 🪟 | Dark card with `mdi:window-open-variant` swinging on a top-pivot (rotateX) |
| `smoke` | 🌫️ | Dark grey card with drifting smoke puff animation |
| `wind` | 💨 | Dark card with fast horizontal streak lines |
| `leak` | 💧 | Dark blue card with animated drip effect |
| `nebula` | 🌌 | 3D gas clouds |
| `volt` | ⚡ | Electric discharge |
| `storm` | ⛈️ | Lightning storm |

### ℹ️ Info

| Theme | Icon | Visual style |
|-------|------|-------------|
| `info` | ℹ️ | Dark blue card with blue left border and circular icon wrap |
| `notification` | 🔔 | Deep navy card with blue app-icon bubble and pulsing red badge |
| `aurora` | 🌌 | Dark card with shifting aurora gradient background |
| `hologram` | 🔷 | Holographic card with grid lines, horizontal scan beam and glitch flicker |
| `presence` | 🏠 | Dark cyan card with expanding ping rings radiating from icon |
| `update` | 🔄 | Dark card with spinning double progress ring |
| `cloud` | ☁️ | Soft floating cloud pulse |
| `satellite` | 📡 | Radiating signal waves |
| `tips` | 💡 | Amber lightbulb glow |
| `light` | 🔆 | Warm incandescent glow with conical light beam fanning out from icon; bulb flares on pulse |
| `music` | 🎵 | Dark purple/magenta card with musical notes (♪ ♫ ♩ ♬) floating upward and pulsing icon glow |
| `arcade` | 🕹️ | 3D Tron grid |
| `prism` | 💎 | Prismatic spectrum |
| `frost` | ❄️ | Snow & frost |

### ✅ OK / All Clear

| Theme | Icon | Visual style |
|-------|------|-------------|
| `success` | ✅ | Dark green card with green left border |
| `check` | 🟢 | Dark green card with pulsing ring around icon |
| `confetti` | 🎉 | Dark green card with floating coloured particles |
| `heartbeat` | 💓 | Dark card with scrolling ECG line at the bottom and beating pulse ring |
| `shield` | 🛡️ | Dark teal card with rotating scan wave and glow pulse |
| `power` | ⚡ | Dark green card with energy surge lines and lightning zap |
| `sunrise` | 🌅 | Warm golden rising light |
| `plant` | 🌱 | Green growing pulse |
| `lock` | 🔒 | Deep blue secure pulse |
| `diamond` | 💠 | Crystal shimmer |
| `quantum` | ⚛️ | 3D atomic orbitals |

### 🎨 Style

| Theme | Icon | Visual style |
|-------|------|-------------|
| `ticker` | 📰 | Full-width scrolling news ticker bar with all active alerts |
| `neon` | ⚡ | Cyberpunk black card with cyan/magenta glow and scanning line |
| `glass` | 🔮 | Glassmorphism card with purple/pink gradient and frosted border |
| `matrix` | 💻 | Terminal-style green-on-black monospace card with blinking cursor |
| `minimal` | 📋 | Clean light card with dynamic accent left border |
| `retro` | 📺 | CRT amber phosphor card with scanlines, screen flicker and warm glow |
| `cyberpunk` | 🤖 | Neon purple/cyan diagonal stripes with glitch bar |
| `vapor` | 🌸 | Vaporwave perspective grid with pink/cyan gradient |
| `lava` | 🌋 | Black card with floating orange lava blobs |

### ⏱️ Timer *(available for `timer.*` entities and sensors with `device_class: timestamp`)*

| Theme | Icon | Visual style |
|-------|------|-------------|
| `countdown` | ⏱️ | Horizontal progress bar at the bottom that shrinks as time passes. Pulses red when < 20% remaining. |
| `hourglass` | ⏳ | Background vertical fill that drains from top to bottom, like sand in an hourglass. |
| `timer_pulse` | 💥 | Card glows with a pulsing halo — pulse speed increases as time runs out. |
| `timer_ring` | 🔵 | SVG circular ring on the right side with the countdown in the center. |

All timer themes transition green → orange → red as the remaining time decreases. When using a `device_class: timestamp` sensor (e.g. an Alexa/Echo timer sensor), the progress bar is hidden since no total duration is known — the countdown still shows.

> **Note:** The `clear_theme` accepts any theme from the ✅ OK category: `success`, `check`, `confetti`, `heartbeat`, `shield`, `power`, `sunrise`, `plant`, `lock`.

---

## How It Works

### Alert lifecycle

1. Configure one or more **alerts**, each linked to an entity + condition
2. When an entity matches the condition (and any extra `conditions` rules), the alert becomes **active**
3. Active alerts are shown **in list order** (drag to reorder in the editor)
4. The card **displays** the current alert and **auto-cycles** through multiple active alerts
5. Use ◀ / ▶ buttons (or swipe) to jump between alerts manually
6. **Tap** or **hold** the card to execute configured actions
7. **Snooze** any alert with 💤 — one tap for fixed duration, or choose from the menu
8. **📋** opens the alert history with timestamps
9. When no alerts are active and `show_when_clear: true`, the card shows the **all-clear state** (message, clock, or weather)

### Transition animations

When multiple alerts are active, the card cycles using the selected animation:

| Animation | Description |
|-----------|-------------|
| `fold` *(default)* | 3D page-turn along the X axis |
| `slide` | Horizontal push left/right |
| `fade` | Cross-dissolve opacity fade |
| `flip` | RotateY card flip |
| `zoom` | Scale punch in/out |
| `glitch` | Clip-path jitter digital noise |
| `bounce` | Elastic spring from below |
| `swing` | RotateZ pendulum |
| `blur` | Gaussian dissolve |
| `split` | Vertical split (top up, bottom down) |
| `roll` | RotateY + translateX combined roll |
| `curtain` | Opens from center (theater curtain) |

### Manual alert navigation

When 2 or more alerts are active, **◀** and **▶** buttons appear on the left/right edges on hover (first touch on mobile). Clicking jumps to the previous/next alert and resets the auto-cycle timer. On mobile, **left/right swipe** also navigates (if `swipe_to_snooze` is enabled, left-swipe keeps its snooze behaviour and only right-swipe navigates).

### Secondary entity value

Display a live entity value as a second line below the alert message:

> 📄 YAML: [Secondary entity value](YAML.md#secondary-entity-value)

### tap_action / hold_action / double_tap_action

Standard Lovelace interactions — tap, hold (500 ms), or double-tap the whole card to trigger any action:

> 📄 YAML: [tap_action / hold_action / double_tap_action](YAML.md#tap_action--hold_action--double_tap_action)

> When `double_tap_action` is set, a single tap waits 300 ms to distinguish the two gestures.

Supported action types: `call-service`, `navigate`, `more-info`, `url`, `none`.

#### `confirmation` — ask before executing *(new in 1.3.9.9.5)*

Any of the action fields (`tap_action`, `hold_action`, `double_tap_action`, `snooze_action`, and the card-level `clear_*_action`) now support the HA-native `confirmation` field. When set, a confirmation dialog appears before the action fires — perfect for destructive operations:

> 📄 YAML: [confirmation — ask before executing](YAML.md#confirmation--ask-before-executing)

**Short form** — reuse the default text:

**Full form** with per-user exemptions:

Any user listed under `exemptions` skips the prompt — useful when you want the owner to bypass while guests must confirm.

Fully editable in the visual editor: every action section now has an **Ask for confirmation** toggle with an optional custom message field.

### on_change — trigger on any state change

Fire an alert whenever an entity changes state, regardless of the `operator`/`state` condition. The alert stays visible until the next state change, or auto-dismisses after `auto_dismiss_after` seconds:

> 📄 YAML: [on_change — trigger on any state change](YAML.md#on_change--trigger-on-any-state-change)

### time_range — restrict to a time window

> 🧩 Still supported in YAML. The visual editor stores this as a [rule set](#-rule-sets).

Show an alert only within a specific time window. Supports midnight crossing:

> 📄 YAML: [time_range — restrict to a time window](YAML.md#time_range--restrict-to-a-time-window)

The card re-evaluates at each minute boundary so alerts appear and disappear on time without any entity state change. Leave both fields empty for always-active.

### visible_to — per-alert user filter

Restrict an alert to specific Home Assistant users without separate cards or conditional wrappers:

> 📄 YAML: [visible_to — per-alert user filter](YAML.md#visible_to--per-alert-user-filter)

| Value | Effect |
|-------|--------|
| `admin` | Admins only |
| `non_admin` | Non-admin users only |
| `"Display Name"` | Single user by display name |
| `["Name1", "Name2"]` | Multiple users by display name |
| *(omit)* | Shown to everyone |

### device_class — auto-discover by device class

> 🧩 Still supported in YAML. The visual editor stores this as a [rule set](#-rule-sets).

Instead of listing individual entities or writing a text filter, specify a HA device class. The card auto-discovers every entity with that class and creates one alert per match:

> 📄 YAML: [device_class — auto-discover by device class](YAML.md#device_class--auto-discover-by-device-class)

Supports the same `include`/`exclude` panel as `entity_filter` and all the same message placeholders (`{name}`, `{state}`, `{entity}`, `{device}`).

### Jinja2 in the `state` trigger field

The trigger threshold itself can be a Jinja2 template — useful when the threshold is stored in a helper entity:

> 📄 YAML: [Jinja2 in the state trigger field](YAML.md#jinja2-in-the-state-trigger-field)

Any HA template that evaluates to a string or number works here.

### All-clear widget (clock / weather / forecast)

When `show_when_clear: true` is set and no alerts are active, the card can show an animated clock, live weather display, or 7-day forecast instead of a plain text message:

> 📄 YAML: [All-clear widget (clock / weather / forecast)](YAML.md#all-clear-widget-clock--weather--forecast)

| Mode | Display |
|------|---------|
| `message` | Standard all-clear text message (default) |
| `clock` | Animated digital clock with date, deep navy background and blue glow |
| `weather` | Animated weather background with condition, temperature, wind speed, humidity |
| `weather_clock` | Weather background + clock badge in top-right corner |
| `forecast` | **NEW** — full 7-day forecast grid: emoji, high/low temp, precipitation bars, today highlighted |
| `weather_forecast` | **NEW** — alternates every 5 s between current weather + clock and 7-day forecast |

Weather modes show full animated particle backgrounds (sun rays, stars/moon/aurora, floating clouds, fog, wind streaks, rain, snow, hail, lightning, exceptional). All weather info and the clock are rendered as frosted-glass corner badges so the animated sky stays fully visible.

#### 🗓️ 7-day forecast widget

The `forecast` and `weather_forecast` modes display a full-width daily forecast grid sourced from HA's `weather/subscribe_forecast` WebSocket API (HA 2023.9+):

- **Weather emoji** and condition label for each day
- **High / low temperatures** color-coded: blue (cold) → amber (warm) → red (hot)
- **Precipitation probability bar** visible when ≥20%
- **Today's column** elevated with frosted glass, floating emoji animation, and accent glow
- Day labels auto-localized via `Intl.DateTimeFormat` in all 11 supported languages

When used with `show_widget_in_cycle: true`, the card ensures **both** the weather panel and forecast panel have been shown before advancing to the next alert.

#### Clock styles (`clear_display_mode: clock`)

| Style | Visual |
|-------|--------|
| *(default)* | Deep navy background, blue glow digits |
| `aurora` | Animated northern-lights gradient background, green glow |
| `gold` | Warm golden hue, thin weight digits |
| `matrix` | Black background, monospace green digits with scanline glow |

#### Weather badge styles (all weather modes)

| Style | Layout |
|-------|--------|
| *(default)* | Animated sky, frosted corner badges |
| `stage` | Large centered clock on top; weather compacted into a single horizontal frosted pill below |
| `split` | Card divided into two equal full-height panels — left: weather icon + temperature, right: clock |
| `cinematic` | Animated weather background fills the entire card; all info condensed into a transparent caption bar pinned to the bottom |
| `wallpanel` | Default layout with larger weather typography for wall-mounted displays; hides high/low temperatures and wind and focuses on temperature + humidity |

> The `split` style works with all weather modes including `weather_forecast` — the first panel shows weather + clock side by side, then alternates with the 7-day forecast.

Configure these in the editor (All Clear tab). Use `clear_clock_show_date` to toggle the date display, and `clear_clock_date_position` (`above` / `below`) to choose its position relative to the time.

### Weather/time as a slide in the alert cycle

Insert the configured clear widget (clock / weather / weather+clock) as an extra slide in the alert rotation — displayed between alerts like any other:

> 📄 YAML: [Weather/time as a slide in the alert cycle](YAML.md#weathertime-as-a-slide-in-the-alert-cycle)

The widget uses the same `cycle_animation` and `cycle_interval` as alerts. Enable this in the editor (Cycling & Animation section), visible only when `clear_display_mode` is already configured.

### Overlay / toast notification

Enable a global floating banner that fires when a new alert triggers — **visible from any dashboard view**, not just the one where the card lives:

> 📄 YAML: [Overlay / toast notification](YAML.md#overlay--toast-notification)

How it works:
- When the card's view is **currently visible**, the banner is suppressed (no redundant notification — the card itself already shows the alert).
- When you navigate away to another view (or the card is off-screen), an independent watcher reads entity states from the always-present `<home-assistant>` element every 2 seconds and fires the banner automatically.
- A 10-second deduplication window prevents the same alert from firing twice.
- The banner is styled according to the alert category (Critical / Warning / Info / OK / Style / Timer) and dismisses automatically after `overlay_duration` seconds, or manually via the × button.

#### Overlay scale

Use `overlay_scale` to enlarge the entire banner for wall-mounted tablets or TVs:

| Value | Effect |
|-------|--------|
| `1` | Default size |
| `1.5` | 50% larger — font, icon, padding, border-radius all scale |
| `2` | Double size — ideal for wall tablets |
| `3` | Triple size — for TV or kiosk displays |

The max-width grows with the scale while staying within the viewport. Camera snapshot images (if set) also scale proportionally.

Position options:
| Value | Behavior |
|-------|----------|
| `top` | Slides in from the top of the screen |
| `center` | Pops in at the center of the screen (scale animation) |
| `bottom` | Slides in from the bottom of the screen |

### Snooze

Tap 💤 on any active alert to snooze it. Two modes (configurable in Global Defaults → Snooze):

- **Menu** *(default)* — choose 1h / 4h / 8h / 24h from a menu on the card
- **Fixed duration** — configure 30min / 1h / 4h / 8h / 24h for immediate one-tap snooze

Snoozed alerts persist in `localStorage` and the card restores them automatically when the duration expires. A small amber 💤 pill appears when some alerts are snoozed while others remain active — tap it to resume all.

#### 🔄 Cross-device sync *(new in 1.3.9.9.5)*

If you have multiple browser tabs / wall panels / mobile devices all showing the same alert, snoozing, dismissing, or clearing a persistent alert on **one** device now propagates to **all the others in real time**. No configuration required — the card uses Home Assistant's WebSocket event bus (`alertticker_sync` events) to broadcast state changes. Each card instance ignores its own broadcasts via a per-tab device ID, so there are no loops.

Works for all state transitions:
- Snooze / unsnooze
- Dismiss / reset all dismissed
- Persistent alert dismiss

**Note:** Because the sync uses live events, a device that was offline (browser closed) when a snooze happened won't automatically catch up when it comes back online. In that case its local storage still holds the last-known state until the next sync event or the alert re-triggers.

**Requires admin user (since 1.3.9.9.6):** Home Assistant restricts custom-event WebSocket subscriptions to admin/owner accounts only. For **non-admin** users the card silently skips subscribing (no HA log noise, no errors) and falls back to local-only snooze/dismiss — exactly like pre-1.3.9.9.5. If you want cross-device sync to work for a specific user, that user needs the admin role in Home Assistant.

### snooze_action

Execute a Lovelace action when the 💤 button is tapped, in addition to snoozing. Useful for resetting sensors:

> 📄 YAML: [snooze_action](YAML.md#snooze_action)

### Alert history

Tap 📋 to flip the card and view a timestamped log of every alert that became active. Includes a Clear button. History is stored in `localStorage` (configurable max: 25 / 50 / 100 / 200 events).

### entity_filter

> 🧩 Still supported in YAML. The visual editor stores this as a [rule set](#-rule-sets).

Instead of specifying a single entity, write a text filter. The card finds all entities whose ID or friendly name contains the filter text and creates one alert per match:

> 📄 YAML: [entity_filter](YAML.md#entity_filter)

**Message placeholders:**

| Placeholder | Replaced with |
|---|---|
| `{name}` | Entity friendly name |
| `{entity}` | Entity ID |
| `{state}` | Current state value (translated) |
| `{device}` | HA device name from the device registry |
| `{area}` | HA area name (from entity or device area assignment) |
| `{timer}` | Live countdown for `timer.*` entities (`mm:ss` / `h:mm:ss`) |
| `{trigger_state}` | State the entity had when the alert **first fired** — useful for `persistent: true` alerts where the sensor may return to normal while the alert stays visible |
| `{trigger_attribute}` | Attribute value at fire time (only when `attribute:` is set) |
| `{trigger_time}` | Local time string of when the alert first fired |

The matched entity's friendly name is also automatically shown below the message so you always know which device triggered the alert.

### HA template syntax in messages

The `message` field (and `secondary_text`) supports **full Jinja2 template syntax** — rendered server-side by Home Assistant via the WebSocket API, with live updates whenever entities change.

> 📄 YAML: [HA template syntax in messages](YAML.md#ha-template-syntax-in-messages)

Any template that works in HA automations and template sensors works here too.

**Editor preview:** type a filter text and a live counter shows how many entities match. Click the counter to expand a full list with names, entity IDs and current states. Click any entity to exclude it (✗) or re-include it (✓).

### Timer themes

Select a `timer.*` entity and use one of the 4 dedicated timer themes. The card reads `finishes_at` from the timer attributes and updates the display every second:

> 📄 YAML: [Timer themes](YAML.md#timer-themes)

Use `{timer}` in the message to display the live countdown (`mm:ss` or `h:mm:ss`).

When a timer entity is selected in the editor, `state` is automatically set to `active` and the theme switches to `countdown`.

### Numeric / comparison conditions

> 📄 YAML: [Numeric / comparison conditions](YAML.md#numeric--comparison-conditions)

Supported operators: `=` (default), `!=`, `>`, `<`, `>=`, `<=`, `contains`, `not_contains`.

### Attribute-based triggers

> 📄 YAML: [Attribute-based triggers](YAML.md#attribute-based-triggers)

### AND / OR multi-entity conditions

> 🧩 Still supported in YAML. The visual editor stores this as a [rule set](#-rule-sets).

> 📄 YAML: [AND / OR multi-entity conditions](YAML.md#and--or-multi-entity-conditions)

- `and` — all conditions must match (default)
- `or` — at least one must match: the alert's own condition **or** any extra condition (an alert without its own condition shows when any extra condition matches)

### HA icons (mdi:)

> 🎨 In the visual editor this is set on a **custom theme** (Themes → Icon); every alert using the theme follows.

Enable the `use_ha_icon` toggle per alert to use a native HA icon instead of an emoji. When enabled, the card first reads the entity's icon from the HA entity registry — so you get the correct icon automatically without setting it manually. You can also pick any `mdi:` or `hass:` icon from the native HA icon picker in the editor. Combine with `icon_color` to tint the icon with any CSS color.

Any icon namespace is accepted — not just `mdi:` and `hass:`. Icons from `hue:`, `phu:`, `cil:`, and any other custom set registered via `extra_module_url` work automatically.

### Entity picture / custom image as icon *(new in 1.3.9.8)*

> 🎨 In the visual editor this is set on a **custom theme** (Themes → Icon); every alert using the theme follows.

Two new options let you use an image instead of an emoji or MDI icon.

**`use_entity_picture`** — pulls the image HA shows for the entity (`entity_picture` attribute). Works with any entity that exposes a picture: bin/waste sensors, person trackers, camera thumbnails, weather entities, etc.

> 📄 YAML: [Entity picture / custom image as icon](YAML.md#entity-picture--custom-image-as-icon)

**`icon_image`** — point directly to any image by path or URL, without needing an entity with `entity_picture`. Takes priority over `use_entity_picture` if both are set.

Both options render a small rounded square image. `icon_size` accepts any CSS length (`2rem`, `48px`, etc.) and its field appears automatically in the visual editor when either option is active.

### Message placeholders

`{state}`, `{name}`, `{entity}`, and `{device}` work in the `message` field of **any** alert that has an entity set — not just `entity_filter` alerts:

> 📄 YAML: [Message placeholders](YAML.md#message-placeholders)

### secondary_text

A static second line displayed below the message. Supports placeholders. Does not require a secondary entity:

> 📄 YAML: [secondary_text](YAML.md#secondary_text)

### Badge customization

> 🎨 In the visual editor this is set on a **custom theme** (Themes → Severity label); every alert using the theme follows.

Hide the category badge or replace its text:

> 📄 YAML: [Badge customization](YAML.md#badge-customization)

### Sound notifications

Play an audio tone when an alert becomes active. Uses the Web Audio API — no files required for the default tones:

> 📄 YAML: [Sound notifications](YAML.md#sound-notifications)

Default tones by category: Critical = double high beep · Warning = medium beep · Info = soft beep · OK = rising chime.

> **Note:** requires browser autoplay permission. Works out of the box on wall-mounted tablets with HA Companion.

### Large buttons

Always-visible pill-shaped 💤 and 📋 buttons — useful for wall-mounted tablets where hover is not available:

> 📄 YAML: [Large buttons](YAML.md#large-buttons)

### Swipe to snooze

Enable a left-swipe gesture to snooze the current alert on touch devices. Works independently of `tap_action` and `hold_action` — no conflict:

> 📄 YAML: [Swipe to snooze](YAML.md#swipe-to-snooze)

Swipe at least 60 px horizontally to trigger. Uses the configured `snooze_duration` (or 1 h if none is set).

### Invisible touch zone (mobile)

A 22%-wide invisible zone on the right side of the card reveals the action buttons (snooze / history / nav arrows) on the first tap. The buttons auto-hide after 4 seconds. Never interferes with `tap_action`, `hold_action`, or `double_tap_action`.

### Vertical layout

Stack the icon on top and the message below, centered — useful for narrow columns or square card grids:

> 📄 YAML: [Vertical layout](YAML.md#vertical-layout)

Works with all 50 themes. The **Ticker** theme keeps its horizontal scrolling. Can be combined with `ha_theme: true` and `large_buttons: true`.

### HA theme adaptation

Adapt the card's color palette to the active Home Assistant global theme:

> 📄 YAML: [HA theme adaptation](YAML.md#ha-theme-adaptation)

When enabled:
- Card background → `--card-background-color`
- Text → `--primary-text-color` / `--secondary-text-color`
- Critical badges/borders → `--error-color`
- Warning badges/borders → `--warning-color`
- Info badges/borders → `--info-color`
- OK badges/borders → `--success-color`

All 50 visual themes retain their animations and layouts — only the color palette adapts. Compatible with Mushroom, Material, iOS, and any custom HA theme.

### Severity border

Each alert block also gets a 1px border in its severity color (critical/warning/info/OK), separate from the badge/text colors above. Turn it off per-card while keeping the color-coded badges and icons:

> 📄 YAML: [Severity border](YAML.md#severity-border)

Default: `true` (on) — existing dashboards are unaffected. The border width is also exposed as the `--atc-severity-border-width` CSS custom property (default `1px`) if you'd rather control it theme-wide instead of per-card:

`severity_border: false` on the card always wins over the theme variable.

### Card border

Enable a persistent visible border around the card using the standard HA border style:

> 📄 YAML: [Card border](YAML.md#card-border)

Default: `false` (off). Uses `--ha-card-border-width` and `--ha-card-border-color` from the active HA theme. When `card_border` is on and the card is otherwise hidden (no alerts, `show_when_clear` off), a subtle dashed placeholder with a 🔔 icon is shown so the card remains discoverable and editable.

### Test mode

Force all configured alerts to display as active — useful for previewing the card appearance without waiting for real conditions:

> 📄 YAML: [Test mode](YAML.md#test-mode)

> Test mode only applies while this card's editor is open: a config saved with `test_mode: true` behaves normally once the editor is closed (a yellow banner shows it while editing).

In the visual editor, open the **Alerts tab** → enable **Test mode** at the bottom → expand any alert to instantly preview it on the card.

---

## Install via HACS

[![Open your Home Assistant instance and open this repository in HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=Ltek&repository=easy-alert-card&category=plugin)

1. Click the button above, **or** open **HACS → ⋮ → Custom repositories** and add `https://github.com/Ltek/easy-alert-card` as type **Dashboard**
2. Find **Easy Alert Card (Ltek)** and click **Download**
3. **Reload** your browser

---

## Visual Editor

No YAML knowledge required. The editor uses a **hub-and-spoke** layout: the main menu shows all sections as tiles; click any tile to open it.

### 🧩 Rule Sets tab

Create **entity** and **notification** rule sets: name, include and exclude rules (field + operator + value) with Home Assistant's own pickers (labels, areas, floors, entities) and lists of your device classes, domains and integrations, and a live match list right under the ID, with **Exclude** / **Include** buttons per entity, and the alerts using the set at the top. See [Rule Sets](#-rule-sets) and [Notification alerts](#-notification-alerts).

### 🔔 Alerts tab

Add an alert with **Entity**, **Entity Rule Set** or **Notification Rule Set**, or from **Alert Presets**: each preset shows how many entities it can match on your system and how many are active now (click the count for the list), with **Create** (stays on the list) and **Create & edit** (opens the new alert). Preset alerts are inserted by importance — critical ones near the top. An alert's type is fixed when it's added.

Inside an entity rule-set alert, **Can match N entities** lists every entity it can cover, whatever their state right now; a green state marks the ones alerting now.

**Themes** (main screen) — all look settings live on themes, so an alert looks exactly like its theme and the editor preview matches the live card. There are two kinds:

- **Built-in themes** are fixed templates. Open one (👁) to see it and its preset associations; **✎+ Duplicate to customize** makes an editable copy.
- **Custom themes** (*My themes*) are your copies, each marked *based on Flood* etc. — rename, duplicate, delete (its alerts go back to the built-in), 🔍 preview. A custom theme's panel has Icon (theme icon, emoji, the entity's own icon, a custom `mdi:` icon, entity picture, image; color, size), Message / Entity info text (size, color), Severity label (show / hide, text), Effects (disable animations, pulse, flash background), Colors (accent, background) and Layout (card height, font scale, centered text, card border, severity border), with **Reset look to <built-in>**. *Default* means the Global Defaults value or the built-in's own look.

Buttons at the top filter the list — only the matching themes are shown, grouped by category (Critical, Warning, Info…) and sorted by name: **Themes in Use**, **My Custom Themes**, **Alert Presets**, **Built-Ins**. Every Reset asks for confirmation first. The alert editor has no look settings any more — it picks a theme and links to *Edit theme* or *Duplicate & customize theme*. Vertical, large buttons, the counter and the snooze / history buttons stay card-wide (Global Defaults).

When the editor opens a config with per-alert look settings (`icon`, `color`, `show_badge`, `badge_label`, `disable_animation`, …), it moves them into custom themes — alerts with the same base theme and settings share one — and says so once. The card itself still honours per-alert look keys written in YAML.

**Alert Presets and associations** are separate from the look and can be set on any theme, built-in or custom. Every preset shows what it is associated with as chips: a domain (`lock`), a device class (`class: moisture`), `notifications`, or *you pick the entity*. In a theme's *Alert Preset* group every association is a chip with ✕ — built-in ones (e.g. `class: door · Doors & Windows`) and your own domains / device classes alike. **+ Add association…** offers built-in associations from other themes (picking one *moves* it here), device classes and domains found in your HA. Removing a built-in association drops it from its preset (a preset with nothing left disappears); **Reset associations** restores the defaults. Your own domains / classes build one alert with the theme — when the state matches the optional *alert when state is*, otherwise on any change. Alerts created from a preset are separate copies.

> 📄 YAML: [Custom themes & Alert Preset associations](YAML.md#custom-themes--alert-preset-associations)

In **Alert Presets**, 🔍 on a preset previews it on the card in the editor's preview pane (only while editing; the preview is passed to the card directly, never through the card config, so saving can't store it — it stops when you click 🔍 again, close the panel or change anything).

On the main screen, **🚀 Quick Start** (click to open) explains how to get going with Alert Presets.

Each alert row: the theme icon, the name, then **Show in overlay**, on/off, duplicate, delete, and on the far right ▲▼ and the drag handle to reorder (the order decides which alert shows first). **Show in overlay** is greyed until the card's overlay is on. Click a row to open its settings in the same panel. Sections, top to bottom: **Options** (Persistent / Sticky, Show in overlay, per-alert snooze duration, and Trigger on any change for rule-set alerts), **Appearance** (theme, the entity-name line under the message, icon — theme icon, custom emoji, the entity's own HA icon, a custom `mdi:` icon, the entity picture (photo / thumbnail) or an image, accent color, animations, custom card), the alert's source / **Condition**, timing, **Message**, secondary values, sound, TTS, push, camera, visibility, **Tap Actions** (single tap, double tap, hold, snooze) and **Set Entity Value** (`active_state_entity`). Settings are checkboxes. Every section collapses; a ✎ marks sections whose settings differ from the defaults (*Expand all / Collapse all* at the top). The Overlay tab lists every alert with its **Show in overlay** switch.

#### 📚 Alert Presets *(new in 1.3.9.9.7 as "presets")*

The **Alert Presets** panel (under the Add buttons) — the Alert Themes that have a domain or device class associated with them; using one immediately builds an alert for those entities, which you can still edit. It gives one-click access to **twelve built-in presets** plus any theme you gave **Associated domains** in Themes — *All Notifications* first, the rest alphabetical — each showing how many of your entities it can match (✓ *Added* when you already use it). Each preset uses HA `device_class` filters so it auto-matches every pertinent entity on your instance — no per-entity picking required.

**Basic bundles** (one feature per preset):

| Preset | What it does | Themes used |
|----------|-------------|-------------|
| 🔋 **Battery Monitor** | Alerts on every battery entity below 20% | `battery3d` |
| 🚪 **Doors & Windows** | Alerts on any door or window sensor left open | `caution` |
| 🔥 **Fire & CO Safety** | Smoke and CO detectors, critical priority | `fire`, `toxic` |
| 💧 **Water Leak** | Moisture / leak sensors, critical priority | `flood` |
| 👁 **Motion** | All motion sensors triggering | `motion` |
| 🔄 **Software Updates** | HA and integration updates available | `update` |

**Advanced bundles** (multi-feature showcase):

| Preset | What it does | Extra card features |
|----------|-------------|---------------------|
| 🎥 **Security Camera** | Motion → full-screen camera live overlay | `overlay_mode` + `camera_entity` + `camera_live` |
| 🔔 **Doorbell** | Persistent alert with camera, sound, TTS, push | Full notification stack in one preset |
| 🏠 **People Presence** | `on_change` on any `person.*` with auto-dismiss | `on_change` + `auto_dismiss_after` |
| 🌡 **Climate Comfort** | Alert when temperature exits 18–26°C range | Two numeric-operator alerts + `frost` theme |
| 📡 **Devices Offline** | Battery sensors going `unavailable` / `unknown` | Array-state match syntax |

Pick one → the preset's alerts are **appended** to your current list (you can edit / delete each one individually afterwards). Alert messages are intentionally minimal (`{name}` or `{name} — {state}%`) so the theme's icon and colour palette convey the alert type — no translation needed.

Advanced bundles that require card-level defaults (like `overlay_mode: true` for camera/doorbell) apply those defaults **only if you haven't already set them**, so your existing dashboard config is never overwritten.

Duplicates are allowed on purpose — if you want two Battery Monitor alerts with different thresholds, just pick the preset twice and tweak.

> ✨ **First-time hint:** the very first time you open the editor after upgrading, the presets panel pulses with a soft blue glow and a ✨ sparkle badge to draw your attention. Focus the dropdown once and the hint disappears permanently.

#### Alert editor sections

| Section | What's in it |
|---------|--------------|
| **Options** | Persistent / Sticky, Show in overlay, snooze duration, trigger on any change (rule-set alerts) |
| **Appearance** | Theme (built-in or *My themes*), the entity-name line under the message, custom card. Icon, colors, text, severity label and effects come from the theme — *Edit theme* / *Duplicate & customize theme* |
| **Condition** | Single-entity alerts: *When this entity…* (operator + value, or *changes*), then *…and also* inline rules |
| **Message** | Message (placeholders, Jinja2), history message |
| **Secondary value** | Secondary entity / attribute / text and its position |
| **Timing** | Trigger delay, auto-dismiss |
| **Alert Grouping** | Group many matches into one summary slide, with its own tap / hold |
| **Tap Actions** | Single tap, double tap, hold (500 ms), snooze |
| **Sound / Audio**, **TTS**, **Push**, **Camera** | Per-alert notifications and camera |
| **Visibility**, **Set Entity Value** | `visible_to`, `active_state_entity` |

Reorder alerts by dragging the handle or with ▲ / ▼; each row also has Show in overlay, on / off, duplicate and delete.

Every editor page has a **💾 Save** button in its header: it saves the card and keeps the editor open (HA's own Save closes it). It uses the edit dialog's internal save, so on a Home Assistant version where that isn't available the button is hidden.

The main screen lists every page as a full-width tile: Alerts, Rule Sets, Themes, Global Defaults, History, Overlay, All Clear. All on/off settings are checkboxes.

### ⚙️ Global Defaults

Card-wide settings, rarely changed, in collapsible groups (closed by default; ✎ marks a changed group). Themes can override the Look settings per theme, and an alert its own.

| Group | Fields |
|-------|--------|
| **🖼️ Look** | Adapt to HA theme, vertical layout, centered text, large buttons, fixed card height (and *Fill the card height*), font scale, card border, severity border, custom background |
| **🔄 Cycling & Animation** | Cycle interval, transition animation (preview plays on change), disable animations |
| **🎛️ Card controls** | Show the snooze bar, 💤 snooze button, 📋 history button, counter and dismiss bar |
| **💤 Snooze** | Fixed duration or menu (30 min – 1 month); swipe to snooze |
| **🗣️ Voice & Push** | Master switches for all TTS announcements and all push notifications |

### 📋 History

| Field | Description |
|-------|-------------|
| **Stored in this browser** | Keep up to N alerts (max 5000) or N days (max 5) |
| **Shown on the card (📋)** | Everything stored, the latest N (max 500), or a time window (1 hour – 5 days) |
| **View stored history** | List what this browser has recorded |

### 🎨 Themes

Built-in themes are templates; custom themes hold your look settings — see *Themes* above. A custom theme's *Default* values come from Global Defaults → Look.

### 🔔 Overlay tab

| Field | Description |
|-------|-------------|
| **Enable overlay** | Toggle the global floating banner notification |
| **Position** | `Top` / `Center` / `Bottom` — where the banner appears on screen |
| **Duration** | Seconds before auto-dismiss (0 = manual close only) |
| **Scale** | `1` / `1.5` / `2` / `3` — enlarge the banner for wall displays |

The tab shows an **ON** badge when overlay mode is active.

### ✅ All Clear tab

| Field | Description |
|-------|-------------|
| **Show when no alerts** | Toggle to keep the card visible when everything is OK |
| **Display mode** | `Message` · `Clock` · `Weather` · `Weather + Clock` |
| **Clock style** | Style variant for clock-only mode (`aurora`, `gold`, `matrix`) |
| **Weather badge style** | Layout variant for weather modes (`stage`, `split`, `cinematic`, `wallpanel`) |
| **Show date** | Toggle date display in clock / weather+clock mode |
| **Date position** | `Above` or `Below` the time digits |
| **Weather entity** | `weather.*` entity (shown when mode is Weather or Weather + Clock) |
| **Message when clear** | Text to show in message mode |
| **Theme for all-clear** | Visual theme for the all-clear card (OK themes only) |
| **Badge label** | Custom badge text on the all-clear card |
| **Tap / Hold / Double-tap action** | Actions for the all-clear card |

---

## YAML Configuration

Every YAML option — card-level, per alert, actions, custom themes, rule sets, notification rule sets, TTS / push / music options — with snippets and real-world examples is in **[YAML.md](YAML.md)**. You never need it: the visual editor writes all of it.

---

## Languages

The card automatically detects the language from your Home Assistant settings.

| Language | Code | Fallback |
|----------|------|---------|
| Italian | `it` | — |
| English | `en` | ✅ default |
| French | `fr` | — |
| German | `de` | — |
| Dutch | `nl` | — |
| Vietnamese | `vi` | — |
| Russian | `ru` | — |
| Danish | `da` | — |
| Czech | `cs` | — |
| Portuguese | `pt` | — |
| Spanish | `es` | — |
| Turkish | `tr` | — |

TTS fallback messages (auto-generated when no `tts_message` is set) are available in all 12 languages and adapt automatically to the alert's theme category (critical / warning / info / ok / timer).

---

## Troubleshooting

**Card not appearing after installation**
- Add `easy-alert-card.js` as a JavaScript module in Settings → Dashboards → Resources
- Hard-reload the browser (Ctrl+Shift+R / Cmd+Shift+R)

**Features not working after update (secondary text, templates, new options)**
- HA and browsers cache custom card files aggressively. After updating, always do a **hard-reload** (`Ctrl+Shift+R` / `Cmd+Shift+R`) or go to **Settings → System → Restart → Clear cache and restart**. You can verify the running version by searching for `CARD_VERSION` in the JS file via browser DevTools.

**Entity picker not showing in editor**
- Known HA lazy-loading issue. The card handles it automatically. If it still doesn't appear, close and reopen the editor.

**Card disappears when alerts resolve**
- Set `show_when_clear: true` to keep the card visible.

**Trigger state not matching**
- State values are case-sensitive exact strings. Use the live **Current state** hint in the editor or check Developer Tools → States.

**Timer not updating**
- Ensure the timer entity state is `active`. The card reads `finishes_at` from the timer attributes. If `finishes_at` is missing, the countdown shows `--:--`.

**entity_filter matching too many entities**
- Use a more specific filter text, or click individual entities in the editor preview list to exclude them.

**Weather widget shows placeholder but entity is configured**
- Make sure `clear_display_mode` is set to `weather` or `weather_clock` AND `clear_weather_entity` points to a valid `weather.*` entity.

**TTS not playing**
- Check that `tts_enabled` is not `false`. For standard TTS, ensure `tts_entity` is a valid `media_player.*`. For Alexa, set `tts_notify_service` to the correct `alexa_media_*` service name (visible in Developer Tools → Services). The TTS engine is auto-detected from the first `tts.*` state — if none is found, set `tts_engine` explicitly.
- TTS and push notifications are fired directly from the browser tab and only work while the dashboard is open. The card does **not** create any server-side automations. For 24/7 delivery (when the browser is closed), create a native HA automation that calls the same `notify.*` or `tts.speak` service.

**Push notifications not arriving**
- Verify `push_notify_enabled` is not `false`. Check that `push_notify_service` matches the service name exactly (e.g. `mobile_app_my_phone` — without the `notify.` prefix). The card sends push via the HA frontend API while the dashboard is open. For 24/7 delivery, create a native HA automation that calls the same `notify.*` service.

**Camera image not appearing in overlay**
- Verify the `camera_entity` entity exists and has an `entity_picture` attribute in Developer Tools → States. The image is loaded directly from the HA proxied URL — no extra authentication needed on the local network.

---

## License

MIT — see [LICENSE](LICENSE). Easy Alert Card is based on [AlertTicker Card](https://github.com/djdevil/AlertTicker-Card) by djdevil; its copyright notice is kept in LICENSE. Report Easy Alert Card problems at [Ltek/easy-alert-card issues](https://github.com/Ltek/easy-alert-card/issues), not to AlertTicker Card.

---

## Translators

The translations come from AlertTicker Card and its contributors:

A special thank you to **[@edwardtich1](https://github.com/edwardtich1)** for contributing the full **Russian (RU) language** translation — covering all card labels, editor UI, theme defaults, and operator names. ([#53](https://github.com/djdevil/AlertTicker-Card/issues/53))

A special thank you to **[@vdt2210](https://github.com/vdt2210)** for contributing the **Vietnamese (VI) language** translation. ([#12](https://github.com/djdevil/AlertTicker-Card/pull/12))

A special thank you to **[@kgn3400](https://github.com/kgn3400)** for contributing the full **Danish (DA) language** translation — covering all card labels, editor UI, theme defaults, operator names, and overlay strings. ([#57](https://github.com/djdevil/AlertTicker-Card/pull/57))

A special thank you to **[@feixm1](https://github.com/feixm1)** for contributing the full **Czech (CS) language** translation — covering all card labels, editor UI, theme defaults, operator names, and overlay strings. ([#74](https://github.com/djdevil/AlertTicker-Card/pull/74))

A special thank you to **[@Bsector](https://github.com/Bsector)** for contributing the **Portuguese / pt-BR language** translation — providing the core card runtime strings that formed the basis of the full pt-BR support now included in the card. ([#90](https://github.com/djdevil/AlertTicker-Card/issues/90))

A special thank you to **[@yunusuztr](https://github.com/yunusuztr)** for contributing the full **Turkish (TR) language** translation — covering all card labels, editor UI, theme defaults, TTS prefixes, operator names, and overlay strings. ([#134](https://github.com/djdevil/AlertTicker-Card/issues/134))
