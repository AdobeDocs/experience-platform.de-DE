---
title: Übersicht über die Web SDK JavaScript-Bibliothek
description: Senden von Daten an Adobe Experience Platform Edge Network mithilfe von JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 3%

---

# Übersicht über die Web SDK JavaScript-Bibliothek

Die **Adobe Experience Platform Web SDK** ist eine Client-seitige JavaScript-Bibliothek, mit der Sie Daten an die Adobe Experience Platform Edge Network senden können. In diesem Handbuch wird der Implementierungspfad der Web SDK JavaScript Library (`alloy.js`) dokumentiert, einschließlich der grundlegenden Konzepte, Installation, Konfiguration und Befehle. Informationen zur Web SDK-Tag-Erweiterung in der Datenerfassungs-Benutzeroberfläche finden Sie unter [Web SDK-Tag-Erweiterung](/help/tags/extensions/client/web-sdk/overview.md).

Web SDK sendet Daten lösungsunabhängig (XDM) an Experience Platform Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und in Echtzeit sendet.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network bietet eine Datenerfassung mit niedriger Latenz, Plug-in-Datenverarbeitung und schnelle Datenaktivierung über alle adressierbaren Kanäle hinweg. Sie bietet eine einzige konsolidierte SDK für Web-, Mobil- und Server-seitige Kanäle, die Daten an eine gemeinsame Adobe-Domain (`adobedc.net`) sendet und eine einzige Payload für die Daten- und Erlebnisbereitstellung empfängt.

Auf der Serverseite vereinfachen ein einheitliches Edge-Gateway und ein gemeinsames Plattform-Service-Framework die Bereitstellung neuer Funktionen und bieten gleichzeitig die folgenden Vorteile:

* Verkürzung der Amortisierungszeit für Kunden
* Abschaffung der Notwendigkeit von punktuellen Integrationen;
* Verbesserung der Leistung im Vergleich zu den alten Bibliotheken
* Sinkende Betriebskosten;
* Erhöhung der Innovationsgeschwindigkeit;
* Schaffung nachhaltiger Wettbewerbsvorteile für Adobe-Kunden.

Mit einem konsolidierten Edge-System können Sie Werbe-, Marketing- und Personalisierungskampagnen auf allen Kanälen verwalten. Dies reduziert die Gesamtbetriebskosten und unterstützt verschiedene Datentypen, sodass Sie Ihr Datenmodell für die Verwendung mit mehreren Experience Cloud-Produkten zuordnen können.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch Web SDK ersetzte Bibliotheken {#sdks}

Web SDK ist eine von Grund auf neu erstellte Open-Source-Bibliothek, die Funktionen bestehender Bibliotheken integriert. Es behandelt Probleme mit der Tag-Auslösereihenfolge, Versionsinkonsistenzen und der Abhängigkeitsverwaltung und bietet eine Möglichkeit zur Implementierung vieler Experience Cloud-Produkte. Web SDK ersetzt die Datenerfassung für die folgenden Services:

* Adobe Experience Platform-Besucher-ID-Dienst (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`
* Adobe Target (`AT.js`
* Adobe Audience Manager (`DIL.js`
* Adobe Media Analytics
* Adobe Advertising

Außerdem wird ein neuer Endpunkt eingeführt, der HTTP-Anfragen an Adobe-Lösungen optimiert. Zuvor waren mehrere Aufrufe für jede Datenerfassungsbibliothek erforderlich. Mit einem einzigen Aufruf können Sie nun eine ID abrufen, ein [!DNL Target] Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und Daten an Adobe Experience Platform übergeben.

## Migration von vorhandenen Bibliotheken zu Web SDK {#migrating-to-web-sdk}

Adobe bietet einen optimierten Aktualisierungspfad, um die Migration von einer der vorhandenen Bibliotheken zur Web-SDK zu vereinfachen. Sie können jede Seite Ihrer Website einzeln migrieren, ohne die gesamte Website gleichzeitig migrieren zu müssen. Sie können den Web-SDK auf einigen Seiten verwenden, während vorhandene Bibliotheken auf anderen verbleiben, was einen schrittweisen Übergang ermöglicht.
