---
title: Bot-Filterung in Query Service mit maschinellem Lernen
description: Dieses Dokument bietet einen Überblick darüber, wie Sie Query Service und maschinelles Lernen verwenden können, um Bot-Aktivitäten zu bestimmen und ihre Aktionen nach dem echten Besucher-Traffic auf einer Online-Website zu filtern.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 6%

---

# Bot-Filterung in [!DNL Query Service] mit maschinellem Lernen

Bot-Aktivitäten können sich auf Analytics-Metriken auswirken und die Datenintegrität beeinträchtigen. Adobe Experience Platform [!DNL Query Service] kann verwendet werden, um Ihre Datenqualität durch Bot-Filterung zu erhalten.

Mit der Bot-Filterung können Sie die Qualität Ihrer Daten gewährleisten, indem Sie die Kontamination von Daten, die aus nicht menschlichen Interaktionen mit Ihrer Website resultieren, weitgehend entfernen. Dieser Prozess wird durch die Kombination von SQL-Abfragen und maschinellem Lernen erreicht.

Bot-Aktivitäten können auf verschiedene Weise identifiziert werden. Der in diesem Dokument verfolgte Ansatz konzentriert sich auf Aktivitätspitzen, in diesem Fall auf die Anzahl der Aktionen, die ein Benutzer in einem bestimmten Zeitraum durchgeführt hat. Zunächst legt eine SQL-Abfrage willkürlich einen Schwellenwert für die Anzahl der Aktionen fest, die über einen bestimmten Zeitraum durchgeführt wurden, um als Bot-Aktivität zu gelten. Diese Schwelle wird dann dynamisch mithilfe eines maschinellen Lernmodells verfeinert, um die Genauigkeit dieser Verhältnisse zu verbessern.

Dieses Dokument bietet einen Überblick und detaillierte Beispiele für die SQL-Bot-Filterabfragen und die maschinellen Lernmodelle, die für die Einrichtung des Prozesses in Ihrer Umgebung erforderlich sind.

## Erste Schritte

Im Rahmen dieses Prozesses müssen Sie ein Modell für maschinelles Lernen trainieren. In diesem Dokument wird davon ausgegangen, dass Sie über Kenntnisse in einer oder mehreren Umgebungen für maschinelles Lernen verfügen.

