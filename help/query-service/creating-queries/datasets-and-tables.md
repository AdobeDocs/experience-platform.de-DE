---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datensätze vs. Tabellen und Schemas
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 79%

---


# Datensätze vs. Tabellen und Schemas

Überprüfen Sie die Liste der verfügbaren Datensätze in der [Benutzeroberfläche von Adobe Experience Platform](https://platform.adobe.com/datasets); achten Sie dabei auf die Namen der Datensätze.
>[!NOTE]
>
>Einige Datensatznamen weisen Leerzeichen auf und sind ggf. anderweitig nicht SQL-sicher.

![](../images/queries/datasets-and-tables/dataset-names.png)


Überprüfen Sie die hierarchische Struktur des Datensatzschemas in der Benutzeroberfläche, indem Sie in der Datensatztabelle auf einen Schemanamen klicken.

![](../images/queries/datasets-and-tables/schema-information.png)

Öffnen Sie die PSQL-Befehlszeile und verwenden Sie die Verbindungsdetails von hier: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

To view the available tables on [!DNL Platform] with SQL, you can use either `\d` or `SHOW TABLES;`.


`\d` zeigt die standardmäßige PostgreSQL-Ansicht an.

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` ist ein benutzerdefinierter Befehl, der eine detailliertere Ansicht bietet und die Tabelle sowie den Dataset-Namen in der [!DNL Platform] Benutzeroberfläche darstellt.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Um das Stammschema einer Tabelle anzuzeigen, verwenden Sie den Befehl `\d table_name`.

>[!NOTE]
>
>Das präsentierte Schema zeigt die Stammfelder an, die meist komplex sind und auf die ein Objekttyp in der Benutzeroberfläche für Datensatzschemas verweist.

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

Um das Schema genauer anzusehen, verwenden Sie Unterstriche (`_`). Dadurch können Sie die Spalte in der Tabelle, die Sie beschreiben möchten, deklarieren. Beispiel: `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
