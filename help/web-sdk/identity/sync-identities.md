---
title: Synchronisieren von Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe der Experience Platform Web SDK
description: Erfahren Sie, wie Sie Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe der Experience Platform Web SDK synchronisieren
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: Audience Manager;AAM;Identitäten;Identitäten synchronisieren;Namespace;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Synchronisieren von Identitäten zwischen Audience Manager und Experience Platform

Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den Befehl [sendEvent](./overview.md#syncing-identities) zu deklarieren.

Wählen Sie Ihre Namespaces aus den [Identity Service-Namespaces](../../identity/../identity-service/features/namespaces.md) aus, um den Kontext anzugeben, auf den sich eine Identität bezieht, indem Sie die Werte in der Spalte „Identitätssymbol“ verwenden:

![Ansicht der Namespaces-Benutzeroberfläche](../assets/identity/edge_namespaceUI_identity-symbol.png)

Wenn Sie Audience Manager-Kunde sind, verfügen alle vorhandenen Datenquellen, die den ID-Typ verwenden: Geräteübergreifend, automatisch über einen entsprechenden Identity-Namespace. Um den entsprechenden Identity-Namespace für Ihre Audience Manager Data Source zu finden, melden Sie sich bei Adobe Experience Platform an und navigieren Sie zum Abschnitt Identitäten .

Jeder neue [!DNL Audience Manager]-Daten-Source, der den ID-Typ „Geräteübergreifend“ verwendet, generiert einen entsprechenden Identity-Namespace. Data Source ID Types Cookie und Device Advertising ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identity-Namespace einen entsprechenden [!DNL Audience Manager] Data Source, wobei jedoch zu beachten ist, dass die syncIdentity-Methode nur Namespace-Identitätssymbole unterstützt.
