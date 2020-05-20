---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Zugriffskontrollen
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Handbuch zur Fehlerbehebung bei Zugriffskontrollen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Zugriffskontrolle in der Adobe Experience Platform. Fragen und Fehlerbehebung zu anderen Plattformdiensten finden Sie im Handbuch [Experience Platform zur Fehlerbehebung](../landing/troubleshooting.md).

Die Experience Platform nutzt die Profil der [Adobe Admin-Konsole](http://adminconsole.adobe.com) , um rollenbasierte **Zugriffskontrollen** bereitzustellen und Benutzer mit Berechtigungen und Sandboxen zu verknüpfen.  See the [access control overview](home.md) for more information.

## Wo finde ich meine aktuellen Zugriffsberechtigungen?

Wenn Sie Systemadministrator, Produktadministrator oder Produktadministrator für Ihre IMS-Organisation sind, können Sie Ihr zugewiesenes Produkt-Profil und die damit verbundenen Berechtigungen in der Adobe Admin-Konsole Ansicht haben. Anweisungen zum Navigieren in der Admin-Konsole zur Ansicht der Berechtigungen eines Profils finden Sie im Benutzerhandbuch für die [Zugriffskontrolle](./ui/overview.md) .

Wenn Sie kein Administrator sind, können Sie Ihre aktuellen Zugriffsberechtigungen dennoch Ansicht haben, indem Sie eine Anforderung an den `/acl/effective-policies` Endpunkt in der Zugriffskontrollen-API senden. Weitere Informationen finden Sie im Abschnitt &quot;Ansicht-Richtlinien&quot;im [Zugriffskontrolle-Entwicklerhandbuch](./api/effective-policies.md) .

## Einige Funktionen der Plattform-Benutzeroberfläche sind nicht verfügbar. Wie wird der Zugriff auf diese Funktionen durch Berechtigungen gesteuert?

Wenn Sie keine Zugriffsberechtigungen für eine bestimmte Plattformfunktion haben, wird diese Funktion in der Experience Platform-Benutzeroberfläche ausgeblendet oder ausgegraut dargestellt. Um beispielsweise die Registerkarte &quot;Profil&quot;Ansicht, müssen Sie entweder über die Berechtigungen &quot;Ansicht Profil&quot;oder &quot;Profil verwalten&quot;verfügen. Wenden Sie sich an Ihren Administrator, wenn Sie zusätzliche Berechtigungen für Experience Platform-Funktionen benötigen.

## Wie werden Berechtigungen gruppiert und welche Gruppe enthält die Berechtigung, die ich verwenden möchte?

Berechtigungen werden nach Plattformfunktionen gruppiert und kategorisiert, auf die sie angewendet werden (z. B. Data Management- und Profil-Management). Eine vollständige Liste der verfügbaren Berechtigungen und der Gruppen, zu denen sie gehören, finden Sie im Abschnitt &quot; [Berechtigungen&quot;](home.md#permissions) in der Übersicht über die Zugriffskontrolle.

Weitere Informationen zur rollenbasierten Zugriffskontrolle finden Sie in der Übersicht über die [Zugriffskontrolle](home.md) .