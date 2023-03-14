---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;Adobe Admin Console
solution: Experience Platform
feature: Attribution AI
title: Zugriffssteuerung für Attributions-KI
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffssteuerung für Attributions-KI.
source-git-commit: d82fd8dd5efbe314c09d32905f8ab964640cc11a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 100%

---


# Zugriffssteuerung

Die Zugriffssteuerung für Attributions-KI wird über Adobe Experience Platform in [Adobe Admin Console](https://adminconsole.adobe.com/) bereitgestellt Diese Funktion nutzt Produktprofile in Admin Console, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../../access-control/home.md).

## Attributbasierte Zugriffssteuerung

>[!IMPORTANT]
>
>Die attributbasierte Zugriffssteuerung ist derzeit nur in einer eingeschränkten Version verfügbar.

[Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. ](../../../access-control/abac/overview.md) Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mit der attributbasierten Zugriffssteuerung können Sie Schemafelder des Experience-Datenmodells (XDM) mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Admins die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzenden oder Gruppen von Benutzenden (internen, externen oder Dritten) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Admins die Verwaltung des Zugriffs auf bestimmte Segmente.

Mithilfe der attributbasierten Zugriffssteuerung können Administrierende den Zugriff der Benutzenden sowohl auf sensible persönliche Daten (Sensitive Personal Data, SPD) als auch auf personenbezogene Daten (Personally Identifiable Information, PII) für alle Platform-Workflows und -Ressourcen steuern. Administrierende können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

Aufgrund der attributbasierten Zugriffssteuerung sind einige Felder und Funktionen möglicherweise eingeschränkt und für bestimmte Attributions-KI-Service-Mdelle nicht verfügbar. Beispiele sind „Identität“, „Bewertungsdefinition“ und „Klon“.

Oben auf der **Insight-Seite** des Arbeitsbereichs „Attributions-KI“ kann auf die Details, die in der Seitenleiste angezeigt werden, nur eingeschränkt zugegriffen werden.

![Der Arbeitsbereich „Attributions-KI“ mit hervorgehobenen eingeschränkten Schemafeldern.](../images/user-guide/access-restricted.png)

Wenn Sie auf der Seite **[!UICONTROL Modell-Workflow erstellen]** Datensätze mit eingeschränkten Schemata auswählen, wird neben dem Datensatznamen ein Warnzeichen mit folgender Meldung angezeigt: [!UICONTROL Eingeschränkte Informationen sind ausgeschlossen].

![Der Arbeitsbereich „Attributions-KI“ mit hervorgehobenen eingeschränkten Datensatzfeldern](../images/user-guide/restricted-info-excluded.png)

Bei der Vorschau von Datensätzen mit eingeschränktem Schema auf der Seite **[!UICONTROL Modell-Workflow erstellen]** werden Sie über eine Warnung darauf hingewiesen, dass [!UICONTROL aufgrund von Zugriffsbeschränkungen bestimmte Informationen nicht in der Datensatzvorschau angezeigt werden].

![Der Arbeitsbereich „Attributions-KI“ mit hervorgehobenen Vorschauergebnissen bei eingeschränkten Schemafeldern](../images/user-guide/restricted-dataset-preview.png)

Wenn Sie ein Modell mit eingeschränkten Informationen erstellt haben und mit dem Schritt **[!UICONTROL Ziel definieren]** fortfahren, wird oben folgende Warnung angezeigt: [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Konfiguration angezeigt.]

![Der Arbeitsbereich „Attributions-KI“ mit hervorgehobenen eingeschränkten Feldern der Modellergebnisse.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Nächste Schritte

Durch das Lesen dieses Handbuchs haben Sie sich mit den Hauptgrundsätzen der Zugangssteuerung in [!DNL Experience Platform] vertraut gemacht. Nun können Sie im [Benutzerhandbuch für die Zugangssteuerung](../overview.md) ausführliche Schritte nachlesen, wie Sie die [!DNL Admin Console] zur Erstellung von Produktprofilen und zur Erteilung von Berechtigungen für [!DNL Platform] nutzen.
