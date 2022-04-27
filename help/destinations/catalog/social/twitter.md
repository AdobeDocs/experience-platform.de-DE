---
title: Verbindung von twitter Custom Audiences
description: Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 20%

---

# [!DNL Twitter Custom Audiences]-Verbindung

## Übersicht {#overview}

Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren.

## Voraussetzungen {#prerequisites}

Vor der Konfiguration [!DNL Twitter Custom Audiences] überprüfen Sie unbedingt die folgenden Twitter-Voraussetzungen, die Sie erfüllen müssen.

1. Ihre [!DNL Twitter Ads] für Werbung zugelassen sein. Neu [!DNL Twitter Ads] -Konten sind in den ersten zwei Wochen nach ihrer Erstellung nicht für Werbung geeignet.
2. Ihr Twitter-Benutzerkonto, für das Sie den Zugriff in genehmigt haben [!DNL Twitter Audience Manager] muss über *[!DNL Partner Audience Manager]* -Berechtigung aktiviert ist.

## Unterstützte Identitäten {#supported-identities}

[!DNL Twitter Custom Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| device_id | IDFA/AdID/Android-ID | Google Advertising ID (GAID) und Apple ID for Advertisers (IDFA) werden in Adobe Experience Platform unterstützt. Ordnen Sie diese Namespaces und/oder Attribute aus Ihrem Quellschema entsprechend im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows. |
| email | E-Mail-Adresse(n) für den Benutzer | Bitte ordnen Sie in diesem Feld Ihre E-Mail-Adressen mit normalem Text und Ihre SHA256-Hash-E-Mail-Adressen zu. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. Wenn Sie Ihre Kunden-E-Mail-Adressen vor dem Hochladen in Adobe Experience Platform hash, beachten Sie bitte, dass diese Identitäten mit SHA256 ohne Salz gehasht werden müssen. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den Kennungen, die im Twitter-Ziel für benutzerdefinierte Zielgruppen verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Twitter Custom Audiences] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Richten Sie Ihre bestehenden Follower und Kunden in Twitter ein und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform as erstellten Zielgruppen aktivieren. [!DNL List Custom Audiences] in Twitter.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL Twitter Ads] Konto-ID. Diese finden Sie in Ihrer [!DNL Twitter Ads] -Einstellungen.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Weitere Ressourcen {#additional-resources}

Stellen Sie beim Zuordnen von Zielgruppensegmenten zu Twitter sicher, dass Sie die folgenden Segmentbenennungsanforderungen erfüllen:

1. Stellen Sie für Menschen lesbare Namen für die Segmentzuordnung bereit. Es wird empfohlen, denselben Namen zu verwenden, den Sie für die Experience Platform-Segmente verwendet haben.
2. Verwenden Sie keine Sonderzeichen (+ &amp; , % : ; @ / = ? $) in den Namen der Segment- und Segmentzuordnung. Wenn der Segmentname Ihrer Experience Platform diese Zeichen enthält, entfernen Sie diese, bevor Sie das Segment einem Twitter-Ziel zuordnen.

Weitere Informationen [!DNL List Custom Audiences] in Twitter finden Sie im Abschnitt [Twitter-Dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
