---
title: Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen
description: Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie mit einem Texteditor in Ihrer lokalen Umgebung eine Dokumentationsseite für Ihr Experience Platform-Ziel erstellen und zur Überprüfung senden können.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 6%

---

# Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen {#local-authoring}

Die Anweisungen auf dieser Seite zeigen Ihnen, wie Sie einen Texteditor verwenden können, um in Ihrer lokalen Umgebung Dokumentation zu erstellen und eine Pull-Anforderung (PR) zu senden. Bevor Sie die hier aufgeführten Schritte durchführen, lesen Sie [Dokumentieren Ihres Ziels in Adobe Experience Platform-Zielen](./documentation-instructions.md).

>[!TIP]
>
>Weitere Informationen finden Sie in der entsprechenden Dokumentation im Mitarbeiter-Handbuch der Adobe:
>* [Git- und Markdown-Bearbeitungswerkzeuge installieren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Lokales Git-Repository für Dokumentation einrichten](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [GitHub-Beitragsarbeitsablauf für umfangreiche Änderungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Stellen Sie eine Verbindung zu GitHub her und richten Sie Ihre lokale Authoring-Umgebung ein. {#set-up-environment}

1. Navigieren Sie im Browser zu `https://github.com/AdobeDocs/experience-platform.en`
2. nach [Abspaltung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) Klicken Sie im Repository auf **Verzweigung** wie unten dargestellt. Dadurch wird eine Kopie des Experience Platform-Repositorys in Ihrem eigenen GitHub-Konto erstellt.

   ![Dokumentation zur Adobe von Verzweigungen](../assets/docs-framework/ssd-fork-repository.gif)

3. Repository auf Ihren lokalen Computer klonen. Auswählen **Code > HTTPS > Öffnen mit GitHub Desktop**, wie unten dargestellt. Stellen Sie sicher, dass [GitHub Desktop](https://desktop.github.com/) installiert. Weitere Informationen finden Sie unter [Lokalen Klon des Repositorys erstellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) im Adobe-Contributor-Handbuch.

   ![Adobe-Dokumentations-Repository in lokale Umgebung klonen](../assets/docs-framework/clone-local.png)

4. Navigieren Sie in der lokalen Dateistruktur zu `experience-platform.en/help/destinations/catalog/[...]`, wobei `[...]` ist die gewünschte Kategorie für Ihr Ziel. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die `personalization` Ordner.

## Dokumentationsseite für Ihr Ziel erstellen {#author-documentation}

1. Ihre Dokumentationsseite basiert auf der [Self-Service-Zielvorlage](../docs-framework/self-service-template.md). Laden Sie die [Zielvorlage](../assets/docs-framework/yourdestination-template.zip). Entpacken Sie es und extrahieren Sie die Datei `yourdestination-template.md` in den in Schritt 4 genannten Ordner.  Datei umbenennen `YOURDESTINATION.md`, wobei YOURDESTINATION der Name Ihres Ziels in Adobe Experience Platform ist. Wenn Ihr Unternehmen beispielsweise Moviestar heißt, geben Sie Ihrer Datei einen Namen `moviestar.md`.
2. Öffnen Sie die neue Datei in [Texteditor der Wahl](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe empfiehlt die Verwendung von [Visual Studio-Code](https://code.visualstudio.com/) und installieren Sie die Adobe Markdown Authoring-Erweiterung. Um die Erweiterung zu installieren, öffnen Sie Visual Studio Code und wählen Sie die **[!DNL Extensions]** auf der linken Bildschirmseite nach `adobe markdown authoring`. Wählen Sie die Erweiterung aus und klicken Sie auf **[!DNL Install]**.
   ![Installieren der Adobe Markdown Authoring-Erweiterung](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Bearbeiten Sie die Vorlage mit relevanten Informationen für Ihr Ziel. Befolgen Sie die Anweisungen in der Vorlage.
4. Screenshots oder Bilder, die Sie Ihrer Dokumentation hinzufügen möchten, finden Sie unter `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, wobei `[...]` ist die gewünschte Kategorie für Ihr Ziel. Wenn Sie beispielsweise ein Personalisierungsziel zu Experience Platform hinzufügen, wählen Sie die `personalization` Ordner. Erstellen Sie einen neuen Ordner für Ihr Ziel und speichern Sie Ihre Bilder hier. Sie müssen auf der Seite, die Sie erstellen, eine Verknüpfung zu ihnen herstellen. Siehe [Anweisungen zum Verknüpfen von Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Wenn Sie bereit sind, speichern Sie die Datei, an der Sie arbeiten.

## Übermitteln der Dokumentation zur Überprüfung {#submit-review}

>[!TIP]
>
>Beachten Sie, dass hier nichts kaputt gemacht werden kann. Indem Sie den Anweisungen in diesem Abschnitt folgen, schlagen Sie einfach eine Aktualisierung der Dokumentation vor. Ihre vorgeschlagene Aktualisierung wird vom Dokumentationsteam von Adobe Experience Platform genehmigt oder bearbeitet.

1. Erstellen Sie in GitHub Desktop eine Arbeitsverzweigung für Ihre Aktualisierungen und wählen Sie **Veröffentlichungsverzweigung** , um die Verzweigung in GitHub zu veröffentlichen.

![Neuer lokaler Zweig](../assets/docs-framework/new-branch-local.gif)

1. In GitHub Desktop [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) Ihre Arbeit, wie unten dargestellt.

   ![Lokal bestätigen](../assets/docs-framework/commit-local.png)

1. In GitHub Desktop [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) Ihre Arbeit [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) -Verzweigung, wie unten dargestellt.

   ![Übertragen](../assets/docs-framework/push-local-to-remote.png)

1. Öffnen Sie in der GitHub-Webschnittstelle eine Pull-Anfrage (PA), um Ihre Arbeitsverzweigung mit der Übergeordneten Verzweigung des Adobe-Dokumentations-Repositorys zusammenzuführen. Vergewissern Sie sich, dass der Zweig, an dem Sie gearbeitet haben, ausgewählt ist, und wählen Sie **Beitragen > Pull-Anforderung öffnen**.

   ![Pull-Anforderung erstellen](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Stellen Sie sicher, dass die Basis- und Vergleichsverzweigungen korrekt sind. Fügen Sie einen Hinweis zur PR hinzu, beschreiben Sie Ihr Update und wählen Sie **Pull-Anforderung erstellen**. Dadurch wird ein PR-Vorgang geöffnet, um die Arbeitsverzweigung Ihrer Verzweigung mit der Übergeordneten Verzweigung des Adobe-Repositorys zusammenzuführen.
   >[!TIP]
   >
   >Lassen Sie die **Zulassen von Änderungen durch Maintainer** aktivieren, damit das Adobe-Dokumentationsteam die PR bearbeiten kann.

   ![Pull-Anforderung zum Adobe-Dokumentations-Repository erstellen](../assets/docs-framework/ssd-create-pull-request-2.png)

1. An dieser Stelle wird eine Benachrichtigung angezeigt, in der Sie aufgefordert werden, die Adobe Contributor License Agreement (CLA) zu unterzeichnen. Dies ist ein notwendiger Schritt. Nachdem Sie die CLA signiert haben, aktualisieren Sie die PR-Seite und senden Sie die Pull-Anforderung.

1. Sie können bestätigen, dass die Pull-Anforderung gesendet wurde, indem Sie die **Pull-Anforderungen** Registerkarte in `https://github.com/AdobeDocs/experience-platform.en`.

![PR erfolgreich](../assets/docs-framework/ssd-pr-successful.png)

1. Vielen Dank! Das Dokumentationsteam der Adobe wird sich in der PR für den Fall, dass Änderungen erforderlich sind, an Sie wenden und Ihnen mitteilen, wann die Dokumentation veröffentlicht wird.

>[!TIP]
>
>Lesen Sie zum Hinzufügen von Bildern und Links zu Ihrer Dokumentation sowie zu allen anderen Fragen rund um Markdown den Abschnitt [Markdown verwenden](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) in der kollaborativen Anleitung der Adobe.
