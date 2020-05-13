---
title: Senden von Daten an Adobe Audience Manager
seo-title: Senden von Daten an Adobe Audience Manager mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Audience Manager gesendet werden
seo-description: Erfahren Sie, wie Daten mit dem Experience Platform Web SDK an Adobe Audience Manager gesendet werden
translation-type: tm+mt
source-git-commit: dfe9ea2889b3ba2e74f8b10296bfb2d123ad9d57
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 7%

---


# (Beta) Audience Manager im Experience Platform Edge Network

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das Adobe Experience Platform Web SDK ist in Adobe Audience Manager integriert und unterstützt das Senden und Empfangen von Daten von Audience Manager, Cookie- und URL-Zielen und ID-Synchronisierung.

## Aktivieren von Audience Manager

Zur Aktivierung von Audience Manager müssen Sie folgende Schritte ausführen:

- Aktivieren Sie Audience Manager in Ihrer [Edge-Konfiguration](../../fundamentals/edge-configuration.md).
- Aktivieren oder deaktivieren Sie Cookie- und URL-Ziele.
- Geben Sie Ihren ID-Synchronisierungs-Container für externe Partnersynchronisierungen an (optional)

## Identitäten synchronisieren

Das Adobe Experience Platform Web SDK unterstützt die Möglichkeit, Kunden-IDs und deren Authentifizierungsstatus über den Befehl [SyncIdentity](../../fundamentals/identity.md) zu deklarieren.

Die syncIdentity-Methode verwendet [Identitätsdienst-Namensraum](../../../identity/../identity-service/namespaces.md) , um den Kontext anzugeben, auf den sich eine Identität bezieht. Als Audience Manager-Kunde verwenden Sie alle vorhandenen Data Sources, die den ID-Typ verwenden: Geräteübergreifend wird automatisch ein Identitäts-Namensraum verwendet. Um den entsprechenden Identitäts-Namensraum für Ihre Audience Manager-Datenquelle zu finden, melden Sie sich bei der Adobe Experience Platform an und navigieren Sie zum Identitätsabschnitt.

![Ansicht der Benutzeroberfläche der Namensraum](../../../assets/edge_configuration_identity.png)

Hier können Sie nach Ihrer Audience Manager-Datenquelle anhand des Namens suchen. Die syncIdentity-Methode verwendet das Identitätssymbol, um den Namensraum anzugeben.

Jede neue Audience Manager-Datenquelle, die den ID-Typ verwendet: Geräteübergreifend wird ein entsprechender Identitäts-Namensraum generiert. Datenquellen-ID-Typen Cookie und Geräte-Advertising-ID werden derzeit nicht unterstützt. Darüber hinaus generiert jeder in Adobe Experience Platform erstellte Identity Namensraum eine entsprechende Audience Manager-Datenquelle, beachten Sie jedoch, dass die syncIdentity-Methode nur Namensraum-Identitätssymbole unterstützt.
