---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: df36d88de8ac117206d8d744cfcdd7804fcec61e
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 82%

---


# Datenschutzaufträge

In diesem Dokument wird beschrieben, wie Sie mit Datenschutzaufträgen mit API-Aufrufen arbeiten. Insbesondere wird die Verwendung des `/job` Endpunkts in der Privacy Service-API behandelt. Before reading this guide, refer to the [getting started section](./getting-started.md#getting-started) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Alle Aufträge auflisten {#list}

You can view a list of all available privacy jobs within your organization by making a GET request to the `/jobs` endpoint.

**API-Format**

This request format uses a `regulation` query parameter on the `/jobs` endpoint, therefore it begins with a question mark (`?`) as shown below. Die Antwort wird paginiert, sodass Sie andere Abfrageparameter (`page` und `size`) verwenden können, um die Antwort zu filtern. Sie können mehrere Parameter mithilfe von Ampersands (`&`) trennen.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{REGULATION}` | Der Regelungstyp für die Abfrage. Zulässige Werte sind `gdpr`, `ccpa`und `pdpa_tha`. |
| `{PAGE}` | Die Seite der anzuzeigenden Daten mit 0-basierter Nummerierung. Die Standardeinstellung lautet `0`. |
| `{SIZE}` | Die Anzahl der Ergebnisse, die auf jeder Seite angezeigt werden sollen. Der Standardwert ist `1` und der Maximalwert ist `100`. Wenn Sie den Maximalwert überschreiten, gibt die API einen 400-Code-Fehler zurück. |

**Anfrage**

Die folgende Anfrage ruft eine paginierte Liste aller Aufträge innerhalb eines IMS-Unternehmens ab, beginnend mit der dritten Seite mit einem Seitenformat von 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Aufträgen zurück, wobei jeder Auftrag Details wie z. B. seine `jobId` enthält. In diesem Beispiel würde die Antwort eine Liste von 50 Aufträgen enthalten, beginnend mit der dritten Ergebnisseite.

### Zugreifen auf nachfolgende Seiten

Um den nächsten Ergebnissatz in einer paginierten Antwort abzurufen, müssen Sie einen weiteren API-Aufruf an denselben Endpunkt ausführen, während Sie den Parameter `page` um 1 erhöhen.

## Erstellen eines Datenschutzauftrags {#create-job}

Bevor Sie eine neue Auftragsanfrage erstellen, müssen Sie zunächst identifizierende Informationen zu den betroffenen Personen erfassen, deren Daten Sie aufrufen, löschen oder für die Sie ein Opt-out aus dem Verkauf erwirken möchten. Once you have the required data, it must be provided in the payload of a POST request to the `/jobs` endpoint.

>[!NOTE]
>
>Kompatible Adobe Experience Cloud-Anwendungen verwenden unterschiedliche Werte zur Identifizierung von Datensubjekten. Weitere Informationen zu den erforderlichen Identifikatoren für Ihre Anwendungen finden Sie im Handbuch zu [Privacy Service und Experience Cloud-Anwendungen](../experience-cloud-apps.md). Eine allgemeine Anleitung zur Bestimmung der IDs, die an Privacy Service gesendet werden sollen, finden Sie im Dokument zu [Identitätsdaten in Datenschutzanforderungen](../identity-data.md).

Die Privacy Service-API unterstützt zwei Arten von Auftragsanfragen für personenbezogene Daten:

* [Zugriff und/oder Löschen](#access-delete): Zugriff (lesen) oder Löschen personenbezogener Daten.
* [Opt-out vom Verkauf](#opt-out): Markieren Sie persönliche Daten als nicht verkäuflich.

>[!IMPORTANT]
>
>Während Zugriff- und Löschanfragen zu einem einzigen API-Aufruf kombiniert werden können, müssen Opt-Out-Anfragen separat gestellt werden.

### Erstellen/Löschen eines Auftrags {#access-delete}

In diesem Abschnitt wird gezeigt, wie mithilfe der API eine Anfrage zum Zugriff/Löschen von Aufträgen erstellt wird.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Mit der folgenden Anfrage wird eine neue Auftragsanfrage erstellt, die von den Attributen konfiguriert wird, die in der Payload wie unten beschrieben bereitgestellt werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Identifikator enthält die folgenden Attribute: <ul><li>`namespace`: Den Namensraum eines Identifikators.</li><li>`value`: Den Wert des Identifikators.</li></ul>Es ist **erforderlich**, dass einer der Identifikatoren `imsOrgId` als sein `namespace` verwendet wird, wobei sein `value` die eindeutige ID für Ihre IMS-Organisation enthält. <br/><br/>Zusätzliche Identifikatoren können produktspezifische Firmenqualifizierer sein (z. B. `Campaign`), die eine Integration mit einer Adobe-Anwendung Ihrer Organisation identifizieren. Mögliche Werte sind Kontonamen, Client-Codes, Mandanten-IDs oder andere Anwendungs-Identifikatoren. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, auf den Sie zugreifen, oder den Sie löschen möchten. In einer einzigen Anfrage können maximal 1000 Benutzer-IDs bereitgestellt werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-IDs in den Antwortdaten zu qualifizieren. Es gilt als Best Practice, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten auflistet. Je nach den Aktionen, die Sie ausführen möchten, muss dieses Array `access`, `delete` oder beide enthalten.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value` und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md).</li></ul> Eine ausführlichere Erläuterung zu `users` und `userIDs` finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anfrage zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei Festlegung auf `true` eine Optimierung für die Verarbeitung der IDs in den Anwendungen darstellt (derzeit nur von Analytics unterstützt). Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anfragen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn keine `priority` angegeben wird, lautet das Standardverhalten `normal`. |
| `analyticsDeleteMethod` | Eine optionale Eigenschaft, die angibt, wie Adobe Analytics mit den personenbezogenen Daten umgehen soll. Für dieses Attribut werden zwei mögliche Werte akzeptiert: <ul><li>`anonymize`: Alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, werden anonym gemacht. Wenn `analyticsDeleteMethod` ausgelassen wird, ist dies das Standardverhalten.</li><li>`purge`: Alle Daten werden vollständig entfernt.</li></ul> |
| `regulation` **(Erforderlich)** | Die Verordnung für die Anfrage. Muss einer der folgenden drei Werte sein: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Aufträge zurück.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `jobId` | Eine schreibgeschützte, eindeutige, systemgenerierte ID für einen Auftrag. Dieser Wert wird im nächsten Schritt der Suche nach einem bestimmten Auftrag verwendet. |

