---
title: Kontoprofileinblicke
description: Entdecken Sie die SQL, mit der Sie Ihre Kontoprofil-Einblicke gewinnen und diese Abfragen nutzen können, um benutzerdefinierte Einblicke zu generieren, mit denen Sie Ihre Kunden und deren Kundenerlebnisse weiter untersuchen können.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: f9ef0e25dac1715bbb6d73db52d6368c543bf7ec
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Einblicke in Kontoprofile

[Kontoprofile](../../rtcdp/accounts/account-profile-overview.md) werden verwendet, um Kontoinformationen aus verschiedenen Quellen zu konsolidieren, einschließlich mehrerer Marketing-Kanäle und Unternehmenssysteme. Diese einheitliche Ansicht ermöglicht ein umfassendes Verständnis der Kundenkonten und verbessert so die B2B-Marketingkampagnen. Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-time Customer Data Platform B2B-Daten leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.

Mit dem Zugriff auf die SQL-Datenbank, die Ihre Einblicke ermöglicht, können Sie Ihre B2B-Daten besser verstehen und Ihre eigenen, hochgradig benutzerdefinierten wiederverwendbaren Einblicke generieren, um Ihre Kundenkontoinformationen weiter zu untersuchen. Transformieren Sie Ihre Rohdaten in neue umsetzbare Einblicke, indem Sie die vorhandene SQL des Real-Time CDP-Datenmodells als Anregung verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Die folgenden Einblicke stehen Ihnen im Dashboard [Kontoprofile](../guides/account-profiles.md) oder im benutzerdefinierten Dashboard [Dashboard](../standard-dashboards.md) zur Verfügung. Anweisungen zum Anpassen Ihres Dashboards oder zum Erstellen und Bearbeiten neuer Widgets ](../customize/custom-widgets.md) in der Widget-Bibliothek und [benutzerdefinierten Dashboards](../standard-dashboards.md#create-widget) finden Sie in der [Übersicht zur Anpassung](../customize/overview.md) .[

## Hinzugefügte Kontoprofile {#account-profiles-added}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Kontoprofile wurden in einem bestimmten Zeitraum hinzugefügt?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Neue Abschlüsse nach Wirtschaftszweigen {#accounts-by-industry}

Fragen, die durch diesen Einblick beantwortet werden:

- Zu welchen fünf Branchen gehören die Kontoprofile?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hoch ist die Anzahl der Konten nach ihrer Art?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Möglichkeiten wurden in einem bestimmten Zeitraum hinzugefügt?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Neue Möglichkeiten für die Rolle der Person {#opportunities-by-person-role}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie groß sind die verschiedenen Rollen in einer Chance und wie hoch sind sie?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Neue Einnahmenmöglichkeiten {#opportunities-by-revenue}

Fragen, die durch diesen Einblick beantwortet werden:

- Welches sind die 20 besten Chancen nach ihrem Umsatz (in USD)?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Neue Möglichkeiten nach Status und Phase {#opportunities-by-status-and-stage}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Öffnungsmöglichkeiten gibt es und in welchem Stadium des Verkaufs- oder Marketingtrichters?
- Welche geschlossenen Möglichkeiten gibt es und in welchem Stadium des Verkaufs- oder Marketingtrichters?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Neue Chancen gewonnen {#opportunities-won}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Möglichkeiten gibt es, die erfolgreich abgeschlossen oder abgeschlossen wurden?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Gewonnene Chancen (Kantengraph) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Möglichkeiten wurden in einem bestimmten Zeitraum erfolgreich geschlossen oder abgeschlossen (gewonnen)?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Kunden nach Kontoübersicht {#customers-per-account-overview}

>[!NOTE]
>
>Das Diagramm [!UICONTROL Kunden pro Konto - Übersicht] enthält drei Durchlaufeinblicke: [!UICONTROL Kunden pro Kontodetails], [!UICONTROL Chancen pro Konto - Übersicht] und [!UICONTROL Möglichkeiten pro Kontodetails]. Diese Durchsichten bieten detailliertere Einblicke, indem Kunden- und Opportunity-Zählungen nach Kategorien (wie direkten und indirekten Kunden) und Bereichen (wie Kunden- und Opportunitäts-Bands) aufgeschlüsselt werden. Diese Diagramme sind von den von Ihnen festgelegten globalen Datumsfiltern nicht betroffen.

Fragen, die durch diesen Einblick beantwortet werden:

- Wie ist die Verteilung der Konten darauf ausgerichtet, ob sie direkte oder indirekte Kunden haben?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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
>Diese Einblicke sind von globalen Datumsfiltern nicht betroffen.

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Konten weisen unterschiedliche Bereiche von direkten oder indirekten Kunden auf?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Übersicht über die Möglichkeiten pro Konto {#opportunities-per-account-overview}

>[!NOTE]
>
>Diese Einblicke sind von globalen Datumsfiltern nicht betroffen.

Fragen, die durch diesen Einblick beantwortet werden:

- Wie wird die Verteilung der Konten darauf verteilt, ob ihnen damit verbundene Möglichkeiten zur Verfügung stehen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

## Möglichkeiten pro Kontodetails {#opportunities-per-account-detail}

>[!NOTE]
>
>Diese Einblicke sind von globalen Datumsfiltern nicht betroffen.

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Konten verfügen über unterschiedliche Bereiche der zugehörigen Möglichkeiten?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Durch Lesen dieses Dokuments verstehen Sie jetzt die SQL, die Einblicke in das Kontoprofil-Dashboard generiert, und welche häufig gestellten Fragen diese Analyse löst. Jetzt können Sie die SQL bearbeiten und iterieren, um Ihre eigenen Einblicke zu generieren. Informationen zum Generieren benutzerdefinierter Einblicke mit SQL finden Sie in der [Übersicht über Query Pro Mode](../sql-insights-query-pro-mode/overview.md) .

Sie können auch die SQL lesen und verstehen, die Einblicke in die Dashboards [Profile](./profiles.md), [Zielgruppen](./audiences.md) und [Ziele](./destinations.md) generiert.
