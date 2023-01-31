---
keywords: Experience Platform;Startseite;beliebte Themen;Zugangssteuerung;adobe Admin Console
solution: Experience Platform
feature: Attribution AI
title: Zugriffskontrolle für Attribution AI
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffskontrolle für Attribution AI.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 43%

---


# Zugriffssteuerung

Die Zugriffskontrolle für Attribution AI wird über Adobe Experience Platform im Abschnitt [Adobe Admin Console](https://adminconsole.adobe.com/). Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/home).

## Attributbasierte Zugriffssteuerung

>[!IMPORTANT]
>
>Die attributbasierte Zugriffskontrolle ist derzeit nur in einer eingeschränkten Version verfügbar.

[Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können.](../../../help/access-control/abac/overview.md) Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mit der attributbasierten Zugriffssteuerung können Sie Schemafelder des Experience-Datenmodells (XDM) mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Admins die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzenden oder Gruppen von Benutzenden (internen, externen oder Dritten) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Admins die Verwaltung des Zugriffs auf bestimmte Segmente.

Mithilfe der attributbasierten Zugriffskontrolle können Administratoren den Zugriff der Benutzer auf sowohl sensible persönliche Daten (EPPD) als auch personenbezogene Daten (PII) in allen Platform-Workflows und -Ressourcen steuern. Administratoren können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

Aufgrund der attributbasierten Zugriffskontrolle sind einige Felder und Funktionen möglicherweise eingeschränkt und für bestimmte Attribution AI-Dienstmodelle nicht verfügbar. Beispiele sind &quot;Identität&quot;, &quot;Score-Definition&quot;und &quot;Klon&quot;.

Oben im Arbeitsbereich &quot;Attribution AI&quot; **Insight-Seite**, haben die Details, die in der Seitenleiste angezeigt werden, eingeschränkten Zugriff.

![Der Arbeitsbereich Attribution AI mit hervorgehobenen eingeschränkten Schemafeldern.](./images/user-guide/access-restricted.png)

Wenn Sie Datensätze mit eingeschränkten Schemas im **[!UICONTROL Modell-Workflow erstellen]** -Seite wird neben dem Datensatznamen ein Warnzeichen mit der Meldung angezeigt: [!UICONTROL Eingeschränkte Informationen sind ausgeschlossen].

![Der Arbeitsbereich Attribution AI mit hervorgehobenen eingeschränkten Datensatzfeldern.](./images/user-guide/restricted-info-excluded.png)

Bei der Vorschau von Datensätzen mit eingeschränktem Schema auf der **[!UICONTROL Modell-Workflow erstellen]** angezeigt wird, erscheint ein Warnhinweis, der Ihnen mitteilt, dass [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Datensatzvorschau angezeigt.]

![Der Arbeitsbereich Attribution AI , in dem die Ergebnisse der eingeschränkten Vorschau von Schemafeldern hervorgehoben sind.](./images/user-guide/restricted-dataset-preview.png)

Nachdem Sie ein Modell mit eingeschränkten Informationen erstellt haben, fahren Sie mit dem **[!UICONTROL Ziel definieren]** Schritt, wird oben eine Warnung angezeigt: [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Konfiguration angezeigt.]

![Der Arbeitsbereich Attribution AI mit den eingeschränkten Feldern der Modellergebnisse hervorgehoben.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Nächste Schritte

Durch das Lesen dieses Handbuchs haben Sie sich mit den Hauptgrundsätzen der Zugangssteuerung in [!DNL Experience Platform] vertraut gemacht. Nun können Sie im [Benutzerhandbuch für die Zugangssteuerung](./ui/overview.md) ausführliche Schritte nachlesen, wie Sie die [!DNL Admin Console] zur Erstellung von Produktprofilen und zur Erteilung von Berechtigungen für [!DNL Platform] nutzen.
