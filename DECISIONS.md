# Entscheidungen – England Reise 2027 (POI-Bewertungs-App)

Kurzes Decision Record zur Erweiterung der Bewertungs-App um den London-Städtetrip.
Quelle der POIs: Google-Doc „London Reiseplan für Familien" (Reisen/England27).

## Glossar / Ubiquitäre Sprache
- **POI** – Point of Interest / bewertbare Sehenswürdigkeit (`id, station, name, area, tag, desc`).
- **Etappe (station)** – reines Gruppierungs-Label, kein erzwungener Fahrweg. 1–9 = Südengland-Roadtrip, 10 = London, 11 = „Eigene POIs" (Auffang-Bucket).
- **tag** – Kategorie: Highlight | Familie | Geheimtipp | Kultur | Natur.
- **Bewertung** – pro POI vier Einzelnoten (2 Erw. + 2 Kinder), gespeichert unter `poiRatings[id]`.
- **Seed** – einmalige Migration der hartcodierten Basis-POIs (`SEED_POIS`) nach localStorage/Firebase. Läuft nur bei leerer Liste.
- **custom-POI** – im Frontend angelegter POI mit kollisionssicherer String-ID `custom-<timestamp>-<zufall>`.
- **gestrichen (skip)** – POI-Flag „wird nicht besucht": bleibt erhalten, wird ausgegraut/ans Ende sortiert und aus allen Statistik-Kacheln ausgenommen.

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

---

# POI-Verwaltung im Frontend (Feature 2)

Anforderung: POIs im Frontend hinzufügen/bearbeiten/löschen und auf „wird nicht besucht" setzen, um sie zu bewerten.

## Entscheidungen
1. **Speicher-/Sync-Modell (B – Migration):** Gesamte POI-Liste wird zu Daten. Firestore-Doc
   `suedengland/pois` als **Map** `{ id: {…} }` + `setDoc(merge:true)`; parallel localStorage-Key
   `suedengland_pois`. Das hartcodierte `SEED_POIS`-Array ist nur noch Erst-Seed/Fallback.
2. **Seeding & Source of Truth:** Seed nur, wenn Cloud/localStorage leer. Danach ist die App die
   Wahrheit – Code-Array-Änderungen erscheinen NICHT mehr automatisch. Listenpflege läuft über die App.
3. **Datenform & IDs:** Map keyed by id (nebenläufigkeitssicher via merge). Basis-POIs behalten
   String-IDs „1".."74"; neue POIs kollisionssicher `custom-<timestamp>-<zufall>`.
4. **Formularfelder:** nur `name` Pflicht; `area`, `tag` (Default „Familie"), `Etappe`
   (Default „Etappe 11: Eigene POIs"), `desc` optional.
5. **Etappen-Zuordnung:** Auffang-Bucket „Etappe 11: Eigene POIs" als Default, im Formular auf 1–11 setzbar.
6. **Funktionsumfang:** Hinzufügen + Bearbeiten (auch der Basis-POIs) + Löschen (mit Bestätigung,
   entfernt POI **und** dessen Bewertungen) + `skip`-Toggle.
7. **„wird nicht besucht" (skip):** sichtbar, aber ausgegraut/durchgestrichen, ans Listenende sortiert,
   **raus aus allen Statistik-Kacheln**; Bewertungen bleiben, jederzeit reaktivierbar. Filter „Gestrichene ausblenden".
8. **Statistik:** Kacheln (Gesamt/Bewertet/Ø/Top-Favoriten) werden über die **gesamte** nicht-gestrichene
   Liste berechnet (nicht über den aktuell gefilterten Ausschnitt). „Gesamt POIs" ist jetzt dynamisch.
9. **Datenerhalt:** Bewertungen (`suedengland/family_ratings`) unverändert, weiter per `id` verknüpft.

## Betroffene Datei
- `index.html`: Firestore-Imports (`updateDoc`, `deleteField`), Seed-/Map-Logik (`loadLocalPois`,
  `getPoisArray`, `poiSortKey`, `persistPoiRemote`/`removePoiRemote`/`removeRatingRemote`),
  `subscribeToPoisCloud`, `renderTable` (Map-Quelle + skip + Aktionsspalte), POI-Modal + Handler
  (`openPoiModal`/`savePoiFromModal`/`toggleSkip`/`deletePoi`), Header-Button „➕ POI hinzufügen",
  Filter „Gestrichene ausblenden" + „Etappe 11", CSV-Export (+Status-Spalte).
