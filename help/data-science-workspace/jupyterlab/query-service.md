---
keywords: Experience Platform;JupyterLab;Notebooks;Data Science Workspace;beliebte Themen;Abfrage
solution: Experience Platform
title: Abfrage-Service im Jupyter-Notebook
topic-legacy: tutorial
type: Tutorial
description: Mit Adobe Experience Platform können Sie SQL (Structured Query Language) in Data Science Workspace verwenden, indem Sie Query Service als Standardfunktion in JupyterLab integrieren. In diesem Lernprogramm werden Beispiele von SQL-Abfragen für gängige Anwendungsfälle zur Untersuchung, Transformation und Analyse von Adobe Analytics-Daten vorgestellt.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 60%

---

# Abfrage-Service im Jupyter-Notebook

[!DNL Adobe Experience Platform] ermöglicht die Verwendung von SQL (Structured Abfrage Language) in  [!DNL Data Science Workspace] durch Integration  [!DNL Query Service] in  [!DNL JupyterLab] eine Standardfunktion.

In diesem Lernprogramm werden Beispieldaten aus SQL-Abfragen für gängige Anwendungsfälle zur Untersuchung, Transformation und Analyse von [!DNL Adobe Analytics]-Daten vorgestellt.

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:

- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich vor dem Fortfahren an Ihren Systemadministrator

- Ein [!DNL Adobe Analytics]-Datensatz

