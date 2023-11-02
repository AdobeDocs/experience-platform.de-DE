---
title: Best Practices für die Inhaltserstellung
description: Erfahren Sie, welche Regeln und Tipps Sie beim Verfassen Ihrer Zieldokumentationsseite befolgen sollten, um sicherzustellen, dass sie den Qualitätsstandards der Adobe Experience Platform-Dokumentation entspricht.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 89%

---

# Best Practices für die Inhaltserstellung

## Übersicht {#overview}

Auf dieser Seite werden die Regeln beschrieben, die Sie beim [Verfassen Ihrer Zieldokumentation](./documentation-instructions.md) befolgen sollten, um sicherzustellen, dass die Seite den Qualitätsstandards der Adobe Experience Platform-Dokumentation entspricht.

## Allgemeine Leitlinien {#general-guidance}

* Wenn Sie die [Vorlage](./self-service-template.md) für Ihre Zieldokumentation ausfüllen, finden Sie im Adobe Contributor Guide Informationen über [Verknüpfungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [Tabellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), die [unterstützte Markdown-Syntax](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [Schreibanleitungen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) und mehr.
* Fügen Sie in der Produktdokumentation keine Beobachtungen und Schätzungen hinzu.
* In der Experience Platform-Dokumentation verwenden Adobe-Autorinnen und -Autoren **Fettformatierung**, um auf Steuerelemente der Benutzeroberfläche zu verweisen, wie in diesem Beispiel:
   * Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Sehen Sie sich in einem [Tutorial zu Zielen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination) ein Beispiel dafür an, wie die Steuerelemente der Benutzeroberfläche dokumentiert werden.

## Schreibstil

>[!IMPORTANT]
>
>Lesen Sie die [Schreibanleitung für die Adobe-Dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html), bevor Sie mit der Bearbeitung der Zieldokumentationsseite beginnen.

* Halten Sie Ihre Sätze kurz und kommen Sie schnell zur Sache. Wenn Ihr Satz über 20 Wörter lang ist oder mehrere Kommas verwendet, sollten Sie ihn in separate Sätze aufteilen. Sätze mit mehr als 20 Wörtern können für Leserinnen und Leser eine Herausforderung darstellen.
* Seien Sie nicht übertrieben höflich. Vermeiden Sie die Verwendung von „Bitte“ in der technischen Dokumentation.

## Verlinken {#linking}

Befolgen Sie die bereitgestellte Dokumentationsvorlage und bearbeiten Sie nicht die vorhandenen Links in der Vorlage. Was das Einschließen neuer Links betrifft, lesen Sie [Verwenden von Links in der Dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) im Mitarbeiter-Handbuch.

## Branding-Richtlinien {#branding}

* Die Abkürzung AEP ist kein anerkannter Begriff für die Öffentlichkeit. Verwenden Sie vorzugsweise „Adobe Experience Platform“, danach „Experience Platform“ und dann „Platform“.
   * **Verwenden Sie nicht**: Bevor Sie Daten aus AEP an Ihr Ziel exportieren können, sollten Sie diese Voraussetzungen unbedingt lesen und erfüllen.
   * **Verwenden Sie**: Bevor Sie Daten aus Adobe Experience Platform nach YourDestination exportieren können, sollten Sie diese Voraussetzungen unbedingt lesen und erfüllen.

## Bilder und Screenshots {#images-and-screenshots}

* Informationen zum [Verknüpfen mit Bildern](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images)finden Sie im Mitarbeiter-Handbuch.
* Stellen Sie bei der Verwendung von Screenshots sicher, dass Ihr Screenshot den gesamten Bildschirm der Platform-Benutzeroberfläche erfasst.
* Wenn Sie Bilder markieren, um ein bestimmtes Steuerelement oder eine bestimmte Beschriftung auf der Seite hervorzuheben, versuchen Sie, dem gleichen Markierungsstil zu folgen, den das Dokumentations-Team von Experience Platform verwendet. Beachten Sie, wie in [diesem Screenshot](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency) „profilbasiert“ hervorgehoben wird.
* Verwenden Sie Bilder im `png`-Format.
* Verwenden Sie keine nummerierten Screenshots als Dateinamen. Bilddateinamen sollten beschreibend sein.
   * **Verwenden Sie nicht**: `1.png`, `2.png`, `3.png`
   * **Verwenden Sie**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Verwenden Sie ALT-Text für alle Bilder, die Sie zur Dokumentation hinzufügen, und verwenden Sie eine korrekte Grammatik im ALT-Text.
   * **Verwenden Sie nicht**: Details zur Zielverbindung
   * **Verwenden Sie**: Bild der Platform-Benutzeroberfläche mit ausgefüllten Details zur Zielverbindung.

## Prozess {#process}

* Die [Dokumentationsvorlage](./self-service-template.md) wird selten aktualisiert, basierend auf dem Partner-Feedback. Bevor Sie mit der Erstellung der Dokumentation für Ihr Ziel beginnen, stellen Sie sicher, dass Sie die [aktuelle Version der Vorlage](../assets/docs-framework/yourdestination-template.zip) heruntergeladen haben.
* Erstellen Sie die Dokumentation und erstellen Sie die Dokumentation Pull Request (PR) an einer Zweigstelle in Ihrer Abspaltung, *die nicht der Hauptzweig ist*. Lesen Sie beim Bearbeiten in der [GitHub-Benutzeroberfläche](./use-github-interface-to-create-documentation.md#submit-review) oder in [Ihrer lokalen Umgebung](./work-in-local-environment.md#submit-review) den Abschnitt zum Senden eines Ziels für die Überprüfung.
