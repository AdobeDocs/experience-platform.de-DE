---
keywords: Experience Platform; Paketquelldateien; Data Science Workspace; beliebte Themen; Docker; Docker-Bild
solution: Experience Platform
title: Quelldateien in einem Rezept verpacken
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquelldateien für Einzelhandelsumsätze in eine Archivdatei verpacken können, die zum Erstellen eines Rezepts in Adobe Experience Platform Data Science Workspace verwendet werden kann, indem Sie dem Workflow für den Rezeptimport entweder in der Benutzeroberfläche oder mithilfe der API folgen.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 1%

---

# Packen von Quelldateien in ein Rezept

In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquelldateien für Einzelhandelsumsätze in eine Archivdatei verpacken können, die zum Erstellen eines Rezepts in Adobe Experience Platform verwendet werden kann. [!DNL Data Science Workspace] durch Befolgen des Workflows zum Importieren von Rezepten in der Benutzeroberfläche oder mithilfe der API.

Konzepte zum Verständnis:

- **Rezepte**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation und ist ein Container auf oberster Ebene, der einen bestimmten maschinellen Lernprozess, einen künstlichen Intelligenzalgorithmus oder eine Gruppe von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Erstellen und Ausführen eines trainierten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Quelldateien**: Einzelne Dateien in Ihrem Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Rezepterstellung

Die Erstellung von Rezepten beginnt mit dem Verpacken von Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala. Die erstellten Archivdateien haben die Form eines Docker-Bildes. Nach der Erstellung wird die gepackte Archivdatei in [!DNL Data Science Workspace] , um ein Rezept zu erstellen [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [Verwendung der API](./import-packaged-recipe-api.md).

### Docker-basiertes Modell-Authoring {#docker-based-model-authoring}

Ein Docker-Bild ermöglicht es einem Entwickler, eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten zu verpacken und als ein Paket auszugeben.

Das erstellte Docker-Bild wird mithilfe der Anmeldeinformationen, die Ihnen während des Workflows zur Rezepterstellung zur Verfügung gestellt werden, an die Azure Container Registry gesendet.

Um Ihre Anmeldedaten für die Azure Container Registry zu erhalten, melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com). Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Auswählen **[!UICONTROL Rezept importieren]** gefolgt von der Auswahl **[!UICONTROL Launch]**. Weitere Informationen finden Sie im Screenshot unten.

![](../images/models-recipes/package-source-files/import.png)

Die **[!UICONTROL Konfigurieren]** Seite geöffnet. Stellen Sie eine geeignete **[!UICONTROL Rezeptname]**, z. B. &quot;Rezept für Einzelhandelsumsätze&quot;und optional eine Beschreibung oder Dokumentations-URL angeben. Klicken Sie nach Abschluss des Vorgangs auf **[!UICONTROL Nächste]**.

![](../images/models-recipes/package-source-files/configure.png)

Wählen Sie die entsprechende *Laufzeit*, wählen Sie dann eine **[!UICONTROL Klassifizierung]** für *Typ*. Ihre Anmeldedaten für die Azure Container Registry werden nach Abschluss generiert.

>[!NOTE]
>
>*Typ* ist die Klasse des Problems des maschinellen Lernens, für das das Rezept entwickelt wurde und nach dem Training verwendet wird, um die Trainings-Läufe anzupassen.

>[!TIP]
>
>- Für [!DNL Python] Rezepte wählen Sie die **[!UICONTROL Python]** Laufzeit.
>- Wählen Sie für Rezepte die Option **[!UICONTROL R]** Laufzeit.
>- Wählen Sie für PySpark-Rezepte die **[!UICONTROL PySpark]** Laufzeit. Ein Artefakttyp wird automatisch ausgefüllt.
>- Wählen Sie für Scala-Rezepte die **[!UICONTROL Spark]** Laufzeit. Ein Artefakttyp wird automatisch ausgefüllt.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für Docker-Host, Benutzername und Kennwort. Diese werden verwendet, um Ihre [!DNL Docker] in den unten beschriebenen Workflows angezeigt.

