---
title: Überblick über das Adobe Experience Platform Web Software Development Kit (SDK)
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Web SDK Experience Platform-Funktionen in Ihre Website integrieren können.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 5%

---

# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, die es Adobe Experience Cloud-Kunden ermöglicht, über Adobe Experience Platform Edge Network mit ihren Services zu interagieren.

Sie können Web SDK auf zwei Arten implementieren:

* Die [Web SDK-Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Weitere Informationen finden Sie im Tutorial [Implementieren von Adobe Experience Cloud SDK mit Web ](https://experienceleague.adobe.com/de/docs/platform-learn/implement-web-sdk/overview)&quot;.
* Manuelle Implementierung mithilfe der [Web SDK JavaScript Library](install/library.md).

Dieses Handbuch enthält Anweisungen für die Interaktion mit Experience Cloud-Lösungen unter Verwendung der Web SDK JavaScript-Bibliothek und der Tag-Erweiterung.

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK ist Teil von Adobe Experience Platform Edge Network, das Folgendes umfasst:

* **[Experience Platform Web SDK](#overview)**: Eine JavaScript-Bibliothek und Tag-Erweiterung zur Vereinfachung der Bereitstellung von Adobe-Technologie.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: Eine Erweiterung von Mobile SDK v5 für die neue Bereitstellungsmethode.
* **[Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/)**: Eine Server-seitige API für Datenerfassungs-, Personalisierungs-, Werbe- und Marketing-Anwendungsfälle. Sie können sie auf Servern, IoT-Geräten, Set-Top-Boxen und anderen Geräten verwenden.

Der Edge Network bietet Datenerfassung mit niedriger Latenz, Plug-in-Datenverarbeitung und schnelle Datenaktivierung über alle adressierbaren Kanäle hinweg. Sie bietet eine einzige konsolidierte SDK für Web-, Mobil- und Server-seitige Kanäle, die Daten an eine gemeinsame Adobe-Domain (`adobedc.net`) sendet und eine einzige Payload für die Daten- und Erlebnisbereitstellung empfängt.

Auf der Serverseite vereinfachen ein einheitliches Edge-Gateway und ein gemeinsames Plattform-Service-Framework die Bereitstellung neuer Funktionen und bieten gleichzeitig die folgenden Vorteile:

* Verkürzung der Amortisierungszeit für Kunden
* Abschaffung der Notwendigkeit von punktuellen Integrationen;
* Verbesserung der Leistung im Vergleich zu den alten Bibliotheken
* Sinkende Betriebskosten;
* Erhöhung der Innovationsgeschwindigkeit;
* Schaffung nachhaltiger Wettbewerbsvorteile für Adobe-Kunden.

Mit einem konsolidierten Edge-System können Sie Werbe-, Marketing- und Personalisierungskampagnen auf allen Kanälen verwalten. Dies reduziert die Gesamtbetriebskosten und unterstützt verschiedene Datentypen, sodass Sie Ihr Datenmodell für die Verwendung mit mehreren Experience Cloud-Produkten zuordnen können.

## Videoüberblick {#video}

Sehen Sie sich das folgende Video an, um einen Überblick über die Adobe Experience Platform-[!DNL Web SDK] und die [!DNL Edge Network] zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch Web SDK ersetzte Bibliotheken {#sdks}

Web SDK ist eine neue Open-Source-Bibliothek, die von Grund auf neu erstellt wurde, um Funktionen bestehender Bibliotheken zu integrieren. Es behandelt Probleme mit der Tag-Auslösereihenfolge, Versionsinkonsistenzen und der Abhängigkeitsverwaltung und bietet eine neue, [Open Source](https://github.com/adobe/alloy)-Methode zur Implementierung der [!DNL Experience Cloud].

Web SDK ersetzt:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Außerdem wird ein neuer Endpunkt eingeführt, der HTTP-Anfragen an Adobe-Lösungen optimiert. Zuvor waren mehrere Aufrufe für `Visitor.js`, `AT.js`, `DIL.js` und `AppMeasurement.js` erforderlich. Mit einem einzigen Aufruf können Sie nun eine ID abrufen, ein [!DNL Target] Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und Daten an Adobe Experience Platform übergeben.

Sehen Sie sich das folgende Video an, um die [!DNL Web SDK] und [!DNL Edge Network] von Adobe Experience Platform in Aktion zu sehen, wobei ein einziger Aufruf zum Senden von Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] verwendet wird.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migration von vorhandenen Bibliotheken zu Web SDK {#migrating-to-web-sdk}

Adobe bietet einen optimierten Aktualisierungspfad, um die Migration von einer der [ Bibliotheken ](#sdks) Web SDK zu vereinfachen. Sie können jede Seite Ihrer Website einzeln migrieren, ohne die gesamte Website gleichzeitig migrieren zu müssen. Sie können den Web-SDK auf einigen Seiten verwenden, während vorhandene Bibliotheken auf anderen verbleiben, was einen schrittweisen Übergang ermöglicht.

### Überlegungen zur Migration von `AT.js` zu Web SDK {#considerations}

Aktivieren Sie vor der Migration von Seiten mit `AT.js` zu Web SDK die folgenden Konfigurationsoptionen für Web SDK, um sicherzustellen, dass das Besucherprofil beim Navigieren zwischen Seiten beibehalten wird.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Die folgenden Target-Funktionen werden bei der Migration von `at.js` zu Web SDK nicht unterstützt:
>
>* [Umleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=de)
>* [CNAME- und domänenübergreifende Unterstützung](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Nach der Migration von `AT.js` zur Web-SDK entfernen Sie die Option `targetMigrationEnabled` aus Ihrer Konfiguration.
