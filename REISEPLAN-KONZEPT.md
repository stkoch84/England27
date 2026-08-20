# Konzept – Reiseplan England Reise 2027

Bewertungsgetriebener Reiseplan auf Basis der abgeschlossenen POI-Bewertungen (Firestore
`enland27` → `suedengland/family_ratings` + `suedengland/pois`, Stand der Durchgrillung).
Familie: 2 Erwachsene + 2 Kinder (12 & 9 J.).

> Status: **Route durchgegrillt.** Grundlage für den App-Umbau (Etappen-Restrukturierung + Streichungen).

## Rahmen (fix vorgegeben)
- **Anreise:** So **27.06.2027**, Fähre Calais→Dover vormittags. Erste ÜN Dover.
- **London:** Anreisetag + 2 volle Tage (3 Nächte).
- **Endpunkt:** Dover. **Rückfahrt:** Mi **14.07.2027** Fähre Dover→Calais vormittags.
- **Budget:** 17 Nächte gesamt (Nacht 1 = So 27.06 … letzte Nacht = Di 13.07).
- **Wunsch-Takt:** im Idealfall mind. 2 Nächte pro Zwischenstopp.

## Glossar (Ergänzung zur bestehenden ubiquitären Sprache)
- **Basis / Standort** – Ort, an dem übernachtet wird; von hier Tagesausflüge/-etappen.
- **Etappe (station)** – wird inhaltlich zur **geografischen Region in Routenreihenfolge** (1 Dover
  … 9 Isle of Wight). Mechanik unverändert; Skip-Flag weiterhin unabhängig.
- **Transfertag** – Fahrtag zwischen zwei Basen, auf dem POIs „im Vorbeifahren" mitgenommen werden.
- **Korridor** – Streckenabschnitt ohne eigene Basis, auf dem mehrere Gems auf Transfertage verteilt
  werden (hier: Bath → Cornwall-Westspitze).
- **Pflicht / Kür** – Auswahl-Policy: Ø ≥ 8.0 = Pflicht (Route wird darum gebaut); Ø 7.0–7.9 = Kür
  (nur wenn on-route/am Basis-Tag); Ø < 7.0 = raus (außer Null-Umweg-Ausnahme).

## Grundentscheidungen
1. **West-Reichweite: voll bis Land's End / Cornwall.** Die 13 Nächte nach London tragen den vollen
   Sweep – knapp, aber machbar. Verworfen: Cap bei Devon (verliert den hochbewerteten Far-West-Cluster).
2. **Sussex komplett gestrichen.** Alle POIs in/um **Rye & Brighton** raus (inkl. Seven Sisters – ohne
   Sussex-Basis ein Orphan, zudem redundant zu den White Cliffs 9.0). Konsequenz: Der Korridor
   Zentral-England → Dover ist POI-leer → reine Transitstrecke am Ende.
3. **Isle of Wight rein** (trotz Auto-Fähre). Grund: **Needles 9.2 + Shanklin 9.0 + Osborne 8.0** =
   höchstbewerteter Cluster außerhalb Londons. Preis: Cornwall-Westspitze etwas enger getaktet.
4. **Schleifenrichtung: gegen den Uhrzeigersinn** (Inland raus, Küste zurück). IoW ist die *letzte*
   West-Basis → kurzes, scenisches Finale (IoW→Dover ~2,5 Std.) statt 4-Std-Leertransit. Kultur-Cluster
   (Gloucester/Warwick/Stratford/Bath/Cheddar) früh & frisch direkt nach London.
5. **Nächte-Verteilung:** 13 Nächte nach London = 12 West-Regionen + 1 letzte Dover-Nacht.
   Zwei Sparmaßnahmen statt „überall 2 Nächte": **Tintagel = 1 Transit-Nacht**, **Dorset = keine eigene
   Nacht** (Jurassic-Coast-Stopps auf dem Transfertag Devon→IoW). Dafür **Cornwall-Westspitze = 3 Nächte**.
