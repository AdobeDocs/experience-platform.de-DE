---
title: Versionshinweise zur Adobe Content Analytics-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung "Content Analytics" in Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Versionshinweise zur Adobe Content Analytics-Erweiterung

Im Folgenden finden Sie eine Liste der Versionshinweise für die Content Analytics-Tag-Erweiterung.

| Version | Datum | Fehlerbehebungen |
|---|---|---|
| <p>1,0,47</p> | <p>&#x200B;23. Juli 2025</p> | <ul><li>Behebt den Fehler, auf den ein Kunde gestoßen ist, wenn Erlebnisse nicht aktiviert waren und die Prüfung des regulären Ausdrucks auf Erlebnisse fehlgeschlagen ist. Dies führt dazu, dass Content Analytics-Daten nicht erfasst werden.</li><li>Behebung des Standardsprachfehlers, der verhinderte, dass die Tags-Benutzeroberfläche für einige Benutzer angezeigt wurde, wenn deren primäre Standardsprache nicht in Experience Cloud festgelegt war.</li></ul> |
| <p>1,0,46</p> | <p>&#x200B;18. Juni 2025</p> | <ul><li>Fügt eine Popup-Benachrichtigung hinzu, wenn beim Versuch, die Erweiterungskonfiguration zu speichern, kein Produktionsdatenstrom vorhanden ist.</li><li>Repariert vorübergehend die Sichtbarkeit der Content Analytics-Payload, platziert jedoch den stringisierten Inhalt der Content Analytics-Payload in der Konsole.</li><li>Fügt Lokalisierung zur Erweiterungs-Benutzeroberfläche hinzu.</li><li>Es wurde ein CSS-Problem mit zusätzlichem Abstand zum Inhalt der Erweiterungs-Benutzeroberfläche teilweise behoben.</li></ul> |
| <p>1,0,45</p> | <p>&#x200B;14. April 2025</p> | <ul><li>Behebt einige Fehler in den Konfigurationseinstellungen für beim Halten von Content Analytics-Ereignissen beim Warten auf Seitenansichtsereignisse. Jetzt wartet Content Analytics standardmäßig, bis Ereignisse ausgelöst werden, bis das erste Seitenansichtsereignis eintritt.</li></ul> |
| <p>1,0,44</p> | <p>&#x200B;31. März 2025</p> | <ul><li>Erste Iteration der AppMeasurement-Integration.</li><li>Diese Version unterstützt nicht die Filterung nach bestimmten Anfragen (z. B. Seitenansichten), kann aber zu einem späteren Zeitpunkt hinzugefügt werden.  Hierbei wird auch die erste AppMeasurement-Instanz auf der Seite verwendet.</li></ul> |
| <p>1,0,43</p> | <p>&#x200B;10. März 2025</p> | <ul><li>Erste Erweiterungsversion.</li></ul> |

