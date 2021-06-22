---
keywords: 'Werbung; Schläuche; '
title: Microsoft Bing-Verbindung
description: Mit dem Microsoft Bing-Verbindungsziel können Sie digitale Kampagnen für Retargeting und Zielgruppen-Targeting in Microsoft Display Advertising ausführen.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 5%

---

# [!DNL Microsoft Bing] connection  {#bing-destination}

## Übersicht {#overview}

Mit dem [!DNL Microsoft Bing]-Ziel können Sie Profildaten an [!DNL Microsoft Display Advertising] senden.

Um Profildaten an [!DNL Microsoft Bing] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Anwendungsbeispiele {#use-cases}

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

## Mit Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL Microsoft Bing] und klicken Sie auf **[!UICONTROL Konfigurieren]**.

![Microsoft Bing-Ziel konfigurieren](../../assets/catalog/advertising/bing/configure.png)

Wenn bereits eine Verbindung mit diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Activate]** und **[!UICONTROL Configure]** finden Sie im Abschnitt [Catalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Ziel-Workspace.

![Microsoft Bing-Ziel aktivieren](../../assets/catalog/advertising/bing/activate.png)

## Authentifizierungsschritt {#authentication}

Im Schritt **[!UICONTROL Authentifizierung]** müssen Sie die Details der Zielverbindung eingeben:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr  [!DNL Bing Ads CID].
* **[!UICONTROL Marketing-Aktion]**: Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Data Governance in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Informationen zu den einzelnen von der Adobe definierten Marketing-Aktionen finden Sie unter [Übersicht über Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

![Microsoft Bing Destination Authentication](../../assets/catalog/advertising/bing/authentication.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**. Ihr Ziel wird jetzt erstellt. Sie können auf [!UICONTROL Speichern und beenden] klicken, wenn Sie Segmente später aktivieren möchten, oder Sie können auf [!UICONTROL Weiter] klicken, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Segmente aktivieren](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md#select-attributes).

Im Schritt [Segment schedule](../../ui/activate-destinations.md#segment-schedule) müssen Sie Ihre Segmente manuell ihrer entsprechenden ID oder dem Anzeigenamen im Ziel zuordnen.

Für die Zuordnung von Segmenten empfehlen wir, den Segmentnamen [!DNL Platform] oder eine kürzere Form zu verwenden, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der ID in Ihrem [!DNL Platform]-Konto übereinstimmen. Alle Werte, die Sie in das Zuordnungsfeld einfügen, werden vom Ziel übernommen.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Microsoft Bing]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Bing Ads]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
