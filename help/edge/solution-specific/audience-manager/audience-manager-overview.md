---
title: Daten an Adobe Audience Manager senden
seo-title: Senden von Daten an Adobe Audience Manager mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Audience Manager gesendet werden
seo-description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Audience Manager gesendet werden
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] auf [!DNL Experience Platform Edge Network]

Die Adobe Experience Platform [!DNL Web SDK] ist in Adobe Audience Manager integriert und unterstützt das Senden und Empfangen von Daten von [!DNL Audience Manager], Cookie- und URL-Zielen und ID-Synchronisierung.

## Aktivieren [!DNL Audience Manager]

Zur Aktivierung müssen [!DNL Audience Manager] Sie Folgendes ausführen:

- Aktivieren Sie [!DNL Audience Manager] die [Edge-Konfiguration](../../fundamentals/edge-configuration.md).
- Aktivieren oder deaktivieren Sie Cookie- und URL-Ziele.
- Geben Sie Ihren ID-Synchronisierungs-Container für externe Partnersynchronisierungen an (optional)

## Identitäten synchronisieren

Die Adobe Experience Platform [!DNL Web SDK] unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den [SyncIdentity](../../fundamentals/identity.md) -Befehl zu deklarieren.

Die syncIdentity-Methode verwendet [Identitätsdienst-Namensraum](../../../identity/../identity-service/namespaces.md) , um den Kontext anzugeben, auf den sich eine Identität bezieht. Als [!DNL Audience Manager] Kunde verwenden alle vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifend wird automatisch eine entsprechende Funktion [!DNL Identity Namespace]verwendet. Melden Sie sich zur entsprechenden [!DNL Identity Namespace] Adobe Experience Platform an [!DNL Audience Manager Data Source][!DNL Identities] und navigieren Sie zum entsprechenden Abschnitt.

![Ansicht der Benutzeroberfläche der Namensraum](../../../assets/edge_configuration_identity.png)

Hier können Sie Ihre [!DNL Audience Manager] Datenquelle nach Name suchen. Die syncIdentity-Methode verwendet das Identitätssymbol, um den Namensraum anzugeben.

Jede neue [!DNL Audience Manager] Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identitäts-Namensraum generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identity Namensraum eine entsprechende [!DNL Audience Manager] Datenquelle, beachten Sie jedoch, dass die syncIdentity-Methode nur Namensraum-Identitätssymbole unterstützt.
