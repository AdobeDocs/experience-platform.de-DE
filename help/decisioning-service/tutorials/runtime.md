---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Arbeiten mit der Laufzeit des Entscheidungsdienstes mithilfe von APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# Arbeiten mit der Laufzeit des Entscheidungsdienstes mithilfe von APIs

Dieses Dokument bietet eine Anleitung zum Arbeiten mit den Laufzeitdiensten des Entscheidungsdienstes mithilfe von Adobe Experience Platform-APIs.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der Experience Platform-Dienste, die bei der Entscheidungsfindung und der Festlegung des nächsten besten Angebots für die Präsentation während der Kundenerfahrung eine Rolle spielen. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für Folgendes:

- [Entscheidungsdienst](./../home.md): Bietet das Framework zum Hinzufügen und Entfernen von Angeboten und zum Erstellen von Algorithmen zur Auswahl der besten, die während des Kundenerlebnisses präsentiert werden sollen.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [Profil Abfrage Language (PQL)](../../segmentation/pql/overview.md): PQL wird zum Definieren von Regeln und Filtern verwendet.
- [Verwalten von Entscheidungsobjekten und Regeln mithilfe von APIs](./entities.md): Vor der Verwendung der Laufzeit der Entscheidungsdienste müssen Sie die entsprechenden Entitäten einrichten.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Plattform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../tutorials/authentication.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

Wird auch für Laufzeitanforderungen benötigt:

- x-request-id: `{UUID}`

>[!NOTE] `UUID` ist eine Zeichenfolge im UUUID-Format, die global eindeutig ist und nicht für verschiedene API-Aufrufe wiederverwendet werden darf.

Der Entscheidungsdienst wird von einer Reihe miteinander verbundener Geschäftsobjekte gesteuert. Alle Geschäftsobjekte werden im Business Object Repository der Plattform, XDM Core Object Repository, gespeichert. Eine wichtige Funktion dieses Repositorys ist, dass die APIs orthogonal zum Typ des Geschäftsobjekts sind. Statt eine POST-, GET-, PUT-, PATCH- oder DELETE-API zu verwenden, die den Typ der Ressource im API-Endpunkt angibt, gibt es nur 6 generische Endpunkte, die jedoch einen Parameter akzeptieren oder zurückgeben, der den Typ des Objekts angibt, wenn diese Unterscheidung erforderlich ist. Das Schema muss beim Repository registriert sein, darüber hinaus ist das Repository jedoch für einen Satz von Objekttypen mit offenem Ende einsetzbar.

Die Endpunktpfade für alle XDM Core Object Repository APIs Beginn mit `https://platform.adobe.io/data/core/ode/`.

Das erste Pfadelement nach dem Endpunkt ist der `containerId`. Diese Kennung wird über den XDM-Core-Objekt-Repository-Stammendpunkt abgerufen `GET https://platform.adobe.io/data/core/xcore/`.

## Zusammenstellung von Entscheidungsmodellen

Die Aktivierung der Business-Logik-Entitäten erfolgt automatisch und kontinuierlich. Sobald eine neue Option im Repository gespeichert und als &quot;genehmigt&quot;markiert ist, wird sie als Option zur Einbeziehung der verfügbaren Optionen angezeigt. Sobald eine Entscheidungsregel aktualisiert ist, wird der Regelsatz wieder zusammengestellt und für die Ausführung zur Laufzeit vorbereitet. Bei diesem Schritt der automatischen Aktivierung werden alle von der Geschäftslogik definierten Einschränkungen, die nicht vom Laufzeitkontext abhängen, ausgewertet. Die Ergebnisse dieses Aktivierung-Schritts werden an einen Cache gesendet, wo sie für die Laufzeit des Entscheidungsdienstes verfügbar sind.

### Auswirkungen von Platzierungen, Filtern und Lebenszyklusstatus

