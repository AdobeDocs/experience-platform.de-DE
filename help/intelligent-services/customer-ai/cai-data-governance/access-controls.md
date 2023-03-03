---
keywords: Experience Platform; Benutzerhandbuch; Kundinnen- und Kunden-KI; beliebte Themen; Zugriffskontrollen; Modell erstellen;
solution: Experience Platform
feature: Customer AI
title: Zugriffskontrolle für Kundinnen- und Kunden-KI
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffskontrolle für Kundinnen- und Kunden-KI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: ht
source-wordcount: '516'
ht-degree: 100%

---


# Attributbasierte Zugriffssteuerung

>[!IMPORTANT]
>
>Die attributbasierte Zugriffssteuerung ist derzeit nur in einer eingeschränkten Version verfügbar.

Die [attributbasierte Zugriffssteuerung](../../../access-control/abac/overview.md) ist eine Funktion von Adobe Experience Platform, mit der Admins den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mit der attributbasierten Zugriffssteuerung können Sie Schemafelder des Experience-Datenmodells (XDM) mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Admins die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzenden oder Gruppen von Benutzenden (internen, externen oder Dritten) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Admins die Verwaltung des Zugriffs auf bestimmte Segmente.

Mithilfe der attributbasierten Zugriffssteuerung können Admins Ihrer Organisation den Zugriff der Benutzenden sowohl auf sensible persönliche Daten (Sensitive Personal Data, SPD) als auch auf personenbezogene Daten (PII) für alle Platform-Workflows und -Ressourcen steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

Aufgrund der attributbasierten Zugriffskontrolle hätten einige Felder und Funktionen Zugriffsbeschränkungen und wären für bestimmte Kundinnen- und Kunden-KI-Service-Modelle nicht verfügbar. Beispiele sind „Identität“, „Bewertungsdefinition“ und „Klon“.

![Der Arbeitsbereich für die Kundinnen- oder Kunden-KI mit den eingeschränkten Feldern des Service-Modells wird hervorgehoben.](../images/user-guide/unavailable-functionalities.png)

Am oberen Rand der **Insight-Seite** des Arbeitsbereichs der Kundinnen- und Kunden-KI sehen Sie, dass die Details in der Seitenleiste, Bewertungsdefinition, Identität und Profilattribute alle „Zugriff eingeschränkt“ anzeigen.

![Der Arbeitsbereich der Kundinnen- und Kunden-KI mit den eingeschränkten Feldern des Schemas wird hervorgehoben.](../images/user-guide/access-restricted.png)

Bei der Vorschau von Datensätzen mit eingeschränktem Schema auf der Seite **[!UICONTROL Modell-Workflow erstellen]** erscheint ein Warnhinweis, der Ihnen Folgendes mitteilt: [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Datensatzvorschau angezeigt.]

![Der Arbeitsbereich der Kundinnen- und Kunden-KI mit den eingeschränkten Feldern der Vorschaudatensätze mit eingeschränkten Schemaergebnissen wird hervorgehoben.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Nachdem Sie ein Modell mit eingeschränkten Informationen erstellt haben und mit dem Schritt **[!UICONTROL Ziel festlegen]** fortfahren, wird oben eine Warnung angezeigt: [!UICONTROL Aufgrund von Zugriffsbeschränkungen werden bestimmte Informationen nicht in der Konfiguration angezeigt.]

![Der Arbeitsbereich der Kundinnen- und Kunden-KI mit den eingeschränkten Feldern des Service-Modells wird hervorgehoben.](../images/user-guide/information-not-displayed-save-and-exit.png)

Bei Verwendung der Zugriffssteuerung gewähren die Berechtigungen **Anzeigen der Kundinnen- und Kunden-KI** und **Verwalten der Kundinnen- und Kunden-KI** Zugriff auf verschiedene Funktionen der Kundinnen- und Kunden-KI. Die Berechtigung **Verwalten der Kundinnen- und Kunden-KI** erlaubt es Ihnen, ein Modell zu **erstellen**, zu **aktualisieren**, zu **löschen**, zu **aktivieren** oder zu **deaktivieren**, während Sie es mit **Anzeigen der Kundinnen- und Kunden-KI** lesen bzw. anzeigen können. Die Aktionen **Erstellen**, **Aktualisieren** und **Löschen** werden in Adminprotokollen aufgezeichnet.

Weitere Informationen finden Sie in der Dokumentation [Zuweisen von Berechtigungen für die Zugriffskontrolle](../../../access-control/home.md) oder [Verwenden von Adminprotokollen zur Überwachung von Zugriff und Aktivität](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte

Durch das Lesen dieses Handbuchs haben Sie sich mit den Hauptgrundsätzen der Zugangssteuerung in [!DNL Experience Platform] vertraut gemacht. Nun können Sie im [Benutzerhandbuch für die Zugangssteuerung](../overview.md) ausführliche Schritte nachlesen, wie Sie die [!DNL Admin Console] zur Erstellung von Produktprofilen und zur Erteilung von Berechtigungen für [!DNL Platform] nutzen.