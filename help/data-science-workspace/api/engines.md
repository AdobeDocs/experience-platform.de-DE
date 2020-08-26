---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Engines
topic: Developer guide
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 70%

---


# Engines

Engines dienen als Grundlage für maschinelle Lernmodelle in Data Science Workspace. Sie enthalten Algorithmen für maschinelles Lernen, die bestimmte Probleme lösen, Pipelines zur Funktionsentwicklung aufweisen oder beides.

## Ihre Docker-Registrierung nachschlagen

>[!TIP]
>Wenn Sie keine Docker-URL haben, besuchen Sie die Quelldateien des [Pakets in einem Rezept](../models-recipes/package-source-files-recipe.md) -Lernprogramm, um eine schrittweise Anleitung zum Erstellen einer Docker-Host-URL zu erhalten.

Ihre Anmeldedaten für die Docker-Registrierung benötigen Sie, um eine verpackte Rezeptdatei hochladen zu können, einschließlich Ihrer Docker-Host-URL, des Benutzernamens und des Passworts. Sie können diese Daten nachschlagen, indem Sie die folgende GET-Anfrage ausführen:

**API-Format**

```https
GET /engines/dockerRegistry
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details Ihrer Docker-Registrierung einschließlich der Docker-URL (`host`), des Benutzernamens (`username`) und des Passworts (`password`) enthält.

>[!NOTE]
>
>Ihr Docker-Passwort ändert sich jedes Mal, wenn Ihr `{ACCESS_TOKEN}` aktualisiert wird.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Engine mithilfe von Docker-URLs erstellen {#docker-image}

Sie können eine Engine erstellen, indem Sie eine POST-Anfrage ausführen und gleichzeitig die zugehörigen Metadaten und eine Docker-URL angeben, die in mehrteiligen Forms auf ein Docker-Image verweist.

**API-Format**

```https
POST /engines
```

**Python/R anfordern**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Rezeptname. |
| `description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Beschreibung des Rezepts. Diese Eigenschaft ist erforderlich. Wenn Sie keine Beschreibung angeben möchten, legen Sie als Wert eine leere Zeichenfolge fest. |
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Image beruht, und kann entweder „Python“, „R“ oder „TensorFlow“ lauten. |
| `algorithm` | Eine Zeichenfolge, die den Typ des maschinellen Lernalgorithmus angibt. Zu den unterstützten Algorithmustypen gehören „Klassifizierung“, „Regression“ oder „Benutzerdefiniert“. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Image beruht, und kann entweder „Python“, „R“ oder „TensorFlow“ lauten. |

**Anfrage PySpark/Scala**

