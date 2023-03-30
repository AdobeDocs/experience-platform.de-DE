---
title: Fuzzy Match in Query Service
description: Erfahren Sie, wie Sie eine Übereinstimmung mit Ihren Platform-Daten durchführen, die Ergebnisse aus mehreren Datensätzen kombiniert, indem Sie ungefähr eine Zeichenfolge Ihrer Wahl abgleichen.
source-git-commit: a3a4ca4179610348eba73cf1239861265d2bf887
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# Fuzzy Match

Verwenden Sie eine Fuzzy-Übereinstimmung in Ihren Platform-Daten, um die wahrscheinlichsten, ungefähren Übereinstimmungen zurückzugeben, ohne nach Zeichenfolgen mit identischen Zeichen suchen zu müssen. Dies ermöglicht eine wesentlich flexiblere Suche nach Ihren Daten und erleichtert den Zugriff auf Ihre Daten, indem Zeit und Mühe eingespart werden.

Statt zu versuchen, die Suchzeichenfolgen neu zu formatieren, um sie abzugleichen, analysiert die unscharfe Übereinstimmung das Verhältnis der Ähnlichkeit zwischen zwei Sequenzen und gibt den Prozentsatz der Ähnlichkeit zurück. [!DNL FuzzyWuzzy] wird für diesen Prozess empfohlen, da seine Funktionen besser dazu geeignet sind, Zeichenfolgen in komplexeren Situationen im Vergleich zu [!DNL regex] oder [!DNL difflib].

Das in diesem Nutzungsszenario bereitgestellte Beispiel konzentriert sich auf die Zuordnung ähnlicher Attribute aus einer Hotelraumsuche über zwei verschiedene Reisebüro-Datensätze hinweg. Das Dokument zeigt, wie Zeichenfolgen anhand ihres Ähnlichkeitsgrads mit großen separaten Datenquellen abgeglichen werden. In diesem Beispiel vergleicht die Fuzzy Match die Suchergebnisse für die Funktionen eines Zimmers der Reisebüros Luma und Acme.

## Erste Schritte {#getting-started}

Im Rahmen dieses Prozesses müssen Sie ein Modell für maschinelles Lernen trainieren. In diesem Dokument wird davon ausgegangen, dass Sie über Kenntnisse in einer oder mehreren Umgebungen für maschinelles Lernen verfügen.

