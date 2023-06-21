---
title: Häufig gestellte Fragen zu berechneten Attributen
description: Erfahren Sie mehr über die Antworten auf häufig gestellte Fragen zur Verwendung berechneter Attribute.
badge: „Beta“
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 4%

---


# Häufig gestellte Fragen

>[!IMPORTANT]
>
>Berechnete Attribute befinden sich derzeit in **Beta** und **not** für alle Benutzer verfügbar.

In Adobe Experience Platform sind berechnete Attribute Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu berechneten Attributen.

## Welche Datensätze tragen zu berechneten Attributberechnungen bei?

Bei berechneten Attributen werden für das Echtzeit-Kundenprofil aktivierte Erlebnisereignis-Datensätze zur Berechnung berechneter Attribute berücksichtigt.

## Welche Experience-Datenmodell (XDM)-Felder können zum Erstellen berechneter Attribute verwendet werden?

Alle XDM-Felder in Ihrem Experience Event Vereinigungsschema können zum Erstellen berechneter Attribute verwendet werden.

## Was bedeutet die &quot;letzte Auswertungszeit&quot;?

Die letzte Auswertungszeit bedeutet, dass die Ereignisse **before** zu diesem Zeitstempel wurden bei der letzten erfolgreichen Aktualisierung des berechneten Attributs berücksichtigt.

## Kann ich die Aktualisierungshäufigkeit wählen? Wie wird das entschieden?

Die Aktualisierungshäufigkeit wird automatisch anhand des Lookback-Zeitraums Ihres berechneten Attributs bestimmt. Weitere Informationen hierzu finden Sie im [Abschnitt zum Lookback-Zeitraum](./overview.md#lookback-periods) der Übersicht über berechnete Attribute.

## Wie wirkt sich die Gültigkeit von Erlebnisereignisdaten auf Berechnungen aus?

Berechnete Attributberechnungen basieren auf dem definierten Lookback-Zeitraum und den Erlebnisereignissen, die in diesen Zeitraum fallen. Daher sind diese Berechnungen **not** von den Ablauf der Erlebnisereignisdaten betroffen sind. Um jedoch die Genauigkeit Ihrer berechneten Attribute sicherzustellen, sollte Ihr Lookback-Zeitraum beibehalten werden. **Innerhalb** die Grenzen Ihrer Datenabläufe.

## Kann ich ein berechnetes Attribut basierend auf einem anderen berechneten Attribut erstellen?

Da berechnete Attribute mit Experience Event-Feldern erstellt werden und sich in einem Profilfeld befinden, ist es nicht möglich, ein berechnetes Attribut direkt zu verwenden, um ein weiteres berechnetes Attribut zu erstellen.

## Gibt es Einschränkungen bei der Anzahl berechneter Attribute, die ich erstellen kann?

Die aktuelle Höchstzahl von **veröffentlicht** berechnete Attribute 25.

## Gibt es nachgelagerte Auswirkungen auf die Deaktivierung eines berechneten Attributs?

Bevor Sie Ihr berechnetes Attribut deaktivieren, müssen Sie **sollte** Entfernen Sie sie aus Ihren nachgelagerten Systemen (z. B. Segmentierung, Journey oder Ziele), da möglicherweise Komplikationen auftreten, wenn sie nicht entfernt werden.

## Was passiert, wenn ich ein berechnetes Attribut deaktiviert habe? {#inactive-status}

Wenn ein berechnetes Attribut deaktiviert oder inaktiv gemacht wird, wird es nicht mehr aktualisiert. Daher wird dieses berechnete Attribut **cannot** in der Profilsuche oder anderen nachgelagerten Verwendungen verwendet werden.

## Wie können berechnete Attribute die Interaktion fördern?

Berechnete Attribute fördern die Profilanreicherung, indem Sie Ihre Ereignisattribute auf einer zusammengeführten Profilebene aggregieren. Sie können beispielsweise Marketing-E-Mails mit dem zuletzt angezeigten Produkt personalisieren.
