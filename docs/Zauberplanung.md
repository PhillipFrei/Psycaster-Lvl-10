# Zauberplanung – Psycaster Level 1–10

**Status: Entwurf vom 15.11.2026.** Diese Datei dokumentiert die Wünsche, überprüfte Referenzen und **vorgeschlagene** Level/Werte. Nichts in diesem Dokument ist schon als neue Mod implementiert oder spielgetestet.

## Aktueller Quellenstand

**Aktualisiert am 16.11.2026.** Die hochgeladene `CoolerPsycastsTweaks.zip` enthält neuere Änderungen als die zuvor genutzte v4-Dokumentation. Die zweite Referenz-ZIP enthält zudem eine überarbeitete Perfect-Skip-Implementierung. Einzelheiten und Migrations-/Teststatus stehen in **[Importierte Anpassungen](Importierte-Anpassungen.md)**. Die neuen ZIP-Werte ersetzen unten die veralteten Zahlen; sie sind **noch nicht als Teil der neuen Mod gebaut**.

## 1. Kernmechanik

- **Royalty + RimWorld 1.6.** Der Psycaster kann Stufe 1 bis 10 erreichen.
- Bei jedem Psylink-Levelaufstieg wird ein **Auswahlfenster** mit Psycasts geöffnet; der Spieler wählt frei und unabhängig von Klassen. Die Zahl der wählbaren Psycasts pro Aufstieg und mögliche spätere Nachlernmechaniken werden noch festgelegt. Bereits vorhandene Psycasts gehen beim Aufstieg nicht verloren.
- **Level 1–6** werden durch normale Neuroformer freigeschaltet.
- **Level 7–10** benötigen eine Archotech-Umwandlung von Psylink-Neuroformern in **transzendierte Psylink-Neuroformer**. Die Umwandlung kann z. B. an einem Archotech-Objekt stattfinden; das konkret benutzte Gerät und die Kosten sind noch festzulegen. Ein Level-6-Pawn darf erst durch Anwendung eines solchen transzendierten Neuroformers Level 7 erreichen. Für Aufstieg 8–10 gilt weiterhin der transzendierte Weg.
- Der Mod soll möglichst unabhängig von anderen Psycast-Mods sein. Referenzimplementierungen dienen zur technischen Analyse, werden nicht blind kopiert.
- Psylink-Level bezeichnet die Berechtigung zum Lernen; das Ausbalancieren der Effekte ist davon getrennt.

## 2. Einheitliche Balance und Darstellung

- **RimWorld-Zeit:** 60.000 Ticks = 1 Spieltag / 24 Spielstunden; 3 Spieltage = 180.000 Ticks.
- **Stärke:** offensichtliche Verbesserungen, insbesondere Bewegung, Angriffsrate, Lernen, Blutstillung und Heilung; keine Schein-Buffs.
- **Dauer:** Umweltkugeln 3 Tage; mittlere Buffs meist 12–24 Spielstunden; hohe Spezialeffekte nach Bedarf. Ein Ziel soll Wirkzeit, Statänderungen und Restdauer im UI sehen.
- **Visuelle Effekte:** immer mindestens Cast-Impuls am Ziel, optional Strahl/Projektil; bleibende Zauber mit sichtbarem Objekt, Aura oder visueller Zustandsmarkierung. Wirkung nicht nur durch kurze Toast-Meldung anzeigen.
- **Spielbarkeit:** Abklingzeiten pro Pawn, Neuralhitze, Psyfokus, Friendly Fire, Resistenz, Mehrfachzauber, Umschalten in anderen Maps, Save/Load und kompatible Zielauswahl prüfen.
- Vorgeschlagene Zahlen sind **Startwerte**, bis Spieltests sie bestätigen. Bei Skalierung mit psychischer Sensitivität feste Grenzen vorsehen, damit Werte nicht explodieren.

## 3. Geplanter Psycast-Katalog

Pro Zeile: **Vorschlagslevel**, Psycast, Rolle, bestehende Referenz und gewünschte Mechanik. Namen mit „Neu“ sind nicht als existierende Mods identifiziert.

