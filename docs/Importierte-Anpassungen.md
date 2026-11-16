# Importierte Psycast-Anpassungen – Analyse der beiden ZIP-Archive

**Stand:** 16. November 2026. **Status:** Quellprüfung und Migrationsplan, **keine Integration in eine spielbare Mod**.

## Quelle und Teststatus

Der Benutzer hat die beiden Archive `Psycast-Referenzmods(1).zip` und `CoolerPsycastsTweaks.zip` bereitgestellt und mitgeteilt, dass darin **einige Änderungen bereits umgesetzt und im Spiel getestet** wurden. Die Dateien wurden inhaltlich verglichen; **welche einzelnen Fähigkeiten erfolgreich getestet wurden, ist nicht im ZIP dokumentiert**. In dieser Umgebung wurde weder RimWorld gestartet noch die DLL selbst kompiliert. Deshalb trennen wir ausdrücklich:
- **Im Archiv implementiert:** XML-Patches/Definitionen und zugehörige vorkompilierte .NET-DLL existieren.
- **Vom Benutzer als teils getestet gemeldet:** keine per Fähigkeit zuordenbaren Testlogs oder Versionstests.
- **In Psycaster-Lvl-10 übernommen:** derzeit noch **nicht**. Die folgenden Funktionen sind verbindliche Vorlagen für die nächste Implementierung.

Die aus dem Archiv `CoolerPsycastsTweaks.zip` stammende DLL ist eine **kompilierte** `CoolerPsycastsTweaks.dll` (46.080 Byte). Ein passender **C#-Source-Ordner liegt in dieser ZIP nicht vor**. Im anderen GitHub-Repository [Cooler-Psycasts-Tweaks](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks) befindet sich älterer, dokumentierter C#-Quellcode (README-Stand v4). Neuere v5–v8-Erweiterungen dürfen **nicht** allein anhand des v4-Sourcecodes als vollständig reproduzierbar gelten. Die ZIP kann zur Laufzeit als eigener Add-on-Mod benutzt werden; für die unabhängige neue Mod brauchen wir passende neue oder aktualisierte C#-Implementierungen.

## A. Stand der hochgeladenen CoolerPsycastsTweaks.zip

Datenquelle: `1.6/Patches/*.xml`, `1.6/Defs/*.xml` und Klassen-Namen der `1.6/Assemblies/CoolerPsycastsTweaks.dll`. In der XML finden sich Kommentare zu v5/v6/v7/v8; daher ist sie **neuer als die v4-README** im alten Repository.

