---
title: Adobe Experience Platform Web SDK – Hilfe
seo-title: Adobe Experience Platform Web SDK – Hilfe
description: Erfahren Sie, was das Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Kunden von Adobe Experience Cloud die Interaktion mit den verschiedenen Diensten in der Experience Cloud ermöglichen.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 33%

---


# Was ist das Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is a client-side JavaScript library that allows customers of the Adobe Experience Cloud to interact with the various services in the [!DNL Experience Cloud] through the Adobe [!DNL Experience Platform Edge Network].

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

Das folgende Video zeigt die Adobe Experience Platform [!DNL Web SDK] und die [!DNL Edge Network] Aktion. Im Videobeispiel wird ein einzelner Aufruf an Adobe verwendet, der Daten an [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]und [!DNL Target]sendet.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)


## Erste Schritte

Wir empfehlen Ihnen dringend, sich unsere Anleitung [zu den ersten Schritten mit Adobe Launch](getting-started/quick-start-with-launch.md) anzuschauen.

Dieses Produkt entwickelt sich ständig und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um auf dem neuesten Stand zu sein, schauen Sie sich unser [unterstütztes Gebrauchsanweisung](https://github.com/adobe/alloy/projects/5)an. Wir halten dies auf dem neuesten Stand mit den derzeit unterstützten Anwendungsfällen und den Fällen, an denen wir arbeiten, damit Sie die bestmöglichen Entscheidungen treffen können.

* __Anwendungsfälle, die noch nicht unterstützt__ werden - Dies sind Anwendungsfälle, die auf unserem Plan stehen und in Zukunft unterstützt werden sollen.
* __Anwendungsfälle noch nicht abgeschlossen__ - Dies sind die Anwendungsfälle, mit denen das Team derzeit arbeitet.
* __Unterstützte Anwendungsfälle__ - Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* __Nutzungsszenarien, die wir nicht unterstützen__ - dies sind die Anwendungsfälle, die wir beschlossen haben, nicht zu unterstützen.
