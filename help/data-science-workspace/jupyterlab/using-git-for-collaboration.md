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

# Zusammenarbeit in [!DNL JupyterLab] mithilfe von [!DNL Git]

[!DNL Git] ist ein verteiltes Versionskontrollsystem zur Verfolgung von Änderungen im Quellcode während der Softwareentwicklung. Git wird in der Umgebung [!DNL Data Science Workspace JupyterLab] vorinstalliert.

## Voraussetzungen

>[!NOTE]
>
> Der Git-Server, den Sie verwenden möchten, muss über das Internet zugänglich sein.

Die [!DNL Data Science Workspace JupyterLab]-Umgebung ist eine gehostete Umgebung, die nicht in Ihrer Unternehmens-Firewall bereitgestellt wird. Daher muss der Git-Server, zu dem Sie eine Verbindung herstellen, über das öffentliche Internet zugänglich sein. Dies kann ein öffentliches oder privates Repository auf [GitHub](https://github.com/) oder eine andere Instanz eines [!DNL Git]-Servers sein, die Sie selbst hosten möchten.

## Verbinden Sie [!DNL Git] mit der [!DNL Data Science Workspace JupyterLab Notebooks]-Umgebung

Starten Sie [!DNL Adobe Experience Platform] und navigieren Sie zur Umgebung [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) .

Wählen Sie in [!DNL JupyterLab] **[!UICONTROL Datei]** und bewegen Sie dann den Mauszeiger über **[!UICONTROL Neu]**. Wählen Sie im angezeigten Dropdown-Menü **[!UICONTROL Terminal]** aus.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Navigieren Sie anschließend in *Terminal* mithilfe des folgenden Befehls zu Ihrem Arbeitsbereich: `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Um eine Liste der verfügbaren Git-Befehle anzuzeigen, geben Sie den Befehl aus: `git -help` in Ihrem Terminal.

Klonen Sie anschließend das Repository, das Sie mit dem Befehl `git clone` verwenden möchten. Klonen Sie Ihr Projekt mit einer `https://`-URL anstelle von `ssh://`.

**Beispiel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Um beispielsweise Schreibvorgänge (`git push`) durchzuführen, müssen die folgenden Konfigurationsbefehle für jede neue Sitzung ausgeführt werden. Beachten Sie außerdem, dass bei jedem Push-Befehl ein Benutzername und ein Kennwort angezeigt werden.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nächste Schritte

Nachdem Sie das Klonen Ihres Repositorys abgeschlossen haben, können Sie Git wie gewohnt auf Ihrem lokalen Computer verwenden, um mit anderen an Notebooks zusammenzuarbeiten. Weitere Informationen dazu, was Sie in [!DNL JupyterLab] tun können, finden Sie unter [[!DNL JupyterLab user guide]](./overview.md).
