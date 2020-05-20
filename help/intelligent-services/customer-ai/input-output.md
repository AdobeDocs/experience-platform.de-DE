---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Eingabe und Ausgabe von Kunden-AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---


# Eingabe und Ausgabe von Kunden-AI

Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten erläutert, die in der Kundentechnik verwendet werden.

## Daten zur Kundenaktieneingabe

Die Kundentelefonie verwendet Consumer Experience Ereignis-Daten, um Tendenzwerte zu berechnen. Weitere Informationen zu Consumer Experience Ereignis finden Sie in der Dokumentation [](../data-preparation.md)Vorbereiten von Daten für die Verwendung in Intelligent Services.

## Daten zur Kundenaktivität

Die Kundentelefonie generiert mehrere Attribute für einzelne Profil, die als förderfähig gelten. Es gibt zwei Möglichkeiten, das Ergebnis auf Basis des von Ihnen bereitgestellten Ergebnisses zu konsumieren. Wenn Sie Echtzeit-Kundendaten für Ihr Dataset aktiviert haben, können Sie es über Echtzeit-Kundendaten-Profil nutzen. Wenn Sie kein Echtzeit-Kundendaten-Profil haben, können Sie das Ausgabedataset der Kunden-API herunterladen, das auf dem Datensee verfügbar ist.

>[!NOTE]
>Ausgabewerte werden vom Echtzeit-Kundensegment verwendet, das zum Erstellen und Definieren von Segmenten verwendet werden kann.

Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Kunden-API gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| Ergebnis | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils für das Erreichen des prognostizierten Ziels innerhalb des definierten Zeitraums. Beim Vergleich der Ergebnisse über verschiedene Ziele hinweg wird empfohlen, dass Sie die Wahrscheinlichkeit über das Perzentil oder das Ergebnis in Betracht ziehen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte förderfähige Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignis, die nicht häufig auftreten, tendenziell auf der unteren Seite liegt. Werte für den Wahrscheinlichkeitsbereich zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für die Kehrtwende weist beispielsweise darauf hin, dass es ein höheres Risiko für Kürzen aufweist als 99 % aller anderen Profil, die bewertet wurden. Die Perzentile reichen von 1 bis 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Bewertung | Das Datum, an dem die Bewertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe, warum ein Profil wahrscheinlich konvertiert oder zerfällt. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das erwartete Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet haben und über alle Anmeldeinformationen und Schema verfügen, befolgen Sie den Beginn im Handbuch &quot; [Eine Kundeninstanz](./user-guide/configure.md) konfigurieren&quot;. Dieser Leitfaden führt Sie durch das Erstellen einer Instanz für die Kundenunterstützung.