### Level 1 – 9 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Kältekugel | Umwelt | Arctic Pinhole | Sichtbare, beschworene Kugel; kühlt den aktuellen geschlossenen Raum für 3 Spieltage auf Zieltemperatur 16 °C; erneuter Cast ersetzt vorhandene Kugel. |
| Wärmekugel | Umwelt | Supernova Pinhole | Sichtbare, beschworene Kugel; wärmt den aktuellen Raum für 3 Spieltage auf 24 °C; unabhängig von Strom; keine globale Kartentemperaturänderung. |
| Fate Weaving – Einzel | Schutz | Fate Weaving | Ein Pawn entgeht garantiert dem nächsten eigentlich treffenden feindlichen Angriff; Wirkung bis Verbrauch oder 12 Stunden. |
| Ignite | Feuer | Ignite | Entzündet ein Ziel/Feld mit deutlichem Flammeneffekt; geringe Kosten. |
| Haemostasis – Blutstillung | Heilung | Haemostasis | Alle bestehenden Blutungen des Ziels sofort auf **0**; stabilisiert, heilt offene Wunden aber nicht; neuer Schaden muss ggf. neu stabilisiert werden. |
| Geschwindigkeit I | Buff | Dash / Ease Gravity | Bewegungsgeschwindigkeit +25 % für 12 Spielstunden; auffälliger Laufspur-Effekt. |
| Healing Boost I | Heilung | Healing Boost | Heilungsrate ×1,5 für 12 Stunden; zusätzlich akute Blutungen vermindern, aber nicht als Ersatz für Haemostasis. |
| Despair | Debuff | Despair | Einzelziel: spürbarer Stimmungsabzug, etwa −20 für 6 Stunden. |
| Brickgate | Utility | Brickgate | Steinbrocken sofort zu den zugehörigen Steinblöcken verarbeiten; keine Materialduplikation. |

### Level 2 – 10 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Flammenschuss | Feuer | Neu aus Ignite/Engulf | Gezieltes Feuerprojektil; direkte Trefferwirkung und Brandchance; kurze Abklingzeit. |
| Guidance | Lernen | Guidance | Lernratenfaktor ×2 für 24 Stunden; ohne sofortige Erfahrung. |
| Psychic Calm | Stimmung | Psychic Calm | Sofortige Beruhigung und +20 Stimmung für 12 Stunden; kein dauerhafter Trait-Eingriff. |
| Beast Bond | Tiere | Beast Bond | Temporäre Kontrolle über ein Tier für 24 Stunden; verbotene oder questkritische Tiere gesondert behandeln. |
| Chemfuelskip | Utility/Kampf | Chemfuelskip | Entzündbaren Chemfuel-Effekt in einer Zielzone erzeugen; mit Ignite kombinierbar. |
| Distortion | Kontrolle | Distortion | Sicht-/Schusslinienverzerrung; Gegner können über Entfernung schlechter oder nicht zielen. |
| Induce Rain | Wetter | Induce Rain | Regen auslösen; Wetterregeln der Karte berücksichtigen. |
| Trapraise | Kampf | Trapraise | 2–4 temporäre Fallen in einer Zielzone; Schaden, Lebensdauer und Verbündete-Sicherheit konfigurierbar. |
| Extinguish | Utility | Extinguish | Großflächig Feuer löschen, kurze Abklingzeit; zunächst Radius etwa 8 Zellen. |
| Stun – Einzel | Kontrolle | Stun Pulse / Vanilla Stun | Ein Gegner wird kurz betäubt; Immunitäten und erneute Betäubung berücksichtigen. |

### Level 3 – 10 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Geschwindigkeit II | Buff | Dash / neu | Bewegung ×1,5; Nahkampf- und Fernkampf-Angriffstempo ×1,25 für 12 Stunden. |
| Fire Shield | Schutz | Fire Shield | Schützt 24 Stunden vor Entzündung, Hitze und ausgewählten Brandschäden. |
| Kinetischer Schild I | Schutz | Neu | Absorbiert einen begrenzten physischen Schadensvorrat (z. B. 80 Schaden) oder läuft nach 12 Stunden ab. |
| Frostbite | Angriff | Frostbite | Akute Kälte-/Erfrierungswirkung auf ein Ziel; sichtbarer Eisstoß. |
| Thermal Shock | Angriff | Thermal Shock | Akute Hitze-/Hitzeschockwirkung auf ein Ziel; sichtbare Hitzewelle. |
| Mass Burden | Kontrolle | Mass Burden | Gegner in kleinem Radius stark verlangsamen, z. B. −50 % Bewegung für 2 Stunden. |
| Stun Pulse | Kontrolle | Stun Pulse | Kurze Flächenbetäubung, z. B. Radius 4 Zellen. |
| Entropic Mend | Reparatur | Entropic Mend | Beschädigte Kleidung/Rüstung/tragbare Gegenstände reparieren; beim Neubau Qualitätsverlust wenn sinnvoll vermeiden, stattdessen Kosten/Cooldown. |
| Arbeitseifer | Buff | Neu / Word of Vigor | Allgemeine Arbeitsgeschwindigkeit ×1,5 für 24 Stunden; kein extrem kurzer Mikro-Buff. |
| Comfort Shield | Schutz | Comfort Shield | Schützt vor extremen Außentemperaturen, ohne einen Raum zu klimatisieren. |