| Psycast / System | In der ZIP definierter Zustand | Übernahme in Psycaster Level 1–10 |
|---|---|---|
| **Gamma Ray** | **90 Schadenspunkte**, eigene Klasse `DamageWorker_DirectGamma`; direkter Burn-Schaden laut XML-Kommentar; nicht mehr die v4-Angabe 30 Schaden / 300 % AP. | Level 8; 90 als neuer Referenzwert; Logik/Schadenskompatibilität portieren. |
| **Gravity Pulse** | **40 Felder Cast-Reichweite**, Wirkungsradius **14**, Einzug über **14 Felder**. **Drei Pulse à 30 Schaden**, **1000 % AP** (`armorPenetration=10`), **180 Ticks Stun**. Schrittintervall 18 Ticks, Haltezeit 120 Ticks, optische Lichtimpulse. Eigene Klasse `CompProperties_GravityConvergence`. | Level 8; neueren v8-Stand statt v4-Zahlen übernehmen; Bewegung, Blockaden, Schadensereignisse und Optik getrennt testen. |
| **Reverse Gravity** | Eigener Fall-Flyer `CPT_DirectFallingFlyer`, Radius **6**; `CompProperties_DirectFall`. | Level 8; Basis für Hochheben und Fallenlassen. |
| **Learn** | `baseAmount=10000` mit `CompProperties_ChooseSkill`; bestehende Beschreibung im anderen Repository: Fertigkeitswahl und Sensitivitäts-Skalierung. | Level 7; diese Version als Vorgabe, nicht 1.000 XP aus dem Originalmod. |
| **Unmake** | Rekonstruktion von Rezept-/Baukosten über `CompProperties_RecipeUnmake`, **420.000 Ticks = 7 Tage Cooldown**. | Level 10; historisch tatsächlich verbrauchte austauschbare Rezeptzutaten können aus Standard-Itemdaten nicht sicher zurückverfolgt werden. |
| **Reverse Time** | `CompProperties_ResetBody`, **7 Tage Cooldown**; gemäß früherem Nutzerprojekt vollständiger Hediff-Reset, auch positive Zustände / Psylink / Implantate. | Level 9; anders als der neue separate Heilzauber, der nur negative Zustände entfernen soll. Vor Tests Save-Backup. |
| **Ease Gravity** | `MoveSpeed ×1,5`, **60.000 Ticks = 24 h**, **10 % Psyfokus** bei Aktivierung; laufender Drain entfernt. | Referenz für Geschwindigkeitsbuffs; Levelverteilung unserer drei Versionen unabhängig anpassen. |
| **Entropic Focus** | Kontrollierte Regeneration: `focusPerTick=0.0001` und `heatPerTick=0.003`; laut Tooltip 4 Stunden von null bis voll (ohne Unterbrechung). | Level 8. |
| **Embed Psycast** | Psychische Falle hält **60.000 Ticks = 24 h**. | Level 5. |
| **Skill Drain** | Eigene Level-7-Fähigkeit `CPT_CombatSkillDrain`, −4 effektive Shooting- oder Melee-Fähigkeit für **5.000 Ticks** (2 Stunden), ab Grundskill 4; Psyfokus +0,5, Cooldown 1 Tag. Original `CoolPsycasts_SkillDrain` wird wenn vorhanden entfernt. | Level 7; neue Fähigkeit mit **eigenen DefNames** planen, um Doppelungen zu vermeiden. |
| **Mind Control** | `CPT_MindControl`: temporäre Fraktionskontrolle **30.000 Ticks = 12 h**, Cooldown **960.000 Ticks = 16 Tage**, **60 % Psyfokus**, 80 Neuralhitze; ohne Ideology. **Im Add-on derzeit Level 6.** | Im neuen System **auf Level 9 verschieben**, Wirkung beibehalten. Original `CoolPsycasts_Enslave` wird aus dem Altmod entfernt, falls vorhanden. |
| **Timeshunt** | `SafeTimeshunt.xml` ersetzt die `TimeshuntSkyfaller`-Klasse, `GlobalTimeshunt.xml` ersetzt die Ability-Komponente für die Rückkehrlogik. | Übernehmen als Vorbild für sichere/über Karten- und Spielstandsgrenzen hinweg funktionierende Rückkehr; ohne C#-Source noch nicht lauffähig portiert. |
| **Graftskip, Multicast, Reverse Gravity, Reverse Time, Unmake** | Auf reguläre Level 7/8/8/9/10 gesetzt; die originale `ArchotechPsycast`-Spezialextension und Aktivität-Komponente werden entfernt. | Regulär über das freie Level-Auswahlmenü lernen, aber **Level 7–10 nur nach transzendiertem Neuroformer**. |

### Besonderheiten und Konflikte

1. Die **frühere v4-README ist für Gamma Ray und Gravity Pulse überholt**. Bei jeder nachfolgenden Implementierung hat die hochgeladene ZIP Vorrang, sofern keine neuere Nutzerentscheidung vorliegt.
2. Die **XML allein ist kein vollständiger Programmcode**: Die Einträge `CoolerPsycastsTweaks.*` referenzieren Klassen in der beigefügten DLL; kopiert man nur die XML-Dateien in eine neue Mod, werden die Casts nicht funktionsfähig. DLL nicht in derselben Spielinstallation mit doppelter aktiver Mod-ID/Def-Benennung ausliefern.
3. **Mind Control** ist im Add-on Level 6, im aktuellen neuen Entwurf aber Level 9. Für die eigenständige Mod gilt Level 9.
4. **Gravity Pulse** nutzt 1000 % Rüstungsdurchdringung. Das ist ein XML-Konfigurationswert; wie andere Combat-/Armor-Mods damit interagieren, muss separat geprüft werden.
5. **Nicht als Spieltest-Nachweis deklarieren**: Die XML-Dateien ließen sich parsen; das belegt nicht, dass jeder Skill mit sämtlichen RimWorld-1.6-Mods korrekt läuft.
6. Die ursprüngliche Erweiterung ist abhängig von `metalocif.coolerpsycasts` und `brrainz.harmony`; diese Abhängigkeit ist für unsere künftige **eigenständige** Mod möglichst zu vermeiden. Sonst explizit als Optional-/Kompatibilitätsintegration kennzeichnen.

