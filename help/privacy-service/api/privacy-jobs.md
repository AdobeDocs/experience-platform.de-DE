---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Endpunkt der Datenschutzaufträge-API
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Privacy Service-API Datenschutzaufträge für Experience Cloud-Anwendungen verwalten.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 68%

---

# Endpunkt für Datenschutzaufträge

In diesem Dokument wird beschrieben, wie Sie mit API-Aufrufen mit Datenschutzaufträgen arbeiten. Konkret betrifft sie die Verwendung der `/job` Endpunkt im [!DNL Privacy Service] API. Bevor Sie dieses Handbuch lesen, beachten Sie die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie kennen müssen, um erfolgreich Aufrufe der API durchzuführen, einschließlich der erforderlichen Kopfzeilen und des Lesens von Beispiel-API-Aufrufen.

>[!NOTE]
>
>Wenn Sie versuchen, Zustimmungs- oder Abmeldeanfragen von Kunden zu verwalten, finden Sie weitere Informationen unter [Endpunkt-Handbuch für Zustimmung](./consent.md).

## Alle Aufträge auflisten {#list}

Sie können eine Liste aller verfügbaren Datenschutzaufträge in Ihrem Unternehmen Ansicht haben, indem Sie eine GET an die `/jobs` Endpunkt.

**API-Format**

Dieses Anforderungsformat verwendet `regulation` Parameter &quot;Abfrage&quot;im `/jobs` Endpunkt beginnt daher mit einem Fragezeichen (`?`) wie unten dargestellt. Die Antwort wird paginiert, sodass Sie andere Abfrageparameter (`page` und `size`) verwenden können, um die Antwort zu filtern. Sie können mehrere Parameter mithilfe von Ampersands (`&`) trennen.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{REGULATION}` | Der Regelungstyp für die Abfrage. Akzeptierte Werte sind: <ul><li>`gdpr` (Europäische Vereinigung)</li><li>`ccpa` (Kalifornien)</li><li>`lgpd_bra` (Brasilien)</li><li>`nzpa_nzl` (Neuseeland)</li><li>`pdpa_tha` (Thailand)</li></ul> |
| `{PAGE}` | Die Seite der anzuzeigenden Daten mit 0-basierter Nummerierung. Die Standardeinstellung lautet `0`. |
| `{SIZE}` | Die Anzahl der Ergebnisse, die auf jeder Seite angezeigt werden sollen. Der Standardwert ist `1` und der Maximalwert ist `100`. Wenn Sie den Maximalwert überschreiten, gibt die API einen 400-Code-Fehler zurück. |

{style=&quot;table-layout:auto&quot;}

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

Um den nächsten Ergebnissatz in einer paginierten Antwort abzurufen, müssen Sie einen weiteren API-Aufruf an denselben Endpunkt ausführen, während Sie den Abfrageparameter `page` um 1 erhöhen.

## Erstellen eines Datenschutzauftrags {#create-job}

Bevor Sie eine neue Auftragsanfrage erstellen, müssen Sie zunächst identifizierende Informationen zu den betroffenen Personen erfassen, deren Daten Sie aufrufen, löschen oder für die Sie ein Opt-out aus dem Verkauf erwirken möchten. Sobald Sie über die erforderlichen Daten verfügen, müssen diese in der Nutzlast einer POST an die `/jobs` Endpunkt.

>[!NOTE]
>
> Kompatible Adobe Experience Cloud-Anwendungen verwenden unterschiedliche Werte zur Identifizierung von Datensubjekten. Weitere Informationen zu den erforderlichen Identifikatoren für Ihre Anwendungen finden Sie im Handbuch zu [Privacy Service und Experience Cloud-Anwendungen](../experience-cloud-apps.md). Allgemeine Hinweise zur Bestimmung der zu sendenden IDs [!DNL Privacy Service], siehe Dokument auf [Identitätsdaten in Datenschutzanforderungen](../identity-data.md).

Die [!DNL Privacy Service] API unterstützt zwei Arten von Jobanfragen für personenbezogene Daten:

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
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Identifikator enthält die folgenden Attribute: <ul><li>`namespace`: Den Namensraum eines Identifikators.</li><li>`value`: Den Wert des Identifikators.</li></ul>Es ist **erforderlich**, dass einer der Identifikatoren `imsOrgId` als sein `namespace` verwendet wird, wobei sein `value` die eindeutige ID für Ihre IMS-Organisation enthält. <br/><br/>Zusätzliche IDs können produktspezifische Firmenqualifizierer sein (z. B. `Campaign`), die eine Integration mit einer Adobe-Anwendung Ihrer Organisation identifizieren. Mögliche Werte sind Kontonamen, Client-Codes, Mandanten-IDs oder andere Anwendungs-Identifikatoren. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, auf den Sie zugreifen, oder den Sie löschen möchten. In einer einzigen Anfrage können maximal 1000 Benutzer-IDs bereitgestellt werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-Identifikatoren in den Antwortdaten zu qualifizieren. Es gilt als Best Practice, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten auflistet. Je nach den Aktionen, die Sie ausführen möchten, muss dieses Array `access`, `delete` oder beide enthalten.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value` und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md).</li></ul> Eine ausführlichere Erläuterung zu `users` und `userIDs` finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anfrage zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei einem Wert von `true`, stellt eine Optimierung für die Verarbeitung der IDs in den Anwendungen dar (wird derzeit nur unterstützt von [!DNL Analytics]). Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anfragen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn keine `priority` angegeben wird, lautet das Standardverhalten `normal`. |
| `analyticsDeleteMethod` | Eine optionale Eigenschaft, die angibt, wie Adobe Analytics mit den personenbezogenen Daten umgehen soll. Für dieses Attribut werden zwei mögliche Werte akzeptiert: <ul><li>`anonymize`: Alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, werden anonym gemacht. Wenn `analyticsDeleteMethod` ausgelassen wird, ist dies das Standardverhalten.</li><li>`purge`: Alle Daten werden vollständig entfernt.</li></ul> |
| `regulation` **(Erforderlich)** | Die Regelung für die Datenschutzfunktion. Folgende Werte werden akzeptiert: <ul><li>`gdpr` (Europäische Vereinigung)</li><li>`ccpa` (Kalifornien)</li><li>`lgpd_bra` (Brasilien)</li><li>`nzpa_nzl` (Neuseeland)</li><li>`pdpa_tha` (Thailand)</li></ul> |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

