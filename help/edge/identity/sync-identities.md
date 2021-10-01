---
title: Synchronisieren von Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK
description: Erfahren Sie, wie Sie Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK synchronisieren.
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: Audience Manager; AAM; Identitäten; Synchronisierungsidentitäten; Namespace;
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Identitäten zwischen Audience Manager und Experience Platform synchronisieren

Das Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den Befehl [sendEvent](./overview.md#syncing-identities) zu deklarieren.

Wählen Sie Ihre Namespaces aus den [Identity Service Namespaces](../../identity/../identity-service/namespaces.md) aus, um mithilfe der Werte in der Spalte Identitätssymbol den Kontext anzugeben, auf den sich eine Identität bezieht:

![Ansicht der Benutzeroberfläche von Namespaces](../images/identity/edge_namespaceUI_identity-symbol.png)

Als Audience Manager-Kunde alle Ihre vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifender Namespace verfügt automatisch über einen entsprechenden Identitäts-Namespace. Um den entsprechenden Identitäts-Namespace für Ihre Audience Manager-Datenquelle zu finden, melden Sie sich bei Adobe Experience Platform an und navigieren Sie zum Abschnitt Identitäten .

Jede neue [!DNL Audience Manager] Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identitäts-Namespace generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identitäts-Namespace eine entsprechende [!DNL Audience Manager] Datenquelle. Beachten Sie jedoch, dass die Methode syncIdentity nur Namespace-Identitätssymbole unterstützt.
