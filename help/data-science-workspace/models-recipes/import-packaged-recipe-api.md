---
keywords: Experience Platform; verpacktes Rezept importieren; Data Science Workspace; beliebte Themen; Rezepte; API; Sensei Machine Learning; Engine erstellen
solution: Experience Platform
title: Importieren eines gepackten Rezepts mit der Sensei Machine Learning API
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial wird die Sensei Machine Learning API verwendet, um eine Engine zu erstellen, die in der Benutzeroberfläche auch als Rezept bezeichnet wird.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 31%

---

# Importieren eines gepackten Rezepts mit der Sensei Machine Learning API

In diesem Tutorial wird [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) verwendet, um eine [Engine](../api/engines.md) zu erstellen, die in der Benutzeroberfläche auch als Rezept bezeichnet wird.

Bevor Sie beginnen, sollten Sie beachten, dass Adobe Experience Platform [!DNL Data Science Workspace] unterschiedliche Begriffe verwendet, um auf ähnliche Elemente in der API und Benutzeroberfläche zu verweisen. Die API-Begriffe werden in diesem Tutorial verwendet. In der folgenden Tabelle sind die entsprechenden Begriffe aufgeführt:

| UI-Begriff | API-Begriff |
| ---- | ---- |
| Rezept | [Engine](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Ausbildung und Evaluierung | [Experiment](../api/experiments.md) |
| Dienst | [MLService](../api/mlservices.md) |

Eine Engine enthält Algorithmen und Logik für maschinelles Lernen, um bestimmte Probleme zu lösen. Das folgende Diagramm zeigt eine Visualisierung des API-Workflows in [!DNL Data Science Workspace]. Dieses Tutorial konzentriert sich auf die Erstellung einer Engine, des Gehirns eines Modells für maschinelles Lernen.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Erste Schritte

Für dieses Tutorial ist eine gepackte Rezeptdatei in Form einer Docker-URL erforderlich. Folgen Sie dem Tutorial [Quelldateien in einem Rezept](./package-source-files-recipe.md) verpacken , um eine verpackte Rezeptdatei zu erstellen oder eine eigene anzugeben.

- `{DOCKER_URL}`: Eine URL-Adresse für ein Docker-Bild eines intelligenten Dienstes.

Für dieses Tutorial müssen Sie das Tutorial [Authentifizierung bei Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abgeschlossen haben, damit Sie erfolgreich Aufrufe an [!DNL Platform]-APIs durchführen können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.
- `{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.

## Engine erstellen

Engines können erstellt werden, indem eine POST-Anfrage an den Endpunkt /engine gesendet wird. Die erstellte Engine wird basierend auf dem Formular der verpackten Rezeptdatei konfiguriert, die als Teil der API-Anfrage enthalten sein muss.

### Erstellen einer Engine mit einer Docker-URL {#create-an-engine-with-a-docker-url}

Um eine Engine mit einer gepackten Rezeptdatei zu erstellen, die in einem Docker-Container gespeichert ist, müssen Sie die Docker-URL für die gepackte Rezeptdatei angeben.

>[!CAUTION]
>
> Wenn Sie [!DNL Python] oder R verwenden, verwenden Sie die unten stehende Anfrage. Wenn Sie PySpark oder Scala verwenden, verwenden Sie das PySpark-/Scala-Anforderungsbeispiel, das sich unter dem Python/R-Beispiel befindet.

**API-Format**

```http
POST /engines
```

**Anfrage Python/R**

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
| `engine.name` | Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der [!DNL Data Science Workspace] -Benutzeroberfläche als Rezeptname angezeigt werden soll. |
| `engine.description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der [!DNL Data Science Workspace] -Benutzeroberfläche als Beschreibung des Rezepts angezeigt werden soll. Entfernen Sie diese Eigenschaft nicht. Lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keine Beschreibung angeben möchten. |
| `engine.type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird. Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, ist `type` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |
| `artifacts.default.image.location` | Ihr `{DOCKER_URL}` wird hier angezeigt. Eine vollständige Docker-URL weist die folgende Struktur auf: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Ein zusätzlicher Name für die Docker-Bilddatei. Entfernen Sie diese Eigenschaft nicht. Lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keinen zusätzlichen Docker-Bilddateinamen angeben möchten. |
| `artifacts.default.image.executionType` | Der Ausführungstyp dieser Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird. Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, ist `executionType` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |

**PySpark anfordern**

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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild auf &quot;PySpark&quot;basiert. |
| `mlLibrary` | Ein Feld, das beim Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild auf &quot;Spark&quot;basiert. |

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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild auf &quot;Spark&quot;basiert. |
| `mlLibrary` | Ein Feld, das beim Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild auf &quot;Spark&quot;basiert. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details der neu erstellten Engine einschließlich ihrer eindeutigen Kennung (`id`) enthält. Die folgende Beispielantwort bezieht sich auf eine [!DNL Python] -Engine. Die Schlüssel `executionType` und `type` ändern sich je nach bereitgestellter POST.

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

Eine erfolgreiche Antwort zeigt eine JSON-Payload mit Informationen zur neu erstellten Engine an. Der `id`-Schlüssel stellt die eindeutige Engine-Kennung dar und ist im nächsten Tutorial zum Erstellen einer MLInstance erforderlich. Stellen Sie sicher, dass die Engine-ID gespeichert wird, bevor Sie mit den nächsten Schritten fortfahren.

## Nächste Schritte {#next-steps}

Sie haben eine Engine mit der API erstellt und eine eindeutige Engine-Kennung wurde als Teil des Antworttextes abgerufen. Sie können diese Engine-Kennung im nächsten Tutorial verwenden, während Sie lernen, wie Sie [ein Modell mithilfe der API](./train-evaluate-model-api.md) erstellen, trainieren und bewerten.
