---
title: Berechnete Attribute - Übersicht
description: Berechnete Attribute sind Funktionen zum Aggregieren von Daten auf Ereignisebene in Attribute auf Profilebene. Diese Funktionen werden automatisch berechnet, damit sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 03f1dfab768e98ef4959d605cc3ead25bb5eb238
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 8%

---

# Berechnete Attribute - Übersicht

Personalization auf der Grundlage des Benutzerverhaltens ist eine wichtige Voraussetzung für Marketing-Experten, um die Wirkung der Personalisierung zu maximieren. Personalisieren Sie beispielsweise die Marketing-E-Mail mit dem zuletzt angezeigten Produkt, um die Konversion zu fördern, oder personalisieren Sie eine Web-Seite basierend auf den Gesamtkäufen, die von Benutzenden getätigt wurden, um die Kundenbindung zu fördern.

Berechnete Attribute helfen dabei, Profilverhaltensdaten schnell in aggregierte Werte auf Profilebene zu konvertieren, ohne von technischen Ressourcen für Folgendes abhängig zu sein:

- Aktivierung gezielter Eins-zu-eins- oder Batch-Personalisierung mit Aktivierung von Verhaltens-Aggregaten für Real-time Customer Data Platform-Ziele und Verwendung in Adobe Journey Optimizer
- Vereinfachte Zielgruppensegmentierung mit Speicherung von Verhaltens-Aggregaten als Profilattribute
- Standardisierung aggregierter Profilverhaltensdaten für die Nutzung über Plattformen und Apps hinweg
- Besseres Daten-Management durch Konsolidierung alter Profilereignisdaten in aussagekräftige Verhaltenserkenntnisse

Diese Aggregate werden auf der Grundlage von profilaktivierten Erlebnisereignis-Datensätzen berechnet, die in Adobe Experience Platform aufgenommen werden. Jedes berechnete Attribut ist ein Profilattribut, das in Ihrem Profilvereinigungsschema erstellt wird und in Ihrem Vereinigungsschema unter der Feldergruppe „SystemComputedAttribute“ gruppiert ist.

Beispiele für Anwendungsfälle sind:

- Personalisieren von Marketing-E-Mails mit Gesamtprämienpunkten, um Benutzern zur Promotion auf eine Premium-Stufe zu gratulieren
- Personalisieren der Kommunikation mit Benutzern basierend auf der Anzahl und Häufigkeit der Käufe
- Aufbewahrungs-E-Mails basierend auf dem Ablaufdatum des Abonnements personalisieren
- Retargeting von Benutzern, die ein Produkt mit dem zuletzt angezeigten Produkt angesehen, aber nicht gekauft haben
- Aktivieren von Ereignisaggregaten über berechnete Attribute für ein nachgelagertes System mithilfe von Real-Time CDP-Zielen
- Reduzieren mehrerer ereignisbasierter Zielgruppen in eine verdichtetere Gruppe berechneter Attribute
- Retargeting nicht authentifizierter Benutzer extern mithilfe aktueller Partner-IDs aus Ereignissen

Dieses Handbuch hilft Ihnen, die Rolle berechneter Attribute innerhalb von Platform besser zu verstehen, und erläutert die Grundlagen berechneter Attribute.

## Berechnete Attribute

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen einfach importieren und zusammenführen, um [!DNL Real-Time Customer Profiles] zu generieren. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). Um diese Daten auf einen Blick leichter verständlich zu machen, können Sie mit [!DNL Platform] berechnete Attribute erstellen, die diese Verweise und Berechnungen automatisch ausführen und den Wert im entsprechenden Feld zurückgeben.

Zu den berechneten Attributen gehört die Erstellung eines Ausdrucks oder einer „Regel“, die mit eingehenden Daten arbeitet und den resultierenden Wert in einem Profilattribut speichert. Ausdrücke können auf verschiedene Weise definiert werden, sodass Sie angeben können, für welche Ereignisse eine Aggregation durchgeführt werden soll, welche Funktionen aggregiert werden sollen oder welche Lookback-Dauer zulässig ist.

### Funktionen

Mit berechneten Attributen können Sie Ereignis-Aggregate eigenständig definieren, indem Sie vordefinierte Funktionen nutzen. Die Details zu diesen Funktionen finden Sie unten:

