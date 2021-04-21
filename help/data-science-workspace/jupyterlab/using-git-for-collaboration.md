---
keywords: Experience Platform;JupyterLab;Notebooks;Data Science Workspace;beliebte Themen;Git;Github
solution: Experience Platform
title: Zusammenarbeit in JupyterLab mithilfe von Git
topic-legacy: tutorial
type: Tutorial
description: Git ist ein verteiltes Versionsverwaltungssystem zur Verfolgung von Änderungen im Quellcode während der Softwareentwicklung. Git wird in der Data Science Workspace JupyterLab-Umgebung vorinstalliert.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# In [!DNL JupyterLab] mit [!DNL Git] zusammenarbeiten

[!DNL Git] ist ein verteiltes Versionskontrollsystem zur Verfolgung von Änderungen im Quellcode während der Softwareentwicklung. Git wird innerhalb der [!DNL Data Science Workspace JupyterLab]-Umgebung vorinstalliert.

## Voraussetzungen

>[!NOTE]
>
> Der Git-Server, den Sie verwenden möchten, muss über das Internet zugänglich sein.

Die [!DNL Data Science Workspace JupyterLab]-Umgebung ist eine gehostete Umgebung und nicht in Ihrer Unternehmens-Firewall bereitgestellt. Daher muss der Git-Server, zu dem Sie eine Verbindung herstellen, über das öffentliche Internet zugänglich sein. Dies kann ein öffentliches oder privates Repository auf [GitHub](https://github.com/) oder eine andere Instanz eines [!DNL Git]-Servers sein, die Sie selbst hosten möchten.

## Verbinden Sie [!DNL Git] mit der [!DNL Data Science Workspace JupyterLab Notebooks]-Umgebung

Beginn durch Starten von [!DNL Adobe Experience Platform] und Navigieren zur Umgebung [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

Wählen Sie in [!DNL JupyterLab] **[!UICONTROL Datei]** und halten Sie den Mauszeiger über **[!UICONTROL Neu]**. Wählen Sie aus der Dropdown-Liste **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Navigieren Sie anschließend mit dem folgenden Befehl innerhalb von *Terminal* zu Ihrem Arbeitsbereich: `cd my-workspace`.

![cd-Arbeitsbereich](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Um eine Liste der verfügbaren Git-Befehle anzuzeigen, geben Sie den Befehl aus: `git -help` in Ihrem Terminal.

Anschließend klonen Sie das Repository, das Sie mit dem Befehl `git clone` verwenden möchten. Klonen Sie Ihr Projekt mit einer `https://`-URL anstelle von `ssh://`.

**Beispiel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Um zum Beispiel Schreibvorgänge auszuführen (`git push`) müssen die folgenden Konfigurationsbefehle für jede neue Sitzung ausgeführt werden. Beachten Sie auch, dass bei jedem Push-Befehl ein Benutzername und ein Kennwort angegeben werden.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nächste Schritte

Nachdem Sie das Klonen Ihres Repositorys abgeschlossen haben, können Sie Git wie gewohnt auf Ihrem lokalen Computer verwenden, um mit anderen an Notebooks zusammenzuarbeiten. Weitere Informationen dazu, was Sie innerhalb von [!DNL JupyterLab] tun können, finden Sie unter [[!DNL JupyterLab user guide]](./overview.md).