### Level 4 – 10 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Fate Weaving – Gruppe | Schutz | Fate Weaving / neu | Alle verbündeten Pawns in kleinem Radius erhalten jeweils einen garantierten Fehlschlag des nächsten Treffers. |
| Awaken | Heilung/Utility | Awaken | Weckt bewusstlose, narkotisierte oder aus bestimmten Koma-Zuständen betroffene Pawns, soweit reversibel; Schlafbedürfnis auffüllen. |
| Healing Boost II | Heilung | Healing Boost + Immunity Boost | Heilungsrate ×3, Immunitätsgewinn ×2, Dauer 24 Stunden; erhebliche Blutungsreduktion. |
| Dart – Weltraumschrott | Angriff | Dart | Gezielter starker Einschlag aus dem Himmel; begrenzter Radius mit Warn-/Einschlag-Effekt. |
| Rüstungsbruch | Debuff | Dismantle / neu | Schädigt getragene Rüstung und halbiert für 6 Stunden die wirksame Rüstungsleistung; kein direkter Angriff auf Körperteile. |
| Vanometric Charge | Utility | Vanometric Charge | Mechanoid-Akku/Batterien laden; feindliche Mechs bei Zielwahl ggf. überladen. |
| Timeshunt | Kontrolle | Timeshunt | Ein Ziel mehrere Spielstunden aus dem aktuellen Zeitfluss versetzen; danach an gültiger Position zurück. |
| Skipscreen | Schutz | Skipscreen | Stationäre Schutzblase gegen schwere Geschosse und Mörsergranaten; keine universelle Kugelabwehr. |
| Mass Stun | Kontrolle | Stun Pulse / neu | Stärkerer Stun über größere Fläche als Level 3; längere Abklingzeit. |
| Strip | Kontrolle | Strip | Entfernt ausgewählte Kleidungs- und Rüstungsstücke eines Ziels; Inventar und Quest-Ausrüstung prüfen. |

### Level 5 – 12 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Potential Unleashed | Buff | Potential Unleashed | Körperkraft +50 %, Nahkampfschaden +40 %, Angriffstempo +25 %, Schmerz −50 %; 6 Stunden und danach Erschöpfung. |
| Arbeitseifer II | Buff | Neu | Arbeitsgeschwindigkeit ×2 für 24 Stunden; keine unmöglichen Tick-/Job-Interaktionen erzwingen. |
| Illusion | Täuschung | Illusion | Steuerbare Illusion mit eindeutig erkennbarer Erscheinungs- und Auflösungsanimation. |
| Phase | Bewegung | Phase | Zeitweise durch Hindernisse/Wände bewegen; Sicherheit bei Auslaufen des Effekts. |
| Skipblade | Waffe | Skipblade | Beschworene Psi-Nahkampfwaffe mit klarer Dauer und Qualitätsskala. |
| Execute | Angriff | Execute | Einziel-Finisher mit kurzer Reichweite; Resistenzregeln für Boss-/Questziele. |
| Psychic Feedback | Psi-Angriff | Psychic Feedback | Schaden steigt mit psychischer Sensitivität des Gegners; bei hoher Neuralhitze Zusatzreaktion. |
| Echo | Beschuss | Echo | Vervielfacht verbündete Projektile durch einen zeitweiligen Skip-Spalt; keine unbegrenzte Projektilschleife. |
| Extend | Metamagie | Extend | Erhöht die Reichweite des nächsten geeigneten Psycasts deutlich; inkompatible Effekte ausschließen. |
| Embed Psycast | Metamagie | Embed Psycast | Verankert einen bekannten Psycast 24 Stunden als sichtbare psychische Falle. |
| Jitterskip | Schutz/Bewegung | Jitterskip | Automatisches Ausweichen bei Projektil-/Nahkampftreffern, mit Psyfokusverbrauch pro Auslösung. |
| Wohnkomfort | Versorgung | Neu aus Word of Vigor | Füllt Komfort und Erholung/Freizeit teilweise und verbessert Stimmung; eine Vorstufe des späteren Vollzaubers. |

