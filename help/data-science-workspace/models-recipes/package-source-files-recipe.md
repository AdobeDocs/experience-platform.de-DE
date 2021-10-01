---
keywords: Experience Platform; Paketquelldateien; Data Science Workspace; beliebte Themen; Docker; Docker-Bild
solution: Experience Platform
title: Quelldateien in einem Rezept verpacken
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquelldateien für Einzelhandelsumsätze in eine Archivdatei verpacken können, die zum Erstellen eines Rezepts in Adobe Experience Platform Data Science Workspace verwendet werden kann, indem Sie dem Workflow für den Rezeptimport entweder in der Benutzeroberfläche oder mithilfe der API folgen.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 1%

---

# Packen von Quelldateien in ein Rezept

In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquelldateien für Einzelhandelsumsätze in eine Archivdatei verpacken können, die zum Erstellen eines Rezepts in Adobe Experience Platform [!DNL Data Science Workspace] verwendet werden kann, indem Sie dem Workflow für den Rezeptimport entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Konzepte zum Verständnis:

- **Rezepte**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation und ist ein Container auf oberster Ebene, der einen bestimmten maschinellen Lernprozess, einen künstlichen Intelligenzalgorithmus oder eine Gruppe von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Erstellen und Ausführen eines trainierten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Quelldateien**: Einzelne Dateien in Ihrem Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Rezepterstellung

Die Erstellung von Rezepten beginnt mit dem Verpacken von Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala geschrieben. Die erstellten Archivdateien haben die Form eines Docker-Bildes. Nach der Erstellung wird die gepackte Archivdatei in [!DNL Data Science Workspace] importiert, um ein Rezept [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [mit der API](./import-packaged-recipe-api.md) zu erstellen.

### Docker-basiertes Modell-Authoring {#docker-based-model-authoring}

Ein Docker-Bild ermöglicht es einem Entwickler, eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten zu verpacken und als ein Paket auszugeben.

Das erstellte Docker-Bild wird mithilfe der Anmeldeinformationen, die Ihnen während des Workflows zur Rezepterstellung zur Verfügung gestellt werden, an die Azure Container Registry gesendet.

Um Ihre Anmeldedaten für die Azure Container Registry zu erhalten, melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an. Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Wählen Sie **[!UICONTROL Rezept importieren]** und danach **[!UICONTROL Launch]** aus. Weitere Informationen finden Sie im Screenshot unten.

![](../images/models-recipes/package-source-files/import.png)

Die Seite **[!UICONTROL Configure]** wird geöffnet. Geben Sie einen geeigneten **[!UICONTROL Rezeptnamen]** ein, z. B. &quot;Rezept für Einzelhandelsumsätze&quot;und geben Sie optional eine Beschreibung oder Dokumentations-URL ein. Klicken Sie nach Abschluss auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/package-source-files/configure.png)

Wählen Sie den entsprechenden *Runtime* und dann **[!UICONTROL Classification]** für *Typ*. Ihre Anmeldedaten für die Azure Container Registry werden nach Abschluss generiert.

>[!NOTE]
>
>** Typisierung nach der Klasse des maschinellen Lernproblems, für das das Rezept entwickelt wurde und nach dem Training verwendet wird, um die Auswertung des Trainings zu erleichtern.

>[!TIP]
>
>- Wählen Sie für [!DNL Python] -Rezepte die Laufzeit **[!UICONTROL Python]** aus.
>- Wählen Sie für R-Rezepte die Laufzeitumgebung **[!UICONTROL R]** aus.
>- Wählen Sie für PySpark-Rezepte die Laufzeit **[!UICONTROL PySpark]** aus. Ein Artefakttyp wird automatisch ausgefüllt.
>- Wählen Sie für Scala-Rezepte die Laufzeitumgebung **[!UICONTROL Spark]** aus. Ein Artefakttyp wird automatisch ausgefüllt.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für Docker-Host, Benutzername und Kennwort. Diese werden verwendet, um Ihr [!DNL Docker]-Bild in den unten beschriebenen Workflows zu erstellen und zu pushen.

>[!NOTE]
>
>Die Quell-URL wird bereitgestellt, nachdem Sie die unten beschriebenen Schritte ausgeführt haben. Die Konfigurationsdatei wird in nachfolgenden Tutorials erklärt, die in [den nächsten Schritten](#next-steps) zu finden sind.

### Quelldateien verpacken

Rufen Sie zunächst die Beispielcodebasis ab, die im Repository <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a> gefunden wird.

- [Python Docker-Bild erstellen](#python-docker)
- [R-Docker-Bild erstellen](#r-docker)
- [PySpark-Docker-Bild erstellen](#pyspark-docker)
- [Scala (Spark)-Docker-Bild erstellen](#scala-docker)

### Build [!DNL Python] Docker-Bild {#python-docker}

Wenn Sie dies noch nicht getan haben, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Skripte `login.sh` und `build.sh`, die zur Anmeldung bei Docker und zur Erstellung des Bildes [!DNL Python Docker] verwendet werden. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es ungefähr so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### Build R [!DNL Docker]-Bild {#r-docker}

Wenn Sie dies noch nicht getan haben, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in Ihrem geklonten Repository. Hier finden Sie die Dateien `login.sh` und `build.sh`, mit denen Sie sich bei Docker anmelden und das R Docker-Bild erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es ungefähr so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### PySpark-Docker-Bild erstellen {#pyspark-docker}

Klonen Sie zunächst das [!DNL GitHub]-Repository auf Ihrem lokalen System mit dem folgenden Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripte `login.sh` und `build.sh` befinden sich hier und werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es ungefähr so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### Scala Docker-Bild erstellen {#scala-docker}

Klonen Sie zunächst das [!DNL GitHub]-Repository auf Ihrem lokalen System mit dem folgenden Befehl im Terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie anschließend zum Verzeichnis `experience-platform-dsw-reference/recipes/scala` , in dem Sie die Skripte `login.sh` und `build.sh` finden. Diese Skripte werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge zum Terminal ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Wenn Sie beim Versuch, sich mit dem Skript `login.sh` bei Docker anzumelden, einen Berechtigungsfehler erhalten, versuchen Sie, den Befehl `bash login.sh` zu verwenden.

Beim Ausführen des Anmeldeskripts müssen Sie den Docker-Host, den Benutzernamen und das Kennwort angeben. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es ungefähr so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

## Nächste Schritte {#next-steps}

In diesem Tutorial wurde das Verpacken von Quelldateien in ein Rezept beschrieben, was die Voraussetzung für den Import eines Rezepts in [!DNL Data Science Workspace] ist. Sie sollten jetzt ein Docker-Bild in Azure Container Registry zusammen mit der entsprechenden Bild-URL haben. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] beginnen. Wählen Sie einen der folgenden Tutorial-Links aus, um zu beginnen:

- [Importieren eines gepackten Rezepts in die Benutzeroberfläche](./import-packaged-recipe-ui.md)
- [Importieren eines verpackten Rezepts mit der API](./import-packaged-recipe-api.md)