6. **WB Studio Tour (10.0) = Abreisetag statt London-Stadttag.** Liegt in Leavesden (NW-London), genau
   auf dem Weg London→Cotswolds. Wird Vormittag von N5 → spart einen London-Tag, City behält 2,5 Tage.
7. **Bath→Cornwall-Korridor: alle vier Gems behalten** (Valley of Rocks 8.5, Clovelly 8.5, Tintagel 8.5,
   Heligan 9.0), verteilt auf zwei intensive Fahrtage (N9/N10). Kein 8.5er geopfert; Boscastle/Dunster (Kür) raus.
8. **Dover Castle (6.5) bleibt** trotz < 7.0 – Null-Umweg (2× ÜN Dover ohnehin).

## Nacht-für-Nacht (17 Nächte)

| Nacht | Datum | Basis | Programm (Ø) |
|---|---|---|---|
| N1 | So 27.06 | **Dover** | Fähre Calais→Dover · nachmittags **White Cliffs 9.0** |
| N2 | Mo 28.06 | **London** | Fahrt Dover→London (~2 Std.) · Anreisetag/erster City-Nachmittag |
| N3 | Di 29.06 | **London** | City voll 1 |
| N4 | Mi 30.06 | **London** | City voll 2 |
| N5 | Do 01.07 | **Cotswolds** | Vormittag **WB Studio Tour 10.0** (Leavesden) → weiter Warwick |
| N6 | Fr 02.07 | **Cotswolds** | **Warwick Castle 8.2** + **Stratford 8.2** |
| N7 | Sa 03.07 | **Bath** | unterwegs **Gloucester Cathedral 9.2** → **Bath 8.2** |
| N8 | So 04.07 | **Bath** | **Cheddar Gorge 9.0** (+ Wells optional) |
| N9 | Mo 05.07 | **Tintagel** | **Valley of Rocks 8.5** → **Clovelly 8.5** → Tintagel *(~4 Std.)* |
| N10 | Di 06.07 | **Cornwall-Westspitze** | **Tintagel Castle 8.5** → **Heligan 9.0** → Penzance *(~4 Std.)* |
| N11 | Mi 07.07 | **Cornwall-Westspitze** | SW-Zipfel: **Porthcurno 8.8** · **Land's End 8.2** · **Minack 7.8** |
| N12 | Do 08.07 | **Cornwall-Westspitze** | **St Michael's Mount 8.2** · **St Ives 8.0** (Trebah 7.0 opt) |
| N13 | Fr 09.07 | **South Devon** | unterwegs **Overbeck's 8.0** · Torbay: **Kents Cavern 8.0** (Exeter/Torquay 7.0 Kür) |
| N14 | Sa 10.07 | **South Devon** | Dartmoor: **Postbridge 8.0** · Lydford 7.8 · Haytor 7.5 · Castle Drogo 7.2 |
| N15 | So 11.07 | **Isle of Wight** | unterwegs Dorset: **Durdle Door/Lulworth 8.0** · **Old Harry 7.8** → Fähre IoW |
| N16 | Mo 12.07 | **Isle of Wight** | **Needles 9.2** · **Shanklin Chine 9.0** · **Osborne 8.0** (Robin Hill 7.5 opt) |
| N17 | Di 13.07 | **Dover** | IoW-Fähre → Dover (~2,5 Std.) · **Dover Castle 6.5** falls Zeit |
| — | Mi 14.07 | Heimreise | Fähre Dover→Calais vormittags |

Längste Einzeletappe ~3 Std.; die zwei intensiven Fahrtage (N9/N10) sind von den 3 ruhigen
Cornwall-Nächten eingerahmt. Hochsommer: hell bis ~21:30.

## Etappen (neue `station`-Struktur, Routenreihenfolge)

