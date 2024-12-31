---
title: Dokumentieren des Ziels in Adobe Experience Platform
description: Schrittweise Anleitungen zum Erstellen einer Dokumentationsseite für Ihr Ziel in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 8%

---

# Dokumentieren des Ziels in Adobe Experience Platform

>[!IMPORTANT]
>
>Der hier dokumentierte Prozess ist nur für Partner erforderlich, die produktbezogene (öffentliche) Ziele einreichen. Wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen, müssen Sie keine Dokumentation für Ihr Ziel erstellen und veröffentlichen.

## Übersicht {#overview}

Willkommen in Adobe Experience Platform, schön, Sie hier zu haben!
Die Dokumentation Ihres Ziels ist der letzte Schritt, bevor es in Adobe Experience Platform live geschaltet werden kann.

Dieser Dokumentationsabschnitt enthält:

* Schrittweise Anweisungen zum Erstellen einer Dokumentationsseite für Ihr neues Ziel.
* Eine Vorlage, die Sie für Ihr Ziel ausfüllen können;
* [Allgemeine Anweisungen zur Verwendung von Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Spezifische Anweisungen für das Adobe-Markdown-](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (das Adobe-Markdown-Format ist dem normalen Markdown sehr ähnlich).
* Eine [Best Practices-Seite](./authoring-best-practices.md) die Ihnen beim Erstellen einer Dokumentationsseite für Ihre Zielseite hilft, die den Qualitätsstandards der Experience Platform-Dokumentation entspricht.

## Voraussetzungen {#prerequisites}

Um eine Dokumentation für Ihr Ziel gemäß den Anweisungen in diesem Artikel zu erstellen, sind die folgenden Elemente erforderlich:

* **Ein GitHub-**. Melden Sie sich für [GitHub](https://github.com/) an, wenn Sie noch kein Konto haben.
* **GitHub-Desktop**. Wenn Sie sich für [Erstellen der Dokumentation in Ihrer lokalen Umgebung](./work-in-local-environment.md) entscheiden, müssen Sie [GitHub Desktop](https://desktop.github.com/) verwenden.
* Ihre Integration mit Adobe muss sich in einer Testphase befinden, wobei Ihr Ziel in einer Staging-Umgebung in Adobe Experience Platform bereitgestellt wird.

## Allgemeine Anweisungen zum Erstellen der Dokumentation für Ihr Ziel in Adobe Experience Platform {#high-level-instructions}

Um eine Dokumentation für Ihr Ziel zu erstellen, müssen Sie [eine Abspaltung erstellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) des Adobe Experience Platform-Dokumentations-Repositorys und die [bereitgestellte Dokumentationsvorlage](./self-service-template.md) in einer neuen Verzweigung bearbeiten. Verwenden Sie die von der Adobe bereitgestellte Vorlage, um eine neue Zielseite zu erstellen. Öffnen Sie eine Pull-Anfrage (PR), wenn Sie bereit sind. Anweisungen dazu finden Sie weiter unten unter [Schritte zum Erstellen Ihrer neuen Zielseite](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Dokumentationsvorlage {#documentation-template}

Um Sie bei der Erstellung Ihrer Dokumentationsseite zu unterstützen, hat Adobe eine [Dokumentationsvorlage](./self-service-template.md) für Sie vorbefüllt. Weiter unten finden Sie Anweisungen, wie Sie die Vorlage bearbeiten und eine Pull-Anfrage öffnen. Das Adobe-Dokumentations-Team überprüft und veröffentlicht die Dokumentation für Ihr neues Ziel.

[Laden Sie hier die Vorlage herunter](../assets/docs-framework/yourdestination-template.zip) und entpacken Sie die Datei, um die `yourdestination.md`-Datei zu extrahieren.

Anweisungen zur Verwendung der Vorlage zum Erstellen Ihrer Dokumentationsseite finden Sie weiter unten.

## Schritte zum Erstellen der neuen Zielseite {#steps-to-create-docs-page}

Sie können die GitHub-Web-Benutzeroberfläche oder Ihre lokale Umgebung verwenden, um Dokumentation für Ihr neues Ziel in Adobe Experience Platform zu erstellen. Anweisungen für beide Optionen finden Sie in den folgenden Links:

* [Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen](./use-github-interface-to-create-documentation.md)
* [Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen](./work-in-local-environment.md)

## Best Practices {#best-practices}

Lesen Sie die [Best Practices zum Authoring](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md), bevor und während Sie die Zieldokumentationsseite erstellen. Lesen Sie auch die [Schreibanleitung für die Adobe-Dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html), um einige weitere Tipps zu erhalten, die das Adobe-Dokumentations-Team beim Verfassen der Dokumentation verwendet.