### Level 6 – 10 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Geschwindigkeit III | Buff | Neu / Dash | Bewegung ×2,5; Nah- und Fernkampftempo ×1,75 für 24 Stunden; sichtbare dauerhafte Aura. |
| Deep Regeneration | Heilung | Deep Regeneration | Heilt schwere Verletzungen über längere Zeit; umfasst ausgewählte alte Verletzungen/Narben. |
| Perfect Skip | Teleport | Perfect Skip | Neue Referenz-ZIP: drehbare Gebäude-Platzierungsvorschau (Q/E), zielgenaues Versetzen, Prüfung freien Platzes und Behandlung von Pflanzen/Monolith-Anbauten; **0,5 Psyfokus, 1 Tag Cooldown**. |
| Skiprifle | Waffe | Skiprifle | Beschworene Psi-Fernkampfwaffe. |
| Organ Skip | Heilung/Kampf | Organ Skip | Organmanipulation/Organtransfer gemäß Referenzfunktion; vor Umsetzung genaue Ziel- und Folgenlogik klären. |
| Firestorm | Feuer | Firestorm | Großer, schadensstarker Flächen-Feuerangriff statt nur einzelner Brandstellen. |
| Mass Reflect | Schutz | Mass Reflect | Schickt geeignete feindliche Geschosse im Bereich zu ihren Absendern zurück. |
| Psychic Healing | Heilung | Psychic Healing | Repariert eine schwere chronische Erkrankung, dauerhafte Verletzung oder fehlendes Körperteil. Neue Referenz-ZIP: **100 Neuralhitze** statt 20; 80 % Psyfokus. |
| Healing Bloom | Heilung | Healing Bloom | Große Heilungs-/Immunitäts-Aura für Verbündete in einem Gebiet; starke skalierbare Wirkung. |
| Fertility Skip (?) | Offen | Fertility Skip (Referenz) | Der diktierte Name „Fatality Skip“ ist nicht im Referenzkatalog; vor Freigabe klären, ob Fertility Skip gemeint war. |

### Level 7 – 8 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Learn – 10.000 XP | Lernen | Learn / bestehendes Tweaks-Projekt | 10.000 Basis-XP für eine auswählbare Fertigkeit, anschließend psychische Sensitivität als Multiplikator wie bestehendes Tweaks-Projekt. |
| Meteor | Angriff | Meteor | Gezielter Meteoriten-Einschlag, mit entsprechend kräftiger Schadens- und Zerstörungswirkung. |
| Portal | Transport | Portal | Langlebiger Teleportationsdurchgang für Fernreisen; Transport- und Kartengrenzen beachten. |
| Healing Bloom – Transzendent | Heilung | Healing Bloom / neu | Verstärkte Flächenregeneration und Immunitätsbeschleunigung, über Level 6 hinaus. |
| Graftskip | Metamagie | Graftskip | Überträgt passende Verletzungen/Schäden eines Ziels auf ein anderes; Schutz vor ungültigen Körperteilen. |
| Skill Drain | Kampf | Bestehendes Tweaks-Projekt | Temporärer Shooting-/Melee-Malus (bestehender Ansatz −4 für 2 Spielstunden), optional Psyfokusgewinn für den Zauberer. |
| Entomb | Kontrolle | Entomb | Schließt ein Ziel kurzfristig mit beschworenen Wänden ein; Rettungs-/Ausgangsregeln definieren. |
| Despair Pulse | Psi-Angriff | Despair Pulse | Starker Flächen-Despair; anstelle mehrerer konkurrierender großer Despair-Versionen. |

