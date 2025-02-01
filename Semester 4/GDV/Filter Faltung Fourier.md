
#### **1. Ich kenne verschiedene Arten von Bildrauschen**

##### **1. Gaußsches Rauschen**

- **Beschreibung**:
    - Gaußsches Rauschen entsteht durch zufällige Intensitätsschwankungen, die einer Gaußschen Normalverteilung folgen.
    - Es wird oft durch elektronische Störungen oder Schwankungen während der Bildaufnahme verursacht.
      
- **Eigenschaften**:
    - Die Intensitätswerte des Rauschens sind normalverteilt, mit den meisten Werten nahe dem Mittelwert.
    - Kann durch **Gauß-Filter** oder andere Weichzeichnungsfilter effektiv reduziert werden.
      
- **Visuelle Wirkung**: Das Bild erscheint "körnig", aber gleichmäßig über die gesamte Fläche verteilt.
  
- **Anwendung zur Reduktion**:
    - Glättungsfilter (wie der Mittelwert- oder Gaußfilter) sind effektiv, allerdings können auch Details im Bild verloren gehen​
##### 2. **Impulsrauschen (Salt-and-Pepper-Rauschen)**

- **Beschreibung**:
    - Dieses Rauschen zeigt sich in Form von zufällig verteilten schwarzen und weißen Pixeln, die sich stark vom umliegenden Bild abheben.
    - Es wird oft durch Übertragungsfehler, defekte Sensoren oder fehlerhafte Datenverarbeitung verursacht.
- **Eigenschaften**:
    - Die betroffenen Pixel haben entweder die minimale (schwarz) oder maximale (weiß) Intensität.
    - Es ist ungleichmäßiger als Gaußsches Rauschen.
- **Visuelle Wirkung**: Die Bildqualität wird stark beeinträchtigt, insbesondere durch die kontrastreichen, auffälligen Punkte.

- **Anwendung zur Reduktion**:
    - Ein **Medianfilter** ist hier besonders effektiv, da er die Spitzenwerte entfernt und keine neuen Farbwerte erzeugt.
    - Morphologische Operationen wie "Dilatation(Lücken oder kleine Löcher in Objekten werden gefüllt)" oder "Erosion (entfernt Pixel an den Rändern von Objekten)" können ebenfalls helfen​

#### **2.Was ist ein Kernel und wie wird er auf ein Bild angewendet**

Ein **Kernel** (auch Filter oder Maske genannt) ist eine kleine Matrix z.B 3x3, die verwendet wird, um Operationen auf Bildern durchzuführen, wie z. B. Rauschunterdrückung, Kantenextraktion oder Bildglättung. Der Kernel legt fest, wie die Pixelwerte in der Nachbarschaft eines Pixels kombiniert werden, um einen neuen Wert für dieses Pixel zu berechnen. Die Werte im Kernel bestimmen, welche Art von Operation durchgeführt wird (z. B. Mittelwertbildung, Schärfung, Gauß-Glättung).

##### **Anwendung eines Kernels auf ein Bild**

##### **1. Schritt: Lokale Nachbarschaft definieren**

- Für jedes Pixel im Bild wird ein Fenster (entsprechend der Größe des Kernels) um das Pixel gelegt. Dieses Fenster umfasst die benachbarten Pixel, die für die Berechnung benötigt werden​​.
##### **2. Schritt: Elementweise Multiplikation**
- Die Pixelwerte im Fenster werden mit den entsprechenden Werten des Kernels multipliziert. Dies geschieht elementweise, d. h., jedes Gewicht im Kernel wird mit dem entsprechenden Pixelwert im Fenster multipliziert.
##### **3. Schritt: Summation**
- Die Ergebnisse der elementweisen Multiplikation werden aufaddiert. Dieser Summenwert wird dann als neuer Wert für das Zielpixel verwendet.
##### **4. Schritt: Wiederholen für alle Pixel**

- Der Kernel wird über jedes Pixel des Bildes geschoben (in einem Prozess, der als "Sliding Window" bezeichnet wird). Für jedes Pixel wird der oben beschriebene Prozess wiederholt.


#### **3.Nenne mir verschiedene morphologische Operationen und erkläre mir wie ich diese auf Bilder anwende**