Nachdem Sie die Auftragsanfrage erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur [Überprüfung des Auftragsstatus](#check-status) fortfahren.

### Erstellen eines Opt-Out-Verkaufsauftrags {#opt-out}

In diesem Abschnitt wird gezeigt, wie eine Anfrage zum Opt-Out vom Verkauf mithilfe der API durchgeführt wird.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Mit der folgenden Anfrage wird eine neue Auftragsanfrage erstellt, die von den Attributen konfiguriert wird, die in der Payload wie unten beschrieben bereitgestellt werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Identifikator enthält die folgenden Attribute: <ul><li>`namespace`: Den Namensraum eines Identifikators.</li><li>`value`: Den Wert des Identifikators.</li></ul>Es ist **erforderlich**, dass einer der Identifikatoren `imsOrgId` als sein `namespace` verwendet wird, wobei sein `value` die eindeutige ID für Ihre IMS-Organisation enthält. <br/><br/>Zusätzliche Identifikatoren können produktspezifische Firmenqualifizierer sein (z. B. `Campaign`), die eine Integration mit einer Adobe-Anwendung Ihrer Organisation identifizieren. Mögliche Werte sind Kontonamen, Client-Codes, Mandanten-IDs oder andere Anwendungs-Identifikatoren. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, auf den Sie zugreifen, oder den Sie löschen möchten. In einer einzigen Anfrage können maximal 1000 Benutzer-IDs bereitgestellt werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-IDs in den Antwortdaten zu qualifizieren. Es gilt als Best Practice, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, in dem die gewünschten Aktionen für die Datenerfassung aufgelistet sind. Bei Opt-Out vom Verkaufs-Anfragen darf das Array nur den Wert `opt-out-of-sale` enthalten.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value` und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md).</li></ul> Eine ausführlichere Erläuterung zu `users` und `userIDs` finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anfrage zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei Festlegung auf `true` eine Optimierung für die Verarbeitung der IDs in den Anwendungen darstellt (derzeit nur von Analytics unterstützt). Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anfragen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn keine `priority` angegeben wird, lautet das Standardverhalten `normal`. |
| `analyticsDeleteMethod` | Eine optionale Eigenschaft, die angibt, wie Adobe Analytics mit den personenbezogenen Daten umgehen soll. Für dieses Attribut werden zwei mögliche Werte akzeptiert: <ul><li>`anonymize`: Alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, werden anonym gemacht. Wenn `analyticsDeleteMethod` ausgelassen wird, ist dies das Standardverhalten.</li><li>`purge`: Alle Daten werden vollständig entfernt.</li></ul> |
| `regulation` **(Erforderlich)** | Die Verordnung für die Anfrage. Muss einer der folgenden drei Werte sein: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Aufträge zurück.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `jobId` | Eine schreibgeschützte, eindeutige, systemgenerierte ID für einen Auftrag. Dieser Wert wird verwendet, um im nächsten Schritt einen bestimmten Auftrag nachzuschlagen. |

Nachdem Sie die Auftragsanfrage erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur Überprüfung des Auftragsstatus fortfahren.

## Status eines Auftrags überprüfen {#check-status}

Sie können Informationen zu einem bestimmten Auftrag abrufen, z. B. seinen aktuellen Verarbeitungsstatus, indem Sie den Auftrag `jobId` im Pfad einer GET-Anforderung zum `/jobs` Endpunkt einschließen.

>[!IMPORTANT]
>
>Daten zu zuvor erstellten Aufträgen stehen nur innerhalb von 30 Tagen nach Abschluss des Auftrags zum Abruf bereit.

**API-Format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{JOB_ID}` | Die ID des Auftrags, den Sie nachschlagen möchten. Diese ID wird unter `jobId` erfolgreichen API-Antworten zum [Erstellen eines Auftrags](#create-job) und zur [Auflistung aller Aufträge](#list)zurückgegeben. |

**Anfrage**

Die folgende Anfrage ruft die Details des Auftrags ab, dessen `jobId` im Anfragepfad angegeben ist.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des angegebenen Auftrags zurück.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `productStatusResponse` | Jedes Objekt im `productResponses` Array enthält Informationen zum aktuellen Status des Auftrags in Bezug auf eine bestimmte [!DNL Experience Cloud] Anwendung. |
| `productStatusResponse.status` | Die aktuelle Status-Kategorie des Auftrags. Die nachstehende Tabelle enthält eine Liste der [verfügbaren Kategorien](#status-categories) und deren Bedeutung. |
| `productStatusResponse.message` | Der spezifische Status des Auftrags, der der Status-Kategorie entspricht. |
| `productStatusResponse.responseMsgCode` | Ein Standardcode für Produktansprechmeldungen, die der Privacy Service erhält. Die Einzelheiten der Nachricht finden Sie unter `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Eine detailliertere Erläuterung des Auftragsstatus. Meldungen für ähnliche Status können je nach Produkt unterschiedlich sein. |
| `productStatusResponse.results` | Bei bestimmten Statusangaben geben einige Produkte möglicherweise ein `results` Objekt zurück, das zusätzliche Informationen bereitstellt, die nicht von abgedeckt werden `responseMsgDetail`. |
| `downloadURL` | Ist der Auftragsstatus `complete`, stellt dieses Attribut eine URL zum Herunterladen der Auftragsergebnisse als ZIP-Datei bereit. Diese Datei kann bis zu 60 Tagen nach Abschluss des Auftrags heruntergeladen werden. |

### Kategorien zum Auftragsstatus {#status-categories}

In der folgenden Tabelle werden die verschiedenen Kategorien zum Auftragsstatus und ihre jeweilige Bedeutung Liste:

| Status-Kategorie | Bedeutung |
| -------------- | -------- |
| Abgeschlossen | Der Auftrag ist abgeschlossen und (falls erforderlich) werden Dateien von jeder Anwendung hochgeladen. |
| Verarbeitung | Anwendungen haben den Auftrag bestätigt und sind derzeit bei der Verarbeitung. |
| Gesendet | Der Auftrag wird bei allen anwendbaren Anwendungen eingereicht. |
| Fehler | Bei der Verarbeitung des Auftrags ist etwas fehlgeschlagen – spezifischere Informationen können Sie durch Abrufen einzelner Auftragsdetails erhalten. |

>[!NOTE]
>
>Ein gesendeter Auftrag kann sich im Verarbeitungsstatus befinden, wenn er einen abhängigen untergeordneten Auftrag hat, der noch verarbeitet wird.

## Nächste Schritte

Sie wissen jetzt, wie Sie mit der Privacy Service-API Datenschutzaufträge erstellen und überwachen. Informationen zum Ausführen derselben Aufgaben über die Benutzeroberfläche finden Sie in der [Privacy Service – UI-Übersicht](../ui/overview.md).
