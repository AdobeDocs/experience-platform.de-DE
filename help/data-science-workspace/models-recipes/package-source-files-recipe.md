---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacken von Quelldateien in einem Rezept
topic: Tutorial
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---


# Verpacken von Quelldateien in einem Rezept

In diesem Lernprogramm wird beschrieben, wie Sie die angegebenen Quelldateien für den Einzelhandel in einer Archivdatei verpacken können, die Sie zum Erstellen eines Rezepts in Adobe Experience Platform verwenden können, [!DNL Data Science Workspace] indem Sie dem Skript-Import-Arbeitsablauf entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Concepts to understand:

- **Rezepte**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen Algorithmus für künstliche Intelligenz oder ein Ensemble von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Aufbau und zur Ausführung eines geschulten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Source files**: Individual files in your project that contain the logic for a recipe.

## Voraussetzungen 

- [!DNL Docker](https://docs.docker.com/install/#supported-platforms)
- [!DNL Python 3 and pip](https://docs.conda.io/en/latest/miniconda.html)
- [!DNL Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [!DNL Maven](https://maven.apache.org/install.html)

## Rezepterstellung

Recipe creation starts with packaging source files to build an archive file. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala geschrieben. Die erstellten Archivdateien haben die Form eines Dockerbilds. Nach der Erstellung wird die verpackte Archivdatei in importiert, [!DNL Data Science Workspace] um ein Rezept [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [mithilfe der API](./import-packaged-recipe-api.md)zu erstellen.

### Docker based model authoring {#docker-based-model-authoring}

A Docker image allows a developer to package up an application with all the parts it needs, such as libraries and other dependencies, and ship it out as one package.

The built Docker image is pushed to the Azure Container Registry using credentials supplied to you during the recipe creation workflow.

To obtain your Azure Container Registry credentials, log into [Adobe Experience Platform](https://platform.adobe.com). Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Select **[!UICONTROL Import Recipe]** followed by selecting **[!UICONTROL Launch]**. See the screen shot below for reference.

![](../images/models-recipes/package-source-files/import.png)

The *Configure* page opens. Geben Sie einen entsprechenden *Rezeptnamen* ein, z. B. &quot;Retail Sales recipe&quot;, und geben Sie optional eine Beschreibung oder eine Dokumentations-URL ein. Once complete, click **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Select the appropriate *Runtime*, then choose a **[!UICONTROL Classification]** for *Type*. Ihre Anmeldedaten für die Azurblase-Container-Registrierung werden nach Abschluss der Überprüfung generiert.

>[!NOTE]
>*Typ *ist die Klasse des maschinellen Lernproblems, für das das Rezept entwickelt wurde und nach dem Training verwendet wird, um die Beurteilung der Trainingslaufzeit anzupassen.

>[!TIP]
>- Wählen Sie für [!DNL Python] Rezepte die **[!UICONTROL Python]** -Laufzeit.
>- Wählen Sie für R-Rezepte die **[!UICONTROL R]** -Laufzeit.
>- Wählen Sie für PySpark-Rezepte die **[!UICONTROL PySpark]** -Laufzeit. Ein Artefakttyp wird automatisch gefüllt.
>- Wählen Sie für Scala-Rezepte die **[!UICONTROL Spark]** -Laufzeit. Ein Artefakttyp wird automatisch gefüllt.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für *Docker-Host*, *Benutzername* und *Kennwort*. These are used to build and push your [!DNL Docker] image in the workflows outlined below.

>[!NOTE]
>The Source URL is provided after completing the steps outlined below. The configuration file is explained in subsequent tutorials found in [next steps](#next-steps).

### Verpacken der Quelldateien

Beginn durch Abrufen der Codebasis für Beispieldateien im <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Data Science Workspace-Referenzrepository</a> der Experience Platform.

- [Python-Docker-Bild erstellen](#python-docker)
- [R-Docker-Bild erstellen](#r-docker)
- [PySpark Docker-Bild erstellen](#pyspark-docker)
- [Punktdiagrammbild erstellen (Spark)](#scala-docker)

### Bild [!DNL Python] für Docker erstellen {#python-docker}

Wenn Sie dies noch nicht getan haben, klonen Sie das [!DNL GitHub] Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Skripte `login.sh` und `build.sh` zur Anmeldung bei Docker und zur Erstellung des [!DNL Python Docker] Bildes. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

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

### R- [!DNL Docker] Bild erstellen {#r-docker}

Wenn Sie dies noch nicht getan haben, klonen Sie das [!DNL GitHub] Repository mit dem folgenden Befehl auf Ihrem lokalen System:

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

### Build PySpark Docker image {#pyspark-docker}

Beginn durch Klonen des [!DNL GitHub] Repositorys auf Ihrem lokalen System mit folgendem Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripten `login.sh` und `build.sh` sind hier zu finden und zum Anmelden bei Docker und zum Erstellen des Docker-Bildes. If you have your [Docker credentials](#docker-based-model-authoring) ready, enter the following commands in order:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. When building, you are required to provide the Docker host and a version tag for the build.

Once the build script is complete, you are given a Docker source file URL in your console output. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zu den [nächsten Schritten](#next-steps).

### Build Scala Docker image {#scala-docker}

Start by cloning the [!DNL GitHub] repository onto your local system with the following command in terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Next, navigate to the directory `experience-platform-dsw-reference/recipes/scala` where you can find the scripts `login.sh` and `build.sh`. Diese Skripten werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. If you have your [Docker credentials](#docker-based-model-authoring) ready, enter the following commands to terminal in order:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>If you are receiving a permission error when trying to login to Docker using the `login.sh` script, try using the command `bash login.sh`.

When executing the login script, you need to provide the Docker host, username, and password. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Once the build script is complete, you are given a Docker source file URL in your console output. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copy this URL and move on to the [next steps](#next-steps).

## Nächste Schritte {#next-steps}

Diese Übung übernahm das Verpacken von Quelldateien in ein Rezept, den notwendigen Schritt zum Importieren eines Rezepts in [!DNL Data Science Workspace]. Sie sollten jetzt ein Docker-Bild in der Azurblauen Container-Registrierung zusammen mit der entsprechenden Bild-URL haben. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in beginnen [!DNL Data Science Workspace]. Wählen Sie einen der folgenden Links zum Einstieg:

- [Verpacktes Rezept in die Benutzeroberfläche importieren](./import-packaged-recipe-ui.md)
- [Verpacktes Rezept mit der API importieren](./import-packaged-recipe-api.md)