Morphologische Operationen werden in der Bildverarbeitung verwendet, um die geometrischen Strukturen zu analysieren oder zu verändern. 
Morphologische Operationen wenden ein strukturierendes Element auf ein
Eingabebild an und erzeugen ein Ausgabebild.
Sie basieren auf der Manipulation von Pixeln mit Hilfe eines strukturierenden Elements (auch Kernel genannt, typischerweise Quadratisch).

##### **Grundlegende morphologische Operationen**

##### **Dilatation (Erweiterung)**

- **Beschreibung**:
    - Die Dilatation erweitert helle Bereiche (z. B. weiße Pixel in binären Bildern). Sie prüft in einer definierten Nachbarschaft (gegeben durch das strukturierende Element), ob mindestens ein Pixel in dieser Nachbarschaft einen bestimmten Wert (z. B. Weiß) hat.
    - logisches Oder bzw. max in OpenCV
- **Wirkung**:
    - Kleine Lücken oder Löcher innerhalb eines Objekts werden geschlossen.
    - Objekte im Bild erscheinen größer.
- **Anwendung**:
    - Bewegte das strukturierende Element (z. B. ein quadratischer Kernel) über das Bild.
    - Ersetze das Pixel in der Mitte durch den Maximalwert der überdeckten Nachbarschaft.
- **Typische Anwendung**: Auffüllen von Lücken oder Verbinden von benachbarten Objekten​​.
##### **Erosion (Abtragung)**

- **Beschreibung**:
    - Die Erosion entfernt helle Pixel an den Rändern eines Objekts. Sie prüft in der Nachbarschaft, ob alle Pixel den gewünschten Wert (z. B. Weiß) erfüllen.
    - logisches Und bzw. min in OpenCV
- **Wirkung**:
    - Objekte werden kleiner.
    - Störungen wie kleine helle Punkte können entfernt werden.
- **Anwendung**:
    - Bewegte das strukturierende Element über das Bild.
    - Ersetze das Pixel in der Mitte durch den Minimalwert der überdeckten Nachbarschaft.
- **Typische Anwendung**: Entfernen von Rauschen (z. B. isolierten hellen Pixeln)

##### **Anwendungsschritte**
Hilft auch bei Salt n Pepper Rauschen -> 
![[Pasted image 20250129223218.png]]

#### **4.Ich habe eine Vorstellung, was mit einem Bild passiert, wenn ich den zu verwendenden Filterkernel sehe**

Wenn du den **Filterkernel** siehst, kannst du dir vorstellen, wie er das Bild verändert, indem du folgende Punkte beachtest:
1. **Größe des Kernels**:
    - Ein kleiner Kernel (z. B. 3x3) beeinflusst nur lokale Pixelbereiche, sorgt für sanfte Veränderungen.
    - Ein großer Kernel (z. B. 7x7 oder 15x15) glättet stärker oder entfernt mehr Details.
      
2. **Werte im Kernel**:
    - **Gleichmäßige Werte (z. B. Mittelwertfilter)**: Glättet das Bild, indem Pixelwerte gleichmäßig gemischt werden.
    - **Zentrierte, größere Werte (z. B. Gaußfilter)**: Bevorzugt nahegelegene Pixel und erzeugt ein weicheres Ergebnis. Vermeidet Artefakte
    - **Negative Werte (z. B. Sobel-Filter)**: Hebt Kontraste hervor, betont Kanten.
      
3. **Art der Gewichtung**:
    - **Symmetrische Filter (z. B. Gauß)**: Glätten ohne Verzerrung.
    - **Richtungsabhängige Filter (z. B. Sobel, Schärfungsfilter)**: Betonen Kanten in bestimmten Richtungen oder schärfen Details.
##### **Zusammengefasst**:
- **Glättung**: Gleichmäßige oder zentrierte positive Werte.
- **Kanten betonen**: Wechsel von positiven zu negativen Werten.
- **Details erhalten**: Symmetrisch abnehmende Werte (z. B. Gauß). Der Kernel definiert die Art der Veränderung – du siehst, ob das Bild weicher, schärfer oder kantiger wird.

#### **5.Ich weiß wie ein Gaußscher Weichzeichner funktioniert**

Ein **Gaußscher Weichzeichner** funktioniert, indem er einen Filter Kernel verwendet, der die Form einer **Gaußschen Glockenkurve** hat.
##### **Schlüsselprinzipien:**

