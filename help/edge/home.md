---
title: Übersicht über das Adobe Experience Platform Web Software Development Kit (SDK)
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch;Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 52dbde052322a00fc33cd9f9c86ab7f92671f36a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 40%

---

# Adobe Experience Platform Web SDK – Überblick {#overview}

Adobe Experience Platform Web Software Development Kit (SDK) ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, über das Adobe Experience Platform Edge Network mit ihren Diensten zu interagieren. Adobe bietet zwei Methoden zur Implementierung des Web SDK:

* Manuelle Implementierung mithilfe von `alloy.js`. Dieses Benutzerhandbuch enthält eine Dokumentation zu dieser Implementierungsmethode.
* Die [Web SDK-Tag-Erweiterung](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Siehe [Tutorial zur Implementierung von Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de) für weitere Informationen.

## Adobe Experience Edge

Das Adobe Experience Platform Web SDK ist Teil der Sammlung, aus der Adobe Experience Edge besteht. Adobe Experience Edge umfasst die folgenden Technologien:

* **[Adobe Experience Platform Web SDK](#overview):** JavaScript-SDK und Tag-Erweiterung zur drastischen Vereinfachung der Bereitstellung von Adobe-Technologien.
* **[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/):** Eine Erweiterung des mobilen SDK v5, damit Kunden die neue Bereitstellungsmethode verwenden können.
* **[Adobe Experience Platform Edge Network](../server-api/overview.md):** Ein globales verteiltes Netzwerk von Servern, das eine neue Methode zur Bereitstellung ermöglicht [!DNL Adobe] products

Adobe Experience Edge ist ein Framework für die Erfassung von Daten mit geringer Latenz, für Pluggable Computing und für die schnelle Aktivierung von Daten über alle adressierbaren Kanäle hinweg.

[!DNL Adobe Experience Edge] bietet ein einziges konsolidiertes SDK für jeden Kanal (JavaScript, Mobil, Server-seitig), das Daten an eine gemeinsame Adobe-Domain sendet (`adobedc.net`) und eine einzige Payload für die Daten- und Erlebnisbereitstellung empfängt.

Auf der Server-Seite erleichtern ein einheitliches Edge-Gateway und ein gemeinsames Plattform-Service-Framework die Bereitstellung neuer Funktionen in dieser Echtzeit-Computerumgebung. Diese Architektur:

* Verkürzt die Time-to-Value für den Kunden
* Macht punktuelle Integrationen überflüssig
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Senkt die Kosten
* Erhöht die Innovationsgeschwindigkeit
* Schafft nachhaltige Wettbewerbsvorteile für Adobe-Kunden

Mit einem einzigen konsolidierten Edge-System können Kunden ihre Werbe-, Marketing- oder Personalisierungskampagnen über alle Kanäle hinweg als integriertes Erlebnis verwalten. Außerdem ermöglicht es Adobe, Dienstleistungen mit geringeren Gesamtbetriebskosten für Kunden zu erbringen. Das Edge-System ist für die meisten Datentypen ausgelegt, sodass Sie Ihr eigenes Datenmodell für die Aufnahme durch mehrere Experience Cloud-Produkte zuordnen können.

## Videoüberblick {#video}

Das folgende Video bietet einen Überblick über das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch Web SDK ersetzte Bibliotheken {#sdks}

Web SDK ist nicht nur ein Wrapper für vorhandene Bibliotheken. Es handelt sich um eine neue Bibliothek, die von Grund auf geschrieben wurde, um Funktionen vorhandener Bibliotheken zu integrieren. Dadurch sollen Probleme wie das Auslösen von Tags in der richtigen Reihenfolge und inkonsistente Bibliotheksversionen gelöst und eine verbesserte Abhängigkeitsverwaltung geboten werden. Dies ist eine neue Methode zur Implementierung von [!DNL Experience Cloud] und steht als [Open Source](https://github.com/adobe/alloy) zur Verfügung.

Platform Web SDK ersetzt die folgenden SDKs:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Vorher `Visitor.js` einen Blockierungsaufruf an den Besucher-ID-Dienst gesendet und dann `AT.js` einen Aufruf an Adobe Target gesendet hat, `DIL.js` einen Aufruf an Adobe Audience Manager gesendet und schließlich `AppMeasurement.js` einen Aufruf an Adobe Analytics gesendet hat. Diese neue Bibliothek und dieser Endpunkt können in einem einzigen Aufruf eine ID abrufen, ein [!DNL Target]-Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und die Daten an Adobe Experience Platform übergeben.

Das folgende Video zeigt das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion. Im Videobeispiel werden über einen einzigen Aufruf an Adobe Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] gesendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migration von vorhandenen Bibliotheken zu Web SDK {#migrating-to-web-sdk}

So vereinfachen Sie die Migration von [vorhandene Bibliotheken](#sdks) zum Web SDK bietet Adobe einen optimierten Aktualisierungspfad. Mit diesem Pfad können Sie jede einzelne Seite Ihrer Website zum Web SDK migrieren, ohne die gesamte Website gleichzeitig migrieren zu müssen. Sie können das Web SDK auf einer bestimmten Seite verwenden, während sich vorhandene Bibliotheken auf anderen Seiten befinden. Sobald Sie fertig sind, können Sie auch diese anderen Seiten migrieren.

### Migration `AT.js` Überlegungen zum Web SDK {#considerations}

Bevor Sie Seiten, die `AT.js` verwenden, zu Web SDK migrieren, müssen Sie die folgenden Web SDK-Konfigurationsoptionen aktivieren. Diese Optionen stellen sicher, dass das Besucherprofil beim Navigieren von Seiten mit `AT.js` auf Seiten, die das Web SDK verwenden.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Die folgenden Target-Funktionen werden bei der Migration von at.js zum Web SDK nicht unterstützt:
>
>* [Weiterleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=de)
>* [CNAME- und domänenübergreifende Unterstützung](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Nach der Migration von `AT.js` im Web SDK entfernen `targetMigrationEnabled` -Option aus Ihrer Konfiguration.