### Level 8 – 8 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Gamma Ray | Angriff | Bestehendes Tweaks-Projekt | **Neuester ZIP-Stand:** 90 direkte Burn-Schadenspunkte mit eigenem DamageWorker. Die alte v4-Angabe 30 Schaden / 300 % AP ist überholt. C#-Port und Verträglichkeit mit Rüstungsmods prüfen. |
| Gravity Pulse | Kontrolle/Angriff | Bestehendes Tweaks-Projekt | **Neuester ZIP-Stand:** Cast-Reichweite 40, Radius 14, Zugdistanz 14, **3 × 30 Schaden** mit 1000 % AP; 180 Ticks Stun, sichtbar pulsierende Gravitation, fließender Einzug. Eigene v8-C#-Klasse erforderlich. |
| Reverse Gravity | Kontrolle/Angriff | Bestehendes Tweaks-Projekt | Kurz hochschleudern und nach Fall Schlag-/Fallschaden; Radius 6, normale Trefferverarbeitung (zu testen). |
| Entropic Focus | Psyfokus | Bestehendes Tweaks-Projekt | Psyfokus von 0 auf 100 % in 4 Spielstunden bei ununterbrochener Wirkung; erzeugt kontrollierte Neuralhitze. |
| Multicast | Metamagie | Multicast | Einen kompatiblen Psycast gleichzeitig auf mehrere Pawns der Zielgruppe anwenden. |
| Psychische Barriere | Schutz | Neu | Ziel-Pawn ist während der Wirkzeit gegen feindliche direkte Psycasts geschützt; Fläche/indirekte Effekte separat behandeln. |
| Vollständige Versorgung | Stimmung/Bedürfnisse | Neu | Füllt Komfort, Erholung und weitere geeignete Bedürfnisse sofort, hebt Stimmung deutlich, lange Abklingzeit; keine Hunger-/Krankheitsheilung unter diesem Namen. |
| Kinetischer Schild II | Schutz | Neu | Großer Schutzvorrat, wehrt schwere Fernkampf-/Nahkampftreffer ab; stärkere Version des Schilds auf Level 3. |

### Level 9 – 7 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Mind Control | Kontrolle | Bestehendes Tweaks-Projekt | Temporäre echte Kontrolle über einen Gegner für 12 Stunden, 16 Tage Abklingzeit gemäß Tweaks-Projekt; Fraktionswechsel robust abwickeln. |
| Reverse Time | Zeit/Heilung | Bestehendes Tweaks-Projekt | Bestehender Totalreset: entfernt sämtliche Hediffs einschließlich positiver, künstlicher Implantate, Psylink/Mechlink; stellt fehlende Körperteile wieder her; 7 Tage Cooldown. |
| Annihilate | Angriff/Karte | Annihilate | Mächtige, dauerhafte Geländeveränderung/Zerstörung; Schutz vor Quest-/Karten-Softlocks. |
| Große Heilung – Reinigung | Heilung | Neu aus Psychic Healing | Entfernt sämtliche **negativen** Gesundheitszustände einschließlich dauerhafter Verletzungen und schwerer Krankheiten; positive Hediffs bleiben erhalten; 3 Tage Cooldown als Startwert. |
| Resurrect | Heilung | Resurrect | Wiederbelebung mit sehr hoher Neuralhitze und mehreren Tagen Cooldown; Biotech-/Rassen-Ausnahmen testen. |
| Execution – Fernwirkung | Angriff | Execute / neu | Größere Reichweite und stärkere Finisher-Variante, mit besonderer Optik und langer Abklingzeit. |
| Archofeuerstrahl | Feuer | Neu aus Firestorm | Extrem starker gebündelter Feuerstrahl mit deutlicher Vorwarnung, erheblichen Schäden und langer Abklingzeit. |

### Level 10 – 3 Zauber

| Fähigkeit | Rolle | Bezug | Vorgesehene Funktion / Startwerte |
|---|---|---|---|
| Unmake | Ressourcen/Karte | Bestehendes Tweaks-Projekt | Vollständige Rekonstruktion rekonstruierbarer Rezeptzutaten/Baukosten, 7 Tage Cooldown; Originalmaterial bei austauschbaren Rezeptzutaten nicht immer rekonstruierbar. |
| Archotech-Kataklysmus (Vorschlag) | Endgame-Angriff | Neu | Großflächige Kombination aus Meteor-/Gravitations-/Feuerwirkung; sehr starke Leistung, lange Vorwarnung und etwa 7 Tage Cooldown. |
| Transzendente Kausalität (Vorschlag) | Endgame-Zauber | Neu | Ein extrem seltener großflächiger Realitätseingriff mit klarer Unterscheidung von normaler Heilung, z. B. einmalige Rettung eigener Pawns vor tödlichem Schlag. |

