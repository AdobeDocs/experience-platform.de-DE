---
keywords: Experience Platform;JupyterLab;Notebooks;Datenwissenschafts-Arbeitsbereich;beliebte Themen;Git;GitHub
solution: Experience Platform
title: Zusammenarbeiten in JupyterLab mit Git
type: Tutorial
description: Git ist ein verteiltes Versionskontrollsystem für das Tracking von Änderungen im Quell-Code während der Software-Entwicklung. Git ist im Datenwissenschafts-Arbeitsbereich der JupyterLab-Umgebung vorinstalliert.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: ht
source-wordcount: '284'
ht-degree: 100%

---

# Zusammenarbeiten in [!DNL JupyterLab] mit [!DNL Git]

[!DNL Git] ist ein verteiltes Versionskontrollsystem zum Tracking von Änderungen im Quell-Code während der Software-Entwicklung. Git ist in der [!DNL Data Science Workspace JupyterLab]-Umgebung vorinstalliert.

## Voraussetzungen

>[!NOTE]
>
> Der Git-Server, den Sie verwenden möchten, muss über das Internet zugänglich sein.

Die [!DNL Data Science Workspace JupyterLab]-Umgebung ist eine gehostete Umgebung und wird nicht innerhalb Ihrer Unternehmens-Firewall bereitgestellt. Daher muss der Git-Server, zu dem Sie eine Verbindung herstellen, über das öffentliche Internet zugänglich sein. Hierbei kann es sich um ein öffentliches oder privates Repository in [GitHub](https://github.com/) oder eine andere Instanz eines [!DNL Git]-Servers handeln, den Sie selbst hosten.

## Verbinden von [!DNL Git] mit der [!DNL Data Science Workspace JupyterLab Notebooks]-Umgebung

Starten Sie zunächst [!DNL Adobe Experience Platform] und navigieren Sie zur [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)-Umgebung.

Wählen Sie in [!DNL JupyterLab] das Menü **[!UICONTROL Datei]** aus und bewegen Sie dann den Mauszeiger über **[!UICONTROL Neu]**. Wählen Sie aus dem angezeigten Dropdown-Menü die Option **[!UICONTROL Terminal]** aus.

![JupyterLab-Navigation](../images/jupyterlab/tutorials/open-terminal.png)

Navigieren Sie als Nächstes innerhalb von *Terminal* mit dem folgenden Befehl zu Ihrem Arbeitsbereich: `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Um eine Liste der verfügbaren Git-Befehle anzuzeigen, geben Sie den Befehl `git -help` in Ihrem Terminal ein.

Klonen Sie anschließend das zu verwendende Repository mit dem Befehl `git clone`. Klonen Sie Ihr Projekt mit einer `https://`-URL statt mit `ssh://`.

**Beispiel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![Klonen](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Um Schreibvorgänge durchzuführen (beispielsweise `git push`), müssen die folgenden Konfigurationsbefehle für jede neue Sitzung ausgeführt werden. Beachten Sie außerdem, dass bei jedem Push-Befehl zur Eingabe eines Benutzernamens und Kennworts aufgefordert wird.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nächste Schritte

Nachdem Sie Ihr Repository geklont haben, können Sie Git wie gewohnt auf Ihrem lokalen Computer verwenden, um mit anderen auf Notebooks zusammenzuarbeiten. Weiterführende Informationen dazu, was alles in [!DNL JupyterLab] möglich ist, finden Sie im [[!DNL JupyterLab user guide]](./overview.md).
