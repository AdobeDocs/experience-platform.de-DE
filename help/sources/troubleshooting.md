---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Erfassung; Fehlerbehebung; Fehlerbehebung; Quellen FAQ; FAQ; Quell-Connectoren; Quell-Connector; FAQ für Quell-Connectoren; Fehlerbehebung bei Quell-Connectoren;
solution: Experience Platform
title: Fehlerbehebung bei Quellen
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Quellen in Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 18%

---

# Handbuch zur Fehlerbehebung bei Quellen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Quellen in Adobe Experience Platform. Für Fragen und Fehlerbehebung im Zusammenhang mit anderen [!DNL Platform] Dienste, einschließlich der Dienste, die in allen [!DNL Platform] APIs, siehe [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

## Häufig gestellte Fragen

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Quellen.

### Muss ich Änderungen an unseren Netzwerksicherheitseinstellungen vornehmen, um Quellen zu aktivieren?

Möglicherweise müssen Sie bestimmte IP-Adressen in Zulassungslisten eintragen, um Quellen zu aktivieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem jeweiligen Quell-Connector.

### Welche Authentifizierungstypen werden von Quellen unterstützt?

Quellen können mithilfe von Verbindungszeichenfolgen, Benutzernamen und Kennwörtern oder Zugriffstoken und -schlüssel authentifiziert werden. Spezifische Details zu unterstützten Authentifizierungstypen finden Sie in der Dokumentation zum angegebenen Quell-Connector.

### Warum schlagen alle meine aktuellen Flüsse fehl?

Wenn Sie feststellen, dass alle Ihre letzten Durchsatzausführungen fehlschlagen, können Ihre Anmeldedaten geändert oder abgelaufen sein. Um dieses Problem zu beheben, versuchen Sie, Ihre Verbindung mit den neuesten Anmeldedaten zu aktualisieren.

### Welche Dateitypen werden unterstützt?

Derzeit werden als Dateitypen getrennte Dateien, JSON und Parquet unterstützt.

### Welche Einschränkungen gelten für Dateinamen und Dateigrößen?

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie für Dateien in Quellen berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).
- Die maximale Anzahl von Dateien pro Batch beträgt 1500, wobei die maximale Batch-Größe 100 GB beträgt.
- Die maximale Anzahl von Eigenschaften oder Feldern pro Zeile beträgt 10.000.
- Die maximale Anzahl von Batches, die pro Benutzer und Minute gesendet werden können, beträgt 138.

### Welche Datentypen werden unterstützt?

Zu den unterstützten Datentypen gehören Ganzzahlen, Zeichenfolgen, Boolesche Werte, Datetime-Objekte, Arrays und Objekte.

### Welche Datums- und Uhrzeitformate werden unterstützt?

Quellen unterstützen eine Vielzahl von Datenzeitformaten bei der Erfassung von Daten. Weitere Informationen zu unterstützten Datumszeitformaten finden Sie im Abschnitt Datumsangaben im Abschnitt [Handbuch zur Handhabung von Datenformaten](../data-prep/data-handling.md#dates) in der Datenvorbereitung-Dokumentation.

### Wie formatiere ich Arrays in CSV-, JSON- und Parquet-Dateien?

JSON- und Parquet-Dateien unterstützen nativ Arrays. Bei flachen Strukturen wie CSVs werden Arrays nicht unterstützt. Zeichenfolgen mit mehreren Werten können jedoch mithilfe von Datenvorbereitungsfunktionen wie Explodieren und Verbinden in ein Array aufgeteilt werden. Weitere Informationen zu diesen Datenvorbereitungsfunktionen finden Sie im [Funktionsleitfaden für Datenvorbereitung](../data-prep/functions.md#string)

### Welche Quellen unterstützen die partielle Erfassung?

Alle Batch-Erfassungsquellen unterstützen die partielle Erfassung. Streaming-Erfassungsquellen unterstützen jedoch keine partielle Erfassung.

### Wann sollte ich die partielle Erfassung anwenden?

Wenn Sie dies tun, sollte die partielle Erfassung verwendet werden **not** haben Einschränkungen, z. B. die Aufnahme der gesamten Datei in Platform. Alternativ sollte eine partielle Erfassung verwendet werden, wenn Sie keine Daten erfassen möchten, die Fehler enthalten können.

### Was ist der typische Fehlerschwellenwert bei der partiellen Erfassung?

Es gibt keinen &quot;typischen Fehlerschwellenwert&quot;für die partielle Erfassung. Stattdessen kann dieser Wert von Anwendungsfall zu Anwendungsfall variieren. Standardmäßig ist der Fehlerschwellenwert auf 5 % festgelegt.

### Wie lange dauert es, bis ein Flusslaufstatus nach der Erstellung eines neuen Datenflusses aktualisiert wird?

Flussläufe werden nicht sofort generiert und können etwa zwei bis drei Minuten dauern, bis sie nach der Zuweisung aktualisiert werden. `startTime`. Beim Überprüfen des Status eines Flusslaufs werden unmittelbar nach der Erstellung eines neuen Datenflusses keine Informationen zum Ausführungsablauf zurückgegeben. `lastRunDetails` wie es noch nicht geschehen ist. Es wird empfohlen, den Datenfluss einige Minuten zu generieren, bevor der Status der Flussausführung überprüft wird.