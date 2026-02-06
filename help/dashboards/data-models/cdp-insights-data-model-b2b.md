---
title: Real-Time Customer Data Platform Insights-Datenmodell B2B edition
description: Erfahren Sie, wie Sie SQL-Abfragen mit den Real-Time Customer Data Platform Insights-Datenmodellen (B2B edition) verwenden, um Ihre eigenen Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle anzupassen.
badgeB2B: null
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: a32064848809d1cad07f769f04d82c35df451e38
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 4%

---

# Real-Time CDP Insights-Datenmodell B2B edition

Das Real-Time CDP Insights-Datenmodell für B2B edition stellt die Datenmodelle und SQL zur Verfügung, die die Insights für [Account-Profile](https://experienceleague.adobe.com/de/docs/experience-platform/rtcdp/account/account-profile-overview) unterstützen. Sie können diese SQL-Abfragevorlagen anpassen, um Real-Time CDP-Berichte für Ihre Anwendungsfälle des B2B-Marketings und des Key Performance Indicators (KPI) zu erstellen. Diese Einblicke können dann als benutzerdefinierte Widgets für Ihre Dashboards verwendet werden.

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Weitere Informationen finden Sie in der Dokumentation zu verfügbaren [Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions)Editionen oder wenden Sie sich an den Adobe-Support.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der benutzerdefinierten Dashboards voraus. Lesen Sie die Dokumentation unter [Erstellen eines benutzerdefinierten Dashboards](../standard-dashboards.md) bevor Sie mit diesem Handbuch fortfahren.

## Real-Time CDP B2B insight-Berichte und -Anwendungsfälle {#B2B-insight-reports-and-use-cases}

Die B2B-Berichterstellung von Real-Time CDP bietet Einblicke in die Daten Ihrer Account-Profile und die Beziehung zwischen Accounts und Opportunities. Die folgenden Star-Schemamodelle wurden entwickelt, um eine Vielzahl gängiger Marketing-Anwendungsfälle zu beantworten, und jedes Datenmodell kann mehrere Anwendungsfälle unterstützen.

>[!IMPORTANT]
>
>Die für das Real-Time CDP B2B-Reporting verwendeten Daten sind für eine ausgewählte Zusammenführungsrichtlinie und vom letzten täglichen Schnappschuss korrekt.

### Account-Profilmodell {#account-profile-model}

Das Kontoprofilmodell besteht aus acht Datensätzen:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

Das folgende Diagramm zeigt die relevanten Datenfelder in jedem Datensatz, ihren Datentyp und die Fremdschlüssel, die die Datensätze miteinander verknüpfen.

![Das Entitäts-Relations-Diagramm für das Kontoprofilmodell.](../images/data-models/account-profile-model.png)

#### Die neuen Konten nach Branchen-Anwendungsfall {#accounts-by-industry}

Die für die [!UICONTROL New accounts by industry] insight verwendete Logik gibt die fünf wichtigsten Branchen entsprechend ihrer Anzahl an Account-Profilen und ihrer relativen Größe zueinander zurück. Weitere Informationen finden Sie in der Dokumentation [[!UICONTROL New accounts By Industry] Widgets &#x200B;](../guides/account-profiles.md#accounts-by-industry) .

>[!TIP]
>
>Sie können diese SQL-Abfrage so anpassen, dass mehr oder weniger als die fünf wichtigsten Branchen zurückgegeben werden.

Der SQL-Code, der die [!UICONTROL New accounts by industry] insight generiert, wird im ausblendbaren Abschnitt unten angezeigt.

+++SQL-Abfrage

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### Die neuen Konten nach Typ - Anwendungsfall {#accounts-by-type}

Die für die [!UICONTROL New accounts by type] insight verwendete Logik gibt die numerische Aufschlüsselung der Konten nach ihrem Typ zurück. Diese insight kann bei der Ausrichtung von Geschäftsstrategien und -vorgängen helfen, einschließlich Ressourcenzuordnungs- oder Marketing-Strategien. Weitere Informationen finden Sie in der Dokumentation [[!UICONTROL New accounts by type] Widgets &#x200B;](../guides/account-profiles.md#accounts-by-type) .

Der SQL-Code, der die [!UICONTROL New accounts by type] insight generiert, wird im ausblendbaren Abschnitt unten angezeigt.

+++SQL-Abfrage

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

### Opportunity-Modell {#opportunity-model}

Das Opportunity-Modell besteht aus sieben Datensätzen:

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

Das folgende Diagramm zeigt die relevanten Datenfelder in jedem Datensatz.

![Das Entitäts-Relations-Diagramm für das Opportunity-Modell.](../images/data-models/opportunity-model.png)
