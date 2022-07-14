---
title: Abgeleitete Attribute
description: Abgeleitete Attribute bieten eine praktische Möglichkeit, um Attribute Ihrer Wahl zu generieren, die bei jeder regulären Platzierung aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden können. Dieses Dokument bietet einen Überblick darüber, wie Sie mit Query Service abgeleitete Attribute zur Verwendung mit Ihren Profildaten erstellen können.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 61e0895484b8005e2109056d51557f609fecaf97
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Abgeleitete Attribute

Die abgeleitete Attributfunktion bietet eine praktische Möglichkeit, Attribute Ihrer Wahl aus anderen im Data Lake verfügbaren Informationen zu generieren. Diese Attribute können in jedem normalen Cadence aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden. Abgeleitete Attribute decken die Notwendigkeit ab, komplexe Attribute wie Dezimalzahl, Perzentil und Quartil über einfachere Attribute wie max, count und average zu erstellen. Diese Attribute können speziell für einen einzelnen Benutzer oder für eine Geschäftsentität berechnet werden. Auf diese Weise können Sie Attribute ableiten, die direkt für eine Kennung akkreditiert werden können, z. B. E-Mail-Adressen, Geräte-IDs und Telefonnummern, und Attribute ableiten, die indirekt mit diesem Benutzer oder Geschäftsprofil verknüpft sind.

Abgeleitete Attribute werden für eine Vielzahl von Anwendungsfällen benötigt, wenn Daten im Data Lake analysiert werden. Diese Daten können dann für die Verwendung im Echtzeit-Kundenprofil markiert und in nachgelagerten Anwendungsfällen wie der Erstellung hochfokussierter Zielgruppen verwendet werden. Einige potenzielle Anwendungsfälle für diese Funktion könnten sein:

* Identifizieren der niedrigsten 10 % der Abonnenten basierend auf der Kanalanzeige. Dadurch können Marketing-Experten eine bestimmte Zielgruppe ansprechen und ein neues Abonnentenpaket verkaufen.
* Identifizieren einer Zielgruppe, die zu den 10 % der Flugzeuge gehört, basierend auf ihrer Gesamtzahl der Flugmeilen, die sie zurückgelegt haben, und deren Status &quot;Flyer&quot; lautet. Diese Zielgruppe kann verwendet werden, um gezielt den Verkauf eines neuen Kreditkartenangebots anzusprechen.
* Bestimmen Sie die Abwanderungsrate basierend auf dem Abonnement.
* Ermittlung des obersten 1 % des Haushaltseinkommens in einer Provinz oder einem Bundesstaat und Angabe der Zahl der Personen, die in den letzten &quot;n&quot;Monaten aus dieser Gruppe ausscheiden.

## Komplexe abgeleitete Attribute

Um eine Rangfolge basierend auf einer oder mehreren Metriken (z. B. Umsatz, Besucherdauer usw.) für eine bestimmte Dimension (Kategorie) zu erstellen, sind komplexe abgeleitete Attribute erforderlich. Dekaden, Quartil und Perzentile ermöglichen Flexibilität und Präzision bei der Rangordnung von Daten mit abgeleiteten Attributen.

Eine Dezimalzahl ist eine Methode, einen Satz von Rangdaten in 10 gleiche Teile aufzuteilen. Wenn die Daten in Dezimalzahlen unterteilt sind, wird jeder Zeile des Datensatzes ein Dezimalrang zugewiesen. Dadurch können die Daten in absteigender oder aufsteigender Reihenfolge sortiert werden.

Ein Dezimalrang ordnet die Daten in der Reihenfolge von unten nach oben an und erfolgt auf einer Skala von 1 bis 10, wobei jede aufeinander folgende Zahl einer Steigerung von 10 Prozentpunkten entspricht.

Decile Buckets stellen die Anzahl der Ranggruppen dar und werden verwendet, um einer Dimension (Kategorie) im Datensatz eine Rangfolge zuzuweisen. Der Bucket kann eine Zahl oder ein Ausdruck sein, der als positiver ganzzahliger Wert für jede Partition ausgewertet wird. Die Behälter dürfen keinen Nullwert haben.

Quartile werden verwendet, um die Verteilung durch vier und Perzentile durch 100 zu teilen.

## Analytische abgeleitete Attribute

Query Service bietet unter anderem integrierte Funktionen wie Sitzungserstellung und Letztkontakt, die Sie auf alle Zeitreihendaten anwenden können, um geschäftsbezogene abgeleitete Attribute zu generieren. Sie haben die Möglichkeit, diese analytischen abgeleiteten Attribute auf einer oder mehreren Identitäten zu basieren und die Daten bei Bedarf optional in Echtzeit-Kundenprofil zu veröffentlichen.

Einige potenzielle Anwendungsfälle für diesen Typ von abgeleiteten Attributen können Folgendes umfassen:

* Tracking von Produkten, die während einer Benutzersitzung gescannt wurden und nicht vorrätig waren.
* Tracking beliebter Metriken wie Größe, Farbe oder Produktkategorie der Produkte, die durchsucht oder gekauft werden.
* Verfolgen der Plattformquelle, die zu einem Produktdurchsuchen oder Einkauf geführt hat.
* Tracking des zuletzt durchsuchten Elements anhand einer Identität.
* Tracking-Metriken wie durchschnittliche Artikelanzahl im Warenkorb, Warenkorbabbruch oder durchschnittliche Kaufhäufigkeit.

## Andere abgeleitete Attribute

Sie können Geschäftsmetriken auch als abgeleitetes Attribut berechnen und in Verbindung mit einfachen Attributen wie Postleitzahl oder einer aggregierten Metrik wie der Gesamtanzahl verwenden. Beispielsweise die Gesamtzahl basierend auf einer Stadt oder Provinz oder die Gesamtzahl anhand einer Geschäftskategorie und einer Stadt/Provinz.

## Nächste Schritte und Anwendungsfälle

Durch Lesen dieses Dokuments können Sie besser verstehen, wie abgeleitete Attribute von Query Service komplexe Anwendungsfälle zur Maximierung der Nützlichkeit Ihrer Daten erleichtern. Als Nächstes sollten Sie die [Anwendungsfall für dezimalbasierte abgeleitete Attribute](./deciles-use-case.md) um zu sehen, wie diese Funktion in einem realen Szenario angewendet wird.
