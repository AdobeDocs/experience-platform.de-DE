---
title: Abgeleitete Datensätze
description: Abgeleitete Datensätze bieten eine praktische Möglichkeit, um Datensätze Ihrer Wahl zu generieren, die bei jeder regulären Platzierung aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden können. Dieses Dokument bietet einen Überblick darüber, wie Sie mit Query Service abgeleitete Datensätze erstellen können, die mit Ihren Profildaten verwendet werden.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Abgeleitete Datensätze

Die Funktion für abgeleitete Datensätze bietet eine praktische Möglichkeit, Datensätze Ihrer Wahl aus anderen im Data Lake verfügbaren Informationen zu generieren. Diese Datensätze können in jedem regulären Fall aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden. Abgeleitete Datensätze decken die Notwendigkeit ab, komplexe Datensätze wie Dezimal, Perzentil und Quartil über einfachere Datensätze wie max, count und average zu erstellen. Diese Datensätze können speziell für einen einzelnen Benutzer oder für eine Geschäftsentität berechnet werden. Auf diese Weise können Sie Datensätze ableiten, die direkt für eine Kennung akkreditiert werden können, z. B. E-Mail-Adressen, Geräte-IDs und Telefonnummern, und Datensätze ableiten, die indirekt mit diesem Benutzer oder Geschäftsprofil verknüpft sind.

Abgeleitete Datensätze werden für eine Vielzahl von Anwendungsfällen benötigt, wenn Daten im Data Lake analysiert werden. Diese Daten können dann für die Verwendung im Echtzeit-Kundenprofil markiert und in nachgelagerten Anwendungsfällen wie der Erstellung hochfokussierter Zielgruppen verwendet werden. Einige potenzielle Anwendungsfälle für diese Funktion könnten sein:

* Identifizieren der niedrigsten 10 % der Abonnenten basierend auf der Kanalanzeige. Auf diese Weise können Marketing-Experten eine bestimmte Zielgruppe ansprechen und ein neues Abonnentenpaket verkaufen.
* Identifizieren einer Zielgruppe, die zu den 10 % der Flugzeuge gehört, basierend auf ihrer Gesamtzahl der Flugmeilen, die sie zurückgelegt haben, und deren Status &quot;Flyer&quot; lautet. Diese Zielgruppe kann verwendet werden, um gezielt den Verkauf eines neuen Kreditkartenangebots anzusprechen.
* Bestimmen Sie die Abwanderungsrate basierend auf dem Abonnement.
* Ermittlung des obersten 1 % des Haushaltseinkommens in einer Provinz oder einem Bundesstaat und Angabe der Zahl der Personen, die in den letzten &quot;n&quot;Monaten aus dieser Gruppe ausscheiden.

## Komplexe abgeleitete Datensätze

Um eine Rangfolge basierend auf einer oder mehreren Metriken (z. B. Umsatz, Besucherdauer usw.) für eine bestimmte Dimension (Kategorie) zu erstellen, sind komplexe abgeleitete Datensätze erforderlich. Dekaden, Quartil und Perzentile ermöglichen Flexibilität und Präzision bei der Rangordnung von Daten mit abgeleiteten Datensätzen.

Eine Dezimalzahl ist eine Methode, einen Satz von Rangdaten in 10 gleiche Teile aufzuteilen. Wenn die Daten in Dezimalzahlen unterteilt sind, wird jeder Zeile des Datensatzes ein Dezimalrang zugewiesen. Dadurch können die Daten in absteigender oder aufsteigender Reihenfolge sortiert werden.

Ein Dezimalrang ordnet die Daten in der Reihenfolge von unten nach oben an und erfolgt auf einer Skala von 1 bis 10, wobei jede aufeinander folgende Zahl einer Steigerung von 10 Prozentpunkten entspricht.

Decile Buckets stellen die Anzahl der Ranggruppen dar und werden verwendet, um einer Dimension (Kategorie) im Datensatz eine Rangfolge zuzuweisen. Der Bucket kann eine Zahl oder ein Ausdruck sein, der als positiver ganzzahliger Wert für jede Partition ausgewertet wird. Die Behälter dürfen keinen Nullwert haben.

Quartile werden verwendet, um die Verteilung durch vier und Perzentile durch 100 zu teilen.

## Analytische abgeleitete Datensätze

Query Service bietet integrierte Funktionen wie Sitzungserstellung und Letztkontakt, die Sie auf alle Zeitreihendaten anwenden können, um geschäftsbezogene abgeleitete Datensätze zu generieren. Sie haben die Möglichkeit, diese analytisch abgeleiteten Datensätze auf einer oder mehreren Identitäten zu basieren und die Daten optional im Echtzeit-Kundenprofil zu veröffentlichen, falls erforderlich.

Einige potenzielle Anwendungsfälle für diesen Typ von abgeleiteten Attributen können Folgendes umfassen:

* Tracking von Produkten, die während einer Benutzersitzung gescannt wurden und nicht vorrätig waren.
* Tracking beliebter Metriken wie Größe, Farbe oder Produktkategorie der Produkte, die durchsucht oder gekauft werden.
* Verfolgen der Plattformquelle, die zu einem Produktdurchsuchen oder Einkauf geführt hat.
* Tracking des zuletzt durchsuchten Elements anhand einer Identität.
* Tracking-Metriken wie durchschnittliche Artikelanzahl im Warenkorb, Warenkorbabbruch oder durchschnittliche Kaufhäufigkeit.

## Andere abgeleitete Datensätze

Sie können Geschäftsmetriken auch als abgeleitetes Attribut berechnen und in Verbindung mit einfachen Datensätzen wie Postleitzahl oder einer aggregierten Metrik wie der Gesamtanzahl verwenden. Beispielsweise die Gesamtzahl basierend auf einer Stadt oder Provinz oder die Gesamtzahl anhand einer Geschäftskategorie und einer Stadt/Provinz.

## Nächste Schritte und Anwendungsfälle

Durch Lesen dieses Dokuments können Sie besser verstehen, wie abgeleitete Datensätze aus Query Service komplexe Anwendungsfälle zur Maximierung der Nützlichkeit Ihrer Daten erleichtern. Als Nächstes sollten Sie die [Anwendungsfall für dezimalbasierte abgeleitete Attribute](../../use-cases/deciles-use-case.md) um zu sehen, wie diese Funktion in einem realen Szenario angewendet wird.
