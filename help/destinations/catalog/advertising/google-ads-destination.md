---
keywords: Google Ads; Google Ads; Google AdWords; Google AdWords; Google AdWords
title: Google Ads-Verbindung
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 15%

---

# [!DNL Google Ads] connection

## Übersicht {#overview}

[!DNL Google Ads], früher als  [!DNL Google AdWords] bezeichnet, ist ein Online-Werbedienst, mit dem Unternehmen Pay-per-Click-Werbung für textbasierte Suchen, grafische Anzeigen,  [!DNL YouTube] Videos und mobile In-App-Anzeigen erstellen können.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die speziell für [!DNL Google Ads]-Ziele gelten:

* Aktivierte Zielgruppen werden programmgesteuert in der Plattform [!DNL Google] erstellt.
* [!DNL Platform] enthält derzeit keine Messmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Google Ads] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

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

### Vorhandenes [!DNL Google Ads]-Konto

>[!IMPORTANT]
>
> [!DNL Google] hat keine neuen  [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern mehr unterstützt. Um die im nächsten Abschnitt beschriebenen Zulassungslisten durchzuführen, müssen Sie über eine bestehende Integration mit [!DNL Google Ads] verfügen. Daher wird für die Verwendung von [!DNL Google Ads] empfohlen, eine [!DNL Google Customer Match] -Integration einzurichten. Weitere Informationen zum Erstellen einer [!DNL Google Customer Match]-Integration finden Sie im Tutorial zum Erstellen einer [[!DNL Google Customer Match]](./google-customer-match.md)-Verbindung.

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ads]-Ziel in Platform einrichten. Stellen Sie sicher, dass die unten beschriebene Zulassungsliste von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Ads]-Ziel in Platform erstellen, müssen Sie sich an [!DNL Google] wenden, damit die Adobe auf die Liste der zulässigen Datenanbieter gesetzt und Ihr Konto zur Zulassungsliste hinzugefügt werden kann. Kontaktieren Sie [!DNL Google] und geben Sie die folgenden Informationen ein:

* **Konto-ID**: Kontokennung der Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID der Adobe bei Google. Kunden-ID: 89690775.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID**: Dies ist Ihre ID mit  [!DNL Google]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID  [!DNL Google Ads]ein. Das Format der Kennung lautet in der Regel 123-456-7890.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

## Exportierte Daten

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Google Ads]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ads]-Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kunden versuchen, das Ziel ohne vorhandenes [!DNL Google Ads]-Konto zu konfigurieren.

[!DNL Google] hat keine neuen  [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern mehr unterstützt. Um die Schritte [allow-list](#allow-listing) durchzuführen, müssen Sie über eine vorhandene Integration mit [!DNL Google Ads] verfügen.

Der empfohlene Ansatz für die Verwendung von [!DNL Google Ads] ist das Einrichten einer [[!DNL Google Customer Match]](google-customer-match.md) -Integration.
