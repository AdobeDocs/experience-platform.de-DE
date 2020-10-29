---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform
title: Eingabe und Ausgabe von Kunden-AI
topic: Getting started
description: Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten erläutert, die in der Kundentechnik verwendet werden.
translation-type: tm+mt
source-git-commit: 0f45f12ca4f43de9489eb609fd541aa2be3bae78
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 34%

---


# Eingabe und Ausgabe von Kunden-AI

Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten erläutert, die in der Kundentechnik verwendet werden.

## Daten zur Kundenaktieneingabe

Die Kundentelefonie verwendet Consumer Experience Ereignis-Daten, um Tendenzwerte zu berechnen. Weitere Informationen zu Consumer Experience Ereignis finden Sie in der Dokumentation [](../data-preparation.md)Vorbereiten von Daten für die Verwendung in Intelligent Services.

### Historische Daten

Für die Kunden-API sind historische Daten für die Modellschulung erforderlich. Die erforderliche Datenmenge basiert jedoch auf zwei Schlüsselelementen: Ergebnisfenster und förderfähige Bevölkerung.

Standardmäßig sucht die Kunden-API, ob ein Benutzer in den letzten 120 Tagen Aktivität hatte, wenn während der Anwendungskonfiguration keine geeignete Populationsdefinition angegeben wurde. Darüber hinaus erfordert die KUNDENKUNDENKRANKHEIT mindestens 500 qualifizierte und 500 nicht qualifizierte Ereignisse (insgesamt 1000) historische Daten, die auf einer voraussichtlichen Zieldefinition basieren.

In den folgenden Beispielen wird eine einfache Formel verwendet, mit der Sie die erforderliche Mindestdatenmenge festlegen können. Wenn Sie mehr als die Mindestanforderung haben, liefert Ihr Modell wahrscheinlich genauere Ergebnisse. Wenn Sie weniger als den erforderlichen Mindestwert haben, schlägt das Modell fehl, da für die Modellschulung nicht genügend Daten vorhanden sind.

**Formel**:

Mindestlänge der erforderlichen Daten = förderfähige Bevölkerung + Ergebnisfenster

>[!NOTE]
>
> 30 ist die Mindestanzahl Tage, die für die förderfähige Bevölkerung erforderlich ist. Wenn dies nicht angegeben wird, ist der Standardwert 120 Tage.

Beispiele :

- Sie möchten vorhersagen, ob ein Kunde in den nächsten 30 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 60 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 60 Tage + 30 Tage erforderlich. Die förderfähige Bevölkerung beträgt 60 Tage, das Ergebnisfenster insgesamt 90 Tage.

- Sie möchten vorhersagen, ob der Benutzer in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. In diesem Fall ist die Mindestdatenlänge = 120 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung beträgt standardmäßig 120 Tage und das Ergebnisfenster insgesamt 127 Tage.

- Sie möchten vorhersagen, ob der Kunde in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 7 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 30 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung benötigt mindestens 30 Tage und das Ergebnisfenster beträgt 7 Tage und insgesamt 37 Tage.

Zusätzlich zu den erforderlichen Mindestdaten funktioniert die Kundentreueanweisung auch am besten mit aktuellen Daten. In diesem Anwendungsfall erstellt die Kunden-API eine Prognose für die Zukunft, die auf den neuesten Verhaltensdaten eines Benutzers basiert. Mit anderen Worten: Jüngere Daten werden wahrscheinlich eine genauere Prognose liefern.

## Ausgabedaten von Customer AI

Customer AI generiert mehrere Attribute für einzelne Profile, die als geeignet gelten. Es gibt zwei Möglichkeiten, das Ergebnis auf Basis des von Ihnen bereitgestellten Ergebnisses zu konsumieren. Wenn Sie Echtzeit-Kundendaten für Ihr Dataset aktiviert haben, können Sie es über Echtzeit-Kundendaten-Profil nutzen. Wenn Sie kein Echtzeit-Kundendaten-Profil haben, können Sie das Ausgabedataset der Kunden-API herunterladen, das auf dem Datensee verfügbar ist.

>[!NOTE]
>
>Ausgabewerte werden vom Echtzeit-Kundensegment verwendet, das zum Erstellen und Definieren von Segmenten verwendet werden kann.

Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Customer AI gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| Ergebnis | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils, dass es das das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Beim Vergleich der Ausgaben über verschiedene Ziele hinweg wird empfohlen, dass Sie die Wahrscheinlichkeit über das Perzentil oder das Ergebnis in Betracht ziehen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte geeignete Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignisse, die nicht häufig auftreten, tendenziell niedriger liegt. Werte für den Wahrscheinlichkeitsbereich zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für Kundenabwanderung weist beispielsweise darauf hin, dass es ein höheres Risiko für Abwanderungen aufweist als 99 % aller anderen Profile, die bewertet wurden. Die Perzentile liegen zwischen 1 und 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe, warum ein Profil wahrscheinlich konvertiert oder abwandert. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet haben und über alle Anmeldeinformationen und Schema verfügen, befolgen Sie den Beginn im Handbuch &quot; [Eine Kundeninstanz](./user-guide/configure.md) konfigurieren&quot;. Dieser Leitfaden führt Sie durch das Erstellen einer Instanz für die Kundenunterstützung.