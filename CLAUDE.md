# einmaleins

Einmaleins-Trainer (Mal und Geteilt) mit einem Pferd für ein 9-jähriges Kind am iPad.
Eine einzige Datei: **`index.html`** — kein Build, kein Framework, ausgeliefert über GitHub Pages:
https://strakekine.github.io/einmaleins/

**Herkunft:** gebaut am 23.11.2026 im Repo `strakekine/panini-wm-2026` als `einmaleins.html`, am selben
Tag auf Wunsch des Nutzers hierher umgezogen. Dort liegt nur noch eine Umzugsseite. Der Lernstand
(localStorage, Schlüssel `einmaleins_v1…`) hängt an der Herkunft `strakekine.github.io` und bleibt beim Umzug
im selben Browser erhalten; die Home-Bildschirm-App hat aber einen **eigenen** Speicher — vor dem neuen
Anlegen sichern (Einstellungen & Sicherung → SICHERN) und danach WIEDERHERSTELLEN.

Nutzer: Laurent (Luxemburg), der Vater. Deutsch, Du-Form, Widerspruch und Begründungen erwünscht, keine
Höflichkeitszustimmung. Änderungen gehen nach Absprache direkt auf `main`.

## iPhone/iPad-Regeln (aus den anderen Apps des Nutzers übernommen, dort am Gerät gelernt)

- **Kein `viewport-fit=cover`** im Viewport-Meta. Sonst liegt der Inhalt unter der Statusleiste und
  alles braucht `env(safe-area-inset-*)`, das sich im Home-Bildschirm-Modus anders verhält als im Browser.
- Ein fokussiertes Eingabefeld bekommt nie `.value` zugewiesen, und ein Container mit fokussiertem Feld
  wird nicht per innerHTML neu gebaut (sonst klappt die Tastatur bei jedem Zeichen ein).
- Home-Bildschirm-Symbol nur als **PNG** (iOS nimmt kein SVG); iOS übernimmt ein neues Symbol nur beim
  neuen Anlegen auf dem Home-Bildschirm.
- Safari und Home-Bildschirm-App haben **getrennte Speicher**. Sicherung als Datei über `navigator.share`.
- Nach einem Push läuft am Gerät oft noch die alte Datei (Zwischenspeicher): **`FASSUNG`** unten im
  Startbild bei jeder Änderung hochzählen und den Nutzer zuerst die Fassung prüfen lassen.
- Im Browser sieht jede Inset-/Layout-Variante richtig aus — Entscheidendes nur am Gerät beurteilen.

## Stand und Regeln

Gebaut am 23.11.2026 auf Wunsch des Nutzers für ein **9-jähriges Kind am iPad** (iOS, Safari /
Home-Bildschirm). **Nur Mal und Geteilt** (vom Nutzer), Reihen 1–10, 11/12 zuschaltbar. Die Figur ist
ein **herzliches Pferd** (vom Nutzer gewünscht), eigenes SVG (`pferdSVG`), Name und Fellfarbe wählt
das Kind beim ersten Start. **Stil flach, ohne Konturen** — am 23.11. vier Stile gezeigt (flach, Comic mit
Konturen, Kawaii, halbrealistisch), vom Nutzer „A behalten“. Vorbild war die App „1x1 Einmaleins Übungen Mathe“ (Artie PRO, Kominak
Studio: herabsinkende Antwortkisten, drei Leben, Levels, Bronze/Silber/Gold) — **Spielidee
übernommen, Figur, Namen und Aussehen nicht**. Kein 3D/AR. Hell und warm (Himmel, Wiese, Heu).
Die iPhone-Regeln unten gelten.

