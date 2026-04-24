# Docky ESPHome LVGL Smart Display

ESPHome configuration for an ESP32-2432S028 smart display using LVGL, Elms Sans text, a local Material Design Icons weather font, a 320×240 background image, Home Assistant time, Pirate Weather summary/condition, and outdoor temperature.

## Repository layout

```text
docky-esphome-lvgl/
├── docky.yaml
├── secrets.yaml.example
├── .gitignore
├── THIRD_PARTY_NOTICES.md
├── fonts/
│   ├── README.md
│   └── materialdesignicons-webfont.ttf        # you add this
└── images/
    ├── README.md
    └── background.png                         # you add this
```

## What to commit to GitHub

Commit these:

```text
docky.yaml
secrets.yaml.example
.gitignore
README.md
THIRD_PARTY_NOTICES.md
fonts/README.md
images/README.md
images/background.png, if it is your image or you have rights to share it
fonts/materialdesignicons-webfont.ttf, if you are comfortable redistributing it and include the license/notice
```

Do not commit these:

```text
secrets.yaml
.esphome/
firmware binaries such as *.bin, *.elf, *.map, *.uf2
logs/
```

## Setup

1. Clone or copy this repo into your ESPHome config directory.

   Example:

   ```bash
   cd /root/config
   git clone <your-github-repo-url> docky-esphome-lvgl
   cd docky-esphome-lvgl
   ```

2. Copy your downloaded MDI webfont into the repo:

   ```bash
   cp /root/config/fonts/materialdesignicons-webfont.ttf fonts/materialdesignicons-webfont.ttf
   ```

3. Add your background image:

   ```bash
   cp /root/config/images/background.png images/background.png
   ```

   Best result: crop/export it as exactly 320×240.

4. Create your local secrets file:

   ```bash
   cp secrets.yaml.example secrets.yaml
   nano secrets.yaml
   ```

5. Validate and upload with ESPHome:

   ```bash
   esphome config docky.yaml
   esphome run docky.yaml
   ```

## Home Assistant entities used

The YAML expects these Home Assistant entities:

```text
sensor.pirateweather_minutely_summary
weather.pirateweather
weather.pirateweather attribute: temperature
```

If your entity names differ, edit these sections in `docky.yaml`:

```yaml
text_sensor:
  - platform: homeassistant
    id: weather_summary
    entity_id: sensor.pirateweather_minutely_summary

  - platform: homeassistant
    id: weather_condition
    entity_id: weather.pirateweather

sensor:
  - platform: homeassistant
    id: outdoor_temp
    entity_id: weather.pirateweather
    attribute: temperature
```

## Git commands for first push

```bash
git init
git add .
git status
git commit -m "Add Docky ESPHome LVGL display config"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

Before running `git commit`, check that `secrets.yaml` is not listed in `git status`.
