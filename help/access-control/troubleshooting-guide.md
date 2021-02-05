---
keywords: Experience Platform;Home;beliebte Themen;Fehlerbehebung;Zugriffskontrolle
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Zugriffskontrollen
topic: troubleshooting guide
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 68%

---


# Handbuch zur Fehlerbehebung bei der Zugriffskontrolle

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform. Fragen und Fehlerbehebung zu anderen [!DNL Platform]-Diensten finden Sie im [Handbuch zur Fehlerbehebung für Experience Platformen](../landing/troubleshooting.md).

[!DNL Experience Platform] nutzt Produktprofile in der [Adobe Admin Console](http://adminconsole.adobe.com), um rollenbasierte Zugriffskontrolle bereitzustellen und Anwender mit Berechtigungen und Sandboxes zu verknüpfen.  Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](home.md).

## Wo finde ich meine aktuellen Zugriffsberechtigungen?

Wenn Sie Systemadministrator, Produktadministrator oder Produktprofiladministrator für Ihre IMS-Organisation sind, können Sie Ihr zugewiesenes Produktprofil und die damit verbundenen Berechtigungen in der Adobe Admin Console anzeigen. Anweisungen zum Navigieren der für das Anzeigen der Berechtigungen eines Produktprofils finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](./ui/overview.md).[!DNL Admin Console]

Wenn Sie kein Administrator sind, können Sie Ihre aktuellen Zugriffsberechtigungen dennoch anzeigen, indem Sie eine Anfrage an den `/acl/effective-policies`-Endpunkt in der Access Control-API senden. Weiterführende Informationen finden Sie im Abschnitt „Gültige Richtlinien anzeigen“ im [Entwicklerhandbuch zur Zugriffskontrolle](./api/effective-policies.md).

## Einige Funktionen der Benutzeroberfläche [!DNL Platform] sind nicht verfügbar. Wie wird der Zugriff auf diese Funktionen durch Berechtigungen gesteuert?

Wenn Sie keine Zugriffsberechtigungen für eine bestimmte [!DNL Platform]-Funktion haben, wird diese Funktion in der [!DNL Experience Platform]-Benutzeroberfläche ausgeblendet oder grau ausgeblendet. Um beispielsweise die Registerkarte &quot;[!UICONTROL Profil]&quot;Ansicht, müssen Sie entweder über die Profile &quot;[!UICONTROL Ansicht]&quot;oder &quot;[!UICONTROL Profil verwalten]&quot;verfügen. Wenden Sie sich an Ihren Administrator, wenn Sie zusätzliche Berechtigungen für [!DNL Experience Platform]-Funktionen benötigen.

## Wie werden Berechtigungen angeordnet, und welche Gruppe enthält die Berechtigung, die ich verwenden möchte?

Berechtigungen werden nach den [!DNL Platform]-Funktionen gruppiert und kategorisiert, auf die sie angewendet werden (z. B. [!DNL Data Management] und [!DNL Profile Management]). Eine vollständige Liste der verfügbaren Berechtigungen sowie der Gruppen, zu denen sie gehören, finden Sie im Abschnitt [Berechtigungen](home.md#permissions) in der Übersicht zur Zugriffskontrolle.

Weiterführende Informationen zur Bereitstellung rollenbasierter Zugriffskontrolle finden Sie unter [Zugriffskontrolle – Übersicht](home.md).