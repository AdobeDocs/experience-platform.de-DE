---
keywords: Google Ad Manager;Google Ad Manager;DoubleClick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager;Google Ad Manager; DFP
title: Google Ad Manager-Verbindung
description: Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 23%

---

# [!DNL Google Ad Manager] connection

## Übersicht {#overview}

[!DNL Google Ad Manager], früher als  [!DNL DoubleClick for Publishers] (DFP) oder  [!DNL DoubleClick AdX], ist eine Adserving-Plattform von , über  [!DNL Google] die Herausgeber die Möglichkeit erhalten, die Anzeige von Werbung auf ihren Websites, über Videos und in mobilen Apps zu verwalten.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die speziell für [!DNL Google Ad Manager]-Ziele gelten:

* Aktivierte Zielgruppen werden programmgesteuert in der Plattform [!DNL Google] erstellt.
* [!DNL Platform] enthält derzeit keine Messmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), auch als  [!DNL Device ID] bezeichnet. Eine numerische, 38-stellige Geräte-ID, die der Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), um Benutzer in Kalifornien als Ziel festzulegen, und die Google Cookie-ID für alle anderen Benutzer. |
| [!DNL Google] Cookie-ID | [!DNL Google] Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzer außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising ID. Diese ID identifiziert Geräte mit Windows 10 eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Google-Ziel.

## Voraussetzungen

Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL Google] -Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager]-Ziel in Platform einrichten. Stellen Sie sicher, dass die unten beschriebene Zulassungsliste von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Ad Manager]-Ziel in Platform erstellen, müssen Sie sich an [!DNL Google] wenden, damit die Adobe auf die Liste der zulässigen Datenanbieter gesetzt und Ihr Konto zur Zulassungsliste hinzugefügt werden kann. Kontaktieren Sie [!DNL Google] und geben Sie die folgenden Informationen ein:

* **Konto-ID**: Kontokennung der Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID der Adobe bei Google. Kunden-ID: 89690775.
* **Netzwerkkennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `DFP by Google` für for Publishers.[!DNL DoubleClick]
   * `AdX buyer` für [!DNL Google AdX] verwenden
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID  [!DNL Google]ein. Dies kann Ihre Netzwerkkennung oder Ihre Zielgruppenverknüpfungskennung sein. Normalerweise ist dies eine achtstellige Kennung.

>[!NOTE]
>
>Wenden Sie sich beim Einrichten eines [!DNL Google Ad Manager]-Ziels an Ihren [!DNL Google Account Manager]- oder Kundenbetreuer, um zu erfahren, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

## Exportierte Daten

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Google Ad Manager]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.