**Zwei Spielarten:** HEUBALLEN — vier Ballen mit Antworten sinken auf das Pferd, richtige antippen
(`pointerdown`), drei Herzen, Landen = Fehler, Tempo Gemütlich/Normal/Schnell = 12/9/6 s Fallzeit.
**Reihen hintereinander** (vom Nutzer, Fassung c, Vorgabe; umschaltbar „Einzeln“, `S.kette`): die nächste Reihe
startet, sobald die jüngste die halbe Strecke gefallen ist (höchstens 3, `G.rows`); jede Reihe trägt ihre Aufgabe
auf einem Schild, **geantwortet wird nur auf die unterste** (`.reihe.aktiv`, Tippen oben zählt nicht), Antwortzeit
ab da, wo sie unterste wurde (`aktivAb`); während der Rückmeldung stehen alle still (`lockAt`).
RECHNEN — Ergebnis über eigenes Ziffernfeld (keine iOS-Tastatur), ✓ zum Abschicken (kein
automatisches Abschicken nach der Stellenzahl, das verriete die Länge), keine Herzen. Level = 10
Aufgaben (`levelBauen`: fällige zuerst, niedrigstes Fach zuerst, höchstens 4 neue). Falsch → Lösung
1,9 s sichtbar, Aufgabe kommt drei später wieder; bewertet wird nur der erste Versuch.

**Karteikasten** (`grade`): Fächer 0–4, `FACH = [1,1,2,4,7]` Tage. Falsch → Fach 0 (oder 1, wenn
schon einmal 2+), morgen, rot (`bad`). **Heuballen sind Auswahl, darum höchstens Fach 3**; „sicher“
(Fach 4) nur beim RECHNEN in ≤ 6 s (`SCHNELL_MS`), langsam getippt ebenfalls höchstens 3. Gedeckelt →
Marke `wt`; schnell getippt springt eine `wt`-Karte sofort auf 4, auch wenn nicht fällig. Richtig
bei nicht fälligen Karten ändert sonst nichts (wie im Vokabeltrainer). Karten-id `m|d:k:r`
(k · r bzw. (k·r) : r, r = Reihe) — **nie umbenennen**, daran hängt der Lernstand.
**Medaille** (`medaille`): Gold = fehlerfrei und flott (Heuballen: Schnitt ≤ halbe Fallzeit;
Rechnen ≤ 5 s), Silber = ≤ 1 Fehler, Bronze = geschafft, ohne Herzen keine. Wurde eine Reihe allein
gespielt, steht ihre beste Medaille an der Reihe.
**Tafel** 10×10 (bzw. 12×12), Mal/Geteilt umschaltbar, Farbe je Fach (`stufe`), Zeilenkopf = nur diese Reihe.
**Motivation:** Karotten (1 je erster richtiger Antwort, Medaille +3/6/10) für den **Laden**
(`WAREN`: Schleife, Halstuch, Blumenkranz, Mähnen rosa/Regenbogen — nur eine gleichzeitig —,
Decke, Brille, Sattel, Krone). Lerntag = 30 erste Antworten, davon 20 richtig; 5 Lerntage Mo–So =
Wochenstern, einlösen per `prompt()` (wie Vokabeltrainer). **Papa-Geheimknopf:** 5× in 3 s auf
„EINMALEINS“ → Code STERN, TAG oder KAROTTEN (+50). Töne per WebAudio, abschaltbar.
**Wachsen** (vom Nutzer, 23.11.2026, Fassung b: „Tamagotchi“ — Claude riet von Hunger/Verfall ab, Nutzer
einverstanden): Pferd beginnt als **Fohlen** und wächst mit Futter für Karotten (`FUTTER`: Heu 4→4, Apfel 10→11,
Hafer 20→24, Zuckerstück 35→45 🌱; ein zufälliges **Lieblingsfutter** je Pferd ×1,5, wird beim ersten Füttern
entdeckt und dann markiert). `STUFEN`: Fohlen 0, Jährling 40, junges Pony 160, Pony 400, großes Pferd 800
(`stufeVon`, `fuettern`, `naechsteStufe`). **Nie Hunger, nie kleiner**, ausgewachsen = kein Futter mehr. Zielgröße:
in etwa 6–8 Wochen normalen Übens groß, wenn auch im Laden gekauft wird. `pferdSVG(fell, wear, stufe, szene)`:
Größe, Kopf, Beinlänge/-dicke, Mähne (Stummel bis Jährling), Schweif je Stufe; Hintergrund wächst mit
(`szeneSVG`: Zaun, Blumen, Stall, Siegerschleife). CSS-Animationen sitzen auf inneren Gruppen, die Stufen-
Transformationen auf äußeren Wrappern (sonst überschreibt CSS-`transform` das SVG-Attribut). Aufstieg →
Feier-Fenster (`#feier`). **Sattel erst ab Pony** (`WAREN.ab`, ein Fohlen trägt keinen Sattel). Wer vorher schon
gespielt hat: Ausgegebenes im Laden zählt als Wachstum, höchstens bis junges Pony (`wachsStart`), nichts geht
verloren. Speicher `_pf` = `{w, lieb, liebBekannt}`, in der Sicherung mit drin. Startbild zeigt Stufe + Balken
und „Psst … Appetit“, Ergebnisseite „🍎 Jetzt füttern“, sobald das billigste Futter bezahlbar ist.
**Abbrechen mit ✕ behält die schon verdienten Karotten** (vorher gingen sie verloren), nur ohne Medaille.
**Großer Ausbau, Fassung d** (vom Nutzer, 23.11.2026: „ruhig komplex, zur Motivation“; kurze Recherche: Spielfigur
zum Anziehen, mehrere Mini-Spiele, Sammelbares sind die üblichen Antreiber):
- **Das Kind** (`kindSVG`, von vorn, ~130 hoch) steht rechts neben dem Pferd. `pferdMalen` baut die Szene 300 breit:
  Hintergrund `szeneSVG(st, 300)`, Pferd als verschachteltes `<svg>` (eigene viewBox 220×200), Kind mit `KIND_GR[stufe]`
  — **wächst mit dem Pferd**. Aussehen beim ersten Start und in den Einstellungen (`S.haut/haar/frisur/shirt`, `lookHtml`).
  Arme hoch bei „froh“, Kopf runter bei „traurig“ (CSS mit `transform-box:fill-box`). CSS gilt nur für `.pferd > svg`
  (sonst zieht `width:100%` das verschachtelte Pferd-SVG auf die ganze Breite).
