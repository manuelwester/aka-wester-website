# STUDIO aka WESTER — Website

Statische Website für [aka-wester.de](https://aka-wester.de) — Boutique Hairstyling, Berlin.
Komplett-Neuaufbau (Juni 2026) als Ablösung der alten Webflow-Seite.

## Stack

- Reines HTML/CSS/JS, keine Frameworks, kein Build-Schritt
- Hosting: Cloudflare Workers (Static Assets), Account „Saloncare" (`bef6…2597`)
- Fonts lokal (Cormorant Garamond + Montserrat, woff2) — kein Google-Fonts-CDN (DSGVO)
- Bilder als WebP (Originale der alten Seite, von 32 MB auf ~2,6 MB optimiert)
- Farbwelt nach Salon-Interieur: Petrol `#155159`, Gold `#c2a05e`, Ivory `#faf7f2`

## Struktur

```
public/
  index.html            Startseite
  ueber-uns.html        Philosophie, Studio, Team
  services.html         Leistungen + Preishinweis
  vipladiesday.html     Style & Dine Event (399/299 € p. P.)
  events.html           Cut'n Drink, VIP Ladies Day, CSD Pride Party
  maehnen-der-welt.html Doku-Serie (YouTube-Verlinkung, kein Embed)
  impressum.html        inkl. AGB/Storno-Bedingungen (§ 5 DDG)
  datenschutz.html      eigene Datenschutzerklärung (Cloudflare-Hosting)
  404.html              Fehlerseite
  css/ fonts/ img/ js/  Assets
```

## Entwicklung & Deploy

```bash
# Lokale Vorschau
npx wrangler dev

# Deploy (WICHTIG: FrontNow-Token aus ~/.zsh_secrets umgehen!)
env -u CLOUDFLARE_API_TOKEN npx wrangler deploy
```

Login: `manuel@aka-wester.de` (wrangler OAuth).

## Go-Live (einmalig)

1. Zone `aka-wester.de` im Cloudflare-Dashboard anlegen (Account Saloncare)
2. Bei Strato die Nameserver auf die von Cloudflare genannten umstellen
3. `routes` in `wrangler.jsonc` einkommentieren, erneut deployen
4. DNS-Records für `aka-wester.de` + `www` als proxied Platzhalter anlegen
   (analog salon.care, siehe deren wrangler.jsonc-Kommentar)

## Offene Punkte (Stand 12.06.2026)

- Cloudflare-Login manuel@aka-wester.de per E-Mail verifizieren, dann `wrangler deploy` (Fehler 10034)
- Datenschutzerklärung anwaltlich prüfen lassen
- „Vertreten durch: Hans-Josef Wester" basiert auf alter Website + Registerpublikation 2018 — bei Wechsel der Geschäftsführung aktualisieren

Geklärt am 12.06.2026 (Manuel): Firma ist Wester Styling UG (haftungsbeschränkt) — Highstyle GmbH entfernt;
USt-ID DE319354587; Register AG Charlottenburg HRB 199273 B; VIP Ladies Day einheitlich 399 € (299 € war Aktion).