1. **Gewichtete Nachbarschaft**:
    - Pixel in der Nähe des Zielpixels werden stärker gewichtet, während weiter entfernte Pixel weniger Gewicht erhalten.
    - Dies wird durch die Werte im Gauß-Kernel bestimmt, die symmetrisch abnehmen.

2. **Effekt auf das Bild**:
    - **Hohe Frequenzen (Details, Rauschen)** werden geglättet.
    - **Tiefe Frequenzen (gleichmäßige Bereiche)** bleiben erhalten.
##### **Zusammengefasst**:
Ein Gaußscher Weichzeichner reduziert Bildrauschen und Details, indem er nahegelegene Pixel stärker einbezieht und so sanfte Übergänge schafft. Je größer σ\sigmaσ oder der Kernel, desto stärker wird das Bild geglättet.

#### 6.**Ich weiß was Faltung bedeutet**

### Faltung:
• Mathematisch klar definierte Operation. die verwendet wird, um **Filter (Kernel)** auf ein Bild anzuwenden.
• Der Kernel muss in beide Richtungen umgedreht werden (flip).
• Dann die Kreuzkorrelation anwenden.
Die **Kreuzkorrelation** ist eine Methode zur **Messung der Ähnlichkeit zwischen zwei Signalen oder Bildern**, indem sie eines über das andere **verschiebt** und die Übereinstimmung an jeder Position berechnet.

#### Eigenschaft:  
**Verschiebungsinvariant** (shift invariant):
	• Der Operator verhält sich überall gleich, d. h. der Wert der Ausgabe hängt von dem Muster in der Bildumgebung ab, nicht von der Position der Umgebung.
	
Kommutativ (Reihenfolge egal)

Assoziativ (Zusammenfassung möglich)

Distributiv bezüglich der Addition

Skalare lassen sich herauslösen:
Bilder können vorher oder nachher skaliert werden, Skalierung über Kernel möglich

1. **Der Faltungsprozess**:
    - Der Filter wird über das Bild bewegt, und für jedes Pixel wird eine neue Zahl berechnet. Diese Zahl ergibt sich aus der Gewichtung der Pixelwerte im Filterbereich.
    - Zum Beispiel: Wenn der Filter auf einen bestimmten Pixel angewendet wird, multiplizieren wir die Werte der benachbarten Pixel mit den entsprechenden Werten im Filter und addieren diese Produkte.
      
2. **Beispiel**:
    - Bei **Weichzeichnen** wird ein Filter verwendet, der benachbarte Pixel zu einem neuen Wert zusammenfasst, sodass das Bild insgesamt unschärfer wird.
    - Bei **Kantenerkennung** wird der Filter so gewählt, dass er Bereiche im Bild erkennt, in denen sich die Helligkeit schnell verändert – also Kanten.
      
3. **Mathematisch ausgedrückt**: Die neue Zahl für einen Pixel ergibt sich aus der Summe der Produkte der Pixelwerte und der Filterwerte. Dies geschieht über das gesamte Bild hinweg.
##### Fazit:
Faltung ist eine Methode, um ein Bild mit einem Filter zu transformieren, indem benachbarte Pixel gewichtet und kombiniert werden. Sie wird häufig verwendet, um Bilder zu verändern, wie etwa durch Weichzeichnen oder Kanten erkennen.

#### **7. Ich erkenne Alising Effekte und weiß wie man sie verhindern kann

Aliasing passiert, wenn ein Signal mit zu niedriger Auflösung abgetastet wird, was zu verzerrten oder unschönen Mustern führt, wie z. B. Zickzack-Kanten oder Moire-Effekten.
##### Erkennung:
- **Zickzack-Linien** oder **unerwünschte Muster** in Bildern.
- **Unnatürlich „zackige“ Kanten** anstatt weicher Übergänge.
##### Vermeidung:
1. **Antialiasing**: Glättet Kanten, um Treppeneffekte zu vermeiden.
2. **Höhere Abtastrate**: Mehr Daten oder Pixel erfassen, um Details besser abzubilden.
3. **Low-Pass-Filter**: Entfernt hohe Frequenzen vor dem Abtasten, um Aliasing zu verhindern.

Kurz gesagt, Aliasing lässt sich durch höhere Auflösung, spezielle Filter oder Antialiasing-Techniken vermeiden.

#### **8. Ich weiß was die Fouriertransfortmation macht und was der Orts- und der Frequenzbereich sind*

