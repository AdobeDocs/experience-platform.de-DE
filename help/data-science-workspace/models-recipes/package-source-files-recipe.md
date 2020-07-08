---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Verpacken von Quelldateien in einem Rezept
topic: Tutorial
translation-type: tm+mt
source-git-commit: 45461e3420f3b7e227f80fe775d80b8442a1069c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---


# Verpacken von Quelldateien in einem Rezept

In diesem Lernprogramm wird beschrieben, wie Sie die angegebenen Quelldateien für den Einzelhandel in einer Archivdatei verpacken können, die Sie verwenden können, um ein Rezept in der Adobe Experience Platform zu erstellen, [!DNL Data Science Workspace] indem Sie dem Skript-Import-Arbeitsablauf entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Konzepte zum Verständnis:

- **Rezepte**: Ein Rezept ist der von Adobe verwendete Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen Algorithmus für künstliche Intelligenz oder ein Ensemble von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die zum Aufbau und Ausführen eines geschulten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Quelldateien**: Einzelne Dateien im Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [!DNL Docker](https://docs.docker.com/install/#supported-platforms)
- [!DNL Python 3 and pip](https://docs.conda.io/en/latest/miniconda.html)
- [!DNL Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [!DNL Maven](https://maven.apache.org/install.html)

## Rezepterstellung

Beginn zur Rezepterstellung mit Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala geschrieben. Die erstellten Archivdateien haben die Form eines Dockerbilds. Nach der Erstellung wird die verpackte Archivdatei in importiert, [!DNL Data Science Workspace] um ein Rezept [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [mithilfe der API](./import-packaged-recipe-api.md)zu erstellen.

### Dockerbasiertes Modell-Authoring {#docker-based-model-authoring}

Ein Docker-Bild ermöglicht es einem Entwickler, eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten zu verpacken und als ein Paket zu versenden.

Das erstellte Docker-Bild wird mit den Anmeldeinformationen, die Sie während des Rezepterstellungsarbeitsablaufs erhalten haben, in die Azurblaue Container-Registrierung verschoben.

Melden Sie sich bei der <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>an, um Ihre Azurblase Container Registry-Anmeldeinformationen zu erhalten. Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Wählen Sie **[!UICONTROL Rezept]** importieren und anschließend **[!UICONTROL Starten]**. Siehe Screenshot unten als Referenz.

![](../images/models-recipes/package-source-files/import.png)

Die Seite &quot; *Konfigurieren* &quot;wird geöffnet. Geben Sie einen entsprechenden *Rezeptnamen* ein, z. B. &quot;Retail Sales recipe&quot;, und geben Sie optional eine Beschreibung oder eine Dokumentations-URL ein. Klicken Sie nach Abschluss des Vorgangs auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/package-source-files/configure.png)

Wählen Sie die entsprechende *Laufzeitumgebung* und dann eine **[!UICONTROL Klassifizierung]** für den *Typ*. Ihre Anmeldedaten für die Azurblase-Container-Registrierung werden nach Abschluss der Überprüfung generiert.

>[!NOTE]
>*Typ *ist die Klasse des maschinellen Lernproblems, für das das Rezept entwickelt wurde und nach dem Training verwendet wird, um die Beurteilung der Trainingslaufzeit anzupassen.

>[!TIP]
>- Wählen Sie für [!DNL Python] Rezepte die **[!UICONTROL Python]** -Laufzeit.
>- Wählen Sie für R-Rezepte die **[!UICONTROL R]** -Laufzeit.
>- Wählen Sie für PySpark-Rezepte die **[!UICONTROL PySpark]** -Laufzeit. Ein Artefakttyp wird automatisch gefüllt.
>- Wählen Sie für Scala-Rezepte die **[!UICONTROL Spark]** -Laufzeit. Ein Artefakttyp wird automatisch gefüllt.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für *Docker-Host*, *Benutzername* und *Kennwort*. Diese werden verwendet, um Ihr [!DNL Docker] Bild in der Workflows unten beschrieben zu erstellen und zu verschieben.

>[!NOTE]
>Die Quell-URL wird nach Abschluss der unten beschriebenen Schritte bereitgestellt. Die Konfigurationsdatei wird in den nachfolgenden Übungen in den [nächsten Schritten](#next-steps)erläutert.

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

### PySpark Docker-Bild erstellen {#pyspark-docker}

Beginn durch Klonen des [!DNL GitHub] Repositorys auf Ihrem lokalen System mit folgendem Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripten `login.sh` und `build.sh` sind hier zu finden und zum Anmelden bei Docker und zum Erstellen des Docker-Bildes. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

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
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zu den [nächsten Schritten](#next-steps).

### Erstellen eines Skala-Dockerbilds {#scala-docker}

Beginn durch Klonen des [!DNL GitHub] Repositorys auf Ihrem lokalen System mit dem folgenden Befehl im Terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie anschließend zum Ordner, in dem Sie die Skripte `experience-platform-dsw-reference/recipes/scala` und `login.sh` `build.sh`die Skripte finden können. Diese Skripten werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>Wenn Sie beim Versuch, sich mit dem `login.sh` Skript bei Docker anzumelden, einen Berechtigungsfehler erhalten, versuchen Sie, den Befehl zu verwenden `bash login.sh`.

Beim Ausführen des Anmeldeskripts müssen Sie den Docker-Host, den Benutzernamen und das Kennwort angeben. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Nachdem das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in der Konsolenausgabe. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zu den [nächsten Schritten](#next-steps).

## Nächste Schritte {#next-steps}

Diese Übung übernahm das Verpacken von Quelldateien in ein Rezept, den notwendigen Schritt zum Importieren eines Rezepts in [!DNL Data Science Workspace]. Sie sollten jetzt ein Docker-Bild in der Azurblauen Container-Registrierung zusammen mit der entsprechenden Bild-URL haben. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in beginnen [!DNL Data Science Workspace]. Wählen Sie einen der folgenden Links zum Einstieg:

- [Verpacktes Rezept in die Benutzeroberfläche importieren](./import-packaged-recipe-ui.md)
- [Verpacktes Rezept mit der API importieren](./import-packaged-recipe-api.md)