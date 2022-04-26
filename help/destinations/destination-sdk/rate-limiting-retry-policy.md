---
description: Erfahren Sie, wie Experience Platform mit verschiedenen Fehlertypen umgeht, die von Streaming-Zielen zurückgegeben werden, und wie es erneut versucht, Daten an die Zielplattform zu senden.
title: Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele, die mit Destination SDK erstellt wurden
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 4%

---

# Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele, die mit Destination SDK erstellt wurden

## Übersicht {#overview}

Partnerdefinierte Ziele können verschiedene Fehler zurückgeben und unterschiedliche Ratenbegrenzungsrichtlinien haben. Auf dieser Seite wird erläutert, wie Experience Platform mit verschiedenen Fehlertypen umgeht, die von Streaming-Zielen zurückgegeben werden.

Bei der Konfiguration eines Ziels mithilfe von Destination SDK können Sie zwischen zwei Aggregattypen wählen: [Aggregation des besten Aufwands](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) und [konfigurierbare Aggregation](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Je nach ausgewähltem Aggregationstyp können Sie im Folgenden nachlesen, wie Experience Platform mit Fehlern und Ratenbeschränkungen umgeht.

## Best-Effort-Aggregation {#best-effort-aggregation}

Bei allen HTTP-Aufrufen an Ihr Ziel, die fehlschlagen, versucht Experience Platform, den Aufruf unmittelbar nach dem ersten Aufruf erneut durchzuführen. Wenn der Aufruf beim zweiten Versuch immer noch fehlschlägt, löscht Experience Platform den Aufruf und versucht ihn nicht erneut, es erneut zu versuchen.

## Konfigurierbare Aggregation {#configurable-aggregation}

Bei Zielplattformen, die mit konfigurierbarer Aggregation eingerichtet werden, unterscheidet die Experience Platform zwischen dem von Ihrer Plattform zurückgegebenen Fehlertyp:

* Fehler, bei denen Experience Platform erneut versucht, die Daten an Ihre Plattform zu senden:
   * HTTP-Antwortcodes 420 und 429
   * HTTP-Antwort-Codes größer als 500
* Fehler bei Experience Platform *nicht* Versuchen Sie erneut, die Daten an Ihre Plattform zu senden: alle anderen von Ihrer Plattform zurückgegebenen

### Erneuter Versuch beschrieben {#retry-approach}

Der Ansatz der Experience Platform für konfigurierbare Aggregationen wird nachfolgend beschrieben. In diesem Beispiel wird davon ausgegangen, dass Experience Platform Daten an eine Zielplattform sendet, die 429-Fehler-Codes zurückgibt, wenn sie mehr als 50.000 Anfragen pro Minute erhält:

* Minute 1: Experience Platform sammelt 40.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 40.000 HTTP-Anfragen durch und alle sind erfolgreich.
* Minute 2: Experience Platform sammelt 70.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 70.000 HTTP-Anfragen durch und 50.000 sind erfolgreich. Die anderen 20.000 Personen erhalten von Ihrem Endpunkt einen Fehler zur Ratenbegrenzung und werden in 30 Minuten erneut versucht.
* Minute 3: Experience Platform sammelt 30.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 30.000 HTTP-Anfragen durch und alle sind erfolgreich.
* ...
* ...
* Minute 32: Experience Platform versucht erneut, die 20.000 Batches zu senden, die in Minute 2 fehlgeschlagen sind. Alle Aufrufe sind erfolgreich.

## Nächste Schritte {#next-steps}

Sie wissen jetzt, wie Experience Platform Fehler behandelt und die Ratenbegrenzung von Zielplattformen entsprechend der Aggregationsrichtlinie begrenzt, die Sie beim Konfigurieren Ihres Streaming-Ziels ausgewählt haben. Als Nächstes können Sie die folgende Dokumentation lesen:

* [Testen einer Zielkonfiguration](/help/destinations/destination-sdk/test-destination.md)
* [Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung](/help/destinations/destination-sdk/submit-destination.md)
