---
keywords: Experience Platform;Startseite;beliebte Themen;
title: Anleitung zur Fehlerbehebung bei der Datenvorbereitung
topic-legacy: troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Adobe Experience Platform-Datenvorbereitung.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!DNL Data Prep] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Prep]sowie eine Anleitung zur Fehlerbehebung für häufige Fehler. Fragen und Informationen zur Fehlerbehebung für Platform-APIs im Allgemeinen finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Adobe Experience Platform API](../landing/troubleshooting.md).

## FAQs

Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu [!DNL Data Prep] und ihre Antworten.

### Wie werden Transformationsfehler behoben?

[!DNL Data Prep] lokalisiert alle Umwandlungsfehler in die Spalte, in der sie aufgetreten sind. Daher wird diese Spalte ungültig und der Rest der Zeile wird weiterhin verarbeitet. Diese Transformationsprobleme werden protokolliert als **Warnungen**. Es wird empfohlen, die Warnungen regelmäßig zu überprüfen und die Umwandlungslogik so anzupassen, dass die Transformationsprobleme berücksichtigt werden. Dies erhöht die Qualität der in Experience Platform erfassten Daten.

Wenn die Spalten als **Erforderlich** aufgrund von Transformationsproblemen aufgehoben werden, wird die Zeile nicht erfasst. Wenn die partielle Datenerfassung aktiviert ist, können Sie den Schwellenwert für solche Zurückweisungen festlegen, bevor der gesamte Fluss fehlschlägt. Wenn sich das Attribut &quot;nullified&quot;nicht auf Überprüfungen auf Schemaebene ausgewirkt hat, wird die Zeile weiterhin erfasst.

Alle Zeilen, die ungültig sind, auch ohne Transformationsfehler, werden ebenfalls zurückgewiesen. Beispielsweise kann ein Datenaufnahme-Fluss eine Übergabe durch die Zuordnung (keine Transformationslogik) zu einem erforderlichen Feld haben und es gibt keinen eingehenden Wert für dieses Attribut. Diese Zeile wird abgelehnt.