# Konzept – Algarve Reise 2026 (POI-Bewertungs-App)

Decision Record für eine **zweite, eigenständige** Bewertungs-App als Klon der England-App.
Quelle der POIs: Google-Doc „Familienausflüge Algarve Ab Albufeira" (Reisen/Algarve 27).
Basis der Reise: *Adriana Beach Club Hotel Resort*, Praia da Falésia (Açoteias/Olhos de Água),
Reisezeitraum 03.–16.10.2026, Familie: 2 Erwachsene + 2 Kinder (8 & 11 J.).

> Status: **Konzept durchgegrillt, noch nichts umgesetzt.** Grundlage für die spätere Umsetzung.

## Glossar / Ubiquitäre Sprache
- **POI** – Point of Interest / bewertbare Sehenswürdigkeit (`id, station, name, area, tag, desc`).
  Schema **identisch** zur England-App.
- **Region (station)** – reines Gruppierungs-Label (kein Fahrweg – Algarve ist ein Sternförmiges
  Tagesausflug-Modell von fixer Basis, kein linearer Roadtrip). 1 Zentral · 2 Barrocal ·
  3 Barlavento · 4 Sotavento · 5 Costa Vicentina · 6 „Eigene POIs" (Auffang-Bucket).
- **area** – Orts-/Ankerpunkt des POI (z. B. „Carvoeiro", „Loulé", „Tavira", „Sagres").
- **desc** – Kurzbeschreibung; **vorangestellt** Fahrzeit ab Resort + der eine kritische
  Planungshinweis (Öffnungszeiten / Gezeiten / Mindestgröße), analog zum England-Muster
  (dort Harry-Potter-Drehortbezug vorangestellt).
- **tag** – Kategorie: Highlight | Familie | Geheimtipp | Kultur | Natur (identisch zu England).
- **Bewertung** – pro POI vier Einzelnoten (Erwachsener 1, Erwachsener 2, Kind 1 (11J), Kind 2 (8J)),
  gespeichert unter `algarve/family_ratings`.
- **Seed** – einmalige Migration der 13 hartcodierten Basis-POIs; läuft nur bei leerer Liste.
- **custom-POI** – im Frontend angelegter POI mit kollisionssicherer ID `custom-<timestamp>-<zufall>`.
- **gestrichen (skip)** – POI-Flag „wird nicht besucht"; bleibt erhalten, ausgegraut/ans Ende
  sortiert, aus allen Statistik-Kacheln ausgenommen.

## Entscheidungen
1. **Struktur & Datenisolation:** Neue Datei `algarve.html`, **gleiches** Firebase-Projekt/DB
   `enland27`, aber **eigener Namespace `algarve`** (`algarve/pois`, `algarve/family_ratings`),
   eigener localStorage-Key `algarve_pois` (+ `algarve_custom_firebase_config`).
   Begründung: Infrastruktur (Config, anonyme Auth, Sync) 1:1 wiederverwendbar, Bewertungen von
   England (`suedengland/…`) bleiben komplett unberührt.
