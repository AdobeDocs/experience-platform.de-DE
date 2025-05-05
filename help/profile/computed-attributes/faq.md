---
title: Häufig gestellte Fragen zu berechneten Attributen
description: Erfahren Sie Antworten auf häufig gestellte Fragen zur Verwendung berechneter Attribute.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 1%

---

# Häufig gestellte Fragen

In Adobe Experience Platform sind berechnete Attribute Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu berechneten Attributen.

## Wie erhalte ich Zugriff auf berechnete Attribute?

Für den Zugriff auf berechnete Attribute benötigen Sie die entsprechenden Berechtigungen (**Berechnete Attribute anzeigen** und **Berechnete Attribute verwalten**). Weitere Informationen zu den erforderlichen Berechtigungen finden Sie in der [Dokumentation zur Zugriffssteuerung](../../access-control/home.md). Informationen zum Anwenden dieser Berechtigungen finden Sie im [Handbuch zum Verwalten von Berechtigungen](../../access-control/ui/permissions.md).

## Welche Datensätze tragen zur Berechnung berechneter Attribute bei?

Berechnete Attribute berücksichtigen für die Berechnung berechneter Attribute Echtzeit-Kundenprofil-aktivierte Erlebnisereignis-Datensätze.

## Welche Experience-Datenmodell (XDM)-Felder können zum Erstellen berechneter Attribute verwendet werden?

Alle XDM-Felder im Vereinigungsschema Ihres Erlebnisereignisses können zum Erstellen berechneter Attribute verwendet werden.

## Was bedeuten „Letzte Auswertung“ und „Letzter Auswertungsstatus“?

Zuletzt ausgewertet bezieht sich auf den Zeitstempel, bis zu dem Ereignisse beim letzten erfolgreichen Durchgang berücksichtigt werden. Der letzte Auswertungsstatus bezieht sich darauf, ob der letzte Auswertungsdurchgang erfolgreich war oder nicht.

## Kann ich die Aktualisierungshäufigkeit auswählen? Wie wird das entschieden?

