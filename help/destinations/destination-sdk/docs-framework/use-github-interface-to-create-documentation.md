---
title: 'Verwenden Sie die GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen '
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden können.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: 83539a9aa2fddcae0c9a44302d8bfa9d9f56de0c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Verwenden Sie die GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen {#github-interface}

Die folgenden Anweisungen zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche Dokumentation erstellen und eine Pull-Anforderung (PA) senden können. Bevor Sie die hier angegebenen Schritte durchführen, lesen Sie [Ihr Ziel in Adobe Experience Platform Destinations](./documentation-instructions.md) dokumentieren.

>[!TIP]
>
>Weitere Informationen finden Sie in der entsprechenden Dokumentation im Mitarbeiter-Handbuch der Adobe:
>* [Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Lokales Git-Repository für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [GitHub-Beitragsarbeitsablauf für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## GitHub-Authoring-Umgebung einrichten {#set-up-environment}

1. Navigieren Sie im Browser zu `https://github.com/AdobeDocs/experience-platform.en`.
2. Um das Repository [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) zu verlassen, klicken Sie auf **Fork**, wie in der Abbildung unten dargestellt.

   ![Dokumentation zur Adobe von Verzweigungen](./assets/ssd-fork-repository.gif)

3. Erstellen Sie in Ihrer Abspaltung des Repositorys eine neue Verzweigung für Ihr Projekt, wie unten dargestellt. Verwenden Sie diesen neuen Zweig für Ihre Arbeit.

   ![Neue GitHub-Verzweigung erstellen](./assets/new-branch-github.gif)

4. Navigieren Sie in der GitHub-Ordnerstruktur des abgespalteten Repositorys zu `experience-platform.en/help/destinations/catalog/[...]`, wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Wählen Sie **Datei hinzufügen > Neue Datei erstellen**.

   ![Neue Datei hinzufügen](./assets/github-navigate-and-create-file.gif)

5. Benennen Sie Ihr Ziel `YOURDESTINATION.md`, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihr Unternehmen beispielsweise Moviestar heißt, würden Sie Ihre Datei `moviestar.md` nennen.

## Dokumentationsseite für Ihr Ziel erstellen {#author-documentation}

1. Sie erstellen den Inhalt Ihrer Zielseite basierend auf der [Dokumentations-Self-Service-Vorlage](./self-service-template.md). **[](assets/yourdestination-template.zip)** Laden Sie die Vorlage herunter und dekomprimieren Sie sie, um die  `.md` Dateivorlage zu extrahieren.
2. Fügen Sie den Inhalt der Vorlage ein und bearbeiten Sie ihn mit relevanten Informationen für Ihr Ziel in einem Online-Markdown-Editor, z. B. [dillinger.io](https://dillinger.io/). Folgen Sie den Anweisungen in der Vorlage, um zu erfahren, was Sie ausfüllen und welche Absätze entfernt werden können.

   >[!TIP]
   >
   >Sie können Ihr Browser-Fenster jederzeit schließen und später erneut öffnen. Ihre Arbeit wird automatisch gespeichert und wartet auf Sie, wenn Sie den Browser erneut öffnen.
3. Kopieren Sie den Inhalt aus dem Markdown-Editor in Ihre neue Datei in GitHub.
4. Verwenden Sie für alle Screenshots oder Bilder, die Sie verwenden möchten, die GitHub-Oberfläche, um die Dateien in `experience-platform.en/help/destinations/assets/catalog/[...]` hochzuladen, wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Sie müssen eine Verknüpfung zu den Bildern der Seite herstellen, die Sie erstellen. Siehe [Anweisungen zum Verknüpfen von Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Bild in GitHub hochladen](./assets/upload-image.gif)

5. Wenn Sie bereit sind, speichern Sie die Datei in Ihrer Verzweigung.

![Dateierstellung bestätigen](./assets/ssd-confirm-file-creation.png)

## Übermitteln der Dokumentation zur Überprüfung {#submit-review}

>[!TIP]
>
>Beachten Sie, dass hier nichts kaputt gemacht werden kann. Indem Sie den Anweisungen in diesem Abschnitt folgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Ihre vorgeschlagene Aktualisierung wird vom Dokumentationsteam von Adobe Experience Platform genehmigt oder bearbeitet.

1. Nachdem Sie die Datei gespeichert und die gewünschten Bilder hochgeladen haben, können Sie eine Pull-Anfrage (PA) öffnen, um Ihre Arbeitsverzweigung in die Übergeordnete Verzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Vergewissern Sie sich, dass die Verzweigung, an der Sie gearbeitet haben, ausgewählt ist, und wählen Sie **Contribute > Pull request**.

![Pull-Anforderung erstellen](./assets/ssd-create-pull-request-1.gif)

1. Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie der PA einen Hinweis hinzu, beschreiben Sie Ihre Aktualisierung und wählen Sie **Pull-Anforderung erstellen** aus. Dadurch wird ein PR-Vorgang geöffnet, um die Arbeitsverzweigung Ihrer Verzweigung mit der Übergeordneten Verzweigung des Adobe-Repositorys zusammenzuführen.

   >[!TIP]
   >
   >Lassen Sie das Kontrollkästchen **Bearbeitungen durch Betreuer zulassen** aktiviert, damit das Adobe-Dokumentationsteam Änderungen an der PA vornehmen kann.

   ![Pull-Anforderung zum Adobe-Dokumentations-Repository erstellen](./assets/ssd-create-pull-request-2.png)

1. An dieser Stelle wird eine Benachrichtigung angezeigt, in der Sie aufgefordert werden, die Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein notwendiger Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anforderung.

1. Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die Registerkarte **Pull Requests** in `https://github.com/AdobeDocs/experience-platform.en` überprüfen.

   ![PR erfolgreich](./assets/ssd-pr-successful.png)

1. Vielen Dank! Das Dokumentationsteam der Adobe wird sich in der PR für den Fall, dass Änderungen erforderlich sind, an Sie wenden und Ihnen mitteilen, wann die Dokumentation veröffentlicht wird.

>[!TIP]
>
>Um Bilder und Links zu Ihrer Dokumentation hinzuzufügen und weitere Fragen rund um Markdown zu beantworten, lesen Sie [Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) im kollaborativen Schreibleitfaden der Adobe.
