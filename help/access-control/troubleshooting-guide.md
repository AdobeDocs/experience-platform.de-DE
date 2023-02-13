---
keywords: Experience Platform;Home;beliebte Themen;Fehlerbehebung;Zugriffssteuerung
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei der Zugriffssteuerung
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: ht
source-wordcount: '408'
ht-degree: 100%

---

# Handbuch zur Fehlerbehebung bei der Zugriffssteuerung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in Adobe Experience Platform. Fragen und Fehlerbehebungen für andere [!DNL Platform]-Services finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] nutzt Produktprofile in der [Adobe Admin Console](https://adminconsole.adobe.com), um rollenbasierte Zugriffskontrolle bereitzustellen und Anwender mit Berechtigungen und Sandboxes zu verknüpfen.  Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](home.md).

## Wo finde ich meine aktuellen Zugriffsberechtigungen?

Wenn Sie Systemadministrator, Produktadministrator oder Produktprofiladministrator für Ihre IMS-Organisation sind, können Sie Ihr zugewiesenes Produktprofil und die damit verbundenen Berechtigungen in der Adobe Admin Console anzeigen. Anweisungen zum Navigieren der für das Anzeigen der Berechtigungen eines Produktprofils finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](./ui/overview.md) [!DNL Admin Console].

Wenn Sie kein Administrator sind, können Sie Ihre aktuellen Zugriffsberechtigungen dennoch anzeigen, indem Sie eine Anfrage an den `/acl/effective-policies`-Endpunkt in der Access Control-API senden. Weiterführende Informationen finden Sie im Abschnitt „Gültige Richtlinien anzeigen“ im [Entwicklerhandbuch zur Zugriffskontrolle](./api/effective-policies.md).

## Einige Funktionen in der [!DNL Platform]-Benutzeroberfläche sind nicht verfügbar. Wie wird der Zugriff auf diese Funktionen durch Berechtigungen gesteuert?

Wenn Sie keine Zugriffsberechtigungen für eine bestimmte [!DNL Platform]-Funktion haben, wird diese Funktion in der [!DNL Experience Platform]-Benutzeroberfläche ausgeblendet oder ausgegraut dargestellt. Um beispielsweise den Tab [!UICONTROL Profile] anzeigen zu können, müssen Sie entweder über die Berechtigung [!UICONTROL Profile anzeigen] oder über [!UICONTROL Profile verwalten] verfügen. Wenden Sie sich an Ihren Administrator, wenn Sie zusätzliche Berechtigungen für Funktionen von [!DNL Experience Platform] benötigen.

## Wie werden Berechtigungen angeordnet, und welche Gruppe enthält die Berechtigung, die ich verwenden möchte?

Berechtigungen werden nach den Funktionen von [!DNL Platform] gruppiert und kategorisiert, für die sie gelten (z. B. [!DNL Data Management] und [!DNL Profile Management]). Eine vollständige Liste der verfügbaren Berechtigungen sowie der Gruppen, zu denen sie gehören, finden Sie im Abschnitt [Berechtigungen](home.md#permissions) in der Übersicht zur Zugriffskontrolle.

Weiterführende Informationen zur Bereitstellung rollenbasierter Zugriffskontrolle finden Sie unter [Zugriffskontrolle – Übersicht](home.md).

## Was passiert mit Berechtigungen nach der Migration von Adobe IO zu Business ID?

Die Zugriffssteuerung verwendet die Benutzer-ID (eine interne eindeutige ID, die einem Benutzer zugewiesen ist) zum Gewähren von Berechtigungen. Wenn eine Organisation von Adobe ID zu Business ID migriert wird, gehen alle für ihre Benutzer festgelegten Berechtigungen verloren, da sich die Benutzer-ID ändert und die Zugriffssteuerung die neu generierte Benutzer-ID verwendet. Wenn Ihre Organisation zu Business ID migriert wird, wenden Sie sich an den Adobe-Support-Mitarbeiter, um Ihre Benutzer-ID von Adobe ID zu Business ID zu migrieren.
