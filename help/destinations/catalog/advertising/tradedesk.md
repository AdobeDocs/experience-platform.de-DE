---
keywords: Werbung; die Geschäftsstelle; Werbefachgeschäft
title: Verbindung zum Trade Desk
description: Das Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, mit der sie digitale Kampagnen für Zielgruppen und Zielgruppen aus Display-, Video- und mobilen Inventarquellen ausführen können.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 169a7ad1adfa3282bd0503ce277373b654ec57cd
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# [!DNL The Trade Desk] connection

## Übersicht {#overview}

[!DNL The Trade Desk] Das Ziel hilft beim Senden von Profildaten an [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Self-Service-Plattform für Anzeigenkäufer zur Durchführung von Retargeting- und zielgerichteten digitalen Kampagnen für Display-, Video- und mobile Inventarquellen.

So senden Sie Profildaten an [!DNL Trade Desk], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketer möchte ich Segmente verwenden können, die aus [!DNL Trade Desk IDs] oder Geräte-IDs zum Erstellen von Retargeting oder zielgerichteten digitalen Kampagnen für Zielgruppen.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsschalter-ID | Advertiser-ID in der Trade Desk-Plattform |

## Exporttyp {#export-type}

**[!DNL Segment export]** - Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Ziel.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL The Trade Desk] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) Wenden Sie sich in der Vergangenheit (mit Adobe Audience Manager oder anderen Experience Cloud-ID-Diensten) an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL The Trade Desk] -Integrationen in Audience Manager werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL Trade Desk] [!UICONTROL Konto-ID].
* **[!UICONTROL Server-Speicherort]**: Fragen Sie Ihre [!DNL Trade Desk] repräsentativ für den regionalen Server, den Sie verwenden sollten. Diese regionalen Server stehen zur Auswahl:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Nordamerika Osten]**
   * **[!UICONTROL Nordamerika - Westen]**
   * **[!UICONTROL Lateinamerika]**

## Aktivieren von Segmenten für dieses Ziel {#activate}

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

Im [Segmentplan](../../ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie Ihre Segmente manuell ihrer entsprechenden ID oder dem Anzeigenamen in der Zielplattform zuordnen.

Für die Zuordnung von Segmenten empfehlen wir die Verwendung des Platform-Segmentnamens oder einer kürzeren Form davon, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem Platform-Konto übereinstimmen. Alle Werte, die Sie in das Zuordnungsfeld einfügen, werden vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen (Cookie-IDs, [!DNL IDFA], [!DNL GAID]), stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] aggregiert alle Daten in einem einzelnen Segment mit einer Aufschlüsselung auf Geräteebene.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

So überprüfen Sie, ob die Daten erfolgreich nach exportiert wurden [!DNL The Trade Desk] Ziel, überprüfen Sie Ihre [!DNL Trade Desk] -Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
