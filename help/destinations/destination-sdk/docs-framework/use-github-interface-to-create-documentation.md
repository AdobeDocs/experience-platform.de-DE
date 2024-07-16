---
title: Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden können.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 3%

---

# Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen {#github-interface}

Die folgenden Anweisungen zeigen Ihnen, wie Sie mit der GitHub-Web-Oberfläche Dokumentation erstellen und eine Pull-Anforderung (PA) senden können. Bevor Sie die hier angegebenen Schritte durchführen, lesen Sie [Ihr Ziel in Adobe Experience Platform-Zielen dokumentieren](./documentation-instructions.md).

>[!TIP]
>
>Weitere Informationen finden Sie in der unterstützenden Dokumentation im Adobe Contributor Guide:
>* [Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [ Git-Repository lokal für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Arbeitsablauf für GitHub-Beiträge für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## GitHub-Authoring-Umgebung einrichten {#set-up-environment}

1. Navigieren Sie in Ihrem Browser zu &quot;`https://github.com/AdobeDocs/experience-platform.en`&quot;.
2. Um das Repository zu [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) zu verzweigen, klicken Sie auf **Verzweigung** , wie unten dargestellt. Dadurch wird eine Kopie des Experience Platform-Repositorys in Ihrem eigenen GitHub-Konto erstellt.

   ![Fork-Adobe-Dokumentations-Repository](../assets/docs-framework/ssd-fork-repository.gif)

3. Erstellen Sie in Ihrer Abspaltung des Repositorys eine neue Verzweigung für Ihr Projekt, wie unten dargestellt. Verwenden Sie diese neue Verzweigung für Ihre Arbeit.

   ![Neue GitHub-Verzweigung erstellen](../assets/docs-framework/new-branch-github.gif)

4. Navigieren Sie in der GitHub-Ordnerstruktur des abgespalteten Repositorys zu &quot;`experience-platform.en/help/destinations/catalog/[...]`&quot;, wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Wählen Sie **Datei hinzufügen > Neue Datei erstellen** aus.

   ![Neue Datei hinzufügen](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Nennen Sie Ihr Ziel &quot;`YOURDESTINATION.md`&quot;, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihr Unternehmen beispielsweise Moviestar heißt, würden Sie Ihre Datei `moviestar.md` nennen.

## Dokumentationsseite für Ihr Ziel erstellen {#author-documentation}

1. Sie erstellen den Inhalt Ihrer Zielseite auf der Grundlage der [Vorlage für die Dokumentations-Selbstbedienung](./self-service-template.md). **[Laden Sie die Vorlage herunter](../assets/docs-framework/yourdestination-template.zip)** und dekomprimieren Sie sie, um die `.md` -Dateivorlage zu extrahieren.
2. Fügen Sie den Inhalt der Vorlage mit relevanten Informationen für Ihr Ziel in einen Online-Markdown-Editor ein, z. B. [dillinger.io](https://dillinger.io/). Folgen Sie den Anweisungen in der Vorlage, um zu erfahren, was Sie ausfüllen und welche Absätze entfernt werden können.

   >[!TIP]
   >
   >Sie können Ihr Browser-Fenster jederzeit schließen und später erneut öffnen. Ihre Arbeit wird automatisch gespeichert und wartet auf Sie, wenn Sie den Browser erneut öffnen.
3. Kopieren Sie den Inhalt aus dem Markdown-Editor in Ihre neue Datei in GitHub.
4. Verwenden Sie für alle Screenshots oder Bilder, die Sie verwenden möchten, die GitHub-Oberfläche, um die Dateien in `experience-platform.en/help/destinations/assets/catalog/[...]` hochzuladen, wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Sie müssen eine Verknüpfung zu den Bildern der Seite herstellen, die Sie erstellen. Siehe [Anweisungen zum Verknüpfen von Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Bild auf GitHub hochladen](../assets/docs-framework/upload-image.gif)

5. Wenn Sie bereit sind, speichern Sie die Datei in Ihrer Verzweigung.

![Dateierstellung bestätigen](../assets/docs-framework/ssd-confirm-file-creation.png)

## Übermitteln der Dokumentation zur Überprüfung {#submit-review}

>[!TIP]
>
>Beachten Sie, dass hier nichts kaputt gemacht werden kann. Indem Sie den Anweisungen in diesem Abschnitt folgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Ihre vorgeschlagene Aktualisierung wird vom Dokumentationsteam von Adobe Experience Platform genehmigt oder bearbeitet.

1. Nachdem Sie die Datei gespeichert und die gewünschten Bilder hochgeladen haben, können Sie eine Pull-Anforderung (PA) öffnen, um Ihre Arbeitsverzweigung mit der Masterverzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Stellen Sie sicher, dass die Verzweigung, an der Sie gearbeitet haben, ausgewählt ist, und wählen Sie **Contribute > Pull-Anforderung öffnen** aus.

![Pull-Anforderung erstellen](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie der PA einen Hinweis hinzu, beschreiben Sie Ihre Aktualisierung und wählen Sie **Pull-Anforderung erstellen** aus. Dadurch wird ein PR-Vorgang zum Zusammenführen der Arbeitsverzweigung Ihrer Verzweigung mit der Masterverzweigung des Adobe-Repositorys geöffnet.

   >[!TIP]
   >
   >Lassen Sie das Kontrollkästchen **Änderungen durch Betreuer zulassen** aktiviert, damit das Adobe-Dokumentationsteam die PR bearbeiten kann.

   ![Pull-Anforderung zum Adobe-Dokumentations-Repository erstellen](../assets/docs-framework/ssd-create-pull-request-2.png)

1. An dieser Stelle wird eine Benachrichtigung angezeigt, in der Sie aufgefordert werden, die Lizenzvereinbarung für Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein notwendiger Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anforderung.

1. Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die Registerkarte **Pull Requests** in `https://github.com/AdobeDocs/experience-platform.en` überprüfen.

   ![PA erfolgreich](../assets/docs-framework/ssd-pr-successful.png)

1. Vielen Dank! Das Adobe-Dokumentationsteam wird sich in der PR für den Fall, dass Änderungen erforderlich sind, an Sie wenden und Ihnen mitteilen, wann die Dokumentation veröffentlicht wird.

>[!TIP]
>
>Lesen Sie zum Hinzufügen von Bildern und Links zu Ihrer Dokumentation sowie zu allen anderen Fragen rund um Markdown den Abschnitt [Verwenden von ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) in der kollaborativen Anleitung zum Schreiben in Adobe Markdown.
