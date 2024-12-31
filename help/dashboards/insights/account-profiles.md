---
title: Account Profile Insights
description: Entdecken Sie die SQL-Daten, die Ihren Account-Profil-Einblicken zugrunde liegen, und verwenden Sie diese Abfragen, um benutzerdefinierte Einblicke zu generieren, die Ihre Kunden und deren Kundenerlebnisse weiter untersuchen.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P-Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Account Profile Insights

[Account-Profile](../../rtcdp/accounts/account-profile-overview.md) werden verwendet, um Account-Informationen aus verschiedenen Quellen zu konsolidieren, einschließlich mehrerer Marketing-Kanäle und Organisationssysteme. Diese einheitliche Ansicht ermöglicht ein umfassendes Verständnis von Kundenkonten und verbessert B2B-Marketing-Kampagnen. Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-Time CDP B2B-Daten zugänglicher, verständlicher und wirkungsvoller für die Entscheidungsfindung.

Mit dem Zugriff auf die SQL, die Ihre Einblicke ermöglicht, können Sie Ihre B2B-Daten besser verstehen und Ihre eigenen hochgradig benutzerdefinierten wiederverwendbaren Einblicke generieren, um Ihre Kundenkontoinformationen weiter zu untersuchen. Wandeln Sie Ihre Rohdaten in neue umsetzbare Einblicke um, indem Sie das vorhandene Real-Time CDP-Datenmodell als SQL-Inspiration verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Die folgenden Einblicke stehen Ihnen als Teil des Dashboards [Kontoprofile“ oder ](../guides/account-profiles.md)benutzerdefinierten Dashboards[ zur ](../standard-dashboards.md). Anleitungen zum Anpassen Ihres Dashboards oder zum [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und im benutzerdefinierten Dashboard finden [ ](../customize/overview.md) in der [Anpassungsübersicht](../standard-dashboards.md#create-widget).

## Hinzugefügte Kontoprofile {#account-profiles-added}

Diese Einsicht beantwortet Fragen:

- Wie viele Account-Profile wurden in einem bestimmten Zeitraum hinzugefügt?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Neue Konten nach Branche {#accounts-by-industry}

Diese Einsicht beantwortet Fragen:

- Zu welchen fünf Branchen gehören die Account-Profile?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Neue Konten nach Typ {#accounts-by-type}

Diese Einsicht beantwortet Fragen:

- Wie viele Konten werden nach ihrem Typ gezählt?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

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

## Hinzugefügte Opportunities {#opportunities-added}

Diese Einsicht beantwortet Fragen:

- Wie viele Opportunitys wurden in einem bestimmten Zeitraum hinzugefügt?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Neue Opportunitys nach Personenrolle {#opportunities-by-person-role}

Diese Einsicht beantwortet Fragen:

- Wie groß und wie hoch sind die verschiedenen Rollen in einer Opportunity?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Neue Chancen nach Umsatz {#opportunities-by-revenue}

Diese Einsicht beantwortet Fragen:

- Welches sind die 20 Top-Vertriebschancen, die nach ihrem Umsatz (in USD) gereiht werden?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Neue Opportunities nach Status und Phase {#opportunities-by-status-and-stage}

Diese Einsicht beantwortet Fragen:

- Welche offenen Möglichkeiten gibt es und in welcher Phase des Verkaufs- oder Marketingtrichters sind sie?
- Welche geschlossenen Möglichkeiten gibt es und in welcher Phase des Verkaufs- oder Marketingtrichters befinden sie sich?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Neue gewonnene Gelegenheiten {#opportunities-won}

Diese Einsicht beantwortet Fragen:

- Wie viele Opportunitys wurden erfolgreich abgeschlossen oder abgeschlossen?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Opportunities gewonnen (Liniendiagramm) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Diese Einsicht beantwortet Fragen:

- Wie viele Opportunities wurden in einem bestimmten Zeitraum erfolgreich geschlossen oder abgeschlossen (gewonnen)?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Kunden pro Konto - Übersicht {#customers-per-account-overview}

>[!NOTE]
>
>Das Diagramm [!UICONTROL Kunden pro Konto - Übersicht] enthält drei Drill-Through-Einblicke: [!UICONTROL Kunden pro Kontodetails], [!UICONTROL Vertriebschancen pro Konto - Übersicht] und [!UICONTROL Vertriebschancen pro Kontodetail]. Diese Drill-Throughs bieten detailliertere Einblicke, indem sie die Kunden- und Opportunity-Anzahl nach Kategorien (z. B. direkte und indirekte Kunden) und Bereiche (z. B. Kunden- und Opportunity-Anzahl) aufschlüsseln. Diese Diagramme sind von globalen Datumsfiltern, die Sie möglicherweise festgelegt haben, nicht betroffen.

Diese Einsicht beantwortet Fragen:

- Wie verteilen sich Konten, je nachdem, ob sie direkte oder indirekte Kunden haben?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## Kunden pro Kontodetails {#customers-per-account-detail}

>[!NOTE]
>
>Diese Einsicht wird von globalen Datumsfiltern nicht beeinflusst.

Diese Einsicht beantwortet Fragen:

- Wie viele Accounts haben verschiedene Bereiche von direkten oder indirekten Kunden?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## Vertriebschancen pro Konto - Übersicht {#opportunities-per-account-overview}

>[!NOTE]
>
>Diese Einsicht wird von globalen Datumsfiltern nicht beeinflusst.

Diese Einsicht beantwortet Fragen:

- Wie ist die Kontenverteilung, je nachdem, ob es verknüpfte Opportunitys gibt?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## Vertriebschancen nach Kontodetails {#opportunities-per-account-detail}

>[!NOTE]
>
>Diese Einsicht wird von globalen Datumsfiltern nicht beeinflusst.

Diese Einsicht beantwortet Fragen:

- Wie viele Accounts sind mit unterschiedlichen Opportunities verbunden?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, welche SQL-Einblicke das Dashboard für Kontoprofile generiert und welche allgemeinen Fragen durch diese Analyse gelöst werden. Sie können jetzt SQL bearbeiten und iterieren, um eigene Einblicke zu generieren. Im Abschnitt [Query Pro-Modus - Übersicht](../sql-insights-query-pro-mode/overview.md) erfahren Sie, wie Sie mit SQL benutzerdefinierte Einblicke generieren können.

Sie können auch den SQL-Code lesen und verstehen, der Einblicke für die Dashboards [Profile](./profiles.md), [Audiences](./audiences.md) und [Ziele](./destinations.md) generiert.
