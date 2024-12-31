---
keywords: Experience Platform;Gepacktes Rezept importieren;Data Science Workspace;beliebte Themen;Rezepte;API;Sensei Machine Learning;Engine erstellen
solution: Experience Platform
title: Importieren eines gepackten Rezepts mithilfe der Sensei-API für maschinelles Lernen
type: Tutorial
description: In diesem Tutorial wird die Sensei-API für maschinelles Lernen verwendet, um in der Benutzeroberfläche eine Engine zu erstellen, die auch als Rezept bezeichnet wird.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 26%

---

# Importieren eines gepackten Rezepts mithilfe der Sensei-API für maschinelles Lernen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial wird die [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) zum Erstellen einer [Engine](../api/engines.md) verwendet, die in der Benutzeroberfläche auch als Rezept bezeichnet wird.

Bevor Sie beginnen, sollten Sie beachten, dass Adobe Experience Platform [!DNL Data Science Workspace] verschiedene Begriffe verwendet, um auf ähnliche Elemente in der API und Benutzeroberfläche zu verweisen. Die API-Begriffe werden im Verlauf dieses Tutorials verwendet und in der folgenden Tabelle sind die entsprechenden Begriffe aufgeführt:

| UI-Begriff | API-Begriff |
| ---- | ---- |
| Rezept | [Engine](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Schulung und Evaluierung | [Experiment](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Eine Engine enthält Algorithmen und Logik für maschinelles Lernen, um spezifische Probleme zu lösen. Das folgende Diagramm zeigt eine Visualisierung des API-Workflows in [!DNL Data Science Workspace]. Dieses Tutorial konzentriert sich auf die Erstellung einer Engine, das Gehirn eines Modells für maschinelles Lernen.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Erste Schritte

Für dieses Tutorial ist eine gepackte Recipe File in Form einer Docker-URL erforderlich. Befolgen Sie das Tutorial [Quelldateien in ein Rezept packen](./package-source-files-recipe.md) zum Erstellen einer gepackten Rezeptdatei oder zum Bereitstellen einer eigenen.

- `{DOCKER_URL}`: Eine URL-Adresse zu einem Docker-Image eines Intelligent Service.

Für dieses Tutorial müssen Sie das Tutorial [Authentifizierung bei Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform] APIs erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.
- `{ORG_ID}`: Ihre Unternehmensanmeldeinformationen wurden in Ihrer eindeutigen Adobe Experience Platform-Integration gefunden.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.

## Engine erstellen

Engines können erstellt werden, indem eine POST-Anfrage an den /engines-Endpunkt gesendet wird. Die erstellte Engine wird basierend auf dem Formular der gepackten Recipe File konfiguriert, die als Teil der API-Anfrage enthalten sein muss.

### Erstellen einer Engine mit einer Docker-URL {#create-an-engine-with-a-docker-url}

Um ein Modul mit einer gepackten Recipe File zu erstellen, die in einem Docker-Container gespeichert ist, müssen Sie die Docker-URL für die gepackte Recipe File angeben.

>[!CAUTION]
>
> Wenn Sie [!DNL Python] oder R verwenden, verwenden Sie die nachstehende Anfrage. Wenn Sie PySpark oder Scala verwenden, verwenden Sie das PySpark-/Scala-Anfragebeispiel unter dem Python/R-Beispiel.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in [!DNL Data Science Workspace] Benutzeroberfläche als Name des Rezepts angezeigt wird. |
| `engine.description` | Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in [!DNL Data Science Workspace] Benutzeroberfläche als Beschreibung des Rezepts angezeigt wird. Entfernen Sie diese Eigenschaft nicht. Wenn Sie keine Beschreibung angeben möchten, darf dieser Wert eine leere Zeichenfolge sein. |
| `engine.type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image entwickelt wird. Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, `type` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |
| `artifacts.default.image.location` | Ihr `{DOCKER_URL}` geht hierher. Eine vollständige Docker-URL weist die folgende Struktur auf: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Ein zusätzlicher Name für die Docker-Grafikdatei. Entfernen Sie diese Eigenschaft nicht. Wenn Sie keinen zusätzlichen Docker-Bilddateinamen angeben möchten, darf dieser Wert eine leere Zeichenfolge sein. |
| `artifacts.default.image.executionType` | Der Ausführungstyp dieser Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image entwickelt wird. Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, `executionType` entweder `Python`, `R`, `PySpark`, `Spark` (Scala) oder `Tensorflow`. |

**PySpark anfordern**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image auf „PySpark“ erstellt wird. |
| `mlLibrary` | Ein Feld, das beim Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image auf „Spark“ erstellt wird. |

**Scala anfordern**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image auf „Spark“ erstellt wird. |
| `mlLibrary` | Ein Feld, das beim Erstellen von Engines für PySpark- und Scala-Rezepte erforderlich ist. |
| `artifacts.default.image.location` | Der Speicherort des Docker-Images, mit dem eine Docker-URL verknüpft ist. |
| `artifacts.default.image.executionType` | Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Image auf „Spark“ erstellt wird. |

**Antwort**

Bei einer erfolgreichen Antwort wird eine Payload zurückgegeben, die die Details der neu erstellten Engine einschließlich ihrer eindeutigen Kennung (`id`) enthält. Die folgende Beispielantwort gilt für eine [!DNL Python]. Die `executionType`- und `type` ändern sich je nach der angegebenen POST.

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

Eine erfolgreiche Antwort zeigt eine JSON-Payload mit Informationen zur neu erstellten Engine. Der `id` stellt die eindeutige Engine-Kennung dar und ist im nächsten Tutorial zum Erstellen einer MLInstance erforderlich. Stellen Sie sicher, dass die Engine-Kennung gespeichert ist, bevor Sie mit den nächsten Schritten fortfahren.

## Nächste Schritte {#next-steps}

Sie haben eine Engine mithilfe der API erstellt und eine eindeutige Engine-Kennung wurde als Teil der Antwort abgerufen. Sie können diese Engine-Kennung im nächsten Tutorial verwenden, in dem Sie lernen[ wie Sie ein Modell mithilfe der API erstellen, trainieren und bewerten](./train-evaluate-model-api.md).
