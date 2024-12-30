---
title: Explorative Datenanalyse
description: Erfahren Sie, wie Sie mit Data Distiller Daten aus einem Python-Notebook untersuchen und analysieren können.
exl-id: 1dd4cf6e-f7cc-4f4b-afbd-bfc1d342a2c3
source-git-commit: 27834417a1683136a173996cff1fd422305e65b9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 14%

---

# Explorative Datenanalyse

Dieses Dokument enthält einige grundlegende Beispiele und Best Practices für die Verwendung von Data Distiller zum Untersuchen und Analysieren von Daten aus einem [!DNL Python]-Notebook.

## Erste Schritte

Bevor Sie mit diesem Handbuch fortfahren, stellen Sie sicher, dass Sie eine Verbindung zu Data Distiller in Ihrem [!DNL Python]-Notebook erstellt haben. In der Dokumentation finden Sie Anweisungen zum Verbinden [ Notebooks mit  [!DNL Python]  Distiller](./establish-connection.md).

## Erfassen grundlegender Statistiken {#basic-statistics}

Verwenden Sie den folgenden Code, um die Anzahl der Zeilen und eindeutigen Profile in einem Datensatz abzurufen.

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

## Erstellen einer beispielhaften Version großer Datensätze {#create-dataset-sample}

Wenn der abzufragende Datensatz sehr groß ist oder keine exakten Ergebnisse aus explorativen Abfragen erforderlich sind, verwenden Sie die [Sampling-Funktion](../../key-concepts/dataset-samples.md) die für Data Distiller-Abfragen verfügbar ist. Dies ist ein zweistufiger Prozess:

- Analysieren **zunächst** Datensatz, um eine Stichprobenversion mit einem bestimmten Stichprobenverhältnis zu erstellen
- Fragen Sie anschließend die Beispielversion des Datensatzes ab. Je nach den Funktionen, die Sie auf den abgetasteten Datensatz anwenden, möchten Sie die Ausgabe möglicherweise auf die Zahlen im vollständigen Datensatz skalieren

### Erstellen einer 5 %-Stichprobe {#create-sample}

Im folgenden Beispiel wird der Datensatz analysiert und eine 5%ige Stichprobe erstellt:

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### Beispiele anzeigen {#view-sample}

Sie können die `sample_meta`-Funktion verwenden, um alle Beispiele anzuzeigen, die aus einem bestimmten Datensatz erstellt wurden. Der folgende Codeausschnitt zeigt, wie Sie die `sample_meta`-Funktion verwenden.

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**Beispielausgabe**:

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | Sampling_Rate | filter_condition_on_source_dataset | sample_num_rows | Erstellt |
|---|---|---|---|---|---|---|---|---|
| 0 | CMLE_SYNTHETIC_DATA_EXPERIENCE_EVENT_DATASET_C… | 650f7a09ed6c3e28d34d7fc2 | 64FB4D7A7D748828D304A2F4 | gleichförmig | 0,5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### Abfrage Ihres Beispiels {#query-sample-data}

Sie können Ihr Beispiel direkt abfragen, indem Sie auf den Beispieltabellennamen aus den zurückgegebenen Metadaten verweisen. Sie können dann die Ergebnisse mit dem Sampling-Verhältnis multiplizieren, um eine Schätzung zu erhalten.

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**Beispielausgabe**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## E-Mail-Trichteranalyse {#email-funnel-analysis}

Eine Trichteranalyse dient zum Verständnis der Schritte, die zum Erreichen eines Zielergebnisses erforderlich sind, und der Anzahl der Benutzer, die die einzelnen Schritte durchlaufen. Das folgende Beispiel zeigt eine einfache Trichteranalyse der Schritte, die dazu führen, dass ein Benutzer einen Newsletter abonniert. Das Abonnementergebnis wird durch einen Ereignistyp von `web.formFilledOut` dargestellt.

Führen Sie zunächst eine Abfrage aus, um die Anzahl der Benutzer in jedem Schritt abzurufen.

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

