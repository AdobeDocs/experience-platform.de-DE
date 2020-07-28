---
title: Adobe Experience Platform Web SDK – Hilfe
seo-title: Adobe Experience Platform Web SDK – Hilfe
description: Erfahren Sie, was das Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Kunden von Adobe Experience Cloud die Interaktion mit den verschiedenen Diensten in der Experience Cloud ermöglichen.
translation-type: tm+mt
source-git-commit: fc8b26e237821d5fa2d72fb38189894ed0b05271
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 22%

---


# Was ist das Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is a client-side JavaScript library that allows customers of the Adobe Experience Cloud to interact with the various services in the [!DNL Experience Cloud] through the Adobe [!DNL Experience Platform Edge Network]. Zusätzlich zur JavaScript-Bibliothek gibt es eine [Launch-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) , die Sie bei Ihren Web SDK-Konfigurationen unterstützt.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] ist Teil der Sammlung, aus der Experience Edge besteht. Experience Edge umfasst drei Technologien:

* **[!DNL Adobe Experience Platform Web SDK]:**JavaScript-SDK und -[!DNL Launch]Erweiterung zur drastischen Vereinfachung der Bereitstellung von[!DNL Adobe]Technologien
* **Adobe Experience Platform Mobile SDK:** Eine Erweiterung des mobilen v5-SDK, damit Kunden die neue Bereitstellungsmethodik verwenden können
* **[!DNL Adobe Experience Platform Edge Network]:**Ein globales Netzwerk verteilter Server, das eine neue Methode zur Bereitstellung von[!DNL Adobe]Produkten ermöglicht

The [!DNL Adobe Experience Edge] is a new framework for low-latency data collection, pluggable computing and rapid data activation across all addressable channels.

[!DNL Adobe Experience Edge] stellt für jeden Kanal (JavaScript, Mobil, Server-seitig) ein einziges konsolidiertes SDK bereit, das Daten an eine allgemeine Adobe-Domäne (`adobedc.net`) sendet und eine einzige Nutzlast für Daten- und Erlebnis-Versand erhält.

Serverseitig ermöglicht ein einheitliches Edge-Gateway und ein gemeinsames Framework für Plattformdienste eine einfache Plug-in- und Bereitstellung neuer Funktionen in dieser Echtzeit-Computing-Umgebung.  Diese Architektur:

* Verringert die Besuchszeit für Kunden
* Beendet die Notwendigkeit von &quot;Point&quot;-Integrationen
* Verbessert die Leistung im Vergleich zu den alten Bibliotheken
* Kostensenkungen
* Erhöht die Innovationsgeschwindigkeit
* Erwirbt nachhaltige Wettbewerbsvorteile für Adoben

Ein einheitliches konsolidiertes Kantensystem ermöglicht es Kunden, ihre Werbe-, Marketing- oder Personalisierungs-Kampagnen über alle Kanal hinweg zu verwalten.  Es ermöglicht die Erbringung von Dienstleistungen mit geringeren Gesamtbetriebskosten für Kunden. [!DNL Adobe]  Darüber hinaus trägt sie dazu bei, die Produktneuheit zu beschleunigen, indem sie die Echtzeit-Edge-Plug-ins bereitstellt und es [!DNL Adobe] und seinen Kunden ermöglicht, diesem Echtzeit-System schneller neue Funktionen und kundenspezifische Logik hinzuzufügen.

## Videoüberblick

Das folgende Video gibt einen Überblick über die Adobe Experience Platform [!DNL Web SDK] und [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck ist es, Herausforderungen zu beenden, indem Tags in der richtigen Reihenfolge ausgelöst werden müssen, die nicht mit den Versionshinweisen der Bibliothek übereinstimmen und die Abhängigkeitsverwaltung verbessert wird. Es ist eine neue Methode, um die zu implementieren [!DNL Experience Cloud] und es ist [Open Source](https://github.com/adobe/alloy).

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. This new library and endpoint can retrieve an ID, fetch a [!DNL Target] experience, send data to [!DNL Audience Manager], and pass the data to the Adobe Experience Platform in a single call.

Das folgende Video zeigt die Adobe Experience Platform [!DNL Web SDK] und die [!DNL Edge Network] Aktion. Das Videobeispiel verwendet einen einzigen Aufruf an die Adobe, der Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]und [!DNL Target]sendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

## Erste Schritte

Wir empfehlen Ihnen dringend, [sich in unserer Anleitung](getting-started/quick-start-with-launch.md) für die ersten Schritte mit Adobe Launch einen kurzen Überblick zu verschaffen.

Dieses Produkt entwickelt sich ständig und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um auf dem neuesten Stand zu sein, schauen Sie sich unser [unterstütztes Gebrauchsanweisung](https://github.com/adobe/alloy/projects/5)an. Wir halten dies auf dem neuesten Stand mit den derzeit unterstützten Anwendungsfällen und den Fällen, an denen wir arbeiten, damit Sie die bestmöglichen Entscheidungen treffen können.

* **Anwendungsfälle, die noch nicht unterstützt werden:** Dies sind Anwendungsfälle, die auf unserem Fahrplan stehen und in Zukunft unterstützt werden sollen.
* **Anwendungsfälle:** Dies sind die Anwendungsfälle, mit denen das Team derzeit arbeitet, um die Veröffentlichung abzuschließen.
* **Unterstützte Anwendungsfälle:** Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* **Anwendungsfälle, die wir nicht unterstützen:** Dies sind die Anwendungsfälle, die wir beschlossen haben, nicht zu unterstützen.
