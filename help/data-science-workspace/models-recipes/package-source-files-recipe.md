---
keywords: Experience Platform;Paketquelldateien;Data Science Workspace;beliebte Themen;Docker;Docker-Image
solution: Experience Platform
title: Packen von Source-Dateien in ein Rezept
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquellendateien für den Einzelhandel in eine Archivdatei packen können, die Sie zum Erstellen eines Rezepts in Adobe Experience Platform Data Science Workspace verwenden können, indem Sie den Workflow zum Importieren von Rezepten entweder in der Benutzeroberfläche oder mithilfe der -API befolgen.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Packen von Quelldateien in ein Rezept

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial erfahren Sie, wie Sie die bereitgestellten Beispielquelldateien für den Einzelhandel in eine Archivdatei packen können, mit der Sie in Adobe Experience Platform [!DNL Data Science Workspace] ein Rezept erstellen können, indem Sie dem Import-Workflow für Rezepte entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Zu verstehende Konzepte:

- **Rezepte**: Ein Rezept ist ein Adobe-Begriff für eine Modellspezifikation und ein Container auf oberster Ebene, der einen bestimmten Algorithmus für maschinelles Lernen, einen Algorithmus für künstliche Intelligenz oder eine Gruppe von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die zum Erstellen und Ausführen eines trainierten Modells und somit zur Lösung spezifischer Geschäftsprobleme erforderlich sind.
- **Source-**: Einzelne Dateien in Ihrem Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Rezepterstellung

