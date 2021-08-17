---
keywords: Werbung; die Geschäftsstelle; Werbefachgeschäft
title: Verbindung zum Trade Desk
description: Das Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, mit der sie digitale Kampagnen für Zielgruppen und Zielgruppen aus Display-, Video- und mobilen Inventarquellen ausführen können.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---

# [!DNL The Trade Desk] connection

## Übersicht {#overview}

[!DNL The Trade Desk] Mit dem Ziel können Sie Profildaten an senden  [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Self-Service-Plattform für Anzeigenkäufer zur Durchführung von Retargeting- und zielgerichteten digitalen Kampagnen für Display-, Video- und mobile Inventarquellen.

Um Profildaten an [!DNL Trade Desk] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsbeispiele {#use-cases}

Als Marketer möchte ich Segmente verwenden können, die aus [!DNL Trade Desk IDs] oder Geräte-IDs erstellt wurden, um Retargeting oder zielgruppenorientierte digitale Kampagnen zu erstellen.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsschalter-ID | Advertiser-ID in der Trade Desk-Plattform |

## Exporttyp {#export-type}

**[!DNL Segment export]** - Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Ziel.

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL The Trade Desk] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst noch nicht aktiviert haben (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL The Trade Desk] -Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre  [!DNL Trade Desk] [!UICONTROL Konto-ID].
* **[!UICONTROL Server-Speicherort]**: Fragen Sie Ihren  [!DNL Trade Desk] Kundenbetreuer, welchen regionalen Server Sie verwenden sollten. Diese regionalen Server stehen zur Auswahl:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Nordamerika Osten]**
   * **[!UICONTROL Nordamerika - Westen]**
   * **[!UICONTROL Lateinamerika]**

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für Ziele finden Sie unter [Aktivieren von Profilen und Segmenten für ein Ziel](../../ui/activate-destinations.md) .

Im Schritt [Segment schedule](../../ui/activate-destinations.md#segment-schedule) müssen Sie Ihre Segmente manuell ihrer entsprechenden ID oder dem Anzeigenamen in der Zielplattform zuordnen.

Für die Zuordnung von Segmenten empfehlen wir die Verwendung des Platform-Segmentnamens oder einer kürzeren Form davon, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem Platform-Konto übereinstimmen. Alle Werte, die Sie in das Zuordnungsfeld einfügen, werden vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen (Cookie-IDs, [!DNL IDFA], [!DNL GAID]) verwenden, stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] aggregiert alle Daten in einem einzelnen Segment mit einer Aufschlüsselung auf Geräteebene.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL The Trade Desk]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Trade Desk]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
