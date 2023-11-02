---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Verwenden Sie die GitHub-Webschnittstelle, um eine Quelldokumentationsseite zu erstellen
description: In diesem Dokument erfahren Sie, wie Sie mit der GitHub-Web-Oberfläche die Dokumentation erstellen und eine Pull-Anforderung (PA) senden können.
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 5%

---

# Verwenden Sie die GitHub-Web-Oberfläche, um eine Quelldokumentationsseite zu erstellen

In diesem Dokument erfahren Sie, wie Sie mit der GitHub-Web-Oberfläche die Dokumentation erstellen und eine Pull-Anforderung (PA) senden können.

>[!TIP]
>
>Die folgenden Dokumente aus dem Adobe Contributing Guide können zur weiteren Unterstützung Ihres Dokumentationsprozesses verwendet werden: <ul><li>[Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Lokales Git-Repository für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[GitHub-Beitragsarbeitsablauf für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## GitHub-Umgebung einrichten

Der erste Schritt bei der Einrichtung Ihrer GitHub-Umgebung besteht darin, zur [Adobe Experience Platform GitHub-Repository](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Wählen Sie als Nächstes **Verzweigung**.

![Abspaltung](../assets/fork.png)

Nachdem die Verzweigung abgeschlossen ist, wählen Sie **master** und geben Sie im angezeigten Dropdown-Menü einen Namen für die neue Verzweigung ein. Stellen Sie sicher, dass Sie einen beschreibenden Namen für Ihre Verzweigung angeben, da dieser für Ihre Arbeit verwendet wird, und wählen Sie dann **Zweig erstellen**.

![create-branch](../assets/create-branch.png)

Navigieren Sie in der GitHub-Ordnerstruktur Ihres abgespalteten Repositorys zu [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) und wählen Sie dann die gewünschte Kategorie für Ihre Quelle aus der Liste aus. Wenn Sie beispielsweise die Dokumentation für eine neue CRM-Quelle erstellen, wählen Sie **crm**.

>[!TIP]
>
>Wenn Sie die Dokumentation für die Benutzeroberfläche erstellen, navigieren Sie zu [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) und wählen Sie die entsprechende Kategorie für Ihre Quelle aus. Navigieren Sie zum Hinzufügen Ihrer Bilder zu [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) Fügen Sie dann Ihre Screenshots zum `sdk` Ordner.

![crm](../assets/crm.png)

Ein Ordner mit vorhandenen CRM-Quellen wird angezeigt. Um die Dokumentation für eine neue Quelle hinzuzufügen, wählen Sie **Datei hinzufügen** und wählen Sie **Neue Datei erstellen** aus dem angezeigten Dropdown-Menü.

![create-new-file](../assets/create-new-file.png)

Benennen Sie die Quelldatei `YOURSOURCE.md` wobei YOURSOURCE der Name Ihrer Quelle in Platform ist. Wenn Ihr Unternehmen beispielsweise ACME CRM ist, sollte Ihr Dateiname `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Erstellen Sie die Dokumentationsseite für Ihre Quelle.

Um mit der Dokumentation der neuen Quelle zu beginnen, fügen Sie den Inhalt der [Quelldokumentationsvorlage](./template.md) in den GitHub-Web-Editor. Sie können auch die Vorlage herunterladen [here](../assets/api-template.zip).

Nachdem die Vorlage in die GitHub-Web-Editor-Oberfläche kopiert wurde, befolgen Sie die in der Vorlage beschriebenen Anweisungen und bearbeiten Sie die Werte, die relevante Informationen für Ihre Quelle enthalten.

![paste-template](../assets/paste-template.png)

Bestätigen Sie nach Abschluss des Vorgangs die Datei in Ihrer Verzweigung.

![commit](../assets/commit.png)

## Übermitteln der Dokumentation zur Überprüfung

Nachdem die Datei übertragen wurde, können Sie eine Pull-Anfrage (PA) öffnen, um Ihre Arbeitsverzweigung mit der Masterverzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Stellen Sie sicher, dass die Verzweigung, an der Sie gearbeitet haben, ausgewählt ist, und wählen Sie dann **Vergleich und Pull-Anforderung**.

![compare-pr](../assets/compare-pr.png)

Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie einen Hinweis zur PR hinzu, beschreiben Sie Ihr Update und wählen Sie dann **Pull-Anforderung erstellen**. Dadurch wird ein PR-Vorgang zum Zusammenführen der Arbeitsverzweigung Ihrer Arbeit mit der Masterverzweigung des Adobe-Repositorys geöffnet.

>[!TIP]
>
>Lassen Sie die **Zulassen von Änderungen durch Maintainer** aktivieren, um sicherzustellen, dass das Adobe-Dokumentationsteam die PR bearbeiten kann.

![create-pr](../assets/create-pr.png)

An dieser Stelle wird eine Benachrichtigung angezeigt, in der Sie aufgefordert werden, die Lizenzvereinbarung für Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein notwendiger Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anforderung.

Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die Registerkarte &quot;Pull Requests&quot;in https://github.com/AdobeDocs/experience-platform.en überprüfen.

![confirm-pr](../assets/confirm-pr.png)
