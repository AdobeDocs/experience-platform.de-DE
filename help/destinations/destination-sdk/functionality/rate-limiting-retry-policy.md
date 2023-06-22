---
description: Erfahren Sie, wie Experience Platform mit verschiedenen Fehlertypen umgeht, die von Streaming-Zielen zurückgegeben werden, und wie es erneut versucht, Daten an die Zielplattform zu senden.
title: Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele, die mit Destination SDK erstellt wurden
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: ht
source-wordcount: '426'
ht-degree: 100%

---

# Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele, die mit Destination SDK erstellt wurden

Partnerdefinierte Ziele können verschiedene Fehler zurückgeben und unterschiedliche Ratenbegrenzungsrichtlinien haben. Auf dieser Seite wird erläutert, wie Experience Platform mit verschiedenen Fehlertypen umgeht, die von Streaming-Zielen zurückgegeben werden.

Bei der Konfiguration eines Ziels mithilfe von Destination SDK können Sie zwischen zwei Aggregattypen wählen: [Löschen einer Zielgruppenvorlage](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) und [konfigurierbare Aggregation](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Je nach ausgewähltem Aggregationstyp können Sie im Folgenden nachlesen, wie Experience Platform mit Fehlern und Ratenbeschränkungen umgeht.

## Aggregation nach bestem Bemühen (Best-Effort-Aggregation) {#best-effort-aggregation}

Bei allen HTTP-Aufrufen an Ihr Ziel, die fehlschlagen, versucht Experience Platform, den Aufruf unmittelbar nach dem ersten Aufruf einmal erneut durchzuführen. Wenn der Aufruf beim zweiten Versuch immer noch fehlschlägt, löscht Experience Platform den Aufruf und versucht ihn nicht ein drittes Mal.

## Konfigurierbare Aggregation {#configurable-aggregation}

Bei Zielplattformen, die mit konfigurierbarer Aggregation eingerichtet werden, unterscheidet Experience Platform zwischen den von Ihrer Plattform zurückgegebenen Fehlertypen:

* Fehler, bei denen Experience Platform erneut versucht, die Daten an Ihre Plattform zu senden:
   * HTTP-Antwort-Codes 420 und 429
   * HTTP-Antwort-Codes größer als 500
* Fehler, bei denen Experience Platform *nicht versucht*, erneut die Daten an Ihre Plattform zu senden: alle anderen von Ihrer Plattform zurückgegebenen

### Beschreibung, wie das erneuter Versuchen abläuft {#retry-approach}

Nachfolgend wird der Ansatz von Experience Platform für konfigurierbare Aggregationen beschrieben. In diesem Beispiel wird davon ausgegangen, dass Experience Platform Daten an eine Zielplattform sendet, die Fehler-Codes 429 zurückgibt, wenn sie mehr als 50.000 Anfragen pro Minute erhält:

* Minute 1: Experience Platform aggregiert 40.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 40.000 HTTP-Anfragen durch und alle sind erfolgreich.
* Minute 2: Experience Platform aggregiert 70.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 70.000 HTTP-Anfragen durch, von denen 50.000 erfolgreich sind. Für die übrigen 20.000 wird von Ihrem Endpunkt ein Fehler wegen Ratenbegrenzung gemeldet, und sie werden 30 Minuten später erneut versucht.
* Minute 3: Experience Platform aggregiert 30.000 Batches mit Profilen, die an Ihre Zielplattform gesendet werden. Experience Platform führt 30.000 HTTP-Anfragen durch und alle sind erfolgreich.
* ...
* ...
* Minute 32: Experience Platform versucht erneut, die 20.000 Batches zu senden, die in Minute 2 fehlgeschlagen sind. Alle Aufrufe sind erfolgreich.

## Nächste Schritte {#next-steps}

Sie wissen jetzt, wie Experience Platform Fehler behandelt und die Ratenbegrenzung von Zielplattformen entsprechend der Aggregationsrichtlinie anwendet, die Sie beim Konfigurieren Ihres Streaming-Ziels ausgewählt haben. Als Nächstes können Sie die folgende Dokumentation lesen:

* [Testen einer Zielkonfiguration](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung](../guides/submit-destination.md)
