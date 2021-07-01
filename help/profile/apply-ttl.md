---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatz; Datensatz; Live-Zeit; ttl; Time-to-Live;
solution: Experience Platform
title: Live-Zeiten für Datensätze
description: Dieses Dokument enthält allgemeine Anleitungen zur Time-to-Live (TTL) für Datensätze im Profilspeicher für Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# Time-to-Live (TTL) des Profildienstes

Mit dem Profildienst können Benutzer die Time-to-Live (TTL) auf Daten im Profilspeicher anwenden. TTL ist ein Mechanismus, der die Zeitdauer begrenzt, die Daten in einem Datensatz verbringen. Auf diese Weise können Sie automatisch Daten aus dem Profilspeicher entfernen, die für Ihre Anwendungsfälle nicht mehr nützlich sind.

Derzeit unterstützt Profil nur die TTL von Erlebnisereignissen.

## TTL für Erlebnisereignisse

Mit der TTL für Erlebnisereignisse können Sie TTL auf Datensätze anwenden, die für das Echtzeit-Kundenprofil aktiviert sind, um Daten aus dem Profilspeicher zu entfernen, die nicht mehr gültig sind.

>[!NOTE]
>
>Sie müssen sich an den Support wenden, um die TTL des Erlebnisereignisses in Ihren Datensätzen zu aktivieren.

Nach der Aktivierung der TTL für Erlebnisereignisse in einem für Profile aktivierten Datensatz wendet Platform in zwei Schritten automatisch den TTL-Ablaufwert auf die Erlebnisereignisdaten an:

1. Für alle neuen Daten, die in den Datensatz aufgenommen werden, wird der TTL-Ablaufwert zur Erfassungszeit angewendet.
2. Für alle vorhandenen Daten im Datensatz wird der TTL-Ablaufwert rückwirkend als einmaliger Aufstockungssystemauftrag angewendet. Sobald der TTL-Ablaufwert im Datensatz platziert wurde, werden Ereignisse, die älter als der TTL-Ablaufwert sind, sofort bei Ausführung des Systemauftrags gelöscht. Alle anderen Ereignisse werden entfernt, sobald sie ihre TTL-Ablaufwerte vom Zeitstempel des Ereignisses erreichen.

>[!NOTE]
>
>Sobald TTL angewendet wird, sind alle Daten, die älter als die Anzahl der Tage der TTL sind, **dauerhaft gelöscht** und können nicht wiederhergestellt werden.
> 
>Stellen Sie außerdem sicher, dass sich das Lookback-Fenster für das Segment innerhalb der TTL-Grenze befindet. Andernfalls können die Segmentergebnisse nach der Anwendung von TTL falsch werden. Wenn Sie beispielsweise eine TTL von 30 Tagen angewendet haben und ein Segment haben, das versucht hat, Daten von bis zu 45 Tagen anzuzeigen, würde das Segment falsche Profile erzeugen.
> 
>Daher sollten Sie nach Möglichkeit für alle Datensätze dieselbe TTL beibehalten, um die Auswirkungen verschiedener TTL-Werte auf verschiedene Datensätze in der Segmentierungslogik zu vermeiden.

Wenn Sie beispielsweise am 15. Mai einen TTL-Wert von 30 Tagen angewendet haben, würden die folgenden Schritte ausgeführt:

1. Für alle neuen Ereignisse wird bei der Erfassung ein TTL-Wert von 30 Tagen angewendet.
2. Alle vorhandenen Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden mit dem Systemauftrag sofort gelöscht.
3. Alle vorhandenen Ereignisse mit einem Zeitstempel, der neuer als der 15. April ist, haben einen TTL-Ablaufwert von 30 Tagen nach ihrem Ereignis-Zeitstempel. Wenn ein Ereignis also einen Zeitstempel vom 18. April hat, wird es dreißig Tage nach dem Datum dieses Zeitstempels gelöscht, also am 18. Mai.

