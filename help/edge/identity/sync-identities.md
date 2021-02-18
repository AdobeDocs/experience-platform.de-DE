---
title: Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK synchronisieren
description: Erfahren Sie, wie Identitäten zwischen Audience Manager und Adobe Experience Platform mithilfe des Platform Web SDK synchronisiert werden.
seo-description: Erfahren Sie, wie Identitäten mit Adobe Audience Manager mit Experience Platform Web SDK synchronisiert werden
keywords: Audiencen-Manager;aam;Identitäten;Synchronisierungskennungen;Namensraum;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Identitäten zwischen Audience Manager und Experience Platform synchronisieren

Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den Befehl [sendEvent](./overview.md#syncing-identities) zu deklarieren.

Wählen Sie Ihre Namensraum aus den Namensräumen [Identitätsdienst](../../identity/../identity-service/namespaces.md) aus, um mithilfe der Werte in der Spalte &quot;Identitätssymbol&quot;den Kontext anzugeben, auf den sich eine Identität bezieht:

![Ansicht der Benutzeroberfläche der Namensraum](../../assets/edge_namespaceUI_identity-symbol.png)

Als Audience Manager verwenden Sie alle vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifende Elemente verfügen automatisch über einen entsprechenden Identitäts-Namensraum. Um den entsprechenden Identitäts-Namensraum für Ihre Audience Manager-Datenquelle zu finden, melden Sie sich bei Adobe Experience Platform an und navigieren Sie zum Identitätsabschnitt.

Jede neue [!DNL Audience Manager]-Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identitäts-Namensraum generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identity Namensraum eine entsprechende [!DNL Audience Manager]-Datenquelle, beachten Sie jedoch, dass die syncIdentity-Methode nur Namensraum-Identitätssymbole unterstützt.
