---
title: Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit einem Texteditor in Ihrer lokalen Umgebung eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden können.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 4%

---

# Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen {#local-authoring}

Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie einen Texteditor verwenden, um in Ihrer lokalen Umgebung zu arbeiten, um Dokumentation zu erstellen und eine Pull-Anfrage (PR) zu senden. Bevor Sie die hier angegebenen Schritte durchlaufen, lesen Sie [Dokumentieren Ihres Ziels in Adobe Experience Platform-Zielen](./documentation-instructions.md).

>[!TIP]
>
>Weitere Informationen finden Sie auch in der unterstützenden Dokumentation im Adobe-Handbuch für Mitwirkende:
>
>* [Installieren von Git- und Markdown-Authoring-Tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Richten Sie das Git-Repository zur Dokumentation lokal ein](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [GitHub-Beitrags-Workflow für wichtige &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Verbinden mit GitHub und Einrichten der lokalen Authoring-Umgebung {#set-up-environment}

1. Navigieren Sie im Browser zu `https://github.com/AdobeDocs/experience-platform.en`
2. Um [Verzweigung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) das Repository anzuzeigen, klicken Sie auf **Verzweigung** wie unten dargestellt. Dadurch wird eine Kopie des Experience Platform-Repositorys in Ihrem eigenen GitHub-Konto erstellt.

   ![Fork Adobe-Dokumentations-Repository](../assets/docs-framework/ssd-fork-repository.gif)

3. Klonen Sie das Repository auf Ihrem lokalen Computer. Wählen Sie **Code > HTTPS > Mit GitHub Desktop öffnen** aus, wie unten dargestellt. Stellen Sie sicher, dass [GitHub Desktop](https://desktop.github.com/) installiert ist. Weitere Informationen finden Sie unter [Erstellen eines lokalen Klons des Repositorys](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository) im Adobe Contributor Guide.

   ![Klonen Sie das Dokumentations-Repository von Adobe in eine lokale Umgebung](../assets/docs-framework/clone-local.png)

4. Navigieren Sie in Ihrer lokalen Dateistruktur zu `experience-platform.en/help/destinations/catalog/[...]` , wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie den Ordner `personalization` aus.

## Erstellen der Dokumentationsseite für Ihr Ziel {#author-documentation}

1. Ihre Dokumentationsseite basiert auf der [Self-Service-Zielvorlage](../docs-framework/self-service-template.md). Laden Sie die [Zielvorlage“ &#x200B;](../assets/docs-framework/yourdestination-template.zip). Entpacken Sie sie und extrahieren Sie die Datei `yourdestination-template.md` in das in Schritt 4 oben erwähnte Verzeichnis.  Benennen Sie die Datei `YOURDESTINATION.md` um, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihre Firma beispielsweise Moviestar heißt, würden Sie Ihre Datei `moviestar.md` nennen.
2. Öffnen Sie die neue Datei in Ihrem [Texteditor Ihrer Wahl](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors). Adobe empfiehlt die Verwendung von [Visual Studio Code](https://code.visualstudio.com/) und die Installation der Adobe Markdown Authoring-Erweiterung. Um die Erweiterung zu installieren, öffnen Sie Visual Studio Code, wählen Sie die Registerkarte **[!DNL Extensions]** auf der linken Seite des Bildschirms aus und suchen Sie nach `adobe markdown authoring`. Wählen Sie die Erweiterung aus und klicken Sie auf **[!DNL Install]**.
   ![Installieren der Adobe Markdown Authoring-Erweiterung](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Bearbeiten Sie die Vorlage mit relevanten Informationen für Ihr Ziel. Befolgen Sie die Anweisungen in der Vorlage.
4. Screenshots oder Bilder, die Sie Ihrer Dokumentation hinzufügen möchten, finden Sie unter `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]` , wobei `[...]` die gewünschte Kategorie für Ihr Ziel ist. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie den Ordner `personalization` aus. Erstellen Sie einen neuen Ordner für Ihr Ziel und speichern Sie Ihre Bilder hier. Sie müssen von der Seite, die Sie erstellen, aus eine Verknüpfung zu ihnen herstellen. Siehe [Anweisungen zum Verknüpfen mit Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).
5. Wenn Sie fertig sind, speichern Sie die Datei, an der Sie arbeiten.

## Reichen Sie Ihre Dokumentation zur Überprüfung ein {#submit-review}

>[!TIP]
>
>Beachten Sie, dass es hier nichts gibt, was Sie brechen können. Wenn Sie die Anweisungen in diesem Abschnitt befolgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Die vorgeschlagene Aktualisierung wird vom Dokumentations-Team von Adobe Experience Platform genehmigt oder bearbeitet.

1. Erstellen Sie in GitHub Desktop eine Arbeitsverzweigung für Ihre Aktualisierungen und wählen Sie **Verzweigung veröffentlichen**, um die Verzweigung in GitHub zu veröffentlichen.

![Neue lokale Verzweigung](../assets/docs-framework/new-branch-local.gif)

1. Führen Sie in GitHub Desktop [Commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) Ihre Arbeit aus, wie unten dargestellt.

   ![Commit lokal](../assets/docs-framework/commit-local.png)

1. Wählen Sie in GitHub Desktop [Push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) Ihre Arbeit in die [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote)-Verzweigung aus, wie unten dargestellt.

   ![Pushen Sie Ihren Commit](../assets/docs-framework/push-local-to-remote.png)

1. Öffnen Sie in der GitHub-Web-Benutzeroberfläche eine Pull Request (PR), um Ihre Arbeitsverzweigung mit der Hauptverzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Stellen Sie sicher, dass die Verzweigung, an der Sie gearbeitet haben, ausgewählt ist und wählen **Beitragen > Pull Request öffnen**.

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
