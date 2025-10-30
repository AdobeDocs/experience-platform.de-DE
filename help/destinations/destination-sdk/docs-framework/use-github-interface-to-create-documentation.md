---
title: Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit der GitHub-Web-Benutzeroberfläche eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: ff094c0c2c75e097140626d77478b8da9a7edf04
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 3%

---

# Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen {#github-interface}

Die folgenden Anweisungen zeigen Ihnen, wie Sie die GitHub-Web-Oberfläche verwenden, um Dokumentationen zu erstellen und eine Pull-Anfrage (PR) zu senden. Bevor Sie die hier angegebenen Schritte durchlaufen, lesen Sie [Dokumentieren Ihres Ziels in Adobe Experience Platform-Zielen](./documentation-instructions.md).

>[!TIP]
>
>Weitere Informationen finden Sie auch in der unterstützenden Dokumentation im Adobe-Handbuch für Mitwirkende:
>
>* [Installieren von Git- und Markdown-Authoring-Tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Richten Sie das Git-Repository zur Dokumentation lokal ein](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [GitHub-Beitrags-Workflow für wichtige &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Einrichten der GitHub-Authoring-Umgebung {#set-up-environment}

1. Navigieren Sie im Browser zu `https://github.com/AdobeDocs/experience-platform.en`.
1. Um [Verzweigung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) das Repository anzuzeigen, klicken Sie auf **Verzweigung** wie unten dargestellt. Dadurch wird eine Kopie des Experience Platform-Repositorys in Ihrem eigenen GitHub-Konto erstellt.

   ![Fork Adobe-Dokumentations-Repository](../assets/docs-framework/ssd-fork-repository.gif)

1. Erstellen Sie in Ihrem Abspaltungs-Repository eine neue Verzweigung für Ihr Projekt, wie unten dargestellt. Verwenden Sie diese neue Verzweigung für Ihre Arbeit.

   ![Neue GitHub-Verzweigung erstellen](../assets/docs-framework/new-branch-github.gif)

1. Navigieren Sie in der GitHub-Ordnerstruktur des abgespalteten Repositorys zu `experience-platform.en/help/destinations/catalog/[...]` , wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Wählen Sie **Datei hinzufügen > Neue Datei erstellen**.

   ![Neue Datei hinzufügen](../assets/docs-framework/github-navigate-and-create-file.gif)

1. Benennen Sie Ihr `YOURDESTINATION.md`, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihre Firma beispielsweise Moviestar heißt, würden Sie Ihre Datei `moviestar.md` nennen.

## Erstellen der Dokumentationsseite für Ihr Ziel {#author-documentation}

1. Sie erstellen den Inhalt Ihrer Zielseite basierend auf der [Dokumentations-Self-Service-Vorlage](./self-service-template.md). **[Laden Sie](../assets/docs-framework/yourdestination-template.zip)** Vorlage herunter und entpacken Sie sie, um die `.md` Dateivorlage zu extrahieren.
1. Fügen Sie den Inhalt der Vorlage ein und bearbeiten Sie ihn mit relevanten Informationen für Ihr Ziel in einem Online-Markdown-Editor, z. B. [dillinger.io](https://dillinger.io/). Folgen Sie den Anweisungen in der Vorlage, um zu erfahren, was Sie ausfüllen sollten und welche Absätze entfernt werden können.

   >[!TIP]
   >
   >Sie können Ihr Browser-Fenster jederzeit schließen und später erneut öffnen. Ihre Arbeit wird automatisch gespeichert und wartet auf Sie, wenn Sie den Browser erneut öffnen.
1. Kopieren Sie den Inhalt aus dem Markdown-Editor in Ihre neue Datei in GitHub.
1. Verwenden Sie für alle Screenshots oder Bilder, die Sie verwenden möchten, die GitHub-Oberfläche, um die Dateien in `experience-platform.en/help/destinations/assets/catalog/[...]` hochzuladen, wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die Kategorie `personalization` aus. Sie müssen eine Verknüpfung zu den Bildern auf der Seite herstellen, die Sie gerade bearbeiten. Siehe [Anweisungen zum Verknüpfen mit Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Bild auf GitHub hochladen](../assets/docs-framework/upload-image.gif)

1. Wenn Sie fertig sind, speichern Sie die Datei in Ihrer Verzweigung.

   ![Bestätigen der Dateierstellung](../assets/docs-framework/ssd-confirm-file-creation.png)

## Reichen Sie Ihre Dokumentation zur Überprüfung ein {#submit-review}

>[!TIP]
>
>Beachten Sie, dass es hier nichts gibt, was Sie brechen können. Wenn Sie die Anweisungen in diesem Abschnitt befolgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Die vorgeschlagene Aktualisierung wird vom Dokumentations-Team von Adobe Experience Platform genehmigt oder bearbeitet.

1. Nachdem Sie die Datei gespeichert und die gewünschten Bilder hochgeladen haben, können Sie eine Pull-Anfrage (PR) öffnen, um Ihre Arbeitsverzweigung mit der Hauptverzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Stellen Sie sicher, dass die Verzweigung, an der Sie gearbeitet haben, ausgewählt ist und wählen Sie **Beitragen > Pull Request öffnen**.

   ![Pull-Anfrage erstellen](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie der PR einen Hinweis hinzu, der Ihre Aktualisierung beschreibt, und wählen Sie **Pull-Anfrage erstellen**. Dadurch wird ein PR geöffnet, in dem der Arbeitszweig Ihres Abspaltungs mit dem Hauptzweig des Adobe-Repositorys zusammengeführt wird.

   >[!TIP]
   >
   >Lassen Sie das **Bearbeitung durch Betreuer zulassen** aktiviert, damit das Dokumentations-Team von Adobe Änderungen am PR vornehmen kann.

   ![Erstellen einer Pull-Anfrage an das Dokumentations-Repository von Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. An dieser Stelle wird eine Benachrichtigung angezeigt, die Sie auffordert, die Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein obligatorischer Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anfrage.

1. Sie können bestätigen, dass die Pull-Anfrage gesendet wurde, indem Sie die Registerkarte **Pull-Anfragen** in `https://github.com/AdobeDocs/experience-platform.en` überprüfen.

   ![PR erfolgreich](../assets/docs-framework/ssd-pr-successful.png)

1. Vielen Dank! Das Dokumentations-Team von Adobe wird sich an das PR wenden, falls Änderungen erforderlich sind, und Ihnen mitteilen, wann die Dokumentation veröffentlicht wird.

>[!TIP]
>
>Informationen zum Hinzufügen von Bildern und Links zu Ihrer Dokumentation sowie zu allen anderen Fragen rund um Markdown finden Sie unter [Verwenden von &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)) im Handbuch für gemeinsames Schreiben in Adobe.
