---
keywords: Experience Platform;Paketquellendateien;Data Science Workspace;beliebte Themen;Docker;Docker-Bild
solution: Experience Platform
title: Quelldateien in einem Rezept verpacken
topic-legacy: tutorial
type: Tutorial
description: In diesem Lernprogramm wird beschrieben, wie Sie die angegebenen Quelldateien für den Einzelhandel in eine Archivdatei packen können, die zum Erstellen eines Rezepts in Adobe Experience Platform Data Science Workspace verwendet werden kann, indem Sie dem Skript-Import-Arbeitsablauf entweder in der Benutzeroberfläche oder mithilfe der API folgen.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Verpacken von Quelldateien in einem Rezept

Dieses Lernprogramm enthält Anweisungen dazu, wie Sie die angegebenen Quelldateien für den Einzelhandel in einer Archivdatei verpacken können, die zum Erstellen eines Rezepts in Adobe Experience Platform [!DNL Data Science Workspace] verwendet werden kann, indem Sie dem Skript-Import-Arbeitsablauf entweder in der Benutzeroberfläche oder mithilfe der API folgen.

Konzepte zum Verständnis:

- **Rezepte**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen Algorithmus für künstliche Intelligenz oder ein Ensemble von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Aufbau und zur Ausführung eines geschulten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.
- **Quelldateien**: Einzelne Dateien im Projekt, die die Logik für ein Rezept enthalten.

## Voraussetzungen

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Rezepterstellung

Beginn zur Rezepterstellung mit Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden, und werden entweder in [!DNL Python], R, PySpark oder Scala geschrieben. Die erstellten Archivdateien haben die Form eines Dockerbilds. Nach der Erstellung wird die verpackte Archivdatei in [!DNL Data Science Workspace] importiert, um ein Rezept [in der Benutzeroberfläche](./import-packaged-recipe-ui.md) oder [mit der API](./import-packaged-recipe-api.md) zu erstellen.

### Dockerbasiertes Modell-Authoring {#docker-based-model-authoring}

Ein Docker-Bild ermöglicht es einem Entwickler, eine Anwendung mit allen benötigten Teilen wie Bibliotheken und anderen Abhängigkeiten zu verpacken und als ein Paket zu versenden.

Das erstellte Docker-Bild wird mit den Anmeldeinformationen, die Sie während des Rezepterstellungsarbeitsablaufs erhalten haben, in die Azurblaue Container-Registrierung verschoben.