- Ein Verständnis der folgenden Schlüsselkonzepte, die in diesem Tutorial verwendet werden:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Zugriff auf [!DNL JupyterLab] und [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Navigieren Sie in [[!DNL Experience Platform]](https://platform.adobe.com) in der linken Navigationsspalte zu **[!UICONTROL Notebooks]**. Warten Sie einen Moment, bis JupyterLab geladen ist.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Wenn nicht automatisch eine neue Registerkarte &quot;Starter&quot;angezeigt wird, öffnen Sie eine neue Registerkarte &quot;Starter&quot;, indem Sie auf **[!UICONTROL Datei]** und dann **[!UICONTROL Neuer Starter]** klicken.

2. Klicken Sie auf der Registerkarte „Launcher“ auf das Symbol **[!UICONTROL Leer]** in einer Python 3-Umgebung, um ein leeres Notebook zu öffnen.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 ist derzeit die einzige unterstützte Umgebung für Query Service in Notebooks.

3. Klicken Sie in der linken Auswahlleiste auf das Symbol **[!UICONTROL Daten]** und doppelklicken Sie auf das Verzeichnis **[!UICONTROL Datensätze]**, um alle Datensätze aufzulisten.

   ![](../images/jupyterlab/query/dataset.png)

4. Suchen Sie nach einem [!DNL Adobe Analytics]-Datensatz, den Sie untersuchen möchten, und klicken Sie mit der rechten Maustaste auf den Eintrag, klicken Sie auf **[!UICONTROL Abfrage Daten in Notebook]**, um SQL-Abfragen im leeren Notebook zu generieren.

5. Klicken Sie auf die erste generierte Zelle, die die Funktion `qs_connect()` enthält, und führen Sie sie durch Klicken auf die Wiedergabeschaltfläche aus. Diese Funktion erstellt eine Verbindung zwischen Ihrer Notebook-Instanz und [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Kopieren Sie den [!DNL Adobe Analytics]-Datasetnamen aus der zweiten generierten SQL-Abfrage herunter. Dieser Wert ist der Wert nach `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Fügen Sie eine neue Notebook-Zelle ein, indem Sie auf die Schaltfläche **+** klicken.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Kopieren Sie die folgenden Importerklärungen, fügen Sie sie in eine neue Zelle ein und führen Sie sie aus. Diese Erklärungen werden zur Visualisierung Ihrer Daten verwendet:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Kopieren Sie anschließend die folgenden Variablen und fügen Sie sie in eine neue Zelle ein. Ändern Sie die Werte nach Bedarf und führen Sie sie dann aus.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` : Name des  [!DNL Adobe Analytics] Datensatzes.
   - `target_year` : Bestimmtes Jahr, aus dem die Daten der Zielgruppe stammen.
   - `target_month` : Bestimmter Monat, aus dem die Zielgruppe stammt.
   - `target_day` : Bestimmter Tag, von dem die Daten der Zielgruppe stammen.

   >[!NOTE]
   >
   > Sie können diese Werte jederzeit ändern. Führen Sie dabei die Variablenzelle aus, damit die Änderungen angewendet werden.

## Abfragen der Daten {#query-your-data}

Geben Sie die folgenden SQL-Abfragen in die einzelnen Notebook-Zellen ein. Führen Sie eine Abfrage aus, indem Sie sie auf der Zelle auswählen und dann auf die Schaltfläche **[!UICONTROL play]** klicken. Erfolgreiche Abfrageergebnisse oder Fehlerprotokolle werden unterhalb der ausgeführten Zelle angezeigt.

Wenn ein Notebook über einen längeren Zeitraum inaktiv ist, kann die Verbindung zwischen dem Notebook und [!DNL Query Service] unterbrochen werden. In solchen Fällen müssen Sie [!DNL JupyterLab] neu starten, indem Sie die Schaltfläche **Neustart** ![Neustart](../images/jupyterlab/user-guide/restart_button.png) in der oberen rechten Ecke neben dem Betriebsschalter auswählen.

Der Notebook-Kernel setzt, aber die Zellen bleiben, alle Zellen erneut ausführen, um dort weiterzumachen, wo Sie aufgehört hatten.

### Stündliche Besucherzahl {#hourly-visitor-count}

Die folgende Abfrage gibt die stündliche Besucherzahl für ein bestimmtes Datum zurück:

#### Abfrage

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

In der obigen Abfrage ist der Zeitstempel in der `WHERE`-Klausel auf den Wert `target_year` eingestellt. Fügen Sie Variablen in SQL-Abfragen ein, indem Sie diese in geschweifte Klammern setzen (`{}`).

Die erste Zeile der Abfrage enthält die optionale Variable `hourly_visitor`. Die Abfrage-Ergebnisse werden in dieser Variablen als Pandas-Dataframe gespeichert. Das Speichern von Ergebnissen in einem Datenraum ermöglicht es Ihnen, die Ergebnisse der Abfrage später mit einem gewünschten [!DNL Python]-Paket darzustellen. Führen Sie den folgenden [!DNL Python]-Code in einer neuen Zelle aus, um ein Balkendiagramm zu generieren:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Stündliche Aktivitätenzahl {#hourly-activity-count}

Die folgende Abfrage gibt die Anzahl der stündlichen Aktionen für ein bestimmtes Datum zurück:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Die Ausführung der oben genannten Abfrage speichert die Ergebnisse in `hourly_actions` als Dataframe. Führen Sie die folgende Funktion in einer neuen Zelle aus, um eine Vorschau der Ergebnisse anzuzeigen:

```python
hourly_actions.head()
```

Die obige Abfrage kann geändert werden, um die Anzahl der stündlichen Aktionen für einen bestimmten Datumsbereich zurückzugeben, indem logische Operatoren in der **WHERE**-Klausel verwendet werden:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Beim Ausführen der geänderten Abfrage werden die Ergebnisse in `hourly_actions_date_range` als Datenformat gespeichert. Führen Sie die folgende Funktion in einer neuen Zelle aus, um eine Vorschau der Ergebnisse anzuzeigen:

```python
hourly_actions_date_rage.head()
```

### Anzahl der Ereignisse pro Besuchersitzung  {#number-of-events-per-visitor-session}

Die folgende Abfrage gibt die Anzahl der Ereignisse pro Besuchersitzung für ein bestimmtes Datum zurück:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Führen Sie den folgenden [!DNL Python]-Code aus, um ein Histogramm für die Anzahl der Ereignis pro Besuchssitzung zu generieren:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Beliebte Seiten an einem bestimmten Tag {#popular-pages-for-a-given-day}

Die folgende Abfrage gibt die zehn beliebtesten Seiten an einem festgelegten Datum zurück:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Aktive Benutzer an einem bestimmten Tag  {#active-users-for-a-given-day}

In der folgenden Abfrage werden die zehn aktivsten Benutzer an einem bestimmten Datum zurückgegeben:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Aktive Städte nach Aktivität des Benutzers  {#active-cities-by-user-activity}

In der folgenden Abfrage werden die zehn Städte zurückgegeben, in denen die meisten Aktivitäten an einem bestimmten Datum generiert wurden:

#### Abfrage <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Nächste Schritte

In diesem Lernprogramm wurden einige Beispielverwendungsfälle für die Verwendung von [!DNL Query Service] in [!DNL Jupyter]-Notebooks erläutert. Folgen Sie dem Tutorial [Analysieren Ihrer Daten mit Jupyter Notebooks](./analyze-your-data.md), um zu sehen, wie ähnliche Vorgänge mit dem Data Access SDK ausgeführt werden.
