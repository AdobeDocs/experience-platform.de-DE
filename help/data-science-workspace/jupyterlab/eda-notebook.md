---
keywords: Experience Platform;JupyterLab;Notebooks;Datenwissenschafts-Arbeitsbereich;beliebte Themen;Notebooks zur Datenanalyse;eda; explorative Datenanalyse;Datenwissenschaft
solution: Experience Platform
title: Notebook zur explorativen Datenanalyse (EDA)
type: Tutorial
description: In diesem Handbuch wird beschrieben, wie Sie mit dem Notebook zur explorativen Datenanalyse (EDA) Muster in Web-Daten erkennen, Ereignisse mit einem Prognoseziel aggregieren, aggregierte Daten bereinigen und die Beziehung zwischen Prädiktoren und Zielen verstehen können.
exl-id: 48209326-0a07-4b5c-8b49-a2082a78fa47
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 100%

---

# Untersuchen Web-basierter Daten für Prognosemodelle mit dem Notebook zur explorativen Datenanalyse (EDA)

Das Notebook zur explorativen Datenanalyse (EDA) hilft Ihnen beim Erkennen von Datenmustern, Überprüfen der Datenplausibilität und Zusammenfassen der relevanten Daten für Prognosemodelle.

Das EDA-Notebook-Beispiel wurde im Hinblick auf Web-basierte Daten optimiert und besteht aus zwei Teilen. Teil 1 beginnt mit der Verwendung des Abfrage-Service zum Anzeigen von Trends und Daten-Schnappschüssen. Als Nächstes werden die Daten zur explorativen Datenanalyse auf Profil- und Besucherebene aggregiert.

Teil 2 beginnt mit der deskriptiven Analyse aggregierter Daten mithilfe von Python-Bibliotheken. Dieses Notebook enthält Visualisierungen wie Histogramme, Streudiagramme, Boxplot-Diagramme und eine Korrelationsmatrix, um praktische Insights zu erhalten, mit denen bestimmt wird, welche Funktionen bei der Prognose eines Ziels am ehesten hilfreich sein dürften.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, nutzen Sie bitte das [[!DNL JupyterLab] Benutzerhandbuch](./overview.md) für eine allgemeine Einführung in [!DNL JupyterLab] und dessen Rolle im Datenwissenschafts-Arbeitsbereich. Wenn Sie Ihre eigenen Daten verwenden, lesen Sie bitte außerdem die Dokumentation zum [Datenzugriff in  [!DNL Jupyterlab] -Notebooks](./access-notebook-data.md). Dieses Handbuch enthält wichtige Informationen zu Notebook-Dateneinschränkungen.

Dieses Notebook verwendet einen midvalues-Datensatz in Form von Adobe Analytics Experience Events-Daten aus dem Analytics Analysis Workspace. Um das EDA-Notebook zu verwenden, müssen Sie Ihre Datentabelle mit den folgenden Werten `target_table` und `target_table_id` definieren. Es können beliebige midvalues-Datensätze verwendet werden.

