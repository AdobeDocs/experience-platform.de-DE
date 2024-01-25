---
title: Synchronisieren von Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK
description: Erfahren Sie, wie Sie Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK synchronisieren.
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: Audience Manager; AAM; Identitäten; Synchronisierungsidentitäten; Namespace;
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Synchronisieren von Identitäten zwischen Audience Manager und Experience Platform

Das Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und ihre Authentifizierungsstatus über die [sendEvent](./overview.md#syncing-identities) Befehl.

Wählen Sie Ihre Namespaces aus dem [Identity Service-Namespaces](../../identity/../identity-service/features/namespaces.md) um den Kontext anzugeben, auf den sich eine Identität bezieht, indem Sie die Werte in der Spalte Identitätssymbol verwenden:

![Ansicht der Benutzeroberfläche von Namespaces](../assets/identity/edge_namespaceUI_identity-symbol.png)

Als Audience Manager-Kunde verfügen alle Ihre vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifender Identitäts-Namespace automatisch über einen entsprechenden Identitäts-Namespace. Um den entsprechenden Identitäts-Namespace für Ihre Audience Manager-Datenquelle zu finden, melden Sie sich bei Adobe Experience Platform an und navigieren Sie zum Abschnitt Identitäten .

Alle neuen [!DNL Audience Manager] Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identity-Namespace generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identitäts-Namespace einen entsprechenden [!DNL Audience Manager] Datenquelle, beachten Sie jedoch, dass die Methode syncIdentity nur Namespace-Identitätssymbole unterstützt.
