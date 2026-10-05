# weather

Tiny terminal weather tool. `weather <location>` prints the current conditions
and today's forecast, straight to stdout — no pager, no API key.

```
$ weather trossingen
🌍  Trossingen, Baden-Wurttemberg, Germany
   48.08, 8.639999 · 701 m

🕐 Current Time
   2026-10-05 05:30   (Europe/Berlin)

☀️ Now — Slight rain showers
   🌡️  Temperature    12.5 °C (feels like 12.7 °C)
   💧  Humidity       96 %
   🌬️  Wind           3.0 km/h ↓ S
   🌧️  Precipitation  0.20 mm
   🧭  Pressure       1026.5 hPa

📅 Today — Slight rain showers
   🔻  Min / Max      12.0 °C / 19.9 °C
   🌧️  Rain total     1.90 mm
   🌅  Sunrise        07:30   Sunset 18:56
```

## Install

```sh
git clone https://github.com/QuantxAmpere/weather.git
ln -s "$PWD/weather/weather" ~/.local/bin/weather   # or anywhere on $PATH
```

## How it works

- [Open-Meteo geocoding](https://open-meteo.com/en/docs/geocoding-api) turns the
  name into coordinates, [Open-Meteo](https://open-meteo.com/en/docs) supplies the
  weather. Both are free and keyless.
- If the geocoder can't match the wording (`weather "moscow dmitrov"`), a
  headless `pi` run proposes a search string that does resolve, verifies it
  against the geocoder, and the lookup is retried with it. Costs a few seconds
  and only happens when the plain lookup fails.
- Colors are emitted only when stdout is a TTY, so piping into a file or another
  program gives clean text.

## Note

This is a small toy project, written entirely by **DeepSeek V4.1 Flash**
(`commandcode/deepseek/deepseek-v4.1-flash`, low reasoning) in a single session,
as a personal evaluation of how well that model handles my day-to-day work and how
fast it gets there. It is not meant to be a polished or maintained tool.

## Requirements

`bash`, `curl`, `jq`. The fuzzy-location fallback additionally needs
[`pi`](https://github.com/earendil-works/pi) on `$PATH`.
