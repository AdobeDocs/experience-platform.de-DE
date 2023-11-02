---
title: Testen einer Adobe Target-Implementierung mit Adobe Experience Platform Debugger
description: Erfahren Sie, wie Sie mit Adobe Experience Platform Debugger eine Website testen und debuggen können, die für Adobe Target aktiviert ist.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 98%

---

# Testen einer Adobe Target-Implementierung mit Adobe Experience Platform Debugger

Adobe Experience Platform Debugger bietet eine Suite nützlicher Tools zum Testen und Debuggen einer Website, die mit einer Adobe Target-Implementierung ausgestattet wurde. In diesem Handbuch werden einige gängige Workflows und Best Practices für die Verwendung von Platform Debugger auf einer Target-fähigen Website behandelt.

## Voraussetzungen

Um Platform Debugger für Target nutzen zu können, muss die Website die [at.js-Bibliothek](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) Version 1.x oder höher verwenden. Frühere Versionen werden nicht unterstützt.

## Initialisieren von Platform Debugger

Öffnen Sie die Website, die Sie testen möchten, in einem Browser und öffnen Sie dann die Platform Debugger-Erweiterung.

Wählen Sie **[!DNL Target]** in der linken Navigationsleiste aus. Wenn Platform Debugger erkennt, dass eine kompatible Version von at.js auf der Site ausgeführt wird, werden Adobe Target-Implementierungsdetails angezeigt.

![Die in Platform Debugger ausgewählte Target-Ansicht zeigt an, dass Adobe Target auf der aktuell angezeigten Browser-Seite aktiv ist.](../images/solutions/target/target-initialized.png)

## Globale Konfigurationsinformationen

Informationen zur globalen Konfiguration der Implementierung werden am oberen Rand der Target-Ansicht in Platform Debugger angezeigt.

![Globale Konfigurationsinformationen für Target in Platform Debugger werden hier hervorgehoben](../images/solutions/target/global-config.png)

| Name | Beschreibung |
| --- | --- |
| Clientcode | Eine eindeutige ID, die Ihre Organisation identifiziert. |
| Version | Die aktuell auf der Website installierte Version der Adobe Target-Bibliothek. |
| Globaler Anfragename | Der Name der [globalen mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) für die Target-Implementierung, wobei der Standardname `target-global-mbox` lautet. |
| Ereignis zum Laden der Seite | Ein boolescher Wert, der angibt, ob ein [Seitenladeereignis](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) stattgefunden hat. Seitenladeereignisse werden nur bei Versionen at.js 2.x unterstützt. Bei nicht kompatiblen Versionen wird dieser Wert standardmäßig auf `None` festgelegt. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Wählen Sie **[!DNL Network Requests]** aus, um zusammenfassende Informationen zu den einzelnen Netzwerkanfragen anzuzeigen, die auf der Seite durchgeführt wurden.

![Der Abschnitt [!DNL Network Requests] für Target wurde in Platform Debugger ausgewählt](../images/solutions/target/network-requests.png)

Wenn Sie Aktionen auf der Seite ausführen (einschließlich des Neuladens der Seite), werden der Tabelle automatisch neue Spalten hinzugefügt, sodass Sie die Sequenz der Aktionen und die Änderungen von Werten zwischen den einzelnen Anfragen anzeigen können.

![Der Abschnitt [!DNL Network Requests] für Target wurde in Platform Debugger ausgewählt](../images/solutions/target/new-request.png)

Die folgenden Werte werden erfasst:

