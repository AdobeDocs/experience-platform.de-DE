---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacktes Rezept (API) importieren
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# Verpacktes Rezept (API) importieren

Dieses Lernprogramm verwendet die [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) , um eine [Engine](../api/engines.md)zu erstellen, die in der Benutzeroberfläche auch als Rezept bezeichnet wird.

Bevor Sie beginnen, sollten Sie bedenken, dass Adobe Experience Platform Data Science Workspace verschiedene Begriffe verwendet, um auf ähnliche Elemente innerhalb der API und Benutzeroberfläche zu verweisen. Die API-Begriffe werden in diesem Lernprogramm verwendet, und die folgende Tabelle zeigt die entsprechenden Begriffe an:

| Begriff der Benutzeroberfläche | API-Begriff |
| ---- | ---- |
| Rezept | [Engine](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Ausbildung und Evaluierung | [Experiment](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Eine Engine enthält Algorithmen und Logik zum maschinellen Lernen, um bestimmte Probleme zu lösen. Das unten stehende Diagramm bietet eine Visualisierung des API-Workflows im Data Science Workspace. Diese Übung konzentriert sich auf die Erstellung einer Engine, das Gehirn eines maschinellen Lernmodells.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Erste Schritte

Dieses Lernprogramm erfordert eine gepackte Rezeptdatei in Form eines binären Artefakts oder einer Docker-URL. Folgen Sie den Quelldateien [des Pakets in einem Rezept](./package-source-files-recipe.md) -Lernprogramm, um eine verpackte Rezept-Datei zu erstellen oder eine eigene anzugeben.

- Artefakt binär: Das binäre Artefakt (z. JAR, EGG), mit dem eine Engine erstellt wird.
- `{DOCKER_URL}` : Eine URL-Adresse für ein Docker-Bild eines intelligenten Dienstes.

Für dieses Lernprogramm müssen Sie das Lernprogramm &quot; [Authentifizierung für Adobe Experience Platform&quot;abgeschlossen haben, damit Sie erfolgreich Aufrufe an Plattform-APIs durchführen können](../../tutorials/authentication.md) . Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- `{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.

## Erstellen einer Engine

Je nachdem, in welcher Form die verpackte Recipe-Datei als Teil der API-Anforderung enthalten sein soll, wird eine Engine auf zwei Arten erstellt:
- [Erstellen einer Engine mit einem binären Artefakt](#create-an-engine-with-a-binary-artifact)
- [Erstellen einer Engine mit einer Docker-URL](#create-an-engine-with-a-docker-url)

### Erstellen einer Engine mit einem binären Artefakt

Um eine Engine mit einem lokalen gepackten `.jar` oder `.egg` binären Artefakt zu erstellen, müssen Sie den absoluten Pfad zur binären Artefaktdatei in Ihrem lokalen Dateisystem angeben. Erwägen Sie, zu dem Ordner zu navigieren, der das binäre Artefakt in einer Terminal-Umgebung enthält, und den `pwd` Unix-Befehl für den absoluten Pfad auszuführen.

Der folgende Aufruf erstellt eine Engine mit einem binären Artefakt:

#### API-Format

```http
POST /engines
```

#### Anfrage

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` : Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der Data Science Workspace-Benutzeroberfläche als Rezeptname angezeigt wird.
- `engine > description` : Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der Benutzeroberfläche von Data Science Workspace als Beschreibung des Rezepts angezeigt wird. Entfernen Sie diese Eigenschaft nicht, lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keine Beschreibung angeben möchten.
- `engine > type`: Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das binäre Artefakt entwickelt wurde.

   >[!NOTE] Wenn Sie ein binäres Artefakt hochladen, um eine Engine zu erstellen, `type` ist entweder `Spark` oder `PySpark`.

- `defaultArtifact` : Der absolute Pfad zur binären Artefaktdatei, die zum Erstellen der Engine verwendet wird.

   >[!NOTE] Vergewissern Sie sich, dass sie `@` vor dem Dateipfad enthalten sind.

#### Antwort

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

Eine erfolgreiche Antwort zeigt eine JSON-Nutzlast mit Informationen zur neu erstellten Engine. Der `id` Schlüssel stellt die eindeutige Engine-ID dar und ist im nächsten Lernprogramm erforderlich, um eine MLInstanz zu erstellen. Stellen Sie sicher, dass die Engine-ID gespeichert wird, bevor Sie mit den [nächsten Schritten](#next-steps)fortfahren.

### Erstellen einer Engine mit einer Docker-URL

Um eine Engine mit einer gepackten Rezept-Datei zu erstellen, die in einem Docker-Container gespeichert ist, müssen Sie die Docker-URL zur gepackten Rezeptdatei angeben.

Mit dem folgenden Aufruf wird eine Engine mit einer Docker-URL erstellt:

#### API-Format

```http
POST /engines
```

#### Anfrage

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

- `engine > name` : Der gewünschte Name für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der Data Science Workspace-Benutzeroberfläche als Rezeptname angezeigt wird.
- `engine > description` : Eine optionale Beschreibung für die Engine. Das Rezept, das dieser Engine entspricht, übernimmt diesen Wert, der in der Benutzeroberfläche von Data Science Workspace als Beschreibung des Rezepts angezeigt wird. Entfernen Sie diese Eigenschaft nicht, lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keine Beschreibung angeben möchten.
- `engine > type`: Der Ausführungstyp der Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird.

   >[!NOTE] Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, `type` ist entweder `Python`, `R`oder `Tensorflow`.

- `artifacts > default > image > location` : Du `{DOCKER_URL}` gehst hierher. Eine vollständige Docker-URL hat die folgende Struktur:

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` : Ein zusätzlicher Name für die Docker-Bilddatei. Entfernen Sie diese Eigenschaft nicht, lassen Sie diesen Wert eine leere Zeichenfolge sein, wenn Sie keinen zusätzlichen Docker-Bilddateinamen angeben möchten.
- `artifacts > default > image > executionType` : Der Ausführungstyp dieser Engine. Dieser Wert entspricht der Sprache, in der das Docker-Bild entwickelt wird.

   >[!NOTE] Wenn eine Docker-URL zum Erstellen einer Engine bereitgestellt wird, `executionType` ist entweder `Python`, `R`oder `Tensorflow`.

#### Antwort

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Eine erfolgreiche Antwort zeigt eine JSON-Nutzlast mit Informationen zur neu erstellten Engine. Der `id` Schlüssel stellt die eindeutige Engine-ID dar und ist im nächsten Lernprogramm erforderlich, um eine MLInstanz zu erstellen. Stellen Sie sicher, dass die Engine-ID gespeichert wird, bevor Sie mit den nächsten Schritten fortfahren.

## Nächste Schritte

Sie haben eine Engine mit der API erstellt und eine eindeutige Engine-ID wurde als Teil des Antwortkörpers abgerufen. Sie können diese Engine-ID im nächsten Lernprogramm verwenden, während Sie erfahren, wie Sie ein Modell mithilfe der API [erstellen, ausbilden und auswerten](./train-evaluate-model-api.md).