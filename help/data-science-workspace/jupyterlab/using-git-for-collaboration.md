---
keywords: Experience Platform;JupyterLab;Notebooks;Data Science Workspace;beliebte Themen;Git;Git;GitHub
solution: Experience Platform
title: Zusammenarbeit in JupyterLab mithilfe von Git
topic-legacy: tutorial
type: Tutorial
description: Git ist ein verteiltes Versionskontrollsystem zum Verfolgen von Änderungen im Quellcode während der Softwareentwicklung. Git wird in der JupyterLab-Umgebung von Data Science Workspace vorinstalliert.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Zusammenarbeit in [!DNL JupyterLab] using [!DNL Git]

[!DNL Git] ist ein verteiltes Versionskontrollsystem zur Verfolgung von Änderungen im Quellcode während der Softwareentwicklung. Git wird im [!DNL Data Science Workspace JupyterLab] Umgebung.

## Voraussetzungen

>[!NOTE]
>
> Der Git-Server, den Sie verwenden möchten, muss über das Internet zugänglich sein.

Die [!DNL Data Science Workspace JupyterLab] -Umgebung ist eine gehostete Umgebung und nicht in Ihrer Unternehmens-Firewall bereitgestellt. Daher muss der Git-Server, zu dem Sie eine Verbindung herstellen, über das öffentliche Internet zugänglich sein. Dies kann ein öffentliches oder privates Repository in [GitHub](https://github.com/) oder einer anderen Instanz eines [!DNL Git] -Server, den Sie selbst hosten möchten.

## Verbinden [!DNL Git] der [!DNL Data Science Workspace JupyterLab Notebooks] Umgebung

Starten durch Starten [!DNL Adobe Experience Platform] und zur [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) Umgebung.

Within [!DNL JupyterLab]auswählen **[!UICONTROL Datei]** dann den Mauszeiger darüber bewegen **[!UICONTROL Neu]**. Wählen Sie aus dem angezeigten Dropdown-Menü **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Weiter, innerhalb *Terminal* Navigieren Sie mit dem folgenden Befehl zu Ihrem Arbeitsbereich: `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Um eine Liste der verfügbaren Git-Befehle anzuzeigen, geben Sie den Befehl aus: `git -help` in Ihrem Terminal.

Klonen Sie anschließend das Repository, das Sie mit dem `git clone` Befehl. Projekt mithilfe eines `https://` URL anstelle von `ssh://`.

**Beispiel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Um alle Schreibvorgänge durchzuführen (`git push` Beispielsweise müssen die folgenden Konfigurationsbefehle für jede neue Sitzung ausgeführt werden. Beachten Sie außerdem, dass bei jedem Push-Befehl ein Benutzername und ein Kennwort angezeigt werden.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nächste Schritte

Nachdem Sie das Klonen Ihres Repositorys abgeschlossen haben, können Sie Git wie gewohnt auf Ihrem lokalen Computer verwenden, um mit anderen an Notebooks zusammenzuarbeiten. Weitere Informationen dazu, was Sie in [!DNL JupyterLab], siehe [[!DNL JupyterLab user guide]](./overview.md).