- **Kleidung** (`KLEIDUNG`, Laden-Karte „Für dich“): je `platz` (kopf/oben/unten/fuss/extra) ein Teil, Neues ersetzt
  das alte, Besitz bleibt (`kindKaufen`, `kindAnziehen`, `SHOP.kwear`).
- **Spielwiese** (`miniStart`, gleiche Spielansicht, Klasse am `#spiel`): **Pferderennen** (12 richtige bis ins Ziel,
  Gegner „Wirbelwind“ braucht 12 × `RENN_MS[tempo]`, steht während der Rückmeldung; Antworten zählen für den Lerntag),
  **Wahr oder falsch** (60 s, Punkte = richtig − falsch, zählt NICHT für den Lerntag — Raten), **Memory** (6 Paare,
  Ergebnisse verschieden). **Keins davon ändert den Karteikasten** — „sicher“ bleibt bei Heuballen/Rechnen.
- **Tagesaufgaben** (`QUESTS`, `tagesQuests(Datum)` deterministisch, drei je Tag, `TQ.ids` beim ersten Aufruf des Tages
  festgehalten — ausgewachsen ohne „Füttern“): je 10 🥕, alle drei +10. Gemeldet über `belohnen([[typ, n]])` am
  Spielende, beim Abbrechen, Füttern, Kaufen; das vergibt auch **Abzeichen** (`ABZEICHEN`, 17 Stück, `abzeichenNeu`,
  Kennzahlen aus `statistik()`, Speicher `_abz`, Zähler `_stat`). Hinweise außerhalb der Ergebnisseite als `toast`
  (oben, `pointer-events:none` — unten verdeckte er die Knöpfe).
