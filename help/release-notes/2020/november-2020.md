---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform November 2020
doc-type: release notes
last-update: November, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 45%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: November 2020**

Neue Funktionen in Adobe Experience Platform:

- [[!DNL-Zugriffskontrolle]](#access-control)
- [[!DNL Sandboxes]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Platform-Funktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Berechtigungen | In the [!DNL Admin Console], the  tab within a [!DNL Platform] product profile allows you customize which [!DNL Platform] capabilities are available for the users attached to that profile. Available permission categories include: [!UICONTROL Data Modeling], [!UICONTROL Data Management], [!UICONTROL Profile Management], [!UICONTROL Identities], [!UICONTROL Data Monitoring], [!UICONTROL Sandbox Administration], [!UICONTROL Destinations], [!UICONTROL Sources]. |
| Zugriff auf Sandboxes | The **[!UICONTROL Permissions]** tab within a [!DNL Platform] product profile can grant users access to specific sandboxes. Zusätzliche Informationen finden Sie im Abschnitt zu [Sandboxes](#sandboxes) unten. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. In order to address this need, [!DNL Experience Platform] provides sandboxes which partition a single [!DNL Platform] instance into separate virtual environments to help develop and evolve digital experience applications.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Produktions-Sandbox | [!DNL Experience Platform] stellt eine einzelne Produktions-Sandbox bereit, die weder gelöscht noch zurückgesetzt werden kann. |
| Nicht-Produktions-Sandboxes | Multiple non-production sandboxes can be created for a single [!DNL Platform] instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox. |
| Sandbox-Wechsler | In the [!DNL Experience Platform] user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu. |
| `x-sandbox-name`-Kopfzeile | All calls to [!DNL Experience Platform] APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in. |

Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).