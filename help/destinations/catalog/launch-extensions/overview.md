---
keywords: Launch-Erweiterungen; Launch-Erweiterung; Launch-Ziele; platform launch-Erweiterungen;platform launch-Erweiterung;platform launch-Ziele
title: Adobe Experience Platform Launch-Erweiterung
description: Adobe Experience Platform Launch markiert die nächste Generation der Funktionen von Adobe für das Tag-Management. Platform Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 20a9103dd96116f3099bccc9eeb678be5ac2bb79
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 48%

---

# Adobe Experience Platform Launch-Erweiterungen

Adobe Experience Platform Launch ist die nächste Generation der Tag-Management-Funktionen von Adobe. Platform
Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.  Platform Launch ist für Adobe Experience Cloud-Kunden als integrierte, Mehrwert bietende Funktion verfügbar.

Eine Einführung in die Funktionen von Experience Platform Launch finden Sie in den folgenden Ressourcen:

- Adobe Experience Platform Launch [documentation](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=de)
- Adobe Experience Platform Launch [Schnellstartvideos](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Beginnen Sie mit [Einführung in Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) und [Übersicht über den Veröffentlichungsprozess](https://helpx.adobe.com/de/analytics/how-to/adobe-launch-publishing-process.html) und fahren Sie dann mit den nächsten Konzepten fort.

## Suchen der Platform launch-Erweiterungen in der Platform-Oberfläche {#how-to-find-extensions-in-interface}

Um die Platform launch-Erweiterungen in der Platform-Oberfläche zu finden, navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** und wählen Sie **[!UICONTROL Erweiterungen]** im Filter **[!UICONTROL Typen]** aus.

![Erweiterungsfilter in der Benutzeroberfläche](../../assets/catalog/launch-extensions/filter.png)

## Funktionsweise von Platform launch-Erweiterungen {#how-extensions-work}

platform launch Extensions leiten Rohdaten von Ereignissen an verschiedene Zieltypen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](../personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](../voice/confirmit-digital-feedback.md).

**Profil-/Segmentexportziele in Adobe Experience Platform erfassen** Ereignisdaten, kombinieren sie mit anderen Datenquellen, wenden die Segmentierung an und exportieren Segmente und qualifizierte Profile in Ziele. Beispiele hierfür sind das [Amazon S3 Cloud-Speicher-Ziel](../cloud-storage/amazon-s3.md) oder das [Google Display &amp; Video 360-Werbeziel](../advertising/google-dv360.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](../../assets/common/launch-and-other-destinations.png)

## Vorteile der Verwendung von Platform launch Extensions {#extensions-benefits}

Adobe Experience Platform Launch ist für Bestandskunden von Experience Cloud kostenlos. platform launch vereinfacht die Tag-Implementierung auf Ihrer Website mithilfe benutzerfreundlicher Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. platform launch hat einen geringen Platzbedarf auf Ihrer Website und ermöglicht Ihnen, Ihre Seiten schnell zu laden.

>[!IMPORTANT]
>
>Sie können zwar keine Segmente für Platform launch-Erweiterungen aktivieren, aber Sie können Regeln einrichten, um Ereignisdaten nur in bestimmten Situationen weiterzuleiten. Weitere Informationen finden Sie unten.

Sie können *Regeln* erstellen, die bestimmen, wann Ereignisdaten an Erweiterungen weitergeleitet werden. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. Weitere Informationen finden Sie unter Regeln in der [Adobe Experience Platform Launch-Dokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Anwendungsbeispiele für Platform launch-Erweiterungen {#extensions-use-cases}

Mit platform launch-Erweiterungen können Sie verschiedene Anwendungsfälle für Kunden erfüllen. Einige Anwendungsbeispiele für die Verwendung von Platform launch-Erweiterungen sind:

- Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
- Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
- Sie können eine Client-seitige Chatbox-App zum richtigen Zeitpunkt aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren, entsprechend den Regeln, die Sie unter Platform launch eingerichtet haben.

## Erweiterungskategorien {#extension-categories}

platform launch-Erweiterungen können in Platform unter die folgenden Kategorien fallen:

- [Werbung](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Daten-Management-Plattform](../data-management/overview.md)
- [E-Mail-Marketing-Ziele ](../email-marketing/overview.md)
- [Personalisierung](../personalization/overview.md)
- [Umfragen](../survey/overview.md)
- [Stimme des Kunden](../voice/overview.md)
