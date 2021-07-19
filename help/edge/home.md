---
title: Übersicht über das Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch;Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 14%

---

# Übersicht über das Adobe Experience Platform Web SDK

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, mit der Kunden von Adobe Experience Cloud über das Adobe Experience Platform Edge Network mit den verschiedenen Diensten im [!DNL Experience Cloud] interagieren können. Zusätzlich zur JavaScript-Bibliothek gibt es eine [Experience Platform Launch-Erweiterung](../tags/extensions/web/sdk/overview.md), die Ihnen bei Ihren Web SDK-Konfigurationen hilft.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] ist Teil der Sammlung, aus der Experience Edge besteht. Experience Edge umfasst drei Technologien:

* **[!DNL Adobe Experience Platform Web SDK]:** Ein JavaScript-SDK und eine  [!DNL Experience Platform Launch] Erweiterung zur drastischen Vereinfachung der Bereitstellung von  [!DNL Adobe] Technologien
* **Adobe Experience Platform Mobile SDK:**  Eine Erweiterung des Mobile SDK v5, um Kunden die Verwendung der neuen Bereitstellungsmethode zu ermöglichen
* **[!DNL Adobe Experience Platform Edge Network]:** Ein globales Netzwerk verteilter Server, das eine neue Methode zur Bereitstellung von  [!DNL Adobe] Produkten ermöglicht

[!DNL Adobe Experience Edge] ist ein neues Framework für die Erfassung von Daten mit geringer Latenz, für Pluggable Computing und für die schnelle Aktivierung von Daten über alle adressierbaren Kanäle hinweg.

[!DNL Adobe Experience Edge] bietet für jeden Kanal (JavaScript, Mobil, Server-seitig) ein einziges konsolidiertes SDK, das Daten an eine gemeinsame Adobe-Domain (`adobedc.net`) sendet und eine einzige Payload für die Daten- und Erlebnisbereitstellung erhält.

Auf der Server-Seite erleichtert ein einheitliches Edge-Gateway und ein gemeinsames Framework für Plattformdienste das Plug-in und die Bereitstellung neuer Funktionen in dieser Echtzeit-Computerumgebung.  Diese Architektur:

* Verringert Kundenzeit bis Wert
* Beendet die Notwendigkeit von &quot;Point&quot;-Integrationen
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Kostensenkungen
* Erhöht die Innovationsgeschwindigkeit
* Erstellt nachhaltige Wettbewerbsvorteile für Adobe-Kunden

Mit einem einzigen konsolidierten Edge-System können Kunden ihre Werbe-, Marketing- oder Personalisierungskampagnen über alle Kanäle hinweg als integriertes Erlebnis verwalten.  Dadurch kann [!DNL Adobe] Dienste mit geringeren Gesamtbetriebskosten für Kunden bereitstellen.  Es trägt auch zur Beschleunigung der Produktinnovation bei, indem es die Echtzeit-Edge-Plugins ermöglicht und [!DNL Adobe] und seinen Kunden ermöglicht, diesem Echtzeit-System schneller neue Funktionen und kundendefinierte Logik hinzuzufügen.

## Videoüberblick

Das folgende Video gibt einen Überblick über die Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck besteht darin, Herausforderungen zu beenden, indem Tags in der richtigen Reihenfolge ausgelöst werden, die Konsistenz mit Herausforderungen bei der Bibliotheksversionierung beeinträchtigt wird und die Abhängigkeitsverwaltung verbessert wird. Es ist eine neue Methode, [!DNL Experience Cloud] zu implementieren und ist [Open Source](https://github.com/adobe/alloy).

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen, ein [!DNL Target]-Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und die Daten in einem einzigen Aufruf an Adobe Experience Platform übergeben.

Das folgende Video zeigt Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion. Das Videobeispiel verwendet einen einzigen Aufruf an Adobe, der Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] sendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dieses Produkt entwickelt sich ständig weiter und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um mit dem neuesten Stand zu bleiben, lesen Sie die Seite [Unterstützte Anwendungsfälle](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Auf dieser Seite werden die aktuell unterstützten Anwendungsfälle mit Links zu weiteren Informationen aufgeführt, sofern verfügbar.

* **Nutzungsszenarios noch nicht unterstützt:**  Dies sind Anwendungsfälle, die auf unserem Fahrplan stehen und in Zukunft unterstützt werden sollen.
* **Anwendungsfälle in Bearbeitung:**  Dies sind die Anwendungsfälle, mit denen das Team derzeit eine Version abschließt.
* **Unterstützte Anwendungsfälle:** Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* **Nutzungsszenarios, die wir nicht unterstützen:** Dies sind die Anwendungsfälle, für die wir entschieden haben, sie nicht zu unterstützen.