| Funktion | Beschreibung | Unterstützte Datentypen | Beispielverwendung |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Eine Funktion, **den** Wert für qualifizierte Ereignisse summiert. | Ganzzahlen, Zahlen, Längen | Summe aller Käufe in den letzten 7 Tagen |
| ANZAHL | Eine Funktion, die **zählt** die Anzahl der Ereignisse, die für die angegebene Regel aufgetreten sind. | K. A. | Anzahl der Käufe in den letzten 3 Monaten |
| MIN | Eine Funktion, die den **Mindestwert** für die qualifizierten Ereignisse findet. | Ganzzahlen, Zahlen, Länge, Zeitstempel | Erste Kaufdaten in den letzten 7 Tagen<br/>Mindestbestellmenge in den letzten 4 Wochen |
| MAX | Eine Funktion, die den **Maximum**-Wert für die qualifizierten Ereignisse findet. | Ganzzahlen, Zahlen, Länge, Zeitstempel | Daten des letzten Kaufs in den letzten 7 Tagen<br/>Maximaler Bestellbetrag in den letzten 4 Wochen |
| MOST_RECENT | Eine Funktion, die den angegebenen Attributwert aus dem neuesten qualifizierten Ereignis findet. Diese Funktion gibt **sowohl** den Wert als auch den Zeitstempel des Attributs an. | Alle primitiven Werte, Arrays von primitiven Werten | Neuestes Produkt in den letzten 7 Tagen angezeigt |

### Lookback-Zeiten

Berechnete Attribute werden in Stapeln berechnet, sodass Sie Ihre Aggregate aktuell halten und die neuesten Ereignisse verwenden können. Um diese Szenarien mit minimaler Verzögerung zu unterstützen, variiert die Aktualisierungshäufigkeit je nach dem Lookback-Zeitraum des Ereignisses.

Der Lookback-Zeitraum bezieht sich auf die Zeitdauer, die beim Aggregieren von Erlebnisereignissen für das berechnete Attribut überprüft wird. Dieser Zeitraum kann in Stunden, Tagen, Wochen oder Monaten definiert werden.

Die Aktualisierungshäufigkeit bezieht sich auf die Häufigkeit, mit der die berechneten Attribute aktualisiert werden. Dieser Wert hängt vom Lookback-Zeitraum ab und wird automatisch festgelegt.

| Lookback-Zeitraum | Häufigkeit der Aktualisierung |
| --------------- | ----------------- |
| Bis zu 24 Stunden | Stündlich |
| Bis zu 7 Tage | Täglich |
| Bis zu 4 Wochen | Wöchentlich |
| Bis zu 6 Monate | Monatlich |

Wenn Ihr berechnetes Attribut beispielsweise einen Lookback-Zeitraum der letzten 7 Tage aufweist, wird dieser Wert auf der Grundlage der Werte der letzten 7 Tage berechnet und dann täglich aktualisiert.

>[!NOTE]
>
>Sowohl Wochen als auch Monate werden bei Verwendung **Ereignis** Lookbacks als **Kalendermonate** betrachtet. Die Kalenderwoche beginnt am **Sonntag** und endet am **Samstag** der Woche. Der Kalendermonat beginnt am **.** des Monats und endet am **letzten Tag** des Monats.

Der Lookback-Zeitraum für berechnete Attribute ist ein **rollierender)**. Wenn beispielsweise eine erste Auswertung am 15. Oktober um 12 Uhr UTC erfolgt, ruft der Lookback-Zeitraum von zwei Wochen alle Ereignisse vom 1. Oktober bis zum 15. Oktober ab, aktualisiert am 22. Oktober in einer Woche und ruft dann alle Ereignisse vom 8. Oktober bis zum 22. Oktober ab.

**Schnelle Aktualisierung** {#fast-refresh}

Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Durch Aktivierung dieser Option können Sie Ihre berechneten Attribute täglich aktualisieren, auch für längere Lookback-Zeiträume, sodass Sie schnell auf Benutzeraktivitäten reagieren können.

>[!NOTE]
>
>Die Aktivierung einer schnellen Aktualisierung variiert von Ihrer Ereignis-Lookback-Dauer, da der Lookback-Zeitraum wöchentlich bzw. monatlich rolliert.
>
>Wenn Sie ein berechnetes Attribut mit einem zweiwöchigen Lookback-Zeitraum mit aktivierter schneller Aktualisierung erstellen, bedeutet dies, dass der erste Lookback-Zeitraum zwei Wochen beträgt. Bei jeder täglichen Aktualisierung umfasst der Lookback-Zeitraum jedoch Ereignisse des zusätzlichen Tages. Diese Addition von Tagen wird bis zum Beginn der nächsten Kalenderwoche fortgesetzt, in der das Lookback-Fenster umgeschaltet wird und zu zwei Wochen zurückkehrt.
>
>Wenn beispielsweise ein zweiwöchiger Lookback-Zeitraum am 15. März (Sonntag) mit aktivierter schneller Aktualisierung und täglicher Aktualisierung begann, wird der Lookback-Zeitraum einschließlich bis zum 22. März verlängert und dann wieder auf zwei Wochen zurückgesetzt. Kurz gesagt, das berechnete Attribut wird täglich **aktualisiert** wobei der Lookback-Zeitraum während der Woche von **zwei** Wochen auf **drei** Wochen zunimmt und dann wieder auf **zwei** Wochen zurückkehrt.

## Nächste Schritte

Weitere Informationen zum Erstellen und Verwalten berechneter Attribute finden Sie im [Handbuch zur API für berechnete Attribute](./api.md) oder im [Handbuch zur Benutzeroberfläche für berechnete Attribute](./ui.md).