Angebot werden fortlaufend erstellt, Änderungen am Lebenszyklusstatus oder neue Inhaltsdarstellungen. Der Angebot-Filter einer Aktivität kann Angebot, deren Tag-Sets aktualisiert wurden, ändern, ergänzen oder herausfiltern. Dieser Prozess kann fair einbezogen werden, und die Bewerbungen und Dienste müssen wissen, wie die sich daraus ergebende Kandidatur einer Aktivität aussehen wird. Die Entscheidungslaufzeit bietet eine Aktivität-zu-Angebot-API, mit der Filter nicht genehmigte Angebot ausschließen, die nicht mit dem Angebot-Filter übereinstimmen oder für die Platzierung, auf die die Aktivität verweist, keine Darstellung haben.

**Anfrage**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Antwort**

Der Parameter `activityId` kann in der URL wiederholt werden und es können bis zu 30 verschiedene Aktivitäten in einer Anforderung angegeben werden. Die Antwort ist nützlich, um unerwartete Umstände zu erkennen, die sich aus der Einrichtung ergeben, und sieht wie folgt aus:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Zwischen der Aktualisierung der Objekte und dem Zeitpunkt, zu dem die API-Antwort die Zuordnung der Aktivität zu Angeboten widerspiegelt, gibt es eine kleine Verzögerung von einigen Sekunden. Die Revision der einzelnen Objekte wird in der Antwort angegeben, damit Kunden überprüfen können, ob eine Aktualisierung der Objekte vorliegt, die nicht übernommen wurden.

### Diagnose-API und Fehlerbehebung

Aktivitäten, Angebot und Eignungsregeln werden in ein internes Format (Laufzeit-Angebotskatalog) kompiliert, das von der Decision Service Runtime verwendet wird. Die Kompilierung kann Fehler erkennen, die nicht von den Prüfungen erfasst wurden, die durchgeführt wurden, als die Objekte gespeichert und Links im XDM-Core-Objekt-Repository eingerichtet wurden.

Es wird eine Diagnose-API bereitgestellt, um Kompilierungsfehler zu erhalten, die in diesem Schritt aufgetreten sind. Falls keine Fehler vorliegen, erhalten Sie Informationen zum Zeitpunkt der letzten Neukompilierung der Regeln und Aktivitäten.

**Anfrage**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

Der einzige Parameter für diesen API-Aufruf ist `containerId`. Das Ergebnis sind alle Aktualisierungen aller Clients, die Entscheidungsregeln, Angebot, Aktivitäten oder Angebot-Filter in diesem Container geändert haben. Zwischen dem Zeitpunkt der Aktualisierung der Objekte und dem Zeitpunkt, zu dem die Kompilierung abgeschlossen ist, gibt es eine kleine Verzögerung von einigen Sekunden. Der letzte Aktualisierungszeitstempel und alle Fehler werden in der Antwort auf den Diagnoseaufruf zurückgegeben.

**Antwort**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## REST-API-Aufrufe zum Ausführen von Entscheidungen

Die REST-API ist eine der Routen für Anwendungen, die auf der Plattform ausgeführt werden, um das nächste beste Erlebnis zu erhalten, das auf den Regeln, Modellen und Einschränkungen basiert, die das Unternehmen für seine Benutzer festgelegt hat. Anwendungen senden eine ID des Profils (Profil-ID und Identitäts-Namensraum), die der Entscheidungsdienst im Profil nachschlagen wird und die Informationen zur Anwendung der Geschäftslogik verwendet werden. Zusätzliche Kontextdaten können an die Anforderung übergeben werden. Wenn dies in den Geschäftsregeln angegeben ist, werden die Daten zur Entscheidungsfindung in die Daten aufgenommen.

Anwendungen können eine bessere Leistung erzielen, indem sie eine Entscheidung für bis zu 30 Aktivitäten gleichzeitig anfordern. Die URIs der Aktivitäten werden in derselben Anforderung übergeben. Die REST-API ist synchron und gibt die vorgeschlagenen Optionen für alle diese Aktivitäten oder die Ausweichoption zurück, wenn keine Personalisierungsoption die Einschränkungen erfüllt.

