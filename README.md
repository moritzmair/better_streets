# Straßenskizze

Einzelne HTML-Datei, kein Build, keine Abhängigkeiten außer Google Fonts.
`index.html` im Browser öffnen – fertig.

## Ablauf

1. **Luftbild laden** – Datei wählen, ins Fenster ziehen oder mit `Strg/Cmd+V` einfügen.
2. **Maßstab setzen** – zwei Punkte mit bekanntem Abstand anklicken, Länge in Metern eintragen.
   Erst danach stimmen die vorgegebenen Breiten. Späteres Nachkalibrieren skaliert den Entwurf mit.
3. **Zeichnen** – Werkzeug links wählen, Punkte klicken, `Doppelklick`/`Enter` beendet den Zug.
   Breiten sind als Planungsmaße vorbelegt und pro Element im Inspektor änderbar.

## Kurven und Radien

Jeder Zug hat eine Kurvenführung:

* **Weich** (Vorgabe) – zentripetaler Catmull-Rom-Spline durch alle Punkte. Der kleinste
  Krümmungsradius wird numerisch aus der Kurve bestimmt.
* **Bogen** – an jeder Ecke ein Kreisbogen mit festem Radius (Bordstein-/Kurvenradius).
  Vorbelegt: Kfz 6 m, Bus 12 m, Rad 10 m, Fuß 3 m. Radius 0 ergibt spitze Ecken.
  Reicht die Schenkellänge nicht, wird der Bogen verkleinert – der Inspektor zeigt dann
  den tatsächlich erreichten Radius.

Liegt ein Radius unter dem Richtwert des Typs (Kfz 5 m, Bus 10 m, Radweg einspurig 2,5 m, übrige Radanlagen 5 m, Fuß 1,5 m),
markiert die Prüfung die Stelle im Bild mit dem gemessenen Radius. Über „Radien" abschaltbar;
im Export sind die Marken nie enthalten. Beim Kreisverkehr ordnet der Inspektor den
Außendurchmesser ein (Mini 13–22 m, klein 26–40 m).

Die Werte sind Orientierungswerte aus der Entwurfspraxis (RASt/ERA-Größenordnung),
keine Normprüfung – im Zweifel das Regelwerk heranziehen.

## Wege ändern

Ist ein Weg ausgewählt, erscheinen orange **+**-Marken:

* **+ am Ende** verlängert den Weg – weitere Punkte klicken, `Enter` beendet. Hängen dort
  gekoppelte Nachbarspuren, wachsen sie mit; das Verlängern greift immer an der Bezugsspur an.
* **+ zwischen zwei Punkten** setzt dort einen Wegpunkt. Er liegt auf der bestehenden Kurve,
  die Form ändert sich also nicht – erst das Ziehen des neuen Griffs verändert sie.

## Markierungsabschnitte

Das Werkzeug **Trennen** teilt einen Weg in Abschnitte, ohne ihn geometrisch zu zerschneiden:
die Linienführung bleibt eine durchgehende Kurve, nur die Markierung darf ab dort anders sein –
etwa Leitlinie auf der freien Strecke, durchgezogen vor der Kreuzung.

