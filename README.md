# Einmaleins 🐴

Einmaleins-Trainer (Mal und Geteilt) mit einem Pferd, das mitwächst — für das iPad, vom Home-Bildschirm.

**Öffnen:** https://strakekine.github.io/einmaleins/
Am iPad in Safari öffnen, dann Teilen → „Zum Home-Bildschirm“.

- Heuballen (Antwort antippen) und Rechnen (selbst eintippen) mit Karteikasten
- Spielwiese: Pferderennen, Wahr oder falsch, Memory — je mit Schwierigkeitsstufe
- Karotten für Futter, Zubehör, Kleidung und Stalltiere; Tagesaufgaben, Abzeichen, Wochensterne
- Lernstand nur auf dem Gerät; Sicherung als Datei unter „Einstellungen & Sicherung“

Eine einzige Datei (`index.html`), kein Build. Regeln und Entscheidungen: [`CLAUDE.md`](CLAUDE.md).

```sh
node test/einmaleins.mjs
node test/einmaleins-oberflaeche.mjs   # Browser (Playwright)
```