Dieses Beispiel verwendet [!DNL Jupyter Notebook] als Entwicklungsumgebung. Es stehen zwar viele Optionen zur Verfügung, [!DNL Jupyter Notebook] wird empfohlen, da es sich um eine Open-Source-Webanwendung mit niedrigen Rechenanforderungen handelt. Es kann [von der offiziellen Website heruntergeladen](https://jupyter.org/).

## Verwendung [!DNL Query Service] Definieren eines Schwellenwerts für die Bot-Aktivität

Die beiden Attribute, die zum Extrahieren von Daten für die Bot-Erkennung verwendet werden, sind:

* Experience Cloud Visitor ID (ECID, auch als MCID bezeichnet): Dies bietet eine universelle, beständige ID zum Identifizieren Ihrer Besucher über alle Adobe-Lösungen hinweg.
* Zeitstempel: Dadurch werden Uhrzeit und Datum im UTC-Format bereitgestellt, zu dem eine Aktivität auf der Website erfolgte.

>[!NOTE]
>
>Die Verwendung von `mcid` weiterhin in Namespace-Verweisen auf die Experience Cloud-Besucher-ID gefunden werden, wie im folgenden Beispiel gezeigt.

Die folgende SQL-Anweisung bietet ein erstes Beispiel zur Identifizierung von Bot-Aktivitäten. In der Anweisung wird davon ausgegangen, dass der Benutzer ein Bot ist, wenn ein Besucher innerhalb einer Minute 50 Klicks durchführt.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

Der Ausdruck filtert die ECIDs (`mcid`) aller Besucher, die den Schwellenwert erreichen, jedoch keine Traffic-Spitzen aus anderen Intervallen ansprechen.

## Verbessern der Bot-Erkennung mit maschinellem Lernen

Die ursprüngliche SQL-Anweisung kann verfeinert werden, um zu einer Abfrage zur Funktionsextraktion für maschinelles Lernen zu werden. Die verbesserte Abfrage sollte mehr Funktionen für eine Vielzahl von Intervallen für das Training von Modellen für maschinelles Lernen mit hoher Genauigkeit liefern.

Die Beispielanweisung wird von einer Minute mit bis zu 60 Klicks erweitert und umfasst nun fünf- und 30-minütige Zeiträume mit Klickzahlen von 300 bzw. 1800.

Die Beispielanweisung erfasst die maximale Anzahl von Klicks für jede ECID (`mcid`) über die verschiedenen Zeiträume. Die erste Anweisung wurde um einen Zeitraum von einer Minute (60 Sekunden), 5 Minuten (300 Sekunden) und einer Stunde (d. h. 1800 Sekunden) erweitert.

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

Das Ergebnis dieses Ausdrucks ähnelt möglicherweise der unten angegebenen Tabelle.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identifizieren neuer Spitzenschwellen mithilfe des maschinellen Lernens

Exportieren Sie dann den resultierenden Abfragedatensatz in das CSV-Format und importieren Sie ihn in [!DNL Jupyter Notebook]. Aus dieser Umgebung können Sie ein Modell für maschinelles Lernen mithilfe aktueller Bibliotheken für maschinelles Lernen trainieren. Weitere Informationen finden Sie im Handbuch zur Fehlerbehebung . [Exportieren von Daten aus [!DNL Query Service] im CSV-Format](../troubleshooting-guide.md#export-csv)

Die anfänglich festgelegten Ad-hoc-Spitzenschwellen sind nicht datengesteuert und daher ungenau. Modelle für maschinelles Lernen können verwendet werden, um Parameter als Schwellenwerte zu trainieren. Daher können Sie die Abfrageeffizienz steigern, indem Sie die Anzahl der `GROUP BY` Suchbegriffe verwenden, indem nicht benötigte Funktionen entfernt werden.

In diesem Beispiel wird die Maschinenlernbibliothek Scikit-Learn verwendet, die standardmäßig mit [!DNL Jupyter Notebook]. Die Python-Bibliothek &quot;pandas&quot;wird ebenfalls zur Verwendung hier importiert. Die folgenden Befehle werden in [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Als Nächstes müssen Sie einen Entscheidungsbaum-Klassifizierer für den Datensatz trainieren und die Logik beachten, die sich aus dem Modell ergibt.

Die Bibliothek &quot;Matplotlib&quot;wird verwendet, um die Entscheidungsbaum-Classification im folgenden Beispiel zu visualisieren.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

Die von [!DNL Jupyter Notebook] für dieses Beispiel wie folgt aussehen.

```text
Model Accuracy: 0.99935
```

![Statistische Ausgabe aus [!DNL Jupyter Notebook] Modell für maschinelles Lernen.](../images/use-cases/jupiter-notebook-output.png)

Die Ergebnisse für das im obigen Beispiel dargestellte Modell sind zu über 99 % korrekt.

Da der Entscheidungsbaum-Klassifizierer mithilfe von Daten aus [!DNL Query Service] bei regelmäßiger Kadenz mithilfe geplanter Abfragen die Datenintegrität sicherstellen, indem Sie Bot-Aktivitäten mit hoher Genauigkeit filtern. Mithilfe der vom maschinellen Lernmodell abgeleiteten Parameter können die ursprünglichen Abfragen mit den hochpräzisen Parametern aktualisiert werden, die vom Modell erstellt wurden.

Das Beispielmodell, das mit einer hohen Genauigkeit bestimmt wird, dass alle Besucher mit mehr als 130 Interaktionen in fünf Minuten Bots sind. Diese Informationen können jetzt verwendet werden, um Ihre SQL-Abfragen zum Filtern von Bots zu verfeinern.

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie die Verwendung von [!DNL Query Service] und maschinelles Lernen zum Ermitteln und Filtern von Bot-Aktivitäten.

Andere Dokumente, die die Vorteile von [!DNL Query Service] zu den strategischen geschäftlichen Einblicken Ihres Unternehmens sind die [Anwendungsfall für abgebrochenes Durchsuchen](./abandoned-browse.md) Beispiel.
