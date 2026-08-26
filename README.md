# Straßenskizze

Einzelne HTML-Datei, kein Build, keine Abhängigkeiten außer Google Fonts.
`index.html` im Browser öffnen – fertig.

## Ablauf

1. **Luftbild laden** – Datei wählen, ins Fenster ziehen oder mit `Strg/Cmd+V` einfügen.
2. **Maßstab setzen** – zwei Punkte mit bekanntem Abstand anklicken, Länge in Metern eintragen.
   Erst danach stimmen die vorgegebenen Breiten. Späteres Nachkalibrieren skaliert den Entwurf mit.
3. **Zeichnen** – Werkzeug links wählen, Punkte klicken, `Doppelklick`/`Enter` beendet den Zug.
   Breiten sind als Planungsmaße vorbelegt und pro Element im Inspektor änderbar.

## Kurven

Jeder Zug hat eine Kurvenführung:

* **Weich** (Vorgabe) – kubische Bézier durch alle Stützpunkte. Jeder Punkt hat eine
  Tangente: ohne eigene Einstellung wird sie aus den Nachbarpunkten abgeleitet, sonst
  bestimmt sie Richtung und Stärke der Kurve.
* **Bogen** – an jeder Ecke ein Kreisbogen mit festem Radius (Bordstein-/Kurvenradius).
  Vorbelegt: Kfz 6 m, Bus 12 m, Rad 10 m, Fuß 3 m. Radius 0 ergibt spitze Ecken.

**Kurve aufziehen:** Beim Setzen eines Punktes gedrückt halten und ziehen – wie beim
Zeichenstift in Vektorprogrammen. So entsteht mit zwei Punkten eine vollständige Kurve.
Das gilt beim Zeichnen wie beim Verlängern.

**Nachjustieren:** Ist ein weicher Zug ausgewählt, hat jeder Punkt zwei runde Griffe an
einer dünnen Linie – das sind die Tangenten. Ziehen ändert die Kurve nur lokal, der Rest
des Zuges bleibt stehen. Ein gefüllter Griff heißt: hier ist die Tangente selbst gesetzt.

**Anschlüsse teilen ihre Richtung.** Schließt ein Zug an einen vorhandenen an – Punkt auf
Punkt oder über den Kantenfang parallel daneben – übernimmt er dessen Tangente, läuft also
knickfrei weiter. Danach hängen die Tangenten aneinander: wer an einem Anschlusspunkt zieht,
zieht den Nachbarn mit, sodass beide Wege in dieselbe Richtung zeigen. Gegenläufig gezeichnete
Wege werden dabei gespiegelt, quer verlaufende gar nicht erst verbunden.

**Anschlüsse halten beim Verschieben.** Liegen zwei Wege auf demselben Punkt, ist er mit einem
Ring markiert. Ihn zu ziehen bewegt beide Wege zugleich und gleicht ihre Richtung an – der
Übergang bleibt also glatt, statt aufzureißen. Dasselbe gilt für den Gruppengriff und für das
Verlängern über einen Anschluss hinweg.

Liegt ein Radius unter dem Richtwert des Typs (Kfz 5 m, Bus 10 m, Radweg einspurig 2,5 m,
übrige Radanlagen 5 m, Fuß 1,5 m), markiert die Prüfung die Stelle mit dem gemessenen
Radius. Über „Radien" abschaltbar; im Export sind die Marken nie enthalten.

Die Werte sind Orientierungswerte aus der Entwurfspraxis (RASt/ERA-Größenordnung),
keine Normprüfung.

## Spuren nebeneinander

Zwei Wege, eine Spur bündig an die nächste zu legen:

* **Kantenfang** – beim Zeichnen und Ziehen rastet ein Punkt in der Nähe einer Spur auf den
  bündigen Achsabstand ein (halbe Breite + halbe Breite). Auf Höhe eines Stützpunktes der
  Nachbarspur rastet er zusätzlich **längs** ein, sodass beide Punkte übereinander liegen –
  erkennbar an der längeren Quermarke mit Kästchen. Damit greifen Gruppengriff und
  Tangentenkopplung von selbst. `Alt` hebt den Fang auf.