Die Aktualisierungshäufigkeit wird automatisch anhand der Lookback-Periode Ihres berechneten Attributs bestimmt. Weiterführende Informationen hierzu finden Sie im Abschnitt [Lookback-Zeitraum](./overview.md#lookback-periods) der Übersicht über berechnete Attribute.

## Wie wirken sich Abläufe von Erlebnisereignisdaten auf Berechnungen aus?

Berechnete Attributberechnungen werden für die definierte Lookback-Dauer in der ersten Auswertung aufgestockt und basierend auf inkrementellen Ereignissen für nachfolgende Aktualisierungen aktualisiert. Daher sind diese Berechnungen **nicht** von den Gültigkeitsdauern von Erlebnisereignisdaten der alten Daten nach der ersten Auswertung betroffen.

Wenn Sie beispielsweise ein berechnetes Attribut erstellen, das monatlich mit einem dreimonatigen Lookback-Zeitraum ausgewertet wird, berechnet das berechnete Attribut für die erste Auswertung alle Ereignisse innerhalb dieses dreimonatigen Lookback-Zeitraums. Selbst wenn der Erlebnisereignis-Datensatz eine Datengültigkeit von einem Monat hat, wirkt sich diese Datengültigkeit **nicht** auf die monatliche Aktualisierung der berechneten Attribute aus, da die Auswertungsausführung des nächsten Monats Ereignisse inkrementell aggregiert und die Berechnung aktualisiert.

>[!NOTE]
>
>Abgelaufene Daten **können** später durch ein berechnetes Attribut aufgestockt werden. Ablauf von Ereignisdatensatzdaten **kann** die Möglichkeit einschränken, den Wert des berechneten Attributs zu einem späteren Zeitpunkt zu überprüfen. Um den berechneten Attributwert zu überprüfen, sollte Ihr Lookback-Zeitraum innerhalb **Grenzen** Datenablaufs bleiben.

## Kann ich ein berechnetes Attribut auf der Grundlage eines anderen berechneten Attributs erstellen?

Da berechnete Attribute mithilfe von Erlebnisereignisfeldern erstellt werden und sich in einem Profilfeld befinden, gibt es keine Möglichkeit, ein berechnetes Attribut direkt zum Erstellen eines anderen berechneten Attributs zu verwenden.

## Gibt es Beschränkungen für die Anzahl der berechneten Attribute, die ich erstellen kann?

Ja, die Anzahl der berechneten Attribute, die Sie erstellen können, ist begrenzt. Diese Beschränkung gilt nur für **aktive** berechnete Attribute. Weitere Informationen entnehmen Sie bitte der Produktbeschreibung oder wenden Sie sich an das Adobe Account Team.

## Gibt es nachgelagerte Auswirkungen auf die Deaktivierung eines berechneten Attributs?

Bevor Sie Ihr berechnetes Attribut deaktivieren **sollten** Sie es aus Ihren nachgelagerten Systemen (wie Segmentierung, Journey oder Zielen) entfernen, da es zu Komplikationen kommen kann, wenn sie nicht entfernt werden.

## Was passiert, wenn ich ein berechnetes Attribut deaktiviere? {#inactive-status}

Wenn ein berechnetes Attribut deaktiviert oder inaktiv gemacht wird, wird es nicht mehr aktualisiert. Daher kann dieses berechnete Attribut **nicht** bei der Profilsuche oder anderen nachgelagerten Verwendungen verwendet werden.

## Wie fördern berechnete Attribute die Interaktion?

Berechnete Attribute fördern die Profilanreicherung durch die Aggregation Ihrer Ereignisattribute auf der Ebene eines zusammengeführten Profils. Sie können beispielsweise Marketing-E-Mails mit dem zuletzt angezeigten Produkt personalisieren.

## Wie oft werden berechnete Attribute ausgewertet? Ist dies mit dem Zeitplan für die Zielgruppenauswertung verbunden?

Berechnete Attribute werden in einer **Batch**-Häufigkeit ausgewertet, die **unabhängig** dem Zeitplan Ihrer Zielgruppe-, Ziel- und Journey-Auswertung ist. Das bedeutet, dass das berechnete Attribut unabhängig vom Segmentierungstyp (Batch- oder Streaming-Segmentierung) nach einem eigenen Zeitplan ausgewertet wird (stündlich, täglich, wöchentlich oder monatlich).

Die erste Auswertung Ihres berechneten Attributs erfolgt innerhalb der 24 Stunden nach seiner **Erstellung**. Die nachfolgenden Batch-Auswertungen erfolgen stündlich, täglich, wöchentlich oder monatlich, je nach definiertem Lookback-Zeitraum.

Wenn beispielsweise am 9. Oktober um 12 Uhr UTC eine erste Auswertung erfolgt, würden die nachfolgenden Auswertungen zu folgenden Zeiten erfolgen:

- Nächste tägliche Aktualisierung: 12 Uhr UTC am 10. Oktober
- Nächste wöchentliche Aktualisierung: 12 Uhr UTC am 15. Oktober
- Nächste monatliche Aktualisierung: 12 Uhr UTC am 1. November

>[!IMPORTANT]
>
>Dies ist nur der Fall, wenn die schnelle Aktualisierung **nicht** aktiviert ist. Informationen dazu, wie sich die Lookback-Periode ändert, wenn die schnelle Aktualisierung aktiviert ist, finden Sie [ Abschnitt „Schnelle Aktualisierung](./overview.md#fast-refresh).

Die **wöchentliche** und **monatliche** Aktualisierung erfolgt am Beginn der **Kalenderwoche** (Sonntag der neuen Woche) oder am Beginn des **Kalendermonats** (der erste des neuen Monats), im Gegensatz zu genau einer Woche oder einem Monat nach dem ersten Auswertungsdatum.

>[!NOTE]
>
>Der berechnete Attributwert wird **nicht** nach jedem Auswertungsdurchgang im Profil aktualisiert. Um sicherzustellen, dass der aktualisierte Wert in Ihren Profilen enthalten ist, sollten Sie einen Puffer von einigen Stunden zwischen der Auswertungszeit und der Verwendung berechneter Attribute in Betracht ziehen. Der berechnete Aktualisierungszeitplan für das Attribut **(systembestimmt** und **kann** geändert werden. Für weitere Informationen wenden Sie sich bitte an die Kundenunterstützung von Adobe.

## Wie interagieren berechnete Attribute mit Zielgruppen, die mithilfe der Streaming-Segmentierung bewertet wurden?

Wenn eine Zielgruppe, die für die Streaming-Segmentierung ausgewertet wird, ein berechnetes Attribut verwendet, verwendet sie den **neuesten Wert** des berechneten Attributs, während die Zielgruppe ausgewertet wird. Wenn die Zielgruppe beispielsweise nach Kaufereignissen sucht, verweist die Zielgruppe auf den zuletzt ausgewerteten berechneten Attributwert, wenn das Kaufereignis eintritt.

## Kann ich berechnete Attribute in Edge verwenden?

Wie jedes andere Profilattribut sind berechnete Attribute verfügbar und können an Kanten verwendet werden. Beachten Sie, dass berechnete Attribute **nicht** in Edge berechnet werden.

## Wie werden Datennutzungsbeschriftungen auf berechnete Attribute angewendet?

Berechnete Attribute leiten automatisch Datennutzungsbeschriftungen von den Quellfeldern und Datensätzen ab, die zur Definition der berechneten Attribute verwendet wurden. Dadurch wird sichergestellt, dass Ihre Verhaltensdaten ordnungsgemäß verwendet werden.

## Wie verwende ich berechnete Attribute mit Adobe Journey Optimizer?

Um berechnete Attribute in Journey zu verwenden, müssen Sie die `SystemComputedAttributes` Feldergruppe zur Experience Platform-Datenquelle hinzufügen. Weitere Informationen zum Konfigurieren der Experience Platform-Datenquelle finden Sie im Handbuch zu Adobe Experience Platform-Datenquellen [&#128279;](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html).
