---
title: Übersicht über die RainFocus-Quelle
description: Erfahren Sie, wie Sie Ereignismanagement- und Analysedaten aus Ihrem RainFocus-Konto in die Experience Platform übertragen können.
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
source-git-commit: f3d70e986148d39429f394a60d12686617e3fd3d
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 8%

---

# [!DNL RainFocus]

>[!NOTE]
>
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

[!DNL RainFocus] ist eine Plattform, mit der Sie Ihre Veranstaltungen bewerben und Ihre Zielgruppen erstellen können. Sie können [!DNL RainFocus] , um schöne Werbeseiten zu erstellen, die Kampagnenleistung zu verfolgen und Registrierungsumrechnungen zu optimieren.

Verwenden Sie die [!DNL RainFocus] in Adobe Experience Platform und Real-time Customer Data Platform zur automatischen Anreicherung Ihrer Kundendatenprofile mit Teilnehmererlebnisereignissen in Echtzeit. Nach der Aktivierung werden Erlebnisereignisse automatisch in Real-Time CDP gestreamt, was eine leistungsstarke Zielgruppensegmentierung, Datenanalyse und Aktivierung der Journey mit nachgelagerten Zielen und Anwendungen wie Customer Journey Analytics und Adobe Journey Optimizer ermöglicht.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von der [!DNL RainFocus] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an den Kundendienst<span>@rainfocus.com oder besuchen Sie die [[!DNL RainFocus] Hilfe-Center](https://help.rainfocus.com/hc/en-us)

## Voraussetzungen

Sie müssen die folgenden Voraussetzungen erfüllen, bevor Sie die [!DNL RainFocus] Integration in Experience Platform:

[Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe hat vor kurzem die Einstellung von JWT-Token zugunsten von OAuth angekündigt. Um dieser Änderung Rechnung zu tragen, muss die Variable [!DNL RainFocus] -Quelle wird in naher Zukunft auf OAuth migriert.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung herzustellen [!DNL RainFocus] zur Experience Platform hinzufügen, müssen Sie Werte für die folgenden Verbindungseigenschaften in [!DNL RainFocus]:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Die Client-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Client-Geheimnis | Das Client-Geheimnis kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID des technischen Kontos | Die technische Konto-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisations-ID | Die Organisations-ID kann über das Adobe Service-Konto im Adobe Developer Portal abgerufen werden. | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Erstellen eines XDM-Schemas und Definieren des Identitätsfelds {#create-an-xdm-schema-and-define-the-identity-field}

So speichern Sie die Erlebnisereignisse aus [!DNL RainFocus] in Experience Platform müssen Sie ein Experience-Datenmodell (XDM)-Schema erstellen, um einen Datensatz zu beschreiben, in dem die möglichen Felder und Datentypen gespeichert werden können, von denen gesendet wird [!DNL RainFocus].

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
| `attendee.email` | Zeichenfolge | Benutzer<span>@company.com | Die E-Mail-Adresse des Teilnehmers. |
| `transmissionId` | Zeichenfolge | 1680309557133001YHhz | Eine eindeutige Kennung, die für Daten-Push verwendet wird. |
| `eventType` | Zeichenfolge | SessionScheduled | Der Name des Teilnehmer-Erlebnisereignisses. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000 Z | Der Zeitstempel der Daten-Push-Benachrichtigung. |
| `event.name` | Zeichenfolge | Adobe Summit 2023 | Der Name des Ereignisses, bei dem eine Übertragung stattgefunden hat. |
| `exhibitor.exhibitorId` | Zeichenfolge | 1680309557133001YHhz | Die [!DNL RainFocus] Kennung des Ausstellers. |
| `exhibitor.externalId` | Zeichenfolge | 1666809514105001lSJN | Die Kennung für den Aussteller im Kundensystem. |
| `exhibitor.name` | Zeichenfolge | IBM | Der Name des Ausstellers. |
| `lead.leadId` | Zeichenfolge | 1666809456617001wyPj | Die [!DNL RainFocus] Kennung für den Lead. |
| `lead.note` | Zeichenfolge | | |
| `session.sessionId` | Zeichenfolge | 1666809373585001t4aV | Die [!DNL RainFocus] Kennung für die Sitzung. |
| `session.externalId` | Zeichenfolge | 1666809456617001wyPj | Die Kennung für die Sitzung im Client-System. |
| `session.code` | Zeichenfolge | GS3 | Der Code für die Sitzung. |
| `session.title` | Zeichenfolge | Inspiration - Keynote | Der Titel der Sitzung. |
| `session.length` | Ganzzahl | 90 | Die Dauer der Sitzung. |
| `sessiontime.sessiontimeId` | Zeichenfolge | 1673033149739001OJLZ | Die [!DNL RainFocus] Kennung für die Sitzungszeit. |
| `sessiontime.startTime` | Zeichenfolge | 2023-03-22 10:00:00 | Die Startzeit der Sitzung. |
| `sessiontime.endTime` | Zeichenfolge | 2023-03-22 10:00:00 | Die Endzeit der Sitzung. |
| `sessiontime.room` | Zeichenfolge | B32 | Der für die Sitzung verwendete Raum. |

{style="table-layout:auto"}

So erstellen Sie Ihr Schema für [!DNL RainFocus] -Daten finden Sie in der folgenden Dokumentation Schritte zum Erstellen eines Schemas mithilfe von APIs oder der Benutzeroberfläche.

* [Erstellen des Schemas mithilfe der Benutzeroberfläche](../../../xdm/tutorials/create-schema-ui.md)
* [Schema mit der API erstellen](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Das Schema muss die **XDM ExperienceEvent-Klasse.**
>* Sie müssen sicherstellen, dass das Schema eine **primäre Identität** und ist **aktiviert für Profil**. Weitere Informationen finden Sie im Handbuch unter [Identitätsfelder in der Benutzeroberfläche definieren](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Sie können die Beispielidentität (E-Mail) durch eine andere geeignete Kennung wie eine SHA256-E-Mail oder ECID ersetzen.

### Erstellen eines Integrationsprofils in RainFocus {#create-an-integration-profile-in-rainfocus}

Sobald Ihr Dienstkonto und Ihr XDM-Schema fertig sind, können Sie jetzt die [!DNL Integration Profile] durch [!DNL RainFocus] Plattform. Die [!DNL Integration Profile] ist für das Streaming von Daten an Experience Platform verantwortlich.

Melden Sie sich bei der [[!DNL RainFocus] platform](https://app.rainfocus.com). Wählen Sie im primären Navigationsmenü die Option **[!DNL Libraries]** und wählen Sie **[!DNL Integration Profiles]**

![Die RainFocus-Benutzeroberfläche mit ausgewählten Bibliotheken und Integrationsprofilen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Um ein neues Profil zu erstellen, wählen Sie die **(`+`)** Symbol. Wählen Sie als Nächstes **Adobe Real-time Customer Data Platform** und wählen Sie **OK**.

![Das Fenster Integrationsprofil erstellen in der RainFocus -Benutzeroberfläche.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Geben Sie anschließend die Anmeldeinformationen ein, die Sie im Adobe Developer Portal-Projekt abgerufen haben:

* **Client-ID**
* **Client-Geheimnis**
* **ID des technischen Kontos**
* **Organisations-ID**

Nachdem die Anmeldeinformationen bereitgestellt wurden, wählen Sie **[!DNL Save]**.Jetzt sollte die neue [!DNL Integration Profile] im [!DNL RainFocus] Dashboard.

Wählen Sie die [!DNL Integration Profile] die Sie gerade erstellt haben, um eine Liste vordefinierter **Push-Typen** bereits konfiguriert wurde. Dies sind die [Erlebnisereignisse](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=de) wird an Experience Platform gesendet, sobald sie auftreten.

![Eine Liste vordefinierter Push-Typen im Dashboard &quot;RainFocus&quot;.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Um eine Kopie der JSON-Beispielnutzlast abzurufen, wählen Sie **[!DNL Sample JSON Payload]**. Markieren und kopieren Sie als Nächstes die JSON-Beispielnutzlast und **Speichern Sie sie in einer neuen Datei mit der Erweiterung .json .**. Dies wird später in der Experience Platform für [Zuordnungskonfigurationen](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Eine JSON-Beispielnutzlast im Dashboard &quot;RainFocus&quot;.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Die Einrichtung ist noch nicht abgeschlossen.**: Sobald Ihr Datenfluss erstellt wurde, müssen Sie zum [!DNL RainFocus] Dashboard, um Ihre [!DNL Integration Profile] durch Bereitstellung **Streaming-Endpunkt-URL** und **dataflow-ID**.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderlichen Voraussetzungen für das Streamen von Daten aus Ihrem [!DNL RainFocus] -Konto auf Experience Platform. Sie können jetzt mit dem Handbuch zu [Verbindung [!DNL RainFocus] zur Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/analytics/rainfocus.md).