2. **Funktionsumfang – 1:1 wie England:** POI-Verwaltung (Hinzufügen/Bearbeiten/Löschen/Skip),
   Filter (inkl. „Gestrichene ausblenden"), Statistik-Kacheln (Gesamt/Bewertet/Ø/Top-Favoriten),
   CSV-Export, Realtime-Sync + localStorage-Fallback. Seed nur bei leerer Liste, danach App =
   Source of Truth.
3. **`station` → Region:** Algarve ist kein Roadtrip, sondern Tagesausflüge von fixer Basis. Das
   `station`-Feld wird inhaltlich zur **geografischen Region** (Doc-Struktur folgend), Mechanik
   unverändert. Reihenfolge nach Fahrzeit ab Resort aufsteigend. Region 6 „Eigene POIs" als
   Default im Formular.
   Verworfen: Fahrzeit-Bänder; flache Liste ohne Gruppierung.
4. **Schema identisch:** `{ id, station, name, area, tag, desc }` – keine neuen Felder.
   Operatives Beiwerk (Fahrzeit, Öffnungszeiten, Mindestgröße, Gezeiten) wandert vorne in `desc`.
   Verworfen: Zusatzfelder `drive`/`hint` (würden Formular, Tabelle, CSV berühren und von England
   abweichen).
5. **Granularität (2 bewusste Splits):**
   - „Ponta da Piedade & Lagos" → **getrennt** (Klippenstege = Natur, Stadt & Forte = Kultur).
   - Costa-Vicentina-Tag: **Cabo de São Vicente & Fortaleza de Sagres zusammen** (benachbarter
     Stopp-Cluster), **Praia da Bordeira eigener** POI.
   Alle übrigen Doppel-Nennungen bleiben je 1 POI (Alte+Wasserfall, Algar Seco, Barril, Cacela).
   Ergebnis: **13 POIs**, id `"1"`–`"13"`.
6. **Bewerter:** Erwachsener 1, Erwachsener 2, **Kind 1 (11J), Kind 2 (8J)** (dieselben Kinder wie
   England, hier ein Jahr jünger). Reihenfolge Kind 1 = das ältere.
7. **Tags:** Set identisch (Highlight | Familie | Geheimtipp | Kultur | Natur). Kein „Strand"-Tag –
   Strände unter Natur/Familie.
8. **Branding & Navigation:** Header „Algarve Reise 2026", Untertitel
   „(2 Erwachsene, 2 Kinder – 8 & 11 J.) · Basis: Adriana Beach Club, Falésia · 03.–16.10.2026",
   Tab-Titel analog. **Gegenseitiger Header-Link** zwischen England- und Algarve-Seite (kleiner
   Eingriff in `index.html`).

## Die 13 Basis-POIs (Seed)

| id | station (Region) | name | area | tag | desc (Fahrzeit + Kernhinweis vorangestellt) |
|----|------------------|------|------|-----|---------------------------------------------|
| 1 | 1 Zentral | Parque Aventura Albufeira | Santa Eulália | Familie | 🚗 15 min · ⚠️ Okt nur Sa/So ab 10:00 (werktags erst 14:00), Reservierung; Mindestgröße 1,30 m / 1,40 m. Hochseilgarten im Pinienwald, durchgehende Clic-It-Sicherung. |
| 2 | 1 Zentral | Zoomarine Algarve | Guia | Familie | 🚗 25 min · ⚠️ Di–Sa 10–17, So/Mo im Okt geschlossen. Meeres-Themenpark: Delfin-/Robbenshows, Großaquarium, Fahrgeschäfte, kaum Wartezeiten. |
| 3 | 2 Barrocal | Salzbergwerk Loulé (Mina de Sal-Gema) | Loulé | Geheimtipp | 🚗 25–30 min · ⚠️ Reservierung obligatorisch, geschlossene Schuhe, ab 6 J.; 23 °C konstant = Schlechtwetter-Alternative. 230 m Schachtfahrt, 1,3 km Stollen im Salzstock. |
| 4 | 2 Barrocal | Alte & Wasserfall Queda do Vigário | Alte | Natur | 🚗 30–35 min · frei zugänglich, festes Schuhwerk. Quellbecken Fonte Grande unter Platanen + 24 m Wasserfall im Karst-Hinterland. |
| 5 | 3 Barlavento | Castelo de Silves | Silves | Kultur | 🚗 35 min · täglich ab 09:00, Vormittagsschatten. Größte Wehranlage der Algarve aus rotem Sandstein, begehbare Zinnenmauern, Zisterne aus dem 11. Jh. |
| 6 | 3 Barlavento | Algar Seco & Passadiços Carvoeiro | Carvoeiro | Natur | 🚗 35–40 min · ⚠️ vor 10:00 wegen Parkraum, Trittsicherheit nötig. 570 m Holzsteg, Felsenfenster „A Boneca", meerwassergefüllte Gezeitenpools. |
| 7 | 3 Barlavento | Grotte von Benagil (Bootstour) | Benagil | Highlight | 🚗 35–40 min · ⚠️ ruhige See vormittags 09–11; Anlande-/Schwimmverbot. RIB-Boot ab Albufeira, Einfahrt in den Felsdom mit Blick auf den Oculus. |
| 8 | 3 Barlavento | Ponta da Piedade (Klippenstege) | Lagos | Natur | 🚗 50–55 min · vormittags bestes Licht, Parkplatz am Leuchtturm früh anfahren. 2024 erneuerte Passadiços, Felsbögen, Grotten, Buchten. |
| 9 | 3 Barlavento | Lagos Altstadt & Forte da Ponta da Bandeira | Lagos | Kultur | 🚗 50–55 min · gut mit Ponta da Piedade kombinierbar. Seefahrerstadt Heinrichs d. Seefahrers, Forte an der Bensafrim-Mündung, Stadtmauern, Marina. |
| 10 | 4 Sotavento | Praia do Barril & Ankerfriedhof | Tavira | Familie | 🚗 45–50 min · Parken Pedras d'El Rei; Schmalspurbahn pendelt, tideunabhängig, flacher Einstieg. 200+ Thunfischanker im Dünensand (Cemitério das Âncoras). |
| 11 | 4 Sotavento | Cacela Velha & Lagune | Cacela Velha | Geheimtipp | 🚗 50–55 min · ⚠️ nur bei Niedrigwasser (Gezeitenkalender, Start ~60 min vor NW). Wattung zur Praia da Fábrica, Winkerkrabben & Muscheln; weißes Wehrdorf mit Panorama. |
| 12 | 5 Costa Vicentina | Cabo de São Vicente & Fortaleza de Sagres | Sagres | Highlight | 🚗 1h30 (Tagesausflug) · ⚠️ Windjacke! 75 m Steilklippen an Europas Südwestspitze, lichtstärkster Leuchtturm, Windrose Rosa dos Ventos (Ø 40 m). |
| 13 | 5 Costa Vicentina | Praia da Bordeira | Carrapateira | Natur | 🚗 1h35 (Tagesausflug, mit Cabo/Sagres kombinierbar) · Holzstege über Wanderdünen, flache warme Flusslagune zum Waten, seeseitig Surfstrand. |

## Betroffene Dateien (bei späterer Umsetzung)
- **Neu:** `algarve.html` – Klon von `index.html` mit: Namespace `algarve` in allen Firestore-Pfaden,
  localStorage-Keys `algarve_*`, `SEED_POIS` = obige 13 POIs, Region-Dropdown (1–6),
  Bewerter-Labels (11J/8J), Header/Untertitel/`<title>`, Statistik-Kachel „Gesamt POIs" = 13.
- **Änderung:** `index.html` – nur gegenseitiger Header-Link „↔ Algarve-Reise" (England-Daten und
  -Logik unberührt).
