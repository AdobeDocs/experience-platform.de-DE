---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Generieren von Datensätzen aus Abfrageergebnissen
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 56%

---


# Generieren von Datensätzen aus Abfrageergebnissen

The true power of [!DNL Query Service] is revealed when queries are used to generate datasets in the [!DNL Data Lake] to be used as input into more queries or in other services such as [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], or [!DNL Analysis Workspace].

[!DNL Query Service] ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Führen Sie folgende Schritte aus:

1. Schreiben Sie Ihre Anfrage mit einem verbundenen Client und validieren Sie die Ausgabe.
2. Log in to the [!DNL Platform] UI and go to Queries.
3. Suchen Sie Ihre Abfrage in der Liste und bewegen Sie den Mauszeiger über die Zeile.
4. Klicken Sie auf **[!UICONTROL Datensatz erstellen]**. ![Bild](../images/queries/create-datasets/click-create-dataset.png)
5. Geben Sie einen Namen für den Datensatz, dem Ihre LDAP-ID vorangestellt wird (muss nicht eindeutig oder SQL-sicher sein). Das System erzeugt anhand des hier angegebenen Namens einen „Tabellennamen“).
6. Geben Sie eine Beschreibung für den Datensatz ein und klicken Sie dann auf **[!UICONTROL Abfrage ausführen]**.![Bild](../images/queries/create-datasets/run-query.png)
7. Warten Sie, bis die Abfrage abgeschlossen ist, und rufen Sie dann die Seite mit der Datensatzliste auf, um den gerade erstellten Datensatz anzuzeigen.

After a dataset is created, it can be accessed like any other dataset in the [!DNL Data Lake] and used for a variety of use cases.

>[!NOTE]
>
>In a live implementation, you must apply [!DNL Data Governance] labels after the dataset is created.

## Erstellen von Datensätzen mit einem vordefinierten [!DNL Experience Data Model] Schema

In order to generate a dataset with a pre-defined [!DNL Experience Data Model] (XDM) schema, you will have to use the SQL syntax. Weitere Informationen zur Syntax finden Sie im [Handbuch zur SQL-Syntax](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Some downstream services require datasets with particular [!DNL Experience Data Model] (XDM) schemas. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.