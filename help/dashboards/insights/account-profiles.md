---
title: Kontoprofileinblicke
description: Entdecken Sie die SQL, mit der Sie Ihre Kontoprofil-Einblicke gewinnen und diese Abfragen nutzen können, um benutzerdefinierte Einblicke zu generieren, mit denen Sie Ihre Kunden und deren Kundenerlebnisse weiter untersuchen können.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Einblicke in Kontoprofile

[Kontoprofile](../../rtcdp/accounts/account-profile-overview.md) werden verwendet, um Kontoinformationen aus verschiedenen Quellen zu konsolidieren, einschließlich verschiedener Marketing-Kanäle und Unternehmenssysteme. Diese einheitliche Ansicht ermöglicht ein umfassendes Verständnis der Kundenkonten und verbessert so die B2B-Marketingkampagnen. Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-time Customer Data Platform B2B-Daten leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.

Mit dem Zugriff auf die SQL-Datenbank, die Ihre Einblicke ermöglicht, können Sie Ihre B2B-Daten besser verstehen und Ihre eigenen, hochgradig benutzerdefinierten wiederverwendbaren Einblicke generieren, um Ihre Kundenkontoinformationen weiter zu untersuchen. Transformieren Sie Ihre Rohdaten in neue umsetzbare Einblicke, indem Sie die vorhandene SQL des Real-Time CDP-Datenmodells als Anregung verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Die folgenden Einblicke stehen Ihnen als Teil der [Dashboard &quot;Kontoprofile&quot;](../guides/account-profiles.md) oder [benutzerdefiniertes Dashboard](../user-defined-dashboards.md). Siehe [Anpassungsübersicht](../customize/overview.md) Anweisungen zum Anpassen Ihres Dashboards erhalten Sie oder [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und [Benutzerdefiniertes Dashboard](../user-defined-dashboards.md#create-widget).

## Kontoprofile hinzugefügt {#account-profiles-added}

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

## Hinzugefügte Möglichkeiten {#opportunities-added}

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

## Nächste Schritte

Durch Lesen dieses Dokuments verstehen Sie jetzt die SQL, die Einblicke in das Kontoprofil-Dashboard generiert, und welche häufig gestellten Fragen diese Analyse löst. Jetzt können Sie die SQL bearbeiten und iterieren, um Ihre eigenen Einblicke zu generieren.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

Sie können auch die SQL lesen und verstehen, die Einblicke für die [Profile](./profiles.md), [Zielgruppen](./audiences.md), und [Ziele](./destinations.md) Dashboards.
