---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Datensätze generieren; Datensatz generieren; Datensatz erstellen; Datensatz erstellen
solution: Experience Platform
title: Generieren von Datensätzen aus Ergebnissen in Query Service
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Data Lake aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 40%

---

# Generieren von Datensätzen aus Ergebnissen in Query Service

Die wahre Stärke von [!DNL Query Service] wird deutlich, wenn Abfragen zum Generieren von Datensätzen in [!DNL Data Lake] verwendet werden, die als Eingabe für weitere Abfragen oder in anderen Diensten wie [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] oder [!DNL Analysis Workspace] verwendet werden.

[!DNL Query Service] ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Führen Sie folgende Schritte aus:

1. Schreiben Sie Ihre Anfrage mit einem verbundenen Client und validieren Sie die Ausgabe.
2. Melden Sie sich bei der [!DNL Platform] -Benutzeroberfläche an und gehen Sie zu Abfragen .
3. Suchen Sie Ihre Abfrage in der Liste und bewegen Sie den Mauszeiger über die Zeile.
4. Wählen Sie **[!UICONTROL Datensatz erstellen]** aus. ![Bild](../images/ui/create-datasets/output-dataset.png)
5. Geben Sie einen Namen für den Datensatz, dem Ihre LDAP-ID vorangestellt wird (muss nicht eindeutig oder SQL-sicher sein. Das System erzeugt anhand des hier angegebenen Namens einen „Tabellennamen“).
6. Geben Sie eine Datensatzbeschreibung ein und wählen Sie **[!UICONTROL Abfrage ausführen]** aus.![Bild](../images/ui/create-datasets/run-query.png)
7. Warten Sie, bis die Abfrage abgeschlossen ist, und rufen Sie dann die Seite mit der Datensatzliste auf, um den gerade erstellten Datensatz anzuzeigen.

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz in [!DNL Data Lake] aufgerufen und für verschiedene Anwendungsfälle verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie [!DNL Data Governance]-Beschriftungen nach der Erstellung des Datensatzes anwenden.

## Generieren von Datensätzen mit einem vordefinierten [!DNL Experience Data Model]-Schema

Um einen Datensatz mit einem vordefinierten [!DNL Experience Data Model] (XDM)-Schema zu generieren, müssen Sie die SQL-Syntax verwenden. Weitere Informationen zur Syntax finden Sie im [Handbuch zur SQL-Syntax](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Einige nachgelagerte Dienste erfordern Datensätze mit bestimmten [!DNL Experience Data Model] (XDM)-Schemas. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.
