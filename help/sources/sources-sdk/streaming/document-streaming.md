---
title: Dokumentieren der Source (Streaming-SDK)
description: Der letzte Schritt, bevor Ihre neue Quelle in Adobe Experience Platform live geschaltet werden kann, besteht darin, Ihre neue Quelle zu dokumentieren.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# Dokumentieren einer Quelle (Streaming-SDK)

>[!NOTE]
>
>Selbstbedienungsquellen-Streaming SDK befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Der letzte Schritt, bevor Ihre neue Quelle in Adobe Experience Platform live geschaltet werden kann, besteht darin, Ihre neue Quelle zu dokumentieren.

Dieses Dokumentationshandbuch umfasst:

* Ein Tutorial, dem Sie folgen können, um eine Dokumentationsseite für Ihre neue Quelle zu erstellen;
* Eine Dokumentationsvorlage, die Sie für Ihre neue Quelle ausfüllen können;
* [Anweisungen zur Verwendung von Markdown zum Schreiben technischer Dokumentationen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Anleitung zum Verstehen der Adobe-Markdown-Variante](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Voraussetzungen

Die folgenden Elemente sind erforderlich, bevor Sie mit der Dokumentation Ihrer neuen Quelle beginnen können:

* **Ein gültiges GitHub-Benutzerkonto**: Wenn Sie noch kein GitHub-Konto haben, müssen Sie eines über die [GitHub-Anmeldeseite](https://github.com/) erstellen;
* **Zugriff auf GitHub Desktop**: Sie müssen die [GitHub Desktop App](https://desktop.github.com/) verwenden, um Ihre Quelldokumentation in Ihrer lokalen Umgebung zu erstellen;
* Ihre Integration mit Adobe muss sich in einer Testphase befinden, während Ihre Quelle in einer Staging-Umgebung in Platform bereitgestellt wird.

## Allgemeine Anweisungen zum Erstellen der Dokumentation für Ihre Quelle in Platform

Um eine Dokumentation für Ihre Quelle zu erstellen, müssen Sie eine Abspaltung des Platform-Dokumentations-Repositorys erstellen und die bereitgestellte Dokumentationsvorlage in einer neuen Verzweigung bearbeiten. Verwenden Sie die von der Adobe bereitgestellte Vorlage, um eine neue Quellseite zu erstellen und eine Pull-Anfrage (PR) zu öffnen, wenn Sie bereit sind. Anweisungen dazu finden Sie weiter unten, in Schritten zum Erstellen Ihrer neuen Quellseite.

## Dokumentationsvorlage

Sie können eine vorausgefüllte [API-Dokumentationsvorlage](streaming-template-api.md) oder die [UI-Dokumentationsvorlage](streaming-template-ui.md) verwenden, um die Erstellung der Dokumentation für Ihre Quelle zu unterstützen. Weiter unten finden Sie Anweisungen zum Bearbeiten der Vorlage und zum Öffnen einer Pull-Anfrage. Die eingereichten Dokumentationen für Ihre neue Quelle werden vom Adobe-Dokumentations-Team geprüft und veröffentlicht.

Sie können auch die folgenden Dokumentationsvorlagen herunterladen:

* [API-Dokumentationsvorlage](../assets/streaming/streaming-template-api.zip)
* [Dokumentationsvorlage für die Benutzeroberfläche](../assets/streaming/streaming-template-ui.zip)

## Neue Quellseite erstellen

Sie können die GitHub-Web-Oberfläche oder Ihre lokale Umgebung verwenden, um Dokumentation für Ihre neue Quelle in Platform zu erstellen. Anweisungen für beide Optionen finden Sie in den folgenden Links:

* [Verwenden der GitHub-Web-Oberfläche zum Erstellen einer Quelldokumentationsseite](../documentation/github.md)
* [Verwenden eines Texteditors in Ihrer lokalen Umgebung, um eine Quelldokumentationsseite zu erstellen](../documentation/text-editor.md)
