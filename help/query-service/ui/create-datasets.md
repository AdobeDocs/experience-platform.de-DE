---
keywords: Experience Platform;Startseite;beliebte Themen;Abfragedienst;Abfrage-Service;Datensätze generieren;Datensatz generieren;Datensatz erstellen
solution: Experience Platform
title: Generieren von Ausgabedatensätzen aus Abfrageergebnissen
type: Tutorial
description: Der Abfrage-Service von Adobe Experience Platform ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Data Lake aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 84%

---

# Generieren von Ausgabedatensätzen aus Abfrageergebnissen

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Abfragen zum Generieren von Datensätzen im [!DNL Data Lake]. Diese Datensätze können dann als Eingabe für weitere Abfragen oder in anderen Diensten wie [!DNL Data Science Workspace], Echtzeit-Kundenprofil oder [!DNL Analysis Workspace].

## Generieren von Datensätzen über die Benutzeroberfläche von Adobe Experience Platform

Gehen Sie wie folgt vor, um Datensätze über die Adobe Experience Platform-Benutzeroberfläche zu erstellen:

1. Schreiben Sie Ihre Abfrage mit einem verbundenen Client und validieren Sie die Ausgabe. Um zu erfahren, wie Sie Abfragen mit dem [!DNL Query Editor] schreiben können, lesen Sie im Handbuch zur [!DNL Query Editor]-Benutzeroberfläche [über das Erstellen von Abfragen](./user-guide.md#writing-queries).

2. Navigieren Sie in der Platform-Benutzeroberfläche zu **[!UICONTROL Abfragen]** und wählen Sie auf der Registerkarte **[!UICONTROL Vorlagen]** die erstellte Abfrage aus. Weitere Informationen zum Anzeigen von Abfragen, die für Ihre Organisation in der Platform-Benutzeroberfläche erstellt und gespeichert wurden, finden Sie in der [[!DNL Query Service] Übersicht](./overview.md#browse).

3. Wählen Sie im Bereich &quot;Query details&quot;die Option **[!UICONTROL Als CTAS ausführen]**.

   ![Der Arbeitsbereich &quot;Abfragen&quot; [!UICONTROL Vorlagen] Registerkarte mit Auswahl [!UICONTROL Als CTAS ausführen] hervorgehoben.](../images/ui/create-datasets/run-as-ctas.png)

4. Geben Sie im angezeigten Dialogfeld einen Datensatznamen ein, dem Ihre LDAP-ID vorangestellt ist. Der Datensatzname muss nicht eindeutig oder SQL-sicher sein. Beachten Sie, dass der Tabellenname für Ihren Datensatz basierend auf dem hier erstellten Datensatznamen generiert wird.

5. Geben Sie als Nächstes eine Beschreibung für Ihren Datensatz in die [!UICONTROL Beschreibung] Feld und wählen Sie **[!UICONTROL Als CTAS ausführen]**.

   ![Das Dialogfeld Ausgabedatensatz mit den Datensatzdetails und [!UICONTROL Als CTAS ausführen] hervorgehoben](../images/ui/create-datasets/run-query.png)

6. Nachdem die Abfrage ausgeführt wurde, navigieren Sie zu **[!UICONTROL Datensätze]**, um den von Ihnen erstellten Datensatz anzuzeigen. Weitere Informationen zum Ausführen allgemeiner Aktionen beim Arbeiten mit Datensätzen in der Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche von Datensätzen](../../catalog/datasets/user-guide.md).

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im [!DNL Data Lake] aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie nach der Erstellung des Datensatzes die Data Governance-Beschriftungen angeben. Weitere Informationen zum Anwenden von Datennutzungskennzeichnungen auf Datensätze finden Sie in der [Übersicht über Datennutzungskennzeichnungen](../../data-governance/labels/overview.md).

## Erstellen von Datensätzen mit einem vordefinierten [!DNL Experience Data Model]-Schema

Verwenden Sie die SQL-Syntax, um einen Datensatz mit einem vordefinierten [!DNL Experience Data Model]-Schema (XDM) zu erstellen. Um weitere Informationen zur Syntax zu erhalten, die vom [!DNL Query Service] unterstützt wird, lesen Sie bitte das [Handbuch zur SQL-Syntax](../sql/syntax.md#create-table-as-select).

## Ausgeben von Datensätzen

Mit dieser Funktionalität erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der in der SQL-Anweisung definierten Struktur der Ausgabedaten entspricht. Einige nachgelagerte Services erfordern Datensätze mit bestimmten XDM-Schemata. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Services, bevor Sie Ihre Abfragen schreiben.

## Nächste Schritte

Nach dem Lesen dieses Dokuments sollten Sie jetzt wissen, wie Sie den [!DNL Query Service] verwenden, um Datensätze über die Platform-Benutzeroberfläche zu generieren. Weitere Informationen zum Zugreifen auf, Schreiben und Ausführen von Abfragen in der Platform-Benutzeroberfläche finden Sie in der [[!DNL Query Service] Benutzeroberflächen-Übersicht](./overview.md).
