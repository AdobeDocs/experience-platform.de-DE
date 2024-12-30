---
title: Bot-Filterung im Abfrage-Service mit maschinellem Lernen
description: In diesem Dokument erhalten Sie einen Überblick darüber, wie Sie mit Query Service und maschinellem Lernen die Aktivitäten von sowohl als auch die Filterung ihrer Aktionen anhand des echten Traffics von Online-Website-Besuchern ermitteln können.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# Bot-Filterung in [!DNL Query Service] mit maschinellem Lernen

Bot-Aktivitäten können sich auf Analysemetriken auswirken und die Datenintegrität beeinträchtigen. Adobe Experience Platform [!DNL Query Service] kann verwendet werden, um die Datenqualität durch den Prozess der Bot-Filterung zu erhalten.

Mit Bot-Filtern können Sie Ihre Datenqualität aufrechterhalten, indem Sie die Datenkontamination, die aus nicht menschlicher Interaktion mit Ihrer Website resultiert, weitgehend entfernen. Dieser Prozess wird durch die Kombination von SQL-Abfragen und maschinellem Lernen erreicht.

Bot-Aktivitäten können auf verschiedene Weise identifiziert werden. Der in diesem Dokument verfolgte Ansatz konzentriert sich auf Aktivitätsspitzen, in diesem Fall auf die Anzahl der Aktionen, die eine Benutzerin oder ein Benutzer in einem bestimmten Zeitraum durchgeführt hat. Anfänglich legt eine SQL-Abfrage willkürlich einen Schwellenwert für die Anzahl der Aktionen fest, die über einen bestimmten Zeitraum durchgeführt wurden, um als Bot-Aktivität zu gelten. Dieser Schwellenwert wird dann mithilfe eines maschinellen Lernmodells dynamisch verfeinert, um die Genauigkeit dieser Verhältnisse zu verbessern.

Dieses Dokument bietet einen Überblick und detaillierte Beispiele für die SQL-Bot-Filterabfragen und die Modelle für maschinelles Lernen, die Sie zum Einrichten des Prozesses in Ihrer Umgebung benötigen.

## Erste Schritte

Im Rahmen dieses Prozesses müssen Sie ein Modell für maschinelles Lernen trainieren. Dieses Dokument setzt Kenntnisse über eine oder mehrere maschinelle Lernumgebungen voraus.

