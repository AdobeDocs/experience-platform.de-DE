---
keywords: Experience Platform;Startseite;beliebte Themen;
title: Anleitung zur Fehlerbehebung bei der Datenvorbereitung
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Adobe Experience Platform-Datenvorbereitung.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 2%

---

# [!DNL Data Prep] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Prep]sowie eine Anleitung zur Fehlerbehebung für häufige Fehler. Fragen und Informationen zur Fehlerbehebung für Platform-APIs im Allgemeinen finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Adobe Experience Platform API](../landing/troubleshooting.md).

## FAQs

Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu [!DNL Data Prep] und ihre Antworten.

### Wie werden Transformationsfehler behoben?

[!DNL Data Prep] lokalisiert alle Umwandlungsfehler in die Spalte, in der sie aufgetreten sind. Daher wird diese Spalte ungültig und der Rest der Zeile wird weiterhin verarbeitet. Diese Transformationsprobleme werden protokolliert als **Warnungen**. Es wird empfohlen, die Warnungen regelmäßig zu überprüfen und die Umwandlungslogik so anzupassen, dass die Transformationsprobleme berücksichtigt werden. Dies erhöht die Qualität der in Experience Platform erfassten Daten.

Wenn die Spalten als **Erforderlich** aufgrund von Transformationsproblemen aufgehoben werden, wird die Zeile nicht erfasst. Wenn die partielle Datenerfassung aktiviert ist, können Sie den Schwellenwert für solche Zurückweisungen festlegen, bevor der gesamte Fluss fehlschlägt. Wenn sich das Attribut &quot;nullified&quot;nicht auf Überprüfungen auf Schemaebene ausgewirkt hat, wird die Zeile weiterhin erfasst.

Alle Zeilen, die ungültig sind, auch ohne Transformationsfehler, werden ebenfalls zurückgewiesen. Beispielsweise kann ein Datenaufnahme-Fluss eine Übergabe durch die Zuordnung (keine Transformationslogik) zu einem erforderlichen Feld haben und es gibt keinen eingehenden Wert für dieses Attribut. Diese Zeile wird abgelehnt.

### Wie kann ich Sonderzeichen in einem Feld ausschließen?

Sie können Sonderzeichen in einem Feld mit `${...}`. JSON-Dateien mit Feldern mit einem Punkt (`.`) werden von diesem Mechanismus nicht unterstützt. Wenn bei der Interaktion mit Hierarchien ein untergeordnetes Attribut einen Punkt (`.`), müssen Sie einen umgekehrten Schrägstrich (`\`), um Sonderzeichen zu maskieren. Beispiel: `address` ist ein Objekt, das das Attribut enthält `street.name`, kann dies dann als `address.street\.name` anstelle von `address.street.name`.

### Wie lang sind die berechneten Felder maximal?

Berechnete Felder haben eine maximale Länge von 4096 Zeichen.