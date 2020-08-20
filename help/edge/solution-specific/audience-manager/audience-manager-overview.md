---
title: Daten an Adobe Audience Manager senden
seo-title: Senden von Daten an Adobe Audience Manager mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Daten mit Experience Platform Web SDK an Adobe Audience Manager gesendet werden
seo-description: Erfahren Sie, wie Daten mit Experience Platform Web SDK an Adobe Audience Manager gesendet werden
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] auf [!DNL Experience Platform Edge Network]

Das Adobe Experience Platform [!DNL Web SDK] ist in Adobe Audience Manager integriert und unterstützt das Senden und Empfangen von Daten von [!DNL Audience Manager], Cookie- und URL-Zielen und ID-Synchronisierung.

## Aktivieren [!DNL Audience Manager]

Zur Aktivierung müssen [!DNL Audience Manager] Sie Folgendes ausführen:

- Aktivieren Sie [!DNL Audience Manager] die [Edge-Konfiguration](../../fundamentals/edge-configuration.md).
- Aktivieren oder deaktivieren Sie Cookie- und URL-Ziele.
- Geben Sie Ihren ID-Synchronisierungs-Container für externe Partnersynchronisierungen an (optional)

## Identitäten synchronisieren

Das Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den [sendEvent](../../fundamentals/identity.md#syncing-identities) -Befehl zu deklarieren.

Wählen Sie Ihre Namensraum aus den Namensräumen [für den](../../../identity/../identity-service/namespaces.md) Identitätsdienst aus, um mithilfe der Werte in der Spalte &quot;Identitätssymbol&quot;anzugeben, auf welchen Kontext sich eine Identität bezieht:

![Ansicht der Benutzeroberfläche der Namensraum](../../../assets/edge_namespaceUI_identity-symbol.png)

Als Audience Manager verwenden Sie alle vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifende Elemente verfügen automatisch über einen entsprechenden Identitäts-Namensraum. Um den entsprechenden Identitäts-Namensraum für Ihre Audience Manager-Datenquelle zu finden, melden Sie sich beim Adobe Experience Platform an und navigieren Sie zum Identitätsabschnitt.

Jede neue [!DNL Audience Manager] Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identitäts-Namensraum generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identity Namensraum eine entsprechende [!DNL Audience Manager] Datenquelle, beachten Sie jedoch, dass die syncIdentity-Methode nur Namensraum-Identitätssymbole unterstützt.