Nachdem Sie die Auftragsanfrage erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur [Überprüfung des Auftragsstatus](#check-status) fortfahren.

## Status eines Auftrags überprüfen {#check-status}

Sie können Informationen über einen bestimmten Auftrag abrufen, z. B. seinen aktuellen Verarbeitungsstatus, indem Sie die `jobId` im Pfad einer GET-Anfrage an `/jobs` Endpunkt.

>[!IMPORTANT]
>
>Daten zu zuvor erstellten Aufträgen stehen nur innerhalb von 30 Tagen nach Abschluss des Auftrags zum Abruf bereit.

**API-Format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{JOB_ID}` | Die ID des Jobs, den Sie nachschlagen möchten. Diese ID wird zurückgegeben unter `jobId` in erfolgreichen API-Antworten für [Auftrag wird erstellt](#create-job) und [Alle Jobs auflisten](#list). |

{style=&quot;table-layout:auto&quot;}

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
| `productStatusResponse` | Jedes Objekt innerhalb von `productResponses` enthält Informationen über den aktuellen Status des Auftrags in Bezug auf einen bestimmten [!DNL Experience Cloud] Anwendung. |
| `productStatusResponse.status` | Die aktuelle Status-Kategorie des Auftrags. Eine Liste von [Verfügbare Status-Kategorien](#status-categories) und deren Bedeutung. |
| `productStatusResponse.message` | Der spezifische Status des Auftrags, der der Status-Kategorie entspricht. |
| `productStatusResponse.responseMsgCode` | Ein Standardcode für Produkt-Antwortnachrichten, die von [!DNL Privacy Service]. Einzelheiten der Nachricht finden Sie unter `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Eine detailliertere Erläuterung des Stellenstatus. Nachrichten für ähnliche Status können von Produkt zu Produkt unterschiedlich sein. |
| `productStatusResponse.results` | Für bestimmte Statusangaben können einige Produkte eine `results` Objekt, das zusätzliche Informationen liefert, die nicht von `responseMsgDetail`. |
| `downloadURL` | Ist der Auftragsstatus `complete`, stellt dieses Attribut eine URL zum Herunterladen der Auftragsergebnisse als ZIP-Datei bereit. Diese Datei kann bis zu 60 Tagen nach Abschluss des Auftrags heruntergeladen werden. |

{style=&quot;table-layout:auto&quot;}

### Kategorien zum Auftragsstatus {#status-categories}

In der folgenden Tabelle werden die verschiedenen möglichen Kategorien des Auftragsstatus und die entsprechende Bedeutung Liste:

| Status-Kategorie | Bedeutung |
| -------------- | -------- |
| `complete` | Der Auftrag ist abgeschlossen und (falls erforderlich) werden Dateien von jeder Anwendung hochgeladen. |
| `processing` | Anwendungen haben den Auftrag bestätigt und sind derzeit bei der Verarbeitung. |
| `submitted` | Der Auftrag wird bei allen anwendbaren Anwendungen eingereicht. |
| `error` | Bei der Verarbeitung des Auftrags ist etwas fehlgeschlagen – spezifischere Informationen können Sie durch Abrufen einzelner Auftragsdetails erhalten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Ein abgegebener Auftrag verbleibt möglicherweise in `processing` angeben, ob ein abhängiger untergeordneter Auftrag noch verarbeitet wird.

## Nächste Schritte

Sie wissen jetzt, wie Sie Datenschutzaufträge mithilfe der [!DNL Privacy Service] API. Informationen zum Ausführen derselben Aufgaben über die Benutzeroberfläche finden Sie in der [Privacy Service – UI-Übersicht](../ui/overview.md).