Klick auf den Weg setzt eine Trennstelle, Klick auf eine bestehende hebt sie auf. Beim
Auswählen bestimmt die angeklickte Stelle, welcher Abschnitt im Inspektor bearbeitet wird:
er wird auf der Karte eingefärbt und beschriftet („Abschnitt 2/3"), seine Trennstellen
stehen kräftig, die übrigen blass. Gekoppelte Nachbarspuren übernehmen die Trennstellen, damit
die gemeinsame Linie auf beiden Seiten gleich läuft.

## Markierungen

Jede Linie hat drei Markierungsspuren – **links, Mitte, rechts** – jeweils: keine,
gestrichelt (3 m / 6 m), gestrichelt kurz (1 m / 1 m), durchgezogen (0,12 m) oder
breit durchgezogen (0,25 m). Vorbelegt nach Typ:

| Typ | Vorgabe |
|---|---|
| Fahrspur, Parkstreifen | außen durchgezogen |
| Busspur | beidseitig breit |
| Radfahrstreifen | links breit durchgezogen |
| Schutzstreifen | links gestrichelt kurz |
| Radweg 2-Richtung | Mittellinie gestrichelt kurz |
| Gehweg, Grünstreifen, Radweg | keine |

Parkstreifen bekommen Stellplatzteiler (quer 2,5 m, längs 5,5 m), die Sperrfläche
eine Schraffur. Der Fußgängerüberweg wird von Bordstein zu Bordstein gezeichnet; seine
Streifen liegen quer zur Gehrichtung, also parallel zur Fahrbahnachse, und sind 4 m tief.
Radverkehrsanlagen sind grün eingefärbt.

## Fahrtrichtungspfeile

Das Werkzeug **Fahrtrichtungspfeil** (Kfz-Verkehr) setzt einen Pfeil auf eine Fahrspur:
Klick auf die Spur genügt, der Pfeil richtet sich nach ihrer Richtung und sitzt auf der
Achse. Sechs Formen im Inspektor: geradeaus, links, rechts, geradeaus + links,
geradeaus + rechts, links + rechts. „Umdrehen" dreht ihn um 180°, wenn die Spur gegen die
Fahrtrichtung gezeichnet wurde; die Länge ist einstellbar (Vorgabe 5 m).

Der Pfeil hängt an seiner Spur: Ziehen verschiebt ihn *entlang* der Spur, Formänderungen der
Spur nimmt er mit, und mit der Spur wird er gelöscht. Seine seitliche Ausdehnung wird auf die
Fahrbahnbreite begrenzt, damit Abbiegepfeile nicht über den Rand ragen. Pfeile lassen sich
nur auf Fahrspuren und Busspuren setzen, nicht auf Rad- oder Gehwegen.

## Querungen

Wege haben einen Rang: Kfz (1) < Rad (2) < Fuß (3). Überquert ein Weg eine rangniedrigere
Anlage, wird die Überlappung automatisch als Querung gezeichnet statt als eigener Belag:

* **Radweg über Fahrbahn** – kein grüner Belag mehr, sondern eine Furt: zwei Reihen weißer
  Blöcke (0,5 m / 0,5 m) an den Rändern der Querung.
* **Gehweg über Fahrbahn oder Radweg** – Zebrastreifen in der Breite des Gehwegs, an jeder
  gequerten Anlage einzeln.

Die Randmarkierungen des querenden Wegs setzen dort aus. Erkannt wird die Überlappung
geometrisch, also auch bei Kurven und schrägen Querungen. Pro Element abschaltbar über
„Querung über Fahrbahn/Radweg" im Inspektor – dann wird wieder durchgehend Belag gezeichnet.

## Kreisverkehr

Der Kreisverkehr liegt über den Zufahrten: eine Fahrspur, die zu weit hineinreicht, wird von
Kreisfahrbahn und Insel überdeckt statt sie zu überzeichnen. Die Markierungen der Zufahrten
enden am Außenrand des Kreises, und die Außenlinie des Kreises reißt an jeder Zufahrt auf.

## Ebenen

Die Zeichenreihenfolge hängt am Typ, nicht an der Reihenfolge des Zeichnens:

| | |
|---|---|
| 10 | Grünflächen, Aufenthaltsflächen, Grünstreifen |
| 20 | Kfz: Parken, Fahrspuren, Kreisverkehr, Busspur |
| 30 | Rad: Schutzstreifen, Radfahrstreifen, Fahrradstraße, Radweg |
| 40 | Fuß: Gehwege |
| 50 | Markierungsflächen: Verkehrsinsel, Sperrfläche |
| 60 | Fußgängerüberwege |
| 70 | Bäume |

Ein später gezeichneter Gehweg liegt also immer über der Fahrbahn, eine Grünfläche immer
darunter – unabhängig davon, wann sie entstanden sind.

## Spuren nebeneinander

Zwei Wege, eine Spur bündig an die nächste zu legen:

* **Kantenfang** – beim Zeichnen und beim Ziehen rastet ein Punkt in der Nähe einer Spur
  auf den bündigen Achsabstand ein (halbe Breite + halbe Breite). `Alt` hebt den Fang auf.
* **Nachbarspur** – im Inspektor „◀ links / rechts ▶". Die neue Spur ist an ihre Bezugsspur
  **gekoppelt**: sie übernimmt deren Form, Kurvenführung und Breitenänderungen über die
  ganze Länge. Zwischen zwei Kfz-Spuren wird dabei automatisch eine Leitlinie gesetzt;
  ändert man die Linie auf der gemeinsamen Kante, zieht die Nachbarspur mit. Über die Typwahl wird daraus z. B. ein Radweg, der Abstand passt sich der
  neuen Breite an.

Die Kopplung löst sich, sobald du einen Punkt der Nachbarspur ziehst – ab da läuft sie frei
(Abbiegespur, ausschwenkender Radweg). „lösen" trennt sie ohne Bewegung.

## Bedienung

| Aktion | |
|---|---|
| Zug beenden | Doppelklick, `Enter` oder Rechtsklick |
| Abbrechen / Auswahlwerkzeug | `Esc`, `V` |
| Löschen | `Entf` |
| Rückgängig / Wiederholen | `Strg+Z` / `Strg+Umschalt+Z` |
| Karte verschieben | `Leertaste` + Ziehen oder mittlere Maustaste |
| Zoomen | Mausrad |
| Winkel einrasten (15°) | `Umschalt` beim Zeichnen |
| Fang aussetzen | `Alt` |
| Vorher/Nachher | `H` |

Endpunkte fangen automatisch an vorhandenen Punkten – so schließen Fahrbahnen bündig an.
Der Stand wird laufend im Browser (localStorage) gesichert, inklusive Luftbild bis ca. 3,5 MB.

## Skizzen speichern und weitergeben

Über **Skizzen** in der Kopfzeile:

* **Im Browser** – Entwurf unter einem Namen ablegen; die Liste zeigt Datum, Anzahl der
  Elemente, ob ein Luftbild dabei ist und wie groß der Eintrag ist. Gleicher Name überschreibt.
  Reicht der Platz für das Luftbild nicht (localStorage fasst je nach Browser rund 5 MB),
  wird die Skizze ohne Bild gesichert und das gesagt.
* **Als Datei speichern** – `.json` mit Geometrie, Maßstab und, wenn vorhanden, dem Luftbild.
  Lokal läuft das über einen Blob-Download; eingebettet (als claude.ai-Artifact) über die
  `downloads`-Fähigkeit der Laufzeit, bei der die Betrachterin den Speichervorgang bestätigt.
  Steht beides nicht zur Verfügung, verschwindet der Knopf und „JSON kopieren" führt zum Ziel.
  Der Bild-Export bietet denselben Weg an.
* **Datei laden…** oder **JSON einfügen** – lädt eine Skizze zurück, egal ob aus Datei oder
  Zwischenablage. Beim Laden wird ein Undo-Punkt gesetzt, `Strg+Z` bringt den vorherigen
  Stand zurück.

Unabhängig davon sichert die Seite den aktuellen Stand weiterhin automatisch, damit nach dem
Schließen des Tabs nichts verloren geht.

## Export

„Bild exportieren" rendert Luftbild + Entwurf in Originalauflösung (max. 4000 px).
Bild per Rechtsklick speichern oder in die Zwischenablage kopieren.

## Projekt

Ein Projekt von **Moritz Mair**.
Wenn es dir weiterhilft: [Kaffee spendieren](https://www.paypal.com/paypalme/moritzmair) ☕