## B. Unterschied in Psycast-Referenzmods(1).zip zum ersten Referenzarchiv

**Beide Archive haben dieselben Pfade**; beim Dateivergleich unterscheiden sich exakt **fünf Dateien**, alle in `3722272756` (More Psycasts – LukaMoria).

| Datei | Unterschied in neuer ZIP |
|---|---|
| `Defs/AbilityDefs/Ability_PerfectSkip.xml` | Psyfokus **0,3 → 0,5**; Cooldown **30.000 → 60.000 Ticks** (ein Spieltag). |
| `Source/AbilityPerfectSkip.cs` | Stark erweiterte Implementierung: Zielplatzierungs-Vorschau (Ghost), Drehung unterstützter Gebäude über Q/E, geplante Teleports mit gespeicherter Drehung, Prüfung freien Platzes vor der Ausführung, Schutz vor Überschreiben am Ziel, Sonderbehandlung von Pflanzen/Monolith-Anbauten. |
| `Languages/English/Keyed/PerfectSkip.xml` | Neue Beschriftung für Rotationshilfe. |
| `Defs/AbilityDefs/Ability_PsychicHealing.xml` | Neuralhitze **20 → 100**; Psyfokus bleibt **0,8**. |
| `Assemblies/MyPsycastMod.dll` | Andere kompilierte DLL; entspricht mutmaßlich der aktualisierten Source, aber ein Buildabgleich wurde nicht durchgeführt. |

**Übernahme:** Neue **Perfect Skip**-Interaktion als Referenz für Level 6 und **Psychic Healing** mit 100 Neuralhitze in die Balance-Planung übernehmen. Der Originalmod-Code gehört dem jeweiligen Urheber; vor Wiederveröffentlichung von C#-Quelltext, DLLs, Grafiken oder XML-Definitionskopien Nutzungsrechte prüfen. Wir können eine eigene Umsetzung nach diesem Verhalten bauen.

## C. Nächste konkrete Implementierung

1. **Level- und Transzendenzsystem** im neuen Projekt unabhängig aufsetzen, freie Fähigkeitenauswahl und Transzendierter-Neuroformer.
2. **Getestete Ausgangsbasis**: jeweils Zielmechanik und Werte aus dem neuen ZIP-Stand priorisieren, insbesondere Learn, Gamma Ray, Gravity Pulse, Reverse Time, Unmake, Mind Control, Timeshunt, Perfect Skip.
3. **C#-Migration:** vorhandenen v4-Quellcode und die neue DLL strukturell vergleichen; fehlende v5–v8-Klassen nachimplementieren statt zu behaupten, dass v4 allein reicht.
4. **Integrationstests** mit realer Spielinstallation (RimWorld 1.6, Royalty, bestehende Mods); danach erst einen Skill als „in neuer Mod getestet“ markieren.
5. **GitHub Actions:** aus eigenen Quellen reproduzierbares, installierbares ZIP erstellen, sobald die Grundarchitektur steht.

## Quellen

- `CoolerPsycastsTweaks.zip`, Nutzerupload vom 16.11.2026: XML und Assemblies; SHA-256 des Archivs `3bf3ee3c6c36c7e51e7c0996d0734899f90c32daa506f0cf158eb8c88c0c701c`.
- `Psycast-Referenzmods(1).zip` und ursprüngliche `Psycast-Referenzmods.zip`, Nutzeruploads; dateibasierter SHA-256-Vergleich der Einträge.
- [Altes Cooler-Psycasts-Tweaks-Repository, README](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks) und [v4-Implementierung](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks/blob/main/docs/v4-Implementierung.md).