* **Spur daneben anlegen** – im Inspektor „◀ links / rechts ▶". Erzeugt eine bündig versetzte
  Kopie mit derselben Form und Kurvenführung; zwischen zwei Kfz-Spuren wird eine Leitlinie
  gesetzt. Es entsteht ein **eigenständiger Weg** – identisch zu einem, den du von Hand daneben
  zeichnest. Es gibt keinen Master und keine Kopie: jeder Weg lässt sich einzeln anfassen,
  verlängern, kürzen und umtypen.

Zusammengehalten werden benachbarte Spuren allein durch ihre Lage: liegen ihre Stützpunkte
quer auf gleicher Höhe, erscheint dazwischen ein Gruppengriff, ihre Tangenten bleiben synchron,
und die Linie auf der gemeinsamen Kante gilt für beide.

**Gruppengriff (Raute).** Liegen Stützpunkte zweier unabhängiger Wege quer auf gleicher Höhe,
erscheint zwischen ihnen eine Raute. Ziehen verschiebt beide Punkte gemeinsam und hält ihren
Abstand; die quadratischen Griffe daneben bewegen weiterhin nur den einen Punkt. Beim
Einzelziehen rastet ein Punkt auf die Höhe eines Nachbarpunktes ein (Fadenkreuz-Marke).

## Wege ändern

Ist ein Weg ausgewählt, erscheinen orange **+**-Marken:

* **+ am Ende** verlängert den Weg – weitere Punkte klicken, `Enter` beendet. Am Anschluss
  eines anderen Weges übernimmt er dessen Richtung.
* **+ zwischen zwei Punkten** setzt dort einen Wegpunkt. Er liegt auf der bestehenden Kurve,
  die Form ändert sich also nicht – erst das Ziehen des neuen Griffs verändert sie.
* **Punkt löschen:** Punkt anklicken (er wird größer und hohl dargestellt), dann `Entf`.
  `Alt`+Klick ohne Ziehen löscht ihn direkt, und im Inspektor steht ein Knopf „Punkt n von m löschen".
  Der letzte verbleibende Zug bleibt geschützt: unter zwei Punkten (Flächen: drei) wird nicht
  gelöscht. Ohne angeklickten Punkt löscht `Entf` weiterhin das ganze Element.

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

Radverkehrsanlagen lassen sich im Inspektor zwischen **grüner und roter Einfärbung**
umschalten; die Wahl wird zur Vorgabe für neue Anlagen und färbt auch die Werkzeugleiste um.

Parkstreifen bekommen Stellplatzteiler (quer 2,5 m, längs 5,5 m), die Sperrfläche
eine Schraffur. Der Fußgängerüberweg wird von Bordstein zu Bordstein gezeichnet; seine
Streifen liegen quer zur Gehrichtung, also parallel zur Fahrbahnachse, und sind 4 m tief.
Radverkehrsanlagen sind grün eingefärbt.

## Fahrtrichtungspfeile

Das Werkzeug **Fahrtrichtungspfeil** (Kfz-Verkehr) setzt einen Pfeil auf eine Fahrspur:
Schon beim Überfahren zeigt eine halbtransparente Vorschau, auf welcher Spur und in welcher
Richtung er landen würde; der Klick setzt ihn dort ab. Liegt keine passende Spur unter dem
Zeiger, erscheint keine Vorschau – dann setzt der Klick auch nichts. Sechs Formen im Inspektor: geradeaus, links, rechts, geradeaus + links,
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

