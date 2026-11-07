# Wo zum Geier?

Ein kleines GeoGuessr-Spiel im Browser. Street View zeigt einen Ort, du setzt einen Pin auf die Karte, und das Spiel sagt dir, wie viele Kilometer du daneben liegst.

- 5 Runden, bis zu 5.000 Punkte pro Runde
- Modi: Welt und Deutschland
- Karte: Leaflet mit OpenStreetMap
- Street View: Google (Embed ohne Key, oder mit eigenem Maps-JavaScript-API-Key)

Das Spiel ist eine einzige statische Datei (`index.html`), ohne Build-Schritt.

## Starten mit Docker

```bash
docker compose up -d --build
```

Danach läuft es auf http://localhost:8080.

Ohne Compose:

```bash
docker build -t wozumgeier .
docker run -d --name wozumgeier -p 8080:80 wozumgeier
```

## Street View mit API-Key

Ohne Key läuft das öffentliche Embed, das oben links die Adresse einblendet (ein Balken verdeckt sie). Mit einem Maps-JavaScript-API-Key im Startbildschirm entfällt das, und Orte ohne Panorama werden ersetzt. Der Key bleibt im `localStorage` des Browsers und wird nirgends sonst gespeichert.

## Reverse Proxy

Hinter einem Proxy (Traefik, nginx Proxy Manager, Caddy) genügt es, auf Port 80 des Containers zu zeigen. Es gibt einen Healthcheck unter `/healthz`.
