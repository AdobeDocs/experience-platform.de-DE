---
keywords: Experience Platform;Home;beliebte Themen;Quellen;Integration;Fehlerbehebung;Fehlerbehebung;Quellquellen FAQ;FAQ;Quellschnittstellen;Quellanschluss;Quellschnittstellen-FAQ;Fehlerbehebung bei den Quellschnittstellen; Fehlerbehebung bei den Quellschnittstellen;
solution: Experience Platform
title: Fehlerbehebung bei Quellen
topic: troubleshooting
description: Dieses Dokument beantwortet häufig gestellte Fragen zu Quellen auf Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
translation-type: tm+mt
source-git-commit: 827a593c046530edba701edf26d9a47918cfd8f8
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# (Beta) Anleitung zur Fehlerbehebung bei Quellen

Dieses Dokument beantwortet häufig gestellte Fragen zu Quellen auf Adobe Experience Platform. Weitere Informationen zu Fragen und zur Fehlerbehebung in Zusammenhang mit anderen [!DNL Platform]-Diensten, einschließlich solcher, die in allen [!DNL Platform]-APIs gefunden werden, finden Sie im Handbuch [Experience Platform Fehlerbehebung](../landing/troubleshooting.md).

## Häufig gestellte Fragen 

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Quellen.

### Muss ich Änderungen an unseren Netzwerksicherheitseinstellungen vornehmen, um Quellen zu aktivieren?

Eventuell müssen Sie bestimmte IP-Adressen in Zulassungslisten eingeben, um Quellen zu aktivieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem jeweiligen Quell-Connector.

### Welche Authentifizierungstypen werden von Quellen unterstützt?

Quellen können mithilfe von Verbindungszeichenfolgen, Benutzernamen und Kennwörtern oder Zugriffstoken und Schlüsseln authentifiziert werden. Genauere Informationen zu unterstützten Authentifizierungstypen finden Sie in der Dokumentation zum angegebenen Quell-Connector.

### Warum scheitern alle meine letzten Ströme?

Wenn Sie bemerken, dass alle zuletzt ausgeführten Vorgänge fehlgeschlagen sind, haben sich Ihre Anmeldeinformationen möglicherweise geändert oder abgelaufen. Um dieses Problem zu beheben, versuchen Sie, Ihre Verbindung mit den neuesten Anmeldedaten zu aktualisieren.

### Welche Dateitypen werden unterstützt?

Derzeit werden die Dateitypen durch Trennzeichen, JSON und Parquet unterstützt.

### Welche Einschränkungen gelten für Dateinamen und Dateigrößen?

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie für Dateien in Quellen berücksichtigen müssen.

- Name der Verzeichnis- und Dateikomponenten darf 255 Zeichen nicht überschreiten.
- Ordner- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Sofern vorhanden, wird sie automatisch entfernt.
- Die folgenden Zeichen für die reservierte URL müssen ordnungsgemäß mit Escape-Zeichen versehen sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundlegende Regeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punkt (.) und zwei Punkt (..).
- Die maximale Anzahl an Dateien pro Stapel beträgt 1500, wobei die maximale Stapelgröße 100 GB beträgt.
- Die maximale Anzahl von Eigenschaften oder Feldern pro Zeile beträgt 10.000.
- Die maximale Anzahl von Stapeln, die pro Benutzer pro Minute gesendet werden können, beträgt 138.

### Welche Datentypen werden unterstützt?

Unterstützte Datentypen sind Ganzzahlen, Zeichenfolgen, Boolesche Werte, Datenzeitobjekte, Arrays und Objekte.

### Welche Datums- und Uhrzeitformate werden unterstützt?

Quellen unterstützen eine Vielzahl von Datenzeitformaten bei der Erfassung von Daten. Weitere Informationen zu unterstützten Datenzeitformaten finden Sie im Abschnitt &quot;Daten&quot;des Handlungshandbuchs [Datenformat](../data-prep/data-handling.md#dates) in der Datenvorbereitung.

### Wie formatiere ich Arrays in CSV-, JSON- und Parquet-Dateien?

JSON- und Parquet-Dateien unterstützen nativ Arrays. Bei flachen Strukturen wie CSVs werden Arrays nicht unterstützt. Zeichenfolgen mit mehreren Werten können jedoch mithilfe von Datenvorgabefunktionen wie Explode und join in ein Array aufgeteilt werden. Weitere Informationen zu diesen Datenvorgabefunktionen finden Sie im Handbuch [Datenvorgabefunktionen](../data-prep/functions.md#string)

### Welche Quellen unterstützen die teilweise Erfassung?

Alle Stapelverarbeitungsquellen unterstützen die teilweise Erfassung. Streaming-Erfassungsquellen unterstützen jedoch keine teilweise Erfassung.

### Wann sollte ich eine partielle Einnahme anwenden?

Die teilweise Erfassung sollte verwendet werden, wenn Sie **nicht** Beschränkungen haben, z. B. wenn die gesamte Datei in die Plattform aufgenommen wird. Alternativ sollte eine partielle Erfassung verwendet werden, wenn Sie nicht daran interessiert sind, Daten zu erfassen, die Fehler enthalten können.

### Was ist der typische Fehlerschwellenwert bei der partiellen Erfassung?

Es gibt keinen &quot;typischen Fehlerschwellenwert&quot;für die teilweise Erfassung. Stattdessen kann dieser Wert von Anwendungsfall zu Anwendungsfall variieren. Standardmäßig ist der Fehlerschwellenwert auf 5 % festgelegt.
