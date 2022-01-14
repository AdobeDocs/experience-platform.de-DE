---
title: Übersicht über das Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Platform-Funktionen in Ihre Website integrieren können.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch;Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 1048f19e2395f63fac8c4218ed92a546b8071a93
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 13%

---

# Übersicht über das Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, mit den verschiedenen Diensten im [!DNL Experience Cloud] über das Adobe Experience Platform Edge Network. Zusätzlich zur JavaScript-Bibliothek gibt es eine [Tag-Erweiterung](./extension/web-sdk-extension-configuration.md) um Hilfe bei Ihren Web SDK-Konfigurationen zu erhalten.

**Eine schrittweise Anleitung zum Einrichten des Web SDK mit Tags und zum Senden von Daten an die Lösungen finden Sie in unserer [Tutorial zur Implementierung von Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] ist Teil der Sammlung, aus der Experience Edge besteht. Experience Edge umfasst drei Technologien:

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript-SDK und Tag-Erweiterung zur drastischen Vereinfachung der Bereitstellung [!DNL Adobe] Technologien
* **Adobe Experience Platform Mobile SDK:** Eine Erweiterung des mobilen SDK v5, um Kunden die Verwendung der neuen Bereitstellungsmethode zu ermöglichen.
* **[!DNL Adobe Experience Platform Edge Network]:** Ein globales verteiltes Netzwerk von Servern, das eine neue Methode zur Bereitstellung ermöglicht [!DNL Adobe] products

Die [!DNL Adobe Experience Edge] ist ein neues Framework für die Erfassung von Daten mit geringer Latenz, für Pluggable Computing und für die schnelle Aktivierung von Daten über alle adressierbaren Kanäle hinweg.

[!DNL Adobe Experience Edge] bietet ein einziges konsolidiertes SDK für jeden Kanal (JavaScript, Mobil, Server-seitig), der Daten an eine gemeinsame Adobe-Domäne (`adobedc.net`) und erhält eine einzige Payload zurück für die Daten- und Erlebnisbereitstellung.

Auf der Server-Seite erleichtert ein einheitliches Edge-Gateway und ein gemeinsames Framework für Plattformdienste das Plug-in und die Bereitstellung neuer Funktionen in dieser Echtzeit-Computerumgebung.  Diese Architektur:

* Verringert Kundenzeit bis Wert
* Beendet die Notwendigkeit von &quot;Point&quot;-Integrationen
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Kostensenkungen
* Erhöht die Innovationsgeschwindigkeit
* Erstellt nachhaltige Wettbewerbsvorteile für Adobe-Kunden

Mit einem einzigen konsolidierten Edge-System können Kunden ihre Werbe-, Marketing- oder Personalisierungskampagnen über alle Kanäle hinweg als integriertes Erlebnis verwalten.  Sie ermöglicht [!DNL Adobe] zur Erbringung von Dienstleistungen mit niedrigeren Gesamtbetriebskosten für Kunden.  Es trägt auch dazu bei, die Geschwindigkeit der Produktinnovation zu erhöhen, indem die Echtzeit-Edge-Verkabelung ermöglicht wird und [!DNL Adobe] und ihren Kunden, um diesem Echtzeit-System schneller neue Funktionen und kundendefinierte Logik hinzuzufügen.

## Videoüberblick

Das folgende Video gibt einen Überblick über die Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck besteht darin, Herausforderungen zu beenden, indem Tags in der richtigen Reihenfolge ausgelöst werden, die Konsistenz mit Herausforderungen bei der Bibliotheksversionierung beeinträchtigt wird und die Abhängigkeitsverwaltung verbessert wird. Dies ist eine neue Methode zur Implementierung der [!DNL Experience Cloud] und [Open Source](https://github.com/adobe/alloy).

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen und eine [!DNL Target] Erlebnis, Daten senden an [!DNL Audience Manager]und übergeben Sie die Daten in einem einzigen Aufruf an Adobe Experience Platform.

Das folgende Video zeigt Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion. Das Videobeispiel verwendet einen einzelnen Aufruf an Adobe, der Daten an sendet. [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]und [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dieses Produkt entwickelt sich ständig weiter und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um mit dem neuesten Stand zu bleiben, lesen Sie den Abschnitt [Seite mit unterstützten Anwendungsfällen](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Auf dieser Seite werden die aktuell unterstützten Anwendungsfälle mit Links zu weiteren Informationen aufgeführt, sofern verfügbar.

* **Anwendungsfälle, die noch nicht unterstützt werden:** Dies sind Anwendungsfälle, die auf unserem Fahrplan stehen und in Zukunft unterstützt werden sollen.
* **In Bearbeitung befindliche Anwendungsfälle:** Dies sind die Anwendungsfälle, an denen das Team derzeit arbeitet, um die Veröffentlichung abzuschließen.
* **Unterstützte Anwendungsfälle:** Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* **Anwendungsfälle, die wir nicht unterstützen:** Dies sind die Anwendungsfälle, die wir beschlossen haben, nicht zu unterstützen.
