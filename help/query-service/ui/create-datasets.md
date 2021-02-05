---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Datensätze generieren;Datensatz generieren;Datensatz erstellen;
solution: Experience Platform
title: Generieren von Datensätzen aus Ergebnissen im Abfrage-Dienst
topic: queries
type: Tutorial
description: 'Der Adobe Experience Platform Abfrage Service ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Data Lake aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden. '
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 43%

---


# Generieren von Datensätzen aus Ergebnissen im Abfrage-Dienst

Die wahre Stärke von [!DNL Query Service] wird angezeigt, wenn Abfragen zum Generieren von Datensätzen im [!DNL Data Lake] verwendet werden, die als Eingabe in mehr Abfragen oder in anderen Diensten wie [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] oder [!DNL Analysis Workspace] verwendet werden sollen.

[!DNL Query Service] ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Führen Sie folgende Schritte aus:

1. Schreiben Sie Ihre Anfrage mit einem verbundenen Client und validieren Sie die Ausgabe.
2. Melden Sie sich bei der [!DNL Platform]-Benutzeroberfläche an und gehen Sie zu Abfragen.
3. Suchen Sie Ihre Abfrage in der Liste und bewegen Sie den Mauszeiger über die Zeile.
4. Klicken Sie auf **[!UICONTROL Datensatz erstellen]**. ![Bild](../images/ui/output-dataset.png)
5. Geben Sie einen Namen für den Datensatz, dem Ihre LDAP-ID vorangestellt wird (muss nicht eindeutig oder SQL-sicher sein. Das System erzeugt anhand des hier angegebenen Namens einen „Tabellennamen“).
6. Geben Sie eine Beschreibung für den Datensatz ein und klicken Sie dann auf **[!UICONTROL Abfrage ausführen]**.![Bild](../images/ui/run-query.png)
7. Warten Sie, bis die Abfrage abgeschlossen ist, und rufen Sie dann die Seite mit der Datensatzliste auf, um den gerade erstellten Datensatz anzuzeigen.

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz in [!DNL Data Lake] aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie nach der Erstellung des Datensatzes [!DNL Data Governance]-Beschriftungen anwenden.

## Generieren von Datensätzen mit einem vordefinierten [!DNL Experience Data Model]-Schema

Um ein Dataset mit einem vordefinierten [!DNL Experience Data Model] (XDM) Schema zu generieren, müssen Sie die SQL-Syntax verwenden. Weitere Informationen zur Syntax finden Sie im [Handbuch zur SQL-Syntax](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Einige nachgelagerte Dienste erfordern Datensätze mit bestimmten [!DNL Experience Data Model] (XDM)-Schemas. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.