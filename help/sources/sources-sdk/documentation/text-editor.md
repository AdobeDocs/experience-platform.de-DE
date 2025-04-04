---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Verwenden eines Texteditors in der lokalen Umgebung, um eine Seite mit der Quelldokumentation zu erstellen
description: In diesem Dokument wird beschrieben, wie Sie mit Ihrer lokalen Umgebung die Dokumentation für Ihre Quelle erstellen und eine Pull-Anfrage (PR) senden.
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 5%

---

# Verwenden eines Texteditors in Ihrer lokalen Umgebung, um die Seite mit der Quellendokumentation zu erstellen.

In diesem Dokument wird beschrieben, wie Sie mit Ihrer lokalen Umgebung die Dokumentation für Ihre Quelle erstellen und eine Pull-Anfrage (PR) senden.

>[!TIP]
>
>Die folgenden Dokumente aus dem Adobe Contributing Guide können verwendet werden, um Ihren Dokumentationsprozess weiter zu unterstützen: <ul><li>[Installieren von Git- und Markdown-Authoring-Tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Richten Sie das Git-Repository zur Dokumentation lokal ein](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[GitHub-Beitrags-Workflow für wichtige Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Voraussetzungen

Für das folgende Tutorial muss GitHub Desktop auf Ihrem lokalen Computer installiert sein. Wenn Sie keinen GitHub-Desktop haben, können Sie die Anwendung ([) ](https://desktop.github.com/).

## Verbinden mit GitHub und Einrichten der lokalen Authoring-Umgebung

Der erste Schritt beim Einrichten Ihrer lokalen Authoring-Umgebung besteht darin, zum [Adobe Experience Platform GitHub-Repository zu ](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Wählen Sie auf der Hauptseite des Experience Platform GitHub-Repositorys **Verzweigung** aus.

![Verzweigung](../assets/fork.png)

Um das Repository auf Ihren lokalen Computer zu klonen, wählen Sie **Code** aus. Wählen Sie aus dem angezeigten Dropdown-Menü **HTTPS** und klicken Sie dann auf **Mit GitHub Desktop öffnen**.

>[!TIP]
>
>Weitere Informationen finden Sie im Tutorial zum [Einrichten eines lokalen Git-Repositorys für die -Dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Warten Sie als Nächstes einige Augenblicke, bis GitHub Desktop das `experience-platform.en`-Repository geklont hat.

![Klonen](../assets/cloning.png)

Sobald der Klonvorgang abgeschlossen ist, gehen Sie zu GitHub Desktop , um eine neue Verzweigung zu erstellen. Wählen Sie **oberen Navigationsbereich die Option** Master“ und dann **Neue Verzweigung**

![neuer Zweig](../assets/new-branch.png)

Geben Sie im angezeigten Popup-Fenster einen beschreibenden Namen für Ihre Verzweigung ein und wählen Sie dann **Verzweigung erstellen** aus.

![create-branch-vs](../assets/create-branch-vs.png)

Wählen Sie als Nächstes **Verzweigung veröffentlichen**.

![publish-branch](../assets/publish-branch.png)

## Erstellen der Dokumentationsseite für Ihre Quelle

Nachdem das Repository auf den lokalen Computer geklont und eine neue Verzweigung erstellt wurde, können Sie jetzt mit dem Erstellen der Dokumentationsseite für Ihre neue Quelle über den [Texteditor Ihrer Wahl](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors) beginnen.

Adobe empfiehlt die Verwendung von [Visual Studio Code](https://code.visualstudio.com/) und die Installation der Adobe Markdown Authoring-Erweiterung. Um die Erweiterung zu installieren, starten Sie Visual Studio Code, und wählen Sie dann im linken Navigationsbereich **Registerkarte** Erweiterungen“ aus.

![-Erweiterung ](../assets/extension.png)

Geben Sie als Nächstes `Adobe Markdown Authoring` in die Suchleiste ein und wählen Sie dann auf der **Seite die Option** Installieren“ aus.

![Installieren](../assets/install.png)

Wenn Ihr lokaler Computer bereit ist, laden Sie die [Quelldokumentationsvorlage](../assets/api-template.zip) herunter und extrahieren Sie die Datei, um mit [`...`] zu `experience-platform.en/help/sources/tutorials/api/create/...`, die die Kategorie Ihrer Wahl darstellt. Wenn Sie beispielsweise eine Datenbankquelle erstellen, wählen Sie den Datenbankordner aus.

Befolgen Sie abschließend die auf der Vorlage beschriebenen Anweisungen und bearbeiten Sie die Vorlage mit den relevanten Informationen zu Ihrer Quelle.

![edit-template](../assets/edit-template.png)

## Reichen Sie Ihre Dokumentation zur Überprüfung ein

Um eine Pull-Anfrage (PR) zu erstellen und Ihre Dokumentation zur Überprüfung zu senden, speichern Sie zunächst Ihre Arbeit in [!DNL Visual Studio Code] (oder in Ihrem ausgewählten Texteditor). Geben Sie als Nächstes mithilfe von GitHub Desktop eine Commit-Nachricht ein und wählen Sie **Commit an create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

Wählen Sie als Nächstes **Push-Herkunft** aus, um Ihre Arbeit in die Remote-Verzweigung hochzuladen.

![push-origin](../assets/push-origin.png)

Um eine Pull-Anfrage zu erstellen, wählen Sie **Pull-Anfrage erstellen** aus.

![create-pr-vs](../assets/create-pr-vs.png)

Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie der PR einen Hinweis hinzu, der Ihre Aktualisierung beschreibt, und wählen Sie dann **Pull-Anfrage erstellen** aus. Dadurch wird ein PR geöffnet, in dem der Arbeitszweig Ihrer Arbeit mit dem Hauptzweig des Adobe-Repositorys zusammengeführt wird.

>[!TIP]
>
>Lassen Sie das **Bearbeitung durch Betreuer zulassen** aktiviert, um sicherzustellen, dass das Dokumentations-Team von Adobe Änderungen am PR vornehmen kann.

![create-pr](../assets/create-pr.png)

Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die Registerkarte Pull-Anforderungen in https://github.com/AdobeDocs/experience-platform.en überprüfen.

![confirm-pr](../assets/confirm-pr.png)
