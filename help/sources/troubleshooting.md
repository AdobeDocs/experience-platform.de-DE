---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Aufnahme;Fehlerbehebung;Fehlerbehebung bei Quellen;Häufig gestellte Fragen zu Quellen;Häufig gestellte Fragen;Quell-Connectoren;Quell-Connector;Häufig gestellte Fragen zu Quell-Connectoren;Fehlerbehebung bei Quell-Connectoren,
solution: Experience Platform
title: Fehlerbehebung bei Quellen
description: In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zu Quellen in Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 100%

---

# Handbuch zur Fehlerbehebung bei Quellen

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zu Quellen in Adobe Experience Platform. Fragen und Antworten zur Fehlerbehebung bei anderen [!DNL Platform]-Diensten, einschließlich solcher, die für alle [!DNL Platform]-APIs gelten, finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

## Häufig gestellte Fragen

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Quellen.

### Muss ich Änderungen an unseren Netzwerksicherheitseinstellungen vornehmen, um Quellen zu aktivieren?

Möglicherweise müssen Sie bestimmte IP-Adressen auf die Zulassungsliste setzen, um Quellen zu aktivieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem jeweiligen Quell-Connector.

### Welche Authentifizierungsarten werden von Quellen unterstützt?

Quellen können mithilfe von Verbindungszeichenfolgen, Benutzernamen und Kennwörtern oder Zugriffstoken und -schlüsseln authentifiziert werden. Spezifische Details zu unterstützten Authentifizierungsarten finden Sie in der Dokumentation des jeweiligen Quell-Connectors.

### Warum schlagen alle meine aktuellen Durchläufe fehl?

Wenn Sie feststellen, dass alle Ihre letzten Durchläufe fehlgeschlagen sind, haben sich Ihre Anmeldedaten entweder geändert oder sind abgelaufen. Um dieses Problem zu beheben, versuchen Sie, Ihre Verbindung mit den neuesten Anmeldedaten zu aktualisieren.

### Welche Dateitypen werden unterstützt?

Derzeit werden die folgenden Dateitypen unterstützt: Dateien mit Trennzeichen, JSON und Parquet.

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

### Welche Datums- und Zeitformate werden unterstützt?

Quellen unterstützen eine Vielzahl von Datums- und Zeitformaten bei der Datenaufnahme. Weitere Informationen über die unterstützten Datums- und Zeitformate finden Sie im Abschnitt „Datumsangaben“ im [Handbuch zur Handhabung von Datenformaten](../data-prep/data-handling.md#dates) in der Datenvorbereitungs-Dokumentation.

### Wie formatiere ich Arrays in CSV-, JSON- und Parquet-Dateien?

JSON- und Parquet-Dateien unterstützen nativ Arrays. Bei flachen Strukturen, wie beispielsweise CSVs werden Arrays nicht unterstützt. Zeichenfolgen mit mehreren Werten können jedoch mithilfe von Datenvorbereitungsfunktionen wie Explodieren und Verbinden in ein Array aufgeteilt werden. Weitere Informationen zu diesen Datenvorbereitungsfunktionen finden Sie im [Handbuch der Datenvorbereitungsfunktionen](../data-prep/functions.md#string)

### Welche Quellen unterstützen die partielle Aufnahme?

Alle Batch-Aufnahme-Quellen unterstützen eine partielle Aufnahme. Streaming-Aufnahme-Quellen unterstützen jedoch keine partielle Aufnahme.

### Wann sollte ich die partielle Aufnahme verwenden?

Die partielle Aufnahme sollte verwendet werden, wenn Sie **keine** Einschränkungen haben, z.B. dass die gesamte Datei in Platform aufgenommen werden muss. Als Alternative bietet sich eine partielle Aufnahme an, sofern Sie bereit sind, Daten aufzunehmen, die Fehler enthalten können.

### Was ist der typische Fehlerschwellenwert bei der partiellen Aufnahme?

Es gibt keinen „typischen Fehlerschwellenwert“ bei der partiellen Aufnahme. Vielmehr kann dieser Wert von einem Anwendungsfall zum anderen variieren. Standardmäßig ist der Fehlerschwellenwert auf 5 % festgelegt.

### Wie lange dauert es, bis der Status eines Flussdurchgangs nach der Erstellung eines neuen Datenflusses aktualisiert wird?

Flussdurchgänge werden nicht sofort generiert. Es kann etwa zwei bis drei Minuten dauern, bis sie nach der zugewiesenen `startTime` aktualisiert werden. Beim Überprüfen des Status eines Flussdurchgangs werden unmittelbar nach der Erstellung eines neuen Datenflusses keine `lastRunDetails`-Informationen zum Flussdurchgang zurückgegeben, weil dieser noch nicht stattgefunden hat. Es wird empfohlen, der Generierung des Datenflusses einige Minuten Zeit zu geben, bevor der Status des Flussdurchgangs überprüft wird.