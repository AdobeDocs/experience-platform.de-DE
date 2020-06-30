---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verwalten von Entscheidungsdienst-Entitäten mithilfe von APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '7207'
ht-degree: 0%

---


# Verwalten von Entscheidungsobjekten und Regeln mithilfe von APIs

Dieses Dokument bietet eine Anleitung zum Arbeiten mit den Geschäftseinheiten, die Adobe Experience Platformen-APIs [!DNL Decisioning Service] verwenden.

Das Lernprogramm besteht aus zwei Teilen:

- Generische Repository-APIs zum Verwalten von Geschäftsobjekten werden im [ersten Teil](#managing-repository-entities-using-apis)eingeführt. Diese APIs sind generisch in dem Sinne, dass sie Funktionen zum Erstellen, Lesen, Aktualisieren, Löschen und Suchen für **beliebige** Geschäftsobjekte bereitstellen. Das allgemeine API-Modell wird beschrieben und die Beziehung zur Hypertext Application Language (HAL) wird erklärt.

- Unter Anwendung der Kenntnisse über die Repository-APIs konzentriert sich der [zweite Teil](#creating-and-managing-offer-decisioning-entities-using-apis) auf die Geschäftseinheiten, die über die Repository-APIs verwaltet werden. Bei Anwendung derselben APIs besteht der einzige Unterschied zwischen der Verwaltung zweier verschiedener Entitäten wie einer Aktivität und einer Geschäftsregel in der Anforderungs- und Antwortnutzlast sowie den erforderlichen Header-Werten, die den verwalteten Objekttyp angeben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der [!DNL Experience Platform] Services und API-Konventionen. Das [!DNL Platform] Repository ist ein Dienst, der von mehreren anderen [!DNL Platform] Diensten zum Speichern von Geschäftsobjekten und verschiedenen Metadaten verwendet wird. Es bietet eine sichere und flexible Möglichkeit, diese Objekte zu verwalten und für die Verwendung durch mehrere Laufzeitdienste Abfrage. Das [!DNL Decisioning Service] ist einer davon. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für Folgendes:

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
- [!DNL Decisioning Service](./../home.md): Erläutert die Konzepte und Komponenten, die für die Erlebnisentscheidung im Allgemeinen und für die Angebot-Entscheidungsfindung im Speziellen verwendet werden. Veranschaulicht die Strategien zur Auswahl der besten Option, die während des Kundenerlebnisses angezeigt werden soll.
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL ist eine leistungsstarke Sprache, um Ausdruck über XDM-Instanzen zu schreiben. PQL wird zur Definition von Entscheidungsregeln verwendet.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Platform] APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in [!DNL Platform]finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Repository API-Konventionen

[!DNL Decisioning Service] wird von einer Reihe von Geschäftsobjekten gesteuert, die miteinander verbunden sind. Alle Geschäftsobjekte werden im [!DNL Platform’s] Business Object Repository gespeichert. Eine wichtige Funktion dieses Repositorys ist, dass die APIs orthogonal zum Typ des Geschäftsobjekts sind. Statt eine POST-, GET-, PUT-, PATCH- oder DELETE-API zu verwenden, die den Ressourcentyp im API-Endpunkt angibt, gibt es nur 6 generische Endpunkte, die jedoch einen Parameter akzeptieren oder zurückgeben, der den Objekttyp angibt, wenn diese Unterscheidung erforderlich ist. Das Schema muss beim Repository registriert sein, darüber hinaus ist das Repository jedoch für einen Satz von Objekttypen mit offenem Ende einsetzbar.

Zusätzlich zu den oben aufgeführten Überschriften gelten folgende Konventionen für die APIs zum Erstellen, Lesen, Aktualisieren, Löschen und Abfrage von Repository-Objekten:

- Die Endpunktpfade für alle Repository-APIs, mit denen der Beginn `https://platform.adobe.io/data/core/xcore/`arbeitet.

API-Nutzdatenformate werden mit einem `Accept` oder einer `Content-Type` Kopfzeile ausgehandelt. Die Nachrichtenformate in der `Accept` oder `Content-Type` -Kopfzeile werden durch einen Wert angegeben, `application/vnd.adobe.platform.xcore.{FORMAT}+json` bei dem {FORMAT} von der spezifischen Repository-API-Anforderung oder -Antwortmeldung gemäß der folgenden Tabelle abhängig ist.

| FORMAT-Variante | Beschreibung der Anforderungs- oder Antwortentität |
| --- | --- |
| <br>gefolgt von einem Parameter `schema={schemaId}` | Die Meldung enthält eine Instanz, die von einem JSON-Schema beschrieben wird, das durch das Schema des format-Parameters gekennzeichnet ist. Die Instanz wird in eine JSON-Eigenschaft eingeschlossen `_instance`. Die anderen Eigenschaften der obersten Ebene in der Antwortnutzlast geben Repository-Informationen an, die für alle Ressourcen verfügbar sind.  Nachrichten, die dem HAL-Format entsprechen, haben eine `_links` Eigenschaft, die Verweise im HAL-Format enthält. |
| `patch.hal` | Die Nachricht enthält eine JSON PATCH-Nutzlast mit der Annahme, dass die Instanz, die gepatcht werden soll, HAL-konform ist. Das bedeutet, dass nicht nur die eigenen Instanzeigenschaften, sondern auch die HAL-Verknüpfungen der Instanz gepatcht werden können. Beachten Sie, dass es Einschränkungen gibt, welche Eigenschaften vom Client aktualisiert werden können. |
| `home.hal` | Die Nachricht enthält eine JSON-formatierte Darstellung einer Home-Dokument-Ressource für das Repository. |
| xdm.receipt | Die Nachricht enthält eine JSON-formatierte Antwort für einen Vorgang zum Erstellen, Aktualisieren (Voll- und Patch-Vorgang) oder Löschen. Die Quittungen enthalten Kontrolldaten, die auf die Überarbeitung der Instanz in Form eines ETag hinweisen. |

Die Verwendung der einzelnen **Formatvarianten** hängt von der jeweiligen API ab:

| API | Content-Type-Kopfzeile | Kopfzeile akzeptieren |
| --- | --- | --- |
| Container <br/>&quot;Instanz erstellen&quot; | `hal`<br/>mit Schema-Parameter | `xdm.receipt` |
| Update<br/>InstanceUpdate Container | `hal`<br/>mit Schema-Parameter | `xdm.receipt` |
| Patch-Instanz | `patch.hal` | `xdm.receipt` |
| Löschen<br/>des instanceDelete-Containers | K. A. | `xdm.receipt` |
| Read<br/>InstanceRead-Container | K. A. | `hal` with `schema` parameter |
| Liste<br/>instancesList-Container | K. A. | `hal` mit speziellem `schema` Parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Suchinstanzen | K. A. | hal mit speziellem `schema` Parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Repo-Stamm lesen | K. A. | `home.hal` |

Für Container, die APIs erstellen, aktualisieren und lesen, hat das format parameter-Schema den Wert `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` ist der erste Pfadparameter für die Instanz-APIs. Alle Geschäftseinheiten befinden sich in einem so genannten Container. Ein Container ist ein Isolationsmechanismus, der unterschiedliche Anliegen voneinander trennt. Das erste Pfadelement für die Repository-Instanz-APIs nach dem allgemeinen Endpunkt ist der `containerId`. Der Bezeichner wird aus der Liste der Container gewonnen, auf die der Aufrufer zugreifen kann. Beispielsweise ist die API zum Erstellen einer Instanz in einem Container `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`vorhanden.

Die Liste barrierefreier Container wird durch Aufruf des Repository-Stammendpunkts &quot;/&quot;mit einer HTTP GET-Anforderung unter Verwendung der Standardkopfzeilen abgerufen.

## Zugriff auf Container verwalten

Ein Administrator kann ähnliche Prinzipale, Ressourcen und Zugriffsberechtigungen in Profilen gruppieren. Dies verringert den Verwaltungsaufwand und wird von der Benutzeroberfläche der [Admin Console](https://adminconsole.adobe.com)von Adobe unterstützt. Sie müssen Produktadministrator für die Adobe Experience Platform in Ihrem Unternehmen sein, um Profil zu erstellen und ihnen Benutzer zuzuweisen.

Es reicht aus, Produktanpassungen zu erstellen, die bestimmten Berechtigungen in einem einmaligen Schritt entsprechen, und diese Profil dann einfach zu diesen Profilen hinzuzufügen. Profil fungieren als Gruppen, denen Berechtigungen erteilt wurden, und alle echten Benutzer oder technischen Benutzer in dieser Gruppe erben diese Berechtigungen.

### Benutzerfreundliche Liste-Container und Integrationen

Wenn der Administrator Containern für normale Benutzer oder Integrationen Zugriff gewährt hat, werden diese Container in der so genannten &quot;Home&quot;-Liste des Repositorys angezeigt. Die Liste kann für verschiedene Benutzer oder Integrationen unterschiedlich sein, da sie eine Untergruppe aller Container ist, auf die der Aufrufer zugreifen kann. Die Liste der Container kann durch ihre Verbindung zu den Kontexten gefiltert werden. Der Filterparameter wird aufgerufen `product` und kann wiederholt werden. Wenn mehr als ein Produktkontextfilter angegeben wird, wird die Vereinigung der Container zurückgegeben, die mit einem der angegebenen Kontexte verbunden sind. Beachten Sie, dass ein Container mehreren Kontexten zugeordnet werden kann.

Der Kontext für die [!DNL Platform] Container ist derzeit [!DNL Decisioning Service] `dma_offers`.

>[!NOTE] Der Kontext für [!DNL Platform Decisioning Containers] wird sich bald ändern `acp`. Die Filterung ist optional, aber nur Filter `dma_offers` müssen bei einer zukünftigen Version bearbeitet werden. Zur Vorbereitung auf diese Änderung sollten Kunden keine Filter verwenden oder beide Kontexte als Filter anwenden.

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

Notieren Sie die `instanceId` in den Ergebniselementen aufgelisteten Elemente. Es wird als `containerId` Parameter in den APIs zum Lesen und Manipulieren regulärer Geschäftsobjekte verwendet.

Die Liste wird bereits nach den Benutzerberechtigungen gefiltert, kann aber durch eine Abfrage weiter gefiltert werden.

## Generische APIs zum Verwalten von Entitäten

### Erstellen von Instanzen

Die API zum Erstellen einer neuen Instanz im Repository verwendet einen `containerId` Pfadparameter und identifiziert den Instanztyp im `Content-Type` Header mit dem Schema-Parameter.

Die Instanzeigenschaften werden in der Payload angegeben, die in der `_instance` Eigenschaft eingeschlossen ist. Die Instanzeigenschaften müssen für das JSON-Schema mit der angegebenen Schema-ID gültig sein.

Die HAL- `_links` Eigenschaft muss vorhanden sein, darf jedoch leer sein. Das bedeutet, dass für diese Instanz keine benutzerspezifischen Links definiert sind.

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

Die Antwort enthält die instanceId des soeben erstellten Objekts. Diese instanceId ist unveränderlich, wird immer vom Repository zugewiesen und global eindeutig. Der Wert dient als physischer Bezeichner.

Darüber hinaus wird in der Eigenschaft der `@id` Antwortnutzlast eine URI (Universal Resource Identifier) zurückgegeben, wenn das Schema über eine solche Eigenschaft verfügt. Jede Instanz sollte über eine Eigenschaft verfügen, die als URI und Primärschlüssel der Instanz dient. Dieser Bezeichner wird von anderen Instanzen verwendet, um Beziehungen zur neuen Instanz zu erstellen, auch über verschiedene Typen hinweg. In der aktuellen Version werden die URIs vom Repository generiert und sind in der `@id` Eigenschaft enthalten. Zukünftige Versionen können diese Regel entspannen und es Kunden ermöglichen, ihre eigenen URI-Werte zu verwalten und die Eigenschaft zu benennen, die sie enthält.

Beachten Sie, dass diese URIs keine URLs sind und keine Möglichkeit bieten, die Ressource direkt abzurufen. Um diesen Aspekt anzugeben, wird dem URI ein URI-Schema vorangestellt, das kein Abrufprotokoll angibt. Die URIs können jedoch zum Nachschlagen der Instanz mit einer Abfrage verwendet werden.

Die REST-Antwort verfügt über einen Location-Header, der eine URL-Komponente enthält, mit der die soeben erstellte Instanz abgerufen werden kann. Diese Komponente ist eine relative URI-Referenz und muss auf den Basis-URI des Repositorys angewendet werden. Der Basis-URI wird in der `Content-Base` Kopfzeile zurückgegeben.

Die `repo:etag` Eigenschaft gibt die Revision der Instanz an. Dieser Wert kann bei Aktualisierungsvorgängen verwendet werden, um Konsistenz zu erzwingen. Der HTTP-Header `If-Match` kann verwendet werden, um einem PUT- oder PATCH-API-Aufruf eine Bedingung hinzuzufügen, die sicherstellt, dass keine andere Änderung an der Instanz vorgenommen wurde, die versehentlich überschrieben werden konnte. Der `repo:etag` Wert wird bei jedem Aufruf zum Erstellen, Lesen, Aktualisieren, Löschen und Abfrage zurückgegeben. Der Wert wird als Wert in der ` If-Match` Kopfzeile gemäß [RFC7232 Abschnitt 3.1](https://tools.ietf.org/html/rfc7232#section-3.1)verwendet.

Die übrigen Eigenschaften geben an, welches Konto und welcher API-Schlüssel zum Erstellen und letzten Ändern der Instanz verwendet wurden. Da die Instanz durch diesen Aufruf erstellt wurde, sind die entsprechenden Werte die der Anforderung.

### Instanz nach ID suchen

Mithilfe der URL in der Kopfzeile &quot;Position&quot;, die mit dem Aufruf &quot;Erstellen&quot;zurückgegeben wird, kann eine Anwendung eine Instanz nachschlagen.

**Anfrage**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE] Obwohl dieser Parameter als Pfadparameter angegeben `instanceId` wird, sollten Anwendungen den Pfad nach Möglichkeit nicht selbst erstellen und stattdessen Links zu Instanzen in Liste- und Suchvorgängen folgen. Einzelheiten finden Sie in den Abschnitten ‎ 6.4.4 und ‎ 6.4.6.

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

Die JSON-Eigenschaften der Instanz werden in die `_instance` Eigenschaft eingeschlossen und die anderen Eigenschaften auf der Stammebene enthalten Metadaten zur Instanz.

Die Ressource enthält auch ein Array von JSON-Schema-IDs. Dieses Array zeigt die JSON-Schema an, für die diese Instanz validiert wurde.

Jede Instanz enthält einen HAL-Link des Beziehungstyps selbst, der der von der IANA registrierten Selbstbeziehung entspricht (wie in [RFC5988]definiert).

**Testen auf neuere Revisionen einer Instanz**

Der aktuelle `eTag` Wert der Instanz wird mit der Antwort zurückgegeben. Er ermöglicht es Kunden, bedingte Vorgänge für die Instanz auszuführen, um entweder zu vermeiden, dass der gleiche Ressourcenstatus erneut abgerufen wird, oder um zu vermeiden, dass die Werte einer späteren Revision ohne Wissen des Kunden überschrieben werden.

Mit der Lookup-API kann ein Client einen `If-None-Match` Header-Parameter angeben. Siehe Definition dieses standardmäßigen HTTP-Parameters [RFC2616]. Der entity-Tag-Wert, den ein Client angibt, ist der Wert, den er mit der neuesten Antwort erhalten hat, entweder von einem Update-, Lese-, Listen- oder Such-API-Aufruf. Beachten Sie, dass der `etag` Wert für den Client undurchsichtig sein und als Zeichenfolge, umgeben von Anführungszeichen, angegeben werden muss.

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

Die Repository-API reagiert mit dem Status 304 Nicht geändert, wenn die letzte Version der Instanz mit dem angegebenen Tag identisch ist.

### Instanzen der Liste für ein Schema - Sortieren und Paging

Kunden können die Instanzen, die sie erstellen, nicht verfolgen und können daher über ihre physische instanceId darauf zugreifen. Die Verwendung der Read-Instanz-API bildet die Ausnahme. Kunden wissen auch nicht, welche Instanzen andere Clients erstellt haben.

Ein typischeres Zugriffsmuster ist die Seite durch den Satz aller Instanzen.

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

Die Antwort hängt von der `{schemaId}` angegebenen ab. Für &quot;https<span></span>://ns.adobe.com/experience/Angebot-management/Angebot-Aktivität&amp;id=xcore:Angebot-Aktivität:fa24f9e8fc15c73&quot;entspricht die Antwort beispielsweise folgendem:

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

>[!NOTE] Das Ergebnis enthält die Instanzen für das angegebene Schema oder die erste Seite dieser Liste. Beachten Sie, dass Instanzen mehr als einem Schema entsprechen können und daher in mehr als einer Liste angezeigt werden können.

Seitenressourcen sind transient und schreibgeschützt. sie können nicht aktualisiert oder gelöscht werden. Das Paging-Modell bietet zufälligen Zugriff auf Teilmengen großer Listen über einen längeren Zeitraum hinweg, ohne dass der Status pro Client beibehalten wird.

Um auf diese Weise auf eine Instanz-Liste pro Seite zugreifen zu können, muss es möglich sein, eine stabile Sortierung über die von dieser Instanz-Liste aufgezählten Einträge zu definieren. Beachten Sie, dass &quot;stabil&quot;nicht bedeutet, dass Instanzen auf einer vordefinierten Seite angezeigt werden. Wenn eine Seitenreihenfolge durch Sortieren von Instanzen gemäß einer Eigenschaft P gebildet wird und ein Client diese Eigenschaft P aktualisiert, kann ein anderer Client diese Instanz erneut auf einer anderen Seite erreichen, während er durch die Liste blättert. Mit anderen Worten: Das Modell bevorzugt die Rückgabe aktuellerer Ergebnisse.

Wenn die Sortierreihenfolge jedoch auf einer nicht änderbaren Eigenschaft basiert, garantiert eine &quot;stabile&quot;Sortierreihenfolge, dass alle Instanzen, die zu Beginn des Seitenvorgangs vorhanden waren, erreicht werden (es sei denn, sie wurden beim Erreichen der Seite gelöscht). Befindet sich diese Sortierreihenfolge auf einer Eigenschaft, die monoton zunimmt, werden auch Instanzen erreicht, die nach dem Starten des Paging-Vorgangs erstellt wurden.

Ein Client kann Hinweise zur gewünschten Seitengröße geben, aber es liegt ganz am Repository, mehr oder weniger Instanzen mit der zurückgegebenen Seite bereitzustellen. Um eine stabile Reihenfolge zu gewährleisten, muss der Dienst Elemente der Seite hinzufügen oder entfernen, damit der Wert der Sortiereigenschaft über Seitengrenzen hinweg unterschiedlich ist. Auf diese Weise enthält die nächste Seite keine Elemente der letzten Seite mehr oder im schlimmsten Fall bleiben auf jeder Seite dieselben Elemente hängen.

Die Paging-Funktion wird durch folgende Parameter gesteuert:

- **`orderBy`**: Enthält eine kommagetrennte, geordnete Liste von Eigenschaften, nach denen die Liste der Instanz sortiert ist. Die erste Eigenschaft wird für die primäre Sortierung verwendet, die zweite Eigenschaft zum Auflösen von Verbindungen in der primären Sortierung usw. Wenn eine Eigenschaft angegeben wird, die einen eindeutigen Wert pro Instanz hat, sind keine Verknüpfungen möglich, und nach jedem Element kann ein Seitenumbruch auftreten. Dem Namen einer Eigenschaft kann ein Präfix vorangestellt werden, `+` um die aufsteigende Reihenfolge anzugeben oder die absteigende Reihenfolge durch diese Eigenschaft anzugeben `-` . Wenn der Eigenschaftsname nicht vorangestellt wird, wird das Ergebnis in aufsteigender Reihenfolge sortiert. Wenn in der Anforderung nicht angegeben `orderBy` ist, verwendet das Repository stattdessen die physische instanceId-Eigenschaft.
- **`start`**: Clients verwenden den Parameter Beginn, um die Seite zu definieren, die sie abrufen möchten. Der Beginn-Parameter bestimmt den Anfang der gewünschten Seite. Die Antwort enthält Instanzen, die mit Instanzen beginnen, die einen `orderBy` Eigenschaftswert haben, der strikt größer ist als (für aufsteigende Werte) oder strikt kleiner als (für absteigende Werte) der angegebene Wert. Wenn der Parameter &quot;Abfrage&quot;nicht angegeben wird, wird standardmäßig der Wert instanceId verwendet, der vor dem ersten Instanzbezeichner sortiert wird. Daher wird dieser Wert auf der ersten Seite weggelassen.
- **`limit`**: gibt eine positive Ganzzahl als Hinweis auf die maximale Anzahl von Elementen an, die für eine bestimmte Anforderung zurückgegeben werden sollen. Die tatsächliche Antwortgröße kann kleiner oder größer sein, da eine zuverlässige Funktion des Beginn-Parameters erforderlich ist

### Filtern von Listen

Das Filtern von Listen ist möglich und erfolgt unabhängig vom Seitenmechanismus. Filter überspringen Instanzen einfach in der Reihenfolge der Listen oder fordern explizit nur die Instanzen auf, die eine bestimmte Bedingung erfüllen. Ein Client kann die Verwendung des Ausdrucks der Eigenschaft als Filter anfordern oder eine Liste von URIs angeben, die als Werte des Primärschlüssels der Instanzen verwendet werden sollen.

- **`property`**: Enthält einen Eigenschaftsnamenpfad gefolgt von einem Vergleichsoperator gefolgt von einem Wert. <br/>
Die zurückgegebene Liste von Instanzen enthält die Instanzen, für die der Ausdruck &quot;true&quot;ergibt. Angenommen, die Instanz verfügt über eine Payload-Eigenschaft `status``draft``approved``archived``deleted``property=_instance.status==approved`<br/>




- Für Eigenschaften mit Zeichenfolgen-, numerischen oder Datums-/Uhrzeitwerten sind folgende Operatoren zulässig: `==`, `!=`, `<`, `<=`, `>` und `>=`. Darüber hinaus `~` kann für Eigenschaften mit einem Zeichenfolgenwert ein Operator verwendet werden. Der `~` -Operator stimmt mit der angegebenen Eigenschaft gemäß einem regulären Ausdruck überein. Der Zeichenfolgenwert der Eigenschaft muss mit dem **gesamten** Ausdruck übereinstimmen, damit die Entitäten in die gefilterten Ergebnisse einbezogen werden. Wenn Sie beispielsweise nach der Zeichenfolge `cars` an einer beliebigen Stelle im Eigenschaftswert suchen, muss der reguläre Ausdruck `.*cars.*`vorhanden sein. Ohne den Anfang oder das Ende `.*`stimmen nur Entitäten überein, bei denen ein Eigenschaftswert beginnt oder endet `cars`. Für den `~` Operator wird beim Vergleich von Buchstaben nicht zwischen Groß- und Kleinschreibung unterschieden. Bei allen anderen Operatoren wird beim Vergleich die Groß-/Kleinschreibung beachtet.<br/><br/>
In Filter-Ausdrücken können nicht nur Instanznutzlasteigenschaften verwendet werden. Die Hülleneigenschaften werden auf die gleiche Weise verglichen, z. `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Der Parameter `property` &quot;Abfrage&quot;kann wiederholt werden, sodass mehrere Filterbedingungen angewendet werden, z. B. um alle Instanzen zurückzugeben, die nach einem bestimmten Datum und vor einem bestimmten Datum zuletzt geändert wurden. Die Werte in diesen Ausdrücken müssen URL-kodiert sein. Wenn kein Ausdruck angegeben ist und der Name der Eigenschaft einfach aufgelistet ist, sind die Elemente, die eine Eigenschaft mit dem angegebenen Namen haben, die entsprechenden Kriterien.<br/>
<br/>

**`id`**: Manchmal muss eine Liste durch den URI der Instanzen gefiltert werden. Der Parameter `property` &quot;Abfrage&quot;kann verwendet werden, um eine Instanz zu filtern. Um jedoch mehr als eine Instanz zu erhalten, kann der Anforderung eine Liste von URIs zugewiesen werden. Der `id` Parameter wird wiederholt, und jedes Vorkommen gibt einen URI-Wert an. Die URI-Werte müssen URL-kodiert sein. `id={URI_1}&id={URI_2},…`

Seitenergebnisse werden als spezieller MIME-Typ zurückgegeben `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Anfrage**

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

**Antwort**

### Die Antwort enthält die Liste der Ergebniselemente in den Ergebnissen der JSON-Eigenschaft neben zwei Eigenschaften, die die Anzahl der Ergebnisse auf dieser Seite und die Gesamtanzahl der Elemente in der gefilterten Liste angeben, beginnend mit der soeben zurückgegebenen Seite.

Volltextsuche und strukturierte Abfragen

**In Fällen, in denen Kunden komplexere Filterbedingungen und Suchinstanzen nach Begriffen in Zeichenfolgeneigenschaften bereitstellen möchten, stellt das Repository eine leistungsfähigere Such-API bereit.**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

**Anfrage**

Zusätzlich zu den Paging- und Filterparametern aus den Liste-APIs ermöglicht diese API den Clients das Hinzufügen von Volltext- und booleschen Abfragen-Parametern.

- **`q`**Die Volltextsuche wird durch die folgenden Parameter gesteuert:`q`[]
- **`q`**: Enthält eine durch Leerzeichen getrennte, ungeordnete Liste von Begriffen, die normalisiert werden, bevor sie mit Zeichenfolgeneigenschaften der Instanzen abgeglichen werden. Zeichenfolgeneigenschaften werden auf Begriffe analysiert und diese Begriffe werden ebenfalls normalisiert. Die Abfrage &quot;Suchen&quot;versucht, einem oder mehreren der im `q` Parameter angegebenen Begriffe zu entsprechen. Die Zeichen +, -, =, &amp;, ||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, : / haben eine besondere Bedeutung für die Bestimmung der Wortgrenzen in der Abfrage-Zeichenfolge und sollten bei der Darstellung in einem Token, das mit dem Zeichen übereinstimmen sollte, mit einem umgekehrten Schrägstrich versehen werden. Die Zeichenfolge für die Abfrage kann durch Anführungszeichen für die Dublette der exakten Zeichenfolgenübereinstimmung und um Sonderzeichen zu Escape-Zeichen umgeben werden.
- **`field`**: Wenn die Suchbegriffe nur mit einer Untergruppe der Eigenschaften übereinstimmen sollten, kann der Feldparameter den Pfad zu dieser Eigenschaft angeben. Der Parameter kann wiederholt werden, um mehr als eine Eigenschaft anzugeben, die abgeglichen werden soll.

### **`qop`**: Enthält einen Steuerungsparameter, mit dem das passende Verhalten der Suche geändert wird. Wenn der Parameter auf festgelegt ist und dann alle Suchbegriffe übereinstimmen müssen und wenn der Parameter fehlt oder sein Wert auf gesetzt ist oder dann kann jeder Begriff für eine Übereinstimmung zählen.

Aktualisieren und Patchen von Instanzen

Um eine Instanz zu aktualisieren, kann ein Client entweder die gesamte Liste von Eigenschaften gleichzeitig überschreiben oder eine JSON PATCH-Anforderung verwenden, um einzelne Eigenschaftenwerte einschließlich Listen zu bearbeiten.[](#create-instances)`Location``containerId``instanceId`

In beiden Fällen gibt die URL der Anforderung den Pfad zur physischen Instanz an, und in beiden Fällen ist die Antwort eine JSON-Quittung wie die vom [Erstellungsvorgang](#create-instances)zurückgegebene Nutzlast. Ein Client sollte vorzugsweise den `Location` Header oder einen HAL-Link verwenden, den er von einem vorherigen API-Aufruf für dieses Objekt erhalten hat, als vollständigen URL-Pfad für diese API. Ist dies nicht möglich, kann der Client die URL aus der `containerId` und der `instanceId`.

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

**Anforderung** (PUT)

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

**Anforderung** (PATCH)

**Die PATCH-Anforderung wendet die Anweisungen an und validiert dann die resultierende Entität gegen das Schema und dieselben Entitäts- und Referenziellen Integritätsregeln wie die PUT-Anforderung.**

**Bearbeiten von Eigenschaftswerten steuern**

- **`"meta:usereditable"`**Mithilfe der folgenden Anmerkungen können Sie verhindern, dass Eigenschaften beim Erstellen und/oder Aktualisieren festgelegt werden:`"meta:usereditable": false`
- **`"meta:usereditable"`**: Boolescher Wert: Wenn eine Anforderung von einem Benutzeragenten stammt, der den Aufrufer mit einem Zugriffstoken für ein Benutzerkonto oder ein technisches Konto identifiziert, `"meta:usereditable": false` sollten Eigenschaften, mit denen eine Anmerkung versehen wurde, nicht in der Payload vorhanden sein. Ist dies der Fall, dürfen sie keinen anderen Wert haben als den, der derzeit festgelegt wird. Wenn sich die Werte unterscheiden, wird die Anforderung zum Aktualisieren oder Patch mit dem Status 422 Nicht verarbeitbare Entität abgelehnt.

**`"meta:immutable"`**: Boolescher Wert: Eigenschaften, die mit Anmerkungen versehen sind, `"meta:immutable": true` können nach dem Festlegen nicht mehr geändert werden. Dies gilt für Anfragen, die von einem Endbenutzer, einer technischen Kontointegration oder einem besonderen Dienst kommen.**

**Test auf gleichzeitige Aktualisierung**`etag``etag``etag`

### Es gibt Bedingungen, unter denen mehrere Clients versuchen, eine Instanz gleichzeitig zu aktualisieren. Das Repository wird auf einem Cluster von Rechnerknoten ohne zentrale Transaktionsverwaltung betrieben. Um zu vermeiden, dass ein Client eine Instanz schreibt, die gleichzeitig von einer anderen geschrieben wird, können die Clients eine bedingte Update- oder Patch-Anforderung verwenden. Wenn Sie die `etag` Zeichenfolge in der Kopfzeile angeben, muss `If-Match` das Repository sicherstellen, dass nur die erste Anforderung erfolgreich ist und die Folgeanforderungen anderer Clients, die denselben `etag` Wert verwenden, fehlschlagen. Der `etag` Wert ändert sich mit jeder Änderung der Instanz. Clients müssen die Instanz abrufen, um den neuesten `etag` Wert abzurufen, und dann kann nur ein von vielen Clients, die die Aktualisierung versuchen, diesen Wert verwenden. Andere Kunden werden mit der Meldung 409 Konflikt abgelehnt.

Löschen von Instanzen`Location``containerId``instanceId`

Instanzen können mit einem DELETE-Aufruf gelöscht werden. Ein Client sollte vorzugsweise den `Location` Header oder einen HAL-Link verwenden, den er von einem vorherigen API-Aufruf dafür erhalten hat, als vollständigen URL-Pfad. Ist dies nicht möglich, kann der Client die URL aus dem `containerId` und dem physischen `instanceId`.

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Anfrage**

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

**Antwort**

Nach Erhalt einer Löschanforderung prüft das Repository, ob andere Instanzen eines beliebigen Schemas auf die zu löschende Instanz verweisen. In einem verteilten, hochverfügbaren System kann die referenzielle Integrität nicht sofort überprüft werden. Wenn Fremdschlüsselbeziehungen definiert sind, werden Prüfungen asynchron durchgeführt. Dies führt zu einer etwas verzögerten Antwort auf das Ergebnis der Löschanforderung. Wenn diese Prüfungen durchgeführt werden, enthält die sofortige Antwort den Status 202 Akzeptiert und einen Link, um das Ergebnis des Löschvorgangs in der `Location` Kopfzeile zu überprüfen. Ein Kunde sollte dann diesen Link für das Ergebnis überprüfen.

## Wenn eine Instanz gefunden wird, die auf die zu löschende Instanz verweist, wird der Löschvorgang abgelehnt. Wenn keine weiteren Fremdschlüsselverweise gefunden werden, wird der Löschvorgang abgeschlossen. Wenn das Ergebnis noch nicht entschieden ist, zeigt die Antwort, dass durch weitere 202 Akzeptierte Antwort mit der gleichen `Location` Kopfzeile und fordert den Kunden, die Überprüfung. Wenn das Ergebnis bestimmt wird, zeigt die Antwort an, dass mit einem 200-Ok-Status und der Nutzlast der Antwort das Ergebnis der ursprünglichen Löschanforderung enthalten ist. Beachten Sie, dass die Antwort &quot;200 OK&quot;nur bedeutet, dass das Ergebnis bekannt ist und der Antworttext die Bestätigung oder Ablehnung der Löschanforderung enthält.

Erstellen von Angeboten und ihren Unterkomponenten`content-type`

Die im vorherigen Abschnitt beschriebenen APIs gelten einheitlich für alle Typen von Geschäftsobjekten. Der einzige Unterschied zwischen z. B. dem Erstellen eines Angebots und einer Aktivität ist der `content-type` Header, der das JSON-Schema und die JSON-Nutzlast der Anforderung angibt, die dem Schema entspricht. Daher müssen sich die folgenden Abschnitte nur auf diese Schemas und die Beziehungen zwischen ihnen konzentrieren.`_instance``_links`

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

>Bei Verwendung der APIs mit dem Inhaltstyp `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`werden die eigenen Eigenschaften der Instanz in die `_instance` Eigenschaft eingebettet, neben der eine `_links` Eigenschaft vorhanden ist. Dies ist das allgemeine Format, in dem alle Instanzen dargestellt werden:

### [!NOTE] Aus Gründen der Kürze werden in allen JSON-Snippets nur die Instanzeigenschaften veranschaulicht und nur dann, wenn dies erforderlich ist, werden die Hülleneigenschaften und der Abschnitt &quot;_links&quot;angezeigt.

Allgemeine Eigenschaften von Angeboten

- **`@id`**Angebot sind eine Art Entscheidungsoption und das JSON-Schema von Angeboten übernimmt die Standardoptionseigenschaften, über die jede Optionsinstanz verfügt.
- **`@id`** - Ein eindeutiger Bezeichner für jede Option, bei der es sich um den Primärschlüssel handelt und mit dem auf die Option von anderen Objekten verwiesen wird. Diese Eigenschaft wird zugewiesen, wenn die Instanz erstellt wird, unveränderlich und nicht bearbeitbar ist.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

**`xdm:name`** - Jede Option hat einen Namen, der für Such- und Anzeigezwecke verwendet wird. Der Name ist nicht unveränderlich und kann nicht zur eindeutigen Identifizierung der Instanz verwendet werden. Der Name kann frei ausgewählt werden, sollte jedoch in allen Angebot-Instanzen eindeutig sein.](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss ein `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` ein Fallback-Angebot sein.

### Jede Angebot-Instanz kann über einen optionalen Satz von Eigenschaften verfügen, die nur für diese Instanz charakteristisch sind. Verschiedene Angebot können unterschiedliche Schlüssel für diese Eigenschaften haben. Die Werte müssen jedoch Zeichenfolgen sein. Diese Eigenschaften können in Entscheidungs- und Segmentierungsregeln verwendet werden. Sie sind auch verfügbar, um das beschlossene Erlebnis zusammenzustellen, um die Nachrichten weiter anzupassen.

Lebenszyklus von Angeboten

![](../images/entities/offer-lifecycle.png)Es gibt einen einfachen Status-Transition-Fluss, dem alle Optionen folgen. Sie werden in einem Entwurfszustand Beginn, und wenn sie bereit sind, wird ihr Zustand auf die Genehmigung eingestellt. Nach Ablauf des Enddatums können sie in den archivierten Zustand verschoben werden. In diesem Zustand können sie gelöscht oder wiederverwendet werden, indem sie wieder in den Entwurfszustand versetzt werden.

- ![](../images/entities/offer-lifecycle.png)

**`xdm:status`** - Diese Eigenschaft wird für das Lebenszyklusmanagement der Instanz verwendet. Der Wert stellt einen Workflow-Status dar, der angibt, ob das Angebot noch in der Konstruktion ist (value = draft), allgemein von der Laufzeit berücksichtigt werden kann (value = authorised) oder ob es nicht mehr verwendet werden sollte (value = archived).

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Ein einfacher PATCH-Vorgang für die Instanz wird normalerweise dazu verwendet, eine `xdm:status` Eigenschaft zu manipulieren:](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

### Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss ein `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` ein Fallback-Angebot sein.

Repräsentationen und Praktika

Angebot sind Entscheidungsoptionen mit Inhaltsdarstellungen. Wenn eine Entscheidung getroffen wird, wird die Option ausgewählt und ihre Kennung verwendet, um die Inhalte oder Inhaltsreferenzen für die Bereitstellung abzurufen, die bereitgestellt werden muss. Ein Angebot kann mehrere Darstellungen aufweisen, für jedes muss jedoch eine andere Platzierungsreferenz vorhanden sein. Dadurch wird sichergestellt, dass die Darstellung mit einer bestimmten Platzierung eindeutig bestimmt werden kann.
Während des Entscheidungsvorgangs wird die Platzierung zusammen mit dem Objekt &quot;Aktivität&quot;bestimmt. Angebot, die mit dieser Platzierung als Referenz nicht repräsentiert sind, werden automatisch aus der Liste der Auswahlmöglichkeiten entfernt.`https://ns.adobe.com/experience/offer-management/offer-placement`

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

Bevor einem Angebot Darstellungen hinzugefügt werden können, müssen die Platzierungsinstanzen vorhanden sein. Diese Instanzen werden mit der Schema-ID`https://ns.adobe.com/experience/offer-management/offer-placement`erstellt.](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss ein `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` ein Fallback-Angebot sein.

- Eine **Platzierungsinstanz** kann die folgenden Eigenschaften aufweisen:
- **`xdm:name`** - Enthält zugewiesene Namen für die Platzierung, auf die in menschlichen Interaktionen und Benutzeroberflächen verwiesen wird.
- **`xdm:description`** - Dient zum Vermitteln von für Menschen lesbaren Absichten darüber, wie Inhalte in dieser Platzierung im gesamten Versand der Nachricht verwendet werden. Wenn Versand-Kanal neue Platzierungen definieren, können sie weitere Informationen zu dieser Eigenschaft hinzufügen, damit ein Inhaltsersteller den Inhalt entsprechend erstellen oder auswählen kann. Diese Anweisungen werden nicht formell ausgelegt oder durchgesetzt. Diese Eigenschaft dient lediglich als Ort, um die Absichten zu kommunizieren.
- **`xdm:channel`** - Der URI eines Kanals. Der Kanal gibt an, wo der dynamische Inhalt bereitgestellt werden soll. Die Kanal-Beschränkung wird verwendet, um nicht nur zu vermitteln, wo das Angebot verwendet wird, sondern auch um den Content-Editor oder Validator zu bestimmen, der für das Erlebnis verwendet wird.
   - **`xdm:componentType`** - Eine Modellkennung, d. h. URI, für den Inhalt, der an dem durch diese Platzierung beschriebenen Ort angezeigt werden kann. Komponententypen sind: Bild-Link, HTML oder Nur-Text. Jeder Komponententyp kann einen bestimmten Satz von Eigenschaften (ein Modell) beinhalten, über die das Inhaltselement verfügen kann. Die Liste von Komponententypen kann erweitert werden. Es gibt drei vordefinierte Komponententypwerte:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
- `https://ns.adobe.com/experience/offer-management/content-component-html`

**`xdm:contentTypes`**, Eine Beschränkung für die Medientypen der Komponenten, die bei dieser Platzierung erwartet werden. Es kann mehr als einen Medientyp für einen Komponententyp geben, z. B. verschiedene Bildformate.**`xdm:representations`

- **Darstellungselemente** in einem Angebot haben eine Objektstruktur in der Array-Eigenschaft `xdm:representations`. Jedes Element kann die folgenden Eigenschaften aufweisen:
- **`xdm:placement`** - Diese Eigenschaft enthält den Verweis auf die Platzierungsinstanz. Der Wert wird überprüft, wenn die Darstellung dem Angebot hinzugefügt wird. Eine Platzierungsinstanz mit diesem URI muss vorhanden sein und darf nicht als gelöscht markiert werden. Darüber hinaus wird eine Überprüfung durchgeführt, um sicherzustellen, dass eine Angebot-Instanz nicht über zwei Darstellungen mit demselben Wert für ihre Platzierungsreferenz verfügt.
   - **`xdm:components`** - Inhaltskomponenten sind die mit einer bestimmten Angebotsdarstellung verknüpften Fragmente. Diese Fragmente werden später verwendet, um das Endbenutzererlebnis zu erstellen. Beachten Sie, dass der Entscheidungsdienst selbst nicht die gesamte Endbenutzererfahrung zusammenstellt. Die folgenden Eigenschaften sind Teil des Modells jeder Komponente.`@type`
   - **`@type`** - diese Eigenschaft identifiziert den Komponententyp. Ein anderer Name für dieses Konzept ist das Inhaltsfragmentmodell. Die Komponente `@type` ist lediglich ein URI für ein Modell, das von der Anwendung oder dem Dienst definiert wird, die bzw. der das Endbenutzererlebnis zusammenstellt.
   - **`repo:id`** - diese Eigenschaft enthält einen global eindeutigen, unveränderlichen Bezeichner für die Hauptressource der Komponente im Repository, in dem das Asset gespeichert wird.
   - **`repo:name`** - Diese Eigenschaft enthält einen lesbaren Namen für das Asset im Repository. Dieser Name ist benutzerdefiniert und garantiert nicht eindeutig.
   - **`repo:resolveURL`** - diese Eigenschaft enthält eine eindeutige Ressourcensuche, um das Asset in einem Inhalts-Repository zu lesen. Dadurch wird es einfacher, das Asset abzurufen, ohne dass der Client versteht, welche APIs aufgerufen werden sollen. Die URL gibt die Bytes der primären Ressource des Assets zurück.
   - **`dc:format`** - diese Eigenschaft stammt von der Dublin Core Metadata Initiative. Das Format kann verwendet werden, um die Software, Hardware oder andere Geräte zu bestimmen, die zum Anzeigen oder Betrieb der Ressource erforderlich sind. Es wird empfohlen, einen Wert aus einem kontrollierten Vokabular auszuwählen (z. B. die Liste von Internetmedientypen, die Computermedienformate definieren).

**`dc:language`** - Diese Eigenschaft enthält die Sprache oder Sprachen der Ressource. Die Sprache wird im Sprachcode gemäß der Definition in IETF RFC 3066 angegeben.

- Es gibt drei vordefinierte Komponententypen, die in der `@type` Eigenschaft ausgedrückt werden:
- https<span></span>://ns.adobe.com/experience/Angebot-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/Angebot-management/content-component-text

https<span></span>://ns.adobe.com/experience/Angebot-management/content-component-html`xdm:components`

- Je nach Wert der `@type` Eigenschaft `xdm:components` enthält die folgenden zusätzlichen Eigenschaften:`user-agent`
- **`xdm:linkURL`** - Vorhanden, wenn die Komponente ein Bild-Link ist. Diese Eigenschaft enthält den Link, der mit dem Bild verknüpft ist und zu dem der Endbenutzer navigiert, wenn er mit dem Angebot interagiert. `user-agent`

**`xdm:copyline`** - Wird verwendet, wenn die Komponente ein Text ist. Zusätzlich zum Verweis auf ein Textelement, z. B. für Angebote mit langer Formulartextformatierung, die Formatierung enthalten können, kann eine kurze Textzeichenfolge direkt in der Eigenschaft xdm:copyline gespeichert werden.

- Clients können zusätzliche Eigenschaften verwenden, um Anweisungen zur Handhabung des Kontexts festzulegen und auszuwerten. Der Angebot UI Library Client fügt beispielsweise die folgenden optionalen Eigenschaften hinzu, um die Anzeige einfacher zu handhaben:`xdm:components`
   - Innerhalb jedes Elements im `xdm:components` Array fügt der UI-Client der Angebot-Bibliothek die folgenden Eigenschaften hinzu. Diese Eigenschaften sollten nicht gelöscht oder bearbeitet werden, ohne die Auswirkungen auf die Benutzeroberfläche zu verstehen:

**`offerui:previewThumbnail`** - Dies ist eine optionale Eigenschaft, die die Benutzeroberfläche der Angebot-Bibliothek verwendet, um eine Wiedergabe des Assets anzuzeigen. Diese Darstellung ist nicht mit dem Asset selbst identisch. Der Inhalt könnte beispielsweise HTML sein, und die Darstellung ist ein Bitmapbild, das nur eine Annäherung zeigt. Diese (minderwertige) Darstellung wird im Repräsentationsblock des Angebots angezeigt.

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

Ein Beispiel für einen PATCH-Vorgang auf einer Angebot-Instanz zeigt, wie die Darstellungen manipuliert werden:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer``https://ns.adobe.com/experience/offer-management/fallback-offer`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss ein `https://ns.adobe.com/experience/offer-management/personalized-offer` oder `https://ns.adobe.com/experience/offer-management/fallback-offer` ein Fallback-Angebot sein.

## Der PATCH-Vorgang kann fehlschlagen, wenn noch keine Eigenschaft vorhanden `xdm:representations` ist. In diesem Fall könnte dem oben genannten Vorgang zum Hinzufügen ein weiterer Vorgang vorangestellt werden, der das `xdm:representations` Array erstellt, oder der Vorgang zum einmaligen Hinzufügen legt das Array direkt fest.
Die beschriebenen Schema und Eigenschaften werden für alle Angebot-Typen, Personalisierungs-Angebot sowie Ausweich-Angebot verwendet. Die folgenden beiden Abschnitte zu Einschränkungen und Entscheidungsregeln erläutern die Aspekte von Personalisierungs-Angeboten.

### Festlegen von Einschränkungen für Angebot

Kalendereinschränkungen`xdm:selectionConstraint`

- Entscheidungsoptionen können generell ein Beginn und ein Enddatum und eine Uhrzeit angeben, die als Kalenderbeschränkung dienen. Die Eigenschaften sind in der Eigenschaft eingebettet `xdm:selectionConstraint`:
- **`xdm:startDate`** - Diese Eigenschaft gibt das Datum und die Uhrzeit des Beginns an. Der Wert ist eine Zeichenfolge, die nach RFC 3339-Regeln formatiert ist, d. h. wie in diesem Zeitstempel: &quot;2019-06-13T11:21:23.356Z&quot;.
Entscheidungsoptionen, die ihren Beginn noch nicht erreicht haben, werden bei der Entscheidung noch nicht berücksichtigt.

**`xdm:endDate`** - Diese Eigenschaft gibt das Enddatum und die Endzeit an. Der Wert ist eine Zeichenfolge, die nach RFC 3339-Regeln formatiert ist, d. h. wie in diesem Zeitstempel: &quot;2019-07-13T11:00:00.000Z&quot;Entscheidungsoptionen, die ihr Enddatum und ihre Uhrzeit überschritten haben, gelten im Entscheidungsprozess nicht mehr als zulässig.

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

Das Ändern einer Kalenderbeschränkung kann mit dem folgenden PATCH-Aufruf ausgeführt werden:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

### Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer`sein. Fallback-Angebot haben keine Einschränkungen.

Beschränkungen für die Deckelung`xdm:cappingConstraint`

- Eine Deckelungsbeschränkung ist eine Komponente in einer Entscheidungsoption, die die Parameter für die Deckelung definiert. Durch die Deckelung wird begrenzt, wie oft eine Option vorgeschlagen werden kann, sowohl für ein einzelnes Profil als auch für alle Profil. Die Eigenschaften enthalten einen ganzzahligen Wert, der größer oder gleich 1 sein muss. Die Eigenschaften sind innerhalb einer Eigenschaft verschachtelt `xdm:cappingConstraint`:
- **`xdm:globalCap`** - Eine globale Obergrenze ist eine Beschränkung dafür, wie oft ein Angebot in seiner Gesamtheit vorgeschlagen werden kann.

**`xdm:profileCap`** - Eine Profil-Obergrenze ist eine Einschränkung, wie oft ein Angebot einem bestimmten Profil vorgeschlagen werden kann.

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

Das Festlegen oder Ändern der Begrenzung für ein Personalisierungs-Angebot kann mit dem folgenden PATCH-Aufruf ausgeführt werden:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer`sein. Fallback-Angebot haben keine Einschränkungen.

### Um die Werte für die Begrenzung zu entfernen, wird der Vorgang &quot;add&quot;durch den Vorgang &quot;remove&quot;ersetzt. Beachten Sie, dass die Werte für die Begrenzung einzeln vorhanden sind und auch einzeln eingestellt oder entfernt werden können.

Berechtigungseinschränkungen

Angebot können im Entscheidungsprozess bedingt ausgewählt werden. Wenn ein Angebot zur Personalisierung einen Verweis auf eine Eignungsregel enthält, muss die Regelbedingung als &quot;true&quot;ausgewertet werden, damit das Angebot-Objekt für ein bestimmtes Profil berücksichtigt wird. Die Eignungsregeln werden unabhängig von den Entscheidungsoptionen erstellt und verwaltet. Dieselbe Regel kann von mehreren Personalisierungs-Angeboten referenziert werden.`xdm:selectionConstraint`

- Der Verweis auf die Regel ist in der Eigenschaft eingebettet `xdm:selectionConstraint`:`@id`

**`xdm:eligibilityRule`** - Diese Eigenschaft enthält einen Verweis auf eine Eignungsregel. Der Wert ist der `@id` einer Instanz von Schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Das Hinzufügen und Löschen einer Regel kann auch mit einem PATCH-Vorgang erfolgen:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer`sein. Fallback-Angebot haben keine Einschränkungen.

## Beachten Sie, dass die Eignungsregel zusammen mit den Kalenderbeschränkungen in die `xdm:selectionConstraint` Eigenschaft eingebettet ist. PATCH-Vorgänge sollten nicht versuchen, die gesamte `SelectionConstraint` Eigenschaft zu entfernen.

Festlegen der Priorität eines Angebots`xdm:rank`

- Qualifizierende Entscheidungsoptionen werden nach Rang geordnet, um die beste Option für das jeweilige Profil zu ermitteln. Um die Rangfolge zu unterstützen und eine Standardeinstellung anzugeben, falls die Rangfolge nicht durch einen anderen Mechanismus bestimmt werden kann, kann für jedes Personalisierungs-Angebot eine Basispriorität festgelegt werden.
Die Basispriorität ist in der Eigenschaft eingebettet `xdm:rank`:

**`xdm:priority`** - Diese Eigenschaft stellt die Standardreihenfolge dar, in der ein Angebot über einem anderen ausgewählt wird, falls keine spezielle Rangreihenfolge für Profil bekannt ist. Wenn nach dem Vergleich des Prioritätswerts immer noch zwei oder mehr Angebot zur Personalisierung gebunden sind, wird eines zufällig ausgewählt und im Angebotsvorschlag verwendet. Der Wert für diese Eigenschaft muss eine Ganzzahl größer oder gleich 0 sein.

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

Die Anpassung der Basispriorität kann mit dem folgenden PATCH-Aufruf erfolgen:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

## Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer`sein. Fallback-Angebot haben keine Rangeigenschaften.

Verwalten von Entscheidungsregeln

> Eignungsregeln verfügen über die Bedingungen, die bewertet werden, um festzustellen, ob eine bestimmte Entscheidungsoption für ein bestimmtes Profil infrage kommt. Wenn eine Regel einer oder mehreren Entscheidungsoptionen zugeordnet wird, muss die Regel für diese Option implizit &quot;true&quot;zurückgeben, damit die Option für diesen Benutzer berücksichtigt wird. Die Regel kann Tests zu Profil-Attributen enthalten, Ausdruck mit Erlebnis-Ereignissen für dieses Profil bewerten und Kontextdaten einschließen, die an die Entscheidungsanforderung weitergeleitet wurden. Eine Bedingung kann beispielsweise wie folgt beschrieben werden:

&quot;Schließen Sie Personen mit Elite-Status ein, die in den letzten sechs Monaten dreimal einen Flug durchgeführt haben und die die Flugnummer des aktuellen Fluges haben.&quot;`_instance`

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

Die Instanzen werden mit der Schema-ID https://ns.adobe.com/experience/offer-management/eligibility-rule erstellt. Die `_instance` Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/eligibility-rule`

Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/eligibility-rule`sein.

Der Wert in der Eigenschaft &quot;Bedingung&quot;der Regel enthält einen PQL-Ausdruck. Die Kontextdaten werden über den Ausdruck für speziellen Pfad @{schemaID} referenziert.[!DNL Experience Platform]`segmentMembership``segmentMembership`

## Regeln richten sich natürlich an Segmente in der Regel aus [!DNL Experience Platform] und oft wird die Segmentabsicht einfach wiederverwendet, indem die `segmentMembership` Eigenschaft eines Profils getestet wird. Die `segmentMembership` Eigenschaft enthält die Ergebnisse der Segmentbedingungen, die bereits bewertet wurden. Auf diese Weise kann eine Organisation ihre domänenspezifischen Audiencen einmal definieren, sie benennen und die Bedingungen einmal auswerten.

### Verwalten von Angebot-Sammlungen

Erstellen von Tags und Tagging-Angeboten

1. Angebot können in Sammlungen organisiert werden, in denen jede Sammlung die anzuwendende Filterbedingung definiert. Derzeit können Filter-Ausdruck in einer Sammlung eine von zwei Formularen haben:`@id`
2. Der `@id` Parameter des Angebots muss mit einem in einer Liste von Bezeichnern übereinstimmen, damit das Angebot in der Sammlung enthalten ist. Dieser Filter ist lediglich eine Auflistung der URIs der Angebot in der Sammlung.\
   Ein Angebot kann eine Liste von Tagverweisen haben und der Filter der Sammlung besteht aus einer Liste von Tags. Das Angebot befindet sich in der Sammlung, wenn:\
   a. eines der Tags des Filters mit einem der Tags des Angebots übereinstimmt

b. alle Tags des Filters entsprechen einem der Tags des Angebots

Tags sind einfache Instanzen, mit denen Angebot-Instanzen verknüpft werden können. Es handelt sich dabei um eigenständige Instanzen mit einem Namen, um sie anzuzeigen. Der Name muss in allen Instanzen eindeutig sein, um die Anzeige in der Benutzeroberfläche zu vereinfachen.

Tag-Objekte dienen dazu, eine Kategorisierung der Entscheidungsoptionen (Angebot) festzulegen. Ein Tag kann von vielen Angeboten verknüpft werden und ein Angebot kann viele Tag-Verweise aufweisen. Eine Kategorie von Angeboten wird erstellt, indem auf alle Angebot verwiesen wird, die zu einem bestimmten Satz von Tag-Instanzen gehören.`_instance`

```json
{
  "xdm:name": "credit card"
} 
```

Die Tag-Instanzen werden mit der Schema-ID https://ns.adobe.com/experience/offer-management/tag erstellt. Die `_instance` Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/tag`


Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/tag`sein.

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Eine Angebot-Instanz kann mit der Liste von Tag-Verweisen wie:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Alternativ kann ein Angebot gepatcht werden, um die Liste der Tags zu ändern:[](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/personalized-offer`

In beiden Fällen finden Sie die vollständige cURL-Syntax unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/personalized-offer`sein.

### Beachten Sie, dass die `xdm:tags` Eigenschaft bereits vorhanden sein muss, damit der Vorgang zum Hinzufügen erfolgreich ist. Es gibt keine Tags in einer Instanz, in der der PATCH-Vorgang zuerst die Array-Eigenschaft hinzufügen und dann einen Tag-Verweis zu diesem Array hinzufügen kann.

Filter für Angebot-Sammlungen definieren`_instance`

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

Die Filterinstanzen werden mit der Schema-ID https://ns.adobe.com/experience/offer-management/offer-filter erstellt. Die `_instance` Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren könnte wie folgt aussehen:](#updating-and-patching-instances)`schemaId``https://ns.adobe.com/experience/offer-management/offer-filter`

- Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/offer-filter`sein.
   - **`xdm:filterType`** - Diese Eigenschaft gibt an, ob der Filter mithilfe von Tags eingerichtet wird oder direkt auf Angebot durch ihre IDs verweist. Wenn der Filter so eingerichtet ist, dass Tags verwendet werden, kann der Filtertyp außerdem angeben, ob alle Tags mit den Tags eines bestimmten Angebots übereinstimmen müssen oder ob eines der angegebenen Tags ausreicht, damit das Angebot für den Filter qualifiziert ist. Die gültigen Werte dieser Enum-Eigenschaft sind:
   - `offers`
   - `anyTags`
- `allTags``xdm:filterType`

**`ids`** - Eine Eigenschaft enthält ein Array von URIs, die je nach Wert von Angebot-Instanzen oder Tag-Instanzen referenzieren `xdm:filterType`. .

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

## Der folgende Aufruf zeigt, wie die `_instance` Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren aussieht, wenn direkt auf Angebot verwiesen wird:

Verwalten von Aktivitäten

Zur Steuerung des Entscheidungsprozesses wird eine Angebot-Aktivität verwendet. Er gibt den auf den Gesamtbestand angewendeten Angebot-Filter an, um Angebot nach Thema/Kategorie einzugrenzen, die Platzierung, um den Bestand auf die Angebot einzugrenzen, die in den reservierten Bereich passen, und eine Ausweichoption an, falls die kombinierten Einschränkungen alle verfügbaren Personalisierungsoptionen (Angebot) deaktivieren.`https://ns.adobe.com/experience/offer-management/offer-activity``_instance`

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

Die Instanzen der Aktivität werden mit der Schema-ID`https://ns.adobe.com/experience/offer-management/offer-activity`erstellt. Die `_instance` Eigenschaft für den Aufruf zum Erstellen oder Aktualisieren sieht wie folgt aus:`schemaId``https://ns.adobe.com/experience/offer-management/offer-activity`

- Die vollständige cURL-Syntax finden Sie unter [Aktualisieren und Patchen von Instanzen](#updating-and-patching-instances) . Der `schemaId` Parameter muss `https://ns.adobe.com/experience/offer-management/offer-activity`sein.
- **`xdm:name`** - Diese obligatorische Eigenschaft enthält den Namen der Aktivität. Der Name wird in verschiedenen Benutzeroberflächen angezeigt.
- **`xdm:status`** - Diese Eigenschaft wird für das Lebenszyklusmanagement der Instanz verwendet. Der Wert stellt einen Workflow-Status dar, der angibt, ob die Aktivität noch im Aufbau ist (value = draft), allgemein von der Laufzeit berücksichtigt werden kann (value = live) oder ob sie nicht mehr verwendet werden sollte (value = archived).`@id`
- **`xdm:placement`** - Eine obligatorische Eigenschaft, die einen Verweis auf eine Platzierung eines Angebots enthält, die auf das Inventar angewendet wird, wenn eine Entscheidung im Kontext dieser Aktivität getroffen wird. Der Wert ist der URI (`@id`) der verwendeten Platzierung des Angebots.
- **`xdm:filter`** - Eine obligatorische Eigenschaft, die einen Verweis auf einen Angebot-Filter enthält, der auf das Inventar angewendet wird, wenn im Rahmen dieser Aktivität eine Entscheidung getroffen wird. Der Wert ist der URI (`@id`) des verwendeten Angebot-Filters.

### **`xdm:fallback`** - Eine obligatorische Eigenschaft, die einen Verweis auf ein Fallback-Angebot enthält. Ein Ausweichmanöver-Angebot wird verwendet, wenn die Entscheidung für diese Aktivität keines der personalisierbaren Angebot qualifiziert. Der Wert ist der URI (`@id`) einer Fallback-Angebot-Instanz.

Verwalten von Fallback-Angeboten`https://ns.adobe.com/experience/offer-management/fallback-offer``_instance`

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

Bevor Instanzen der Aktivität erstellt werden können, muss ein Ausweichmanöver-Angebot vorhanden sein, das für die Platzierung der Aktivität geeignet ist. Die Fallback-Angebot-Instanzen werden mit der Schema-ID`https://ns.adobe.com/experience/offer-management/fallback-offer`erstellt. Die `_instance` Eigenschaft des Erstellungs- oder Aktualisierungsaufrufs enthält dieselben allgemeinen Eigenschaften wie ein Personalisierungs-Angebot, kann jedoch keine anderen Einschränkungen aufweisen.`schemaId``https://ns.adobe.com/experience/offer-management/fallback-offer`

