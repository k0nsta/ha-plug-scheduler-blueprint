# IKEA GRILLPLATS - smart plug schedule

A **helper-driven** Home Assistant blueprint to schedule any `switch`/plug: turn it **ON**
at a start time and **OFF** at an end time (each independently enabled), only on chosen
**days of the week**, with optional **Repeat weekly** (one-shot if off). Modelled on a
typical "Set Schedules" editor.

Unlike a normal blueprint, the schedule values aren't set in the blueprint — they're read
**live from helper entities** (`input_datetime` for the times, `input_boolean` for the
enables/repeat, `input_text` for the days). That means a **dashboard can edit the schedule
on the fly** (time pickers, day chips, toggles) without touching the automation. The `time`
triggers point at the `input_datetime` entities, so Home Assistant re-arms automatically
when you change a time.

**One automation = one plug.** Create the helpers once per plug, then one blueprint
automation wiring them together.

## Import

[![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fk0nsta%2Fha-plug-scheduler-blueprint%2Fblob%2Fmaster%2Fblueprints%2Fplug_scheduler.yaml)

Or **Settings → Automations & Scenes → Blueprints → Import Blueprint** and paste:

```
https://github.com/k0nsta/ha-plug-scheduler-blueprint/blob/master/blueprints/plug_scheduler.yaml
```

## Inputs

All schedule values are **helper entities** you create once (see below).

| Input | Entity type | What it does |
|---|---|---|
| **Switch to control** | `switch` | The plug/switch entity to schedule. |
| **ON enabled** | `input_boolean` | When on, the plug switches **ON** at the start time. |
| **ON at** | `input_datetime` (time) | The start time. |
| **OFF enabled** | `input_boolean` | When on, the plug switches **OFF** at the end time. |
| **OFF at** | `input_datetime` (time) | The end time. |
| **Days** | `input_text` | Selected days as a digit string, `1`=Mon … `7`=Sun (e.g. `"12345"` = weekdays). |
| **Repeat weekly** | `input_boolean` | On = recurring on the chosen days; Off = run once, then it disables that enable after firing. |

### Helpers

Create these per plug (Settings → Devices & Services → Helpers), e.g. for a `coffee` plug:

```yaml
input_datetime:
  plug_coffee_start: { has_date: false, has_time: true }
  plug_coffee_end:   { has_date: false, has_time: true }
input_boolean:
  plug_coffee_start_en: {}
  plug_coffee_end_en:   {}
  plug_coffee_repeat:   {}
input_text:
  plug_coffee_days: { initial: "12345" }   # 1=Mon .. 7=Sun
```

### Notes

- ON and OFF are independent — enable either or both (ON-only, OFF-only, or a fixed window).
- ON/OFF only fire on the selected days; the day string uses ISO weekday digits (1=Mon … 7=Sun).
- Editing any helper takes effect immediately — the `time` triggers re-arm on change.
- For different weekday/weekend behaviour, point a second automation at a second set of helpers
  (or just include/exclude days in the one schedule).

## License

[MIT](LICENSE)
