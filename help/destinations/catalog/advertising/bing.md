---
keywords: Werbung; Bierwerbung;
title: Microsoft Bing-Verbindung
description: Mit dem Microsoft Bing-Verbindungsziel können Sie im gesamten Microsoft Advertising-Netzwerk, einschließlich Display-Werbung, Suche und nativ, zielgruppenorientierte digitale Kampagnen durchführen.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 52%

---

# [!DNL Microsoft Bing]-Verbindung {#bing-destination}

## Übersicht {#overview}

Verwenden Sie die [!DNL Microsoft Bing] Ziel zum Senden von Profildaten an die gesamte [!DNL Microsoft Advertising Network], einschließlich [!DNL Display Advertising], [!DNL Search], und [!DNL Native].

Die [!DNL Microsoft Bing] Ziel erstellt *[!DNL Custom Audiences]* in Microsoft. Diese sind sowohl im [!DNL Microsoft Search Network] und [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]), wie im Abschnitt [Dokumentation zu Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

So senden Sie Profildaten an [!DNL Microsoft Bing], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketer möchte ich in der Lage sein, aus [!DNL Microsoft Advertising IDs] , um Benutzer über Display- oder Suchwerbung gezielt anzusprechen [!DNL Microsoft Advertising] Kanäle.

## Unterstützte Identitäten {#supported-identities}

[!DNL Microsoft Bing] unterstützt die Aktivierung von Zielgruppen basierend auf den Identitäten, die in der folgenden Tabelle angezeigt werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Identität | Beschreibung |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

**[!DNL Audience Export]** - Sie exportieren alle Mitglieder einer Audience in die [!DNL Microsoft Bing] Ziel.

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe in die [!DNL Microsoft Bing] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Microsoft Bing] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) Wenden Sie sich in der Vergangenheit (mit Adobe Audience Manager oder anderen Anwendungen) an die Adobe Consulting- oder Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor schon [!DNL Microsoft Bing]-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

Beim Konfigurieren des Ziels müssen Sie die folgenden Informationen angeben:

* [!UICONTROL Konto-ID]: Dies ist Ihr [!DNL Bing Ads CID], im ganzzahligen Format.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Ausfüllen der Zieldetails {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr [!DNL Bing Ads Customer ID] (CID). Ihre CID ist eine Ganzzahl, die bei der Anmeldung in der URL zu finden ist [!DNL Microsoft Advertising].

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Zuordnungs-ID"
>abstract="Geben Sie die numerische Bing-Zielgruppen-ID ein, der Sie das ausgewählte Segment zuordnen möchten. Wenn die angegebene [!UICONTROL Zuordnungs-ID] mit keiner Zielgruppen-ID im Bing-Ziel übereinstimmt, werden die erwarteten Zielgruppendaten in Ihrem Bing-Konto nicht angezeigt."

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im [Zielgruppenplanung](../../ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie den Zielgruppennamen manuell im [!UICONTROL Zuordnungs-ID] -Feld. Dadurch wird sichergestellt, dass Zielgruppen-Metadaten korrekt an [!DNL Bing].

![UI-Bild, das den Bildschirm &quot;Zielgruppenplanung&quot;mit einem Beispiel für die Zuordnung des Zielgruppennamen zur Bing-Mapping-ID anzeigt.](../../assets/catalog/advertising/bing/mapping-id.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Microsoft Bing]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Bing Ads]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
