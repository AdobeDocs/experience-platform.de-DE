---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei der Zugriffskontrolle
topic: troubleshooting guide
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 71%

---


# Handbuch zur Fehlerbehebung bei der Zugriffskontrolle

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform. For questions and troubleshooting related to other [!DNL Platform] services, please refer to the [Experience Platform troubleshooting guide](../landing/troubleshooting.md).

[!DNL Experience Platform] nutzt Produktprofile in der [Adobe Admin Console](http://adminconsole.adobe.com), um rollenbasierte Zugriffskontrolle bereitzustellen und Anwender mit Berechtigungen und Sandboxes zu verknüpfen.  Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](home.md).

## Wo finde ich meine aktuellen Zugriffsberechtigungen?

Wenn Sie Systemadministrator, Produktadministrator oder Produktprofiladministrator für Ihre IMS-Organisation sind, können Sie Ihr zugewiesenes Produktprofil und die damit verbundenen Berechtigungen in der Adobe Admin Console anzeigen. Anweisungen zum Navigieren der für das Anzeigen der Berechtigungen eines Produktprofils finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](./ui/overview.md).[!DNL Admin Console]

Wenn Sie kein Administrator sind, können Sie Ihre aktuellen Zugriffsberechtigungen dennoch anzeigen, indem Sie eine Anfrage an den `/acl/effective-policies`-Endpunkt in der Access Control-API senden. Weiterführende Informationen finden Sie im Abschnitt „Gültige Richtlinien anzeigen“ im [Entwicklerhandbuch zur Zugriffskontrolle](./api/effective-policies.md).

## Some features in the [!DNL Platform] UI are not available. Wie wird der Zugriff auf diese Funktionen durch Berechtigungen gesteuert?

If you do not have access permissions for a particular [!DNL Platform] feature, that feature will be hidden or greyed-out in the [!DNL Experience Platform] UI. For example, in order to view the &quot;[!UICONTROL Profiles]&quot; tab, you must have either the &quot;[!UICONTROL View Profiles]&quot; or &quot;[!UICONTROL Manage Profiles]&quot; permissions. Contact your administrator if you require additional permissions for [!DNL Experience Platform] capabilities.

## Wie werden Berechtigungen angeordnet, und welche Gruppe enthält die Berechtigung, die ich verwenden möchte?

Berechtigungen werden nach den [!DNL Platform] Funktionen gruppiert und kategorisiert, für die sie gelten (z. B. [!DNL Data Management] und [!DNL Profile Management]). Eine vollständige Liste der verfügbaren Berechtigungen sowie der Gruppen, zu denen sie gehören, finden Sie im Abschnitt [Berechtigungen](home.md#permissions) in der Übersicht zur Zugriffskontrolle.

Weiterführende Informationen zur Bereitstellung rollenbasierter Zugriffskontrolle finden Sie unter [Zugriffskontrolle – Übersicht](home.md).