Wenn Sie eine Anfrage für PySpark Rezepte, ist der `executionType` und `type` ist &quot;PySpark&quot;. Wenn Sie eine Anforderung für Scala-Rezepte stellen, lautet das `executionType` und `type` &quot;Spark&quot;. Im folgenden Scala-Rezept-Beispiel wird Spark verwendet:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Rezeptname. |
| `description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Beschreibung des Rezepts. Diese Eigenschaft ist erforderlich. Wenn Sie keine Beschreibung angeben möchten, legen Sie als Wert eine leere Zeichenfolge fest. |
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Bild aufgebaut ist. Der Wert kann auf Spark oder PySpark eingestellt werden. |
| `mlLibrary` | Ein Feld, das zum Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. Dieses Feld muss auf `databricks-spark`. |
| `artifacts.default.image.location` | Die Position des Dockerbilds. Nur der ACR oder der öffentliche (nicht authentifizierte) Dockerhub wird unterstützt. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Bild aufgebaut ist. Dies kann entweder &quot;Spark&quot;oder &quot;PySpark&quot;sein. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details der neu erstellten Engine einschließlich ihrer eindeutigen Kennung (`id`) enthält. Die folgende Beispielantwort bezieht sich auf eine Python-Engine. Alle Engine-Antworten haben das folgende Format:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Erstellen einer Feature Pipeline-Engine mit Docker-URLs {#feature-pipeline-docker}

Sie können eine Feature Pipeline-Engine erstellen, indem Sie eine Anforderung zur POST ausführen und gleichzeitig die Metadaten und eine Docker-URL bereitstellen, die auf ein Dockerbild verweist.

**API-Format**

```https
POST /engines
```

**Anfrage**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Bild aufgebaut ist. Der Wert kann auf Spark oder PySpark eingestellt werden. |
| `algorithm` | Der verwendete Algorithmus setzt diesen Wert auf `fp` (Feature-Pipeline). |
| `name` | Der gewünschte Name für die Feature Pipeline-Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Rezeptname. |
| `description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt den Wert, der in der Benutzeroberfläche angezeigt werden soll, als Beschreibung des Rezepts. Diese Eigenschaft ist erforderlich. Wenn Sie keine Beschreibung angeben möchten, legen Sie als Wert eine leere Zeichenfolge fest. |
| `mlLibrary` | Ein Feld, das zum Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. Dieses Feld muss auf `databricks-spark`. |
| `artifacts.default.image.location` | Die Position des Dockerbilds. Nur der ACR oder der öffentliche (nicht authentifizierte) Dockerhub wird unterstützt. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, auf der das Docker-Bild aufgebaut ist. Dies kann entweder &quot;Spark&quot;oder &quot;PySpark&quot;sein. |
| `artifacts.default.image.packagingType` | Der Verpackungstyp des Motors. Dieser Wert sollte auf `docker`gesetzt werden. |
| `artifacts.default.defaultMLInstanceConfigs` | Ihre `pipeline.json` Konfigurationsdateiparameter. |

**Antwort**

A successful response returns a payload containing the details of the newly created feature pipeline Engine including its unique identifier (`id`). Die folgende Beispielantwort bezieht sich auf eine PySpark Feature Pipeline Engine.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Liste von Engines abrufen

Sie können eine Liste von Engines abrufen, indem Sie eine GET-Anfrage ausführen. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der Engines und ihre Details zurück.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Bestimmte Engine abrufen {#retrieve-specific}

Sie können die Details einer bestimmten Engine abrufen, indem Sie eine GET-Anfrage ausführen, die im Anfragepfad die Kennung der gewünschten Engine enthält.

**API-Format**

```https
GET /engines/{ENGINE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENGINE_ID}` | Die Kennung einer vorhandenen Engine. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload mit den Details der gewünschten Engine zurück.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Engine aktualisieren

Sie können eine vorhandene Engine ändern und aktualisieren, indem Sie ihre Eigenschaften durch eine PUT-Anfrage überschreiben, die die Kennung der Ziel-Engine im Anfragepfad enthält, und eine JSON-Payload mit aktualisierten Eigenschaften angeben.

>[!NOTE]
>
> Um den Erfolg dieser PUT-Anfrage zu gewährleisten, wird empfohlen, zuerst eine GET-Anfrage zum [Abrufen der Engine nach Kennung](#retrieve-specific) auszuführen. Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

Der folgende Beispiel-API-Aufruf aktualisiert den Namen und die Beschreibung einer Engine und weist zunächst folgende Eigenschaften auf:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API-Format**

```https
PUT /engines/{ENGINE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENGINE_ID}` | Die Kennung einer vorhandenen Engine. |

**Anfrage**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload mit den aktualisierten Details der Engine zurück.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Engine löschen

Sie können eine Engine löschen, indem Sie eine DELETE-Anfrage ausführen und dabei die Kennung der Ziel-Engine im Anfragepfad angeben. Durch das Löschen einer Engine werden alle MLInstances, die auf diese Engine verweisen, kaskadiert (inklusive aller Experimente und Experimentläufe, die zu diesen MLInstances gehören).

**API-Format**

```https
DELETE /engines/{ENGINE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENGINE_ID}` | Die Kennung einer vorhandenen Engine. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
