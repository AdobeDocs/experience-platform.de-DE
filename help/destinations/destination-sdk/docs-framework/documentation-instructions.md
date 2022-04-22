---
title: Dokumentieren des Ziels in Adobe Experience Platform
description: Schrittweise Anleitungen zum Erstellen einer Dokumentationsseite für Ihr Ziel in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: 3c871471802e905b58acf8cd25db6788f49b9e43
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 8%

---

# Dokumentieren des Ziels in Adobe Experience Platform

## Übersicht {#overview}

Willkommen in Adobe Experience Platform, ein tolles Angebot für Sie!
Die Dokumentation Ihres Ziels ist der letzte Schritt, bevor es in Adobe Experience Platform live gesetzt werden kann.

Dieser Dokumentationsabschnitt umfasst:

* Schrittweise Anleitungen zum Erstellen einer Dokumentationsseite für Ihr neues Ziel;
* eine Vorlage, die Sie für Ihr Ziel ausfüllen können;
* [Allgemeine Anweisungen zur Verwendung von Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Spezifische Anweisungen für den Markdown-Geschmack der Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (Der Markdown-Geschmack der Adobe ähnelt dem regulären Markdown sehr.)
* A [Best Practices-Seite](./authoring-best-practices.md) um Ihnen zu helfen, eine Dokumentationsseite für Ihre Zielseite zu erstellen, die den Qualitätsstandards der Experience Platform-Dokumentation entspricht.

## Voraussetzungen {#prerequisites}

Um die Dokumentation für Ihr Ziel gemäß den Anweisungen in diesem Artikel zu erstellen, sind die folgenden Elemente erforderlich:

* **Ein GitHub-Konto**. Registrieren Sie sich für [GitHub](https://github.com/) wenn Sie noch kein Konto haben.
* **GitHub Desktop**. Wenn Sie auswählen, [Erstellen Sie die Dokumentation in Ihrer lokalen Umgebung.](./work-in-local-environment.md), müssen Sie [GitHub Desktop](https://desktop.github.com/).
* Ihre Integration mit Adobe muss sich in einer Testphase befinden, während Ihr Ziel in einer Staging-Umgebung in Adobe Experience Platform bereitgestellt wird.

## Allgemeine Anweisungen zum Erstellen der Dokumentation für Ihr Ziel in Adobe Experience Platform {#high-level-instructions}

Auf einer übergeordneten Ebene müssen Sie zur Erstellung der Dokumentation für Ihr Ziel [eine Abspaltung erstellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) des Adobe Experience Platform-Dokumentations-Repositorys erstellen und die [bereitgestellte Dokumentationsvorlage](./self-service-template.md) in einer neuen Verzweigung. Verwenden Sie die von der Adobe bereitgestellte Vorlage, um eine neue Zielseite zu erstellen. Öffnen Sie eine Pull-Anforderung (PA), wenn Sie bereit sind. Anweisungen hierzu finden Sie weiter unten unter [Schritte zum Erstellen Ihrer neuen Zielseite](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Dokumentationsvorlage {#documentation-template}

Um Sie bei der Erstellung Ihrer Dokumentationsseite zu unterstützen, hat Adobe bereits eine [Dokumentationsvorlage](./self-service-template.md) für Sie. Weiter unten finden Sie Anweisungen zum Bearbeiten der Vorlage und Öffnen einer Pull-Anforderung. Das Dokumentationsteam der Adobe prüft und veröffentlicht die Dokumentation für Ihr neues Ziel.

[Laden Sie die Vorlage hier herunter](assets/yourdestination-template.zip) und entpacken Sie die Datei, um die `yourdestination.md` -Datei.

Anweisungen zur Verwendung der Vorlage zum Erstellen Ihrer Dokumentationsseite finden Sie weiter unten.

## Schritte zum Erstellen Ihrer neuen Zielseite {#steps-to-create-docs-page}

Sie können die GitHub-Webschnittstelle oder Ihre lokale Umgebung verwenden, um eine Dokumentation für Ihr neues Ziel in Adobe Experience Platform zu erstellen. Anweisungen für beide Optionen finden Sie unter den folgenden Links:

* [Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen](./use-github-interface-to-create-documentation.md)
* [Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen](./work-in-local-environment.md)

## Best Practices {#best-practices}

Überprüfen Sie die [Best Practices für die Bearbeitung](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) vor und während Sie die Zieldokumentationsseite erstellen. Lesen Sie auch die [Schreibanleitung für die Dokumentation der Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) für einige weitere Tipps zum Schreiben, die das Dokumentationsteam der Adobe bei der Erstellung der Dokumentation verwendet.