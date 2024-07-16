---
title: Übersicht über die RainFocus-Quelle
description: Erfahren Sie, wie Sie Ereignismanagement- und Analysedaten aus Ihrem RainFocus-Konto auf Experience Platform übertragen können.
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 6%

---

# [!DNL RainFocus]

>[!NOTE]
>
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

[!DNL RainFocus] ist eine Plattform, mit der Sie Ihre Ereignisse bewerben und Ihre Zielgruppen erstellen können. Sie können [!DNL RainFocus] verwenden, um wunderschöne Werbeseiten zu erstellen, die Kampagnenleistung zu verfolgen und Registrierungsumrechnungen zu optimieren.

Verwenden Sie die [!DNL RainFocus]-Quelle in Adobe Experience Platform und Real-time Customer Data Platform, um Ihre Kundendatenprofile automatisch mit den zugehörigen Erlebnisereignissen in Echtzeit anzureichern. Nach der Aktivierung werden Erlebnisereignisse automatisch in Real-Time CDP gestreamt, was eine leistungsstarke Zielgruppensegmentierung, Datenanalyse und Aktivierung der Journey mit nachgelagerten Zielen und Anwendungen wie Customer Journey Analytics und Adobe Journey Optimizer ermöglicht.

>[!IMPORTANT]
>
>Diese Quell-Connector- und Dokumentationsseite wird vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an clientcare<span>@rainfocus.com oder besuchen Sie das [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Voraussetzungen

Sie müssen die folgenden Voraussetzungen erfüllen, bevor Sie die [!DNL RainFocus] -Integration auf dem Experience Platform aktivieren können:

[Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe hat vor kurzem die Einstellung von JWT-Token zugunsten von OAuth angekündigt. Um dieser Änderung Rechnung zu tragen, wird die [!DNL RainFocus]-Quelle in naher Zukunft zu OAuth migriert.

### Sammeln erforderlicher Anmeldeinformationen

Um [!DNL RainFocus] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften in [!DNL RainFocus] angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Die Client-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Client-Geheimnis | Das Client-Geheimnis kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Technische Konto-ID | Die technische Konto-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisations-ID | Die Organisations-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Erstellen eines XDM-Schemas und Definieren des Identitätsfelds {#create-an-xdm-schema-and-define-the-identity-field}

Um die Erlebnisereignisse von [!DNL RainFocus] im Experience Platform zu speichern, müssen Sie ein Experience-Datenmodell (XDM)-Schema erstellen, um einen Datensatz zu beschreiben, in dem die möglichen von [!DNL RainFocus] gesendeten Felder und Datentypen gespeichert werden können.

[!DNL RainFocus] empfiehlt die folgenden Felder, die alle standardmäßig gesendeten möglichen Daten abdecken.

Außerdem werden die folgenden Feldergruppen empfohlen (mit Präfix gekennzeichnet):

* Teilnehmer
* Aussteller
* Lead
* Session
* SessionTime

**Das Schema sollte die folgenden Felder enthalten:**

| Feld | Typ | Beispiel | Beschreibung |
| --- | --- | --- | --- |
| `attendee.registered` | Zeichenfolge | Ja | Eine Markierung, die bestimmt, ob der Teilnehmer als registriert gilt. |
| `attendee.attendeeId` | Zeichenfolge | 1619119968857001fvLB | Die Teilnehmer-ID in [!DNL RainFocus]. |
| `attendee.externalId` | Zeichenfolge | 1666809456617001wyPj | Die von einer Organisation angegebene externe ID. |
| `attendee.clientId` | Zeichenfolge | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | Die Teilnehmer-SSO-Client-ID. |
| `attendee.email` | Zeichenfolge | user<span>@company.com | Die E-Mail-Adresse des Teilnehmers. |
| `transmissionId` | Zeichenfolge | 1680309557133001YHhz | Eine eindeutige Kennung, die für Daten-Push verwendet wird. |
| `eventType` | Zeichenfolge | SessionScheduled | Der Name des Teilnehmer-Erlebnisereignisses. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000Z | Der Zeitstempel der Daten-Push-Benachrichtigung. |
| `event.name` | Zeichenfolge | Adobe Summit 2023 | Der Name des Ereignisses, bei dem eine Übertragung stattgefunden hat. |
| `exhibitor.exhibitorId` | Zeichenfolge | 1680309557133001YHhz | Die [!DNL RainFocus]-Kennung des Ausstellers. |
| `exhibitor.externalId` | Zeichenfolge | 1666809514105001lSJN | Die Kennung für den Aussteller im Kundensystem. |
| `exhibitor.name` | Zeichenfolge | IBM | Der Name des Ausstellers. |
| `lead.leadId` | Zeichenfolge | 1666809456617001wyPj | Die [!DNL RainFocus]-Kennung für den Lead. |
| `lead.note` | Zeichenfolge | | |
| `session.sessionId` | Zeichenfolge | 1666809373585001t4aV | Die [!DNL RainFocus]-Kennung für die Sitzung. |
| `session.externalId` | Zeichenfolge | 1666809456617001wyPj | Die Kennung für die Sitzung im Client-System. |
| `session.code` | Zeichenfolge | GS3 | Der Code für die Sitzung. |
| `session.title` | Zeichenfolge | Inspiration - Keynote | Der Titel der Sitzung. |
| `session.length` | Ganzzahl | 90 | Die Dauer der Sitzung. |
| `sessiontime.sessiontimeId` | Zeichenfolge | 1673033149739001OJLZ | Die [!DNL RainFocus] -Kennung für die Sitzungszeit. |
| `sessiontime.startTime` | Zeichenfolge | 22.03.2023 10:00:00 | Die Startzeit der Sitzung. |
| `sessiontime.endTime` | Zeichenfolge | 22.03.2023 10:00:00 | Die Endzeit der Sitzung. |
| `sessiontime.room` | Zeichenfolge | B32 | Der für die Sitzung verwendete Raum. |

{style="table-layout:auto"}

Um Ihr Schema für [!DNL RainFocus] -Daten zu erstellen, lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie ein Schema mit APIs oder der Benutzeroberfläche erstellen.

* [Erstellen des Schemas mithilfe der Benutzeroberfläche](../../../xdm/tutorials/create-schema-ui.md)
* [Erstellen des Schemas mithilfe der API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Das Schema muss die **XDM ExperienceEvent-Klasse** erweitern.
>* Sie müssen sicherstellen, dass das Schema eine **primäre Identität** enthält und **für Profil** aktiviert ist. Weitere Informationen finden Sie im Handbuch zum Definieren von Identitätsfeldern in der Benutzeroberfläche ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)[
>* Sie können die Beispielidentität (E-Mail) durch eine andere geeignete Kennung wie eine SHA256-E-Mail oder ECID ersetzen.

### Erstellen eines Integrationsprofils in RainFocus {#create-an-integration-profile-in-rainfocus}

Sobald Ihr Dienstkonto und Ihr XDM-Schema fertig sind, können Sie jetzt die [!DNL Integration Profile] über die [!DNL RainFocus]-Plattform aktivieren. Der [!DNL Integration Profile] ist für das Streaming von Daten an Experience Platform verantwortlich.

Melden Sie sich bei [[!DNL RainFocus] platform](https://app.rainfocus.com) an. Wählen Sie im primären Navigationsbereich **[!DNL Libraries]** und dann **[!DNL Integration Profiles]** aus.

![Die RainFocus-Benutzeroberfläche mit ausgewählten Bibliotheken und Integrationsprofilen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Um ein neues Profil zu erstellen, wählen Sie das Symbol **(`+`)** aus. Wählen Sie als Nächstes **Adobe Real-time Customer Data Platform** und dann **OK** aus.

![Das Fenster &quot;Integrationsprofil erstellen&quot;in der RainFocus-Benutzeroberfläche.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Geben Sie als Nächstes die Anmeldeinformationen ein, die Sie im Adobe Developer Portal-Projekt abgerufen haben:

* **Client ID** (Client-ID)
* **Client Secret** (Client-Geheimnis)
* **Technische Konto-ID**
* **Organisations-ID**

Nachdem die Anmeldeinformationen angegeben wurden, wählen Sie **[!DNL Save]** aus. Jetzt sollte das neue [!DNL Integration Profile] im Dashboard [!DNL RainFocus] aufgeführt sein.

Wählen Sie die soeben erstellte [!DNL Integration Profile] aus, um eine Liste mit vordefinierten **Push-Typen** anzuzeigen, die bereits konfiguriert sind. Dies sind die [Erlebnisereignisse](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=de), die bei ihrem Auftreten an Experience Platform gesendet werden.

![Eine Liste vordefinierter Push-Typen im Dashboard &quot;RainFocus&quot;.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Um eine Kopie der JSON-Beispielnutzlast abzurufen, wählen Sie **[!DNL Sample JSON Payload]** aus. Markieren und kopieren Sie anschließend die JSON-Beispielnutzlast und speichern Sie sie in einer neuen Datei mit der Erweiterung .json **.** Dies wird später im Experience Platform für [Zuordnungskonfigurationen](../../tutorials/ui/create/analytics/rainfocus.md#mapping) verwendet.

![Eine JSON-Beispielnutzlast im Dashboard &quot;RainFocus&quot;.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Die Einrichtung ist noch nicht abgeschlossen**: Nachdem Ihr Datenfluss erstellt wurde, müssen Sie zum Dashboard [!DNL RainFocus] zurückkehren, um Ihr [!DNL Integration Profile] abzuschließen, indem Sie Ihre **Streaming-Endpunkt-URL** und Ihre **Datenfluss-ID** angeben.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL RainFocus]-Konto an Experience Platform zu streamen. Sie können jetzt mit dem Handbuch zum Verbinden von [1}mit dem Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/analytics/rainfocus.md) fortfahren. [!DNL RainFocus] 
