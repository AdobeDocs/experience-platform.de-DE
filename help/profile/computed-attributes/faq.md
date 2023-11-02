---
title: Häufig gestellte Fragen zu berechneten Attributen
description: Hier finden Sie Antworten auf häufig gestellte Fragen zur Verwendung berechneter Attribute.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 1%

---

# Häufig gestellte Fragen

In Adobe Experience Platform sind berechnete Attribute Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu berechneten Attributen.

## Wie erhalte ich Zugriff auf berechnete Attribute?

Um Zugriff auf berechnete Attribute zu erhalten, benötigen Sie die entsprechenden Berechtigungen (**Berechnete Attribute anzeigen** und **Berechnete Attribute verwalten**). Weitere Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffssteuerungsdokumentation](../../access-control/home.md). Informationen zum Anwenden dieser Berechtigungen finden Sie in der [Berechtigungshandbuch verwalten](../../access-control/ui/permissions.md).

## Welche Datensätze tragen zu berechneten Attributberechnungen bei?

Bei berechneten Attributen werden für das Echtzeit-Kundenprofil aktivierte Erlebnisereignis-Datensätze zur Berechnung berechneter Attribute berücksichtigt.

## Welche Experience-Datenmodell (XDM)-Felder können zum Erstellen berechneter Attribute verwendet werden?

Alle XDM-Felder in Ihrem Experience Event Vereinigungsschema können zum Erstellen berechneter Attribute verwendet werden.

## Was bedeuten &quot;letzte Bewertung&quot;und &quot;letzte Auswertung&quot;?

Die letzte Bewertung bezieht sich auf den Zeitstempel, bis zu dem Ereignisse in der letzten erfolgreichen Ausführung berücksichtigt werden. Der letzte Bewertungsstatus bezieht sich darauf, ob der letzte Bewertungslauf erfolgreich war oder nicht.

## Kann ich die Aktualisierungshäufigkeit wählen? Wie wird das entschieden?