Die **Fouriertransformation** wandelt ein Signal von der **Zeit- oder Ortsdomäne** in die **Frequenzdomäne** um. Sie zeigt, wie viel von jeder Frequenz in einem Signal oder Bild enthalten ist.

- **Ortsbereich**: Hier wird das Signal oder Bild direkt betrachtet, zum Beispiel als Bildpixel oder in der Zeitachse (wie ein Klang über Zeit).
- **Frequenzbereich**: Hier wird das Signal in verschiedene Frequenzen zerlegt, die den schnellen oder langsamen Änderungen im Bild oder Signal entsprechen.

Die Fouriertransformation hilft also, das Signal zu analysieren, indem sie es in seine Frequenzen zerlegt und zeigt, wie das Signal durch unterschiedliche Frequenzen aufgebaut ist.
#### 9. **Ich habe verstanden, warum es Hoch- bzw. Tiefpassfilter heißt**

Hoch- und Tiefpassfilter beziehen sich darauf, welche Arten von „Frequenzen“ (also schnellen oder langsamen Änderungen) in einem Signal oder Bild durchgelassen werden.
##### Tiefpassfilter:

Ein **Tiefpassfilter** lässt die langsamen Änderungen (niedrige Frequenzen) durch und blockiert die schnellen Änderungen (hohe Frequenzen). In Bildern bedeutet das, dass der Filter die feinen Details oder das Rauschen herausfiltert und nur die groben Strukturen übrig bleiben.

- **Wirkung auf das Bild**:
    - **Rauschen wird reduziert**, da es meist durch schnelle Intensitätsschwankungen entsteht.
    - **Kanten und Details werden abgeschwächt**, da sie ebenfalls hohe Frequenzen repräsentieren.
    - Das Bild wirkt weicher und weniger detailreich.
      
- **Beispielanwendungen**:
    1. **Rauschreduktion**:
        - In schlecht beleuchteten Fotos (z. B. Nachtaufnahmen) wird Tiefpassfilterung eingesetzt, um digitales Rauschen zu entfernen und glattere Flächen zu erzeugen.
    2. **Weichzeichnen**:
        - In Fotografie und Grafikdesign, um Porträts weicher wirken zu lassen oder störende Details zu entfernen.
    3. **Vorverarbeitung**:
        - Vor der Anwendung von Algorithmen wie der Kantenextraktion, um unnötige Details zu glätten und die Hauptstrukturen hervorzuheben.
          
- **Fallbeispiel**:
    - **Satellitenbilder**:
        - Rauschen in Satellitenbildern, verursacht durch Signalstörungen, wird durch Tiefpassfilter geglättet, um großflächige Strukturen wie Landschaften oder Wolkenmuster deutlicher darzustellen.
##### Hochpassfilter:
Ein **Hochpassfilter** funktioniert genau andersherum: Er lässt die schnellen Änderungen durch und blockiert die langsamen. In der Bildverarbeitung bedeutet das, dass der Filter die weichen, gleichmäßigen Bereiche entfernt und nur die Details wie Kanten oder scharfe Übergänge übrig lässt.

- **Wirkung auf das Bild**:
    - **Kanten und Texturen werden hervorgehoben**, da sie schnelle Intensitätswechsel repräsentieren.
    - Gleichmäßige Bereiche werden entfernt, wodurch das Bild schärfer wirkt.
      
- **Beispielanwendungen**:
    1. **Kantendetektion**:
        - In der Objekterkennung oder beim Segmentieren von Bildbereichen wird ein Hochpassfilter verwendet, um markante Merkmale wie Kanten zu isolieren.
    2. **Schärfen von Bildern**:
        - Hochpassfilter können verwendet werden, um unscharfe Bilder klarer erscheinen zu lassen, indem die Kanten und Details verstärkt werden.
    3. **Feature-Extraktion**:
        - In Computer-Vision-Anwendungen, um Merkmale wie Texturen und Details hervorzuheben, die für Algorithmen relevant sind.
          
- **Fallbeispiel**:
    - **Gesichtserkennung**:
        - Hochpassfilter helfen, markante Merkmale wie Augenbrauen, Lippen oder Kanten des Gesichts hervorzuheben, um diese für Gesichtserkennungsalgorithmen deutlicher zu machen.
##### Zusammengefasst:
- **Tiefpassfilter** blockieren schnelle Änderungen und lassen die langsamen durch. Sie glätten das Bild und entfernen Details.
- **Hochpassfilter** blockieren langsame Änderungen und lassen schnelle durch. Sie betonen Details und Kanten.

