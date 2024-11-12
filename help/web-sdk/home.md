---
title: Übersicht über das Adobe Experience Platform Web Software Development Kit (SDK)
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Adobe Experience Platform Web SDK {#overview}

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, mit der Adobe Experience Cloud-Kunden über das Adobe Experience Platform-Edge Network mit ihren Diensten interagieren können.

Sie können das Web SDK auf zwei Arten implementieren:

* Die [Web SDK-Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Weitere Informationen finden Sie im Tutorial zum [Implementieren von Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de) .
* Manuelle Implementierung mit der [Web SDK JavaScript-Bibliothek](install/library.md).

Dieses Handbuch enthält Anweisungen zur Interaktion mit Experience Cloud-Lösungen, die sowohl die Web SDK JavaScript-Bibliothek als auch die Tag-Erweiterung verwenden.

## Experience Platform Edge Network {#edge-network}



Das Experience Platform Web SDK ist Teil des Adobe Experience Platform-Edge Networks, das Folgendes umfasst:

* **[Experience Platform Web SDK](#overview)**: Eine JavaScript-Bibliothek und Tag-Erweiterung zur Vereinfachung der Bereitstellung von Adobe-Technologie.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: Eine Erweiterung der neuen Bereitstellungsmethode auf das Mobile SDK v5.
* **[Edge Network-API](../server-api/overview.md)**: Eine serverseitige API für Anwendungsfälle zur Datenerfassung, Personalisierung, Werbung und Marketing. Sie können sie auf Servern, IoT-Geräten, Set-Top-Boxen und anderen Geräten verwenden.

Das Edge Network bietet eine Datenerfassung mit geringer Latenz, Pluggable Computing und eine schnelle Datenaktivierung über alle adressierbaren Kanäle hinweg. Es bietet ein einziges konsolidiertes SDK für Web-, Mobile- und Server-seitige Kanäle, das Senden von Daten an eine gemeinsame Adobe-Domäne (`adobedc.net`) und das Empfangen einer einzigen Payload für die Daten- und Erlebnisbereitstellung.

Auf der Server-Seite vereinfachen ein einheitliches Edge-Gateway und ein gemeinsames Plattform-Service-Framework die Bereitstellung neuer Funktionen und bieten dabei die folgenden Vorteile:

* Verringerung der Kundenzeit bis zur Wertsteigerung;
* Beendigung der Notwendigkeit von &quot;Point&quot;-Integrationen;
* Verbesserung der Leistung im Vergleich zu den alten Bibliotheken;
* sinkende Betriebskosten;
* Steigerung der Innovationsgeschwindigkeit;
* Schaffung nachhaltiger Wettbewerbsvorteile für Adobe-Kunden.

Mit einem konsolidierten Edge-System können Sie Werbe-, Marketing- und Personalisierungskampagnen über alle Kanäle hinweg verwalten. Sie reduziert die Gesamtbetriebskosten und unterstützt verschiedene Datentypen, sodass Sie Ihr Datenmodell für die Verwendung mit mehreren Experience Cloud-Produkten zuordnen können.

## Videoüberblick {#video}

Sehen Sie sich das folgende Video an, um einen Überblick über die Adobe Experience Platform [!DNL Web SDK] und die [!DNL Edge Network] zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch Web SDK ersetzte Bibliotheken {#sdks}

Das Web SDK ist eine neue Open-Source-Bibliothek, die von Grund auf neu zur Integration vorhandener Bibliotheken entwickelt wurde. Es werden Probleme mit der Tag-Auslöserreihenfolge, Versionsinkonsistenzen und der Abhängigkeitsverwaltung behoben, die eine neue [Open Source](https://github.com/adobe/alloy)-Methode zur Implementierung von [!DNL Experience Cloud] bieten.

Das Web SDK ersetzt:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Außerdem wird ein neuer Endpunkt eingeführt, der HTTP-Anforderungen an Adobe-Lösungen optimiert. Zuvor waren mehrere Aufrufe für `Visitor.js`, `AT.js`, `DIL.js` und `AppMeasurement.js` erforderlich. Jetzt kann ein einzelner Aufruf eine ID abrufen, ein [!DNL Target] -Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und Daten an Adobe Experience Platform übergeben.

Sehen Sie sich das folgende Video an, um zu sehen, wie Adobe Experience Platform [!DNL Web SDK] und [!DNL Edge Network] in Aktion sind, indem Sie einen einzigen Aufruf verwenden, um Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] zu senden.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migration von vorhandenen Bibliotheken zu Web SDK {#migrating-to-web-sdk}

Adobe bietet einen optimierten Aktualisierungspfad, um die Migration von einer der [vorhandenen Bibliotheken](#sdks) auf das Web SDK zu vereinfachen. Sie können jede Seite Ihrer Website einzeln migrieren, ohne die gesamte Website gleichzeitig migrieren zu müssen. Sie können das Web SDK auf einigen Seiten verwenden, während vorhandene Bibliotheken auf anderen bleiben, was einen schrittweisen Übergang ermöglicht.

### Überlegungen zur Migration von `AT.js` zum Web SDK {#considerations}

Bevor Sie Seiten mit `AT.js` in das Web SDK migrieren, aktivieren Sie die folgenden Web SDK-Konfigurationsoptionen, um sicherzustellen, dass das Besucherprofil beim Navigieren zwischen Seiten beibehalten wird.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Die folgenden Target-Funktionen werden bei der Migration von `at.js` zum Web SDK nicht unterstützt:
>
>* [Umleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=de)
>* [CNAME- und domänenübergreifende Unterstützung](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Entfernen Sie nach der Migration von `AT.js` zum Web SDK die Option `targetMigrationEnabled` aus Ihrer Konfiguration.