In diesem Beispiel wird [!DNL Jupyter Notebook] als Entwicklungsumgebung verwendet. Obwohl viele Optionen verfügbar sind, wird [!DNL Jupyter Notebook] empfohlen, da es sich um eine Open-Source-Webanwendung mit geringen Rechenanforderungen handelt. Es kann [von der offiziellen Website heruntergeladen werden](https://jupyter.org/).

## [!DNL Query Service] verwenden, um einen Schwellenwert für die Bot-Aktivität zu definieren

Die beiden Attribute, mit denen Daten zur Erkennung von Bots extrahiert werden, sind:

* Experience Cloud-Besucher-ID (ECID, auch als MCID bezeichnet): Diese Methode bietet eine universelle, persistente ID zum Identifizieren Ihrer Besuchenden in allen Adobe-Lösungen.
* Zeitstempel: Gibt die Uhrzeit und das Datum im UTC-Format an, zu dem eine Aktivität auf der Website stattgefunden hat.

>[!NOTE]
>
>Die Verwendung von `mcid` findet sich weiterhin in Namespace-Verweisen auf die Experience Cloud-Besucher-ID, wie im folgenden Beispiel gezeigt.

Die folgende SQL-Anweisung zeigt ein erstes Beispiel zur Identifizierung von Bot-Aktivitäten. In der Anweisung wird davon ausgegangen, dass ein Bot verwendet wird, wenn ein Besucher innerhalb einer Minute 50 Klicks ausführt.

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

Der Ausdruck filtert die ECIDs (`mcid`) aller Besucher, die den Schwellenwert erreichen, behebt jedoch keine Traffic-Spitzen aus anderen Intervallen.

## Verbessern der Bot-Erkennung mit maschinellem Lernen

Die anfängliche SQL-Anweisung kann verfeinert werden, um eine Funktionsextraktionsabfrage für maschinelles Lernen zu werden. Die verbesserte Abfrage sollte mehr Funktionen für eine Vielzahl von Intervallen zum Trainieren von Modellen für maschinelles Lernen mit hoher Genauigkeit generieren.

Die Beispielanweisung wird von einer Minute mit bis zu 60 Klicks erweitert, um einen Zeitraum von fünf Minuten und 30 Minuten mit einer Klickanzahl von 300 bzw. 1800 einzuschließen.

Die Beispielanweisung erfasst die maximale Anzahl an Klicks für jede ECID (`mcid`) über die verschiedenen Zeiträume. Die anfängliche Anweisung wurde erweitert und umfasst jetzt einen Zeitraum von einer Minute (60 Sekunden), 5 Minuten (300 Sekunden) und einer Stunde (d. h. 1800 Sekunden).

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

Das Ergebnis dieses Ausdrucks könnte der unten angegebenen Tabelle ähneln.

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

## Identifizieren neuer Spitzenschwellen mithilfe von maschinellem Lernen

Exportieren Sie als Nächstes den resultierenden Abfragedatensatz in das CSV-Format und importieren Sie ihn dann in [!DNL Jupyter Notebook]. Aus dieser Umgebung können Sie ein Modell für maschinelles Lernen mithilfe aktueller Bibliotheken für maschinelles Lernen trainieren. Weitere Informationen finden Sie im Handbuch zur Fehlerbehebung unter [Exportieren von Daten aus  [!DNL Query Service]  CSV-Format](../troubleshooting-guide.md#export-csv)

Die ursprünglich festgelegten Schwellenwerte für Ad-hoc-Spitzen sind nicht datengesteuert und daher ungenau. Modelle für maschinelles Lernen können verwendet werden, um Parameter als Schwellenwerte zu trainieren. Daher können Sie die Abfrageeffizienz erhöhen, indem Sie die Anzahl der `GROUP BY` Schlüsselwörter reduzieren, indem Sie nicht benötigte Funktionen entfernen.

In diesem Beispiel wird die Bibliothek für maschinelles Lernen vom Typ „Scikit-Learn“ verwendet, die standardmäßig mit [!DNL Jupyter Notebook] installiert wird. Auch die Python-Bibliothek „Pandas“ wird hier importiert. Die folgenden Befehle werden in [!DNL Jupyter Notebook] eingegeben.

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Als Nächstes müssen Sie einen Entscheidungsbaum-Klassifikator für den Datensatz trainieren und die aus dem Modell resultierende Logik beachten.

Die Bibliothek „Matplotlib“ wird verwendet, um den Entscheidungsbaum-Klassifikator im folgenden Beispiel zu visualisieren.

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

Die von [!DNL Jupyter Notebook] für dieses Beispiel zurückgegebenen Werte lauten wie folgt.

```text
Model Accuracy: 0.99935
```

![Statistische Ausgabe [!DNL Jupyter Notebook] Modell für maschinelles Lernen.](../images/use-cases/jupiter-notebook-output.png)

Die Ergebnisse für das im obigen Beispiel dargestellte Modell sind zu über 99 % genau.

Da der Entscheidungsbaum-Klassifikator anhand von Daten aus [!DNL Query Service] in regelmäßigen Abständen mithilfe geplanter Abfragen trainiert werden kann, können Sie die Datenintegrität sicherstellen, indem Sie die Bot-Aktivität mit einem hohen Maß an Genauigkeit filtern. Durch Verwendung der vom Modell für maschinelles Lernen abgeleiteten Parameter können die ursprünglichen Abfragen mit den hochpräzisen Parametern aktualisiert werden, die vom Modell erstellt wurden.

Das Beispielmodell hat mit hoher Genauigkeit festgestellt, dass alle Besucher mit mehr als 130 Interaktionen in fünf Minuten Bots sind. Diese Informationen können jetzt zur Verfeinerung Ihrer Bot-Filter-SQL-Abfragen verwendet werden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie besser, wie Sie mit [!DNL Query Service] und maschinellem Lernen die Bot-Aktivität bestimmen und filtern können.

Andere Dokumente, die die Vorteile der [!DNL Query Service] für die strategischen geschäftlichen Einblicke Ihres Unternehmens zeigen, sind [Anwendungsfall zum Durchsuchen aufgegeben](./abandoned-browse.md).
