---
title: Real-time Customer Data Platform Insights-Datenmodell B2B edition
description: Erfahren Sie, wie Sie mit den Real-time Customer Data Platform Insights-Datenmodellen (B2B edition) SQL-Abfragen verwenden können, um Ihre eigenen Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle anzupassen.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 3%

---

# Real-time Customer Data Platform Insights-Datenmodell B2B edition

Das Real-time Customer Data Platform Insights-Datenmodell für die B2B Edition stellt die Datenmodelle und SQL bereit, die die Einblicke für [Kontoprofile](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview) nutzen. Sie können diese SQL-Abfragevorlagen anpassen, um Real-Time CDP-Berichte für Ihre Anwendungsfälle von B2B-Marketing und Key Performance Indicators (KPI) zu erstellen. Diese Einblicke können dann als benutzerdefinierte Widgets für Ihre Dashboards verwendet werden.

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Weitere Informationen finden Sie in der Dokumentation zu verfügbaren [Real-Time CDP-Editionen](../../rtcdp/overview.md#rtcdp-editions) oder wenden Sie sich an Ihren Adobe-Support-Mitarbeiter.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis benutzerdefinierter Dashboards voraus. Lesen Sie die Dokumentation zu [Erstellen eines benutzerdefinierten Dashboards](../standard-dashboards.md) , bevor Sie mit diesem Handbuch fortfahren.

## Real-Time CDP B2B Insight-Berichte und Anwendungsfälle {#B2B-insight-reports-and-use-cases}

Real-Time CDP B2B Reporting bietet Einblicke in Ihre Kontoprofildaten und die Beziehung zwischen Konten und Chancen. Die folgenden Sternschema-Modelle wurden entwickelt, um eine Vielzahl gängiger Marketing-Anwendungsfälle zu beantworten. Jedes Datenmodell kann mehrere Anwendungsfälle unterstützen.

>[!IMPORTANT]
>
>Die für die B2B-Berichterstellung in Real-Time CDP verwendeten Daten sind für eine bestimmte Zusammenführungsrichtlinie und die aktuellsten täglichen Momentaufnahmen genau.

### Kontoprofilmodell {#account-profile-model}

Das Kontoprofilmodell besteht aus acht Datensätzen:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

Das folgende Diagramm zeigt die relevanten Datenfelder in jedem Datensatz, ihren Datentyp und die Fremdschlüssel, die die Datensätze verknüpfen.

![Das relationale Entitätsdiagramm für das Kontoprofilmodell.](../images/data-models/account-profile-model.png)

#### Die neuen Konten nach Anwendungsfall der Industrie {#accounts-by-industry}

Die Logik, die für den Einblick in [!UICONTROL Neue Konten nach Branche] verwendet wird, gibt die fünf wichtigsten Branchen in Abhängigkeit von ihrer Anzahl der Kontoprofile und ihrer relativen Größe zueinander zurück. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Neue Konten nach Branche]](../guides/account-profiles.md#accounts-by-industry) .

>[!TIP]
>
>Sie können diese SQL-Abfrage so anpassen, dass mehr oder weniger als die fünf wichtigsten Branchen zurückgegeben werden.

Die SQL, die den Einblick in die [!UICONTROL neuen Konten nach Branche] generiert, ist im unten stehenden ausblendbaren Abschnitt dargestellt.

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

#### Anwendungsfall Neue Konten nach Typ {#accounts-by-type}

Die Logik, die für den Einblick in [!UICONTROL Neue Konten nach Typ] verwendet wird, gibt die numerische Aufschlüsselung der Konten nach Typ zurück. Diese Einblicke können dabei helfen, die Geschäftsstrategie und den Betrieb zu steuern, einschließlich Ressourcenzuteilung oder Marketing-Strategien. Weitere Informationen finden Sie in der Dokumentation zu [[!UICONTROL neuen Konten nach Typ] Widget](../guides/account-profiles.md#accounts-by-type) .

Die SQL, die die [!UICONTROL neuen Konten nach Typ] Insight generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

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

![Das relationale Entitätsdiagramm für das Opportunity-Modell.](../images/data-models/opportunity-model.png)
