---
title: Explorative Datenanalyse
description: Erfahren Sie, wie Sie mit Data Distiller Daten aus einem Python-Notebook untersuchen und analysieren können.
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 18%

---

# Explorative Datenanalyse

Dieses Dokument enthält einige grundlegende Beispiele und Best Practices für die Verwendung von Data Distiller zur Erforschung und Analyse von Daten aus einem Python-Notebook.

## Erste Schritte

Bevor Sie mit diesem Handbuch fortfahren, stellen Sie sicher, dass Sie eine Verbindung zu Data Distiller in Ihrem Python-Notebook hergestellt haben. Anweisungen dazu finden Sie in der Dokumentation [ein Python-Notebook mit Data Distiller verbinden](./establish-connection.md).

## Abrufen von Basisstatistiken {#basic-statistics}

Verwenden Sie den unten stehenden Code, um die Anzahl der Zeilen und eindeutigen Profile in einem Datensatz abzurufen.

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**Beispielausgabe**

|     | totalRows | distinctUsers |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## Erstellen einer Stichprobenversion großer Datensätze {#create-dataset-sample}

Wenn der Datensatz, den Sie abfragen möchten, sehr groß ist oder wenn genaue Ergebnisse aus explorativen Abfragen nicht erforderlich sind, verwenden Sie die [Sampling-Funktion](../../essential-concepts/dataset-samples.md) verfügbar für Data Distiller-Abfragen. Dies ist ein zweistufiger Prozess:

- Erstens: **analysieren** Datensatz, um eine Version mit einer Stichprobe mit einem bestimmten Stichprobenverhältnis zu erstellen
- Abfragen Sie als Nächstes die beprobte Version des Datensatzes. Je nach den Funktionen, die Sie auf den Datensatz mit gesampelten Datensätzen anwenden, können Sie die Ausgabe auf die Zahlen auf den vollständigen Datensatz skalieren

### Beispiel für 5 % erstellen {#create-sample}

Im folgenden Beispiel wird der Datensatz analysiert und ein 5 %-Beispiel erstellt:

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### Beispiele anzeigen {#view-sample}

Sie können die `sample_meta` -Funktion, um alle Beispiele anzuzeigen, die aus einem bestimmten Datensatz erstellt wurden. Das folgende Codefragment zeigt die Verwendung der `sample_meta` -Funktion.

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**Beispielausgabe**:

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | sampling_rate | filter_condition_on_source_dataset | sample_num_rows | Erstellt |
|---|---|---|---|---|---|---|---|---|
| 0 | cmle_synthetisch_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | einheitlich | 0.5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### Beispiel abfragen {#query-sample-data}

Sie können Ihr Beispiel direkt abfragen, indem Sie auf den Namen der Beispieltabelle aus den zurückgegebenen Metadaten verweisen. Anschließend können Sie die Ergebnisse mit dem Stichprobenverhältnis multiplizieren, um eine Schätzung zu erhalten.

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**Beispielausgabe**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## E-Mail-Trichteranalyse {#email-funnel-analysis}

Eine Trichteranalyse ist eine Methode, um die Schritte zu verstehen, die zum Erreichen eines Zielergebnisses erforderlich sind, und wie viele Benutzer jeden dieser Schritte durchlaufen. Das folgende Beispiel zeigt eine einfache Trichteranalyse der Schritte, die zu einem Benutzer führen, der einen Newsletter abonniert. Das Abonnementergebnis wird durch einen Ereignistyp `web.formFilledOut`.

Führen Sie zunächst eine Abfrage aus, um die Anzahl der Benutzer bei jedem Schritt abzurufen.

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**Beispielausgabe**

|   | eventType | distinctUsers | distinctEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### Plotabfrageergebnisse {#plot-results}

Als Nächstes zeichnen Sie die Abfrageergebnisse mit dem Python `plotly` -Bibliothek:

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**Beispielausgabe**

![Eine Infografik des eventType-E-Mail-Trichters.](../../images/data-distiller/email-funnel.png)

## Ereigniskorrelationen {#event-correlations}

Eine weitere gängige Analyse besteht darin, Korrelationen zwischen Ereignistypen und einem Zielkonversionsereignistyp zu berechnen. In diesem Beispiel wird das Abonnementereignis durch `web.formFilledOut`. In diesem Beispiel wird die [!DNL Spark] Funktionen, die in Data Distiller-Abfragen verfügbar sind, um die folgenden Schritte auszuführen:

1. Zählen Sie die Anzahl der Ereignisse für jeden Ereignistyp nach Profil.
2. Aggregieren Sie die Zählungen der einzelnen Ereignistypen über Profile hinweg und berechnen Sie die Korrelationen der einzelnen Ereignistypen mit `web,formFilledOut`.
3. Wandeln Sie den Dataframe der Zählungen und Korrelationen in eine Tabelle der Pearson-Korrelationskoeffizienten jeder Funktion (Ereignistypzählungen) mit dem Zielereignis um.
4. Visualisieren Sie die Ergebnisse in einem Diagramm.

Die [!DNL Spark] -Funktionen aggregieren die Daten, um eine kleine Tabelle mit Ergebnissen zurückzugeben, sodass Sie diese Art von Abfrage für den vollständigen Datensatz ausführen können.

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**Beispielausgabe**:

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totaUsers | propositionDisplays_totaUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertisingClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDismisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0.026805 | 0.2779 | Keine | 0.06014 | 0.143656 | 0.305657 | 0.218874 | 0.192836 | 0.259353 | Keine |

{style="table-layout:auto"}

### Umwandeln von Zeilen in Korrelationen von Ereignistypen {#event-type-correlation}

Wandeln Sie anschließend die einzelne Datenzeile in der oben stehenden Abfrageausgabe in eine Tabelle um, die die Korrelationen der einzelnen Ereignistypen mit dem Zielabonnement-Ereignis anzeigt:

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**Beispielausgabe**:

|    | festgelegt | value | Funktion | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0.218874 | EmailOpens | 0.218874 |
| 1 | `webForms_advertisingClicks` | 0.026805 | advertisingClicks | 0.026805 |
| 2 | `webForms_productViews` | 0.277900 | productViews | 0.277900 |
| 3 | `webForms_productPurchases` | 0.000000 | productPurchases | 0.000000 |
| 4 | `webForms_propositionDismisses` | 0.060140 | propositionDismisses | 0.060140 |
| 5 | `webForms_propositionInteracts` | 0.143656 | propositionInteracts | 0.143656 |
| 6 | `webForms_emailClicks` | 0.305657 | emailClicks | 0.305657 |
| 7 | `webForms_emailOpens` | 0.218874 | emailOpens | 0.218874 |
| 8 | `webForms_emailSends` | 0.192836 | emailSends | 0.192836 |
| 9 | `webForms_webLinkClicks` | 0.259353 | webLinkClicks | 0.259353 |
| 10 | `webForms_webPageViews` | 0.000000 | webPageViews | 0.000000 |


Schließlich können Sie die Korrelationen mit der `matplotlib` Python-Bibliothek:

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![Ein Balkendiagramm der Pearson-Korrelation von Ereignissen aus Ereignisergebnissen](../../images/data-distiller/pearson-correlations.png)

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie erfahren, wie Sie mit Data Distiller Daten aus einem Python-Notebook untersuchen und analysieren können. Der nächste Schritt beim Erstellen von Feature Pipelines aus dem Experience Platform, um benutzerdefinierte Modelle in Ihrer maschinellen Lernumgebung zu speisen, besteht darin, [technische Funktionen für maschinelles Lernen](./feature-engineering.md).
