---
title: RainFocus-Quelle - Übersicht
description: Erfahren Sie, wie Sie Ereignis-Management- und Analysedaten aus Ihrem RainFocus-Konto auf Experience Platform übertragen
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
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie &#x200B;](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

[!DNL RainFocus] ist eine Plattform, mit der Sie Ihre Ereignisse bewerben und Ihre Zielgruppen erstellen können. Sie können [!DNL RainFocus] verwenden, um schöne Werbeseiten zu erstellen, die Kampagnenleistung zu verfolgen und die Registrierungs-Konversionen zu optimieren.

Verwenden Sie die [!DNL RainFocus] in Adobe Experience Platform und Real-time Customer Data Platform, um Ihre Kundendatenprofile automatisch in Echtzeit mit Teilnehmererlebnisereignissen anzureichern. Nach der Aktivierung werden Erlebnisereignisse automatisch in Real-Time CDP gestreamt, was eine leistungsstarke Zielgruppensegmentierung, Datenanalyse und Aktivierung der Teilnehmer-Journey mit nachgelagerten Zielen und Anwendungen wie Customer Journey Analytics und Adobe Journey Optimizer ermöglicht.

>[!IMPORTANT]
>
>Dieser Quell-Connector und diese Dokumentationsseite werden vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an clientcare<span>@rainfocus.com oder besuchen Sie das [[!DNL RainFocus] Hilfezentrum](https://help.rainfocus.com/hc/en-us)

## Voraussetzungen

Sie müssen die folgenden Voraussetzungen erfüllen, bevor Sie die [!DNL RainFocus] auf Experience Platform aktivieren können:

[Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer-Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe hat kürzlich bekannt gegeben, dass JWT-Token zugunsten von OAuth nicht mehr unterstützt werden. Um diese Änderung vorzunehmen, wird die [!DNL RainFocus] in naher Zukunft zu OAuth migriert.

### Sammeln erforderlicher Anmeldedaten

Um [!DNL RainFocus] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften in [!DNL RainFocus] angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Die Client-ID erhalten Sie über das Adobe Service-Konto im Adobe Developer-Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Client-Geheimnis | Das Client-Geheimnis können Sie über das Adobe Service-Konto im Adobe Developer-Portal abrufen. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID des technischen Kontos | Die ID des technischen Kontos erhalten Sie über das Adobe Service-Konto im Adobe Developer-Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisations-ID | Die Organisations-ID erhalten Sie vom Adobe Service-Konto im Adobe Developer-Portal | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Erstellen eines XDM-Schemas und Definieren des Identitätsfelds {#create-an-xdm-schema-and-define-the-identity-field}

Um die Erlebnisereignisse aus [!DNL RainFocus] im Experience Platform zu speichern, müssen Sie ein Experience-Datenmodell (XDM)-Schema erstellen, um einen Datensatz zu beschreiben. Dieser Datensatz kann die möglichen Felder und Datentypen speichern, die vom [!DNL RainFocus] gesendet werden.

[!DNL RainFocus] empfiehlt die folgenden Felder, in denen alle standardmäßig gesendeten möglichen Daten erfasst sind.

Außerdem werden die folgenden Feldergruppen empfohlen (durch Präfix gekennzeichnet):

* Teilnehmer
* Aussteller
* Lead
* Session
* Sitzungsdauer

**Das Schema sollte die folgenden Felder enthalten:**

| Feld | Typ | Beispiel | Beschreibung |
| --- | --- | --- | --- |
| `attendee.registered` | Zeichenfolge | Ja | Eine Markierung, die bestimmt, ob der Teilnehmer als registriert gilt. |
| `attendee.attendeeId` | String | 1619119968857001fvLB | Die Teilnehmer-ID in [!DNL RainFocus]. |
| `attendee.externalId` | String | 1666809456617001pj | Die von einer Organisation angegebene externe ID. |
| `attendee.clientId` | String | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | Die Teilnehmer-SSO-Client-ID. |
| `attendee.email` | String | user<span>@company.com | Die E-Mail-Adresse des Teilnehmers. |
| `transmissionId` | String | 1680309557133001JHz | Eine eindeutige Kennung, die für die Daten-Push-Benachrichtigung verwendet wird. |
| `eventType` | String | Sitzung geplant | Der Name des Teilnehmererlebnisereignisses. |
| `timestamp` | DateTime | 01.04.2023:41:T00.57.000Z | Der Zeitstempel der Daten-Push-Benachrichtigung. |
| `event.name` | String | Adobe Summit 2023 | Der Name des Ereignisses, bei dem eine Übertragung stattgefunden hat. |
| `exhibitor.exhibitorId` | String | 1680309557133001JHz | Die [!DNL RainFocus] Kennung des Ausstellers. |
| `exhibitor.externalId` | String | 1666809514105001lSJN | Die Kennung für den Aussteller im Client-System. |
| `exhibitor.name` | String | IBM | Der Name des Ausstellers. |
| `lead.leadId` | String | 1666809456617001pj | Die [!DNL RainFocus] für den Lead. |
| `lead.note` | Zeichenfolge | | |
| `session.sessionId` | Zeichenfolge | 1666809373585001t4aV | Die [!DNL RainFocus] Kennung für die Sitzung. |
| `session.externalId` | String | 1666809456617001pj | Die Kennung für die Sitzung im Client-System. |
| `session.code` | String | GS3 | Der Code für die Sitzung. |
| `session.title` | String | Inspiration Keynote | Der Titel der Sitzung. |
| `session.length` | Ganzzahl | 90 | Die Dauer der Sitzung. |
| `sessiontime.sessiontimeId` | String | 1673033149739001OJLZ | Die [!DNL RainFocus] Kennung für die Sitzungszeit. |
| `sessiontime.startTime` | String | 22.03.2023 :00:.00 | Die Startzeit der Sitzung. |
| `sessiontime.endTime` | String | 22.03.2023 :00:.00 | Die Endzeit der Sitzung. |
| `sessiontime.room` | String | B32 | Der für die Sitzung genutzte Raum |

{style="table-layout:auto"}

Wie Sie Ihr Schema für [!DNL RainFocus] Daten erstellen, erfahren Sie in der folgenden Dokumentation , wie Sie ein Schema mithilfe von APIs oder der Benutzeroberfläche erstellen.

* [Erstellen des Schemas mithilfe der Benutzeroberfläche](../../../xdm/tutorials/create-schema-ui.md)
* [Erstellen des Schemas mithilfe der API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Das Schema muss die Klasse **XDM ExperienceEvent“ erweitern**
>* Sie müssen sicherstellen, dass das Schema eine **primäre Identität** enthält und **für Profil aktiviert** ist. Weitere Informationen finden sich im Handbuch unter [Definieren von Identitätsfeldern in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=de)
>* Sie können die Beispielidentität (E-Mail) durch eine andere geeignete Kennung wie eine sha256-E-Mail oder ECID ersetzen.

### Erstellen eines Integrationsprofils in RainFocus {#create-an-integration-profile-in-rainfocus}

Sobald Ihr Service-Konto und Ihr XDM-Schema fertig sind, können Sie das [!DNL Integration Profile] über die [!DNL RainFocus]-Plattform aktivieren. Die [!DNL Integration Profile] ist für das Streaming von Daten an Experience Platform verantwortlich.

Melden Sie sich bei [[!DNL RainFocus] Plattform](https://app.rainfocus.com) an. Wählen Sie in der primären Navigation **[!DNL Libraries]** und dann **[!DNL Integration Profiles]** aus

![Die RainFocus-Benutzeroberfläche mit ausgewählten Bibliotheken und Integrationsprofilen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Um ein neues Profil zu erstellen, wählen Sie das Symbol **(`+`)** aus. Wählen Sie als Nächstes **Adobe Real-time Customer Data Platform** und dann **OK** aus.

![Das Fenster Integrationsprofil erstellen in der RainFocus-Benutzeroberfläche.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Geben Sie als Nächstes die Anmeldeinformationen an, die Sie im Adobe Developer Portal-Projekt abgerufen haben:

* **Client ID** (Client-ID)
* **Client Secret** (Client-Geheimnis)
* **ID des technischen Kontos**
* **Organisations-ID**

Wählen Sie nach Angabe der Anmeldeinformationen **[!DNL Save]** aus. Jetzt sollte die neue [!DNL Integration Profile] im [!DNL RainFocus]-Dashboard aufgeführt werden.

Wählen Sie die soeben erstellte [!DNL Integration Profile] aus, um eine Liste der bereits konfigurierten vordefinierten **Push-Typen** anzuzeigen. Hierbei handelt es sich um [Erlebnisereignisse](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=de) die bei ihrem Auftreten an Experience Platform gesendet werden.

![Eine Liste vordefinierter Push-Typen im RainFocus-Dashboard.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Um eine Kopie der JSON-Beispiel-Payload abzurufen, wählen Sie **[!DNL Sample JSON Payload]** aus. Markieren und kopieren Sie als Nächstes die JSON-Beispiel-Payload und **Sie sie in einer neuen Datei mit der Erweiterung .json**. Dies wird später beim Experience Platform für „Zuordnungskonfigurationen[&#x200B; verwendet](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Beispiel-JSON-Payload im RainFocus-Dashboard.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Setup ist noch nicht abgeschlossen**: Nachdem Ihr Datenfluss erstellt wurde, müssen Sie zum [!DNL RainFocus]-Dashboard zurückkehren, um Ihre [!DNL Integration Profile] abzuschließen, indem Sie Ihre **Streaming-Endpunkt-URL** und **Datenfluss-ID**.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL RainFocus]-Konto auf Experience Platform zu streamen. Sie können jetzt mit dem Handbuch unter [Verbinden [!DNL RainFocus] Experience Platform über die Benutzeroberfläche fortfahren](../../tutorials/ui/create/analytics/rainfocus.md).