Die Rezepterstellung beginnt mit dem Verpacken von Quelldateien, um eine Archivdatei zu erstellen. Source-Dateien definieren die Logik und die Algorithmen des maschinellen Lernens, die zum Lösen eines bestimmten vorliegenden Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala geschrieben. Die erstellten Archivdateien haben die Form eines Docker-Images. Nach der Erstellung wird die gepackte Archivdatei in [!DNL Data Science Workspace] importiert, um ein Rezept ([&#128279;](./import-packaged-recipe-ui.md) der Benutzeroberfläche oder ([&#x200B; der API](./import-packaged-recipe-api.md) zu erstellen.

### Docker-basierte Modellerstellung {#docker-based-model-authoring}

Mit einem Docker-Image kann ein Entwickler eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten als Paket verpacken und als ein Paket versenden.

Das erstellte Docker-Image wird mithilfe der Anmeldeinformationen, die Sie während des Workflows zur Rezepterstellung erhalten haben, an die Azure-Container-Registrierung gepusht.

Um Ihre Azure Container Registry-Anmeldedaten zu erhalten, melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an. Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Wählen Sie **[!UICONTROL Rezept importieren]** und dann **[!UICONTROL Starten]** aus. Siehe Screenshot unten als Referenz.

![](../images/models-recipes/package-source-files/import.png)

Die **[!UICONTROL „Konfigurieren]** wird geöffnet. Geben Sie einen geeigneten **[!UICONTROL Rezeptnamen]** z. B. „Einzelhandelsverkaufsrezept“ an und geben Sie optional eine Beschreibung oder eine Dokumentations-URL an. Klicken Sie anschließend auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/package-source-files/configure.png)

Wählen Sie die entsprechende *Laufzeit* und wählen Sie dann **[!UICONTROL Klassifizierung]** für *Typ*. Ihre Azure Container-Registrierungsanmeldeinformationen werden nach Abschluss generiert.

>[!NOTE]
>
>*Type* ist die Klasse des Problems des maschinellen Lernens, für das das Rezept entwickelt wurde, und wird nach dem Training verwendet, um die Bewertung des Trainings-Durchgangs anzupassen.

>[!TIP]
>
>- Wählen Sie für [!DNL Python] Rezepte die **[!UICONTROL Python]**-Laufzeit aus.
>- Wählen Sie für Rezepte des Typs R die **[!UICONTROL R]**-Laufzeit aus.
>- Wählen Sie für PySpark-Rezepte die **[!UICONTROL PySpark]**-Laufzeit aus. Ein Artefakttyp wird automatisch ausgefüllt.
>- Wählen Sie für Scala-Rezepte die **[!UICONTROL Spark]**-Laufzeit aus. Ein Artefakttyp wird automatisch ausgefüllt.

![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für Docker-Host, Benutzernamen und Kennwort. Diese werden in den unten beschriebenen Workflows zum Erstellen und Übertragen Ihres [!DNL Docker]-Images verwendet.

>[!NOTE]
>
>Die Source-URL wird bereitgestellt, nachdem Sie die unten beschriebenen Schritte ausgeführt haben. Die Konfigurationsdatei wird in nachfolgenden Tutorials unter &quot;[&#x200B; Schritte“ &#x200B;](#next-steps).

### Packen der Quelldateien

Rufen Sie zunächst die Beispiel-Code-Basis aus dem <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>-Repository ab.

- [Python-Docker-Image erstellen](#python-docker)
- [Build R Docker-Image](#r-docker)
- [PySpark Docker-Image erstellen](#pyspark-docker)
- [Erstellen eines Scala (Spark)-Docker-Images](#scala-docker)

### Erstellen [!DNL Python] Docker-Images {#python-docker}

Wenn Sie dies nicht getan haben, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihr lokales System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Skripte `login.sh` und `build.sh`, mit denen Sie sich bei Docker anmelden und das [!DNL Python Docker]-Image erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Versionstags für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es in etwa so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### R [!DNL Docker]-Image erstellen {#r-docker}

Wenn Sie dies nicht getan haben, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihr lokales System:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` im geklonten Repository. Hier finden Sie die Dateien `login.sh` und `build.sh`, mit denen Sie sich bei Docker anmelden und das R Docker-Image erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Versionstags für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es in etwa so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### PySpark Docker-Image erstellen {#pyspark-docker}

Klonen Sie zunächst das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihr lokales System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Verzeichnis `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripte `login.sh` und `build.sh` befinden sich hier und werden verwendet, um sich bei Docker anzumelden und das Docker-Image zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Beachten Sie, dass Sie beim Ausführen des Anmeldeskripts den Docker-Host, den Benutzernamen und das Kennwort angeben müssen. Beim Erstellen müssen Sie den Docker-Host und ein Versionstags für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es in etwa so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

### Erstellen eines Scala Docker-Images {#scala-docker}

Klonen Sie zunächst das [!DNL GitHub]-Repository auf Ihrem lokalen System mit dem folgenden Befehl im Terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie anschließend zum Verzeichnis `experience-platform-dsw-reference/recipes/scala` , in dem Sie die Skripte `login.sh` und `build.sh` finden. Diese Skripte werden verwendet, um sich bei Docker anzumelden und das Docker-Image zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in die Terminal-Reihenfolge ein:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Wenn Sie beim Versuch, sich mit dem `login.sh`-Skript bei Docker anzumelden, einen Berechtigungsfehler erhalten, versuchen Sie es mit dem `bash login.sh` .

Beim Ausführen des Anmeldeskripts müssen Sie den Docker-Host, den Benutzernamen und das Kennwort angeben. Beim Erstellen müssen Sie den Docker-Host und ein Versionstags für den Build angeben.

Sobald das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in Ihrer Konsolenausgabe. Für dieses spezifische Beispiel sieht es in etwa so aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieren Sie diese URL und fahren Sie mit den [nächsten Schritten](#next-steps) fort.

## Nächste Schritte {#next-steps}

In diesem Tutorial wurde das Verpacken von Quelldateien in ein Rezept erläutert. Dies ist der erforderliche Schritt zum Importieren eines Rezepts in [!DNL Data Science Workspace]. Sie sollten jetzt über ein Docker-Image in der Azure Container-Registrierung zusammen mit der entsprechenden Bild-URL verfügen. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] beginnen. Wählen Sie einen der folgenden Tutorial-Links, um zu beginnen:

- [Gepacktes Rezept in die Benutzeroberfläche importieren](./import-packaged-recipe-ui.md)
- [Importieren eines gepackten Rezepts mithilfe der API](./import-packaged-recipe-api.md)
