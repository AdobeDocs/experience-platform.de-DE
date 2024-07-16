---
title: Übersicht über das Adobe Experience Platform Web Software Development Kit (SDK)
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 28%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>Ende April 2024 wird das Adobe Experience Platform Web SDK alle Versionen von Internet Explorer nicht mehr unterstützen.

Das Adobe Experience Platform Web Software Development Kit (SDK) ist eine Client-seitige JavaScript-Bibliothek, mit der Kunden von Adobe Experience Cloud über das Adobe Experience Platform-Edge Network mit ihren Diensten interagieren können.

Adobe bietet zwei Methoden zur Implementierung des Web SDK:

* Die [Web SDK-Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Weitere Informationen finden Sie im Tutorial zum [Implementieren von Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de) .
* Manuelle Implementierung mithilfe der Web SDK JavaScript-Bibliothek.

Dieses Benutzerhandbuch enthält Anweisungen zur Interaktion mit den Experience Cloud-Lösungen, gegebenenfalls sowohl über die Web SDK JavaScript-Bibliothek als auch über die Tag-Erweiterung.

## Experience Platform Edge Network {#edge-network}

Das Experience Platform Web SDK ist Teil einer Sammlung von Tools, aus denen das Adobe Experience Platform-Edge Network besteht.

Das Edge Network besteht aus den folgenden Komponenten:

* **[Experience Platform Web SDK](#overview):** Eine JavaScript-Bibliothek und eine Tag-Erweiterung, die Ihnen bei der Vereinfachung der Bereitstellung von Adobe-Technologien hilft.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/):** Eine Erweiterung des mobilen SDK v5, mit der Sie die neue Bereitstellungsmethode verwenden können.
* **[Edge Network-Server-API](../server-api/overview.md):** Eine serverseitige API, die Sie für verschiedene Anwendungsfälle für Datenerfassung, Personalisierung, Werbung und Marketing verwenden können. Die Server-API kann auf Servern, IoT-Geräten, Set-Top-Boxen und verschiedenen anderen Geräten verwendet werden.

Das Edge Network ist ein Framework für die Erfassung von Daten mit geringer Latenz, Pluggable Computing und die schnelle Aktivierung von Daten über alle adressierbaren Kanäle hinweg. Es bietet ein einziges konsolidiertes SDK für jeden Kanal (Web, Mobile, Server-seitig), das Daten an eine gemeinsame Adobe-Domäne (`adobedc.net`) sendet und eine einzige Payload für die Daten- und Erlebnisbereitstellung erhält.

Auf der Server-Seite erleichtern ein einheitliches Edge-Gateway und ein gemeinsames Plattform-Service-Framework die Bereitstellung neuer Funktionen in dieser Echtzeit-Computerumgebung. Diese Architektur:

* Verkürzt die Time-to-Value für den Kunden
* Macht punktuelle Integrationen überflüssig
* Verbessert die Performance im Vergleich zu den alten Bibliotheken
* Senkt die Kosten
* Erhöht die Innovationsgeschwindigkeit
* Schafft nachhaltige Wettbewerbsvorteile für Adobe-Kunden

Mit einem einzigen konsolidierten Edge-System können Sie Ihre Werbe-, Marketing- oder Personalisierungskampagnen über alle Kanäle hinweg als integriertes Erlebnis verwalten. Außerdem ermöglicht es Adobe, Dienstleistungen mit geringeren Gesamtbetriebskosten für Kunden zu erbringen. Das Edge-System ist für die meisten Datentypen ausgelegt, sodass Sie Ihr eigenes Datenmodell für die Aufnahme durch mehrere Experience Cloud-Produkte zuordnen können.

## Videoüberblick {#video}

Sehen Sie sich das folgende Video an, um einen Überblick über die Adobe Experience Platform [!DNL Web SDK] und die [!DNL Edge Network] zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch Web SDK ersetzte Bibliotheken {#sdks}

Web SDK ist nicht nur ein Wrapper für vorhandene Bibliotheken. Es handelt sich um eine neue Bibliothek, die von Grund auf geschrieben wurde, um Funktionen vorhandener Bibliotheken zu integrieren. Dadurch sollen Probleme wie das Auslösen von Tags in der richtigen Reihenfolge und inkonsistente Bibliotheksversionen gelöst und eine verbesserte Abhängigkeitsverwaltung geboten werden. Dies ist eine neue Methode zur Implementierung von [!DNL Experience Cloud] und steht als [Open Source](https://github.com/adobe/alloy) zur Verfügung.

Platform Web SDK ersetzt die folgenden SDKs:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete `Visitor.js` einen Sperraufruf an den Besucher-ID-Dienst, dann schickte `AT.js` einen Aufruf an Adobe Target, `DIL.js` einen Aufruf an Adobe Audience Manager und schließlich schickte `AppMeasurement.js` einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können in einem einzigen Aufruf eine ID abrufen, ein [!DNL Target]-Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und die Daten an Adobe Experience Platform übergeben.

Das folgende Video zeigt das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion. Im Videobeispiel werden über einen einzigen Aufruf an Adobe Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] gesendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migration von vorhandenen Bibliotheken zu Web SDK {#migrating-to-web-sdk}

Um die Migration von einer der [vorhandenen Bibliotheken](#sdks) zum Web SDK zu vereinfachen, bietet Adobe einen optimierten Aktualisierungspfad. Mit diesem Pfad können Sie jede einzelne Seite Ihrer Website zum Web SDK migrieren, ohne die gesamte Website gleichzeitig migrieren zu müssen. Sie können das Web SDK auf einer bestimmten Seite verwenden, während sich vorhandene Bibliotheken auf anderen Seiten befinden. Sobald Sie fertig sind, können Sie auch diese anderen Seiten migrieren.

### Überlegungen zur Migration von `AT.js` zum Web SDK {#considerations}

Bevor Sie Seiten, die `AT.js` verwenden, zu Web SDK migrieren, müssen Sie die folgenden Web SDK-Konfigurationsoptionen aktivieren. Diese Optionen stellen sicher, dass das Besucherprofil beibehalten wird, während von Seiten mit `AT.js` zu Seiten mit dem Web SDK navigiert wird.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>Die folgenden Target-Funktionen werden bei der Migration von at.js zum Web SDK nicht unterstützt:
>
>* [Umleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=de)
>* [CNAME- und domänenübergreifende Unterstützung](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Entfernen Sie nach der Migration von `AT.js` zum Web SDK die Option `targetMigrationEnabled` aus Ihrer Konfiguration.
