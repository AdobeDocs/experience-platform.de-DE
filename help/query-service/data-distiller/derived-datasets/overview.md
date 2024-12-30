---
title: Abgeleitete Datensätze
description: Abgeleitete Datensätze bieten eine praktische Möglichkeit, Datensätze Ihrer Wahl zu generieren, die regelmäßig aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden können. Dieses Dokument bietet einen Überblick darüber, wie Sie mit dem Abfrage-Service abgeleitete Datensätze zur Verwendung mit Ihren Profildaten erstellen.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Abgeleitete Datensätze

Die Funktion für abgeleitete Datensätze bietet eine praktische Möglichkeit, Datensätze Ihrer Wahl aus anderen im Data Lake verfügbaren Informationen zu generieren. Diese Datensätze können regelmäßig aktualisiert und optional in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden. Abgeleitete Datensätze decken die Notwendigkeit ab, komplexe Datensätze wie Dezilen, Perzentile und Quartil gegenüber einfacheren wie „max“, „count“ und „mean“ zu erstellen. Diese Datensätze können speziell für einen einzelnen Benutzer oder für eine Geschäftseinheit berechnet werden. Auf diese Weise können Sie Datensätze ableiten, die einer Kennung direkt akkreditiert werden können, z. B. E-Mail-Adressen, Geräte-IDs und Telefonnummern. Außerdem können Sie Datensätze ableiten, die indirekt mit diesem Benutzer oder Geschäftsprofil verknüpft sind.

Abgeleitete Datensätze sind für eine Vielzahl von Anwendungsfällen erforderlich, wenn Daten im Data Lake analysiert werden. Diese Daten können dann für die Verwendung im Echtzeit-Kundenprofil markiert und in nachgelagerten Anwendungsfällen wie der Erstellung hochfokussierter Zielgruppen verwendet werden. Zu den möglichen Anwendungsfällen für diese Funktion gehören:

* Identifizieren der niedrigsten 10 % der Abonnentinnen und Abonnenten basierend auf der Zuschauerzahl nach Kanal. Dadurch könnten Marketing-Fachleute eine bestimmte Zielgruppe ansprechen und ein neues Abonnentenpaket verkaufen.
* Identifizieren einer Zielgruppe, die zu den 10 % der besten Flyer gehört, basierend auf ihrer Gesamtzahl der zurückgelegten Meilen und den Status „Flyer“ hat. Diese Zielgruppe könnte verwendet werden, um den Verkauf eines neuen Kreditkartenangebots gezielt anzusprechen.
* Bestimmen Sie die Abwanderungsrate basierend auf der Anmeldung.
* Die Identifizierung des obersten 1% des Haushaltseinkommens in einer Provinz oder einem Bundesstaat und die Bereitstellung einer Messgröße für die Anzahl der Personen, die in den letzten „n“ Monaten aus dieser kollektiven Gruppe auswandern.

## Komplexe abgeleitete Datensätze

Um ein Ranking auf der Grundlage einer oder mehrerer Metriken (z. B. Umsatz, Dauer der Zuschauerschaft usw.) für eine bestimmte Dimension (Kategorie) zu erstellen, sind komplexe abgeleitete Datensätze erforderlich. Dezilen, Quartilen und Perzentile ermöglichen Flexibilität und Präzision bei der Rangfolge von Daten mit abgeleiteten Datensätzen.

Ein Dezil ist eine Methode, einen Satz von Rangfolgedaten in 10 gleiche Teile aufzuteilen. Wenn die Daten in Dezilen aufgeteilt werden, wird jeder Zeile im Datensatz ein Dezilrang zugewiesen. Dadurch können die Daten in absteigender oder aufsteigender Reihenfolge sortiert werden.

Ein Dezile-Rang ordnet die Daten in der Reihenfolge vom niedrigsten zum höchsten an und erfolgt auf einer Skala von 1 bis 10, wobei jede aufeinander folgende Zahl einer Zunahme von 10 Prozentpunkten entspricht.

Dezil-Buckets stellen die Anzahl der rangierten Gruppen dar und werden verwendet, um einer Dimension (Kategorie) im Datensatz einen Rang zuzuweisen. Der Bucket kann eine Zahl oder ein Ausdruck sein, der für jede Partition als positiver ganzzahliger Wert ausgewertet wird. Die Buckets dürfen keinen Nullwert haben.

Quartile werden verwendet, um die Verteilung durch vier und Perzentile durch 100 zu teilen.

## Abgeleitete Analysedatensätze

Query Service bietet integrierte Funktionen wie Sitzungserstellung und Letztkontakt, die Sie u. a. auf beliebige Zeitreihendaten anwenden können, um geschäftsbezogene abgeleitete Datensätze zu generieren. Sie haben die Möglichkeit, diese analytisch abgeleiteten Datensätze auf einer oder mehreren Identitäten zu basieren und die Daten bei Bedarf im Echtzeit-Kundenprofil zu veröffentlichen.

Einige mögliche Anwendungsfälle für diesen Typ abgeleiteter Attribute sind:

* Tracking von Produkten, die während einer Benutzersitzung gescannt wurden und nicht vorrätig waren.
* Verfolgen beliebter Metriken wie Größe, Farbe oder Produktkategorie der durchsuchten oder gekauften Produkte.
* Tracking der Plattformquelle, die zu einem Produktbrowser oder -kauf geführt hat.
* Verfolgen des zuletzt durchsuchten Elements nach einer Identität.
* Tracking-Metriken wie die durchschnittliche Anzahl der Artikel in einem Warenkorb, Warenkorbabbrüche oder die durchschnittliche Kaufhäufigkeit.

## Andere abgeleitete Datensätze

Sie können Geschäftsmetriken auch als abgeleitetes Attribut berechnen und sie zusammen mit einfachen Datensätzen wie Postleitzahlen oder einer aggregierten Metrik wie der Gesamtanzahl verwenden. Beispiel: eine Gesamtanzahl basierend auf einer Stadt oder Provinz oder eine Gesamtanzahl basierend auf einer Geschäftskategorie und einer Stadt/Provinz.

## Nächste Schritte und Anwendungsfälle

Durch das Lesen dieses Dokuments wissen Sie besser, wie von Query Service abgeleitete Datensätze komplexe Anwendungsfälle erleichtern, um den Nutzen Ihrer Daten zu maximieren. Als Nächstes sollten Sie den Anwendungsfall [Dezil-basierte abgeleitete Attribute](../../use-cases/deciles-use-case.md) lesen, um zu sehen, wie diese Funktion in einem realen Szenario angewendet wird.