| Name | Beschreibung |
| --- | --- |
| [!DNL Page Title] | Der Titel der Seite, die diese Anfrage initiiert hat. |
| [!DNL Page URL] | Die URL der Seite, die die Anfrage initiiert hat. |
| [!DNL URL] | Die unformatierte URL der Anfrage. |
| [!DNL Method] | Die HTTP-Methode für die Anfrage. |
| [!DNL Query String] | Die Abfragezeichenfolge der Anfrage, die der URL entnommen wird. |
| [!DNL POST Body] | Der Text der Anfrage (nur für POST-Anfragen festgelegt). |
| [!DNL Pathname] | Der Pfadname der Anfrage-URL. |
| [!DNL Hostname] | Der Hostname der Anfrage-URL. |
| [!DNL Domain] | Die Domain der Anfrage-URL. |
| [!DNL Timestamp] | Ein Zeitstempel in der Zeitzone des Browsers, der angibt, wann die Anfrage (oder das Ereignis) stattgefunden hat. |
| [!DNL Time Since Page Load] | Die Zeit, die zum Zeitpunkt der Anfrage seit dem ersten Laden der Seite verstrichen ist. |
| [!DNL Initiator] | Der Initiator der Anfrage. Mit anderen Worten, wer die Anfrage gestellt hat. |
| [!DNL clientCode] | Die Kennung für das Konto Ihrer Organisation, die von Target erkannt wurde. |
| [!DNL requestType] | Die für die Anfrage verwendete API. Bei Verwendung von at.js 1.x lautet der Wert `/json`. Bei Verwendung von at.js 2.x lautet der Wert `delivery`. |
| [!DNL Audience Manager Blob] | Stellt Informationen zu verschlüsselten Audience Manager-Metadaten bereit, die als „Blob“ bezeichnet werden. |
| [!DNL Audience Location Hint] | Die Regions-ID für die Datenerfassung. Dies ist eine numerische ID für den geografischen Standort eines bestimmten ID-Service-Rechenzentrums. Weitere Informationen finden Sie in der Audience Manager-Dokumentation unter [DCS-Regions-IDs, Standorte und Hostnamen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=de) sowie im Handbuch zum Experience Cloud Identity Service unter [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Die Browser-Höhe in Pixel. |
| [!DNL Browser Time Offset] | Die mit der Zeitzone des Browsers verknüpfte Zeitverschiebung. |
| [!DNL Browser Width] | Die Browser-Breite in Pixel. |
| [!DNL Color Depth] | Die Farbtiefe des Bildschirms. |
| [!DNL context] | Ein Objekt, das Kontextinformationen über den für die Anfrage verwendeten Browser enthält, einschließlich der Bildschirmmaße und Client-Plattform. |
| [!DNL prefetch] | Die Parameter, die während der `prefetch`-Verarbeitung verwendet werden. |
| [!DNL execute] | Die Parameter, die während der `execute`-Verarbeitung verwendet werden. |
| [!DNL Experience Cloud Visitor ID] | Enthält ggf. Informationen zur [Experience Cloud-ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de), die dem aktuellen Site-Besucher zugewiesen ist. |
| [!DNL experienceCloud] | Enthält die Experience Cloud-IDs für diese spezifische Benutzersitzung: eine [Zusatzdaten-ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?lang=de#section_2C1F745A2B7D41FE9E30915539226E3A) von A4T und eine [Besucher-ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de). |
| [!DNL id] | Die [Target-ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) für den Besucher. |
| [!DNL Mbox Host] | Der [Host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de), an den die Target-Anfrage gesendet wurde. |
| [!DNL Mbox PC] | Eine Zeichenfolge, die die [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)-Sitzungs-ID und den [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=de#concept_0AE2ED8E9DE64288A8B30FCBF1040934)-Standorthinweis enthält. Dieser Wert wird von at.js verwendet, um sicherzustellen, dass die Sitzung und der Edge-Standort persistent bleiben. |
| [!DNL Mbox Referrer] | Der URL-Referrer für die spezifische [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)-Anfrage. |
| [!DNL Mbox URL] | Die URL für den [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)-Server. |
| [!DNL Mbox Version] | Die Version von [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/), die verwendet wird. |
| [!DNL mbox3rdPartyId] | Die dem aktuellen Besucher zugewiesene [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=de). |
| [!DNL mboxRid] | Die [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)-Anfrage-ID. |
| [!DNL requestId] | Eine eindeutige ID für die Anfrage. |
| [!DNL Screen Height] | Die Bildschirmhöhe in Pixel. |
| [!DNL Screen Width] | Die Bildschirmbreite in Pixel. |
| [!DNL Supplemental Data ID] | Eine systemgenerierte ID, mit der Besuchende den entsprechenden Adobe Target- und Adobe Analytics-Aufrufen zugeordnet werden. Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung bei A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?lang=de#section_75002584FA63456D8D9086172925DD8D). |
| [!DNL vst] | Die [Konfiguration der Identity Service-API von Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html?lang=de). |
| [!DNL webGLRenderer] | Enthält Informationen zu dem auf der Seite verwendeten WebGL-Renderer, falls anwendbar. |

{style="table-layout:auto"}

Um die Details eines Parameters für ein bestimmtes Netzwerkereignis anzuzeigen, klicken Sie auf die betreffende Tabellenzelle. Dann wird ein Popup mit weiteren Informationen zum Parameter angezeigt, einschließlich einer Beschreibung und dessen Wert. Wenn es sich bei dem Wert um ein JSON-Objekt handelt, enthält das Dialogfeld eine vollständig navigierbare Ansicht der Objektstruktur.

![Der [!DNL Network Requests]-Abschnitt für Target, der in Platform Debugger ausgewählt wurde](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Wählen Sie **[!DNL Configuration]** aus, um eine Auswahl zusätzlicher Debugging-Werkzeuge für Target zu aktivieren oder zu deaktivieren.

![Der [!DNL Configuration Requests]-Abschnitt für Target, der in Platform Debugger ausgewählt wurde](../images/solutions/target/configuration.png)

| Debugging-Tool | Beschreibung |
| --- | --- |
| [!DNL Target Console Logging] | Wenn diese Option aktiviert ist, können Sie auf der Registerkarte „Konsole“ des Browsers auf die at.js-Protokolle zugreifen. Diese Funktion kann auch durch Hinzufügen eines `mboxDebug`-Abfrageparameters (mit beliebigem Wert) zur Browser-URL aktiviert werden. |
| [!DNL Target Diable] | Wenn diese Option aktiviert ist, sind alle Target-Funktionen auf der Seite deaktiviert. Auf diese Weise können Sie bestimmen, ob ein Target-spezifisches Angebot das Problem auf der Seite verursacht. |
| [!DNL Target Trace] | **Hinweis**: Sie müssen angemeldet sein, um diese Funktion zu aktivieren.<br><br>Wenn diese Option aktiviert ist, werden mit jeder Anfrage Tracking-Token gesendet und in jeder Antwort wird ein Trace-Objekt zurückgegeben. `at.js` analysiert die Antwort `window.__targetTraces`. Jedes Trace-Objekt enthält dieselben Informationen wie die [Registerkarte [!DNL Network Requests]] mit den folgenden Ergänzungen:<ul><li>Eine Momentaufnahme des Profils, in der Attribute vor und nach Anfragen angezeigt werden.</li><li>Übereinstimmende und nicht übereinstimmende [Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de), die zeigen, warum das aktuelle Profil für bestimmte Aktivitäten qualifiziert war oder nicht.<ul><li>Auf diese Weise lässt sich feststellen, für welche Zielgruppen sich ein Profil zu einem bestimmten Zeitpunkt qualifiziert und warum.</li><li>Zieldokumente enthalten mehr Informationen zu verschiedenen Aktivitätstypen</li></ul></li></ul> |

{style="table-layout:auto"}
