---
keywords: Google Ad Manager;Google Ad Manager;DoubleClick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager; DFP
title: Google Ad Manager-Verbindung
description: Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 26%

---

# [!DNL Google Ad Manager]-Verbindung

## Übersicht {#overview}

[!DNL Google Ad Manager], früher bekannt als [!DNL DoubleClick for Publishers] (DFP) oder [!DNL DoubleClick AdX], ist eine Adserving-Plattform von [!DNL Google] , die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in mobilen Apps zu verwalten.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für [!DNL Google Ad Manager] Ziele:

* Aktivierte Zielgruppen werden programmgesteuert im [!DNL Google] Plattform.
* [!DNL Platform] enthält derzeit keine Messmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die der Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) , um Benutzer in Kalifornien als Ziel auszuwählen, und die Google-Cookie-ID für alle anderen Benutzer. |
| [!DNL Google] Cookie-ID | [!DNL Google] Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzer außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte mit Windows 10 eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) Wenden Sie sich in der Vergangenheit (mit Audience Manager oder anderen Experience Cloud-ID-Diensten) an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL Google] -Integrationen in Audience Manager werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsliste ist vor der Einrichtung der ersten [!DNL Google Ad Manager] Ziel in Platform. Vergewissern Sie sich, dass die unten beschriebene Zulassungsliste durch [!DNL Google] vor dem Erstellen eines Ziels.

Vor der Erstellung [!DNL Google Ad Manager] Ziel in Platform müssen Sie [!DNL Google] , damit die Adobe in die Liste der zugelassenen Datenanbieter aufgenommen und Ihr Konto zur Zulassungsliste hinzugefügt werden kann. Kontakt [!DNL Google] und geben Sie die folgenden Informationen an:

* **Konto-ID**: Kontokennung der Adobe mit Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID von Adobe mit Google. Kunden-ID: 89690775.
* **Netzwerkkennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `DFP by Google` für for Publishers.[!DNL DoubleClick]
   * Verwendung `AdX buyer` für [!DNL Google AdX]
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID mit [!DNL Google]. Dies kann Ihre Netzwerkkennung oder Ihre Zielgruppenverknüpfungskennung sein. Normalerweise ist dies eine achtstellige Kennung.

>[!NOTE]
>
>Beim Einrichten einer [!DNL Google Ad Manager] Ziel, arbeiten Sie bitte mit Ihrem [!DNL Google Account Manager] oder dem Kundenbetreuer der Adobe, um zu verstehen, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

So überprüfen Sie, ob die Daten erfolgreich in die [!DNL Google Ad Manager] Ziel, überprüfen Sie Ihre [!DNL Google Ad Manager] -Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
