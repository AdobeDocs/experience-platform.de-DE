---
title: Adobe Experience Platform Web SDK – Hilfe
seo-title: Adobe Experience Platform Web SDK – Hilfe
description: Erfahren Sie, was das Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Erfahren Sie, wie Sie Kunden von Adobe Experience Cloud die Interaktion mit den verschiedenen Services des Experience Cloud ermöglichen.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Besucher.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;Web SDK;Web SDK;Launch;Launch
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 19%

---


# Was ist das Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ist eine clientseitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, über das Adobe Experience Platform Edge Network mit den verschiedenen Diensten im [!DNL Experience Cloud] zu interagieren. Zusätzlich zur JavaScript-Bibliothek gibt es eine [Experience Platform Launch-Erweiterung](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html), die Sie bei Ihren Web SDK-Konfigurationen unterstützen kann.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] ist Teil der Sammlung, aus der Experience Edge besteht. Experience Edge umfasst drei Technologien:

* **[!DNL Adobe Experience Platform Web SDK]:** Ein JavaScript-SDK und eine  [!DNL Experience Platform Launch] Erweiterung zur drastischen Vereinfachung der Bereitstellung von  [!DNL Adobe] Technologien
* **Adobe Experience Platform Mobile SDK:** Eine Erweiterung des v5 Mobile SDK, damit Kunden die neue Bereitstellungsmethodik verwenden können
* **[!DNL Adobe Experience Platform Edge Network]:** Ein globales Netzwerk verteilter Server, das eine neue Methode zur Bereitstellung von  [!DNL Adobe] Produkten ermöglicht

Das [!DNL Adobe Experience Edge] ist ein neues Framework für die Datenerfassung mit geringer Latenz, für Plug-In-Computing und für die schnelle Aktivierung von Daten in allen adressierbaren Kanälen.

[!DNL Adobe Experience Edge] stellt für jeden Kanal (JavaScript, Mobil, Server-seitig) ein einziges konsolidiertes SDK bereit, das Daten an eine allgemeine Adobe-Domäne (`adobedc.net`) sendet und eine einzige Nutzlast für Daten- und Erlebnis-Versand erhält.

Serverseitig ermöglicht ein einheitliches Edge-Gateway und ein gemeinsames Framework für Plattformdienste eine einfache Plug-in- und Bereitstellung neuer Funktionen in dieser Echtzeit-Computing-Umgebung.  Diese Architektur:

* Verringert die Besuchszeit für Kunden
* Beendet die Notwendigkeit von &quot;Point&quot;-Integrationen
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Kostensenkungen
* Erhöht die Innovationsgeschwindigkeit
* Erwirbt nachhaltige Wettbewerbsvorteile für Adoben

Ein einheitliches konsolidiertes Kantensystem ermöglicht es Kunden, ihre Werbe-, Marketing- oder Personalisierungs-Kampagnen über alle Kanal hinweg zu verwalten.  Es ermöglicht [!DNL Adobe], Dienste mit niedrigeren Gesamtbetriebskosten für Kunden bereitzustellen.  Darüber hinaus wird die Produktneuerung beschleunigt, indem der Echtzeit-Edge-Plug-In ermöglicht wird und [!DNL Adobe] und seine Kunden diesem Echtzeit-System schneller neue Funktionen und kundenspezifische Logik hinzufügen können.

## Videoüberblick

Das folgende Video gibt einen Überblick über das Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck ist es, Herausforderungen zu beenden, indem Tags in der richtigen Reihenfolge ausgelöst werden müssen, die nicht mit den Versionshinweisen der Bibliothek übereinstimmen und die Abhängigkeitsverwaltung verbessert wird. Es ist eine neue Methode, die [!DNL Experience Cloud] zu implementieren, und es ist [open source](https://github.com/adobe/alloy).

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen, ein [!DNL Target]-Erlebnis abrufen, Daten an [!DNL Audience Manager] senden und die Daten in einem einzigen Aufruf an Adobe Experience Platform übergeben.

Das folgende Video zeigt, wie Adobe Experience Platform [!DNL Web SDK] und Adobe Experience Platform [!DNL Edge Network] in Aktion ausgeführt werden. Im Videobeispiel wird ein Einzelaufruf an die Adobe verwendet, der Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] und [!DNL Target] sendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dieses Produkt entwickelt sich ständig und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um auf dem neuesten Stand zu sein, schauen Sie sich unser [unterstütztes Gebrauchsanweisung](https://github.com/adobe/alloy/projects/5) an. Wir halten dies auf dem neuesten Stand mit den derzeit unterstützten Anwendungsfällen und den Fällen, an denen wir arbeiten, damit Sie die bestmöglichen Entscheidungen treffen können.

* **Anwendungsfälle, die noch nicht unterstützt werden:** Dies sind Anwendungsfälle, die auf unserem Plan stehen und in Zukunft unterstützt werden sollen.
* **Anwendungsfälle noch nicht abgeschlossen:** Dies sind die Anwendungsfälle, mit denen das Team derzeit arbeitet.
* **Unterstützte Anwendungsfälle:** Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* **Anwendungsfälle, die wir nicht unterstützen werden:** Dies sind die Anwendungsfälle, die wir beschlossen haben, nicht zu unterstützen.