Die Aktualisierungshäufigkeit wird automatisch anhand des Lookback-Zeitraums Ihres berechneten Attributs bestimmt. Weitere Informationen hierzu finden Sie im [Abschnitt zum Lookback-Zeitraum](./overview.md#lookback-periods) der Übersicht über berechnete Attribute.

## Wie wirkt sich die Gültigkeit von Erlebnisereignisdaten auf Berechnungen aus?

Berechnete Attributberechnungen werden für die definierte Lookback-Dauer in der ersten Auswertung aufgestockt und basierend auf inkrementellen Ereignissen für nachfolgende Aktualisierungen aktualisiert. Daher sind diese Berechnungen **not** von den Erlebnisereignis-Datenabläufen der alten Daten nach der ersten Auswertung betroffen sind.

Wenn Sie beispielsweise ein berechnetes Attribut erstellen, das monatlich mit einem Lookback-Zeitraum von drei Monaten ausgewertet wird, wird für die erste Auswertung das berechnete Attribut für alle Ereignisse innerhalb dieses Lookback-Zeitraums von drei Monaten berechnet. Selbst wenn der Experience Event-Datensatz einen Datenablauf von einem Monat hat, wird dieser Datenablauf **not** wirken sich auf die monatliche Aktualisierung des berechneten Attributs aus, da der Bewertungsablauf des nächsten Monats die Ereignisse inkrementell aggregiert und die Berechnung aktualisiert.

>[!NOTE]
>
>Abgelaufene Daten **cannot** später durch ein berechnetes Attribut aufgestockt werden. Ablauf der Ereignisdatensätze **kann** beschränkte die Fähigkeit, den Wert des berechneten Attributs zu einem späteren Zeitpunkt zu überprüfen. Um den berechneten Attributwert zu überprüfen, sollte Ihr Lookback-Zeitraum beibehalten werden. **Innerhalb** die Grenzen der Datenabläufe.

## Kann ich ein berechnetes Attribut basierend auf einem anderen berechneten Attribut erstellen?

Da berechnete Attribute mit Experience Event-Feldern erstellt werden und sich in einem Profilfeld befinden, ist es nicht möglich, ein berechnetes Attribut direkt zu verwenden, um ein weiteres berechnetes Attribut zu erstellen.

## Gibt es Einschränkungen bei der Anzahl berechneter Attribute, die ich erstellen kann?

Ja, die Anzahl der berechneten Attribute, die Sie erstellen können, ist begrenzt. Weitere Informationen erhalten Sie in der Produktbeschreibung oder im Adobe Account Team.

## Gibt es nachgelagerte Auswirkungen auf die Deaktivierung eines berechneten Attributs?

Bevor Sie Ihr berechnetes Attribut deaktivieren, müssen Sie **sollte** Entfernen Sie sie aus Ihren nachgelagerten Systemen (z. B. Segmentierung, Journey oder Ziele), da möglicherweise Komplikationen auftreten, wenn sie nicht entfernt werden.

## Was passiert, wenn ich ein berechnetes Attribut deaktiviert habe? {#inactive-status}

Wenn ein berechnetes Attribut deaktiviert oder inaktiv gemacht wird, wird es nicht mehr aktualisiert. Dieses berechnete Attribut **cannot** in der Profilsuche oder anderen nachgelagerten Verwendungen verwendet werden.

## Wie können berechnete Attribute die Interaktion fördern?

Berechnete Attribute fördern die Profilanreicherung, indem Sie Ihre Ereignisattribute auf einer zusammengeführten Profilebene aggregieren. Sie können beispielsweise Marketing-E-Mails mit dem zuletzt angezeigten Produkt personalisieren.

## Wie oft werden berechnete Attribute ausgewertet? Bezieht sich dies auf den Zeitplan für die Zielgruppenbewertung?

Berechnete Attribute werden in einer **Batch** Häufigkeit, die **unabhängig** an den Zeitplan Ihrer Zielgruppen-, Ziel- und Journey-Evaluierung. Das bedeutet, dass das berechnete Attribut unabhängig vom Segmentierungstyp (Batch-Segmentierung oder Streaming-Segmentierung) nach seinem eigenen Zeitplan (stündlich, täglich, wöchentlich oder monatlich) bewertet wird.

Die erste Auswertung Ihres berechneten Attributs erfolgt innerhalb von 24 Stunden nach **Erstellung**. Die nachfolgenden Batch-Auswertungen erfolgen stündlich, täglich, wöchentlich oder monatlich, abhängig vom definierten Lookback-Zeitraum.

Wenn beispielsweise am 9. Oktober um 12:00 Uhr UTC eine erste Bewertung erfolgt, werden die folgenden Bewertungen zu folgenden Zeiten durchgeführt:

- Nächste tägliche Aktualisierung: 12 Uhr UTC am 10. Oktober
- Nächste wöchentliche Aktualisierung: 12 Uhr UTC am 15. Oktober
- Nächste monatliche Aktualisierung: 12 Uhr UTC am 1. November

>[!IMPORTANT]
>
>Dies ist nur der Fall, wenn die schnelle Aktualisierung **not** aktiviert. Informationen dazu, wie sich der Lookback-Zeitraum ändert, wenn eine schnelle Aktualisierung aktiviert ist, finden Sie im Abschnitt [Bereich für schnelle Aktualisierung](./overview.md#fast-refresh).

Beide **weekly** und **monatlich** Aktualisierungen finden zu Beginn der **Kalenderwoche** (Sonntag der neuen Woche) oder Anfang der **Kalendermonat** (der erste des neuen Monats) im Gegensatz zu genau einer Woche oder einem Monat nach dem ersten Bewertungsdatum.

>[!NOTE]
>
>Der berechnete Attributwert lautet **not** unmittelbar nach jedem Testlauf im Profil aktualisiert. Um sicherzustellen, dass der aktualisierte Wert in Ihren Profilen enthalten ist, sollten Sie einen Puffer von einigen Stunden zwischen der Auswertungszeit und der Nutzung berechneter Attribute berücksichtigen. Der Aktualisierungszeitplan für berechnete Attribute lautet **systembestimmt** und **cannot** geändert werden. Weitere Informationen erhalten Sie bei der Adobe-Kundenunterstützung.

## Wie interagieren berechnete Attribute mit Zielgruppen, die mithilfe der Streaming-Segmentierung ausgewertet werden?

Wenn eine durch Streaming-Segmentierung ausgewertete Zielgruppe ein berechnetes Attribut verwendet, wird die **neuester Wert** des berechneten Attributs, während die Zielgruppe ausgewertet wird. Wenn die Zielgruppe beispielsweise nach Kaufereignissen sucht, bezieht sich die Zielgruppe beim Eintreten des Kaufereignisses auf den zuletzt ausgewerteten berechneten Attributwert.

## Kann ich berechnete Attribute in Edge verwenden?

Wie jedes andere Profilattribut sind berechnete Attribute verfügbar und können an Edges verwendet werden. Bitte beachten Sie, dass berechnete Attribute **not** an der Kante berechnet.

## Wie werden Datennutzungsbezeichnungen auf berechnete Attribute angewendet?

Berechnete Attribute leiten automatisch Datennutzungsbezeichnungen aus den Quellfeldern und Datensätzen ab, die zur Definition der berechneten Attribute verwendet wurden. Dadurch wird sichergestellt, dass Ihre Verhaltensdaten angemessen verwendet werden.

## Wie verwende ich berechnete Attribute mit Adobe Journey Optimizer?

Um berechnete Attribute in Journey zu verwenden, müssen Sie die `SystemComputedAttributes` Feldergruppe zur Experience Platform-Datenquelle. Weitere Informationen zum Konfigurieren der Experience Platform-Datenquelle finden Sie im Abschnitt [Adobe Experience Platform-Datenquellenhandbuch](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html).
