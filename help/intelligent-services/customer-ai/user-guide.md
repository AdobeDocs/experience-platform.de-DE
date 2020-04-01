---
keywords: Experience Platform;user guide;customer ai;popular topics
solution: Experience Platform
title: Handbuch zur Kundenaktivität
topic: User guide
translation-type: tm+mt
source-git-commit: 7987cec12c22e9b48ddc9fdc263d7cd28bd172f2

---


# Handbuch zur Kundenaktivität

Die Kundentechnik als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um maschinelles Lernen kümmern zu müssen.

In diesem Handbuch werden die Schritte zum Arbeiten mit Kunden-API beschrieben. Schritte werden für folgende Themen aufgeführt:

* [Instanz konfigurieren](#configure-an-instance)
* [Kundensegmente mit prognostizierten Werten erstellen](#create-customer-segments-with-predicted-scores)

Darüber hinaus enthält der Anhang zu diesem Lernprogramm Informationen zur [Ausgabe der Kundenaktivität](#customer-ai-output-data).

## Instanz konfigurieren

Intelligent Services bieten Kunden-AI als einfach zu verwendenden Adobe Sensei-Dienst, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

### Instanz einrichten

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **Dienste**. Der Browser für **Dienste** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. Klicken Sie im Container für Customer AI auf **Öffnen**.

![](./images/user-guide/navigate-to-service.png)

Im Bildschirm *Customer AI* werden alle vorhandenen Customer AI-Instanzen angezeigt. Klicken Sie auf **Instanz erstellen**.

![](./images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt *Einrichtung*.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie der Instanz bereitstellen müssen:

* Der Name der Instanz wird an allen Stellen verwendet, an denen die Kunden-AI-Bewertung angezeigt wird. Daher sollte man in Namen beschreiben, was die Prognosewerte darstellen, z. B. &quot;Wahrscheinlichkeit, das Abonnement eines Magazins abzubrechen&quot;.

* Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. Sie können entweder **Abwanderung** oder **Konversion** wählen. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Bewertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

* Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig nutzt Customer AI Kundenerlebnis-Ereignisdaten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz aus der Dropdown-Auswahl auswählen, werden nur die Datensätze aufgelistet, die mit der Kunden-API kompatibel sind.

* Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Geben Sie die erforderlichen Werte ein und klicken Sie auf **Weiter**.

![](./images/user-guide/setup.png)

### Ziel definieren

Der Schritt *Ziel definieren* wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Ziel visuell festlegen können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Klicken Sie auf **Feldnamen eingeben** und wählen Sie ein Feld aus der Dropdown-Liste aus. Klicken Sie auf die zweite Eingabe und wählen Sie eine Klausel für die Ereignisbedingung. Geben Sie dann einen Zielwert ein, um das Ereignis fertigzustellen. Weitere Ereignisse können durch Klicken auf **Ereignis hinzufügen** konfiguriert werden. Schließen Sie das Ziel ab, indem Sie einen Prognosezeitrahmen (Zahl der Tage) anwenden, und klicken Sie dann auf **Weiter**.

![](./images/user-guide/goal.png)

### Zeitplan konfigurieren *(optional)*

Der Schritt *Erweitert* wird angezeigt. In diesem optionalen Schritt können Sie einen Zeitplan konfigurieren, um die Ausführung von Prognosen zu automatisieren, Prognoseausschlüsse zum Filtern bestimmter Ereignisse definieren oder auf **Fertig stellen** klicken, wenn nichts mehr erforderlich ist.

Richten Sie einen Bewertungszeitplan ein, indem Sie die *Bewertungshäufigkeit* festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](./images/user-guide/schedule.png)

Unter der Zeitplankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass bei der Generierung von Werten Ereignisse ausgewertet werden, die bestimmte Bedingungen erfüllen. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

Um bestimmte Ereignisse auszuschließen, klicken Sie auf **Ausschluss hinzufügen** und definieren Sie das Ereignis auf dieselbe Weise wie das Ziel. Um einen Ausschluss zu entfernen, klicken Sie auf die Auslassungspunkte (**...**) oben rechts neben dem Ereignis-Container und dann auf **Container entfernen**.

![](./images/user-guide/exclusion.png)

Schließen Sie Ereignisse nach Bedarf aus und klicken Sie dann auf **Fertig stellen**, um die Instanz zu erstellen.

![](./images/user-guide/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognoseausführung ausgelöst und die nachfolgenden Ausläufe werden gemäß Ihrem definierten Zeitplan ausgeführt.

>[!NOTE] Je nach Größe der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

In diesem Abschnitt haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose durchgeführt. Nach erfolgreichem Abschluss des Vorgangs werden die Profil automatisch mit Ergebniswerten gefüllt. Bitte warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Die Anreicherung von Profilen mit Kundentreuewerten ermöglicht die Erstellung von Kundensegmenten, um Audiencen anhand ihrer Tendenzwerte zu finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Um diese Methode verwenden zu können, muss Echtzeit-Kundendaten-Profil für den Datensatz aktiviert werden.

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **Segmente** und dann auf **Segment erstellen**.

![](./images/user-guide/segments.png)

*Segment Builder* wird angezeigt. Klicken Sie in der linken Spalte *Felder* und auf der Registerkarte *Attribute* auf den Ordner **Individuelles XDM-Profil** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **Customer AI** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](./images/user-guide/results.png)

Ziehen Sie das Attribut **Wert**, das sich in der Mitte von Segment Builder befindet, in die *Arbeitsfläche zum Erstellen von Regeln*, um eine Regel zu definieren.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](./images/user-guide/properties.png)

Klicken Sie über der Spalte &quot; *Felder* links&quot;auf das **Zahnradsymbol** und wählen Sie eine Richtlinie **zum Zusammenführen** aus. Click **Save** to create the segment.

![](./images/user-guide/merge_policy.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe des Segmentaufbaus erfolgreich eine Instanz der Kunden-AI konfiguriert, Tendenzwerte generiert und Audiencen basierend auf ihren Tendenzwerten gefunden. Sie können Ihre Audiencen jetzt in Zielgruppen aktivieren, indem Sie sie an Zielorten aktivieren. See the [destinations overview](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) for more information.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zur Ausgabe der Kunden-API.

### Daten zur Kundenaktivität

Die Kundentelefonie generiert mehrere Attribute für einzelne Profil, die als förderfähig gelten. Diese Werte werden vom Echtzeit-Kundensegment verwendet, das zum Erstellen und Definieren von Segmenten verwendet werden kann. Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Kunden-API gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| Ergebnis | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils für das Erreichen des prognostizierten Ziels innerhalb des definierten Zeitraums. Beim Vergleich der Ergebnisse über verschiedene Ziele hinweg wird empfohlen, dass Sie die Wahrscheinlichkeit über das Perzentil oder das Ergebnis in Betracht ziehen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte förderfähige Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignis, die nicht häufig auftreten, tendenziell auf der unteren Seite liegt. Werte für den Wahrscheinlichkeitsbereich zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für die Kehrtwende weist beispielsweise darauf hin, dass es ein höheres Risiko für Kürzen aufweist als 99 % aller anderen Profil, die bewertet wurden. Die Perzentile reichen von 1 bis 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Bewertung | Das Datum, an dem die Bewertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe, warum ein Profil wahrscheinlich konvertiert oder zerfällt. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das erwartete Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |