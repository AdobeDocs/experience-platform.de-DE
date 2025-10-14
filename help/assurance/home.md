---
title: Überblick über Adobe Experience Platform Assurance
description: Mit Adobe Experience Platform Assurance können Sie die Datenerfassung und die Bereitstellung von Erlebnissen in Ihren Mobile Apps untersuchen, testen, simulieren und überprüfen.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 6%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance ist ein Produkt von [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) mit dem Sie die Datenerfassung und die Bereitstellung von Erlebnissen in Ihrer Mobile App untersuchen, testen, simulieren und validieren können.

>[!IMPORTANT]
>
> Projekt Griffon heißt jetzt **Assurance**!
>
> Project Griffon ist jetzt allgemein für **alle** Adobe Experience Cloud-Kunden als Assurance verfügbar. Weitere Informationen zu dieser Umstellung finden Sie im [Handbuch für den Benutzerzugriff](./user-access.md).

>[!INFO]
>
>Öffentliche Assurance-APIs sind verfügbar!
>
>[Die Assurance-APIs](https://developer.adobe.com/adobe-assurance-public-apis/) sind eine Sammlung von APIs, mit denen Benutzende ihre Web- und Mobile Apps testen und debuggen können, wenn sie mit der Adobe Assurance Mobile SDK ausgestattet sind.

## Allgemeine Verfügbarkeit

Ab dem 15. Oktober 2022 ist Assurance allgemein für alle Adobe Experience Cloud verfügbar.

### Was ändert sich?

Am 15. Oktober wird der Zugriff auf Assurance über Admin Console verwaltet. Lesen Sie das [Benutzerhandbuch“, &#x200B;](./user-access.md) sicherzustellen, dass Sie weiterhin unterbrechungsfreien Zugriff haben.

Für bestehende Assurance-Integrationen, -Sitzungen und -Ereignisse werden keine weiteren Änderungen oder Unterbrechungen erwartet. Der Zugriff auf Assurance kann über [https://griffon.adobe.com](https://griffon.adobe.com) fortgesetzt werden **oder** Sie können (und ein Lesezeichen) [https://experience.adobe.com/assurance verwenden](https://experience.adobe.com/assurance).

## Was kann Assurance für Sie tun?

### Schnelleinrichtung

Beginnen Sie in Eile mit wenigen Codezeilen. Bei mobilen Apps unterstützt Assurance Sie mit dem Adobe Experience Platform Mobile SDK dabei, App-Ereignisse, Standortsignale, Konfigurationsparameter, SDK-Protokolle, Geräteinformationen und mehr zu untersuchen, zu simulieren und zu validieren.

### Unkomplizierte Verbindung

Mit Assurance ist die Verbindung Ihrer App mit Experience Platform einfach und zuverlässig. Sie müssen keine Netzwerk-Proxys ([MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) und andere Netzwerkgymnastiken verwenden - die Verbindung Ihrer App mit Assurance ist so einfach wie das Scannen eines QR-Codes oder das Tippen auf eine Schaltfläche.

![](./images/index/no-hassle-connection.png)

### Echtzeitinspektion, -simulation und -validierung

Nachdem Sie eine Verbindung zu Assurance hergestellt haben, können Sie Live-Streaming-App-Ereignisse und -Aktivitäten untersuchen sowie filtern und suchen, um Rauschen zu beseitigen. Ereignisse enthalten Details zur Validierung, zum Debugging und zur Fehlerbehebung bei der Implementierung Ihrer Mobile App. Mit Assurance können Sie auch Screenshots erstellen, Standortsignale simulieren und vieles mehr in Echtzeit.

![](./images/index/real-time-insepction.png)

### Integration mit Adobe Experience Cloud

Client-seitige Daten und Erlebnisse werden durch die Art und Weise kontextualisiert, wie Benutzer Berichtsregeln, Aktivitäten und Kampagnen auf unseren Marketing-orientierten Benutzeroberflächen einrichten. Um Ihnen die Verbindung zwischen den beiden zu erleichtern, integrieren wir mit Adobe Experience Cloud-Lösungen wie Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service und mehr.

![](./images/index/integration.png)

## Funktionen

### Ereignisse, Protokolle und mehr zu Adobe Experience Platform Mobile SDK

Mit Assurance können Sie unformatierte SDK-Ereignisse untersuchen, die von Adobe Experience Platform Mobile SDK generiert wurden. Alle von der SDK erfassten Ereignisse stehen zur Einsicht bereit. SDK-Ereignisse werden in einer Listenansicht geladen, sortiert nach Zeit. Jedes Ereignis verfügt über eine Detailansicht, die weitere Details enthält. Zusätzliche Ansichten zum Durchsuchen der SDK-Konfiguration, Datenelemente, freigegebenen Status und SDK-Erweiterungsversionen sind ebenfalls verfügbar.

### Adobe Analytics

Die Ansicht Adobe Analytics > Analytics-Ereignisse ist eine fokussierte Ansicht, die Ereignisse im Zusammenhang mit Ihrer Adobe Analytics Mobile-Implementierung anzeigt. Die Listenansicht zeigt den Lebenszyklus- oder Aktions-/Statusereignis-Status nach der Verarbeitung zusammen mit den erforderlichen Ereignisdetails in einer speziell formatierten Ansicht an. Der Status Nachbearbeitet zeigt an, wie das Ereignis von Adobe Analytics verarbeitet wurde, nachdem Verarbeitungsregeln auf das Ereignis angewendet wurden.

### Adobe Analytics für Streaming Media

Die Ansicht Adobe Analytics > Media Analytics-Ereignisse zeigt Ereignisse für Ihre Audio- und Videoanalyseimplementierung an. Die Ereignisdetailansicht zeigt Standard- und benutzerdefinierte Metadaten an, die für jede Wiedergabesitzung verfolgt werden. Darüber hinaus können Sie den Status „Nachbearbeitet“ und nachbearbeitete Media Analytics-Daten anzeigen, z. B. Besuchszeit für Medien oder Gesamtdauer des Puffers.

### Places (Standortdienste)

Die Ansicht Standort-Services ist eine Ansicht auf dem Gerät, die die Ein- und Ausstiegsereignisse des Benutzerstandorts anzeigt, um eine einfache Validierung zu ermöglichen. Diese praktische Ansicht bietet eine praktische Schnittstelle zum Anzeigen standortspezifischer Datenpunkte zur Überprüfung auf dem Client für kontextbezogenes Debugging.

## Ist Assurance sicher?

Assurance verfügt über die folgenden Sicherheitsmaßnahmen:

* Sowohl Assurance als auch die Assurance-Web-Benutzeroberfläche verfügen über einen sicheren, PIN-basierten Handshake für eine Verbindung. Der Benutzer muss explizit einen Handshake erstellen, um zu verhindern, dass „versehentliche“ Assurance-Verbindungen von einem Endbenutzer erstellt werden.
* Es werden nur Verbindungen zwischen Assurance und der Assurance-Web-Benutzeroberfläche unterstützt, die zur selben Adobe Experience Cloud-Organisations-ID gehören.
* Adobe Experience Platform Mobile SDKs-Ereignisse werden über HTTPS übertragen.
* Assurance und Adobe Experience Platform Mobile SDKs verwenden TLS 1.2
* Assurance-Sitzungen werden nach 30 Tagen gelöscht.
* Assurance-Sitzungsdaten werden im Ruhezustand gemäß den Best Practices für die Speicherung verschlüsselt.

## Erste Schritte

Um Assurance einzurichten, müssen Sie zunächst die Assurance-Erweiterung in Ihrer Anwendung installieren. Um zu erfahren, wie Sie dies tun können, lesen Sie das Tutorial [Implementieren der Assurance-Erweiterung](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Nachdem Sie Assurance zu Ihrer App hinzugefügt haben, können Sie eine Assurance-Sitzung erstellen, die mit Ihrem Gerät verbunden werden kann. Um zu erfahren, wie Sie Assurance verwenden, lesen Sie bitte das [Handbuch zur Verwendung von Assurance](./tutorials/using-assurance.md).
