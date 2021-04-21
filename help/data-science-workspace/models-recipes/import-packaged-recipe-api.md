---
keywords: Experience Platform;importiertes verpacktes Rezept;Data Science Workspace;beliebte Themen;Rezepte;API;sensei maschinelles Lernen;Engine erstellen
solution: Experience Platform
title: Importieren eines gepackten Rezepts mit der Sensei Machine Learning API
topic-legacy: tutorial
type: Tutorial
description: Dieses Lernprogramm verwendet die Sensei Machine Learning API, um eine Engine zu erstellen, die auch als Rezept in der Benutzeroberfläche bezeichnet wird.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 31%

---

# Importieren eines gepackten Rezeptes mit der Sensei Machine Learning API

In diesem Lernprogramm wird mithilfe von [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) eine [Engine](../api/engines.md), auch als Rezept in der Benutzeroberfläche bezeichnet, erstellt.

Bevor Sie beginnen, sollten Sie bedenken, dass Adobe Experience Platform [!DNL Data Science Workspace] verschiedene Begriffe verwendet, um auf ähnliche Elemente innerhalb der API und Benutzeroberfläche zu verweisen. Die API-Begriffe werden in diesem Lernprogramm verwendet, und die folgende Tabelle zeigt die entsprechenden Begriffe an:

| UI-Begriff | API-Begriff |
| ---- | ---- |
| Rezept | [Engine](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Ausbildung und Evaluierung | [Experiment](../api/experiments.md) |
| Dienst | [MLService](../api/mlservices.md) |

Eine Engine enthält Algorithmen und Logik zum maschinellen Lernen, um bestimmte Probleme zu lösen. Das unten stehende Diagramm zeigt eine Visualisierung des API-Workflows in [!DNL Data Science Workspace]. Diese Übung konzentriert sich auf die Erstellung einer Engine, das Gehirn eines maschinellen Lernmodells.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Erste Schritte

Für dieses Lernprogramm ist eine gepackte Rezept-Datei in Form einer Docker-URL erforderlich. Folgen Sie dem Tutorial [Quelldateien in einem Rezept](./package-source-files-recipe.md), um eine verpackte Rezept-Datei zu erstellen oder eine eigene anzugeben.

- `{DOCKER_URL}`: Eine URL-Adresse für ein Docker-Bild eines intelligenten Dienstes.

Für dieses Lernprogramm müssen Sie das Tutorial [Authentifizierung bei Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um erfolgreich Aufrufe an [!DNL Platform]-APIs durchführen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.
- `{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.

## Erstellen einer Engine

Motoren können durch eine POST an den Endpunkt /engine erstellt werden. Die erstellte Engine wird auf der Grundlage der gepackten Rezept-Datei konfiguriert, die als Teil der API-Anforderung eingeschlossen werden muss.

### Erstellen einer Engine mit einer Docker-URL {#create-an-engine-with-a-docker-url}

Um eine Engine mit einer gepackten Rezept-Datei zu erstellen, die in einem Docker-Container gespeichert ist, müssen Sie die Docker-URL zur gepackten Rezeptdatei angeben.

>[!CAUTION]
>
> Wenn Sie [!DNL Python] oder R verwenden, verwenden Sie die unten stehende Anforderung. Wenn Sie PySpark oder Scala verwenden, verwenden Sie das PySpark/Scala Anforderungsbeispiel, das sich unterhalb des Python/R-Beispiels befindet.

**API-Format**

```http
POST /engines
```

**Python/R anfordern**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Eigenschaft | Beschreibung |
| -------  | ----------- |
| `engine.name` | Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der [!DNL Data Science Workspace]-Benutzeroberfläche als Rezeptname angezeigt wird. |
| `engine.description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der [!DNL Data Science Workspace]-Benutzeroberfläche als Beschreibung des Rezepts angezeigt wird. Entfernen Sie diese Eigenschaft nicht, lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keine Beschreibung angeben möchten. |
| `engine.type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird. Wenn zum Erstellen einer Engine eine Docker-URL angegeben wird, ist `type` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |
| `artifacts.default.image.location` | Ihr `{DOCKER_URL}` geht hier. Eine vollständige Docker-URL hat die folgende Struktur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Ein zusätzlicher Name für die Docker-Bilddatei. Entfernen Sie diese Eigenschaft nicht, lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keinen zusätzlichen Docker-Bilddateinamen angeben möchten. |
| `artifacts.default.image.executionType` | Der Ausführungstyp dieser Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird. Wenn zum Erstellen einer Engine eine Docker-URL angegeben wird, ist `executionType` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |

**Anfrage PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Dockerbild auf &quot;PySpark&quot;basiert. |
| `mlLibrary` | Ein Feld, das zum Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Dockerbild auf &quot;Spark&quot;basiert. |

**Anforderungsskala**

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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Dockerbild auf &quot;Spark&quot;basiert. |
| `mlLibrary` | Ein Feld, das zum Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Dockerbild auf &quot;Spark&quot;basiert. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details der neu erstellten Engine einschließlich ihrer eindeutigen Kennung (`id`) enthält. Die folgende Beispielantwort bezieht sich auf eine [!DNL Python]-Engine. Die Schlüssel `executionType` und `type` ändern sich je nach bereitgestellter POST.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Eine erfolgreiche Antwort zeigt eine JSON-Nutzlast mit Informationen zur neu erstellten Engine. Der `id`-Schlüssel stellt die eindeutige Engine-ID dar und ist im nächsten Lernprogramm erforderlich, um eine MLInstanz zu erstellen. Stellen Sie sicher, dass die Engine-ID gespeichert wird, bevor Sie mit den nächsten Schritten fortfahren.

## Nächste Schritte {#next-steps}

Sie haben eine Engine mit der API erstellt und eine eindeutige Engine-ID wurde als Teil des Antwortkörpers abgerufen. Sie können diese Engine-ID im nächsten Lernprogramm verwenden, während Sie lernen, wie [ein Modell mithilfe der API](./train-evaluate-model-api.md) erstellt, trainiert und ausgewertet wird.
