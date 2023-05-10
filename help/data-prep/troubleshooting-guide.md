---
keywords: Experience Platform;Startseite;beliebte Themen;
title: Handbuch zur Fehlerbehebung bei der Datenvorbereitung
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Adobe Experience Platform-Datenvorbereitung.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 100%

---

# [!DNL Data Prep] – Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur [!DNL Data Prep] von Adobe Experience Platform sowie eine Anleitung zur Behebung gängiger Fehler. Antworten zu Fragen und allgemeine Informationen zur Fehlerbehebung bei Platform-APIs finden Sie im [Handbuch zur Fehlerbehebung bei Adobe Experience Platform-APIs](../landing/troubleshooting.md).

## FAQs

Im Folgenden finden Sie eine Liste häufig gestellter Fragen zur [!DNL Data Prep] und die zugehörigen Antworten.

### Wie werden Umwandlungsfehler behoben?

Bei der [!DNL Data Prep] werden alle Umwandlungsfehler in der Spalte gefunden, in der sie aufgetreten sind. In der Folge wird diese Spalte ungültig gemacht, wobei der Rest der Zeile weiterhin verarbeitet wird. Diese Umwandlungsprobleme werden in Form von **Warnungen** protokolliert. Es wird empfohlen, die Warnungen regelmäßig zu überprüfen und die Umwandlungslogik entsprechend der Umwandlungsprobleme anzupassen. Dadurch erhöht sich die Qualität der in Experience Platform aufgenommenen Daten.

Wenn die mit **Erforderlich** markierten Spalten aufgrund von Umwandlungsproblemen ungültig gemacht werden, wird die Zeile nicht aufgenommen. Wenn die partielle Datenaufnahme aktiviert ist, können Sie den Schwellenwert für solche Zurückweisungen festlegen, bevor der gesamte Fluss fehlschlägt. Wenn sich das Attribut „ungültig“ nicht auf Validierungen auf Schemaebene ausgewirkt hat, wird die Aufnahme der Zeile fortgesetzt.

Alle Zeilen, die ungültig sind, obwohl keine Umwandlungsfehler vorliegen, werden ebenfalls zurückgewiesen. Beispielsweise kann ein Datenaufnahme-Fluss eine Durchleitungszuordnung (keine Umwandlungslogik) zu einem erforderlichen Feld aufweisen, aber es gibt keinen eingehenden Wert für dieses Attribut. Diese Zeile wird zurückgewiesen.

### Wie kann ich Sonderzeichen in einem Feld mit Escape-Zeichen versehen?

Sie können Sonderzeichen in einem Feld durch die Verwendung von `${...}` mit Escape-Zeichen versehen. Allerdings werden JSON-Dateien, die Felder mit einem Punkt (`.`) enthalten, von diesem Mechanismus nicht unterstützt. Wenn Sie mit Hierarchien arbeiten und ein untergeordnetes Attribut einen Punkt (`.`) enthält, müssen Sie einen Backslash (`\`) verwenden, um Sonderzeichen zu umgehen. Ein Beispiel: `address` ist ein Objekt, das das Attribut `street.name` enthält. Auf dieses kann sich dann durch `address.street\.name` anstelle von `address.street.name` bezogen werden.

### Wie lang können berechnete Felder maximal sein?

Berechnete Felder haben eine maximale Länge von 4096 Zeichen.