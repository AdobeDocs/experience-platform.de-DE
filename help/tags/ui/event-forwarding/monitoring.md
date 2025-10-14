---
title: Überwachen von Aktivitäten bei der Ereignisweiterleitung
description: Erfahren Sie, wie Sie Nutzung, Fehler und Berechnungszeit in Ihren Ereignisweiterleitungseigenschaften überwachen.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: f8988d08e7009cc613a00f34e8151e8560c479d4
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 4%

---

# Überwachen von Aktivitäten in der Ereignisweiterleitung (Beta)

>[!IMPORTANT]
>
>Diese Feature befindet sich derzeit in der Beta-Phase, und Ihre Organisation hat möglicherweise noch keinen Zugriff darauf. Die Funktionalität und Dokumentation können sich ändern.

Auf **[!UICONTROL Registerkarte]** Monitoring“ in der Datenerfassungs-Benutzeroberfläche können Sie Nutzungsmuster, Fehler und die Verarbeitungszeit für die Eigenschaften der Ereignisweiterleitung überwachen. Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie die auf der Registerkarte angezeigten Berichte angezeigt und verstanden werden.

![Bild, das die Registerkarte „Monitoring“ in der Datenerfassungs-Benutzeroberfläche zeigt](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie die Ereignisweiterleitung erworben haben und dass Sie wissen, wie die Ereignisweiterleitung funktioniert. Weitere Informationen finden [&#x200B; in der Übersicht &#x200B;](./overview.md) die Ereignisweiterleitung .

## Videoüberblick

Sehen Sie sich das folgende Video an, um einen allgemeinen Überblick über die Überwachungsfunktion zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3412565?quality=12&learn=on&captions=ger)

## Auswählen von Eigenschaften und Umgebungen

Sie können Metriken in einer einzelnen Umgebung und Eigenschaft oder über alle Eigenschaften und Umgebungen hinweg anzeigen, die Ihrem Unternehmen gehören.

Um Metriken für eine einzelne Eigenschaft anzuzeigen, wählen Sie im Dropdown-Menü Eigenschaft die gewünschte Eigenschaft aus der Liste aus. Nachdem Sie eine Eigenschaft ausgewählt haben, können Sie auch das Dropdown-Menü „Umgebung“ verwenden, um eine gewünschte Umgebung auszuwählen.

![Bild mit den Dropdown-Menüs der Eigenschaftsumgebung in der Benutzeroberfläche](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Verwendung]

>[!NOTE]
>
>Nutzungsdaten werden jeden Monat nach Ablauf des vorherigen Monats aktualisiert.

Der **[!UICONTROL Usage]**-Bericht zeigt eingehende und ausgehende Aufrufe für einen bestimmten Zeitraum. Eingehende Aufrufe stellen Daten dar, die an die Ereignisweiterleitung gesendet werden. Ausgehende Aufrufe stellen Daten dar, die von der Ereignisweiterleitung gesendet werden. Die **[!UICONTROL Gesamtzahl]** Ereignisse“ im linken Bereich ist die Summe der eingehenden und ausgehenden Aufrufe für den jeweiligen Zeitraum.

## [!UICONTROL Fehlerereignisse]

Der Bericht **[!UICONTROL Fehlerereignisse]** zeigt Fehler in der Zusammenfassung an und wird nach HTTP-Antwort-Code aufgeschlüsselt, wenn Sie den Cursor über das Liniendiagramm bewegen. Die angezeigten Fehler stammen aus ausgehenden Aufrufen, und die Antwort-Codes stammen vom Endpunkt, mit dem die Ereignisweiterleitung interagiert.

Die Fehler werden für einen bestimmten Zeitraum angezeigt, der über das bereitgestellte Dropdown-Menü angepasst werden kann.

![Bild mit dem Dropdown-Menü „Zeitraum“ für den Bericht zu Fehlerereignissen](../../images/ui/event-forwarding/monitoring/error-time.png)

Mit dem Suchfeld für das Fehlerereignis können Sie die Ereignisweiterleitung abfragen, um Fehler für eine bestimmte Endpunkt-Domain zu verstehen. Sie müssen die exakte Domain eingeben, da die Suchfunktion keine Annäherungen oder „Fuzzy“-Treffer akzeptiert. Sobald Sie eine exakte Domain angegeben haben, für die ausgehende Fehlerdaten vorliegen, drücken Sie die Eingabetaste und der Bericht wird aktualisiert, um ausgehende Fehler für diese Domain anzuzeigen. Um beispielsweise Fehler vom Facebook Conversions-API-Endpunkt anzuzeigen, sollte die Domain wie `https://graph.facebook.com` geschrieben werden.

## [!UICONTROL Berechnungszeit]

Der **[!UICONTROL Berechnungszeit]**-Bericht zeigt die Berechnungszeit aller Regeln für Ereignisweiterleitungs-Server an.

>[!NOTE]
>
>Die angezeigten Zeiten stellen keine End-to-End-Latenz dar. Die Ereignisweiterleitung hat eine Compute-Time-Beschränkung von 50 Millisekunden. Wenn diese Grenze überschritten wird, werden die zugehörigen Daten gelöscht.

Die folgenden Faktoren wirken sich auf die Rechenzeit aus:

1. Die Anzahl der Regeln
2. Die Komplexität der Regeln, die in der Regel durch die Anzahl der ausgeführten benutzerdefinierten JavaScript bedingt ist

Wenn beispielsweise eine Aktion in der Ereignisweiterleitung einen Endpunkt trifft und dieser Endpunkt zwei Sekunden benötigt, um zu antworten, wird diese Zwei-Sekunden-Latenz nicht für die Berechnungszeit gezählt, da die Ereignisweiterleitung nur wartet und nicht aktiv etwas berechnet. Die Antwortzeit darf 30 Sekunden nicht überschreiten. Andernfalls werden die Daten gelöscht.