#### **10.Ich habe den Unterschied zwischen Farb- Orts- und Frequenzbereich verstanden.

Bilder können auf verschiedene Arten analysiert und verarbeitet werden, je nachdem, welche Informationen im Fokus stehen. Die drei wichtigsten Betrachtungsweisen sind:

1. **Ortsbereich (Raumbereich / Spatial Domain)** – Betrachtung des Bildes als eine Matrix aus Pixelwerten.
2. **Farbbereich (Color Domain)** – Analyse der Bildinformationen anhand von Farbkanälen und Farbräumen.
3. **Frequenzbereich (Frequency Domain)** – Analyse des Bildes hinsichtlich seiner Frequenzkomponenten (schnelle und langsame Intensitätsänderungen).

Jede dieser Domänen bietet unterschiedliche Perspektiven auf ein Bild und wird für spezifische Anwendungen in der Bildverarbeitung genutzt.

---

##### **1. Ortsbereich (Raumbereich / Spatial Domain)**

- **Beschreibung**:
    
    - Im Ortsbereich wird ein Bild als **eine Anordnung von Pixeln** betrachtet.
    - Jedes Pixel hat eine **Position (x, y)** und einen zugehörigen Intensitätswert (z. B. Helligkeit oder Farbe).
    - Typische Operationen wie **Glättung, Schärfung und Kantendetektion** werden direkt auf den Pixeln durchgeführt.
- **Typische Operationen im Ortsbereich**:
    
    1. **Faltung mit Kernels**: Filter wie Gauß- oder Sobel-Filter werden auf das Bild angewendet, indem sie Pixelwerte basierend auf ihren Nachbarn verändern.
    2. **Histogrammmanipulation**: Kontrastanpassungen können durch Veränderung der Pixelintensitäten durchgeführt werden.
    3. **Morphologische Operationen**: Erosion, Dilatation und andere Filter zur Analyse von Strukturen in Bildern.
- **Beispielanwendungen**:
    
    - **Rauschreduzierung**: Glättungsfilter, um Bildrauschen zu reduzieren.
    - **Kantendetektion**: Hochpassfilter zur Hervorhebung von Details und Kanten.

✦ **Beispiel**:  
In einem Foto mit schlechter Beleuchtung können Helligkeitswerte einzelner Pixel angepasst werden, um den Kontrast zu verbessern.

---

##### **2. Farbbereich (Color Domain)**

- **Beschreibung**:
    
    - Der Farbbereich beschreibt ein Bild anhand seiner **Farbinformationen**, unabhängig von der Position der Pixel.
    - Die Farben eines Bildes können in **unterschiedlichen Farbräumen** dargestellt werden, die jeweils für verschiedene Anwendungen optimiert sind.
- **Gängige Farbräume**:
    
    1. **RGB (Rot, Grün, Blau)**:
        - Standardfarbraum für Monitore und Kameras.
        - Farben werden als Mischung der drei Grundfarben definiert.
    2. **HSV (Farbton, Sättigung, Helligkeit)**:
        - Nutzt eine **menschlich verständlichere** Darstellung von Farben.
        - Farbton (H), Sättigung (S) und Helligkeit (V) sind getrennt, sodass Farben unabhängig von Lichtverhältnissen analysiert werden können.
    3. **LAB-Farbraum**:
        - Annäherung an die menschliche Farbwahrnehmung.
        - Nutzt Luminanz (Helligkeit) und zwei Farbkanäle für Farbinformationen.
- **Typische Operationen im Farbbereich**:
    
    1. **Farbraumtransformationen**: Konvertierung zwischen RGB, HSV oder LAB für gezielte Bildbearbeitung.
    2. **Farbsegmentierung**: Identifikation bestimmter Farben für Objekterkennung (z. B. Detektion eines roten Autos in einem Bild).
    3. **Weißabgleich**: Anpassung von Farbtönen, um eine realistische Darstellung unabhängig von der Beleuchtung zu erreichen.
- **Beispielanwendungen**:
    
    - **Bildklassifikation**: Farbinformationen helfen bei der Kategorisierung von Objekten.
    - **Hautfarbenerkennung in Gesichtsdetektion**: HSV-Farbraum wird genutzt, um Hauttöne unabhängig von Beleuchtung zu analysieren.