>[!NOTE]
>
>Die Quell-URL wird bereitgestellt, nachdem Sie die unten beschriebenen Schritte ausgeführt haben. Die Konfigurationsdatei wird in nachfolgenden Tutorials in [Nächste Schritte](#next-steps).

### Quelldateien verpacken

Rufen Sie zunächst die Codebase-Beispieldatei ab, die im <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace-Referenz</a> Repository.

- [Python Docker-Bild erstellen](#python-docker)
- [R-Docker-Bild erstellen](#r-docker)
- [PySpark-Docker-Bild erstellen](#pyspark-docker)
- [Scala (Spark)-Docker-Bild erstellen](#scala-docker)

### Build [!DNL Python] Docker-Bild {#python-docker}

Falls nicht, klonen Sie die [!DNL GitHub] Repository auf Ihrem lokalen System mit dem folgenden Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis . `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Scripts `login.sh` und `build.sh` zum Anmelden bei Docker und zum Erstellen der [!DNL Python Docker] Bild. Wenn Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit, geben Sie die folgenden Befehle in der Reihenfolge ein:

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

Kopieren Sie diese URL und fahren Sie mit dem [Nächste Schritte](#next-steps).

### Build R [!DNL Docker] image {#r-docker}

Falls nicht, klonen Sie die [!DNL GitHub] Repository auf Ihrem lokalen System mit dem folgenden Befehl:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis . `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in Ihrem geklonten Repository. Hier finden Sie die Dateien `login.sh` und `build.sh` die Sie verwenden werden, um sich bei Docker anzumelden und das R Docker-Bild zu erstellen. Wenn Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit, geben Sie die folgenden Befehle in der Reihenfolge ein:

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

Kopieren Sie diese URL und fahren Sie mit dem [Nächste Schritte](#next-steps).

### PySpark-Docker-Bild erstellen {#pyspark-docker}

Beginnen Sie mit dem Klonen der [!DNL GitHub] Repository auf Ihrem lokalen System mit dem folgenden Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis . `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripte `login.sh` und `build.sh` befinden sich hier und werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit, geben Sie die folgenden Befehle in der Reihenfolge ein:

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

Kopieren Sie diese URL und fahren Sie mit dem [Nächste Schritte](#next-steps).

### Scala Docker-Bild erstellen {#scala-docker}

Beginnen Sie mit dem Klonen der [!DNL GitHub] Repository auf Ihrem lokalen System mit dem folgenden Befehl im Terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie anschließend zum Ordner . `experience-platform-dsw-reference/recipes/scala` wo Sie die Skripte finden `login.sh` und `build.sh`. Diese Skripte werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit, geben Sie die folgenden Befehle in der Reihenfolge zum Terminal ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Wenn Sie einen Berechtigungsfehler erhalten, wenn Sie versuchen, sich mit dem `login.sh` Skript, versuchen Sie es mit dem Befehl `bash login.sh`.

Beim Ausführen des Anmeldeskripts müssen Sie den Docker-Host, den Benutzernamen und das Kennwort angeben. Beim Erstellen müssen Sie den Docker-Host und ein Version-Tag für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es ungefähr so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit dem [Nächste Schritte](#next-steps).

## Nächste Schritte {#next-steps}

In diesem Tutorial wurde das Verpacken von Quelldateien in ein Rezept überführt, was die Voraussetzung für den Import eines Rezepts in [!DNL Data Science Workspace]. Sie sollten jetzt ein Docker-Bild in Azure Container Registry zusammen mit der entsprechenden Bild-URL haben. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in beginnen. [!DNL Data Science Workspace]. Wählen Sie einen der folgenden Tutorial-Links aus, um zu beginnen:

- [Importieren eines gepackten Rezepts in die Benutzeroberfläche](./import-packaged-recipe-ui.md)
- [Importieren eines verpackten Rezepts mit der API](./import-packaged-recipe-api.md)
