---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Zusammenarbeit in JupyterLab mit Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Zusammenarbeit bei der [!DNL JupyterLab] Verwendung von [!DNL Git]

[!DNL Git] ist ein verteiltes Versionskontrollsystem zur Verfolgung von Änderungen im Quellcode während der Softwareentwicklung. Git wird innerhalb der [!DNL Data Science Workspace JupyterLab] Umgebung vorinstalliert.

## Voraussetzungen

>[!NOTE]
> Der Git-Server, den Sie verwenden möchten, muss über das Internet zugänglich sein.

Die [!DNL Data Science Workspace JupyterLab] Umgebung ist eine gehostete Umgebung und nicht innerhalb Ihrer Unternehmens-Firewall bereitgestellt. Daher muss der Git-Server, zu dem Sie eine Verbindung herstellen, über das öffentliche Internet zugänglich sein. Dies kann ein öffentliches oder privates Repository auf [GitHub](https://github.com/) oder eine andere Instanz eines [!DNL Git] Servers sein, den Sie selbst hosten möchten.

## Verbindung [!DNL Git] zur [!DNL Data Science Workspace JupyterLab Notebooks] Umgebung

Beginn durch Starten [!DNL Adobe Experience Platform] und Navigieren zur [!DNL JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) Umgebung.

Wählen Sie in [!DNL JupyterLab]der **[!UICONTROL Datei]** die Option und halten Sie den Mauszeiger über **[!UICONTROL Neu]**. Wählen Sie aus der Dropdown-Liste **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Navigieren Sie anschließend in *Terminal* mithilfe des folgenden Befehls zu Ihrem Arbeitsbereich: `cd my-workspace`.

![cd-Arbeitsbereich](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> Um eine Liste der verfügbaren Git-Befehle anzuzeigen, geben Sie den Befehl aus: `git -help` in Ihrem Terminal.

Anschließend klonen Sie das Repository, das Sie mit dem `git clone` Befehl verwenden möchten. Klonen Sie Ihr Projekt mit einer `https://` URL statt `ssh://`.

**Beispiel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> Für die Ausführung von Schreibvorgängen (`git push` z. B.) müssen die folgenden Konfigurationsbefehle für jede neue Sitzung ausgeführt werden. Beachten Sie auch, dass bei jedem Push-Befehl ein Benutzername und ein Kennwort angegeben werden.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nächste Schritte

Nachdem Sie das Klonen Ihres Repositorys abgeschlossen haben, können Sie Git wie gewohnt auf Ihrem lokalen Computer verwenden, um mit anderen an Notebooks zusammenzuarbeiten. Weitere Informationen dazu, was Sie in diesem Abschnitt tun können, [!DNL JupyterLab]finden Sie in der [!DNL JupyterLab user guide](./overview.md).