Melden Sie sich zum Abrufen Ihrer Azurblase Container Registry-Anmeldeinformationen bei [Adobe Experience Platform](https://platform.adobe.com) an. Navigieren Sie in der linken Navigationsspalte zu **[!UICONTROL Workflows]**. Wählen Sie **[!UICONTROL Rezept importieren]** und dann **[!UICONTROL Starten]**. Siehe Screenshot unten als Referenz.

![](../images/models-recipes/package-source-files/import.png)

Die Seite **[!UICONTROL Configure]** wird geöffnet. Geben Sie einen entsprechenden **[!UICONTROL Rezeptnamen]** ein, z. B. &quot;Retail Sales recipe&quot;, und geben Sie optional eine Beschreibung oder eine Dokumentations-URL ein. Klicken Sie nach Abschluss des Vorgangs auf **[!UICONTROL Weiter]**.

![](../images/models-recipes/package-source-files/configure.png)

Wählen Sie die entsprechende *Laufzeitumgebung* und dann **[!UICONTROL Klassifizierung]** für *Typ*. Ihre Anmeldedaten für die Azurblase-Container-Registrierung werden nach Abschluss der Überprüfung generiert.

>[!NOTE]
>
>*Die* Art des maschinellen Lernproblems, für das das Rezept entwickelt wurde und nach dem Training verwendet wird, um eine maßgeschneiderte Auswertung des Trainingslaufs zu ermöglichen.

>[!TIP]
>
>- Wählen Sie für [!DNL Python]-Rezepte die Laufzeit **[!UICONTROL Python]** aus.
>- Wählen Sie für R-Rezepte die Laufzeitumgebung **[!UICONTROL R]**.
>- Wählen Sie für PySpark-Rezepte die Laufzeitumgebung **[!UICONTROL PySpark]**. Ein Artefakttyp wird automatisch gefüllt.
>- Wählen Sie für Scala-Rezepte die Laufzeitumgebung **[!UICONTROL Spark]**. Ein Artefakttyp wird automatisch gefüllt.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notieren Sie die Werte für Docker-Host, Benutzername und Kennwort. Diese werden verwendet, um Ihr [!DNL Docker]-Bild in der Workflows unten beschrieben zu erstellen und zu verschieben.

>[!NOTE]
>
>Die Quell-URL wird nach Abschluss der unten beschriebenen Schritte bereitgestellt. Die Konfigurationsdatei wird in nachfolgenden Lernprogrammen unter [Nächste Schritte](#next-steps) erklärt.

### Verpacken der Quelldateien

Beginn durch Abrufen der Codebasis für Beispieldateien im Repository <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>.

- [Python-Docker-Bild erstellen](#python-docker)
- [R-Docker-Bild erstellen](#r-docker)
- [PySpark Docker-Bild erstellen](#pyspark-docker)
- [Punktdiagrammbild erstellen (Spark)](#scala-docker)

### Erstellen [!DNL Python] Dockerbild {#python-docker}

Falls nicht, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Ordner `experience-platform-dsw-reference/recipes/python/retail`. Hier finden Sie die Skripte `login.sh` und `build.sh`, die zum Anmelden bei Docker und zum Erstellen des [!DNL Python Docker]-Bildes verwendet werden. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

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

Kopieren Sie diese URL und gehen Sie zum [nächsten Schritt](#next-steps).

### Build R [!DNL Docker] Bild {#r-docker}

Falls nicht, klonen Sie das [!DNL GitHub]-Repository mit dem folgenden Befehl auf Ihrem lokalen System:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Ordner `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in Ihrem geklonten Repository. Hier finden Sie die Dateien `login.sh` und `build.sh`, die Sie verwenden werden, um sich bei Docker anzumelden und das R Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

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

Kopieren Sie diese URL und gehen Sie zum [nächsten Schritt](#next-steps).

### PySpark Docker-Bild {#pyspark-docker} erstellen

Beginn durch Klonen des [!DNL GitHub]-Repositorys auf Ihrem lokalen System mit folgendem Befehl:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie zum Ordner `experience-platform-dsw-reference/recipes/pyspark/retail`. Die Skripten `login.sh` und `build.sh` befinden sich hier und dienen zum Anmelden bei Docker und zum Erstellen des Dockerbilds. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der richtigen Reihenfolge ein:

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

Kopieren Sie diese URL und gehen Sie zum [nächsten Schritt](#next-steps).

### Skala-Docker-Bild {#scala-docker} erstellen

Beginn durch Klonen des [!DNL GitHub]-Repositorys auf Ihrem lokalen System mit dem folgenden Befehl im Terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigieren Sie anschließend zum Ordner `experience-platform-dsw-reference/recipes/scala`, in dem Sie die Skripte `login.sh` und `build.sh` finden können. Diese Skripten werden verwendet, um sich bei Docker anzumelden und das Docker-Bild zu erstellen. Wenn Sie Ihre [Docker-Anmeldeinformationen](#docker-based-model-authoring) bereit haben, geben Sie die folgenden Befehle in der Reihenfolge zum Terminal ein:

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

Nachdem das Build-Skript abgeschlossen ist, erhalten Sie eine Docker-Quelldatei-URL in der Konsolenausgabe. Für dieses spezifische Beispiel sieht es wie folgt aus:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieren Sie diese URL und gehen Sie zum [nächsten Schritt](#next-steps).

## Nächste Schritte {#next-steps}

In diesem Lernprogramm wurden Quelldateien in ein Rezept verpackt, das die Voraussetzung für den Import eines Rezepts in [!DNL Data Science Workspace] ist. Sie sollten jetzt ein Docker-Bild in der Azurblauen Container-Registrierung zusammen mit der entsprechenden Bild-URL haben. Sie können jetzt mit dem Tutorial zum Importieren eines gepackten Rezepts in [!DNL Data Science Workspace] beginnen. Wählen Sie einen der folgenden Links zum Einstieg:

- [Verpacktes Rezept in die Benutzeroberfläche importieren](./import-packaged-recipe-ui.md)
- [Verpacktes Rezept mit der API importieren](./import-packaged-recipe-api.md)
