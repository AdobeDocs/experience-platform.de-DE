---
title: Übersicht über berechnete Attribute
description: Berechnete Attribute sind Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.
badge: „Beta“
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 11%

---

# Übersicht über berechnete Attribute

>[!IMPORTANT]
>
>Berechnete Attribute befinden sich derzeit in **Beta** und **not** für alle Benutzer verfügbar.

Eine auf dem Benutzerverhalten basierende Personalisierung ist eine wichtige Voraussetzung für Marketing-Experten, um die Wirkung der Personalisierung zu maximieren. So können Sie z. B. Marketing-E-Mails mit dem zuletzt angezeigten Produkt personalisieren, um die Konversion zu fördern, oder die Webseite basierend auf den Gesamtkäufen personalisieren, die von Benutzern getätigt werden, um die Kundenbindung zu fördern.

Berechnete Attribute helfen Ihnen, Verhaltensdaten von Profilen schnell in aggregierte Werte auf der Profilebene zu konvertieren, ohne von technischen Ressourcen für Folgendes abhängig zu sein:

- Aktivierung einer zielgerichteten Personalisierung mit Aktivierung von Verhaltens-Aggregaten für Real-time Customer Data Platform-Ziele, Verwendung in Adobe Journey Optimizer oder Segmentierung
- Standardisierung aggregierter Profil-Verhaltensdaten für die plattformübergreifende Verwendung in Apps und Apps
- Besseres Datenmanagement mit Konsolidierung alter Profilereignisdaten in aussagekräftige Verhaltenseinblicke

Diese Aggregate werden anhand von in Adobe Experience Platform erfassten profilaktivierten Erlebnisereignis-Datensätzen berechnet. Jedes berechnete Attribut ist ein Profilattribut, das für Ihr Profilvereinigungsschema erstellt wurde und unter der Feldergruppe &quot;Berechnetes Attribut&quot;in Ihrem Vereinigungsschema gruppiert ist.

Beispiele für Nutzungsszenarios sind das Personalisieren von Anzeigen mit dem Namen des zuletzt angezeigten Produkts für Personen, die in den letzten sieben Tagen keine Käufe getätigt haben, das Personalisieren von Marketing-E-Mails mit Gesamtgewinnpunkten, um Benutzer dazu zu gratulieren, zu einer Premium-Ebene beworben zu werden, oder das Berechnen des Lebenszeitwerts jedes Kunden, um ein besseres Targeting zu erzielen.

Dieses Handbuch hilft Ihnen, die Rolle berechneter Attribute in Platform besser zu verstehen und die Grundlagen berechneter Attribute zu erklären.

## Berechnete Attribute

Mit Adobe Experience Platform können Sie Daten aus mehreren Quellen einfach importieren und zusammenführen, um sie zu generieren [!DNL Real-Time Customer Profiles]. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). Damit diese Daten auf einen Blick leichter zu verstehen sind, [!DNL Platform] ermöglicht die Erstellung berechneter Attribute, die diese Verweise und Berechnungen automatisch ausführen und den Wert im entsprechenden Feld zurückgeben.

Berechnete Attribute umfassen das Erstellen eines Ausdrucks oder einer &quot;Regel&quot;, der für eingehende Daten verwendet wird und den resultierenden Wert in einem Profilattribut speichert. Ausdrücke können auf unterschiedliche Weise definiert werden, sodass Sie festlegen können, welche Ereignisse aggregiert werden sollen, welche Funktionen aggregiert werden sollen oder welche Lookback-Dauer gelten soll.

### Funktionen

Mit berechneten Attributen können Sie Ereignis-Aggregate auf Self-Service-Weise definieren, indem Sie vordefinierte Funktionen nutzen. Die Details zu diesen Funktionen finden Sie unten:

