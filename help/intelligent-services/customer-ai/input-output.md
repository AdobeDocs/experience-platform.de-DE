---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Eingabe und Ausgabe von Kunden-AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 5cab341138e809bae79623bb65e499ac6b955f27
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# Eingabe und Ausgabe von Kunden-AI

Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten erläutert, die in der Kundentechnik verwendet werden.

## Daten zur Kundenaktieneingabe

Die Kundentelefonie verwendet Consumer Experience Ereignis-Daten, um Tendenzwerte zu berechnen. Weitere Informationen zu Consumer Experience Ereignis finden Sie in der Dokumentation [](../data-preparation.md)Vorbereiten von Daten für die Verwendung in Intelligent Services.

### Historische Daten

Für die Kunden-API sind historische Daten für die Modellschulung erforderlich. Die erforderliche Datenmenge basiert jedoch auf zwei Schlüsselelementen: Ergebnisfenster und förderfähige Bevölkerung.

Standardmäßig sucht die Kunden-API, ob ein Benutzer in den letzten 120 Tagen Aktivität hatte, wenn während der Anwendungskonfiguration keine geeignete Populationsdefinition angegeben wurde. Zusätzlich zu der erforderlichen Mindestmenge an Consumer Experience Ereignis-Daten benötigt die Kunden-AI auch eine Mindestanzahl von Erfolgserlebnissen, die auf einer prognostizierten Zieldefinition basieren. Derzeit benötigt die Kundentraining-API mindestens 500 Ereignis.

In den folgenden Beispielen wird eine einfache Formel verwendet, mit der Sie die erforderliche Mindestdatenmenge festlegen können. Wenn Sie mehr als die Mindestanforderung haben, liefert Ihr Modell wahrscheinlich genauere Ergebnisse. Wenn Sie weniger als den erforderlichen Mindestwert haben, schlägt das Modell fehl, da für die Modellschulung nicht genügend Daten vorhanden sind.

**Formel**:

Mindestlänge der erforderlichen Daten = förderfähige Bevölkerung + Ergebnisfenster

>[!NOTE]
> 30 ist die Mindestanzahl Tage, die für die förderfähige Bevölkerung erforderlich ist. Wenn dies nicht angegeben wird, ist der Standardwert 120 Tage.

Beispiele :

- Sie möchten vorhersagen, ob ein Kunde in den nächsten 30 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 60 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 60 Tage + 30 Tage erforderlich. Die förderfähige Bevölkerung beträgt 60 Tage, das Ergebnisfenster insgesamt 90 Tage.

- Sie möchten vorhersagen, ob der Benutzer in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. In diesem Fall ist die Mindestdatenlänge = 120 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung beträgt standardmäßig 120 Tage und das Ergebnisfenster insgesamt 127 Tage.

- Sie möchten vorhersagen, ob der Kunde in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 7 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 30 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung benötigt mindestens 30 Tage und das Ergebnisfenster beträgt 7 Tage und insgesamt 37 Tage.

Zusätzlich zu den erforderlichen Mindestdaten funktioniert die Kundentreueanweisung auch am besten mit aktuellen Daten. In diesem Anwendungsfall erstellt die Kunden-API eine Prognose für die Zukunft, die auf den neuesten Verhaltensdaten eines Benutzers basiert. Mit anderen Worten: Jüngere Daten werden wahrscheinlich eine genauere Prognose liefern.

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