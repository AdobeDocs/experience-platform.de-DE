---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz;Datensätze;Time to Live;ttl;Time-to-Live;
solution: Experience Platform
title: Gültigkeitsdauern von Erlebnisereignissen
description: Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren der Gültigkeitsdauern für einzelne Erlebnisereignisse in einem Adobe Experience Platform-Datensatz.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 0fce883528abc62075914abc4a8f81d2bff8f2e6
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 90%

---

# Gültigkeitsdauern von Erlebnisereignissen

In Adobe Experience Platform können Sie Ablaufzeiten für alle Erlebnisereignisse konfigurieren, die in einen Datensatz erfasst werden, der für [Echtzeit-Kundenprofil](./home.md). Auf diese Weise können Sie automatisch Daten aus dem Profilspeicher entfernen, die für Ihre Anwendungsfälle nicht mehr nützlich sind.

Gültigkeitsdauern von Erlebnisereignissen können nicht über die Platform-Benutzeroberfläche oder APIs konfiguriert werden. Stattdessen müssen Sie sich an den Support wenden, um Gültigkeitsdauern von Erlebnisereignissen für Ihre erforderlichen Datensätze zu aktivieren.

>[!IMPORTANT]
>
>Gültigkeitsdauern von Erlebnisereignissen sind nicht mit Gültigkeitsdauern von Datensätzen zu verwechseln, bei denen nach Erreichen des Ablaufdatums der gesamte Datensatz gelöscht wird. Diese werden manuell über die [Adobe Experience Platform-Datenhygiene](../hygiene/home.md) konfiguriert.

## Automatisierter Prozess zur Gültigkeitsdauer

Nachdem Gültigkeitsdauern von Erlebnisereignissen für einen Datensatz mit aktiviertem Profil aktiviert wurden, wendet Platform die Gültigkeitswerte für jedes erfasste Ereignis in einem zweistufigen Prozess automatisch an:

1. Bei allen neuen Daten, die in den Datensatz aufgenommen werden, wird der Ablaufwert zur Aufnahmezeit auf der Grundlage des Ereignis-Zeitstempels angewendet.
1. Für alle bereits vorhandenen Daten im Datensatz wird der Ablaufwert rückwirkend als einmaliger Systemauftrag zur Aufstockung angewendet. Sobald der Gültigkeitswert im Datensatz platziert wurde, werden Ereignisse, die älter als der Gültigkeitswert sind, bei Ausführung des Systemauftrags sofort gelöscht. Alle anderen Ereignisse werden entfernt, sobald sie ihre Gültigkeitswerte vom Zeitstempel des Ereignisses erreichen. Wenn alle Erlebnisereignisse entfernt wurden und das Profil keine Profilattribute mehr aufweist, existiert das Profil nicht mehr.

>[!WARNING]
>
>Nach der Anwendung werden alle Daten, die älter sind als die Anzahl der Tage, die entsprechend dem Gültigkeitswert zulässig sind, **permanent gelöscht** und können nicht wiederhergestellt werden.

Wenn Sie beispielsweise am 15. Mai einen Gültigkeitswert von 30 Tagen angewendet haben, würden die folgenden Schritte eintreten:

1. Für alle neuen Ereignisse wird bei der Aufnahme ein Gültigkeitswert von 30 Tagen angewendet.
1. Alle vorhandenen Ereignisse mit einem Zeitstempel, der vor dem 15. April liegt, werden mit dem Systemauftrag sofort gelöscht.
1. Alle vorhandenen Ereignisse mit einem Zeitstempel, der neuer als der 15. April ist, haben einen Gültigkeitswert von 30 Tagen ab ihrem Ereignis-Zeitstempel. Wenn ein Ereignis also einen Zeitstempel vom 18. April hat, wird es dreißig Tage nach dem Datum dieses Zeitstempels gelöscht, also am 18. Mai.

## Auswirkungen auf die Segmentierung

Sie müssen sicherstellen, dass die Lookback-Fenster für Ihre Segmente innerhalb der Gültigkeitsgrenzen ihrer abhängigen Datensätze liegen, um die Ergebnisse genau zu halten. Wenn Sie beispielsweise einen Gültigkeitswert von 30 Tagen anwenden und ein Segment verwenden, das versucht, Daten von bis zu 45 Tagen anzuzeigen, ist die resultierende Audience wahrscheinlich ungenau.

Daher sollten Sie nach Möglichkeit für alle Datensätze denselben Gültigkeitswert für Erlebnisereignisse beibehalten, um die Auswirkungen verschiedener Gültigkeitswerte auf verschiedene Datensätze in Ihrer Segmentierungslogik zu vermeiden.