Dieses Beispiel verwendet [!DNL Python] und [!DNL Jupyter Notebook] Entwicklungsumgebung. Es stehen zwar viele Optionen zur Verfügung, [!DNL Jupyter Notebook] wird empfohlen, da es sich um eine Open-Source-Webanwendung mit niedrigen Rechenanforderungen handelt. Es kann [heruntergeladen von der offiziellen Jupyter-Website](https://jupyter.org/).

Bevor Sie beginnen, müssen Sie die erforderlichen Bibliotheken importieren. [!DNL FuzzyWuzzy] ist eine Open-Source-Lösung [!DNL Python] Bibliothek, die auf der [!DNL difflib] -Bibliothek und verwendet, um Zeichenfolgen zuzuordnen. Sie verwendet [!DNL Levenshtein Distance] um die Unterschiede zwischen Sequenzen und Mustern zu berechnen. [!DNL FuzzyWuzzy] die folgenden Anforderungen erfüllt:

- [!DNL Python] 2.4 (oder höher)
- [!DNL Python-Levenshtein]

Verwenden Sie in der Befehlszeile den folgenden Befehl, um zu installieren. [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Oder verwenden Sie den folgenden Befehl zum Installieren [!DNL Python-Levenshtein] sowie:

```console
pip install fuzzywuzzy[speedup]
```

Weitere technische Informationen [!DNL Fuzzywuzzy] finden Sie in ihrer [amtliche Dokumentation](https://pypi.org/project/fuzzywuzzy/).

### Verbinden von  mit dem Abfrage-Service

Sie müssen Ihr maschinelles Lernmodell mit Query Service verbinden, indem Sie Ihre Anmeldedaten für die Verbindung angeben. Es können sowohl ablaufende als auch nicht ablaufende Anmeldeinformationen bereitgestellt werden. Siehe [Handbuch zu Anmeldeinformationen](../ui/credentials.md) für weitere Informationen zum Erwerb der erforderlichen Anmeldeinformationen. Wenn Sie [!DNL Jupyter Notebook], lesen Sie bitte das vollständige Handbuch unter [Herstellen einer Verbindung zu Query Service](../clients/jupyter-notebook.md).

Importieren Sie außerdem die [!DNL numpy] in Ihrem [!DNL Python] Umgebung, um die lineare Algebra zu aktivieren.

```python
import numpy as np
```

Die folgenden Befehle sind erforderlich, um eine Verbindung mit Query Service von [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Ihre [!DNL Jupyter Notebook] -Instanz ist jetzt mit Query Service verbunden. Wenn die Verbindung erfolgreich hergestellt wurde, wird keine Meldung angezeigt. Wenn die Verbindung fehlgeschlagen ist, wird ein Fehler angezeigt.

### Zeichnen von Daten aus dem Luma-Datensatz {#luma-dataset}

Daten für die Analyse werden aus dem ersten Datensatz mit den folgenden Befehlen gezogen. Aus Gründen der Kürze wurden die Beispiele auf die ersten 10 Ergebnisse der Spalte beschränkt.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Auswählen **Ausgabe** , um das zurückgegebene Array anzuzeigen.

+++Ausgabe

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Zeichnen von Daten aus dem Acme-Datensatz {#acme-dataset}

Daten für die Analyse werden nun aus dem zweiten Datensatz mit den folgenden Befehlen abgerufen. Auch hier waren die Beispiele aus Gründen der Kürze auf die ersten 10 Ergebnisse der Spalte beschränkt.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Auswählen **Ausgabe** , um das zurückgegebene Array anzuzeigen.

+++Ausgabe

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Erstellen einer unscharfen Scoring-Funktion {#fuzzy-scoring}

Als Nächstes müssen Sie importieren `fuzz` aus der FuzzyWuzzy-Bibliothek und führen Sie einen partiellen Quotienten-Vergleich der Zeichenfolgen aus. Mit der Funktion für das Teilverhältnis können Sie eine Übereinstimmung mit Teilzeichenfolgen durchführen. Hierbei wird die kürzeste Zeichenfolge verwendet und mit allen Unterzeichenfolgen abgeglichen, die dieselbe Länge aufweisen. Die Funktion gibt ein prozentuales Ähnlichkeitsverhältnis von bis zu 100 % zurück. Beispielsweise würde die Funktion für das Teilverhältnis die folgenden Zeichenfolgen &quot;Deluxe Room&quot;, &quot;1 King Bed&quot;und &quot;Deluxe King Room&quot;vergleichen und eine Ähnlichkeitsbewertung von 69 % zurückgeben.

Im Anwendungsfall zur Übereinstimmung von Hotelzimmern wird dies mit den folgenden Befehlen durchgeführt:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Importieren Sie als Nächstes `cdist` von [!DNL SciPy] -Bibliothek, um den Abstand zwischen den einzelnen Paaren in den beiden Eingabekollektionen zu berechnen. Dadurch werden die Bewertungen unter allen Paaren von Hotelzimmern berechnet, die von den einzelnen Reisebüros bereitgestellt werden.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Erstellen Sie Zuordnungen zwischen den beiden Spalten mithilfe der unscharfen Join-Punktzahl.

Nachdem die Spalten nun auf der Grundlage der Entfernung bewertet wurden, können Sie die Paare indizieren und nur Treffer beibehalten, die höher als ein bestimmter Prozentsatz waren. In diesem Beispiel werden nur Paare beibehalten, die mit einem Wert von 70 % oder höher übereinstimmen.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Die Ergebnisse können mit dem folgenden Befehl angezeigt werden. Aus Gründen der Kürze sind die Ergebnisse auf zehn Zeilen beschränkt.

```python
matched_pairs[:10]
```

Auswählen **Ausgabe** um die Ergebnisse anzuzeigen.

+++Ausgabe

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

Die Ergebnisse werden dann mithilfe von SQL mit dem folgenden Befehl abgeglichen:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Anwenden der Zuordnungen für unscharfe Verknüpfungen in Query Service {#mappings-for-query-service}

Als Nächstes werden die Paare, die mit hoher Scoring übereinstimmen, mithilfe von SQL verknüpft, um einen neuen Datensatz zu erstellen.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Auswählen **Ausgabe** um die Ergebnisse dieses Joins zu sehen.

+++Ausgabe

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Unscharfe Übereinstimmungsergebnisse in Platform speichern {#save-to-platform}

Schließlich können die Ergebnisse der unscharfen Übereinstimmung als Datensatz gespeichert werden, der in Adobe Experience Platform mit SQL verwendet werden kann.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```


