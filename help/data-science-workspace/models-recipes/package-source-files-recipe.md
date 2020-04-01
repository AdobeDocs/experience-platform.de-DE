---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacken von Quelldateien in einem Rezept
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Verpacken von Quelldateien in einem Rezept

Dieses Lernprogramm enthält Anweisungen dazu, wie Sie die angegebenen Quelldateien für den Einzelhandel in eine Archivdatei packen können, die zum Erstellen eines Rezepts in Adobe Experience Platform Data Science Workspace verwendet werden kann, indem Sie dem Skript-Import-Arbeitsablauf entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Konzepte zum Verständnis:

- **Rezepte**: Ein Rezept ist der von Adobe verwendete Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen Algorithmus für künstliche Intelligenz oder ein Ensemble von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die zum Aufbau und Ausführen eines geschulten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Quelldateien**: Einzelne Dateien im Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [Docker](https://docs.docker.com/install/#supported-platforms)
- [Python 3 und pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Maven](https://maven.apache.org/install.html)

## Rezepterstellung

Beginn zur Rezepterstellung mit Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in Python, R, PySpark oder Scala Spark geschrieben. Je nachdem, in welcher Sprache die Quelldateien geschrieben werden, sind die erstellten Archivdateien entweder ein Dockerbild oder eine Binärdatei. Nach der Erstellung wird die verpackte Archivdatei in Data Science Workspace importiert, um ein Rezept [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [mithilfe der API](./import-packaged-recipe-api.md)zu erstellen.

### Dockerbasiertes Modell-Authoring

Ein Docker-Bild ermöglicht es einem Entwickler, eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten zu verpacken und als ein Paket zu versenden.

Das erstellte Docker-Bild wird mit den Anmeldeinformationen, die Sie während des Rezepterstellungs-Workflows erhalten haben, in die Azurblase-Container-Registrierung gesendet.

>[!NOTE] Nur Quelldateien, die in **Python**, **R** und **Tensorflow** geschrieben wurden, erfordern die Anmeldeinformationen der Azurblase Container Registry.

Melden Sie sich zum Erhalt der Anmeldedaten für Ihre Azurblase Container-Registrierung bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>an. Navigieren Sie in der linken Navigationsspalte zu **Workflows**. Wählen Sie **Rezept aus Quelldatei** importieren und **starten** Sie eine neue Importaktion. Siehe Screenshot unten als Referenz.

![](../images/models-recipes/package-source-files/workflow_ss.png)

Geben Sie einen entsprechenden **Rezeptnamen** ein, z. B. &quot;Retail Sales recipe&quot;, und geben Sie optional eine Beschreibung oder eine Dokumentations-URL ein. Klicken Sie nach Abschluss des Vorgangs auf **Weiter**.

![](../images/models-recipes/package-source-files/recipe_info.png)

Wählen Sie die entsprechende **Laufzeitumgebung** und dann **Klassifizierung** für **Typ**. Ihre Anmeldedaten für die Blaue Container-Registrierung werden generiert.

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

Notieren Sie die Werte für **Docker-Host**, **Benutzername** und **Kennwort**. Diese werden später zum Erstellen und Push Ihres Docker-Bildes verwendet.

Nach dem Push können Sie und andere Benutzer über URL auf das Bild zugreifen. Das Feld **Quelldatei** erwartet diese URL als Eingabe.

### Binärbasiertes Modell-Authoring

Für Quelldateien, die in Scala oder PySpark geschrieben wurden, wird eine Binärdatei generiert. Das Erstellen der Binärdatei ist so einfach wie das Ausführen des bereitgestellten Buildskripts.
>[!NOTE] Nur Quelldateien, die in ScalaSpark oder PySpark geschrieben wurden, erzeugen beim Ausführen des Buildskripts eine Binärdatei.

### Verpacken der Quelldateien

Beginn durch Abrufen der Codebasis für Beispieldateien im <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a> -Repository. Je nachdem, in welcher Programmiersprache die Beispielquelldateien geschrieben werden, unterscheidet sich das Erstellen der jeweiligen Archivdatei im Verfahren.

- [Python-Docker-Bild erstellen](#build-python-docker-image)
- [R-Docker-Bild erstellen](#build-r-docker-image)
- [PySpark-Binärdateien erstellen](#build-pyspark-binaries)
- [Scala-Binärdateien erstellen](#build-scala-binaries)

#### Python-Docker-Bild erstellen

Falls nicht, klonen Sie das github-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Skripte `login.sh` und `build.sh` die Sie verwenden werden, um sich bei Docker anzumelden und das Python Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Nachdem das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in der Konsolenausgabe. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zu den [nächsten Schritten](#next-steps).

#### R-Docker-Bild erstellen

Falls nicht, klonen Sie das github-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Ordner `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` im geklonten Repository. Hier finden Sie die Dateien `login.sh` und `build.sh` die Sie verwenden werden, um sich bei Docker anzumelden und das R Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Nachdem das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in der Konsolenausgabe. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zu den [nächsten Schritten](#next-steps).

#### PySpark-Binärdateien erstellen

Falls nicht, klonen Sie das github-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum geklonten Repository auf Ihrem lokalen System und führen Sie die folgenden Befehle aus, um die erforderliche `.egg` Datei zum Importieren eines PySpark-Rezeptes zu erstellen:

```BASH
cd recipes/pyspark
./build.sh
```

Die `.egg` Datei wird im `dist` Ordner generiert.

Sie können jetzt zu den [nächsten Schritten](#next-steps)fortfahren.

#### Scala-Binärdateien erstellen

Wenn Sie dies noch nicht getan haben, führen Sie den folgenden Befehl aus, um das Github-Repository auf Ihrem lokalen System zu klonen:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Um das `.jar` Artefakt zum Importieren eines Scala-Rezepts zu erstellen, navigieren Sie zu Ihrem geklonten Repository und führen Sie die folgenden Schritte aus:

```BASH
cd recipes/scala/
./build.sh
```

Das generierte `.jar` Artefakt mit Abhängigkeiten befindet sich im `/target` Verzeichnis.

Sie können jetzt zu den [nächsten Schritten](#next-steps)fortfahren.

## Nächste Schritte

Diese Übung übernahm das Verpacken von Quelldateien in ein Rezept, die Voraussetzung für den Import eines Rezepts in Data Science Workspace. Sie sollten jetzt ein Docker-Bild in der Azurblauen Container-Registrierung zusammen mit der entsprechenden Bild-URL oder eine Binärdatei, die lokal in Ihrem Dateisystem gespeichert ist, haben. Sie können jetzt mit dem Lernprogramm zum **Importieren eines zusammengestellten Rezepts in den Data Science Workspace** beginnen. Wählen Sie einen der folgenden Links, um zu beginnen.

- [Verpacktes Rezept in die Benutzeroberfläche importieren](./import-packaged-recipe-ui.md)
- [Verpacktes Rezept mit der API importieren](./import-packaged-recipe-api.md)