Um diese Werte zu finden, folgen Sie den im Abschnitt [Schreiben in einen Datensatz in Python](./access-notebook-data.md#write-python) des JupyterLab-Handbuchs für den Datenzugriff beschriebenen Schritten. Der Datensatzname (`target_table`) befindet sich im Datensatzverzeichnis. Sobald Sie mit der rechten Maustaste auf den Datensatz klicken, um Daten auf einem Notebook zu untersuchen oder darauf zu schreiben, wird eine Datensatz-ID (`target_table_id`) im Eintrag für den ausführbaren Code bereitgestellt.

## Datenerkennung

Dieser Abschnitt enthält Konfigurationsschritte und Beispielabfragen, mit denen Trends wie die „Top 10 der Städte nach Benutzeraktivität“ oder „Top 10 der angezeigten Produkte“ angezeigt werden.

### Konfiguration von Bibliotheken

JupyterLab unterstützt mehrere Bibliotheken. Der folgende Code kann eingefügt und in einer Code-Zelle ausgeführt werden, um alle in diesem Beispiel verwendeten erforderlichen Pakete zu erfassen und zu installieren. Sie können jenseits dieses Beispiels zusätzliche oder alternative Pakete für Ihre eigene Datenanalyse verwenden. Für eine Liste der unterstützten Pakete kopieren Sie `!pip list --format=columns` und fügen Sie den Inhalt in eine neue Zelle ein.

```python
!pip install colorama
import chart_studio.plotly as py
import plotly.graph_objs as go
from plotly.offline import iplot
from scipy import stats
import numpy as np
import warnings
warnings.filterwarnings('ignore')
from scipy.stats import pearsonr
import matplotlib.pyplot as plt
from scipy.stats import pearsonr
import pandas as pd
import math
import re
import seaborn as sns
from datetime import datetime
import colorama
from colorama import Fore, Style
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
pd.set_option('display.width', 1000)
pd.set_option('display.expand_frame_repr', False)
pd.set_option('display.max_colwidth', -1)
```

### Verbinden mit Adobe Experience Platform [!DNL Query Service]

Mit [!DNL JupyterLab] in Platform können Sie SQL in einem [!DNL Python]-Notebook verwenden, um über den [Abfrage-Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=de) auf Daten zuzugreifen. Der Zugriff auf Daten über den [!DNL Query Service] kann aufgrund der kürzeren Ausführungszeiten bei der Bearbeitung großer Datensätze nützlich sein. Beachten Sie, dass Datenabfragen mit dem [!DNL Query Service] ein Limit bei der Verarbeitungszeit von 10 Minuten aufweisen.

Bevor Sie den [!DNL Query Service] in [!DNL JupyterLab] verwenden, sollten Sie Grundlagenkenntnisse zur [[!DNL Query Service] -SQL-Syntax](https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html?lang=de) besitzen.

Um den Abfrage-Service in JupyterLab zu nutzen, müssen Sie zunächst eine Verbindung zwischen Ihrem ausgeführten Python-Notebook und dem Abfrage-Service herstellen. Dies kann durch Ausführen der folgenden Zelle erreicht werden.

```python
qs_connect()
```

### Definieren des midvalues-Datensatzes zur Untersuchung

Um Daten abfragen und untersuchen zu können, muss eine Tabelle mit midvalues-Datensätzen bereitgestellt werden. Kopieren Sie die Werte `table_name` und `table_id` und ersetzen Sie sie durch Ihre eigenen Datentabellenwerte.

```python
target_table = "table_name"
target_table_id = "table_id"
```

Nach der Fertigstellung sollte diese Zelle dem folgenden Beispiel ähneln:

```python
target_table = "cross_industry_demo_midvalues"
target_table_id = "5f7c40ef488de5194ba0157a"
```

### Untersuchen des Datensatzes auf verfügbare Daten

Mithilfe der unten angegebenen Zelle können Sie den in der Tabelle erfassten Datumsbereich anzeigen. Die Untersuchung der Anzahl der Tage, des ersten Datums und des letzten Datums dient der Auswahl eines Datumsbereichs für weitere Analysen.

```python
%%read_sql -c QS_CONNECTION
SELECT distinct Year(timestamp) as Year, Month(timestamp) as Month, count(distinct DAY(timestamp)) as Count_days, min(DAY(timestamp)) as First_date, max(DAY(timestamp)) as Last_date, count(timestamp) as Count_hits
from {target_table}
group by Month(timestamp), Year(timestamp)
order by Year, Month;
```

Beim Ausführen der Zelle wird die folgende Ausgabe erzeugt:

![Ausgabe des Abfragedatums](../images/jupyterlab/eda/query-date-output.PNG)

### Konfigurieren von Datumsangaben zur Erkennung von Datensätzen

Nachdem Sie die verfügbaren Daten für die Datensatzerkennung ermittelt haben, müssen die folgenden Parameter aktualisiert werden. Die in dieser Zelle konfigurierten Datumsangaben werden nur zur Datenerkennung in Form von Abfragen verwendet. Die Datumsangaben werden später in diesem Handbuch erneut in geeignete Bereiche zur explorativen Datenanalyse aktualisiert.

```python
target_year = "2020" ## The target year
target_month = "02" ## The target month
target_day = "(01,02,03)" ## The target days
```

### Datensatzerkennung

Nachdem Sie alle Parameter konfiguriert und den [!DNL Query Service] gestartet haben sowie über einen Datumsbereich verfügen, können Sie mit dem Lesen von Datenzeilen beginnen. Sie sollten die Anzahl der Zeilen begrenzen, die Sie lesen.

```python
from platform_sdk.dataset_reader import DatasetReader
from datetime import date
dataset_reader = DatasetReader(PLATFORM_SDK_CLIENT_CONTEXT, dataset_id=target_table_id)
# If you do not see any data or would like to expand the default date range, change the following query
Table = dataset_reader.limit(5).read()
```

Verwenden Sie die folgende Zelle, um die Anzahl der im Datensatz verfügbaren Spalten anzuzeigen:

```python
print("\nNumber of columns:",len(Table.columns))
```

Verwenden Sie die folgende Zelle, um die Zeilen des Datensatzes anzuzeigen. In diesem Beispiel ist die Anzahl der Zeilen auf fünf begrenzt.

```python
Table.head(5)
```

![Ausgabe der Tabellenzeile](../images/jupyterlab/eda/data-table-overview.PNG)

Sobald Sie wissen, welche Daten im Datensatz enthalten sind, kann es nützlich sein, den Datensatz weiter aufzuschlüsseln. In diesem Beispiel werden die Spaltennamen und Datentypen für jede Spalte aufgelistet, während die Ausgabe verwendet wird, um zu überprüfen, ob der Datentyp korrekt ist oder nicht.

```python
ColumnNames_Types = pd.DataFrame(Table.dtypes)
ColumnNames_Types = ColumnNames_Types.reset_index()
ColumnNames_Types.columns = ["Column_Name", "Data_Type"]
ColumnNames_Types
```

![Spaltenname und Datentypliste](../images/jupyterlab/eda/data-columns.PNG)

### Untersuchen von Datensatz-Trends

Der folgende Abschnitt enthält vier Beispielabfragen, mit denen Trends und Muster in Daten untersucht werden. Die folgenden Beispiele sind nicht vollständig, decken jedoch einige der am häufigsten angesehenen Funktionen ab.

**Stündliche Aktivitätsanzahl für einen bestimmten Tag**

Diese Abfrage analysiert die Anzahl der Aktionen und Klicks über den ganzen Tag. Die Ausgabe wird in Form einer Tabelle mit Metriken zur Aktivitätsanzahl für jede Stunde des Tages dargestellt.

```sql
%%read_sql query_2_df -c QS_CONNECTION

SELECT Substring(timestamp, 12, 2)                        AS Hour, 
       Count(enduserids._experience.aaid.id) AS Count 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year} 
       AND Month(timestamp) = {target_month}  
       AND Day(timestamp) in {target_day}
GROUP  BY Hour
ORDER  BY Hour;
```

![Ausgabe für Abfrage 1](../images/jupyterlab/eda/hour-count-raw.PNG)

Nach Bestätigung, dass die Abfrage funktioniert, können die Daten in einem univariaten Histogramm dargestellt werden, um die Übersichtlichkeit zu erhöhen.

```python
trace = go.Bar(
    x = query_2_df['Hour'],
    y = query_2_df['Count'],
    name = "Activity Count"
)

layout = go.Layout(
    title = 'Activity Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Balkendiagrammausgabe für Abfrage 1](../images/jupyterlab/eda/activity-count-by-hour-of-day.png)

**Top 10 der angezeigten Seiten für einen bestimmten Tag**

Diese Abfrage analysiert, welche Seiten an einem bestimmten Tag am häufigsten angezeigt wurden. Die Ausgabe wird in Form einer Tabelle mit Metriken zum Seitennamen und zur Anzahl der Seitenansichten dargestellt.

```sql
%%read_sql query_4_df -c QS_CONNECTION

SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

Nach Bestätigung, dass die Abfrage funktioniert, können die Daten in einem univariaten Histogramm dargestellt werden, um die Übersichtlichkeit zu erhöhen.

```python
trace = go.Bar(
    x = query_4_df['Page_Name'],
    y = query_4_df['Page_Views'],
    name = "Page Views"
)

layout = go.Layout(
    title = 'Top Ten Viewed Pages For a Given Day',
    width = 1000,
    height = 600,
    xaxis = dict(title = 'Page_Name'),
    yaxis = dict(title = 'Page_Views')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Top 10 der angezeigten Seiten](../images/jupyterlab/eda/top-ten-viewed-pages-for-a-given-day.png)

**Top 10 der Städte gruppiert nach Benutzeraktivität**

Diese Abfrage analysiert, aus welchen Städten die Daten stammen.

```sql
%%read_sql query_6_df -c QS_CONNECTION

SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

Nach Bestätigung, dass die Abfrage funktioniert, können die Daten in einem univariaten Histogramm dargestellt werden, um die Übersichtlichkeit zu erhöhen.

```python
trace = go.Bar(
    x = query_6_df['state_city'],
    y = query_6_df['Count'],
    name = "Activity by City"
)

layout = go.Layout(
    title = 'Top Ten Cities by User Activity',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'City'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Top 10 der Städte](../images/jupyterlab/eda/top-ten-cities-by-user-activity.png)

**Top 10 der angezeigten Produkte**

Diese Abfrage liefert eine Liste der zehn am häufigsten angezeigten Produkte. Im folgenden Beispiel wird die Funktion `Explode()` verwendet, um jedes Produkt im Objekt `productlistitems` in einer eigenen Zeile zurückzugeben.  Auf diese Weise können Sie eine verschachtelte Abfrage ausführen, um Produktansichten für verschiedene SKUs zu aggregieren.

```sql
%%read_sql query_7_df -c QS_CONNECTION

SELECT Product_List_Items.sku AS Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems) AS Product_List_Items, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  Year(timestamp) = {target_year}
              AND Month(timestamp) = {target_month}
              AND Day(timestamp) in {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

Nach Bestätigung, dass die Abfrage funktioniert, können die Daten in einem univariaten Histogramm dargestellt werden, um die Übersichtlichkeit zu erhöhen.

```python
trace = go.Bar(
    x = "SKU-" + query_7_df['Product_SKU'],
    y = query_7_df['Total_Product_Views'],
    name = "Product View"
)

layout = go.Layout(
    title = 'Top Ten Viewed Products',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'SKU'),
    yaxis = dict(title = 'Product View Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Top 10 der Produktansichten](../images/jupyterlab/eda/top-ten-viewed-products.png)

Nachdem Sie die Trends und Muster der Daten untersucht haben, sollten Sie eine gute Vorstellung davon haben, welche Funktionen Sie zur Prognose eines Ziels erstellen möchten. Bei der Durchsicht von Tabellen können die Form jedes Datenattributs, offensichtliche Fehldarstellungen und große Ausreißer in den Werten schnell hervorgehoben werden. Außerdem ist dies ein Ausgangspunkt, um Beziehungen zwischen den Attributen zwecks Untersuchung vorzuschlagen.

## Explorative Datenanalyse

Die explorative Datenanalyse wird verwendet, um Ihr Verständnis der Daten zu verfeinern und eine Intuition für überzeugende Fragen zu entwickeln, die als Grundlage für die Modellierung verwendet werden können.

Nachdem Sie den Schritt zur Datenerkennung abgeschlossen haben, haben Sie auf Ereignisebene Daten mit einigen Aggregationen auf Ereignis-, Stadt- oder Benutzer-ID-Ebene untersucht, um Trends für einen Tag anzuzeigen. Diese Daten sind zwar wichtig, geben aber kein vollständiges Bild. Sie verstehen immer noch nicht, was einen Kauf auf Ihrer Website auslöst.

Um dies zu verstehen, müssen Sie Daten auf Profil-/Besucherebene aggregieren, ein Kaufziel definieren und statistische Konzepte wie Korrelation, Boxplot-Diagramme und Streudiagramme anwenden. Diese Methoden werden verwendet, um die Aktivitätsmuster von Kaufenden und Nicht-Kaufenden im von Ihnen definierten Prognosefenster zu vergleichen.

Die folgenden Funktionen werden in diesem Abschnitt erstellt und untersucht:

- `COUNT_UNIQUE_PRODUCTS_PURCHASED`: Die Anzahl der gekauften Einzelprodukte.
- `COUNT_CHECK_OUTS`: Die Anzahl der Kassengänge
- `COUNT_PURCHASES`: Die Anzahl der Käufe
- `COUNT_INSTANCE_PRODUCTADDS`: Die Anzahl der Instanzen, in denen Produkte hinzugefügt wurden.
- `NUMBER_VISITS`: Die Anzahl der Besuche.
- `COUNT_PAID_SEARCHES`: Die Anzahl der Paid Searches.
- `DAYS_SINCE_VISIT`: Die Anzahl der Tage seit dem letzten Besuch.
- `TOTAL_ORDER_REVENUE`: Der gesamte Bestellumsatz.
- `DAYS_SINCE_PURCHASE`: Die Anzahl der Tage seit dem vorherigen Kauf
- `AVG_GAP_BETWEEN_ORDERS_DAYS`: Der durchschnittliche Abstand zwischen Käufen in Tagen
- `STATE_CITY`: Enthält das Bundesland bzw. den Kanton und die Stadt

Bevor Sie mit der Datenaggregation fortfahren, müssen Sie die Parameter für die Prognosevariable definieren, die bei der explorativen Datenanalyse verwendet wird. Anders ausgedrückt: Was erwarten Sie von Ihrem Datenwissenschaftsmodell? Zu den häufig verwendeten Parametern gehören ein Ziel, ein Prognosezeitraum und ein Analysezeitraum.

Wenn Sie das EDA-Notebook verwenden, müssen Sie die unten stehenden Werte ersetzen, bevor Sie fortfahren.

```python
goal = "commerce.`order`.purchaseID" #### prediction variable
goal_column_type = "numerical" #### choose either "categorical" or "numerical"
prediction_window_day_start = "2020-01-01" #### YYYY-MM-DD
prediction_window_day_end = "2020-01-31" #### YYYY-MM-DD
analysis_period_day_start = "2020-02-01" #### YYYY-MM-DD
analysis_period_day_end = "2020-02-28" #### YYYY-MM-DD

### If the goal is a categorical goal then select threshold for the defining category and creating bins. 0 is no order placed, and 1 is at least one order placed:
threshold = 1
```

### Datenaggregation für die Erstellung von Funktionen und Zielen

Um mit der explorativen Analyse zu beginnen, müssen Sie ein Ziel auf Profilebene erstellen und dann Ihren Datensatz aggregieren. In diesem Beispiel werden zwei Abfragen bereitgestellt. Die erste Abfrage umfasst die Erstellung eines Ziels. Die zweite Abfrage muss so aktualisiert werden, dass sie andere Variablen als die in der ersten Abfrage enthält. Sie sollten ggf. den `limit`-Wert für Ihre Abfrage aktualisieren. Nach Durchführung der folgenden Abfragen stehen nun aggregierte Daten zur Untersuchung zur Verfügung.

```sql
%%read_sql target_df -d -c QS_CONNECTION

SELECT DISTINCT endUserIDs._experience.aaid.id                  AS ID,
       Count({goal})                                            AS TARGET
FROM   {target_table}
WHERE DATE(TIMESTAMP) BETWEEN '{prediction_window_day_start}' AND '{prediction_window_day_end}'
GROUP BY endUserIDs._experience.aaid.id;
```

```sql
%%read_sql agg_data -d -c QS_CONNECTION

SELECT z.*, z1.state_city as STATE_CITY
from
((SELECT y.*,a2.AVG_GAP_BETWEEN_ORDERS_DAYS as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(select a1.*, f.DAYS_SINCE_PURCHASE as DAYS_SINCE_PURCHASE
from
(SELECT DISTINCT a.ID  AS ID,
COUNT(DISTINCT Product_Items.SKU) as COUNT_UNIQUE_PRODUCTS_PURCHASED,
COUNT(a.check_out) as COUNT_CHECK_OUTS,
COUNT(a.purchases) as COUNT_PURCHASES, 
COUNT(a.product_list_adds) as COUNT_INSTANCE_PRODUCTADDS,
sum(CASE WHEN a.search_paid = 'TRUE' THEN 1 ELSE 0 END) as COUNT_PAID_SEARCHES,
DATEDIFF('{analysis_period_day_end}', MAX(a.date_a)) as DAYS_SINCE_VISIT,
ROUND(SUM(Product_Items.priceTotal * Product_Items.quantity), 2) AS TOTAL_ORDER_REVENUE
from 
(SELECT endUserIDs._experience.aaid.id as ID,
commerce.`checkouts`.value as check_out,
commerce.`order`.purchaseID as purchases, 
commerce.`productListAdds`.value as product_list_adds,
search.isPaid as search_paid,
DATE(TIMESTAMP) as date_a,
Explode(productlistitems) AS Product_Items
from {target_table}
Where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as a
group by a.ID) as a1
left join 
(SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
DATEDIFF('{analysis_period_day_end}', max(DATE(TIMESTAMP))) as DAYS_SINCE_PURCHASE
from {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
and commerce.`order`.purchaseid is not null
GROUP BY endUserIDs._experience.aaid.id) as f
on f.ID = a1.ID
where a1.COUNT_PURCHASES>0) as y
left join
(select ab.ID, avg(DATEDIFF(ab.ORDER_DATES, ab.PriorDate)) as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(SELECT distinct endUserIDs._experience.aaid.id as ID, TO_DATE(DATE(TIMESTAMP)) as ORDER_DATES, 
TO_DATE(LAG(DATE(TIMESTAMP),1) OVER (PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP))) as PriorDate
FROM {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
AND commerce.`order`.purchaseid is not null) AS ab
where ab.PriorDate is not null
GROUP BY ab.ID) as a2
on a2.ID = y.ID) z    
left join
(select t.ID, t.state_city from
(
SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) as state_city, 
ROW_NUMBER() OVER(PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP) DESC) AS ROWNUMBER
FROM   {target_table}
WHERE  DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as t
where t.ROWNUMBER = 1) z1
on z.ID = z1.ID)
limit 500000;
```

### Zusammenführen der Funktionen im aggregierten Datensatz mit einem Ziel

Die folgende Zelle wird verwendet, um die im vorherigen Beispiel beschriebenen Funktionen im aggregierten Datensatz mit Ihrem Prognoseziel zusammenzuführen.

```python
Data = pd.merge(agg_data,target_df, on='ID',how='left')
Data['TARGET'].fillna(0, inplace=True)
```

Die nächsten drei Beispielzellen werden verwendet, um sicherzustellen, dass die Zusammenführung erfolgreich war.

`Data.shape` gibt die Anzahl der Spalten gefolgt von der Anzahl der Zeilen zurück, z. B. (11913, 12).

```python
Data.shape
```

`Data.head(5)` gibt eine Tabelle mit 5 Datenzeilen zurück. Die zurückgegebene Tabelle enthält alle 12 Spalten aggregierter Daten, die einer Profilkennung zugeordnet sind.

```python
Data.head(5)
```

![Beispieltabelle](../images/jupyterlab/eda/raw-aggregate-data.PNG)

Mit dieser Zelle wird die Anzahl der eindeutigen Profile gedruckt.

```python
print("Count of unique profiles:", (len(Data)))
```

### Erkennen von fehlenden Werten und Ausreißern

Nachdem Sie die Datenaggregation abgeschlossen und diese mit Ihrem Ziel zusammengeführt haben, müssen Sie die Daten überprüfen, was auch als Konsistenzprüfung der Daten bezeichnet wird.

Dieser Vorgang umfasst die Identifizierung von fehlenden Werten und Ausreißern. Wenn Probleme erkannt werden, müssen als Nächstes bestimmte Strategien zu deren Bewältigung entwickelt werden.

>[!NOTE]
>
>Während dieses Schritts stellen Sie möglicherweise fehlerhafte Werte fest, die auf ein Problem bei der Datenprotokollierung hinweisen können.

```python
Missing = pd.DataFrame(round(Data.isnull().sum()*100/len(Data),2))
Missing.columns =['Percentage_missing_values'] 
Missing['Features'] = Missing.index
```

Die folgende Zelle wird verwendet, um die fehlenden Werte zu visualisieren.

```python
trace = go.Bar(
    x = Missing['Features'],
    y = Missing['Percentage_missing_values'],
    name = "Percentage_missing_values")

layout = go.Layout(
    title = 'Missing values',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of missing values')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Fehlende Werte](../images/jupyterlab/eda/missing-values.png)

Nach Erkennung fehlender Werte ist es wichtig, Ausreißer zu identifizieren. Parametrische Statistiken wie Mittelwert, Standardabweichung und Korrelation reagieren äußerst empfindlich auf Ausreißer. Darüber hinaus basieren die Annahmen gemeinsamer statistischer Verfahren, wie z. B. bei linearen Regressionen, ebenfalls auf diesen Statistiken. Das bedeutet, dass Ausreißer eine Analyse wirklich durcheinanderbringen können.

Um Ausreißer zu identifizieren, wird in diesem Beispiel der Interquartilbereich verwendet. Der Interquartilbereich (IQB) ist der Bereich zwischen dem ersten und dritten Quartil (25. und 75. Perzentil). In diesem Beispiel werden alle Datenpunkte erfasst, die entweder unter das 1,5-Fache des IQB unter dem 25. Perzentil oder das 1,5-Fache des IQB über dem 75. Perzentil fallen. Werte, die unter einen von diesen fallen, werden in der folgenden Zelle als Ausreißer definiert.

>[!TIP]
>
>Für die Korrektur von Ausreißern müssen Sie das Geschäft und die Branche, in der Sie arbeiten, verstehen. Manchmal lässt sich eine Beobachtung nicht ignorieren, nur weil es sich um einen Ausreißer handelt. Ausreißer können legitime Beobachtungen sein und sind oft besonders interessant. Weitere Informationen zum Ignorieren von Ausreißern finden Sie im [Schritt zur optionalen Datenbereinigung](#optional-data-clean).

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)
Data_numerical1 = Data_numerical

for i in range(0,len(Data_numerical1.columns)):
    Q1 = Data_numerical1.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical1.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical1.iloc[:,i] = np.where(Data_numerical1.iloc[:,i]<(Q1 - 1.5 * IQR),np.nan, np.where(Data_numerical1.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                    np.nan,Data_numerical1.iloc[:,i]))
    
Outlier = pd.DataFrame(round(Data_numerical1.isnull().sum()*100/len(Data),2))
Outlier.columns =['Percentage_outliers'] 
Outlier['Features'] = Outlier.index   
```

Wie immer ist es wichtig, die Ergebnisse zu visualisieren.

```python
trace = go.Bar(
    x = Outlier['Features'],
    y = Outlier['Percentage_outliers'],
    name = "Percentage_outlier")

layout = go.Layout(
    title = 'Outliers',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of outliers')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Ausreißer-Diagramm](../images/jupyterlab/eda/outliers.png)

### Univariate Analyse

Nachdem Ihre Daten in Bezug auf fehlende Werte und Ausreißer korrigiert wurden, können Sie Ihre Analyse starten. Es gibt drei Arten von Analysen: univariate, bivariate und multivariate Analysen. Die univariate Analyse nimmt Daten auf, fasst sie zusammen und findet Muster in den Daten anhand der Beziehungen einzelner Variablen. Die bivariate Analyse betrachtet mehrere Variablen auf einmal, die multivariate Analyse hingegen drei oder mehr Variablen.

Im folgenden Beispiel wird eine Tabelle erstellt, um die Verteilung der Funktionen zu visualisieren.

```python
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
distribution = pd.DataFrame([Data_numerical.count(),Data_numerical.mean(),Data_numerical.quantile(0), Data_numerical.quantile(0.01),
                             Data_numerical.quantile(0.05),Data_numerical.quantile(0.25), Data_numerical.quantile(0.5),
                        Data_numerical.quantile(0.75),  Data_numerical.quantile(0.95),Data_numerical.quantile(0.99), Data_numerical.max()])
distribution = distribution.T
distribution.columns = ['Count', 'Mean', 'Min', '1st_perc','5th_perc','25th_perc', '50th_perc','75th_perc','95th_perc','99th_perc','Max']
distribution
```

![Verteilung der Funktionen](../images/jupyterlab/eda/distribution-of-features.PNG)

Sobald Sie über eine Verteilung der Funktionen verfügen, können Sie visualisierte Datendiagramme mithilfe eines Arrays erstellen. Die folgenden Zellen werden verwendet, um die obige Tabelle mit numerischen Daten zu visualisieren.

```python
A = sns.palplot(sns.color_palette("Blues"))
```

```python
for column in Data_numerical.columns[0:]:
    plt.figure(figsize=(5, 4))
    plt.ticklabel_format(style='plain', axis='y')
    sns.distplot(Data_numerical[column], color = A, kde=False, bins=6, hist_kws={'alpha': 0.4});
```

![Numerische Datendiagramme](../images/jupyterlab/eda/univaiate-graphs.png)

### Kategoriale Daten

Kategoriale Daten werden gruppiert, um die in den einzelnen Spalten aggregierter Daten enthaltenen Werte und deren Verteilung zu verstehen. In diesem Beispiel werden die zehn wichtigsten Kategorien verwendet, um bei der Erstellung der Verteilungen zu helfen. Beachten Sie, dass in einer Spalte Tausende eindeutiger Werte enthalten sein können. Sie brauchen kein überfülltes Diagramm, aus dem niemand schlau wird. Mit Blick auf Ihr Geschäftsziel liefert das Gruppieren von Daten aussagekräftigere Ergebnisse.

```python
Data_categorical = Data.select_dtypes(include='object')
Data_categorical.drop(['ID'], axis = 1, inplace = True, errors = 'ignore')
```

```python
for column in Data_categorical.columns[0:]:
    if (len(Data_categorical[column].value_counts())>10):
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, order = Data_categorical[column].value_counts().iloc[:10].index, palette="Set2");
    else:
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, palette="Set2");
```

![Spalten kategorialer Daten](../images/jupyterlab/eda/graph-category.PNG)

### Entfernen von Spalten mit nur einem eindeutigen Wert

Spalten, die nur einen Wert aufweisen, fügen der Analyse keine Informationen hinzu und können entfernt werden.

```python
for col in Data.columns:
    if len(Data[col].unique()) == 1:
        if col == 'TARGET':
            print(Fore.RED + '\033[1m' + 'WARNING: TARGET HAS A SINGLE UNIQUE VALUE, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        elif col == 'ID':
            print(Fore.RED + '\033[1m' + 'WARNING: THERE IS ONLY ONE PROFILE IN THE DATA, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        else:
            print('Dropped column:',col)
            Data.drop(col,inplace=True,axis=1)
```

Nachdem Sie Einzelwertspalten entfernt haben, überprüfen Sie die übrigen Spalten auf Fehler, indem Sie den Befehl `Data.columns` in einer neuen Zelle verwenden.

### Korrigieren fehlender Werte

Im folgenden Abschnitt finden Sie einige Beispielansätze zur Korrektur fehlender Werte. Obwohl in den oben genannten Daten nur eine Spalte einen fehlenden Wert enthält, werden mit den nachfolgenden Beispielzellen die Werte für alle Datentypen korrigiert. Dazu gehören:

- Numerische Datentypen: Eingabe von 0 oder „max“, wo zutreffend
- Kategoriale Datentypen: Eingabe des Modalwerts

```python
#### Select only numerical data
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])

#### For columns that contain days we impute max days of history for null values, for rest all we impute 0

# Imputing days with max days of history
Days_cols = [col for col in Data_numerical.columns if 'DAYS_' in col]
d1 = datetime.strptime(analysis_period_day_start, "%Y-%m-%d")
d2 = datetime.strptime(analysis_period_day_end, "%Y-%m-%d")
A = abs((d2 - d1).days)

for column in Days_cols:
    Data[column].fillna(A, inplace=True)

# Imputing 0
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Missing_numerical = Data_numerical.columns[Data_numerical.isnull().any()].tolist()

for column in Missing_numerical:
    Data[column].fillna(0, inplace=True)
```

```python
#### Correct for missing values in categorical columns (Replace with mode)
Data_categorical = Data.select_dtypes(include='object')
Missing_cat = Data_categorical.columns[Data_categorical.isnull().any()].tolist() 
for column in Missing_cat:
    Data[column].fillna(Data[column].mode()[0], inplace=True)
```

Anschließend kann für die bereinigten Daten eine bivariate Analyse durchgeführt werden.

### Bivariate Analyse

Die bivariate Analyse wird verwendet, um die Beziehung zwischen zwei Wertesätzen zu verstehen, z. B. denen Ihrer Funktionen und einer Zielvariablen. Da verschiedene Diagramme kategorialen und numerischen Datentypen entsprechen, sollte diese Analyse für jeden Datentyp separat durchgeführt werden. Die folgenden Diagramme werden für die bivariate Analyse empfohlen:

- **Korrelation**: Ein Korrelationskoeffizient misst die Stärke einer Beziehung zwischen zwei Funktionen. Die Korrelation weist Werte zwischen -1 und 1 auf. Dabei steht 1 für eine starke positive Beziehung, -1 für eine starke negative Beziehung und das Ergebnis 0 für überhaupt keine Beziehung.
- **Paardiagramm**: Paardiagramme sind eine einfache Möglichkeit, Beziehungen zwischen den einzelnen Variablen zu visualisieren. Sie erzeugen eine Matrix von Beziehungen zwischen den einzelnen Variablen in den Daten.
- **Heatmap**: Heatmaps stellen die Korrelationskoeffizienten für alle Variablen im Datensatz dar.
- **Boxplot-Diagramm**: Boxplot-Diagramme sind eine standardisierte Methode zur Anzeige der Datenverteilung basierend auf einer aus fünf Zahlen bestehenden Zusammenfassung (Minimum, erstes Quartil (Q1), Median, drittes Quartil (Q3) und Maximum).
- **Zähldiagramm**: Zähldiagramme sind wie Histogramme oder Balkendiagramme für einige kategoriale Funktionen. Sie zeigen die Anzahl der Vorkommnisse eines Elements basierend auf einem bestimmten Kategorietyp an.

Um die Beziehung zwischen der „Ziel“-Variablen und den Prädiktoren/Funktionen zu verstehen, werden Diagramme basierend auf Datentypen verwendet. Für numerische Funktionen sollten Sie ein Boxplot-Diagramm verwenden, wenn die „Ziel“-Variable kategorial ist, sowie ein Paardiagramm und eine Heatmap, wenn die „Ziel“-Variable numerisch ist.

Für kategoriale Funktionen sollten Sie ein Zähldiagramm verwenden, wenn die „Ziel“-Variable kategorial ist, sowie ein Boxplot-Diagramm, wenn die „Ziel“-Variable numerisch ist. Diese Methoden helfen beim Verständnis von Beziehungen. Diese Beziehungen können in Form von Funktionen, Prädiktoren und Zielen vorliegen.

**Numerische Prädiktoren**

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET_categorical.astype(int)], axis = 1)
        ncols_for_charts = len(Data_numerical.columns)-1
        nrows_for_charts = math.ceil(ncols_for_charts/4)
        fig, axes = plt.subplots(nrows=nrows_for_charts, ncols=4, figsize=(18, 15))
        for idx, feat in enumerate(Data_numerical.columns[:-1]):
            ax = axes[int(idx // 4), idx % 4]
            sns.boxplot(x='TARGET_categorical', y=feat, data=Data_numerical, ax=ax)
            ax.set_xlabel('')
            ax.set_ylabel(feat)
            fig.tight_layout();
    else:
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        TARGET = pd.DataFrame(Data_numerical.TARGET)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET.astype(int)], axis = 1)
        for i in Data_numerical.columns[:-1]:
            sns.pairplot(x_vars=i, y_vars=['TARGET'], data=Data_numerical, height = 4)
        f, ax = plt.subplots(figsize = (10,8))
        corr = Data_numerical.corr()
```

Durch Ausführen der Zelle werden folgende Ausgaben erzeugt:

![Diagramme](../images/jupyterlab/eda/bivariant-graphs.png)

![Heatmap](../images/jupyterlab/eda/bi-graph10.PNG)

**Kategoriale Prädiktoren**

Das folgende Beispiel wird verwendet, um die Häufigkeitsverteilung für die zehn wichtigsten Kategorien jeder kategorialen Variablen darzustellen und anzuzeigen.

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Cat_columns = Data_categorical
        Data_categorical = pd.concat([TARGET_categorical,Data_categorical], axis =1)
        for column in Cat_columns.columns:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            plt.figure(figsize=(12, 8))
            sns.countplot(x="TARGET_categorical",hue=column, data = Data_categorical1, palette = 'Blues')
            plt.xlabel("GOAL")
            plt.ylabel("COUNT")
            plt.show();
    else:
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Target = Data.TARGET
        Data_categorical = pd.concat([Data_categorical,Target], axis =1)
        for column in Data_categorical.columns[:-1]:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            sns.catplot(x=column, y="TARGET", kind = "boxen", data =Data_categorical1, height=5, aspect=13/5);
```

Beim Ausführen der Zelle wird die folgende Ausgabe erzeugt:

![Kategoriebeziehung](../images/jupyterlab/eda/categorical-predictor.PNG)

### Wichtige numerische Funktionen

Mithilfe der Korrelationsanalyse können Sie eine Liste der zehn wichtigsten numerischen Funktionen erstellen. Diese Funktionen können alle für die Prognose der „Ziel“-Funktion verwendet werden. Diese Liste kann als Funktionsliste verwendet werden, wenn Sie mit der Erstellung Ihres Modells beginnen.

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
    Correlation = pd.DataFrame(Data_numerical.drop("TARGET", axis=1).apply(lambda x: x.corr(Data_numerical.TARGET)))
    Correlation['Corr_abs'] = abs(Correlation)
    Correlation = Correlation.sort_values(by = 'Corr_abs', ascending = False)
    Imp_features = pd.DataFrame(Correlation.index[0:10])
    Imp_features.rename(columns={0:'Important Feature'}, inplace=True)
    print(Imp_features)
```

![Wichtige Funktionen](../images/jupyterlab/eda/important-feature-model.PNG)

### Beispiel-Einblick

Während Sie Ihre Daten analysieren, ist es nicht ungewöhnlich, Einblicke zu gewinnen. Das folgende Beispiel zeigt einen Einblick, der die Neuigkeit und den Geldwert für ein Zielereignis zuordnet.

```python
# Proxy for monetary value is TOTAL_ORDER_REVENUE and proxy for frequency is NUMBER_VISITS
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    sns.lmplot("DAYS_SINCE_VISIT", "TOTAL_ORDER_REVENUE", Data, hue="TARGET", fit_reg=False);
```

![Beispiel-Einblick](../images/jupyterlab/eda/insight.PNG)

## Optionaler Schritt zur Datenbereinigung {#optional-data-clean}

Für die Korrektur von Ausreißern müssen Sie das Geschäft und die Branche, in der Sie arbeiten, verstehen. Manchmal lässt sich eine Beobachtung nicht ignorieren, nur weil es sich um einen Ausreißer handelt. Ausreißer können legitime Beobachtungen sein und sind oft besonders interessant.

Weiterführende Informationen zu Ausreißern und dazu, ob sie ignoriert werden sollten, finden Sie in diesem Beitrag auf der Website [The Analysis Factor](https://www.theanalysisfactor.com/outliers-to-drop-or-not-to-drop/).

Mit der folgenden Beispielzelle werden für Datenpunkte, bei denen es sich um Ausreißer handelt, mithilfe des [Interquartilbereichs](https://www.thoughtco.com/what-is-the-interquartile-range-rule-3126244) Ober- und Untergrenzen festgelegt.

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)

for i in range(0,len(Data_numerical.columns)):
    Q1 = Data_numerical.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical.iloc[:,i] = np.where(Data_numerical.iloc[:,i]<(Q1 - 1.5 * IQR), (Q1 - 1.5 * IQR), np.where(Data_numerical.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                     (Q3 + 1.5 * IQR),Data_numerical.iloc[:,i]))
Data_categorical = Data.select_dtypes(include='object')
Data = pd.concat([Data_categorical, Data_numerical, TARGET], axis = 1)
```

## Nächste Schritte

Nachdem Sie die explorative Datenanalyse abgeschlossen haben, können Sie mit der Modellerstellung beginnen. Sie können auch die Daten und die von Ihnen abgeleiteten Einblicke verwenden, um ein Dashboard mit Tools wie Power BI zu erstellen.

Adobe Experience Platform unterteilt den Modellerstellungsprozess in zwei unterschiedliche Phasen: Rezepte (eine Modellinstanz) und Modelle. Um mit der Rezepterstellung zu beginnen, lesen Sie die Dokumentation zum [Erstellen eines Rezepts in JupyerLab-Notebooks](./create-a-model.md). Dieses Dokument enthält Informationen und Beispiele zum Erstellen, Trainieren und Bewerten von Rezepten in [!DNL JupyterLab]-Notebooks.
