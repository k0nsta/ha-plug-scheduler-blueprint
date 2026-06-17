# Smart plug scheduler — on/off + auto-off

A Home Assistant blueprint to schedule any `switch`/plug **ON** at a time of day — with
**separate weekday and weekend** times — and turn it **OFF** either:

- a fixed **duration** after it switches on (also catches a *manual* turn-on — handy as a
  coffee-machine / iron / heater safety auto-off), or
- at a fixed **clock time**.

Everything is configurable from the UI — no YAML editing once imported.

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
| **Weekday schedule** | Enable + ON time for Mon–Fri. |
| **Weekend schedule** | Enable + ON time for Sat–Sun. |
| **Off mode** | `Auto-off after a duration` *or* `Off at a fixed time`. |
| **Auto-off after** | Duration the plug stays on after switching on (duration mode). |
| **OFF time** | Fixed clock time to turn off (fixed-time mode). |

### Notes

- The **duration** off mode triggers on *any* turn-on (scheduled or manual), so it doubles as a
  safety auto-off. Set the weekday/weekend times equal if you want the same time every day, or
  disable a group to schedule only weekdays or only weekends.
- The OFF action is never gated by day — turning the plug **off** is always allowed.

## License

[MIT](LICENSE)