Es ist möglich, dass zwei verschiedene Aktivitäten die gleiche Option wie ihre &quot;Besten&quot;haben. Um zu vermeiden, dass sich ein zusammengesetztes Erlebnis wiederholt, werden beim Entscheidungsdienst standardmäßig zwischen den Aktivitäten, auf die in derselben Anforderung verwiesen wird, Schiedsverfahren angewendet. Die Schiedsgerichtsbarkeit bedeutet, dass für jede Aktivität ihre Top-N-Optionen in Betracht gezogen werden, dass aber über diese Aktivitäten hinweg keine Möglichkeit mehr als einmal vorgeschlagen wird. Wenn zwei Aktivitäten die gleiche Option mit der höchsten Rangfolge haben, wird eine von ihnen gewählt, um ihre zweitbeste oder drittbeste Wahl usw. zu verwenden. Diese Deduplizierungsregeln versuchen zu vermeiden, dass eine der Aktivitäten ihre Ausweichmöglichkeit nutzen muss.

Der Entscheidungsantrag enthält die Argumente, die der Hauptteil eines POST-Antrags enthält. Der Haupttext wird als JSON- `Content-Type` Kopfzeilenwert formatiert `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

Das Anforderungs-Schema und die derzeit unterstützte Version werden `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`unterstützt. Zukünftig werden zusätzliche Anforderungs-Schema oder -Versionen bereitgestellt.

**Anfrage**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Wenn der Wert dieser optionalen Eigenschaft auf &quot;true&quot;gesetzt ist, wird der Entscheidungsantrag Beschränkungen der Deckelung unterliegen, diese Zähler aber nicht wirklich abziehen, ist es die Erwartung, dass der Aufrufer das Angebot nie dem Profil vorlegen will. Der Entscheidungsdienst zeichnet den Vorschlag nicht als offizielles XDM-Entscheidungsinstrument auf und wird nicht in den Berichte-Datensätzen angezeigt. Der Standardwert dieser Eigenschaft ist &quot;false&quot;. Wenn die Eigenschaft weggelassen wird, gilt die Entscheidung nicht als Testlauf und wird daher dem Endbenutzer vorgelegt.
- **`xdm:validateContextData`** - Diese optionale Eigenschaft aktiviert bzw. deaktiviert die Überprüfung der Kontextdaten. Wenn die Überprüfung aktiviert ist, wird für jedes angegebene Kontextdatenelement das Schema (basierend auf dem `@type` Feld) aus der XDM-Registrierung abgerufen und das `xdm:data` Objekt wird dafür validiert.

Die Anforderung nach diesem Schema enthält ein Array von URIs, die auf Angebot-Aktivitäten, eine Profil-ID und ein Array mit Kontextdatenelementen verweisen:

- **`xdm:offerActivities`** - Diese obligatorische Eigenschaft ist ein Array von Objekten, bei denen jedes Element Daten zur Angebot-Aktivität enthält. Die Angebot-Aktivität verfügt über die folgenden Eigenschaften:
   - **`xdm:offerActivity`** - Der eindeutige Bezeichner (URI) der Aktivität. Dies ist der Wert der `@id` Eigenschaft der Angebot-Aktivität.
- **`xdm:identityMap`** - Eine obligatorische Eigenschaft mit einem JSON-Objekt, das dem XDM-Schema entspricht `https://ns.adobe.com/xdm/context/identitymap`. Die Eigenschaft definiert eine Zuordnung, bei der der Schlüssel ein Identitäts-Namensraum-Code und der Wert eine Liste von Endbenutzer-IDs im angegebenen Namensraum ist. Wenn m.
- **`xdm:contextData`** - Eine optionale Eigenschaft, die Elemente enthält, die durch einen Verweis auf ihr Schema beschrieben werden. Jedes Kontextdatenelement im Array muss die folgenden Eigenschaften aufweisen:
   - **`@type`** - Eine obligatorische Eigenschaft, die auf das XDM-Schema des Objekts in diesem Element verweist.
   - **`xdm:data`** - Eine obligatorische Eigenschaft, die die Objekteigenschaften gemäß dem XDM-Schema enthält, das in der `@type` Eigenschaft angegeben ist.

## Dynamische Kontextdaten bei der Entscheidung von Anforderungen

