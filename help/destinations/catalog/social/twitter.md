---
title: Verbindung von twitter Custom Audiences
description: Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 74c5924406797c30d53f91782e37ac5e953aab94
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---

# [!DNL Twitter Custom Audiences] connection

## Übersicht {#overview}

Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren.

## Voraussetzungen {#prerequisites}

Bevor Sie Ihr [!DNL Twitter Custom Audiences]-Ziel konfigurieren, überprüfen Sie die folgenden Twitter-Voraussetzungen, die Sie erfüllen müssen.

1. Ihr [!DNL Twitter Ads]-Konto muss für Werbung berechtigt sein. Neue [!DNL Twitter Ads]-Konten sind in den ersten 2 Wochen nach ihrer Erstellung nicht für Werbung geeignet.
2. Für Ihr Twitter-Benutzerkonto, für das Sie den Zugriff in [!DNL Twitter Audience Manager] genehmigt haben, muss die Berechtigung *[!DNL Partner Audience Manager]* aktiviert sein.


## Unterstützte Identitäten {#supported-identities}

[!DNL Twitter Custom Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| device_id | IDFA/AdID/Android-ID | Google Advertising ID (GAID) und Apple ID for Advertisers (IDFA) werden in Adobe Experience Platform unterstützt. Ordnen Sie diese Namespaces und/oder Attribute aus Ihrem Quellschema entsprechend im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows zu. |
| email | E-Mail-Adresse(n) für den Benutzer | Bitte ordnen Sie in diesem Feld Ihre E-Mail-Adressen mit normalem Text und Ihre SHA256-Hash-E-Mail-Adressen zu. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. Wenn Sie Ihre Kunden-E-Mail-Adressen vor dem Hochladen in Adobe Experience Platform hash, beachten Sie bitte, dass diese Identitäten mit SHA256 ohne Salz gehasht werden müssen. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den Kennungen, die im Twitter-Ziel für benutzerdefinierte Zielgruppen verwendet werden.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Twitter Custom Audiences]-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Richten Sie Ihre bestehenden Follower und Kunden in Twitter ein und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen in Twitter als [!DNL List Custom Audiences] aktivieren.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre  [!DNL Twitter Ads] Konto-ID. Dies finden Sie in Ihren [!DNL Twitter Ads] -Einstellungen.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) .

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Zusätzliche Ressourcen {#additional-resources}

Stellen Sie beim Zuordnen von Zielgruppensegmenten zu Twitter sicher, dass Sie die folgenden Segmentbenennungsanforderungen erfüllen:

1. Stellen Sie für Menschen lesbare Namen für die Segmentzuordnung bereit. Es wird empfohlen, denselben Namen zu verwenden, den Sie für die Experience Platform-Segmente verwendet haben.
2. Verwenden Sie keine Sonderzeichen (+ &amp; , % : ; @ / = ? $) in den Namen der Segment- und Segmentzuordnung. Wenn der Segmentname Ihrer Experience Platform diese Zeichen enthält, entfernen Sie diese, bevor Sie das Segment einem Twitter-Ziel zuordnen.

Weitere Informationen zu [!DNL List Custom Audiences] in Twitter finden Sie in der [Twitter-Dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
