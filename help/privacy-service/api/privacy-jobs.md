---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: API-Endpunkt für Datenschutzaufträge
description: Erfahren Sie, wie Sie Datenschutzaufträge für Experience Cloud-Anwendungen mit der Privacy Service-API verwalten.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 26a50f21c1ebebf485eaf62712bd02de3406cceb
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 45%

---

# Endpunkt für Datenschutzaufträge

In diesem Dokument wird beschrieben, wie Sie mit Datenschutzaufträgen arbeiten, indem Sie API-Aufrufe verwenden. Insbesondere wird die Verwendung des `/job`-Endpunkts in der [!DNL Privacy Service]-API behandelt. Bevor Sie dieses Handbuch lesen, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md), um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die -API benötigen, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

>[!NOTE]
>
>Wenn Sie versuchen, Einverständnis- oder Opt-out-Anfragen von Kundinnen und Kunden zu verwalten, lesen Sie das [Handbuch für Einverständnisendpunkte](./consent.md).

## Alle Aufträge auflisten {#list}

Sie können eine Liste aller in Ihrem Unternehmen verfügbaren Datenschutzaufträge anzeigen, indem Sie eine GET-Anfrage an den `/jobs`-Endpunkt senden.

**API-Format**

Dieses Anfrageformat verwendet einen `regulation` Abfrageparameter für den `/jobs`-Endpunkt, daher beginnt es mit einem Fragezeichen (`?`), wie unten gezeigt. Beim Auflisten von Ressourcen gibt die Privacy Service-API bis zu 1.000 Aufträge zurück und paginiert die Antwort. Verwenden Sie andere Abfrageparameter (`page`-, `size`- und Datumsfilter), um die Antwort zu filtern. Sie können mehrere Parameter mithilfe von Ampersands (`&`) trennen.

