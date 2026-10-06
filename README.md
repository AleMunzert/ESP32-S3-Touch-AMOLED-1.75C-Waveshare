# georg-esp32-satellit-kueche

ESPHome-Konfiguration fuer einen Sprachsatelliten auf Basis des **Waveshare ESP32-S3-Touch-AMOLED-1.75C** (Display CO5300, Touch CST9220, Audio-ADC ES7210, Akku-Auslese ueber AXP). Er nutzt den Home-Assistant-Sprachassistenten mit Wake Word direkt auf dem Geraet (microWakeWord) oder in Home Assistant, zeigt Zustandsbilder und Uhrzeit auf dem Display und gibt die Antworten ueber einen externen Mediaplayer aus.

## Inhalt

- `esp32-s3-amoled-satellit.yaml` - die Konfiguration
- `secrets.yaml.example` - Vorlage fuer die eigenen Zugangsdaten
- `.gitignore` - schliesst `secrets.yaml` aus

## Voraussetzungen

- ESPHome 2026.8.0 oder neuer
- Eigene Wake-Word-Modelle (`hey_georgsch.json`, `hai_dschoartsch.json`) unter `/config/esphome/` - nicht Teil dieses Repositories. Alternativ die entsprechenden Eintraege im Block `micro_wake_word` anpassen oder entfernen.
- Eigene Zustandsbilder (PNG, 466x466) unter `/config/esphome/esp_assets/images/` - nicht Teil dieses Repositories. Die Dateinamen stehen im Block `substitutions`.
- Ein Mediaplayer in Home Assistant fuer die Ausgabe (hier `media_player.kueche`)

## Einrichtung

1. `secrets.yaml.example` nach `secrets.yaml` kopieren und die Werte eintragen. Den API-Schluessel mit `openssl rand -base64 32` neu erzeugen.
2. Konfiguration im ESPHome-Dashboard hinzufuegen und mit **Install** auf das Geraet spielen.
3. Das Geraet in Home Assistant einbinden und den gewuenschten Sprachassistenten zuweisen.

## Hinweise

- Die Ausgabe laeuft ueber einen externen Mediaplayer, weil ein lokaler Lautsprecher wegen eines offenen ESPHome-Fehlers (`i2s_audio`-DMA, Issue #16755) umgangen wird.
- Erkennt der Assistent eine Rueckfrage (Antwort endet auf `?`), hoert er danach ohne erneutes Wake Word weiter.
- Zugangsdaten gehoeren nie ins Repository. Alle sensiblen Werte laufen ueber `!secret`.
