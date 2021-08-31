---
keywords: DoubleClick Bid Manager;DoubleClick Bid Manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360-Verbindung
description: Display & Video 360, früher als DoubleClick Bid Manager bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 38%

---

# [!DNL Google Display & Video 360] connection

## Übersicht {#overview}

[!DNL Display & Video 360], früher als bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.[!DNL DoubleClick Bid Manager]

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die speziell für [!DNL Google Display & Video 360]-Ziele gelten:

* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* [!DNL Platform] enthält derzeit keine Messmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Display &amp; Video 360 erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in der Vergangenheit nicht aktiviert hatten (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um die ID-Synchronisierung zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

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

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung

>[!NOTE]
>
>Die Zulassungsauflistung ist vor der Einrichtung Ihres ersten [!DNL Google Display & Video 360]-Ziels in Platform obligatorisch. Stellen Sie sicher, dass der unten beschriebene Genehmigungsprozess von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Display & Video 360]-Ziel in Platform erstellen, müssen Sie sich an Google wenden und darum bitten, die Adobe auf die Liste der zulässigen Datenanbieter zu setzen und Ihr Konto der Zulassungsliste hinzuzufügen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Konto-ID**: Kontokennung der Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID der Adobe bei Google. Kunden-ID: 89690775.
* **Ihr Kontotyp**: Verwenden Sie **[!DNL Invite advertiser]**, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen, oder verwenden Sie **[!DNL Invite partner]**, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `Invite Advertiser`, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
   * Verwenden Sie `Invite Partner`, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
* **[!UICONTROL Kontokennung]**: Geben Sie Ihre **[!DNL Invite partner]**- oder **[!DNL Invite advertiser]**-Kontokennung bei Google ein. In der Regel ist dies eine sechsstellige oder siebenstellige ID.

>[!NOTE]
>
>Wenden Sie sich beim Einrichten eines [!DNL Google Display & Video 360]-Ziels an Ihren [!DNL Google Account Manager]- oder Kundenbetreuer, um zu erfahren, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

## Exportierte Daten

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Google Display & Video 360]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Display & Video 360]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#prerequisites) nicht erfüllen. Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf die Zulassungsliste gesetzt ist.