>[!TIP]
>
>Verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse für bestimmte Abfragen weiter zu filtern. Sie können beispielsweise mithilfe der Abfrageparameter `status`, `fromDate` und `toDate` ermitteln, wie viele Datenschutzaufträge in einem bestimmten Zeitraum gesendet wurden und welchen Status sie haben.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{REGULATION}` | Der Regelungstyp für die Abfrage. Zu den akzeptierten Werten gehören: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa_usa`</li><li>`cpra_usa`</li><li>`ctdpa_usa`</li><li>`dpdpa`</li><li>`fdbr_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`icdpa_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_usa`</li><li>`mhmda_usa`</li><li>`ndpa_usa`</li><li>`nhpa_usa`</li><li>`njdpa_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_usa`</li><li>`pdpa_tha`</li><li>`ql25`</li><li>`tdpsa_usa`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>Weitere Informationen zu den Datenschutzbestimmungen, [ die oben genannten Werte darstellen, finden Sie in der Übersicht zu unterstützten ](../regulations/overview.md)&quot;. |
| `{PAGE}` | Die Seite der anzuzeigenden Daten mit 0-basierter Nummerierung. Die Standardeinstellung lautet `0`. |
| `{SIZE}` | Die Anzahl der Ergebnisse, die auf jeder Seite angezeigt werden sollen. Der Standardwert ist `100` und der Maximalwert ist `1000`. Wenn Sie den Maximalwert überschreiten, gibt die API einen 400-Code-Fehler zurück. |
| `{status}` | Das Standardverhalten besteht darin, alle Status einzuschließen. Wenn Sie einen Statustyp angeben, gibt die Anfrage nur Datenschutzaufträge zurück, die diesem Statustyp entsprechen. Zu den akzeptierten Werten gehören: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Dieser Parameter beschränkt die Ergebnisse auf diejenigen, die vor einem bestimmten Datum verarbeitet wurden. Ab dem Datum der Anfrage kann das System 45 Tage zurückblicken. Der Bereich darf jedoch nicht länger als 30 Tage sein.<br>Sie akzeptiert das Format JJJJ-MM-TT. Das von Ihnen angegebene Datum wird als Enddatum interpretiert, das in Greenwich Mean Time (GMT) angegeben ist.<br>Wenn Sie diesen Parameter (und eine entsprechende `fromDate`) nicht angeben, gibt das Standardverhalten Aufträge zurück, die in den letzten sieben Tagen Daten zurückgegeben haben. Wenn Sie `toDate` verwenden, müssen Sie auch den `fromDate` Abfrageparameter verwenden. Wenn Sie nicht beide verwenden, gibt der Aufruf einen 400-Fehler zurück. |
| `{fromDate}` | Dieser Parameter beschränkt die Ergebnisse auf diejenigen, die nach einem bestimmten Datum verarbeitet werden. Ab dem Datum der Anfrage kann das System 45 Tage zurückblicken. Der Bereich darf jedoch nicht länger als 30 Tage sein.<br>Sie akzeptiert das Format JJJJ-MM-TT. Das von Ihnen angegebene Datum wird als Ursprungsdatum der Anfrage interpretiert, ausgedrückt in Greenwich Mean Time (GMT).<br>Wenn Sie diesen Parameter (und eine entsprechende `toDate`) nicht angeben, gibt das Standardverhalten Aufträge zurück, die in den letzten sieben Tagen Daten zurückgegeben haben. Wenn Sie `fromDate` verwenden, müssen Sie auch den `toDate` Abfrageparameter verwenden. Wenn Sie nicht beide verwenden, gibt der Aufruf einen 400-Fehler zurück. |
| `{filterDate}` | Dieser Parameter beschränkt die Ergebnisse auf die an einem bestimmten Datum verarbeiteten Ergebnisse. Sie akzeptiert das Format JJJJ-MM-TT. Das System kann auf die letzten 45 Tage zurückblicken. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine paginierte Liste aller Aufträge innerhalb einer Organisation ab, beginnend mit der dritten Seite mit einer Seitengröße von 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Aufträgen zurück, wobei jeder Auftrag Details wie z. B. seine `jobId` enthält. In diesem Beispiel würde die Antwort eine Liste von 50 Aufträgen enthalten, beginnend mit der dritten Ergebnisseite.

### Zugreifen auf nachfolgende Seiten

Um den nächsten Ergebnissatz in einer paginierten Antwort abzurufen, müssen Sie einen weiteren API-Aufruf an denselben Endpunkt ausführen, während Sie den Abfrageparameter `page` um 1 erhöhen.

## Erstellen eines Datenschutzauftrags {#create-job}

>[!IMPORTANT]
>
>Privacy Service ist nur für Anfragen der betroffenen Person und für Verbraucherrechtsanfragen vorgesehen. Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig. Adobe ist gesetzlich verpflichtet, diese rechtzeitig zu erfüllen. Daher sind Lasttests auf Privacy Service nicht zulässig, da es sich um eine reine Produktionsumgebung handelt und ein unnötiger Rückstand gültiger Datenschutzanfragen erzeugt wird.
>
>Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern. Für Benutzende, bei denen ein Missbrauch des Systems festgestellt wurde, wird der Zugriff auf den Dienst deaktiviert. Anschließend wird mit ihnen ein Meeting abgehalten, bei dem ihr Handeln und die akzeptable Verwendung von Privacy Service erörtert wird.

Bevor Sie eine neue Auftragsanfrage erstellen, müssen Sie zunächst identifizierende Informationen zu den betroffenen Personen erfassen, deren Daten Sie aufrufen, löschen oder für die Sie ein Opt-out aus dem Verkauf erwirken möchten. Sobald Sie über die erforderlichen Daten verfügen, müssen diese in der Payload einer POST-Anfrage an den `/jobs`-Endpunkt bereitgestellt werden.

>[!NOTE]
>
>Kompatible Adobe Experience Cloud-Anwendungen verwenden unterschiedliche Werte zur Identifizierung von betroffenen Personen. Weitere Informationen zu den erforderlichen Kennungen für Ihre Anwendungen finden [&#128279;](../experience-cloud-apps.md) im Handbuch zu Privacy Service- und Experience Cloud-Anwendungen. Allgemeine Anleitungen dazu, wie Sie festlegen, welche IDs an [!DNL Privacy Service] gesendet werden sollen, finden Sie im Dokument zu [Identitätsdaten in Datenschutzanfragen](../identity-data.md).

Die [!DNL Privacy Service]-API unterstützt zwei Arten von Vorgangsanfragen für personenbezogene Daten:

* [Zugriff und/oder Löschen](#access-delete): Zugriff (lesen) oder Löschen personenbezogener Daten.
* [Opt-out vom Verkauf](#opt-out): Markieren Sie persönliche Daten als nicht verkäuflich.

>[!IMPORTANT]
>
>Zugriffs- und Löschanfragen können zwar als einzelner API-Aufruf kombiniert werden, Opt-out-Anfragen müssen jedoch separat erfolgen.

### Erstellen eines Zugriffs-/Löschvorgangs {#access-delete}

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `companyContexts` **(Erforderlich)** | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Jeder aufgelistete Identifikator enthält die folgenden Attribute: <ul><li>`namespace`: Den Namensraum eines Identifikators.</li><li>`value`: Den Wert des Identifikators.</li></ul>Es ist **erforderlich** dass eine der Kennungen `imsOrgId` als `namespace` verwendet, wobei die `value` die eindeutige ID für Ihre Organisation enthält. <br/><br/>Zusätzliche IDs können produktspezifische Firmenqualifizierer sein (z. B. `Campaign`), die eine Integration mit einer Adobe-Anwendung Ihrer Organisation identifizieren. Mögliche Werte sind Kontonamen, Client-Codes, Mandanten-IDs oder andere Anwendungs-Identifikatoren. |
| `users` **(Erforderlich)** | Ein Array mit einer Sammlung von mindestens einem Benutzer, auf den Sie zugreifen, oder den Sie löschen möchten. In einer Anfrage können maximal 1.000 Benutzer angegeben werden. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-Identifikatoren in den Antwortdaten zu qualifizieren. Es gilt als Best Practice, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später einfach darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten auflistet. Je nach den Aktionen, die Sie ausführen möchten, muss dieses Array `access`, `delete` oder beide enthalten.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität besteht aus einem `namespace`, einem `value` und einem Namensraum-Qualifikator (`type`). Weitere Informationen zu diesen erforderlichen Eigenschaften finden Sie im [Anhang](appendix.md).</li></ul> Eine ausführlichere Erläuterung zu `users` und `userIDs` finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md#user-ids). |
| `include` **(Erforderlich)** | Eine Reihe von Adobe-Produkten, die in Ihre Verarbeitung einbezogen werden sollen. Wenn dieser Wert fehlt oder auf andere Weise leer ist, wird die Anfrage zurückgewiesen. Schließen Sie nur Produkte ein, mit denen Ihr Unternehmen eine Integration hat. Weitere Informationen finden Sie im Abschnitt zu den [anerkannten Produktwerten](appendix.md) im Anhang. |
| `expandIDs` | Eine optionale Eigenschaft, die bei Festlegung auf `true` eine Optimierung der Verarbeitung der IDs in den Programmen darstellt (derzeit nur von [!DNL Analytics] unterstützt). Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |
| `priority` | Eine optionale Eigenschaft, die von Adobe Analytics verwendet wird und die Priorität für die Verarbeitung von Anfragen festlegt. Die zulässigen Werte sind `normal` und `low`. Wenn keine `priority` angegeben wird, lautet das Standardverhalten `normal`. |
| `mergePolicyId` | Bei Datenschutzanfragen für das Echtzeit-Kundenprofil (`profileService`) können Sie optional die ID der spezifischen [Zusammenführungsrichtlinie) angeben](../../profile/merge-policies/overview.md) die Sie für die ID-Zuordnung verwenden möchten. Durch Angabe einer Zusammenführungsrichtlinie können Datenschutzanfragen beim Zurückgeben von Daten zu einem Kunden Zielgruppeninformationen enthalten. Pro Anfrage kann nur eine Zusammenführungsrichtlinie angegeben werden. Wenn keine Zusammenführungsrichtlinie angegeben ist, sind keine Segmentierungsinformationen in der Antwort enthalten. |
| `regulation` **(Erforderlich)** | Die Verordnung für den Datenschutzauftrag. Folgende Werte werden akzeptiert: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Weitere Informationen zu den Datenschutzbestimmungen, [ die oben genannten Werte darstellen, finden Sie in der Übersicht zu unterstützten ](../regulations/overview.md)&quot;. |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

Nachdem Sie die Auftragsanfrage erfolgreich gesendet haben, können Sie mit dem nächsten Schritt zur [Überprüfung des Auftragsstatus](#check-status) fortfahren.

## Status eines Auftrags überprüfen {#check-status}

Sie können Informationen zu einem bestimmten Auftrag abrufen, z. B. zum aktuellen Verarbeitungsstatus, indem Sie die `jobId` dieses Auftrags in den Pfad einer GET-Anfrage an den `/jobs`-Endpunkt aufnehmen.

>[!IMPORTANT]
>
>Daten für zuvor erstellte Aufträge können nur innerhalb von 30 Tagen nach dem Abschlussdatum des Auftrags abgerufen werden.

**API-Format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{JOB_ID}` | Die ID des Auftrags, den Sie suchen möchten. Diese ID wird unter `jobId` in erfolgreichen API-Antworten für „Erstellen [ Auftrags“ ](#create-job) „Auflisten [ Aufträge“ ](#list). |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft die Details des Auftrags ab, dessen `jobId` im Anfragepfad angegeben ist.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `productStatusResponse` | Jedes Objekt im `productResponses`-Array enthält Informationen zum aktuellen Status des Auftrags in Bezug auf eine bestimmte [!DNL Experience Cloud]. |
| `productStatusResponse.status` | Die aktuelle Statuskategorie des Auftrags. In der folgenden Tabelle finden Sie eine Liste der [verfügbaren Statuskategorien](#status-categories) und der entsprechenden Bedeutungen. |
| `productStatusResponse.message` | Der spezifische Status des Auftrags, der der Statuskategorie entspricht. |
| `productStatusResponse.responseMsgCode` | Ein Standardcode für Produktantwortnachrichten, die von [!DNL Privacy Service] empfangen werden. Die Details der Nachricht finden Sie unter `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Eine detailliertere Erklärung des Status des Vorgangs. Nachrichten mit ähnlichen Status können von Produkt zu Produkt variieren. |
| `productStatusResponse.results` | Für bestimmte Status geben einige Produkte möglicherweise ein `results`-Objekt zurück, das zusätzliche Informationen bereitstellt, die nicht von `responseMsgDetail` abgedeckt werden. |
| `downloadURL` | Ist der Auftragsstatus `complete`, stellt dieses Attribut eine URL zum Herunterladen der Auftragsergebnisse als ZIP-Datei bereit. Diese Datei kann bis zu 60 Tagen nach Abschluss des Auftrags heruntergeladen werden. |

{style="table-layout:auto"}

### Auftragsstatus-Kategorien {#status-categories}

In der folgenden Tabelle sind die verschiedenen möglichen Auftragsstatus-Kategorien und ihre entsprechende Bedeutung aufgeführt:

| Statuskategorie | Bedeutung |
| -------------- | -------- |
| `complete` | Der Auftrag ist abgeschlossen und (falls erforderlich) werden Dateien von jeder Anwendung hochgeladen. |
| `processing` | Anwendungen haben den Auftrag bestätigt und sind derzeit bei der Verarbeitung. |
| `submitted` | Der Auftrag wird bei allen anwendbaren Anwendungen eingereicht. |
| `error` | Bei der Verarbeitung des Auftrags ist etwas fehlgeschlagen – spezifischere Informationen können Sie durch Abrufen einzelner Auftragsdetails erhalten. |

{style="table-layout:auto"}

>[!NOTE]
>
>Ein übermittelter Auftrag kann im `processing` verbleiben, wenn er über einen abhängigen untergeordneten Auftrag verfügt, der noch verarbeitet wird.

## Nächste Schritte

Sie wissen jetzt, wie Sie Datenschutzaufträge mit der [!DNL Privacy Service]-API erstellen und überwachen. Informationen zum Ausführen derselben Aufgaben über die Benutzeroberfläche finden Sie in der [Privacy Service – UI-Übersicht](../ui/overview.md).
