# Projekt 01 – Bundesliga live in Home Assistant

Live-Ergebnisse und Tabelle der 1. Bundesliga als Dashboard in Home Assistant. Kostenlos, ohne API-Schlüssel. Daten: [OpenLigaDB](https://www.openligadb.de).

## Was du brauchst

- Home Assistant (getestet mit 2026.11)
- Karte **flex-table-card** (Einstellungen → Marketplace)
- Packages in der `configuration.yaml` aktiviert:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

**Vorher prüfen:**
- Steht in deiner `configuration.yaml` schon eine Zeile mit `packages:`? Dann nichts neu eintragen, sondern `bundesliga.yaml` in den dort angegebenen Ordner legen.
- Gibt es schon einen Block `homeassistant:`? Dann nur die Zeile `packages: …` darunter einfügen, zwei Leerzeichen eingerückt. `homeassistant:` darf nur einmal in der Datei stehen.

## Dateien

| Datei | Wohin | Wofür |
|---|---|---|
| `bundesliga.yaml` | `/config/packages/bundesliga.yaml` | Sensoren für Spieltag und Tabelle |
| `bundesliga-spieltag-karte.yaml` | Dashboard → Karte hinzufügen → Manuell | Spieltag mit Live-Ständen |
| `bundesliga-tabelle-karte.yaml` | Dashboard → Karte hinzufügen → Manuell | Tabelle mit Farbzonen |

## Einbau in 4 Schritten

1. Im File Editor den Ordner `packages` anlegen (falls noch nicht vorhanden), darin „New File“ → `bundesliga.yaml` und den Inhalt einfügen.
2. Entwicklerwerkzeuge → YAML → „Konfiguration prüfen“ → Home Assistant neu starten.
3. Unter Entwicklerwerkzeuge → Zustände nach `bundesliga` suchen. Es sollten u. a. `sensor.bundesliga_aktueller_spieltag`, `sensor.bundesliga_spieltagsdaten` und `sensor.bundesliga_tabellendaten` erscheinen.
4. Dashboard bearbeiten → Karte hinzufügen → Manuell → Inhalt der beiden Karten-Dateien einfügen.

## Warum so?

- **Ein Package statt Einträge in der configuration.yaml:** alles an einer Stelle, leicht zu entfernen.
- **Spiele als Attribut, nicht als Zustand:** Die großen Daten landen nicht im Verlauf, die Datenbank bleibt klein.
- **30-Sekunden-Takt nur bei laufenden Spielen:** schont die freie OpenLigaDB-API.

## Anpassen

- Farben der Tabellenzonen: oben in `bundesliga-tabelle-karte.yaml`.

## Quellen

- Spieldaten: [OpenLigaDB](https://www.openligadb.de)