**Fassung e** (vom Nutzer): **Stalltiere** (`TIERE`: Küken 30, Huhn 40, Hase 50, Katze 60, Igel 70, Schaf 90, Hund 100;
Laden-Karte „Für den Stall“, `tierKaufen`, einmal gekauft immer da) wohnen in der Szene (`tiereSVG`, Plätze `TIER_ORT`;
Schaf hinten am Zaun vor dem Pferd gezeichnet, die anderen vorne), Schwanz/Ohren bewegen sich, hüpfen bei „froh“ mit;
Abzeichen „Tierfreund“. **Schwierigkeit je Spiel** (`SCHWIERIG`, Fenster `#stufeWahl` vor jedem Spiel der Spielwiese,
gemerkt in `S.stufen`): Karotten ×1 / ×1,5 / ×2 (`mitFaktor`). Rennen: Wirbelwind 7 / 5 / 3,5 s je Antwort (`RENN_MS`;
das Heuballen-Tempo spielt dort keine Rolle mehr). Wahr oder falsch: falsches Ergebnis am weitesten / zufällig / am
knappsten daneben. Memory: 4 / 6 / 8 Paare (`MEM_PAARE`, Raster passt sich der Höhe an). Rekorde und deren Abzeichen
zählen bei Wahr/falsch erst ab Mittel, beim Memory nur mit 6 Paaren. **Achtung Klassennamen:** `.aufgabe` ist die
große Aufgabenschrift — Memory-Karten heißen darum `m-aufgabe`/`m-ergebnis` (vorher waren manche Rückseiten riesig).
**Home-Bildschirm-Symbol** (Fassung f, vom Nutzer: „witzig, mit Pferd und 1×1“): „Professor-Pferd“ — Pferdekopf aus `pferdSVG` (froh) mit
Brille und Doktorhut, darüber „1×1“; als PNG 180×180 eingebettet (`apple-touch-icon`). Zwei Varianten verworfen: nur Brille, Karotte im Maul.
iOS übernimmt ein neues Symbol nur beim **neuen Anlegen** auf dem Home-Bildschirm.
**Speicher:** `einmaleins_v1` (+ `_p`, `_days`, `_stars`, `_shop`, `_med`, `_exp`, `_dirty`, `_snooze`),
Sicherung als Datei über `navigator.share`, Erinnerung nach einer Woche ungesichert.
**Fassung** `FASSUNG` unten im Startbild, bei jeder Änderung hochzählen.
**Testen:** `node test/einmaleins.mjs` (Logik zwischen `Logik`…`Oberfläche`, Gegenprobe gemacht) und
`node test/einmaleins-oberflaeche.mjs` (Browser, 820×1180, Tagesaufgaben im Test fest gesetzt: Levels beider Arten,
Herzen, Tafel, Aussehen, Kleidung, Rennen gewinnen/verlieren, Wahr oder falsch, Memory, Laden, Füttern mit Aufstieg, Abbrechen behält Karotten, zwei Reihen/nur unterste zählt, Fokus beim Namen, Neuladen, Papa-Code). **Am iPad noch nicht ausprobiert.**

## Testen

Vor jedem Push beide, jeder mit eigenem Rückgabewert (nicht über `| tail` verketten):

```sh
node test/einmaleins.mjs              # Logik, schneidet den Block „Logik“…„Oberfläche“ aus index.html
node test/einmaleins-oberflaeche.mjs  # Browser (Playwright)
```

Playwright liegt in der Cloud-Umgebung global unter `/opt/node22/lib/node_modules/playwright/index.mjs`
(Umgebungsvariable `PLAYWRIGHT` überschreibt den Pfad). Screenshots und Wegwerf-Skripte nie ins Repo legen.
