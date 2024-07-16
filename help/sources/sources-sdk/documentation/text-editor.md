---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Verwenden Sie einen Texteditor in Ihrer lokalen Umgebung, um eine Seite mit der Quellendokumentation zu erstellen.
description: In diesem Dokument erfahren Sie, wie Sie mit Ihrer lokalen Umgebung die Dokumentation für Ihre Quelle erstellen und eine Pull-Anforderung (PA) senden können.
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Verwenden eines Texteditors in Ihrer lokalen Umgebung, um die Seite mit der Quellendokumentation zu erstellen.

In diesem Dokument erfahren Sie, wie Sie mit Ihrer lokalen Umgebung die Dokumentation für Ihre Quelle erstellen und eine Pull-Anforderung (PA) senden können.

>[!TIP]
>
>Die folgenden Dokumente aus dem Adobe Contributing Guide können zur weiteren Unterstützung Ihres Dokumentationsprozesses verwendet werden: <ul><li>[Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[ Git-Repository lokal für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Arbeitsablauf für GitHub-Beiträge für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Voraussetzungen

Für das folgende Tutorial muss GitHub Desktop auf Ihrem lokalen Computer installiert sein. Wenn Sie nicht über GitHub Desktop verfügen, können Sie die Anwendung [hier](https://desktop.github.com/) herunterladen.

## Stellen Sie eine Verbindung zu GitHub her und richten Sie Ihre lokale Authoring-Umgebung ein.

Der erste Schritt beim Einrichten Ihrer lokalen Authoring-Umgebung besteht darin, zum [Adobe Experience Platform GitHub-Repository](https://github.com/AdobeDocs/experience-platform.en) zu navigieren.

![platform-repo](../assets/platform-repo.png)

Wählen Sie auf der Hauptseite des Platform GitHub-Repositorys **Verzweigung** aus.

![fork](../assets/fork.png)

Um das Repository auf Ihrem lokalen Computer zu klonen, wählen Sie **Code** aus. Wählen Sie im angezeigten Dropdown-Menü **HTTPS** und dann **Mit GitHub Desktop öffnen** aus.

>[!TIP]
>
>Weitere Informationen finden Sie im Tutorial zum [lokalen Einrichten des Git-Repositorys für die Dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Lassen Sie als Nächstes einige Augenblicke zu, bis GitHub Desktop das `experience-platform.en`-Repository klonen kann.

![Klonen](../assets/cloning.png)

Sobald der Klonprozess abgeschlossen ist, wechseln Sie zu GitHub Desktop , um eine neue Verzweigung zu erstellen. Wählen Sie **Master** aus der oberen Navigation und dann **Neuer Zweig** aus.

![new-branch](../assets/new-branch.png)

Geben Sie im angezeigten Popover-Bedienfeld einen beschreibenden Namen für die Verzweigung ein und wählen Sie dann **Verzweigung erstellen** aus.

![create-branch-vs](../assets/create-branch-vs.png)

Wählen Sie als Nächstes **Publish-Verzweigung** aus.

![publish-branch](../assets/publish-branch.png)

## Erstellen Sie die Dokumentationsseite für Ihre Quelle.

Nachdem das Repository auf Ihrem lokalen Computer geklont und eine neue Verzweigung erstellt wurde, können Sie jetzt mit dem Authoring der Dokumentationsseite für Ihre neue Quelle über den [Texteditor Ihrer Wahl](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors) beginnen.

Adobe empfiehlt die Verwendung von [Visual Studio Code](https://code.visualstudio.com/) und die Installation der Adobe Markdown Authoring-Erweiterung. Um die Erweiterung zu installieren, starten Sie Visual Studio Code und wählen Sie dann die Registerkarte **Erweiterungen** im linken Navigationsbereich aus.

![-Erweiterung ](../assets/extension.png)

Geben Sie als Nächstes `Adobe Markdown Authoring` in die Suchleiste ein und wählen Sie dann **Installieren** aus der angezeigten Seite aus.

![install](../assets/install.png)

Laden Sie die Dokumentationsvorlage &quot;[Quellen&quot;](../assets/api-template.zip)&quot;herunter und extrahieren Sie die Datei nach &quot;`experience-platform.en/help/sources/tutorials/api/create/...`&quot;, wobei &quot;[`...`]&quot; der Kategorie Ihrer Wahl entspricht. Wenn Sie beispielsweise eine Datenbankquelle erstellen, wählen Sie den Datenbankordner aus.

Befolgen Sie abschließend die in der Vorlage beschriebenen Anweisungen und bearbeiten Sie die Vorlage mit den entsprechenden Informationen zu Ihrer Quelle.

![edit-template](../assets/edit-template.png)

## Übermitteln der Dokumentation zur Überprüfung

Um eine Pull-Anforderung (PA) zu erstellen und Ihre Dokumentation zur Überprüfung zu übermitteln, speichern Sie zunächst Ihre Arbeit in [!DNL Visual Studio Code] (oder Ihrem ausgewählten Texteditor). Geben Sie als Nächstes mithilfe von GitHub Desktop eine Commit-Meldung ein und wählen Sie **Commit to create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

Wählen Sie als Nächstes **Push origin** aus, um Ihre Arbeit in den Remote-Zweig hochzuladen.

![push-origin](../assets/push-origin.png)

Um eine Pull-Anforderung zu erstellen, wählen Sie **Pull-Anforderung erstellen**.

![create-pr-vs](../assets/create-pr-vs.png)

Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie der PA einen Hinweis hinzu, beschreiben Sie Ihre Aktualisierung und wählen Sie dann **Pull-Anforderung erstellen** aus. Dadurch wird ein PR-Vorgang zum Zusammenführen der Arbeitsverzweigung Ihrer Arbeit mit der Masterverzweigung des Adobe-Repositorys geöffnet.

>[!TIP]
>
>Lassen Sie das Kontrollkästchen **Änderungen durch Betreuer zulassen** aktiviert, um sicherzustellen, dass das Adobe-Dokumentationsteam Änderungen an der PA vornehmen kann.

![create-pr](../assets/create-pr.png)

Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die Registerkarte &quot;Pull Requests&quot;in https://github.com/AdobeDocs/experience-platform.en überprüfen.

![confirm-pr](../assets/confirm-pr.png)
