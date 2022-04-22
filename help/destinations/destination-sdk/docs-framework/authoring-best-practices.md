---
title: Best Practices für die Inhaltserstellung
description: Erfahren Sie, welche Regeln und Tipps Sie beim Verfassen Ihrer Zieldokumentationsseite befolgen sollten, um sicherzustellen, dass sie den Qualitätsstandards der Adobe Experience Platform-Dokumentation entspricht.
source-git-commit: 35e5c388e9572a3b27ec4bce55e766725936eda4
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Best Practices für die Inhaltserstellung

## Übersicht {#overview}

Auf dieser Seite werden die Regeln beschrieben, die Sie bei [Erstellen der Zieldokumentation](./documentation-instructions.md) , um sicherzustellen, dass die Seite den Qualitätsstandards der Adobe Experience Platform-Dokumentation entspricht.

## Allgemeine Leitlinien {#general-guidance}

* Beim Ausfüllen der [template](./self-service-template.md) Informationen zu Ihrer Zieldokumentation finden Sie im Adobe Contributor Guide , um mehr über [Verknüpfung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [Tabellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), die [unterstützte Markdown-Syntax](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [Schreibanleitung](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)und mehr.
* Fügen Sie in der Produktdokumentation keine Beobachtungen und Schätzungen hinzu.
* In der Experience Platform-Dokumentation verwenden Adobe-Autoren **Fettformatierung** , um auf Steuerelemente der Benutzeroberfläche zu verweisen, wie in diesem Beispiel:
   * Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die **[!UICONTROL Katalog]** Registerkarte. Ein Beispiel dafür anzeigen, wie Steuerelemente der Benutzeroberfläche in einer [Tutorial zu Zielen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Verlinken {#linking}

Befolgen Sie die bereitgestellte Dokumentationsvorlage und bearbeiten Sie nicht die vorhandenen Links in der Vorlage. Lesen Sie beim Einschließen neuer Links [Links in der Dokumentation verwenden](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) im Mitarbeiter-Handbuch.

## Branding-Richtlinien {#branding}

* AEP ist kein anerkannter Begriff für die Öffentlichkeit. Verwenden Sie Adobe Experience Platform zuerst, dann Experience Platform und dann Platform.
   * **Verwenden Sie nicht**: Bevor Sie Daten aus AEP nach YourDestination exportieren können, sollten Sie diese Voraussetzungen unbedingt lesen und erfüllen.
   * **Verwendung**: Bevor Sie Daten aus Adobe Experience Platform nach YourDestination exportieren können, sollten Sie diese Voraussetzungen unbedingt lesen und erfüllen.

## Bilder und Screenshots {#images-and-screenshots}

* Informationen über [Verknüpfen mit Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), siehe Mitarbeiter-Handbuch.
* Stellen Sie bei der Verwendung von Screenshots sicher, dass Ihr Screenshot den gesamten Bildschirm der Platform-Benutzeroberfläche erfasst.
* Wenn Sie Bilder markieren, um ein bestimmtes Steuerelement oder eine bestimmte Beschriftung auf der Seite hervorzuheben, versuchen Sie, den vom Dokumentationsteam der Experience Platform verwendeten Markup-Stil zu befolgen. Beachten Sie, wie profilbasiert hervorgehoben wird in [dieser Screenshot](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Verwenden Sie `png` Bilder formatieren.
* Verwenden Sie keine nummerierten Screenshots als Dateinamen. Bilddateinamen sollten beschreibend sein.
   * **Verwenden Sie nicht**: `1.png`, `2.png`, `3.png`
   * **Verwenden Sie**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Verwenden Sie ALT-Text für alle Bilder, die Sie zur Dokumentation hinzufügen, und verwenden Sie die richtige Grammatik im ALT-Text.
   * **Verwenden Sie nicht**: Details zur Zielverbindung
   * **Verwendung**: Bild der Platform-Benutzeroberfläche mit ausgefüllten Details zur Zielverbindung

## Prozess {#process}

* Die [Dokumentationsvorlage](./self-service-template.md) selten aktualisiert wird, basierend auf dem Partner-Feedback. Bevor Sie mit der Erstellung der Dokumentation für Ihr Ziel beginnen, stellen Sie sicher, dass Sie die [aktuelle Version der Vorlage](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Erstellen Sie die Dokumentation und erstellen Sie die Dokumentation Pull Request (PR) aus einer Verzweigung in Ihrer Abspaltung. *andere als die Hauptzweig*. Lesen Sie beim Bearbeiten im Abschnitt Senden des Ziels für Überprüfung den Abschnitt . [GitHub-Benutzeroberfläche](./use-github-interface-to-create-documentation.md#submit-review) oder [Ihre lokale Umgebung](./work-in-local-environment.md#submit-review).