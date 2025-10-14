---
keywords: Experience Platform;Startseite;beliebte Themen;Sandbox-Entwicklerhandbuch
solution: Experience Platform
title: Sandbox-Management-API - Endpunkt
description: Mit dem Endpunkt /sandboxes in der Sandbox-API können Sie Sandboxes in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 44%

---

# Sandbox-Management-Endpunkt

Sandboxes in Adobe Experience Platform bieten isolierte Entwicklungsumgebungen, mit denen Sie Funktionen testen, Experimente durchführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Produktionsumgebung zu beeinträchtigen. Mit dem `/sandboxes`-Endpunkt in der [!DNL Sandbox]-API können Sie Sandboxes in Experience Platform programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Sandboxes {#list}

Sie können alle Sandboxes Ihrer Organisation (aktiv oder nicht) auflisten, indem Sie eine GET-Anfrage an den `/sandboxes`-Endpunkt senden.

**API-Format**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse nach . Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](./appendix.md#query) Abfrageparameter . |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandboxes zurück, die zu Ihrer Organisation gehören, einschließlich Details wie `name`, `title`, `state` und `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Sandbox. Diese Eigenschaft wird für Suchzwecke in API-Aufrufen verwendet. |
| `title` | Der Anzeigename für die Sandbox. |
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann einer der folgenden sein: <br/><ul><li>`creating`: Die Sandbox wurde erstellt, wird aber noch vom System bereitgestellt.</li><li>`active`: Die Sandbox wird erstellt und aktiv.</li><li>`failed`: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>`deleted`: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ. Zu den derzeit unterstützten Sandbox-Typen gehören `development` und `production`. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die standardmäßige Produktions-Sandbox für die Organisation ist. |
| `eTag` | Eine Kennung für eine bestimmte Version der Sandbox. Dieser Wert erleichtert Versionskontrolle und Caching und wird bei jeder Änderung an der Sandbox aktualisiert. |

## Nachschlagen einer Sandbox {#lookup}

Sie können eine Sandbox mittels GET-Anfrage nachschlagen, in der Sie im Anfragepfad die `name`-Eigenschaft der jeweiligen Sandbox angeben.

**API-Format**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie nachschlagen möchten. |

**Anfrage**

Mit der nachfolgenden Anfrage wird eine Sandbox namens „dev-2“ abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Bei erfolgreicher Antwort werden Details zur Sandbox einschließlich `name`, `title`, `state` und `type` zurückgegeben.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name der Sandbox. Diese Eigenschaft wird für Suchzwecke in API-Aufrufen verwendet. |
| `title` | Der Anzeigename für die Sandbox. |
| `state` | Der aktuelle Verarbeitungsstatus der Sandbox. Der Status einer Sandbox kann wie folgt lauten: <ul><li>**Erstellen**: Die Sandbox wurde erstellt, wird jedoch weiterhin vom System bereitgestellt.</li><li>**Aktiv**: Die Sandbox ist erstellt und aktiv.</li><li>**Fehlgeschlagen**: Aufgrund eines Fehlers konnte die Sandbox nicht vom System bereitgestellt werden und ist deaktiviert.</li><li>**Gelöscht**: Die Sandbox wurde manuell deaktiviert.</li></ul> |
| `type` | Der Sandbox-Typ. Zu den derzeit unterstützten Sandbox-Typen gehören: `development` und `production`. |
| `isDefault` | Eine boolesche Eigenschaft, die angibt, ob diese Sandbox die Standard-Sandbox für die Organisation ist. In der Regel ist dies die Produktions-Sandbox. |
| `eTag` | Eine Kennung für eine bestimmte Version der Sandbox. Dieser Wert erleichtert Versionskontrolle und Caching und wird bei jeder Änderung an der Sandbox aktualisiert. |

## Erstellen einer Sandbox {#create}

>[!NOTE]
>
>Wenn eine neue Sandbox erstellt wird, müssen Sie diese neue Sandbox zunächst Ihrem Produktprofil in [Adobe Admin Console](https://adminconsole.adobe.com/) hinzufügen, bevor Sie sie verwenden können. Weitere Informationen zur Bereitstellung einer Sandbox für ein Produktprofil finden Sie in der Dokumentation unter [Verwalten von Berechtigungen für ein Produktprofil](../../access-control/ui/permissions.md).

Sie können eine neue Entwicklungs- oder Produktions-Sandbox erstellen, indem Sie eine POST-Anfrage an den `/sandboxes`-Endpunkt senden.

### Erstellen einer Entwicklungs-Sandbox

Um eine Entwicklungs-Sandbox zu erstellen, müssen Sie in der Payload der Anfrage ein `type` mit dem Wert `development` angeben.

**API-Format**

```http
POST /sandboxes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Entwicklungs-Sandbox mit dem Namen „acme-dev“.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die Kennung, die in zukünftigen Anfragen für den Zugriff auf die Sandbox verwendet wird. Dieser Wert muss eindeutig sein; Best Practice ist, ihn so beschreibend wie möglich zu gestalten. Dieser Wert darf keine Leerzeichen oder Sonderzeichen enthalten. |
| `title` | Ein für Menschen lesbarer Name, der zu Anzeigezwecken in der Benutzeroberfläche von Experience Platform verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Für eine Nicht-Produktions-Sandbox muss dieser Wert `development` werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Sandbox zurück und zeigt an, dass ihr `state` „wird erstellt“ lautet.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Es dauert etwa 30 Sekunden, bis Sandboxes vom System bereitgestellt werden. Danach werden ihre `state` „aktiv“ oder „fehlgeschlagen“.

### Erstellen einer Produktions-Sandbox

Um eine Produktions-Sandbox zu erstellen, müssen Sie in der Payload der Anfrage ein `type` mit dem Wert `production` angeben.

**API-Format**

```http
POST /sandboxes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Produktions-Sandbox mit dem Namen „acme“.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die Kennung, die in zukünftigen Anfragen für den Zugriff auf die Sandbox verwendet wird. Dieser Wert muss eindeutig sein; Best Practice ist, ihn so beschreibend wie möglich zu gestalten. Dieser Wert darf keine Leerzeichen oder Sonderzeichen enthalten. |
| `title` | Ein für Menschen lesbarer Name, der zu Anzeigezwecken in der Benutzeroberfläche von Experience Platform verwendet wird. |
| `type` | Der Typ der zu erstellenden Sandbox. Für eine Produktions-Sandbox muss dieser Wert `production` werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Sandbox zurück und zeigt an, dass ihr `state` „wird erstellt“ lautet.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Es dauert etwa 30 Sekunden, bis Sandboxes vom System bereitgestellt werden. Danach werden ihre `state` „aktiv“ oder „fehlgeschlagen“.

## Aktualisieren einer Sandbox {#put}

Sie können ein oder mehrere Felder in einer Sandbox aktualisieren, indem Sie eine PATCH-Anfrage stellen, die die `name` der Sandbox im Anfragepfad und die zu aktualisierende Eigenschaft in der Anfrage-Payload enthält.

>[!NOTE]
>
>Derzeit kann nur die `title` einer Sandbox aktualisiert werden.

**API-Format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name` der Sandbox, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die `title` der Sandbox mit dem Namen „acme“.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 (OK) mit den Details der neu aktualisierten Sandbox zurückgegeben.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Zurücksetzen einer Sandbox {#reset}

Sandboxes verfügen über eine Funktion zum Zurücksetzen auf die Werkseinstellungen, mit der alle nicht standardmäßigen Ressourcen aus einer Sandbox gelöscht werden. Sie können eine Sandbox zurücksetzen, indem Sie eine PUT-Anfrage stellen, die im Anfragepfad den Namen (`name`) der Sandbox enthält.

**API-Format**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie zurücksetzen möchten. |
| `validationOnly` | Ein optionaler Parameter, mit dem Sie den Sandbox-Zurücksetzungsvorgang vor dem Flug überprüfen können, ohne die eigentliche Anfrage zu stellen. Legen Sie diesen Parameter auf `validationOnly=true` fest, um zu überprüfen, ob die Sandbox, die Sie zurücksetzen möchten, Daten zu Adobe Analytics, Adobe Audience Manager oder zur Segmentfreigabe enthält. |

**Anfrage**

Die folgende Anfrage setzt eine Sandbox mit dem Namen „acme-dev“ zurück.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `action` | Dieser Parameter muss in der Anfrage-Payload mit dem Wert „reset“ angegeben werden, damit die Sandbox zurückgesetzt wird. |

**Antwort**

>[!NOTE]
>
>Nach dem Zurücksetzen einer Sandbox dauert es etwa 30 Sekunden, bis sie vom System bereitgestellt wird.

Eine erfolgreiche Antwort gibt die Details der aktualisierten Sandbox zurück und zeigt an, dass ihr Status (`state`) „wird zurückgesetzt“ lautet.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

Die standardmäßige Produktions-Sandbox und alle benutzererstellten Produktions-Sandboxes können nicht zurückgesetzt werden, wenn das darin gehostete Identitätsdiagramm auch von Adobe Analytics für die Funktion [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=de) verwendet wird oder wenn das darin gehostete Identitätsdiagramm auch von Adobe Audience Manager für die Funktion [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de) verwendet wird.

Im Folgenden finden Sie eine Liste möglicher Ausnahmen, die das Zurücksetzen einer Sandbox verhindern könnten:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Sie können eine Produktions-Sandbox, die für die bidirektionale Segmentfreigabe mit [!DNL Audience Manager] oder [!DNL Audience Core Service] verwendet wird, zurücksetzen, indem Sie den `ignoreWarnings`-Parameter zu Ihrer Anfrage hinzufügen.

**API-Format**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie zurücksetzen möchten. |
| `ignoreWarnings` | Ein optionaler Parameter, mit dem Sie die Validierungsprüfung überspringen und das Zurücksetzen einer Produktions-Sandbox erzwingen können, die für die bidirektionale Segmentfreigabe mit [!DNL Audience Manager] oder [!DNL Audience Core Service] verwendet wird. Dieser Parameter kann nicht auf eine standardmäßige Produktions-Sandbox angewendet werden. |

**Anfrage**

Die folgende Anfrage setzt eine Produktions-Sandbox mit dem Namen „acme“ zurück.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Sandbox zurück und zeigt an, dass ihr Status (`state`) „wird zurückgesetzt“ lautet.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Sandbox löschen {#delete}

>[!IMPORTANT]
>
>Die Standard-Produktions-Sandbox kann nicht gelöscht werden.

Sie können eine Sandbox löschen, indem Sie eine DELETE-Anfrage ausführen, die den `name` der Sandbox im Anfragepfad enthält.

>[!NOTE]
>
>Durch diesen API-Aufruf wird die `status`-Eigenschaft der Sandbox auf „gelöscht“ aktualisiert und deaktiviert. GET-Anfragen können die Details der Sandbox, nachdem sie gelöscht wurde, weiter abrufen.

**API-Format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Der `name` der Sandbox, die Sie löschen möchten. |
| `validationOnly` | Ein optionaler Parameter, mit dem Sie den Sandbox-Löschvorgang vor dem Flug überprüfen können, ohne die eigentliche Anfrage zu stellen. Legen Sie diesen Parameter auf `validationOnly=true` fest, um zu überprüfen, ob die Sandbox, die Sie zurücksetzen möchten, Daten zu Adobe Analytics, Adobe Audience Manager oder zur Segmentfreigabe enthält. |
| `ignoreWarnings` | Ein optionaler Parameter, mit dem Sie die Validierungsprüfung überspringen und das Löschen einer vom Benutzer erstellten Produktions-Sandbox erzwingen können, die für die bidirektionale Segmentfreigabe mit [!DNL Audience Manager] oder [!DNL Audience Core Service] verwendet wird. Dieser Parameter kann nicht auf eine standardmäßige Produktions-Sandbox angewendet werden. |

**Anfrage**

Die folgende Anfrage löscht eine Produktions-Sandbox mit dem Namen „acme“.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die aktualisierten Details der Sandbox zurückgegeben; sie zeigen, dass der `state` der Sandbox „gelöscht“ lautet.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
