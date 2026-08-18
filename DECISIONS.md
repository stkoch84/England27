# Entscheidungen – England Reise 2027 (POI-Bewertungs-App)

Kurzes Decision Record zur Erweiterung der Bewertungs-App um den London-Städtetrip.
Quelle der POIs: Google-Doc „London Reiseplan für Familien" (Reisen/England27).

## Glossar / Ubiquitäre Sprache
- **POI** – Point of Interest / bewertbare Sehenswürdigkeit (`id, station, name, area, tag, desc`).
- **Etappe (station)** – reines Gruppierungs-Label, kein erzwungener Fahrweg. 1–9 = Südengland-Roadtrip, 10 = London.
- **tag** – Kategorie: Highlight | Familie | Geheimtipp | Kultur | Natur.
- **Bewertung** – pro POI vier Einzelnoten (2 Erw. + 2 Kinder), gespeichert unter `poiRatings[id]`.

## Entscheidungen
1. **Struktur:** London wird als **Etappe 10** in dieselbe Tabelle integriert (nicht getrennt/eigene App).
   Begründung: identische Familie, identische Bewertungsmechanik; „Etappe" ist nur ein Label.
2. **Titel/Scope:** Header „Südengland Roadtrip 2026" → **„England Reise 2027"**; alle sichtbaren „2026" → „2027"
   (Reise findet bewusst 2027 statt). Browser-Tab-Titel analog angepasst.
3. **Umfang der Extraktion:** Alle Kern-Sehenswürdigkeiten + St. Pancras, Covent Garden, Themsefahrt, St. Paul's.
   Weggelassen: Palace Theatre (nur Außenansicht), Seven Dials Market (reiner Foodcourt),
   sowie „im Vorbeifahren"-Nennungen (The Shard, Tate Modern, Shakespeare's Globe, London Eye als eigenes POI).
4. **Granularität:** Tower of London und Tower Bridge **getrennt**; Westminster in Abbey und
   „Big Ben & Houses of Parliament" **aufgespalten**. Ergebnis: 15 POIs, id 60–74.
5. **Harry-Potter-Bezug betont:** Drehort-/Filmbezug ist in den `desc`-Feldern der betroffenen POIs vorangestellt.
6. **Datenerhalt (Kernanforderung):** Keine bestehende `id` (1–59) geändert – nur angehängt.
   Bewertungen werden per `id` in localStorage/Firebase gehalten und bleiben unberührt.

## Betroffene Datei
- `index.html`: `pois`-Array (+15), Etappen-Dropdown (+Etappe 10), Header-Titel, `<title>`,
  Statistik-Kachel „Gesamt POIs" 59 → 74.