## 4. Weitere ausdrücklich gewünschte Bestandteile (noch nicht einsortiert)

| Wunsch | Plan |
|---|---|
| **Fate Weaving** für Einzelperson und Gruppe | Beide Varianten enthalten (Level 1 und 4). |
| **Schutz gegen alle psychischen Angriffe** | Level 8; die Erkennung direkter Psycasts ist technisch relativ klar, Flächen-/indirekte Schäden müssen separat abgesichert werden. |
| **Sehr starke Reflexionsschilde** | Mass Reflect auf Level 6, kinetischer Schild II Level 8. |
| **Feuer löschen, viel Fläche, niedriger Cooldown** | Extinguish Level 2. |
| **Alle negativen Gesundheitszustände entfernen** | Level 9: große Heilung; ausdrücklich **anders als Reverse Time**, weil positive Zustände erhalten bleiben sollen. |
| **Pawns dauerhaft schneller arbeiten lassen** | Arbeitseifer Level 3, Arbeitseifer II Level 5. |
| **Psycast-Fertigkeit beeinflusst Genauigkeit** | Bei Feuer/Schaden/Heilung technische Option, noch keine generelle Regel beschlossen. |
| **„Potential Unleashed“ soll konkrete Stats beeinflussen** | Entwurf: +50 % Körperkraft, +40 % Nahkampfschaden, +25 % Angriffstempo, −50 % Schmerz für 6 h + Erschöpfung. Stats technisch auf RimWorld-Typen mappen. |
| **„Grant Psycast“** | **Nicht übernehmen.** Stattdessen echte eigenständige Level-10-Fähigkeit. |
| **„Rewrite Mind“** | Vorläufig **Reserve**, nicht Kernkatalog. |
| **„Despair Pulse“ statt doppeltem starkem Despair** | Einzelfassung Level 1; starke Flächenfassung Level 7. |
| **„Fatality Skip“** | Unklarer Diktatname: Die Referenzliste enthält **Fertility Skip**, keine Fähigkeit „Fatality Skip“; bitte vor Umsetzung verifizieren. |
| **„Orb Skip“** | Möglicherweise „Organ Skip“, die Referenz enthält nur Letzteres; Funktion vor Programmierung präzisieren. |
| **„And Pomp and Tomp“** | Nicht eindeutig zuordenbar; „Entomb“ ist separat in Level 7 aufgenommen, ohne eine Gleichsetzung zu behaupten. |

## 5. Technische Besonderheiten und offene Prüfungen

