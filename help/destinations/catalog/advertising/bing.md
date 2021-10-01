---
keywords: 'Werbung; Schläuche; '
title: Microsoft Bing-Verbindung
description: Mit dem Microsoft Bing-Verbindungsziel können Sie digitale Kampagnen für Retargeting und Zielgruppen-Targeting in Microsoft Display Advertising ausführen.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Übersicht {#overview}

Mit dem [!DNL Microsoft Bing]-Ziel können Sie Profildaten an [!DNL Microsoft Display Advertising] senden.

Um Profildaten an [!DNL Microsoft Bing] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketer möchte ich in der Lage sein, aus [!DNL Microsoft Advertising IDs] erstellte Segmente zu verwenden, um Benutzer über Display-Werbung über [!DNL Microsoft Advertising]-Kanäle hinweg anzusprechen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Microsoft Bing] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung |
|---|---|
| MAID | Microsoft Advertising ID |

## Exporttyp {#export-type}

**[!DNL Segment Export]** - Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das  [!DNL Microsoft Bing] Ziel.

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL Microsoft Bing] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst noch nicht aktiviert haben (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL Microsoft Bing] -Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

Beim Konfigurieren des Ziels müssen Sie die folgenden Informationen angeben:

* [!UICONTROL Konto-ID]: Dies ist Ihr  [!DNL Bing Ads CID]ganzzahliges Format.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr  [!DNL Bing Ads CID].

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

Im Schritt [Segment schedule](../../ui/activate-segment-streaming-destinations.md#scheduling) müssen Sie Ihre Segmente manuell ihrer entsprechenden ID oder dem Anzeigenamen im Ziel zuordnen.

Für die Zuordnung von Segmenten empfehlen wir, den Segmentnamen [!DNL Platform] oder eine kürzere Form zu verwenden, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der ID in Ihrem [!DNL Platform]-Konto übereinstimmen. Alle Werte, die Sie in das Zuordnungsfeld einfügen, werden vom Ziel übernommen.

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Microsoft Bing]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Bing Ads]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