| Funktion | Beschreibung | Unterstützte Datentypen | Beispiel |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Eine Funktion, die **Beträge** den angegebenen Wert für qualifizierte Ereignisse. | Ganzzahlen, Zahlen, Längen | Summe aller Käufe in den letzten sieben Tagen |
| COUNT | Eine Funktion, die **count** die Anzahl der Ereignisse, die für die jeweilige Regel aufgetreten sind. | K. A. | Anzahl der Käufe in den letzten drei Monaten |
| MIN | Eine Funktion, die die **Minimum** für die qualifizierten Ereignisse. | Ganzzahlen, Zahlen, Längen, Zeitstempel | Erste Kaufdaten in den letzten 7 Tagen<br/>Mindestbestellbetrag in den letzten 4 Wochen |
| MAX | Eine Funktion, die die **maximum** für die qualifizierten Ereignisse. | Ganzzahlen, Zahlen, Längen, Zeitstempel | Letzte Kaufdaten der letzten 7 Tage<br/>Höchstbetrag der Bestellungen in den letzten 4 Wochen |
| MOST_RECENT | Eine Funktion, die den angegebenen Attributwert aus dem zuletzt qualifizierten Ereignis findet. | Alle Grundwerte, Arrays von Grundwerten | Neuestes Produkt, das in den letzten 7 Tagen angesehen wurde |

### Lookback-Zeiträume

Berechnete Attribute werden in Stapeln berechnet, sodass Aggregate frisch bleiben und die neuesten Ereignisse verwendet werden. Um diese nahezu Echtzeit-Szenarien zu unterstützen, variiert die Aktualisierungshäufigkeit je nach dem Ereignis-Lookback-Zeitraum.

Der Lookback-Zeitraum bezieht sich auf die Zeit, die beim Aggregieren von Erlebnisereignissen für das berechnete Attribut geprüft wird. Dieser Zeitraum kann in Stunden, Tagen, Wochen oder Monaten definiert werden.

Die Aktualisierungshäufigkeit bezieht sich auf die Häufigkeit, mit der die berechneten Attribute aktualisiert werden. Dieser Wert hängt vom Lookback-Zeitraum ab und wird automatisch festgelegt.

| Lookback-Zeitraum | Häufigkeit der Aktualisierung |
| --------------- | ----------------- |
| Bis zu 24 Stunden | Stündlich |
| Bis zu 7 Tage | Täglich |
| Bis zu 4 Wochen | Wöchentlich |
| Bis zu 6 Monate | Monatlich |

Wenn Ihr berechnetes Attribut beispielsweise über einen Lookback-Zeitraum der letzten 7 Tage verfügt, wird dieser Wert anhand der Werte der letzten 7 Tage berechnet und dann täglich aktualisiert.

>[!NOTE]
>
>Sowohl Wochen als auch Monate gelten als **Kalenderwochen** und **Kalendermonate** bei Verwendung in Ereignis-Lookbacks.

**Schnelle Aktualisierung**

>[!IMPORTANT]
>
>Maximal **fünf** -Attribute pro Sandbox kann die schnelle Aktualisierung aktiviert haben.

Mit der schnellen Aktualisierung können Sie Ihre Attribute auf dem neuesten Stand halten. Durch Aktivierung dieser Option können Sie Ihre berechneten Attribute täglich aktualisieren, auch für längere Lookback-Zeiträume. Dadurch können Sie nahezu in Echtzeit auf Benutzeraktivitäten reagieren. Dieser Wert gilt nur für berechnete Attribute mit einem Lookback-Zeitraum, der größer als die wöchentliche Basis ist.

>[!NOTE]
>
>Die Aktivierung einer schnellen Aktualisierung variiert die Lookback-Dauer des Ereignisses, da der Lookback-Zeitraum wöchentlich bzw. monatlich rolliert.
>
>Wenn Sie beispielsweise ein berechnetes Attribut mit einem Lookback-Zeitraum von zwei Wochen mit aktivierter schneller Aktualisierung erstellen, bedeutet dies, dass der anfängliche Lookback-Zeitraum zwei Wochen beträgt. Bei jeder täglichen Aktualisierung enthält der Lookback-Zeitraum jedoch Ereignisse aus dem zusätzlichen Tag. Diese Hinzufügung von Tagen dauert bis zum Beginn der nächsten Kalenderwoche, in der das Lookback-Fenster aktualisiert und auf zwei Wochen zurückgesetzt wird.

## Nächste Schritte

Weitere Informationen zum Erstellen und Verwalten berechneter Attribute finden Sie im Abschnitt [API-Handbuch für berechnete Attribute](./api.md) oder [UI-Handbuch für berechnete Attribute](./ui.md).
