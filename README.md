# IKEA GRILLPLATS - smart plug schedule

A Home Assistant blueprint to schedule any `switch`/plug, modelled on a typical
"Set Schedules" editor: an independent **ON** time and **OFF** time (each toggled on/off
separately), a **days-of-week** picker, **Repeat weekly**, and an optional **off delay**
(auto-off a set time after it turns on — also catches a *manual* turn-on, handy as a
coffee-machine / iron / heater safety).

**One automation = one schedule.** Create several from this blueprint for different
patterns (e.g. one for weekdays, one for weekends). Everything is configurable from the
UI — no YAML editing once imported.

## Import

[![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fk0nsta%2Fha-plug-scheduler-blueprint%2Fblob%2Fmaster%2Fblueprints%2Fplug_scheduler.yaml)

Or **Settings → Automations & Scenes → Blueprints → Import Blueprint** and paste:

```
https://github.com/k0nsta/ha-plug-scheduler-blueprint/blob/master/blueprints/plug_scheduler.yaml
```

## Inputs

| Input | What it does |
|---|---|
| **Switch to control** | The plug/switch entity to schedule. |
| **Enable ON time** + **ON at** | Turn the plug on at this time (on the chosen days). |
| **Enable OFF time** + **OFF at** | Turn the plug off at this time (on the chosen days). |
| **Enable off delay** + **Off delay** | Turn off this long after the plug switches on — fires for scheduled *and manual* turn-ons. |
| **Days of week** | Which days the ON/OFF times run. |
| **Repeat weekly** | On = recurring; Off = run once, then the schedule disables itself after the next off. |

### Notes

- Mix freely: ON-only + off-delay (auto-off timer), ON + OFF times (fixed window), or all three.
- The **off delay** is never gated by day — turning the plug **off** is always allowed (safety).
- For different weekday/weekend times, create two schedules (one Mon–Fri, one Sat–Sun).

## License

[MIT](LICENSE)
