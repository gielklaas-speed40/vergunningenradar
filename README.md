# Vergunningenradar

Statische site op [vergunningenradar.nl](https://vergunningenradar.nl): verleende en aangevraagde omgevingsvergunningen per gemeente en werksoort, dagelijks uit de gemeentebladen. Gehost via GitHub Pages vanaf `main`.

## Hoe het werkt

`pipeline/run.py` bevraagt de SRU van officielebekendmakingen.nl, leest adres, status en werksoort uit de titel (en bij kale titels uit de publicatietekst), en bouwt pagina's per gemeente, per werksoort en per gemeente en werksoort voor huiseigenaren. Alles wordt in de root van deze repository geschreven. De workflow in `.github/workflows/bijwerken.yml` draait elke ochtend om 07:10 Nederlandse tijd en bij elke wijziging in `pipeline/`, en commit het resultaat.

- `pipeline/config.json`: affiliate-links per werksoort en het AdSense-id. Leeg betekent geen knop en geen advertenties.
- `data/opslag.json`: alle bekendmakingen van de laatste 75 dagen, zodat `python pipeline/run.py --rebuild` zonder netwerk werkt.
- Het aanmeldformulier voor de wekelijkse mail post naar Formspree (`mwlewqjg`).

## Domein

1. Settings, Pages: bron `main`, map `/`, custom domain `vergunningenradar.nl`, Enforce HTTPS aan. De workflow probeert dit ook zelf in te stellen.
2. DNS bij de registrar: `A`-records voor `vergunningenradar.nl` naar `185.199.108.153`, `185.199.109.153`, `185.199.110.153` en `185.199.111.153`, en een `CNAME` voor `www` naar `gielklaas-speed40.github.io`.
