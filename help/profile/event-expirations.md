---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatz; Datensätze; Time to Live; ttl; Time-to-Live;
solution: Experience Platform
title: Ablauf von Erlebnisereignissen
description: Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren der Ablaufzeiten für einzelne Erlebnisereignisse in einem Adobe Experience Platform-Datensatz.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# Ablauf von Erlebnisereignissen

In Adobe Experience Platform können Sie Ablaufzeiten für alle Erlebnisereignisse konfigurieren, die in einen Datensatz erfasst werden, der für [Echtzeit-Kundenprofil](./home.md). Auf diese Weise können Sie automatisch Daten aus dem Daten-Pool und Profilspeicher entfernen, die für Ihre Anwendungsfälle nicht mehr gültig oder nützlich sind.

Experience Event-Abläufe können nicht über die Platform-Benutzeroberfläche oder APIs konfiguriert werden. Stattdessen müssen Sie sich an den Support wenden, um Erlebnisereignisse für Ihre erforderlichen Datensätze zu aktivieren.

>[!IMPORTANT]
>
>Experience Event-Abläufe dürfen nicht mit Datensatzabläufen verwechselt werden, die den gesamten Datensatz löschen, nachdem das Ablaufdatum erreicht wurde. Diese werden manuell konfiguriert über [Adobe Experience Platform-Datenhygiene](../hygiene/home.md).

## Automatisierter Ablauf

Nachdem der Ablauf von Erlebnisereignissen für einen Datensatz mit aktiviertem Profil aktiviert wurde, wendet Platform die Ablaufwerte automatisch für jedes erfasste Ereignis in einem zweistufigen Prozess an:

1. Bei allen neuen Daten, die in den Datensatz aufgenommen werden, wird der Ablaufwert zur Erfassungszeit angewendet.
1. Für alle vorhandenen Daten im Datensatz wird der Ablaufwert rückwirkend als einmaliger Aufstockungssystemauftrag angewendet. Sobald der Ablaufwert im Datensatz platziert wurde, werden Ereignisse, die älter als der Ablaufwert sind, sofort bei Ausführung des Systemauftrags gelöscht. Alle anderen Ereignisse werden entfernt, sobald sie ihre Ablaufwerte aus dem Ereigniszeitstempel erreichen.

>[!WARNING]
>
>Nach der Anwendung werden alle Daten, die älter sind als die Anzahl der Tage, die durch den Ablaufwert zulässig sind, **permanent gelöscht** und kann nicht wiederhergestellt werden.

Wenn Sie beispielsweise am 15. Mai einen Ablaufwert von 30 Tagen angewendet haben, würden die folgenden Schritte ausgeführt:

1. Für alle neuen Ereignisse wird bei der Erfassung ein Ablaufwert von 30 Tagen angewendet.
1. Alle vorhandenen Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden mit dem Systemauftrag sofort gelöscht.
1. Alle vorhandenen Ereignisse mit einem Zeitstempel, der neuer als der 15. April ist, haben einen Ablaufwert von 30 Tagen nach ihrem Ereigniszeitstempel. Wenn ein Ereignis also einen Zeitstempel vom 18. April hat, wird es 30 Tage nach dem Datum dieses Zeitstempels gelöscht, also am 18. Mai.

## Auswirkungen auf die Segmentierung

Sie müssen sicherstellen, dass die Lookback-Fenster für Ihre Segmente innerhalb der Ablaufgrenzen ihrer abhängigen Datensätze liegen, um die Ergebnisse genau zu halten. Wenn Sie beispielsweise einen Ablaufwert von 30 Tagen anwenden und ein Segment verwenden, das versucht, Daten aus bis zu 45 Tagen anzuzeigen, ist die resultierende Zielgruppe wahrscheinlich ungenau.

Daher sollten Sie nach Möglichkeit für alle Datensätze denselben Ablaufwert für Erlebnisereignisse beibehalten, um die Auswirkungen verschiedener Ablaufwerte auf verschiedene Datensätze in Ihrer Segmentierungslogik zu vermeiden.