✦ **Beispiel**:  
Eine Software zur Bildbearbeitung kann den Farbton eines Fotos in den HSV-Farbraum umwandeln, um gezielt bestimmte Farben zu verändern (z. B. den Himmel blauer zu machen, ohne andere Bildteile zu beeinflussen).

---

##### **3. Frequenzbereich (Frequency Domain)**

- **Beschreibung**:
    
    - Im Frequenzbereich wird das Bild als eine Kombination von **hochfrequenten (schnelle Änderungen) und niedrigfrequenten (langsame Änderungen) Komponenten** betrachtet.
    - Dies geschieht durch eine **Fourier-Transformation**, die das Bild in seine **Frequenzanteile zerlegt**.
- **Niedrige Frequenzen**:
    
    - Repräsentieren **langsame Änderungen** im Bild, z. B. große, gleichmäßige Flächen oder sanfte Farbübergänge.
    - Enthalten wenig Detail, aber die Grundstruktur des Bildes.
    - Anwendung: **Weichzeichnen (Tiefpassfilter)**, um Rauschen zu reduzieren.
- **Hohe Frequenzen**:
    
    - Repräsentieren **schnelle Änderungen** im Bild, wie Kanten und feine Details.
    - Werden für **Kantenerkennung (Hochpassfilter)** genutzt, um Details hervorzuheben.
    - Anwendung: **Schärfung und Kantenextraktion**.
- **Typische Operationen im Frequenzbereich**:
    
    1. **Fourier-Transformation**: Umwandlung eines Bildes vom Orts- in den Frequenzbereich.
    2. **Filterung in der Frequenzdomäne**:
        - **Tiefpassfilter** entfernen hohe Frequenzen und glätten das Bild.
        - **Hochpassfilter** entfernen niedrige Frequenzen und betonen Kanten.
    3. **Kompressionstechniken (z. B. JPEG)**:
        - Datenreduktion durch Entfernen hochfrequenter Informationen, die für das menschliche Auge weniger relevant sind.
- **Beispielanwendungen**:
    
    - **Bildkompression (JPEG)** nutzt Frequenzfilterung, um unwichtige Details zu reduzieren und Speicherplatz zu sparen.
    - **Rauschreduzierung in der Medizin**: MRT- oder Röntgenbilder werden im Frequenzbereich gefiltert, um Störungen zu minimieren.

✦ **Beispiel**:  
Eine Fourier-Transformation eines Bildes zeigt die Frequenzkomponenten. Hohe Frequenzen können gezielt entfernt werden, um Bildrauschen zu reduzieren, oder verstärkt werden, um Details hervorzuheben.

---

##### **Vergleich der drei Bereiche**

|Bereich|Betrachtungsebene|Wichtige Eigenschaften|Typische Anwendungen|
|---|---|---|---|
|**Ortsbereich**|Pixelwerte an festen Positionen|Operationen direkt auf Pixeln|Kantenerkennung, Bildverbesserung|
|**Farbbereich**|Farbkanäle (RGB, HSV, LAB)|Farbinformationen unabhängig von Positionen|Farberkennung, Bildsegmentierung|
|**Frequenzbereich**|Zerlegung in hohe und niedrige Frequenzen|Bild als Kombination von schnellen und langsamen Änderungen|Rauschreduktion, Bildkompression|

---

##### **Zusammenfassung**

- **Ortsbereich** → Pixelbasierte Verarbeitung, direkt auf das Bild angewendet (z. B. Schärfung, Weichzeichnung).
- **Farbbereich** → Analyse und Manipulation von Farbinformationen (z. B. Farbkorrekturen, Segmentierung).
- **Frequenzbereich** → Zerlegung des Bildes in Frequenzanteile, um Rauschreduzierung oder Bildkompression zu ermöglichen.

Durch das Verständnis dieser drei Bereiche kann man gezielt entscheiden, welche Methode für eine bestimmte Bildverarbeitungsaufgabe am besten geeignet ist.

#### **11. Ich habe verstanden dass eine Faltung im Ortsbereich einer Multiplikation im Frequenzbereich entspricht und umgekehrt.

Die **Faltung im Ortsbereich** entspricht einer **Multiplikation im Frequenzbereich**, weil die **Fouriertransformation** es ermöglicht, ein Bild oder Signal von der Orts- in die Frequenzdomäne zu übertragen.

