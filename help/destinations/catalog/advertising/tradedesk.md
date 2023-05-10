---
keywords: Werbung; die Geschäftsstelle; Werbefachgeschäft
title: Verbindung mit The Trade Desk
description: Das Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, mit der sie digitale Kampagnen für Zielgruppen und Zielgruppen aus Display-, Video- und mobilen Inventarquellen ausführen können.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 51%

---

# [!DNL The Trade Desk]-Verbindung

## Übersicht {#overview}

[!DNL The Trade Desk] Das Ziel hilft beim Senden von Profildaten an [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Self-Service-Plattform für Anzeigenkäufer zur Durchführung von Retargeting- und zielgerichteten digitalen Kampagnen für Display-, Video- und mobile Inventarquellen.

So senden Sie Profildaten an [!DNL Trade Desk], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketer möchte ich Segmente verwenden können, die aus [!DNL Trade Desk IDs] oder Geräte-IDs zum Erstellen von Retargeting oder zielgerichteten digitalen Kampagnen für Zielgruppen.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsschalter-ID | Advertiser-ID in der Trade Desk-Plattform |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL The Trade Desk] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) Wenden Sie sich in der Vergangenheit (mit Adobe Audience Manager oder anderen Experience Cloud-ID-Diensten) an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor schon [!DNL The Trade Desk]-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL Trade Desk] [!UICONTROL Konto-ID].
* **[!UICONTROL Server-Speicherort]**: Fragen Sie Ihre [!DNL Trade Desk] repräsentativ für den regionalen Server, den Sie verwenden sollten. Diese regionalen Server stehen zur Auswahl:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Nordamerika Osten]**
   * **[!UICONTROL Nordamerika - Westen]**
   * **[!UICONTROL Lateinamerika]**

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md).

Im [Segmentplan](../../ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie Ihre Segmente manuell ihrer entsprechenden ID oder dem Anzeigenamen in der Zielplattform zuordnen.

Für die Zuordnung von Segmenten empfehlen wir die Verwendung des Platform-Segmentnamens oder einer kürzeren Form davon, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem Platform-Konto übereinstimmen. Alle Werte, die Sie in das Zuordnungsfeld einfügen, werden vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen (Cookie-IDs, [!DNL IDFA], [!DNL GAID]), stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] aggregiert alle Daten in einem einzelnen Segment mit einer Aufschlüsselung auf Geräteebene.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

So überprüfen Sie, ob die Daten erfolgreich nach exportiert wurden [!DNL The Trade Desk] Ziel, überprüfen Sie Ihre [!DNL Trade Desk] -Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
