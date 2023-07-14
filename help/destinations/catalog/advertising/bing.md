---
keywords: Werbung; Schläuche;
title: Microsoft Bing-Verbindung
description: Mit dem Microsoft Bing-Verbindungsziel können Sie digitale Kampagnen für Retargeting und Zielgruppen-Targeting in Microsoft Display Advertising durchführen.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 45%

---

# [!DNL Microsoft Bing]-Verbindung {#bing-destination}

## Übersicht {#overview}

Die [!DNL Microsoft Bing] Das Ziel hilft beim Senden von Profildaten an [!DNL Microsoft Display Advertising].

So senden Sie Profildaten an [!DNL Microsoft Bing], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketer möchte ich in der Lage sein, aus [!DNL Microsoft Advertising IDs] , um Benutzer über Display-Werbung anzusprechen. [!DNL Microsoft Advertising] Kanäle.

## Unterstützte Identitäten {#supported-identities}

[!DNL Microsoft Bing] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| MAID | Microsoft Advertising-ID |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Alle Ziele unterstützen die Aktivierung von Zielgruppen, die durch die Experience Platform generiert wurden [Segmentierungsdienst](../../../segmentation/home.md).

Darüber hinaus unterstützt dieses Ziel auch die Aktivierung der in der folgenden Tabelle beschriebenen Zielgruppen.

| Zielgruppentyp | Beschreibung |
---------|----------|
| Benutzerdefinierte Uploads | Zielgruppen, die aus CSV-Dateien in Experience Platform aufgenommen werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

**[!DNL Audience Export]** - Sie exportieren alle Mitglieder einer Audience in die [!DNL Microsoft Bing] Ziel.

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe in die [!DNL Microsoft Bing] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform basierend auf der Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Microsoft Bing] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) Wenden Sie sich in der Vergangenheit (mit Adobe Audience Manager oder anderen Experience Cloud-ID-Diensten) an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor schon [!DNL Microsoft Bing]-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

Beim Konfigurieren des Ziels müssen Sie die folgenden Informationen angeben:

* [!UICONTROL Konto-ID]: ist [!DNL Bing Ads CID], im ganzzahligen Format.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL Bing Ads Customer ID] (CID). Ihre CID ist eine Ganzzahl, die bei der Anmeldung in der URL zu finden ist. [!DNL Microsoft Advertising].

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Zuordnungs-ID"
>abstract="Geben Sie die numerische Bing-Zielgruppen-ID ein, der Sie das ausgewählte Segment zuordnen möchten. Wenn die Variable [!UICONTROL Zuordnungs-ID] entspricht keiner Zielgruppen-ID im Bing-Ziel, werden Ihnen die erwarteten Zielgruppendaten in Ihrem Bing-Konto nicht angezeigt."

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Zielgruppenexport-Ziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

Im [Zielgruppenplanung](../../ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie den Zielgruppennamen manuell im [!UICONTROL Zuordnungs-ID] -Feld. Dadurch wird sichergestellt, dass Zielgruppen-Metadaten korrekt an [!DNL Bing].

![UI-Bild, das den Bildschirm &quot;Zielgruppenplanung&quot;mit einem Beispiel für die Zuordnung des Zielgruppennamen zur Bing-Mapping-ID anzeigt.](../../assets/catalog/advertising/bing/mapping-id.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Microsoft Bing]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Bing Ads]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
