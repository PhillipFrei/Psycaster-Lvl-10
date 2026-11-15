# Psycaster Level 1–10

Konzept für eine eigenständige RimWorld-1.6-Psycaster-Mod mit frei wählbaren Psycasts, Archotech-Transzendenz und sichtbaren, dauerhaft wirksamen Fähigkeiten.

**Status:** Planung – noch keine spielbare Mod.

## Konzept

- 10 Psylink-Level; pro Levelaufstieg freie Auswahl eines Psycasts.
- Level 1–6: normale Psylink-Neuroformer.
- Level 7–10: nur transzendierte Psylink-Neuroformer, die vorher mittels Archotech-Mechanik umgewandelt wurden.
- Eigene Psycast-Definitionen in verschiedenen Rollen: Kampf, Heilung, Schutz, Bewegung, Arbeit, Psyfocus, Umwelt und Teleportation.
- Lange, spielrelevante Buffs und Raumkugeln, gut erkennbare Effekte und starke Fähigkeiten mit balancierten Cooldowns.

## Aktuelle Planungsdatei

**[Vollständiger geplanter Zauberkatalog und Mechanik](docs/Zauberplanung.md)**

Die Liste ist ein **Entwurf**. Zahlen in der Planung sind Zielwerte, keine bereits implementierten oder getesteten Funktionen.

## Technische Leitlinien

- Basis: RimWorld 1.6 + Royalty.
- C# für eigene Effekte und Auswahl-/Neuroformerlogik, XML für AbilityDefs, Hediffs und Balancing, Harmony nur wo nötig.
- Steam-Workshop-Mods aus dem bereitgestellten Referenzarchiv dienen der Analyse; wir verteilen keine fremden DLLs, Texturen oder ungeprüft kopierten Quellcodes.
- Die vorhandenen Anpassungen im Projekt [Cooler-Psycasts-Tweaks](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks) dienen als technische Referenz, insbesondere Learn, Reverse Time, Gamma Ray, Gravity Pulse, Reverse Gravity und Unmake.
- Die fertige Mod soll per GitHub Actions gebaut und als installierbarer ZIP-Ordner bereitgestellt werden.

## Geplante Umsetzung

1. Grundgerüst, Level 1–10, freie Auswahl und Neuroformer-Transzendenz.
2. Buffs, Zustands-/Heilungslogik, Umweltkugeln und grafische Effekte.
3. Kampf-, Schild-, Teleport- und Flächeneffekte.
4. Archotech-Fähigkeiten, Balancing, Sicherheit in Spielständen und GitHub-Release.