### Plotten der Abfrageergebnisse {#plot-results}

Zeichnen Sie anschließend die Abfrageergebnisse mithilfe der [!DNL Python] `plotly`:

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**Beispielausgabe**

![Eine Infografik des eventType-E-Mail-Trichters.](../../images/data-distiller/email-funnel.png)

## Ereignis-Korrelationen {#event-correlations}

Eine weitere gängige Analyse besteht darin, Korrelationen zwischen Ereignistypen und einem Zielkonversionsereignistyp zu berechnen. In diesem Beispiel wird das Abonnementereignis durch `web.formFilledOut` dargestellt. In diesem Beispiel werden die in Distiller-Datenabfragen verfügbaren [!DNL Spark] verwendet, um die folgenden Schritte auszuführen:

1. Zählen Sie die Anzahl der Ereignisse für jeden Ereignistyp nach Profil.
2. Aggregieren Sie die Anzahl jedes Ereignistyps über Profile hinweg und berechnen Sie die Korrelationen jedes Ereignistyps mit `web,formFilledOut`.
3. Transformiert den Datenrahmen der Zählungen und Korrelationen in eine Tabelle der Pearson-Korrelationskoeffizienten jeder Funktion (Anzahl der Ereignistypen) mit dem Zielereignis.
4. Visualisieren Sie die Ergebnisse in einer Zeichnung.

Die [!DNL Spark] aggregieren die Daten und geben eine kleine Ergebnistabelle zurück, sodass Sie diese Art der Abfrage für den gesamten Datensatz ausführen können.

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

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totalUsers | propositionDisplays_totalUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | … | webForms_advertisingClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDismisses | webForms_propositionInteractions | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0,026805 | 0,2779 | Keine | 0,06014 | 0,143656 | 0,305657 | 0,218874 | 0,192836 | 0,259353 | Keine |

{style="table-layout:auto"}

### Zeile in Ereignistyp-Korrelation umwandeln {#event-type-correlation}

Wandeln Sie anschließend die einzelne Datenzeile in der obigen Abfrageausgabe in eine Tabelle um, die die Korrelationen der einzelnen Ereignistypen mit dem Zielabonnement-Ereignis anzeigt:

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**Beispielausgabe**:

|    | Variable | Wert | Funktion | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0,218874 | E-Mail-Öffnungen | 0,218874 |
| 1 | `webForms_advertisingClicks` | 0,026805 | AdvertisingClicks | 0,026805 |
| 2 | `webForms_productViews` | 0,277900 | productViews | 0,277900 |
| 3 | `webForms_productPurchases` | 0,000000 | productPurchases | 0,000000 |
| 4 | `webForms_propositionDismisses` | 0,060140 | propositionDismisses | 0,060140 |
| 5 | `webForms_propositionInteracts` | 0,143656 | propositionInteractions | 0,143656 |
| 6 | `webForms_emailClicks` | 0,305657 | emailClicks | 0,305657 |
| 7 | `webForms_emailOpens` | 0,218874 | E-Mail-Öffnungen | 0,218874 |
| 8 | `webForms_emailSends` | 0,192836 | emailSends | 0,192836 |
| 9 | `webForms_webLinkClicks` | 0,259353 | webLinkClicks | 0,259353 |
| 10 | `webForms_webPageViews` | 0,000000 | webPageViews | 0,000000 |


Schließlich können Sie die Korrelationen mit der `matplotlib` [!DNL Python]-Bibliothek visualisieren:

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![Ein Balkendiagramm der Pearson-Korrelation von Ereignissen von Ereignisergebnissen](../../images/data-distiller/pearson-correlations.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mit Data Distiller Daten aus einem [!DNL Python]-Notebook untersuchen und analysieren können. Der nächste Schritt beim Erstellen von Funktions-Pipelines vom Experience Platform zur Bereitstellung benutzerdefinierter Modelle in Ihrer maschinellen Lernumgebung besteht darin, [Funktionen für maschinelles Lernen zu entwickeln](./feature-engineering.md).
