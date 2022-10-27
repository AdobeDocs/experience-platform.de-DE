---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Datensätze generieren; Datensatz generieren; Datensatz erstellen; Datensatz erstellen
solution: Experience Platform
title: Generieren von Datensätzen aus Ergebnissen in Query Service
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Data Lake aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 228ed51ea056d3593a59bc0eee8d9b767aa74489
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 11%

---

# Generieren von Datensätzen aus Ergebnissen in [!DNL Query Service]

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Abfragen zum Generieren von Datensätzen im [!DNL Data Lake]. Diese Datensätze können dann als Eingabe für weitere Abfragen oder in anderen Diensten wie [!DNL Data Science Workspace], Echtzeit-Kundenprofil oder [!DNL Analysis Workspace].

## Generieren von Datensätzen über die Benutzeroberfläche von Adobe Experience Platform

<!-- Screenshot for #3 will need to be updated if schedule queries is moved. -->

Gehen Sie wie folgt vor, um Datensätze über die Adobe Experience Platform-Benutzeroberfläche zu erstellen:

1. Erstellen Sie eine Abfrage mit einem verbundenen Client und validieren Sie die Ausgabe. So erfahren Sie, wie Sie Abfragen mit [!DNL Query Editor], lesen Sie die [!DNL Query Editor] UI-Handbuch [Erstellen von Abfragen](./user-guide.md#writing-queries).

2. Navigieren Sie in der Platform-Benutzeroberfläche zu **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Durchsuchen]** und wählen Sie die erstellte Abfrage aus. Weitere Informationen zum Anzeigen von Abfragen, die für Ihr Unternehmen in der Platform-Benutzeroberfläche erstellt und gespeichert wurden, finden Sie im Abschnitt [[!DNL Query Service] Übersicht](./overview.md#browse).

3. Wählen Sie im Bereich &quot;Query details&quot;die Option **[!UICONTROL Ausgabedatensatz]**.

   ![Registerkarte &quot;Abfragearbeitsbereichsvorlage&quot;mit hervorgehobenem Symbol Ausgabedatensatz auswählen.](../images/ui/create-datasets/output-dataset.png)

4. Geben Sie im angezeigten Dialogfeld einen Datensatznamen ein, dem Ihre LDAP-ID vorangestellt wird. Der Datensatzname muss nicht eindeutig oder SQL-sicher sein. Beachten Sie, dass der Tabellenname für Ihren Datensatz basierend auf dem hier erstellten Datensatznamen generiert wird.

5. Geben Sie als Nächstes eine Beschreibung für Ihren Datensatz in die [!UICONTROL Beschreibung] Feld und wählen Sie **[!UICONTROL Abfrage ausführen]**.

   ![Das Dialogfeld Ausgabedatensatz mit den Datensatzdetails und hervorgehobenen Ausführungsabfragen](../images/ui/create-datasets/run-query.png)

6. Nachdem die Abfrage ausgeführt wurde, navigieren Sie zu **[!UICONTROL Datensätze]** , um den von Ihnen erstellten Datensatz anzuzeigen. Weitere Informationen zum Ausführen allgemeiner Aktionen beim Arbeiten mit Datensätzen in der Platform-Benutzeroberfläche finden Sie in der [Handbuch zur Benutzeroberfläche von Datensätzen](../../catalog/datasets/user-guide.md).

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im [!DNL Data Lake] und für eine Vielzahl von Anwendungsfällen verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie nach der Erstellung des Datensatzes die Data Governance-Beschriftungen angeben. Weitere Informationen zum Anwenden von Datennutzungsbezeichnungen auf Datensätze finden Sie unter [Datennutzungsbezeichnungen - Übersicht](../../data-governance/labels/overview.md).

## Erstellen von Datensätzen mit einer vordefinierten [!DNL Experience Data Model] schema

Verwenden Sie die SQL-Syntax, um einen Datensatz mit einer vordefinierten [!DNL Experience Data Model] (XDM)-Schema. Weitere Informationen zur Syntax, die von [!DNL Query Service], lesen Sie bitte die [SQL-Syntaxhandbuch](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Einige nachgelagerte Dienste erfordern Datensätze mit bestimmten XDM-Schemas. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.

## Nächste Schritte

Nach dem Lesen dieses Dokuments sollten Sie jetzt wissen, wie Sie [!DNL Query Service] , um Datensätze über die Platform-Benutzeroberfläche zu generieren. Weitere Informationen zum Zugreifen auf, Schreiben und Ausführen von Abfragen in der Platform-Benutzeroberfläche finden Sie unter [[!DNL Query Service] Übersicht über die Benutzeroberfläche](./overview.md).
