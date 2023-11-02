---
title: Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden können.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 5%

---

# Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen {#github-interface}

Die folgenden Anweisungen zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche Dokumentation erstellen und eine Pull-Anforderung (PA) senden können. Bevor Sie die hier aufgeführten Schritte durchführen, lesen Sie [Dokumentieren Ihres Ziels in Adobe Experience Platform-Zielen](./documentation-instructions.md).

>[!TIP]
>
>Weitere Informationen finden Sie in der unterstützenden Dokumentation im Adobe Contributor Guide:
>* [Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Lokales Git-Repository für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [GitHub-Beitragsarbeitsablauf für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## GitHub-Authoring-Umgebung einrichten {#set-up-environment}

1. Navigieren Sie im Browser zu `https://github.com/AdobeDocs/experience-platform.en`.
2. nach [Abspaltung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) Klicken Sie im Repository auf **Verzweigung** wie unten dargestellt. Dadurch wird eine Kopie des Experience Platform-Repositorys in Ihrem eigenen GitHub-Konto erstellt.

   ![Adobe-Dokumentations-Repository für Verzweigungen](../assets/docs-framework/ssd-fork-repository.gif)

3. Erstellen Sie in Ihrer Abspaltung des Repositorys eine neue Verzweigung für Ihr Projekt, wie unten dargestellt. Verwenden Sie diese neue Verzweigung für Ihre Arbeit.

   ![Neue GitHub-Verzweigung erstellen](../assets/docs-framework/new-branch-github.gif)

4. Navigieren Sie in der GitHub-Ordnerstruktur des abgespalteten Repositorys zu `experience-platform.en/help/destinations/catalog/[...]`, wobei `[...]` ist die gewünschte Kategorie für Ihr Ziel. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die `personalization` Kategorie. Auswählen **Datei hinzufügen > Neue Datei erstellen**.

   ![Neue Datei hinzufügen](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Benennen Sie Ihr Ziel `YOURDESTINATION.md`, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihr Unternehmen beispielsweise Moviestar heißt, geben Sie Ihrer Datei einen Namen `moviestar.md`.

## Dokumentationsseite für Ihr Ziel erstellen {#author-documentation}

1. Sie erstellen den Inhalt Ihrer Zielseite basierend auf dem [Dokumentation-Self-Service-Vorlage](./self-service-template.md). **[Herunterladen](../assets/docs-framework/yourdestination-template.zip)** die Vorlage und entpacken sie, um die `.md` Dateivorlage.
2. Fügen Sie den Inhalt der Vorlage mit relevanten Informationen für Ihr Ziel in einen Online-Markdown-Editor ein, z. B. [dillinger.io](https://dillinger.io/). Folgen Sie den Anweisungen in der Vorlage, um zu erfahren, was Sie ausfüllen und welche Absätze entfernt werden können.

   >[!TIP]
   >
   >Sie können Ihr Browser-Fenster jederzeit schließen und später erneut öffnen. Ihre Arbeit wird automatisch gespeichert und wartet auf Sie, wenn Sie den Browser erneut öffnen.
3. Kopieren Sie den Inhalt aus dem Markdown-Editor in Ihre neue Datei in GitHub.
4. Verwenden Sie für alle Screenshots oder Bilder, die Sie verwenden möchten, die GitHub-Oberfläche, um die Dateien in `experience-platform.en/help/destinations/assets/catalog/[...]`, wobei `[...]` ist die gewünschte Kategorie für Ihr Ziel. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die `personalization` Kategorie. Sie müssen eine Verknüpfung zu den Bildern der Seite herstellen, die Sie erstellen. Siehe [Anweisungen zum Verknüpfen von Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Bild in GitHub hochladen](../assets/docs-framework/upload-image.gif)

5. Wenn Sie bereit sind, speichern Sie die Datei in Ihrer Verzweigung.

![Dateierstellung bestätigen](../assets/docs-framework/ssd-confirm-file-creation.png)

## Übermitteln der Dokumentation zur Überprüfung {#submit-review}

>[!TIP]
>
>Beachten Sie, dass hier nichts kaputt gemacht werden kann. Indem Sie den Anweisungen in diesem Abschnitt folgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Ihre vorgeschlagene Aktualisierung wird vom Dokumentationsteam von Adobe Experience Platform genehmigt oder bearbeitet.

1. Nachdem Sie die Datei gespeichert und die gewünschten Bilder hochgeladen haben, können Sie eine Pull-Anforderung (PA) öffnen, um Ihre Arbeitsverzweigung mit der Masterverzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Stellen Sie sicher, dass der Zweig, an dem Sie gearbeitet haben, ausgewählt ist, und wählen Sie **Beitragen > Pull-Anforderung öffnen**.

![Pull-Anforderung erstellen](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie einen Hinweis zur PR hinzu, beschreiben Sie Ihr Update und wählen Sie **Pull-Anforderung erstellen**. Dadurch wird ein PR-Vorgang zum Zusammenführen der Arbeitsverzweigung Ihrer Verzweigung mit der Masterverzweigung des Adobe-Repositorys geöffnet.

   >[!TIP]
   >
   >Lassen Sie die **Zulassen von Änderungen durch Maintainer** aktivieren, damit das Adobe-Dokumentationsteam die PR bearbeiten kann.

   ![Pull-Anforderung zum Adobe-Dokumentations-Repository erstellen](../assets/docs-framework/ssd-create-pull-request-2.png)

1. An dieser Stelle wird eine Benachrichtigung angezeigt, in der Sie aufgefordert werden, die Lizenzvereinbarung für Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein notwendiger Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anforderung.

1. Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die **Pull-Anforderungen** Registerkarte in `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR erfolgreich](../assets/docs-framework/ssd-pr-successful.png)

1. Vielen Dank! Das Adobe-Dokumentationsteam wird sich in der PR für den Fall, dass Änderungen erforderlich sind, an Sie wenden und Ihnen mitteilen, wann die Dokumentation veröffentlicht wird.

>[!TIP]
>
>Lesen Sie zum Hinzufügen von Bildern und Links zu Ihrer Dokumentation sowie zu allen anderen Fragen rund um Markdown den Abschnitt [Markdown verwenden](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) In Adobe haben wir gemeinsam eine Anleitung zum Schreiben erhalten.