- Wenn du im Ortsbereich eine Faltung machst, kombinierst du Pixel aus dem Bild mit denen des Filters.
- Im Frequenzbereich hingegen werden die Frequenzen des Bildes und des Filters miteinander multipliziert, was dasselbe Ergebnis wie die Faltung im Ortsbereich liefert.

Diese Entsprechung kommt daher, dass die Fouriertransformation es ermöglicht, dass Faltung im Ortsbereich durch eine Multiplikation der Frequenzen ersetzt wird, was rechenintensiver sein kann. So kann man im Frequenzbereich schneller arbeiten, um ähnliche Effekte zu erzielen.

#### **12. Ich bin in der Lage, eine sinnvolle Samplingrate zu wählen, wenn ich die im Signal vorkommenden Frequenzen kenne.

Um eine sinnvolle **Samplingrate** zu wählen, wenn du die Frequenzen im Signal kennst, musst du sicherstellen, dass die Samplingrate mindestens doppelt so hoch ist wie die höchste Frequenz im Signal. Das ist das **Nyquist-Kriterium**.

- Wenn du z. B. ein Signal hast, dessen höchste Frequenz 5 kHz beträgt, sollte die Samplingrate mindestens 10 kHz betragen, um das Signal korrekt abzubilden und Aliasing zu vermeiden.

Kurz gesagt, die Samplingrate sollte hoch genug sein, um alle wichtigen Frequenzen im Signal zu erfassen, ohne Details zu verlieren oder Verzerrungen zu erzeugen.

#### 13. **Ich habe verstanden, woher die Artefakte beim Boxfilter kommen

Die **Artefakte beim Boxfilter** entstehen, weil dieser Filter jedem Pixel denselben Wert aus einem bestimmten Bereich (normalerweise ein Quadrat) zuweist. Dabei werden die Übergänge zwischen benachbarten Pixeln zu abrupt, was zu sichtbaren **Blockeffekten** oder **Kantenschärfungen** führt.

Der Boxfilter verursacht diese Artefakte, weil er keine weichen Übergänge erzeugt – er mischt einfach benachbarte Pixel gleichmäßig, was bei feinen Details zu unerwünschten, groben Effekten führt.

#### **14. Ich habe verstanden, dass man die Interpolation als eine Faltung des diskreten Bildsignals interpretieren kann

Interpolation kann als eine **Faltung des diskreten Bildsignals** verstanden werden, weil beim Interpolieren die Werte zwischen den bekannten Pixeln durch eine gewichtete Mischung benachbarter Pixel berechnet werden. Dabei wird ein **Filter (Kernel)** über das Bild angewendet, der die Pixelwerte basierend auf ihrer Position kombiniert, ähnlich wie bei der Faltung.

Im Wesentlichen wird bei der Interpolation das Bild an neuen Positionen „neu abgetastet“, indem benachbarte Werte miteinander gewichtet und summiert werden – was mathematisch wie eine Faltung funktioniert.

#### **15. Ich bin in der Lage, ein 2D Frequenzspektrums bestimmten Bildinhalten zuzuordnen

Ein **2D-Frequenzspektrum** zeigt, welche Frequenzen in einem Bild enthalten sind. Hohe Frequenzen (schnelle Änderungen) sind oft mit **Kanten** oder **Details** verbunden, während niedrige Frequenzen (langsame Änderungen) **grobe Strukturen** oder **sanfte Übergänge** repräsentieren.

Wenn du das Frequenzspektrum eines Bildes betrachtest, kannst du also erkennen, ob das Bild scharfe Kanten (hohe Frequenzen) oder glatte Flächen (niedrige Frequenzen) enthält, da das Spektrum diese Informationen über die Verteilung der Frequenzen im Bild widerspiegelt.


Image sub sampling: (Bild verkleinern)
Alle Pixel in jeder zweiten Reihe und Spalte werden entfernt um ein halb so großes Bild zu erzeugen

Woher kommen Artefakte
Das Rechtecksignal (also auch der Box- bzw. Mittelwertfilter) enthält sehr hohe Frequenzen.
Der Frequenzbereich ist aber im diskreten Bild durch die Auflösung limitiert.
Daher muss irgendwo abgeschnitten werden und dadurch kann das signal nicht vollständig rekonstruiert werden.
Diese unvollständige Rekonstruktion enthält die Überschwinger (Gibbs-Phänomen), die im Bild als Artefakte sichtbar werden.