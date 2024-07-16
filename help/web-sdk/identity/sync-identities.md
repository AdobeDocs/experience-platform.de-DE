---
title: Synchronisieren von Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK
description: Erfahren Sie, wie Sie Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK synchronisieren.
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: Audience Manager; AAM; Identitäten; Synchronisierungsidentitäten; Namespace;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Synchronisieren von Identitäten zwischen Audience Manager und Experience Platform

Das Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den Befehl [sendEvent](./overview.md#syncing-identities) zu deklarieren.

Wählen Sie Ihre Namespaces aus den [Identity Service Namespaces](../../identity/../identity-service/features/namespaces.md) aus, um den Kontext anzugeben, auf den sich eine Identität bezieht, indem Sie die Werte in der Spalte Identity Symbol verwenden:

![Ansicht der Benutzeroberfläche &quot;Namespaces&quot;](../assets/identity/edge_namespaceUI_identity-symbol.png)

Als Audience Manager-Kunde verfügen alle Ihre vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifender Identitäts-Namespace automatisch über einen entsprechenden Identitäts-Namespace. Um den entsprechenden Identitäts-Namespace für Ihren Audience Manager Data Source zu finden, melden Sie sich bei Adobe Experience Platform an und navigieren Sie zum Abschnitt Identitäten .

Jede neue [!DNL Audience Manager] Data Source, die den ID-Typ verwendet: Geräteübergreifend generiert einen entsprechenden Identitäts-Namespace. Cookies und Geräte-Advertising-ID-Typen für Data Source ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identitäts-Namespace eine entsprechende [!DNL Audience Manager] Data Source. Beachten Sie jedoch, dass die syncIdentity-Methode nur Namespace-Identitätssymbole unterstützt.