Belag und Randmarkierungen des querenden Wegs werden exakt an den Kanten der gequerten
Anlage beschnitten: die Furt beginnt und endet dort, wo die jeweilige Kante die Fahrbahn
verlässt, bei schrägen Querungen also seitenweise versetzt. Erkannt wird die Überlappung
geometrisch, funktioniert also auch bei Kurven und beliebigen Winkeln. Pro Element abschaltbar über
„Querung über Fahrbahn/Radweg" im Inspektor – dann wird wieder durchgehend Belag gezeichnet.

## Kreuzungen

Kreuzen sich zwei Anlagen desselben Rangs (zwei Fahrbahnen, zwei Radwege) in einem Winkel
über etwa 20°, gilt die Überlappung als Knotenpunkt: dort hören alle Randmarkierungen und
Leitlinien beider Wege auf, die Fläche bleibt durchgehender Belag. Beschnitten wird am
**Bandpolygon** der kreuzenden Anlage, nicht an einer Position auf der Achse – bei schrägen
Kreuzungen enden linke und rechte Kante daher an unterschiedlichen Stellen, so wie es die
Geometrie verlangt. Das gilt auch für
nebeneinanderliegende Spurenpaare - die Naht zwischen zwei Spuren reißt die Maske nicht auf.
Parallel geführte Spuren sind nicht betroffen; erst der Winkel macht die Kreuzung aus.

Pro Knoten lässt sich das ändern: Ist ein Weg ausgewählt, listet der Inspektor unter
**Kreuzungen** jeden erkannten Partner auf. Je Partner wählbar:

* **Fläche frei** (Vorgabe) – Markierungen hören am Knoten auf.
* **gestrichelt durch** – die Randmarkierungen laufen gestrichelt durch den Knoten weiter,
  wie eine Führungslinie. Die Einstellung gilt für beide beteiligten Wege.

Ein Klick auf den Partnernamen springt zu ihm.

## Halte- und Wartelinie

Das Werkzeug **Halte-/Wartelinie** setzt eine Querlinie auf eine Fahr-, Bus- oder Radspur:
Auch hier zeigt die Vorschau beim Überfahren, wo sie liegen wird; die Linie liegt quer über
die volle Breite der Spur. Im Inspektor
umschaltbar zwischen Haltlinie (durchgezogen, 0,5 m) und Wartelinie (unterbrochen).
Wie der Pfeil hängt sie an ihrer Spur, lässt sich auf ihr verschieben und verschwindet mit ihr.

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
* **Spur daneben anlegen** – im Inspektor „◀ links / rechts ▶". Legt eine bündig versetzte
  Kopie an; zwischen zwei Kfz-Spuren wird automatisch eine Leitlinie gesetzt. Ändert man die
  Linie auf der gemeinsamen Kante, gilt sie für beide. Über die Typwahl wird daraus z. B. ein
  Radweg.

Die neue Spur ist ein vollwertiger, eigenständiger Weg. Ziehst du einen ihrer Punkte weg,
läuft sie ab dort frei (Abbiegespur, ausschwenkender Radweg) – ohne dass etwas „gelöst" werden
müsste; wo ihre Punkte weiter auf gleicher Höhe liegen, bleibt sie mit der Nachbarspur
verbunden.

## Bedienung

| Aktion | |
|---|---|
| Zug beenden | Doppelklick, `Enter` oder Rechtsklick |
| Abbrechen / Auswahlwerkzeug | `Esc`, `V` |
| Punkt oder Element löschen | `Entf` |
| Punkt direkt löschen | `Alt`+Klick (ohne Ziehen) |
| Punkt aus seinen Bindungen lösen | `Alt`+Ziehen |
| Rückgängig / Wiederholen | `Strg+Z` / `Strg+Umschalt+Z` |
| Karte verschieben | `Leertaste` + Ziehen oder mittlere Maustaste |
| Zoomen | Mausrad |
| Kurve aufziehen | beim Klicken ziehen |
| Winkel einrasten (15°) | `Umschalt` beim Zeichnen |
| Fang aussetzen | `Alt` |
| Vorher/Nachher | `H` |
| Ansicht einpassen | Knopf *Alles zeigen* |

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
