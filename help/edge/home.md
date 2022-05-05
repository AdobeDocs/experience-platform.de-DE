---
title: Adobe Experience Platform Web SDK – Überblick
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch;Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: ht
source-wordcount: '622'
ht-degree: 100%

---

# Adobe Experience Platform Web SDK – Überblick

Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, mit der Kunden von Adobe Experience Cloud mit den verschiedenen Services in [!DNL Experience Cloud] interagieren können. Zusätzlich zur JavaScript-Bibliothek steht eine [Tag-Erweiterung](./extension/web-sdk-extension-configuration.md) als Hilfe bei Ihren Web SDK-Konfigurationen zur Verfügung.

**Eine schrittweise Anleitung zum Einrichten des Web SDK mit Tags und zum Senden von Daten an die Lösungen finden Sie in unserem [Tutorial zur Implementierung von Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] ist Teil der Sammlung, aus der Experience Edge besteht. Experience Edge umfasst drei Technologien:

* **[!DNL Adobe Experience Platform Web SDK]:** Ein JavaScript-SDK und eine Tag-Erweiterung, mit der die Implementierung von [!DNL Adobe]-Technologien erheblich vereinfacht wird
* **Adobe Experience Platform Mobile SDK:** Eine Erweiterung des mobilen SDK v5, um Kunden die Verwendung der neuen Implementierungsmethode zu ermöglichen.
* **[!DNL Adobe Experience Platform Edge Network]:** Ein globales verteiltes Netzwerk von Servern, das eine neue Methode zur Implementierung von [!DNL Adobe]-Produkten ermöglicht

[!DNL Adobe Experience Edge] ist ein Framework zur Erfassung von Daten mit niedriger Latenz sowie zum Pluggable Computing und zur schnellen Aktivierung von Daten auf allen adressierbaren Kanälen.

[!DNL Adobe Experience Edge] bietet ein einziges konsolidiertes SDK für jeden Kanal (JavaScript, Mobil, Server-seitig), das Daten an eine gemeinsame Adobe-Domain sendet (`adobedc.net`) und eine einzige Payload für die Daten- und Erlebnisbereitstellung empfängt.

Auf der Server-Seite erleichtert ein einheitliches Edge-Gateway und ein gemeinsames Framework für Plattform-Services die Herstellung einer Verbindung und die Bereitstellung neuer Funktionen für diese Echtzeitumgebung.  Diese Architektur:

* Verkürzt die Time-to-Value für den Kunden
* Macht punktuelle Integrationen überflüssig
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Senkt die Kosten
* Erhöht die Innovationsgeschwindigkeit
* Schafft nachhaltige Wettbewerbsvorteile für Adobe-Kunden

Mit einem einzigen konsolidierten Edge-System können Kunden ihre Werbe-, Marketing- oder Personalisierungskampagnen auf allen Kanälen als integriertes Erlebnis verwalten.  Dieses System ermöglicht [!DNL Adobe], Services mit niedrigeren Gesamtbetriebskosten für Kunden bereitzustellen.  Darüber hinaus erhöht es die Geschwindigkeit der Produktinnovation, da ein Steckanschluss an das Echtzeit-Edge-System ermöglicht wird und [!DNL Adobe] und seine Kunden dieses Echtzeit-System schneller mit neuen Funktionen und kundendefinierter Logik ausstatten können.

## Videoüberblick

Das folgende Video bietet einen Überblick über das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Dadurch sollen Probleme wie das Auslösen von Tags in der richtigen Reihenfolge und inkonsistente Bibliotheksversionen gelöst und eine verbesserte Abhängigkeitsverwaltung geboten werden. Dies ist eine neue Methode zur Implementierung von [!DNL Experience Cloud] und steht als [Open Source](https://github.com/adobe/alloy) zur Verfügung.

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können in einem einzigen Aufruf eine ID abrufen, ein [!DNL Target]-Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und die Daten an Adobe Experience Platform übergeben.

Das folgende Video zeigt das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion. Im Videobeispiel werden über einen einzigen Aufruf an Adobe Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] gesendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dieses Produkt wird laufend weiterentwickelt, um immer mehr Anwendungsfälle zu unterstützen. Um auf dem Laufenden zu bleiben und zu sehen, was derzeit unterstützt wird, besuchen Sie [die Seite mit unterstützten Anwendungsfällen](https://github.com/orgs/adobe/projects/18/views/1).