| Etappe | Region | Geplante POIs (id · Ø) |
|---|---|---|
| **1** | Dover | 2 White Cliffs 9.0 · 1 Dover Castle 6.5 |
| **2** | London | 60 WB Studio 10.0 · 68 Tower Bridge 10.0 · 70 Big Ben 9.8 · 62 Leadenhall 9.2 · 65 Gleis 9¾ 9.2 · 67 Tower of London 9.2 · custom British Museum 9.0 · 61 MinaLima 9.0 · 66 Millennium Bridge 8.8 · 63 Borough Market 8.5 · 69 Westminster Abbey 8.5 · 73 Themsefahrt 8.5 · 71 St Pancras 8.2 · 72 Covent Garden 8.2 · 74 St Paul's 8.2 · 64 Cecil Court 7.5 |
| **3** | Cotswolds & Warwickshire | 59 Gloucester 9.2 · 57 Stratford 8.2 · 58 Warwick 8.2 |
| **4** | Bath & Somerset | 55 Cheddar 9.0 · 56 Bath 8.2 |
| **5** | Nord-Cornwall & Tintagel | 48 Tintagel 8.5 · 50 Clovelly 8.5 · 52 Valley of Rocks 8.5 |
| **6** | Cornwall-Westspitze | 39 Heligan 9.0 · 46 Porthcurno 8.8 · 40 St Michael's Mount 8.2 · 45 Land's End 8.2 · 47 St Ives 8.0 · 44 Minack 7.8 · 43 Trebah 7.0 *(opt)* |
| **7** | South Devon & Dartmoor | 30 Kents Cavern 8.0 · 33 Postbridge 8.0 · 37 Overbeck's 8.0 · 35 Lydford 7.8 · 32 Haytor 7.5 · 34 Castle Drogo 7.2 · 28 Exeter 7.0 · 29 Torquay 7.0 |
| **8** | Dorset (Jurassic-Stopps) | 23 Durdle Door/Lulworth 8.0 · 21 Old Harry 7.8 |
| **9** | Isle of Wight | 12 Needles 9.2 · 15 Shanklin 9.0 · 14 Osborne 8.0 · 17 Robin Hill 7.5 *(opt)* |

## Streichungen (skip = „wird nicht besucht")

**Bereits vor der Durchgrillung gestrichen (9):** Bodiam 5.8, Dungeness 6.5, Devil's Dyke 6.8,
Russell-Cotes 4.2, Hengistbury 6.0, Dorset Museum 3.0, Cerne Abbas 2.5, Cockington 5.0, Tarr Steps 5.2.

**Sussex komplett (6):** Rye 8.0, Camber Sands 8.0, Royal Pavilion 7.0, Brighton Pier 8.2, i360 7.5,
Seven Sisters 7.8.

**Policy < 7.0 (6):** Corfe 6.8, Carisbrooke 6.8, Blackgang 6.8, Bournemouth 6.8, Salcombe 6.8, Barnstaple 6.8.

**Kür ohne Platz (7):** Kimmeridge 7.8, Abbotsbury 7.0, Hope Cove 7.0, Pendennis 7.0, Maritime Museum 7.0,
Boscastle 7.0, Dunster 7.0.

**Summe: 28 gestrichen · 47 geplant** (davon 2 optional: Trebah 7.0, Robin Hill 7.5).

## App-Umbau (Umsetzung)
1. **`station` neu (1–9)** in Routenreihenfolge (siehe Tabelle). Dropdown-Optionen in Filter **und**
   POI-Modal von `index.html` ersetzen; `SEED_POIS` (Fallback) an neue Zuordnung angleichen.
2. **Skip-Flags** für die 19 neuen Streichungen (Sussex 6 + Policy 6 + Kür 7) setzen; die 9 alten bleiben.
3. **Statistik-Kachel „Gesamt POIs"** ergibt sich dynamisch (nur nicht-gestrichene) → 47.
4. **Live-Daten (Firestore):** `station` + `skip` je POI aktualisieren – nur nach ausdrücklicher Freigabe,
   Backup von `pois`/`family_ratings` liegt vor. Bewertungen (`family_ratings`) bleiben per `id` unberührt.