Im vorherigen Abschnitt wurde angegeben, wie XDM-Objekte an eine Entscheidungsanforderung übergeben werden können. Das folgende Beispiel zeigt ein solches context-object-Array:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Das Schema muss von Ihrem Unternehmen erstellt worden sein. Weitere Informationen zum Erstellen von Schemas finden Sie im [Schema Editor Tutorial](../../xdm/tutorials/create-schema-ui.md). Dein Schema wird in einem Namensraum sein `https://ns.adobe.com/{TENANT_ID}/schemas`.

Im Entwicklerhandbuch für die [Schema Registry API wird erläutert](../../xdm/tutorials/create-schema-api.md) , wie auf Schema programmgesteuert zugegriffen werden kann und wie ein Entwickler die Mandant-ID und die numerische ID Ihres Schemas erhält. Die Versionsnummer ist erforderlich und wird auch von den Schema-Registrierungs-APIs bereitgestellt.

Ein von einem Unternehmen definiertes Schema hat in der Regel eine Stammeigenschaft mit dem Namen `_{TENANT_ID}`, die auch als Namensraum-Zeichenfolge des Mandanten bezeichnet wird.
Beachten Sie, dass die von einer globalen Schema-Komponente wie _`https://ns.adobe.com/xdm/context/product` verwendeten Eigenschaften ein Namensraum-Präfix haben `xdm:`. In diesem Fall `productDetails` wurde die von der Organisation definierte Eigenschaft mit diesem Datentyp erstellt. Während Pätnereigenschaften in einer Eigenschaft verschachtelt sind, die nach dem Pächter-Namensraum benannt ist, verwenden global verfügbare Datentypen das reservierte Präfix, `xdm:` um Zusammenstöße von Eigenschaftsnamen zu verhindern.

In der `xdm:contextData` Eigenschaft können mehrere Datenobjekte aufgeführt werden. Jedes Objekt muss seinen Typ über die `@type` Eigenschaft identifizieren.
Die Werte der Kontextdatenobjekte können in PQL-Ausdrücken verwendet werden, z. B. im Zustand einer Eignungsregel. Das Kontextdatenobjekt muss über den speziellen Pfad-Referenz-Ausdruck adressiert werden `@{schemaId}`. Die Ausdruck, die diesem Referenz-Ausdruck folgen, sind Ausdruck mit regulären Pfaden, die auf die Eigenschaften des Datenobjekts zugreifen:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Im obigen Beispiel `p` iteriert die Variable über das Array von Objekten, die mit dem `@type` = gekennzeichnet waren `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Beachten Sie, dass die PQL-Syntax keine Präfixe in Eigenschaftsnamen verwendet. Globale Eigenschaften werden standardmäßig ohne das `xdm:` Präfix referenziert. Eigenschaften, die Ihr Unternehmen definiert, sind innerhalb einer **zusätzlichen** Eigenschaft verschachtelt, die nach dem Namensraum des Mandanten benannt ist (in dem Beispiel, das durch die Variable angegeben wird `{TENANT_ID}`). Um direkt auf die benutzerdefinierten Eigenschaften verweisen zu können, `p` ist die Variable an das Ergebnis des Pfads gebunden, der die zusätzliche Verschachtelungseigenschaft abhebt.

## Verwendung der Profil-Aufzeichnungen

Alle Datensätze für Profil- und Experience Ereignis-Entitäten werden bereits im Profil Store verwaltet. Durch Übergabe einer oder mehrerer Profil-ID an die Anforderung wird das Profil für diese Identitäten identifiziert und vom Store nachgeschlagen. Die Daten stehen dann automatisch für die von der Entscheidungsstrategie evaluierten Entscheidungsregeln und Modelle zur Verfügung.

Zum Abrufen der Profil- und Erlebnisdatensätze wird die standardmäßige Zusammenführungsrichtlinie angewendet.
Beachten Sie, dass es nach dem Hochladen von Profil-Datensätzen in den Platform-Datensatz eine leichte Verzögerung gibt, bis die Profil-Datensätze nachgeschlagen werden können. Dasselbe gilt für die Erfassung von Profil- und Erlebnisdatensätzen über die Streaming-APIs, und erst nach wenigen Sekunden stehen die Daten zur Bewertung von Entscheidungsregeln zur Auswertung von Profil- und Erlebnis-Ereignis-Daten zur Verfügung.