---
keywords: Experience Platform; Benutzerhandbuch; Kundenunterstützung; beliebte Themen; Zugriffskontrollen; Modell erstellen
solution: Experience Platform
feature: Customer AI
title: Zugriffskontrolle für Customer AI
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffskontrolle für Customer AI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 37%

---


# Attributbasierte Zugriffssteuerung

>[!IMPORTANT]
>
>Die attributbasierte Zugriffskontrolle ist derzeit nur in einer eingeschränkten Version verfügbar.

[Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können.](../../../access-control/abac/overview.md) Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mit der attributbasierten Zugriffssteuerung können Sie Schemafelder des Experience-Datenmodells (XDM) mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Admins die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzenden oder Gruppen von Benutzenden (internen, externen oder Dritten) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Admins die Verwaltung des Zugriffs auf bestimmte Segmente.

Mithilfe der attributbasierten Zugriffskontrolle können Administratoren Ihres Unternehmens den Zugriff der Benutzer auf sowohl sensible persönliche Daten (EPPD) als auch personenbezogene Daten (PII) in allen Platform-Workflows und -Ressourcen steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

Aufgrund der attributbasierten Zugriffskontrolle wären für einige Felder und Funktionen Zugriffsbeschränkungen eingeschränkt und für bestimmte Customer AI-Dienstmodelle nicht verfügbar. Beispiele sind &quot;Identität&quot;, &quot;Score-Definition&quot;und &quot;Klon&quot;.

![Der Arbeitsbereich Customer AI mit den eingeschränkten Feldern des Dienstmodells wird hervorgehoben.](../images/user-guide/unavailable-functionalities.png)

Am oberen Rand des Arbeitsbereichs &quot;Customer AI&quot; **Insight-Seite** Beachten Sie, dass die Details in der Seitenleiste, der Bewertungsdefinition, der Identität und den Profilattributen alle &quot;Zugriff eingeschränkt&quot;anzeigen.

![Der Arbeitsbereich Customer AI mit den eingeschränkten Feldern des Schemas wird hervorgehoben.](../images/user-guide/access-restricted.png)

Bei der Vorschau von Datensätzen mit eingeschränktem Schema auf der **[!UICONTROL Modell-Workflow erstellen]** angezeigt wird, erscheint ein Warnhinweis, der Ihnen mitteilt, dass [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Datensatzvorschau angezeigt.]

![Der Customer AI-Arbeitsbereich mit den eingeschränkten Feldern der Vorschau-Datensätze mit eingeschränkten Schemaergebnissen hervorgehoben.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Nachdem Sie ein Modell mit eingeschränkten Informationen erstellt haben, fahren Sie mit dem **[!UICONTROL Ziel definieren]** Schritt, wird oben eine Warnung angezeigt: [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Konfiguration angezeigt.]

![Der Arbeitsbereich Customer AI mit den eingeschränkten Feldern des Dienstmodells wird hervorgehoben.](../images/user-guide/information-not-displayed-save-and-exit.png)

Bei Verwendung der Zugriffssteuerung muss die **Anzeigen von Customer AI** und **Customer AI verwalten** -Berechtigungen gewähren Zugriff auf verschiedene Funktionen von Customer AI. Die **Customer AI verwalten** -Berechtigung **erstellen**,**update**, **delete**, **enable** oder **disable** ein Modell während **Anzeigen von Customer AI** Sie können sie lesen oder anzeigen. Die **erstellen**, **update** und **delete** -Aktionen werden in Auditprotokollen aufgezeichnet.

Weitere Informationen finden Sie in der Dokumentation . [Zuweisen von Berechtigungen für die Zugriffskontrolle](../../../access-control/home.md) oder wie [Verwenden Sie Auditprotokolle zur Überwachung von Zugriff und Aktivität.](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte

Durch das Lesen dieses Handbuchs haben Sie sich mit den Hauptgrundsätzen der Zugangssteuerung in [!DNL Experience Platform] vertraut gemacht. Nun können Sie im [Benutzerhandbuch für die Zugangssteuerung](../overview.md) ausführliche Schritte nachlesen, wie Sie die [!DNL Admin Console] zur Erstellung von Produktprofilen und zur Erteilung von Berechtigungen für [!DNL Platform] nutzen.