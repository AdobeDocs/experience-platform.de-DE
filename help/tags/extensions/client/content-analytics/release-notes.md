---
title: Versionshinweise zur Adobe Content Analytics-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung "Content Analytics" in Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 057d1ad8d61ed386a777175026a3f01f21541389
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Versionshinweise zur Adobe Content Analytics-Erweiterung

Im Folgenden finden Sie eine Liste der Versionshinweise für die Content Analytics-Tag-Erweiterung.

| Version | Datum | Fehlerbehebungen |
|---|---|---|
| 1.0.52 | &#x200B;27. April 2026 | <ul><li>Es wurde ein Tracking für Assets hinzugefügt, bei denen Bilder im Hintergrund eines Elements im DOM von CSS geladen werden.</li><li>Es wurde ein hartcodiertes `permanentlyBlockedURLs`-Array hinzugefügt, das [maps.googleapis.com](https://maps.googleapis.com) und [mapsresources-pa.googleapis.com](https://mapsresources-pa.googleapis.com) enthält. Diese URLs sind in der Content Analytics-Bibliothek standardmäßig immer blockiert.</li><li>`idSource`- und `channel` zu XDM-Datenerfassungsanfragen hinzugefügt.</li></ul> |
| 1.0.51 | &#x200B;13. März 2026 | <ul><li>Es wurde ein kleinerer Fehler behoben, der dazu führen konnte, dass `experienceIDs` beim Navigieren zwischen Seiten zwischengespeichert wurden.</li><li>Es wurde ein Problem mit der Erfassung von Erlebnisabfragezeichenfolgen behoben. Abfrageparameter funktionieren wie folgt:<ul><li>Das Feld Abfrageparameter ist leer: In der Erlebnis-ID werden keine Abfragezeichenfolgenparameter erfasst.</li><li>Abfrageparameter werden explizit definiert (z. B. 1, 2, 3): Nur diese Abfragezeichenfolgenparameter und -werte werden in der Erlebnis-ID erfasst.</li><li>Der Abfrageparameter ist auf einen Platzhalter (`.*`) festgelegt: Die gesamte Zeichenfolge document.location.search ist in der URL enthalten.</li></ul></li></ul> |
| 1.0.49 | &#x200B;12. September 2025 | <ul><li>Es wurde ein kleinerer Fehler behoben, der dazu führte, dass die Benutzeroberfläche der Tags-Erweiterung überhaupt nicht geladen wurde, wenn der Benutzer keine Datenstromberechtigungen hatte. Die Benutzeroberfläche zeigt jetzt in der Option Datenstrom **[!UICONTROL Choose from list]** eine Warnung zu Berechtigungen an und ermöglicht es den Benutzenden weiterhin, Werte manuell einzugeben.</li><li>Ein Pfadproblem für l10n wurde aktualisiert.</li><li>Es wurde ein Problem behoben, bei dem einige Bilder, die untergeordnete Elemente von übergeordneten Elementen waren, die kein Bild waren, Asset-Klicks für diese untergeordneten Bildelemente nicht korrekt erfassten.</li><li>Wenn ein Benutzer das WebSDK in Tags mit einem anderen Instanznamen als `alloy` konfiguriert hat, erkennt die Content Analytics-Bibliothek die erste Instanz der WebSDK-Bibliothek und verwendet diese zum Senden von Content Analytics-Ereignissen.</li></ul> |
| 1.0.48 | &#x200B;25. August 2025 | <ul><li>Fügt Unterstützung für das Tracking von Assets in den Schatten-Stamm-DOM-Elementen eines Dokuments hinzu.</li></ul> |
| 1.0.47 | &#x200B;23. Juli 2025 | <ul><li>Es wurde ein Fehler behoben, der auftrat, wenn Erlebnisse nicht aktiviert waren, was dazu führte, dass die Prüfung regulärer Ausdrücke auf Erlebnisse fehlschlug. Aufgrund dieses Problems konnten keine Content Analytics-Daten erfasst werden.</li><li>Es wurde ein Problem mit der Standardspracheinstellung behoben, das dazu führte, dass die Tags-Benutzeroberfläche für einige Benutzende, deren primäre Standardsprache nicht in Experience Cloud festgelegt war, nicht angezeigt wurde.</li></ul> |
| 1.0.46 | &#x200B;18. Juni 2025 | <ul><li>Beim Versuch, die Erweiterungskonfiguration zu speichern, wurde eine Popup-Benachrichtigung hinzugefügt, wenn kein Produktionsdatenstrom vorhanden ist.</li><li>Das Problem mit der Sichtbarkeit der Content Analytics-Payload wurde vorübergehend behoben, indem die stringisierten Payload-Inhalte stattdessen in der Konsole platziert wurden.</li><li>Es wurde Lokalisierungsunterstützung zur Erweiterungs-Benutzeroberfläche hinzugefügt.</li><li>Ein CSS-Problem, das zu einem zusätzlichen Abstand um den Inhalt der Erweiterungs-Benutzeroberfläche führte, wurde teilweise behoben.</li></ul> |
| 1.0.45 | &#x200B;14. April 2025 | <ul><li>Es wurden mehrere Fehler in den Konfigurationseinstellungen behoben, die sich auf das Halten von Content Analytics-Ereignissen beim Warten auf Seitenansichtsereignisse bezogen. Content Analytics wartet jetzt standardmäßig, bis Ereignisse ausgelöst werden, bis das erste Seitenansichtsereignis eintritt.</li></ul> |
| 1.0.44 | &#x200B;31. März 2025 | <ul><li>Erste Iteration der AppMeasurement-Integration.</li><li>Diese Version unterstützt noch nicht die Filterung spezifischer Anfragen (z. B. Seitenansichten), diese Funktion kann jedoch in einer zukünftigen Aktualisierung hinzugefügt werden. Derzeit wird die erste AppMeasurement-Instanz auf der Seite verwendet.</li></ul> |
| 1.0.43 | &#x200B;10. März 2025 | <ul><li>Erste Erweiterungsversion.</li></ul> |
