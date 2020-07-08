---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 2%

---


# Datenschutzaufträge

In den folgenden Abschnitten werden die Aufrufe erläutert, die Sie mithilfe des `/jobs` Endpunkts in der Privacy Service-API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

## Erstellen eines Datenschutzauftrags {#create-job}

Bevor Sie eine neue Auftragsanforderung erstellen, müssen Sie zunächst identifizierende Informationen zu den betroffenen Personen erfassen, deren Daten Sie aufrufen, löschen oder Opt-out verkaufen möchten. Sobald Sie über die erforderlichen Daten verfügen, müssen diese in der Payload einer POST-Anforderung an den Stamm-Endpunkt bereitgestellt werden.

>[!NOTE]
>
>Kompatible Adobe Experience Cloud-Anwendungen verwenden unterschiedliche Werte zur Identifizierung von Datensubjekten. Weitere Informationen zu den erforderlichen Bezeichnern für Ihre Anwendungen finden Sie im Handbuch zu [Privacy Service- und Experience Cloud-Anwendungen](../experience-cloud-apps.md) .

Die Privacy Service-API unterstützt zwei Arten von Auftragsanforderungen für personenbezogene Daten:

* [Zugriff und/oder Löschen](#access-delete): Zugriff (lesen) oder Löschen personenbezogener Daten.
* [Opt-out:](#opt-out)Markieren Sie persönliche Daten als nicht zu verkaufen.

>[!IMPORTANT]
>
>Während Zugriff- und Löschanforderungen als ein einziger API-Aufruf kombiniert werden können, müssen Abmeldeanforderungen separat gestellt werden.

### Erstellen/Löschen eines Auftrags {#access-delete}

In diesem Abschnitt wird gezeigt, wie mithilfe der API eine Anfrage zum Zugriff/Löschen von Aufträgen erstellt wird.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Mit der folgenden Anforderung wird eine neue Auftragsanforderung erstellt, die von den Attributen konfiguriert wird, die in der Payload wie unten beschrieben bereitgestellt werden.

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
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Bezeichner enthält die folgenden Attribute: <ul><li>`namespace`: Der Namensraum einer Kennung.</li><li>`value`: Der Wert des Bezeichners.</li></ul>Es ist **erforderlich** , dass einer der Bezeichner `imsOrgId` als seinen verwendet `namespace`, wobei die eindeutige ID für Ihre IMS-Organisation `value` enthalten ist. <br/><br/>Zusätzliche IDs können produktspezifische Firmen (z. B. `Campaign`) sein, die eine Integration mit einer Adobe-Anwendung in Ihrem Unternehmen identifizieren. Mögliche Werte sind Kontonamen, Clientcodes, Mieter-IDs oder andere Anwendungskennungen. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, dessen Informationen Sie aufrufen oder löschen möchten. In einer einzigen Anforderung können maximal 1000 Benutzer-IDs bereitgestellt werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Bezeichner für einen Benutzer, der verwendet wird, um die separaten Job-IDs in den Antwortdaten zu qualifizieren. Es empfiehlt sich, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten Liste. Je nach den Aktionen, die Sie ausführen möchten, muss dieses Array `access`, `delete`oder beide enthalten.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value`und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md) .</li></ul> Eine ausführlichere Erläuterung `users` und `userIDs`weitere Informationen finden Sie im Handbuch zur [Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anforderung zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei Festlegung auf `true`eine Optimierung für die Verarbeitung der IDs in den Anwendungen darstellt (derzeit nur von Analytics unterstützt). If omitted, this value defaults to `false`. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anforderungen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn `priority` kein Wert angegeben wird, lautet das Standardverhalten `normal`. |
| `analyticsDeleteMethod` | Eine optionale Eigenschaft, die angibt, wie Adobe Analytics die personenbezogenen Daten handhaben soll. Für dieses Attribut werden zwei mögliche Werte akzeptiert: <ul><li>`anonymize`: Alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, werden anonym gemacht. Wenn `analyticsDeleteMethod` kein Wert angegeben wird, ist dies das Standardverhalten.</li><li>`purge`: Alle Daten werden vollständig entfernt.</li></ul> |
| `regulation` **(Erforderlich)** | Die Verordnung für den Antrag. muss einer der folgenden drei Werte sein: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

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

Nachdem Sie die Auftragsanforderung erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur [Überprüfung des Auftragsstatus](#check-status)fortfahren.

### Erstellen eines Abmeldeauftrags {#opt-out}

In diesem Abschnitt wird gezeigt, wie eine Anforderung zum Ausschluss vom Verkauf mithilfe der API durchgeführt wird.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Mit der folgenden Anforderung wird eine neue Auftragsanforderung erstellt, die von den Attributen konfiguriert wird, die in der Payload wie unten beschrieben bereitgestellt werden.

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
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Bezeichner enthält die folgenden Attribute: <ul><li>`namespace`: Der Namensraum einer Kennung.</li><li>`value`: Der Wert des Bezeichners.</li></ul>Es ist **erforderlich** , dass einer der Bezeichner `imsOrgId` als seinen verwendet `namespace`, wobei die eindeutige ID für Ihre IMS-Organisation `value` enthalten ist. <br/><br/>Zusätzliche IDs können produktspezifische Firmen (z. B. `Campaign`) sein, die eine Integration mit einer Adobe-Anwendung in Ihrem Unternehmen identifizieren. Mögliche Werte sind Kontonamen, Clientcodes, Mieter-IDs oder andere Anwendungskennungen. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, dessen Informationen Sie aufrufen oder löschen möchten. In einer einzigen Anforderung können maximal 1000 Benutzer-IDs bereitgestellt werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Bezeichner für einen Benutzer, der verwendet wird, um die separaten Job-IDs in den Antwortdaten zu qualifizieren. Es empfiehlt sich, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, in dem die gewünschten Aktionen für die Datenerfassung Liste werden. Bei Ausschlussanfragen darf das Array nur den Wert enthalten `opt-out-of-sale`.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value`und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md) .</li></ul> Eine ausführlichere Erläuterung `users` und `userIDs`weitere Informationen finden Sie im Handbuch zur [Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anforderung zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei Festlegung auf `true`eine Optimierung für die Verarbeitung der IDs in den Anwendungen darstellt (derzeit nur von Analytics unterstützt). If omitted, this value defaults to `false`. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anforderungen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn `priority` kein Wert angegeben wird, lautet das Standardverhalten `normal`. |
| `analyticsDeleteMethod` | Eine optionale Eigenschaft, die angibt, wie Adobe Analytics die personenbezogenen Daten handhaben soll. Für dieses Attribut werden zwei mögliche Werte akzeptiert: <ul><li>`anonymize`: Alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, werden anonym gemacht. Wenn `analyticsDeleteMethod` kein Wert angegeben wird, ist dies das Standardverhalten.</li><li>`purge`: Alle Daten werden vollständig entfernt.</li></ul> |
| `regulation` **(Erforderlich)** | Die Verordnung für den Antrag. muss einer der folgenden drei Werte sein: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

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

Nachdem Sie die Auftragsanforderung erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur Überprüfung des Auftragsstatus fortfahren.

## Status eines Auftrags überprüfen {#check-status}

Mithilfe eines der im vorherigen Schritt zurückgegebenen `jobId` Werte können Sie Informationen zu diesem Auftrag abrufen, z. B. den aktuellen Verarbeitungsstatus.

>[!IMPORTANT]
>
>Daten zu zuvor erstellten Aufträgen stehen nur innerhalb von 30 Tagen nach Abschluss des Auftrags zum Abruf bereit.

**API-Format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{JOB_ID}` | Die ID des Auftrags, den Sie nachschlagen möchten, wird `jobId` in der Antwort des [vorherigen Schritts](#create-job)zurückgegeben. |

**Anfrage**

Die folgende Anforderung ruft die Details des Auftrags ab, der im Anforderungspfad angegeben `jobId` ist.

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
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
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
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `productStatusResponse` | Der aktuelle Status des Auftrags. Details zu jedem möglichen Status finden Sie in der unten stehenden Tabelle. |
| `downloadURL` | Ist der Auftragsstatus `complete`vorhanden, stellt dieses Attribut eine URL zum Herunterladen der Auftragsergebnisse als ZIP-Datei bereit. Diese Datei kann 60 Tage nach Abschluss des Auftrags heruntergeladen werden. |

### Auftragsstatus-Antworten

In der folgenden Tabelle werden die verschiedenen möglichen Auftragsstatus und die entsprechende Bedeutung Liste:

| Statuscode | Statusmeldung | Bedeutung |
| ----------- | -------------- | -------- |
| 1 | Complete | Der Auftrag ist abgeschlossen und (falls erforderlich) Dateien werden von jeder Anwendung hochgeladen. |
| 2 | Verarbeitung | Anwendungen haben den Auftrag bestätigt und werden derzeit verarbeitet. |
| 3 | Gesendet | Der Auftrag wird bei jedem Antrag eingereicht. |
| 4 | Fehler | Bei der Verarbeitung des Auftrags ist etwas fehlgeschlagen - spezifischere Informationen können Sie durch Abrufen einzelner Auftragsdetails erhalten. |

>[!NOTE]
>
>Ein gesendeter Auftrag kann sich im Verarbeitungsstatus befinden, wenn er einen abhängigen untergeordneten Auftrag hat, der noch verarbeitet wird.

## Liste aller Aufträge

Sie können eine Liste aller in Ihrem Unternehmen verfügbaren Auftragsanfragen erstellen, indem Sie eine GET-Anforderung an den Stammendpunkt (`/`) senden.

**API-Format**

Dieses Anforderungsformat verwendet einen Parameter für die `regulation` Abfrage am Stamm-Endpunkt (`/`). Daher beginnt es mit einem Fragezeichen (`?`), wie unten dargestellt. Die Antwort wird paginiert, sodass Sie andere Abfragen (`page` und `size`) verwenden können, um die Antwort zu filtern. Sie können mehrere Parameter mithilfe von Ampersands (`&`) trennen.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{REGULATION}` | Der Regelungstyp für die Abfrage. Die zulässigen Werte sind `gdpr`, `ccpa`und `pdpa_tha`. |
| `{PAGE}` | Die Seite der anzuzeigenden Daten mit 0-basierter Nummerierung. Die Standardeinstellung lautet `0`. |
| `{SIZE}` | Die Anzahl der Ergebnisse, die auf jeder Seite angezeigt werden sollen. Der Standardwert ist `1` und der Maximalwert ist `100`. Wenn Sie den Maximalwert überschreiten, gibt die API einen 400-Code-Fehler zurück. |

**Anfrage**

Die folgende Anforderung ruft eine paginierte Liste aller Aufträge innerhalb eines IMS-Unternehmens ab, beginnend mit der dritten Seite mit einem Seitenformat von 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Aufträgen zurück, wobei jeder Auftrag Details wie z. B. seine `jobId`enthält. In diesem Beispiel würde die Antwort eine Liste von 50 Aufträgen enthalten, beginnend mit der dritten Ergebnisseite.

### Zugreifen auf nachfolgende Seiten

Um den nächsten Ergebnissatz in einer paginierten Antwort abzurufen, müssen Sie einen weiteren API-Aufruf an denselben Endpunkt ausführen, während Sie den Parameter &quot; `page` Abfrage&quot;um 1 erhöhen.

## Nächste Schritte

Sie wissen jetzt, wie Sie mit der Privacy Service-API Datenschutzaufträge erstellen und überwachen. Informationen zum Ausführen derselben Aufgaben mithilfe der Benutzeroberfläche finden Sie in der Übersicht über die Benutzeroberfläche des [Privacy Service](../ui/overview.md).
