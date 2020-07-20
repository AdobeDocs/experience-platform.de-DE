---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verwalten von Decisioning Service-Entitäten mithilfe von APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '7207'
ht-degree: 96%

---


# Verwalten von Decisioning-Objekten und -Regeln mithilfe von APIs

This document provides a tutorial for working with the business entities of [!DNL Decisioning Service] using Adobe Experience Platform APIs.

Die Anleitung besteht aus zwei Teilen:

- Generische Repository-APIs zum Verwalten von Geschäftsobjekten werden im [ersten Teil](#managing-repository-entities-using-apis) vorgestellt. Diese APIs sind in dem Sinne generisch, dass sie Funktionen zum Erstellen, Lesen, Aktualisieren, Löschen und Suchen **beliebiger** Geschäftsobjekte bereitstellen. Das generische API-Modell wird beschrieben und die Beziehung zur Hypertext Application Language (HAL) erklärt.

- Auf Basis der Kenntnisse zu den Repository-APIs konzentriert sich der [zweite Teil](#creating-and-managing-offer-decisioning-entities-using-apis) auf die Geschäftsentitäten, die über die Repository-APIs verwaltet werden. Bei Anwendung derselben APIs besteht der einzige Unterschied beim Verwalten von zwei verschiedenen Entitäten (wie Aktivität und Geschäftsregel) in der Anfrage- und Antwort-Payload. Hinzu kommen die erforderlichen Kopfzeilenwerte, die den verwalteten Objekttyp angeben.

## Erste Schritte

This tutorial requires a working understanding of the [!DNL Experience Platform] services and the API conventions. The [!DNL Platform] repository is a service used by several other [!DNL Platform] services to store business objects and various types of metadata. Es bietet eine sichere und flexible Möglichkeit, diese Objekte zu verwalten und für unterschiedliche Laufzeitdienste abzufragen. The [!DNL Decisioning Service] is one of those. Bevor Sie mit dieser Anleitung beginnen, lesen Sie bitte die Dokumentation für Folgendes:

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [!DNL Decisioning Service](./../home.md): Beschreibt die Konzepte und Komponenten, die für Erlebnisentscheidungen im Allgemeinen und Angebotsentscheidungen im Speziellen verwendet werden. Veranschaulicht die Strategien zur Auswahl der besten Option, die während eines Kundenerlebnisses angezeigt wird.
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL ist eine leistungsstarke Sprache, um Ausdruck über XDM-Instanzen zu schreiben. PQL wird zur Definition von Entscheidungsregeln verwendet.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: application/json

## Konventionen der Repository-API

[!DNL Decisioning Service] wird von einer Reihe miteinander verbundener Geschäftsobjekte gesteuert. All business objects are stored in the [!DNL Platform’s] Business Object Repository. Ein wichtiges Merkmal dieses Repositorys ist, dass die APIs orthogonal zum Typ des Geschäftsobjekts sind. Statt eine POST-, GET-, PUT-, PATCH- oder DELETE-API zu nutzen, die den Typ der Ressource im API-Endpunkt angibt, gibt es nur sechs generische Endpunkte. Diese akzeptieren oder geben jedoch einen Parameter zurück, der den Typ des Objekts angibt, wenn eine Unterscheidung erforderlich ist. Das Schema muss beim Repository registriert sein; darüber hinaus ist das Repository jedoch für einen beliebigen Satz von Objekttypen einsetzbar.

Zusätzlich zu den oben aufgeführten Kopfzeilen gelten folgende Konventionen für die APIs zum Erstellen, Lesen, Aktualisieren, Löschen und Abfragen von Repository-Objekten:

- Die Endpunktpfade beginnen bei allen Repository-APIs mit `https://platform.adobe.io/data/core/xcore/`.

API-Payload-Formate werden mit einer `Accept`- oder `Content-Type`-Kopfzeile ausgehandelt. Nachrichtenformate in der Kopfzeile `Accept` oder `Content-Type` werden durch einen Wert `application/vnd.adobe.platform.xcore.{FORMAT}+json` angegeben, bei dem {FORMAT} von der spezifischen Anfrage- oder Antwortnachricht der Repository-API abhängt (gemäß der folgenden Tabelle).

| FORMAT-Variante | Beschreibung der Anfrage- oder Antwortentität |
| --- | --- |
| <br>, gefolgt von einem Parameter `schema={schemaId}` | Die Nachricht enthält eine Instanz, die von einem JSON-Schema beschrieben wird, das durch das Formatparameterschema angegeben wird. Die Instanz ist in eine JSON-Eigenschaft-`_instance` eingeschlossen. Die anderen Eigenschaften der obersten Ebene in der Antwort-Payload geben Repository-Daten an, die für alle Ressourcen verfügbar sind.  Nachrichten, die dem HAL-Format entsprechen, haben eine `_links`-Eigenschaft, die Verweise im HAL-Format enthält. |
| `patch.hal` | Die Nachricht enthält eine JSON PATCH-Payload unter der Annahme, dass die Instanz, die gepatcht werden soll, HAL-konform ist. Das bedeutet, dass nicht nur die eigenen Instanzeigenschaften der Instanz, sondern auch die HAL-Verknüpfungen der Instanz gepatcht werden können. Beachten Sie, dass beschränkt ist, welche Eigenschaften vom Client aktualisiert werden können. |
| `home.hal` | Die Nachricht enthält eine JSON-formatierte Darstellung einer Startdokumentressource für das Repository. |
| xdm.receipt | Die Nachricht enthält eine JSON-formatierte Antwort für einen Vorgang zum Erstellen, Aktualisieren (Voll und Patch) oder Löschen. Receipts enthalten Kontrolldaten, die die Revision der Instanz in Form eines ETag angeben. |

Die Verwendung der einzelnen **Formatvarianten** hängt von der jeweiligen API ab:

| API | Content-Type-Kopfzeile | Accept-Kopfzeile |
| --- | --- | --- |
| Instanz löschen <br/>Container erstellen | `hal`<br/> mit Schemaparameter | `xdm.receipt` |
| Instanz aktualisieren<br/>Container aktualisieren | `hal`<br/> mit Schemaparameter | `xdm.receipt` |
| Instanz patchen | `patch.hal` | `xdm.receipt` |
| Instanz löschen<br/>Container löschen | K. A. | `xdm.receipt` |
| Instanz lesen<br/>Container lesen | K. A. | `hal` mit `schema`-Parameter |
| Instanzen auflisten<br/>Container auflisten | K. A. | `hal` mit speziellem `schema`-Parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Instanzen suchen | K. A. | hal mit speziellem `schema`-Parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Repository-Stamm lesen | K. A. | `home.hal` |

Für die APIs zum Erstellen, Aktualisieren und Lesen von Containern hat das Formatparameterschema den Wert `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` ist der erste Pfadparameter für die Instanz-APIs. Alle Geschäftsentitäten befinden sich in einem so genannten Container. Ein Container ist ein Isolationsmechanismus, der unterschiedliche Aufgaben voneinander trennt. Das erste Pfadelement für die Repository-Instanz-APIs nach dem allgemeinen Endpunkt ist die `containerId`. Die Kennung wird aus der Liste der Container abgerufen, auf die der Aufrufer zugreifen kann. Beispielsweise ist die API zum Erstellen einer Instanz in einem Container `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

Die Liste zugänglicher Container wird mit einer HTTP GET-Anfrage durch Aufruf des Repository-Stammendpunkts „/“ unter Verwendung der Standardkopfzeilen abgerufen.

## Zugriff auf Container verwalten

Ein Administrator kann ähnliche Prinzipale, Ressourcen und Zugriffsberechtigungen in Profilen gruppieren. Dies verringert den Verwaltungsaufwand und wird von der [Benutzeroberfläche von Adobe Admin Console](https://adminconsole.adobe.com) unterstützt. Sie müssen Produktadministrator für die Adobe Experience Platform in Ihrem Unternehmen sein, um Profil zu erstellen und ihnen Benutzer zuzuweisen.

Es reicht aus, in einem einmaligen Schritt Produktprofile einzurichten, die bestimmten Berechtigungen entsprechen, und diesen Profilen dann einfach Benutzer hinzuzufügen. Profile dienen als Gruppen, denen Berechtigungen erteilt wurden; alle echten Benutzer oder technischen Benutzer in dieser Gruppe erben diese Berechtigungen.

### Container auflisten, die für Benutzer und Integrationen zugänglich sind

Wenn der Administrator normalen Benutzern oder Integrationen Zugriff auf Container gewährt hat, werden diese Container in der so genannten „Home“-Liste des Repositorys angezeigt. Die Liste kann bei verschiedenen Benutzern oder Integrationen unterschiedlich ausfallen, da sie eine Untergruppe aller Container ist, auf die der Aufrufer zugreifen kann. Die Liste der Container kann anhand ihrer Verbindung zu Produktkontexten gefiltert werden. Der Filterparameter heißt `product` und kann wiederholt werden. Wenn mehr als ein Produktkontextfilter angegeben ist, wird die Vereinigung der Container zurückgegeben, die mit beliebigen der angegebenen Produktkontexte verbunden sind. Beachten Sie, dass ein Container mehreren Kontexten zugeordnet sein kann.

Der Kontext für die [!DNL Platform] Container ist derzeit [!DNL Decisioning Service] `dma_offers`.

>[!NOTE]
>
>Der Kontext für [!DNL Platform Decisioning Containers] wird sich bald ändern `acp`. Filterung ist optional, aber Filter nur anhand von `dma_offers` müssen bei einer zukünftigen Version bearbeitet werden. Zur Vorbereitung auf diese Änderung sollten Kunden keine Filter verwenden oder beide Produktkontexte als Filter anwenden.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Antwort**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Notieren Sie sich die in den resultierenden Elementen aufgelistete `instanceId`. Sie dient in den APIs zum Lesen und Bearbeiten regulärer Geschäftsobjekte als `containerId`-Parameter.

Die Liste wurde bereits anhand von Zugriffsberechtigungen nach Benutzern gefiltert, kann aber durch eine Eigenschaftsabfrage weiter gefiltert werden.

## Generische APIs zum Verwalten von Entitäten

### Instanzen erstellen

Die API zum Erstellen einer neuen Instanz im Repository verwendet einen `containerId`-Pfadparameter und gibt mit dem Schemaparameter den Instanztyp in der `Content-Type`-Kopfzeile an.

Die Instanzeigenschaften sind in der Payload angegeben, eingeschlossen in der `_instance`-Eigenschaft. Die Instanzeigenschaften müssen für das JSON-Schema mit der angegebenen Schemakennung gültig sein.

Die HAL-`_links`-Eigenschaft muss vorhanden sein, darf jedoch leer sein. Das bedeutet, dass für diese Instanz keine benutzerspezifischen Links definiert sind.

**Anfrage**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Antwort**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

Die Antwort enthält die instanceId des soeben erstellten Objekts. Diese instanceId ist unveränderlich, wird immer vom Repository zugewiesen und ist global eindeutig. Der Wert dient als physische Kennung.

Darüber hinaus wird in der Eigenschaft `@id` der Antwort-Payload ein URI (Universal Resource Identifier) zurückgegeben, wenn das Schema über eine solche Eigenschaft verfügt. Jede Instanz sollte über eine Eigenschaft verfügen, die als URI und Primärschlüssel der Instanz dient. Diese Kennung wird von anderen Instanzen verwendet, um Beziehungen zur neuen Instanz herzustellen, auch über verschiedene Typen hinweg. In der aktuellen Version werden die URIs vom Repository generiert und sind in der `@id`-Eigenschaft enthalten. Zukünftige Versionen können diese Regel lockern und es Kunden ermöglichen, eigene URI-Werte zu verwalten und die Eigenschaft zu benennen, die sie enthält.

Beachten Sie, dass diese URIs keine URLs sind und keine Möglichkeit bieten, die Ressource direkt abzurufen. Um darauf hinzuweisen, wird dem URI ein URI-Schema vorangestellt, das kein Abrufprotokoll angibt. Die URIs können jedoch mit einer Abfrage zum Nachschlagen der Instanz verwendet werden.

Die REST-Antwort verfügt über eine Location-Kopfzeile, die eine URL-Komponente enthält, mit der die soeben erstellte Instanz abgerufen werden kann. Diese Komponente ist eine relative URI-Referenz und muss auf den Basis-URI des Repositorys angewendet werden. Der Basis-URI wird in der `Content-Base`-Kopfzeile zurückgegeben.

Die `repo:etag`-Eigenschaft gibt die Revision der Instanz an. Dieser Wert kann bei Aktualisierungsvorgängen verwendet werden, um Konsistenz zu erzwingen. Die HTTP-Kopfzeile `If-Match` kann genutzt werden, um einem PUT- oder PATCH-API-Aufruf eine Bedingung hinzuzufügen; sie stellt sicher, dass keine anderen Änderungen an der Instanz vorgenommen wurden, die sonst versehentlich überschrieben werden könnten. Der `repo:etag`-Wert wird bei jedem Aufruf zum Erstellen, Lesen, Aktualisieren, Löschen und Abfragen zurückgegeben. Der Wert wird als Wert in der ` If-Match`-Kopfzeile gemäß [RFC7232 Abschnitt 3.1](https://tools.ietf.org/html/rfc7232#section-3.1)verwendet.

Die übrigen Eigenschaften geben an, welches Konto und welcher API-Schlüssel zum Erstellen und letzten Ändern der Instanz verwendet wurden. Da die Instanz durch diesen Aufruf erstellt wurde, sind die entsprechenden Werte die der Anfrage.

### Instanz anhand von Kennung nachschlagen

Mithilfe der URL in der Location-Kopfzeile, die beim Aufruf zum Erstellen zurückgegeben wurde, kann eine Anwendung eine Instanz nachschlagen.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Obwohl `instanceId` als Pfadparameter angegeben ist, sollten Anwendungen den Pfad nach Möglichkeit nicht selbst erstellen und stattdessen Links zu Instanzen in Auflistungs- und Suchvorgängen folgen. Einzelheiten finden Sie in den Abschnitten ‎6.4.4 und ‎6.4.6.

**Antwort**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Die JSON-Eigenschaften der Instanz sind in die `_instance`-Eigenschaft eingeschlossen und die anderen Eigenschaften auf der Stammebene enthalten Metadaten zur Instanz.

Die Ressource enthält auch ein Array von JSON-Schemakennungen. Dieses Array zeigt die JSON-Schemas an, für die diese Instanz validiert wird.

Jede Instanz enthält einen HAL-Link des Verhältnistyps „selbst“, der dem IANA-registrierten Selbstverhältnis entspricht (wie in [RFC5988] definiert).

**Testen auf neuere Revisionen einer Instanz**

Der aktuelle `eTag`-Wert der Instanz wird mit der Antwort zurückgegeben. So können Clients bedingte Vorgänge für die Instanz auszuführen, um entweder zu vermeiden, dass der gleiche Ressourcenstatus erneut abgerufen wird, oder um zu verhindern, dass die Werte einer späteren Revision ohne Wissen des Clients überschrieben werden.

Mit der Lookup-API kann ein Client einen `If-None-Match`-Kopfzeilenparameter angeben. Siehe Definition für diesen standardmäßigen HTTP-Parameter [RFC2616]. Der Entitäts-Tag-Wert, den ein Client angibt, ist der Wert, den er mit der letzten Antwort erhalten hat – von einem API-Aufruf zum Aktualisieren, Lesen, Auflisten oder Suchen. Beachten Sie, dass der `etag`-Wert für den Client opak sein sollte und als Zeichenfolge, umgeben von Anführungszeichen, angegeben werden muss.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

Die Repository-API reagiert mit dem Status „304 Nicht geändert“, wenn die letzte Revision der Instanz die mit dem angegebenen eTag-Wert ist.

### Instanzen für ein Schema auflisten – Sortieren und Paginieren

Clients können die Instanzen, die sie erstellen, nicht verfolgen und greifen daher über deren physische instanceId auf sie zu. Die Verwendung der Read Instance-API bildet eine Ausnahme. Clients wissen auch nicht, welche Instanzen andere Clients erstellt haben.

Ein typischeres Zugriffsmuster besteht im Paginieren durch den Satz aller Instanzen.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwort**

Die Antwort hängt von der angegebenen `{schemaId}` ab. Bei „https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73“ ähnelt die Antwort beispielsweise Folgendem:

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>Das Ergebnis enthält die Instanzen für das angegebene Schema oder die erste Seite dieser Liste. Beachten Sie, dass Instanzen mehr als einem Schema entsprechen und daher in mehr als einer Liste angezeigt werden können.

Seitenressourcen sind vorübergehend und schreibgeschützt; sie können weder aktualisiert noch gelöscht werden. Das Seitenmodell bietet zufälligen Zugriff auf Teilmengen großer Listen über einen längeren Zeitraum hinweg, ohne dass irgendein Status pro Client beibehalten wird.

Um so anhand von Seiten auf eine Instanzliste zugreifen zu können, muss es möglich sein, eine stabile Sortierung für die von dieser Instanzliste aufgeführten Einträge zu definieren. Beachten Sie, dass „stabil“ nicht bedeutet, dass Instanzen auf einer vordefinierten Seite angezeigt werden. Wenn eine Seitenreihenfolge durch Sortieren von Instanzen gemäß einer Eigenschaft P gebildet wird und ein Client diese Eigenschaft P aktualisiert, kann ein anderer Client diese Instanz ggf. erneut auf einer anderen Seite erreichen, während er durch die Liste blättert. Mit anderen Worten: Das Modell bevorzugt die Rückgabe aktuellerer Ergebnisse.

Wenn die Sortierreihenfolge jedoch auf einer nicht änderbaren Eigenschaft basiert, garantiert eine „stabile“ Sortierreihenfolge, dass alle Instanzen, die zu Beginn des Seitenvorgangs vorhanden waren, erreicht werden (es sei denn, sie wurden bis zum Erreichen ihrer Seite gelöscht). Befindet sich diese Sortierreihenfolge in einer Eigenschaft, die monoton zunimmt, werden auch Instanzen erreicht, die nach dem Starten des Paginierungsvorgangs erstellt wurden.

Ein Client kann Hinweise zur gewünschten Seitengröße geben, aber es liegt ganz am Repository, mehr oder weniger Instanzen auf der zurückgegebenen Seite aufzuführen. Um eine stabile Reihenfolge zu gewährleisten, muss der Dienst Elemente der Seite hinzufügen oder von der Seite entfernen, damit der Wert der Sortiereigenschaft über Seitengrenzen hinweg unterschiedlich ist. So enthält die nächste Seite keine Elemente der letzten Seite mehr oder bleibt im schlimmsten Fall mit den denselben Elemente auf jeder Seite hängen.

Das Paginieren wird durch folgende Parameter gesteuert:

- **`orderBy`**: Enthält eine kommagetrennte, geordnete Liste mit Eigenschaften, anhand der die Instanzliste sortiert wird. Die erste Eigenschaft wird für die primäre Sortierung verwendet, die zweite Eigenschaft zum Auflösen von Gleichständen in der primären Sortierung usw. Wenn eine Eigenschaft angegeben wird, die einen eindeutigen Wert pro Instanz hat, sind keine Gleichstände möglich und kann nach jedem Element ein Seitenumbruch erfolgen. Dem Namen einer Eigenschaft kann ein `+`, um aufsteigende Reihenfolge anzugeben, oder ein `-`, um absteigende Reihenfolge anzugeben, vorangestellt werden. Wenn dem Eigenschaftsnamen nichts vorangestellt ist, wird das Ergebnis in aufsteigender Reihenfolge sortiert. Wenn `orderBy` in der Anfrage nicht angegeben ist, nutzt das Repository stattdessen die physische instanceId-Eigenschaft.
- **`start`**: Clients verwenden den Startparameter, um die Seite zu definieren, die sie abrufen möchten. Der Startparameter bestimmt den Anfang der gewünschten Seite. Die Antwort enthält Instanzen, die mit jenen beginnen, die über einen `orderBy`-Eigenschaftswert verfügen, der strikt größer ist als (für aufsteigende Werte) oder strikt kleiner ist als (für absteigende Werte) der angegebene Wert. Wenn der Abfrageparameter nicht angegeben ist, wird standardmäßig ein instanceId-Wert genutzt, der vor der erstmöglichen Instanzkennung sortiert. Daher wird dieser Wert auf der ersten Seite weggelassen.
- **`limit`**: Gibt eine positive Ganzzahl als Hinweis auf die maximale Anzahl von Elementen an, die für eine bestimmte Anfrage zurückgegeben werden soll. Die tatsächliche Antwortgröße kann kleiner oder größer sein, da ein zuverlässiges Funktionieren des Startparameters erforderlich ist.

### Filtern von Listen

Das Filtern von Listen ist möglich und erfolgt unabhängig vom Paginierungsverfahren. Filter überspringen einfach Instanzen in der Reihenfolge der Listen oder schließen explizit nur Instanzen ein, die eine bestimmte Bedingung erfüllen. Ein Client kann die Verwendung des Eigenschaftsausdrucks als Filter anfordern oder eine Liste von URIs angeben, die als Werte des Primärschlüssels der Instanzen verwendet werden sollen.

- **`property`**: Enthält einen Eigenschaftsnamenpfad gefolgt von einem Vergleichsoperator gefolgt von einem Wert. <br/>
Die zurückgegebene Liste von Instanzen enthält die Instanzen, bei denen der Ausdruck „true“ ergibt. Angenommen, die Instanz verfügt über eine Payload-Eigenschaft 
`status` und die möglichen Werte sind `draft`, `approved``archived` und `deleted` `property=_instance.status==approved` dann gibt der Parameter Abfrage nur Instanzen zurück, für die der Status genehmigt wurde. <br/>
<br/>
Die Eigenschaft, die mit dem angegebenen Wert verglichen werden soll, wird als Pfad angegeben. Die einzelnen Pfadkomponenten werden durch „.“ wie folgt getrennt: „_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1“<br/>.

Für Eigenschaften mit Zeichenfolgen-, numerischen oder Datums-/Uhrzeitwerten sind folgende Operatoren zulässig: `==`, `!=`, `<`, `<=`, `>` und `>=`. Darüber hinaus kann für Eigenschaften mit einem Zeichenfolgenwert ein `~`-Operator verwendet werden. Der `~`-Operator stimmt die angegebene Eigenschaft anhand eines regulären Ausdrucks ab. Der Zeichenfolgenwert der Eigenschaft muss mit dem **gesamten** Ausdruck übereinstimmen, damit die Entitäten in die gefilterten Ergebnisse einbezogen werden. Wenn Sie beispielsweise an einer beliebigen Stelle im Eigenschaftswert nach der Zeichenfolge `cars` suchen, muss der reguläre Ausdruck `.*cars.*` vorhanden sein. Ohne vorstehendes oder nachstehendes `.*` werden nur Entitäten gefunden, bei denen ein Eigenschaftswert mit `cars` beginnt oder endet. Beim `~`-Operator unterscheidet der Vergleich von Buchstaben nicht zwischen Groß- und Kleinschreibung. Bei allen anderen Operatoren wird beim Vergleich zwischen Groß- und Kleinschreibung unterschieden.<br/><br/>
In Filterausdrücken können nicht nur Payload-Eigenschaften von Instanzen verwendet werden. Umschlageigenschaften werden auf die gleiche Weise verglichen, z. B. `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Der Abfrageparameter `property` kann wiederholt werden, sodass mehrere Filterbedingungen angewendet werden, z. B. um alle Instanzen zurückzugeben, die nach einem bestimmten Datum und vor einem bestimmten Datum zuletzt geändert wurden. Die Werte in diesen Ausdrücken müssen URL-codiert sein. Wenn kein Ausdruck angegeben ist und der Name der Eigenschaft einfach aufgelistet ist, sind die Elemente qualifiziert, die eine Eigenschaft mit dem angegebenen Namen aufweisen.<br/>
<br/>

- **`id`**: Manchmal muss eine Liste anhand des URI der Instanzen gefiltert werden. Der Abfrageparameter `property` kann verwendet werden, um eine Instanz herauszufiltern. Um jedoch mehr als eine Instanz zu erhalten, kann der Anfrage eine Liste von URIs übergeben werden. Der Parameter `id` wird wiederholt; bei jedem Vorkommen wird ein URI-Wert (`id={URI_1}&id={URI_2},…`) angegeben. Die URI-Werte müssen URL-codiert sein.

Seitenergebnisse werden als spezieller MIME-Typ (`application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`) zurückgegeben.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwort**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

Die Antwort enthält die Liste der Ergebniselemente in den Ergebnissen der JSON-Eigenschaft neben zwei Eigenschaften, die die Anzahl der Ergebnisse auf dieser Seite und die Gesamtzahl der Elemente in der gefilterten Liste angeben, beginnend mit der soeben zurückgegebenen Seite.

### Volltextsuche und strukturierte Abfragen

Für Fälle, in denen Clients komplexere Filterbedingungen verwenden und Instanzen nach Begriffen, die in Zeichenfolgeneigenschaften enthalten sind, durchsuchen möchten, stellt das Repository eine leistungsfähigere Such-API bereit.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Zusätzlich zu den Seiten- und Filterparametern aus den Auflistungs-APIs ermöglicht diese API Clients das Hinzufügen von Volltext- und booleschen Abfrageparametern.

Die Volltextsuche wird durch die folgenden Parameter gesteuert:

- **`q`**: Enthält eine durch Leerzeichen getrennte, ungeordnete Liste von Begriffen, die normalisiert werden, bevor sie mit Zeichenfolgeneigenschaften der Instanzen abgeglichen werden. Zeichenfolgeneigenschaften werden auf Begriffe analysiert; diese Begriffe werden ebenfalls normalisiert. Die Suchabfrage versucht, einen oder mehrere der im `q` Parameter angegebenen Begriffe abzugleichen. Die Zeichen +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, :, / haben eine besondere Bedeutung für die Bestimmung der Wortgrenzen in der Abfragezeichenfolge und sollten beim Auftreten in einem Token, das mit dem Zeichen übereinstimmen soll, mit einem umgekehrten Schrägstrich versehen werden. Die Abfragezeichenfolge kann für exakte Zeichenfolgenübereinstimmungen und das Escaping von Sonderzeichen in doppelte Anführungszeichen eingeschlossen werden.
- **`field`**: Wenn die Suchbegriffe nur mit einer Untergruppe der Eigenschaften übereinstimmen sollen, kann der Feldparameter den Pfad zu dieser Eigenschaft angeben. Der Parameter kann wiederholt werden, um mehr als eine Eigenschaft anzugeben, die abgeglichen werden soll.
- **`qop`**: Enthält einen Steuerungsparameter, mit dem das Trefferverhalten der Suche geändert wird. Wenn der Parameter auf „and“ gesetzt ist, müssen alle Suchbegriffe übereinstimmen; wenn der Parameter fehlt oder sein Wert auf „or“ gesetzt ist, können beliebige Begriffe als Treffer zählen.

### Aktualisieren und Patchen von Instanzen

Um eine Instanz zu aktualisieren, kann ein Client entweder die gesamte Liste von Eigenschaften auf einmal überschreiben oder eine JSON PATCH-Anfrage nutzen, um einzelne Eigenschaftswerte einschließlich Listen zu bearbeiten.

In beiden Fällen gibt die URL der Anfrage den Pfad zur physischen Instanz an, und in beiden Fällen ist die Antwort eine JSON-Receipt-Payload wie die vom [Erstellungsvorgang](#create-instances) zurückgegebene Payload. Ein Client sollte vorzugsweise die `Location`-Kopfzeile oder einen HAL-Link, den er von einem vorherigen API-Aufruf für dieses Objekt erhalten hat, als vollständigen URL-Pfad für diese API verwenden. Ist dies nicht möglich, kann der Client die URL aus der `containerId` und der `instanceId` erstellen.

**Anfrage** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Anfrage** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

Die PATCH-Anfrage wendet die Anweisungen an und validiert dann die resultierende Entität gegen das Schema und dieselben Entitäts- und referenziellen Integritätsregeln wie bei der PUT-Anfrage.

**Bearbeitungen von Eigenschaftswerten kontrollieren**

Mit folgenden Anmerkungen können Sie verhindern, dass Eigenschaften beim Erstellen und/oder Aktualisieren festgelegt werden:

- **`"meta:usereditable"`**: Boolescher Wert – Wenn eine Anfrage von einem Benutzeragenten stammt, der den Aufrufer mit einem Zugriffstoken für Benutzer oder technische Konten angibt, sollten Eigenschaften, die mit `"meta:usereditable": false` kommentiert sind, nicht in der Payload vorhanden sein. Ist das der Fall, dürfen sie keinen anderen Wert haben als den, der derzeit festgelegt ist. Wenn sich die Werte unterscheiden, wird die Update- oder Patch-Anfrage mit dem Status „422 Nicht verarbeitbare Entität“ abgelehnt.
- **`"meta:immutable"`**: Boolescher Wert – Eigenschaften, die mit `"meta:immutable": true` kommentiert sind, können nach der Festlegung nicht mehr geändert werden. Dies gilt für Anfragen, die von einem Endbenutzer, einer technischen Kontointegration oder einem besonderen Dienst stammen.

**Auf gleichzeitige Aktualisierung testen**

Es gibt Bedingungen, bei denen mehrere Clients gleichzeitig versuchen, eine Instanz zu aktualisieren. Das Repository wird in einem Cluster von Rechnerknoten ohne zentrale Transaktionsverwaltung betrieben. Um zu verhindern, dass ein Client in eine Instanz schreibt, in die gleichzeitig von einem anderen Client geschrieben wird, können die Clients eine bedingte Update- oder Patch-Anfrage nutzen. Wenn Sie die `etag`-Zeichenfolge in der Kopfzeile `If-Match` des Repository angeben, müssen Sie sicherstellen, dass nur die erste Anfrage erfolgreich ist und die Folgeanfragen anderer Clients, die denselben `etag`-Wert nutzen, fehlschlagen. Der `etag`-Wert ändert sich mit jeder Änderung der Instanz. Clients müssen die Instanz abrufen, um den neuesten `etag`-Wert zu erhalten; dann kann nur einer von vielen Clients, die die Aktualisierung versuchen, diesen Wert erfolgreich verwenden. Andere Clients werden mit der Nachricht „409 Konflikt“ abgelehnt.

### Löschen von Instanzen

Instanzen können mit einem DELETE-Aufruf gelöscht werden. Ein Client sollte vorzugsweise die Kopfzeile `Location` oder einen HAL-Link, den er von einem vorherigen API-Aufruf erhalten hat, als vollständigen URL-Pfad nutzen. Ist dies nicht möglich, kann der Client die URL aus der `containerId` und der physischen `instanceId` erstellen.

**Anfrage**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwort**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Nach Erhalt einer Löschanfrage prüft das Repository, ob andere Instanzen eines beliebigen Schemas immer noch auf die zu löschende Instanz verweisen. In einem verteilten, hochverfügbaren System kann referenzielle Integrität nicht sofort überprüft werden. Wenn Fremdschlüsselbeziehungen definiert sind, werden Prüfungen asynchron durchgeführt. Dies führt zu einer etwas verzögerten Antwort auf das Ergebnis der Löschanfrage. Wenn diese Prüfungen durchgeführt werden, enthält die sofortige Antwort den Status „202 Akzeptiert“ und einen Link, um das Ergebnis des Löschvorgangs in der `Location`-Kopfzeile zu überprüfen. Ein Client sollte diesen Link dann auf das Ergebnis überprüfen.

Wenn eine Instanz gefunden wird, die auf die zu löschende Instanz verweist, wird der Löschvorgang abgelehnt. Wenn keine weiteren Fremdschlüsselverweise gefunden werden, wird der Löschvorgang ausgeführt. Wenn das Ergebnis noch unentschieden ist, zeigt die Antwort das durch eine weitere „202 Akzeptiert“-Antwort mit der gleichen `Location`-Kopfzeile an und fordert den Client dazu auf, weiter zu überprüfen. Wenn das Ergebnis ermittelt ist, zeigt die Antwort das mit einem „200 OK“-Status an; die Payload der Antwort enthält das Ergebnis der ursprünglichen Löschanfrage. Beachten Sie, dass die Antwort „200 OK“ nur bedeutet, dass das Ergebnis bekannt ist und der Antworttext die Bestätigung oder Ablehnung der Löschanfrage enthalten wird.

## Erstellen von Angeboten und ihren Unterkomponenten

Die im vorherigen Abschnitt beschriebenen APIs gelten einheitlich für alle Typen von Geschäftsobjekten. Der einzige Unterschied zwischen beispielsweise dem Erstellen eines Angebots und einer Aktivität ist die Kopfzeile `content-type`, die das JSON-Schema und die JSON-Payload der Anfrage angibt, die dem Schema entspricht. Daher geht es in den folgenden Abschnitten nur um diese Schemas und die Beziehungen zwischen ihnen.

Bei Verwendung der APIs mit dem Content-Typ `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`werden die eigenen Eigenschaften der Instanz in die `_instance`-Eigenschaft eingebettet, neben der eine `_links`-Eigenschaft vorhanden ist. Dies ist das allgemeine Format, in dem alle Instanzen dargestellt werden:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Aus Gründen der Kürze werden in allen JSON-Snippets lediglich die Instanzeigenschaften veranschaulicht; und nur, wenn dies erforderlich ist, wird der Abschnitt mit Umschlageigenschaften und „_links“ angezeigt.

### Allgemeine Eigenschaften von Angeboten

Angebote sind eine Art von Entscheidungsoption und das JSON-Schema für Angebote übernimmt die Standardoptionseigenschaften, die jede Optionsinstanz aufweisen wird.

- **`@id`** – Eine eindeutige Kennung für jede Option, bei der es sich um den Primärschlüssel handelt und mit der aus anderen Objekten auf die Option verwiesen wird. Diese Eigenschaft wird bei der Erstellung der Instanz zugewiesen und ist unveränderlich sowie nicht bearbeitbar.
- **`xdm:name`** – Jede Option hat einen Namen, der für Such- und Anzeigezwecke verwendet wird. Der Name ist nicht unveränderlich und kann nicht zur eindeutigen Identifizierung der Instanz genutzt werden. Der Name lässt sich frei wählen, sollte jedoch in allen Angebotsinstanzen eindeutig sein.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` sein, wenn das Angebot ein Fallback-Angebot ist.

Jede Angebotsinstanz kann über einen optionalen Satz von Eigenschaften verfügen, die nur für diese Instanz charakteristisch sind. Verschiedene Angebote können unterschiedliche Schlüssel für diese Eigenschaften aufweisen. Die Werte müssen jedoch Zeichenfolgen sein. Diese Eigenschaften können in Entscheidungs- und Segmentierungsregeln verwendet werden. Sie sind auch verfügbar, um das beschlossene Erlebnis zusammenzustellen und die Nachrichten weiter anzupassen.

### Lebenszyklus von Angeboten

Es gibt einen einfachen Statusfluss, dem alle Optionen folgen. Sie beginnen in einem Entwurfsstatus;, wenn sie bereit dazu sind, wird ihr Zustand auf „Validiert“ gesetzt. Nach Ablauf ihres Enddatums können sie in den Status „Archiviert“ verschoben werden. In diesem Status können sie gelöscht oder wiederverwendet werden, indem sie zurück in den Entwurfsstatus versetzt werden.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** – Diese Eigenschaft wird für die Lebenszyklusverwaltung der Instanz verwendet. Der Wert stellt einen Workflow-Status dar, der angibt, ob das Angebot noch in Entwicklung ist (Wert = draft), allgemein von der Laufzeit berücksichtigt werden kann (Wert = authorised) oder nicht mehr verwendet werden sollte (Wert = archived).

Ein einfacher PATCH-Vorgang für die Instanz dient normalerweise dazu, nur eine `xdm:status`-Eigenschaft zu bearbeiten:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` sein, wenn das Angebot ein Fallback-Angebot ist.

### Darstellungen und Platzierungen

Angebote sind Entscheidungsoptionen mit Inhaltsdarstellungen. Wenn eine Entscheidung getroffen wurde, wird die Option ausgewählt und ihre Kennung verwendet, um die Inhalte oder Inhaltsreferenzen für die Platzierung abzurufen, die bereitgestellt werden soll. Ein Angebot kann verschiedene Darstellungen aufweisen; für jede von ihnen muss jedoch eine andere Platzierungsreferenz vorhanden sein. Dadurch wird sichergestellt, dass die Darstellung bei einer bestimmten Platzierung eindeutig identifiziert werden kann.
Während des Entscheidungsvorgangs wird die Platzierung zusammen mit dem Aktivitätsobjekt bestimmt. Angebote, die über keine Darstellung mit dieser Platzierung als Referenz verfügen, werden automatisch aus der Liste der Optionen entfernt.

Bevor einem Angebot Darstellungen hinzugefügt werden können, müssen die Platzierungsinstanzen vorhanden sein. Diese Instanzen werden mit der Schemakennung `https://ns.adobe.com/experience/offer-management/offer-placement` erstellt.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` sein, wenn das Angebot ein Fallback-Angebot ist.

Eine **Platzierungsinstanz** kann die folgenden Eigenschaften aufweisen:

- **`xdm:name`** – Enthält den zugewiesenen Namen für die Platzierung, auf den in menschlichen Interaktionen und Benutzeroberflächen verwiesen wird.
- **`xdm:description`** – Dient zum Vermitteln von visuell lesbaren Absichten dafür, wie Inhalte in dieser Platzierung im übergeordneten Nachrichtenversand verwendet werden sollen. Wenn Versandkanäle neue Platzierungen definieren, können sie weitere Informationen zu dieser Eigenschaft hinzufügen, damit ein Inhaltsersteller den Inhalt entsprechend erstellen oder auswählen kann. Diese Anweisungen werden nicht formell ausgelegt oder durchgesetzt. Diese Eigenschaft dient lediglich als Ort zum Kommunizieren der Absichten.
- **`xdm:channel`** – Der URI eines Kanals. Der Kanal gibt an, wo der dynamische Content bereitgestellt werden soll. Mit der Kanalbegrenzung wird nicht nur vermittelt, wo das Angebot verwendet werden soll, sondern auch der Content-Editor oder -Validator bestimmt, der für das Erlebnis genutzt wird.
- **`xdm:componentType`** – Eine Modellkennung (d. h. ein URI) für den Inhalt, der an dem von dieser Platzierung beschriebenen Ort angezeigt werden kann. Komponententypen sind: Bild-Link, HTML oder Nur-Text. Jeder Komponententyp kann einen bestimmten Satz von Eigenschaften (ein Modell) beinhalten, den das Inhaltselement aufweisen kann. Die Liste von Komponententypen lässt sich erweitern. Es gibt drei vordefinierte Komponententypwerte:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`** – Eine Begrenzung für die Medientypen der Komponenten, die in dieser Platzierung erwartet werden. Für einen Komponententyp kann es mehr als einen Medientyp geben, z. B. verschiedene Bildformate.

**Darstellungselemente** in einem Angebot weisen in der Array-Eigenschaft `xdm:representations` eine Objektstruktur auf. Jedes Element kann über die folgenden Eigenschaften verfügen:

- **`xdm:placement`** – Diese Eigenschaft enthält den Verweis auf die Platzierungsinstanz. Der Wert wird überprüft, wenn die Darstellung dem Angebot hinzugefügt wird. Eine Platzierungsinstanz mit diesem URI muss vorhanden und darf nicht als gelöscht markiert sein. Darüber hinaus wird eine Überprüfung durchgeführt, um sicherzustellen, dass eine Angebotsinstanz nicht zwei Darstellungen mit demselben Wert für ihre Platzierungsreferenz hat.
- **`xdm:components`** – Inhaltskomponenten sind die mit einer bestimmten Angebotsdarstellung verknüpften Fragmente. Diese Fragmente dienen später dazu, das Endbenutzererlebnis einzurichten. Beachten Sie, dass der Decisioning Service allein nicht das gesamte Endbenutzerlebnis zusammenstellt. Folgende Eigenschaften sind Teil des Modells jeder Komponente.
   - **`@type`** – Diese Eigenschaft gibt den Komponententyp an. Ein anderer Name für dieses Konzept ist Inhaltsfragmentmodell. Die Komponente `@type` ist lediglich ein URI für ein Modell, das von der Anwendung oder dem Dienst definiert wird, die bzw. der das Endbenutzererlebnis zusammenstellt.
   - **`repo:id`** – Diese Eigenschaft enthält eine global eindeutige, unveränderliche Kennung für die Hauptressource der Komponente im Repository, in dem das Asset gespeichert ist.
   - **`repo:name`** – Diese Eigenschaft enthält einen für Menschen lesbaren Namen für das Asset im Repository. Dieser Name ist benutzerdefiniert und nicht garantiert eindeutig.
   - **`repo:resolveURL`** – Diese Eigenschaft enthält einen eindeutigen Ressourcen-Locator, um das Asset in einem Content-Repository zu lesen. Dies erleichtert das Abrufen des Assets, ohne dass der Client weiß, welche APIs aufgerufen werden sollen. Die URL gibt die Bytes der primären Ressource des Assets zurück.
   - **`dc:format`** – Diese Eigenschaft stammt von der Dublin Core Metadata Initiative. Das Format kann verwendet werden, um die Software, Hardware oder andere Geräte zu ermitteln, die zum Anzeigen oder Verwenden der Ressource erforderlich sind. Es wird empfohlen, einen Wert aus einem kontrollierten Vokabular auszuwählen (z. B. Liste mit Internet-Medientypen, die Computer-Medienformate definieren).
   - **`dc:language`** – Diese Eigenschaft enthält die Sprache oder Sprachen der Ressource. Sprache werden in Sprach-Code gemäß der Definition in IETF RFC 3066 angegeben.

Es gibt drei vordefinierte Komponententypen, die in der `@type`-Eigenschaft ausgedrückt werden:

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

Je nach Wert der `@type`-Eigenschaft enthält `xdm:components` die folgenden zusätzlichen Eigenschaften:

- **`xdm:linkURL`** – Vorhanden, wenn die Komponente ein Bild-Link ist. Diese Eigenschaft enthält den Link, der mit dem Bild verknüpft ist und zu dem der `user-agent` navigiert, wenn der Endbenutzer mit dem Inhalt des Angebots interagiert.
- **`xdm:copyline`** – Wird verwendet, wenn die Komponente ein Text ist. Zusätzlich zum Verweis auf ein Text-Asset, z. B. für Angebote in Langformtext, die Formatierung enthalten können, kann eine kurze Textzeichenfolge direkt in der Eigenschaft „xdm:copyline“ gespeichert werden.

Clients können zusätzliche Eigenschaften nutzen, um Anweisungen zur Handhabung von Kontext festzulegen und auszuwerten. Der Offer UI Library-Client fügt beispielsweise die folgenden optionalen Eigenschaften hinzu, um das Anzeigen einfacher zu gestalten:

- In jedem Element im `xdm:components`-Array fügt der UI-Client der Angebotsbibliothek die folgenden Eigenschaften hinzu. Diese Eigenschaften sollten Sie weder löschen noch bearbeiten, wenn Sie die Auswirkungen auf die Benutzeroberfläche nicht kennen:
   - **`offerui:previewThumbnail`** – Dies ist eine optionale Eigenschaft, die die Benutzeroberfläche der Angebotsbibliothek verwendet, um eine Darstellung des Assets anzuzeigen. Diese Ausgabedarstellung ist nicht mit dem Asset selbst identisch. Der Inhalt könnte beispielsweise HTML und die Ausgabedarstellung ein Bitmap-Bild sein, das nur eine Annäherung davon wiedergibt. Diese (minderwertige) Ausgabedarstellung wird im Darstellungsblock des Angebots angezeigt.

Ein Beispiel für einen PATCH-Vorgang für eine Angebotsinstanz zeigt, wie sich die Darstellungen bearbeiten lassen:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` sein, wenn das Angebot ein Fallback-Angebot ist.

Der PATCH-Vorgang kann fehlschlagen, wenn es noch keine `xdm:representations`-Eigenschaft gibt. In diesem Fall könnte dem oben genannten Vorgang zum Hinzufügen ein weiterer Vorgang zum Hinzufügen vorangestellt werden, der das `xdm:representations`-Array erstellt; alternativ legt der einmalige Vorgang zum Hinzufügen das Array direkt fest.
Die beschriebenen Schemas und Eigenschaften werden für alle Angebotstypen, Personalisierungsangebote sowie Fallback-Angebote verwendet. Die folgenden beiden Abschnitte zu Begrenzungen und Entscheidungsregeln erläutern Aspekte von Personalisierungsangeboten.

## Festlegen von Angebotsbegrenzungen

### Kalendarische Begrenzungen

Entscheidungsoptionen können generell ein Anfangs- und Enddatum inklusive Uhrzeit erhalten, das als kalendarische Begrenzung dient. Die Eigenschaften sind in der Eigenschaft `xdm:selectionConstraint` eingebettet:

- **`xdm:startDate`** – Diese Eigenschaft gibt das Anfangsdatum inklusive Uhrzeit an. Der Wert ist eine Zeichenfolge, die nach RFC 3339-Regeln formatiert ist, d. h. wie in diesem Zeitstempel: „2019-06-13T11:21:23.356Z“.
Entscheidungsoptionen, die ihren Anfangszeitpunkt (Datum und Uhrzeit) noch nicht erreicht haben, werden bei der Entscheidungsfindung noch nicht berücksichtigt.
- **`xdm:endDate`** – Diese Eigenschaft gibt das Enddatum inklusive Uhrzeit an. Der Wert ist eine Zeichenfolge, die nach RFC 3339-Regeln formatiert ist, d. h. wie in diesem Zeitstempel: „2019-07-13T11:00:00.000Z“
Entscheidungsoptionen, die ihr Enddatum überschritten haben, werden im Entscheidungsprozess nicht mehr berücksichtigt.

Das Ändern einer Kalenderbegrenzung kann mit dem folgenden PATCH-Aufruf ausgeführt werden:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` lauten. Fallback-Angebote haben keine Begrenzungen.

### Begrenzungen

Eine Begrenzung ist eine Komponente in einer Entscheidungsoption, die die Parameter für Begrenzungen definiert. Mit Begrenzungen wird begrenzt, wie oft eine Option vorgeschlagen werden kann – sowohl für ein einzelnes Profil als auch für alle Profile. Die Eigenschaften enthalten einen ganzzahligen Wert, der größer oder gleich 1 sein muss. Die Eigenschaften sind innerhalb einer `xdm:cappingConstraint`-Eigenschaft verschachtelt:

- **`xdm:globalCap`** – Eine globale Begrenzung ist eine Begrenzung dafür, wie oft ein Angebot insgesamt vorgeschlagen werden kann.
- **`xdm:profileCap`** – Eine Profilbegrenzung ist eine Begrenzung dafür, wie oft ein Angebot einem bestimmten Profil vorgeschlagen werden kann.

Das Festlegen oder Ändern der Begrenzung für ein Personalisierungsangebot kann mit dem folgenden PATCH-Aufruf erreicht werden:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` lauten. Fallback-Angebote haben keine Begrenzungen.

Um die Begrenzungswerte zu entfernen, wird der Vorgang „add“ durch den Vorgang „remove“ ersetzt. Beachten Sie, dass die Begrenzungswerte einzeln existieren und auch einzeln festgelegt oder entfernt werden können.

### Eignungsbegrenzungen

Angebote können im Entscheidungsprozess bedingt ausgewählt werden. Wenn ein Personalisierungsangebot einen Verweis auf eine Eignungsregel enthält, muss die Regelbedingung auf „true“ ausgewertet werden, damit das Angebotsobjekt für ein bestimmtes Profil berücksichtigt wird. Die Eignungsregeln werden unabhängig von den Entscheidungsoptionen erstellt und verwaltet. Eine Regel kann von verschiedenen Personalisierungsangeboten referenziert werden.

Der Verweis auf die Regel ist in die Eigenschaft `xdm:selectionConstraint` eingebettet:

- **`xdm:eligibilityRule`** – Diese Eigenschaft enthält einen Verweis auf eine Eignungsregel. Der Wert ist die `@id` einer Instanz von Schema https://ns.adobe.com/experience/offer-management/eligibility-rule.

Das Hinzufügen und Löschen einer Regel lässt sich auch mit einem PATCH-Vorgang erreichen:

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` lauten. Fallback-Angebote haben keine Begrenzungen.

Beachten Sie, dass die Eignungsregel zusammen mit den kalendarischen Begrenzungen in die `xdm:selectionConstraint`-Eigenschaft eingebettet ist. PATCH-Vorgänge sollten nicht versuchen, die gesamte `SelectionConstraint`-Eigenschaft zu entfernen.

## Festlegen der Priorität eines Angebots

Optionen von Eignungsentscheidungen werden nach Rang geordnet, um die beste Option für das jeweilige Profil zu ermitteln. Um das Ranking zu unterstützen und eine Standardeinstellung anzugeben, falls sich die Rangfolge nicht durch einen anderen Mechanismus bestimmen lässt, kann für jedes Personalisierungsangebot eine Basispriorität festgelegt werden.
Die Basispriorität ist in die Eigenschaft `xdm:rank` eingebettet:

- **`xdm:priority`** – Diese Eigenschaft stellt die Standardreihenfolge dar, in der ein Angebot gegenüber einem anderen ausgewählt wird, falls keine spezielle profilspezifische Reihenfolge bekannt ist. Wenn nach dem Vergleichen des Prioritätswerts zwei oder mehr Personalisierungsangebote immer noch Gleichstand aufweisen, wird ein Angebot zufällig ausgewählt und im Angebotsvorschlag verwendet. Der Wert dieser Eigenschaft muss eine Ganzzahl größer oder gleich 0 sein.

Die Basispriorität lässt sich mit dem folgenden PATCH-Aufruf anpassen:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` lauten. Fallback-Angebote haben keine Ranking-Eigenschaften.

## Verwalten von Entscheidungsregeln

Eignungsregeln enthalten die Bedingungen, die ausgewertet werden, um zu ermitteln, ob eine bestimmte Entscheidungsoption für ein bestimmtes Profil geeignet ist. Wenn eine Regel einer oder mehreren Entscheidungsoptionen zugeordnet wird, wird implizit festgelegt, dass die Regel auf „true“ ausgewertet werden muss, damit die Option für diesen Benutzer berücksichtigt wird. Die Regel kann Tests zu Profilattributen enthalten, Ausdrücke mit Erlebnisereignissen für dieses Profil auswerten und Kontextdaten einschließen, die an die Entscheidungsanfrage übermittelt wurden. Eine Bedingung kann beispielsweise wie folgt beschrieben werden:

> „Personen einschließen, die Elite-Status haben und in den letzten sechs Monaten dreimal einen Flug genommen haben, der die Flugnummer des aktuellen Flugs aufwies.“

Die Instanzen werden mit der Schemakennung https://ns.adobe.com/experience/offer-management/eligibility-rule erstellt. Die `_instance`-Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/eligibility-rule` lauten.

Der Wert in der Bedingungseigenschaft der Regel enthält einen PQL-Ausdruck. Die Kontextdaten werden über den speziellen Pfadausdruck @{schemaID} referenziert.

Rules naturally align with segments in the [!DNL Experience Platform] and often a rule will simply reuse a segment’s intent by testing a profile’s `segmentMembership` property. Die `segmentMembership`-Eigenschaft enthält die Ergebnisse der Segmentbedingungen, die bereits ausgewertet wurden. Auf diese Weise kann eine Organisation ihre Domain-spezifischen Audiences einmal definieren, benennen und die Bedingungen einmal auswerten.

## Verwalten von Angebotskollektionen

### Erstellen von Tags und Tagging-Angeboten

Angebote können in Kollektionen angeordnet werden, wobei jede Kollektion die anzuwendende Filterbedingung definiert. Derzeit kann ein Filterausdruck in einer Kollektion eine von zwei Formen haben:

1. Der `@id`-Parameter des Angebots muss mit einer Kennung in einer Liste von Kennungen übereinstimmen, damit das Angebot in die Kollektion aufgenommen wird. Dieser Filter ist lediglich eine Auflistung der URIs der Angebote in der Kollektion.
2. Ein Angebot kann über eine Liste von Tag-Verweisen verfügen; der Filter der Kollektion besteht aus einer Liste von Tags. Das Angebot befindet sich in der Kollektion, wenn:\
   a. beliebige Tags des Filters mit einem der Tags des Angebots übereinstimmen;\
   b. alle Tags des Filters mit einem der Tags des Angebots übereinstimmen.

Tags sind einfache Instanzen, mit denen Angebotsinstanzen verknüpft werden können. Es handelt sich dabei um eigenständige Instanzen mit einem Namen für ihre Anzeige. Der Name muss in allen Instanzen eindeutig sein, um die Anzeige in der Benutzeroberfläche zu vereinfachen.

Tag-Objekte dienen dazu, eine Kategorisierung der Entscheidungsoptionen (Angebote) vorzunehmen. Ein Tag kann mit vielen Angeboten verknüpft werden und ein Angebot kann über viele Tag-Verweise verfügen. Eine Kategorie von Angeboten wird erstellt, indem auf alle Angebote verwiesen wird, die zu einem bestimmten Satz von Tag-Instanzen gehören.

Die Tag-Instanzen werden mit der Schemakennung https://ns.adobe.com/experience/offer-management/tag erstellt. Die `_instance`-Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:

```json
{
  "xdm:name": "credit card"
} 
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/tag` lauten.


Eine Angebotsinstanz kann mit der Liste von Tag-Verweisen erstellt werden, z. B.:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Alternativ kann ein Angebot gepatcht werden, um seine Tag-Liste zu ändern:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

In beiden Fällen sollten Sie [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) konsultieren, um die vollständige cURL-Syntax zu erhalten. Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer` lauten.

Beachten Sie, dass die `xdm:tags`-Eigenschaft bereits vorhanden sein muss, damit sich der Vorgang zum Hinzufügen erfolgreich abschließen lässt. Wenn es keine Tags in einer Instanz gibt, kann der PATCH-Vorgang zuerst die Array-Eigenschaft und dann eine Tag-Referenz zu diesem Array hinzufügen.

### Filter für Angebotskollektionen definieren

Die Filterinstanzen werden mit der Schemakennung https://ns.adobe.com/experience/offer-management/offer-filter erstellt. Die `_instance`­Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren könnte wie folgt aussehen:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/offer-filter` lauten.

- **`xdm:filterType`** – Diese Eigenschaft gibt an, ob der Filter mithilfe von Tags eingerichtet wird oder über Kennungen direkt auf Angebote verweist. Wenn der Filter so eingerichtet ist, dass Tags verwendet werden, kann der Filtertyp außerdem angeben, ob alle Tags mit den Tags eines bestimmten Angebots übereinstimmen müssen oder ob eines der angegebenen Tags ausreicht, damit das Angebot für den Filter qualifiziert ist. Gültige Werte dieser Aufzählungseigenschaft sind:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** – Eine Eigenschaft enthält ein Array von URIs, die je nach dem Wert von `xdm:filterType` auf Angebotsinstanzen oder Tag-Instanzen verweisen.

Der folgende Aufruf zeigt, wie die `_instance`-Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren aussieht, wenn auf Angebote direkt verwiesen wird:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Verwalten von Aktivitäten

Zur Kontrolle des Entscheidungsprozesses wird eine Angebotsaktivität verwendet. Sie gibt den auf den Gesamtbestand anzuwendenden Angebotsfilter an, um Angebote nach Thema/Kategorie einzugrenzen, sowie die Platzierung, um den Bestand auf die Angebote zu begrenzen, die in den reservierten Bereich passen. Hinzu kommt eine Fallback-Option, sollten die kombinierten Begrenzungen alle verfügbaren Personalisierungsoptionen (Angebote) disqualifizieren.

Die Aktivitätsinstanzen werden mit der Schemakennung `https://ns.adobe.com/experience/offer-management/offer-activity` erstellt. Die `_instance`-Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/offer-activity` lauten.

- **`xdm:name`** – Diese obligatorische Eigenschaft enthält den Namen der Aktivität. Der Name wird in verschiedenen Benutzeroberflächen angezeigt.
- **`xdm:status`** – Diese Eigenschaft wird für die Lebenszyklusverwaltung der Instanz verwendet. Der Wert stellt einen Workflow-Status dar, der angibt, ob die Aktivität noch in Entwicklung ist (Wert = draft), im Allgemeinen von der Laufzeit berücksichtigt werden kann (Wert = live) oder nicht mehr verwendet werden soll (Wert = archived).
- **`xdm:placement`** – Eine obligatorische Eigenschaft, die einen Verweis auf eine Angebotsplatzierung enthält, die auf den Bestand angewendet wird, wenn im Kontext dieser Aktivität eine Entscheidung getroffen wird. Der Wert ist der URI (`@id`) der verwendeten Angebotsplatzierung.
- **`xdm:filter`** – Eine obligatorische Eigenschaft, die einen Verweis auf einen Angebotsfilter enthält, der auf den Bestand angewendet wird, wenn im Kontext dieser Aktivität eine Entscheidung getroffen wird. Der Wert ist der URI (`@id`) des verwendeten Angebotsfilters.
- **`xdm:fallback`** – Eine obligatorische Eigenschaft, die einen Verweis auf ein Fallback-Angebot enthält. Ein Fallback-Angebot wird verwendet, wenn der Entscheidungsprozess für diese Aktivität keines der Personalisierungsangebote qualifiziert. Der Wert ist der URI (`@id`) einer Fallback-Angebotsinstanz.

### Verwalten von Fallback-Angeboten

Bevor Aktivitätsinstanzen erstellt werden können, muss ein Fallback-Angebot vorhanden sein, das für die Platzierung der Aktivität geeignet ist. Die Fallback-Angebotsinstanzen werden mit der Schemakennung `https://ns.adobe.com/experience/offer-management/fallback-offer` erstellt. Die `_instance`-Eigenschaft des Erstellungs- oder Aktualisierungsaufrufs enthält dieselben allgemeinen Eigenschaften wie ein Personalisierungsangebot, kann jedoch keine anderen Beschränkungen aufweisen.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances). Der `schemaId`-Parameter muss `https://ns.adobe.com/experience/offer-management/fallback-offer` lauten.

