---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Datensätze generieren; Datensatz generieren; Datensatz erstellen; Datensatz erstellen
solution: Experience Platform
title: Generieren von Datensätzen aus Ergebnissen in Query Service
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Data Lake aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 44%

---

# Generieren von Datensätzen aus Ergebnissen in Query Service

Die wahre Macht von [!DNL Query Service] wird angezeigt, wenn Abfragen zum Generieren von Datensätzen in der [!DNL Data Lake] als Eingabe für weitere Abfragen oder andere Dienste wie [!DNL Data Science Workspace], [!DNL Real-time Customer Profile]oder [!DNL Analysis Workspace].

[!DNL Query Service] ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Führen Sie folgende Schritte aus:

1. Schreiben Sie Ihre Anfrage mit einem verbundenen Client und validieren Sie die Ausgabe.
2. Melden Sie sich bei der [!DNL Platform] Benutzeroberfläche und gehen Sie zu Abfragen .
3. Suchen Sie Ihre Abfrage in der Liste und bewegen Sie den Mauszeiger über die Zeile.
4. Auswählen **[!UICONTROL Datensatz erstellen]**. ![Bild](../images/ui/create-datasets/output-dataset.png)
5. Geben Sie einen Namen für den Datensatz, dem Ihre LDAP-ID vorangestellt wird (muss nicht eindeutig oder SQL-sicher sein. Das System erzeugt anhand des hier angegebenen Namens einen „Tabellennamen“).
6. Geben Sie eine Datensatzbeschreibung ein und wählen Sie **[!UICONTROL Abfrage ausführen]**.![Bild](../images/ui/create-datasets/run-query.png)
7. Warten Sie, bis die Abfrage abgeschlossen ist, und rufen Sie dann die Seite mit der Datensatzliste auf, um den gerade erstellten Datensatz anzuzeigen.

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im [!DNL Data Lake] und für eine Vielzahl von Anwendungsfällen verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie nach der Erstellung des Datensatzes die Data Governance-Beschriftungen angeben.

## Erstellen von Datensätzen mit einer vordefinierten [!DNL Experience Data Model] schema

So generieren Sie einen Datensatz mit einer vordefinierten [!DNL Experience Data Model] (XDM)-Schema verwenden, müssen Sie die SQL-Syntax verwenden. Weitere Informationen zur Syntax finden Sie im [Handbuch zur SQL-Syntax](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Einige nachgelagerte Dienste erfordern Datensätze mit bestimmten [!DNL Experience Data Model] (XDM)-Schemas. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.