1. **Raumkugeln:** als eigene `ThingWithComps`-Objekte oder Gebäude-ähnliche Dinge mit begrenzter Lebensdauer. Wirkung auf den **tatsächlichen Room/Region-Temperaturwert**, nicht auf Umgebungsluft der gesamten Karte. Sobald sich der Raum durch Umbauten teilt/öffnet, Raumbezug neu bestimmen. Übermäßige Temperaturänderung nicht bei jedem Frame ungebremst addieren. Cast + Kugel + Raumluft-Effekt müssen sichtbar sein.
2. **Haemostasis:** `BloodLoss` soll durch bestehende Verletzungen nicht weiter anwachsen, solange die Stabilisierung gilt. Dafür muss die tatsächliche Blutungsrate effektiv auf 0 gesetzt werden. Ein reiner Heilungsratenbonus reicht ausdrücklich **nicht**. Bei neuem Schaden oder Ablauf klare Regeln.
3. **Angriffsgeschwindigkeit:** die relevanten RimWorld-Stats für Nahkampf und Fernkampf sind getrennt; sowohl Cooldown als auch Animation, Kampfmods und ausgeführte Jobs müssen berücksichtigt werden. Eine einzige `MoveSpeed`-Erhöhung reicht nicht.
4. **Fate Weaving:** nächsten passenden Treffer gezielt abfangen. Gruppenvariante gibt jedem Ziel einen einzelnen eigenen Schutz, nicht einen einzigen Schutz für die gesamte Gruppe.
5. **Rüstungsbruch:** tatsächliche Schutzberechnung auf getragene Rüstung reduzieren, nicht nur deren sichtbare HP. Rüstungsschäden/-malus müssen auch beim Ablegen/Anlegen sauber funktionieren.
6. **Schilde:** eigene Treffererkennung je Kategorie (Projektile, Nahkampf, explosiv, Psycast), Ausnahmen und Friendly Fire sauber regeln. Psycast-Immunität ist keine einfache XML-Stat.
7. **Reverse Time:** bestehende Nutzerimplementierung löscht **auch gute** Hediffs, Bionik, Psylink und Mechlink. Das ist absichtlich **kein** reiner Heilzauber. Die Arbeit an dieser Fähigkeit braucht ausdrücklich Save-/Restore-Tests.
8. **Unmake:** historische tatsächlich verbrauchte Rezeptzutaten sind im fertigen Item normalerweise nicht vollständig gespeichert. Bestehende Nutzerimplementierung liefert möglichst rekonstruierte Rezeptkosten; bei austauschbaren Zutaten ist ein exaktes historisches Zurückgeben nicht nachweisbar.
9. **Mind Control:** bestehenden 12-Stunden-Fraktionswechsel aus der neueren ZIP als Ausgangspunkt analysieren; dort ist Mind Control **Level 6** und hat **16 Tage Cooldown**, im neuen Mod wird es **Level 9**. Quest-Pawns, Gefangene, Mechs, Fraktionsbeziehungen und Aftereffects testen.
10. **Bestehende Tweaks:** im Repo [Cooler-Psycasts-Tweaks](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks) steht älterer v4-Quellcode. **Neuere Werte und neue DLL-Klassen stammen aus dem hochgeladenen Add-on-ZIP** und sind in [Importierte Anpassungen](Importierte-Anpassungen.md) dokumentiert. Darin fehlen die C#-Quelldateien der neueren Version; Änderungen nicht blind aus v4 übernehmen.
11. **Rechte und Wartbarkeit:** keine ungeprüft fremden Assemblies, Grafiken oder C#-Quelldateien direkt in dieses öffentliche Repository hochladen. Nachimplementierung / erlaubte Nutzung klären. Eigene IDs/Namensräume und optionale Kompatibilitätspatches verwenden.

## 6. Architektur und Reihenfolge

### Meilenstein 1 – spielbarer Kern
- Mod-Metadaten, XML-Def-Grundstruktur, C#-Projekt, GitHub Actions (buildbares ZIP).
- Psylink-Level 1–10 und Neuroformerumwandlung 6→7 inkl. Level 8–10.
- Auswahlmenü statt zufälliger Psycast-Vergabe.
- 5 vertikale Durchstiche: Kältekugel, Haemostasis, Geschwindigkeit I, Guidance, Ignite.

### Meilenstein 2 – Buffs und Umwelt
- Wärmekugel, alle Geschwindigkeits-/Arbeitsbuffs, Fate Weaving, Stimmung, Heal Boost.
- Visuals, Buff-Ablauf, Room-Handling, UI-Wirkungswerte.

### Meilenstein 3 – Kampf und Schutz
- Feuerangriffe, Frostbite/Thermal Shock, Rüstungsbruch, Stuns, Schilde, Echo, Distortion.
- Friendly Fire, Zauber-Gruppen, Balance, Angriffsgeschwindigkeit.

### Meilenstein 4 – Endgame und Kompatibilität
- Learn, Portal, Meteor, Mind Control, Reverse Time, Unmake, Annihilate, Level-10-Spezialzauber.
- Kompatibilität mit bereits benutzten Psycast-Mods, save-safe Migration, Spieltests auf RimWorld 1.6.

## Quellenbasis und Status

- Vom Benutzer hochgeladen: `Psycast-Referenzmods.zip`, XML und teilweise C# der Psycast-Mods; vorhandener `Psycast-Katalog.csv` und `ModsConfig.xml`.
- Verbundenes GitHub: [Cooler-Psycasts-Tweaks / v4](https://github.com/PhillipFrei/Cooler-Psycasts-Tweaks/blob/main/docs/v4-Implementierung.md).
- Alle nicht als verifiziert gekennzeichneten Zahlen und neuen Zauber sind **Vorschläge**, keine Behauptungen über Originalmod-Funktionen.
- Die neue Mod ist **noch nicht implementiert**.
