---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenbestände vs. Tabellen und Schema
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# Datenbestände vs. Tabellen und Schema

Überprüfen Sie die Liste der in der Benutzeroberfläche [der](https://platform.adobe.com/datasets)Adobe Experience Platform verfügbaren Datensätze, und achten Sie darauf, dass Sie die Datensatznamen beachten.
>[!NOTE]
>
>Einige Dataset-Namen haben Leerzeichen und sind sonst nicht SQL-sicher.

![](../images/queries/datasets-and-tables/dataset-names.png)


Überprüfen Sie die hierarchische Struktur des Dataset-Schemas in der Benutzeroberfläche, indem Sie auf einen Schema in der Datensatztabelle klicken.

![](../images/queries/datasets-and-tables/schema-information.png)

Öffnen Sie die PSQL-Befehlszeile und verwenden Sie die Verbindungsdetails von hier: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Zur Ansicht der verfügbaren Tabellen auf der Platform mit SQL können Sie entweder `\d` oder `SHOW TABLES;`verwenden.


`\d` zeigt die standardmäßige PostgreSQL-Ansicht an

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` ist ein benutzerdefinierter Befehl, der eine detailliertere Ansicht bietet und die Tabelle sowie den Dataset-Namen in der Benutzeroberfläche der Platform darstellt.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Um das Stamm-Schema einer Tabelle Ansicht, verwenden Sie den `\d table_name` Befehl.

>[!NOTE]
>
>Das präsentierte Schema zeigt die Stammfelder, die zumeist komplex sind und auf einen Objekttyp in der Benutzeroberfläche des DataSet-Schemas verweisen.

`\d luma_midvalues`

```
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Um weiter in das Schema zu gehen, verwenden Sie Unterstriche (`_`), um die Tabellenspalte zu deklarieren, die Sie beschreiben möchten. Beispiel, `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
