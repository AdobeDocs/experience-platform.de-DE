---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Standardmäßige Warnhinweisregeln
description: 'In diesem Dokument werden die von Experience Platform bereitgestellten vordefinierten Warnhinweisregeln behandelt. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 16%

---


# Standardmäßige Warnhinweisregeln

Adobe Experience Platform bietet mehrere vordefinierte Warnhinweisregeln, die Sie für Ihr Unternehmen aktivieren können. Die nachstehende Tabelle enthält die Einzelheiten dieser von der Adobe bereitgestellten Warnregeln. Allgemeine Informationen zu Warnhinweisen in Experience Platform finden Sie in der [Warnhinweise - Übersicht](./overview.md).

| Regel  | Beschreibung | Auswertungsfrequenz | Wiederholungsfenster |
| --- | --- | --- | --- |
| Berechtigungsschwellenwert überschritten | Diese Warnung wird Trigger, wenn die Anzahl der erstellten Profile 80 % der Berechtigung Ihres Unternehmens überschreitet. | 30 Sekunden | K. A. |
| Keine Aufnahmeaktivität in den letzten 24 Stunden | Dieser Warnhinweis wird Trigger, wenn in den letzten 24 Stunden keine neuen Daten erfasst wurden. | 1 Tag | 1 Tag |
| SFTP-Quelle hat keine Daten erfasst | Dieser Warnhinweis wird Trigger, wenn eine [SFTP-Quelle](../../sources/connectors/cloud-storage/sftp.md) innerhalb eines bestimmten Zeitraums keine Daten erfasst hat. | 1 Tag | 1 Tag |
| Aufnahmefehlerrate überschritten | Diese Warnung wird Trigger, wenn die Fehlerrate bei der Datenerfassung 20 % überschreitet. | 30 Sekunden | 30 Sekunden |
| Feed-Nachricht | Dieser Warnhinweis, wenn eine Feed-Nachricht zur Identitätsfreigabe an einen Benutzer mit [Segmentübereinstimmung](../../segmentation/ui/segment-match.md) gesendet wurde. | K. A. | K. A. |
| Feedzugriff abgelehnt | Dieser Warnhinweis wird Trigger, wenn ein anderer Platform-Benutzer den Zugriff auf einen Identitäts-Sharing-Feed mithilfe von [Segmentübereinstimmung](../../segmentation/ui/segment-match.md) widerruft. | K. A. | K. A. |
| Feed geändert | Dieser Warnhinweis wird Trigger, wenn ein Identitäts-Sharing-Feed von einem Benutzer geändert wird, der [Segmentübereinstimmung](../../segmentation/ui/segment-match.md) verwendet. | K. A. | K. A. |
| Feed freigegeben | Dieser Warnhinweis wird Trigger, wenn ein Benutzer einen neuen Feed in [Segmentübereinstimmung](../../segmentation/ui/segment-match.md) freigegeben. | K. A. | nicht angegeben |
| Link-Anfrage | Dieser Warnhinweis wird Trigger, wenn ein Benutzer eine Verbindung zur Partnerfreigabe anfordert. | K. A. | K. A. |
| Linkaktion | Dieser Warnhinweis wird Trigger, wenn ein Benutzer eine Anfrage zur Verbindung zur Partnerfreigabe akzeptiert. | K. A. | K. A. |
| Segmentdefinition deaktiviert | Dieser Warnhinweis wird Trigger, wenn eine Segmentdefinition deaktiviert ist. | K. A. | K. A. |
| Verzögerung bei Segmentaufträgen | Dieser Warnhinweis wird Trigger, wenn der Abschluss von Segmentaufträgen länger als 150 Minuten dauert. | 30 Sekunden | 3 Stunden |
| Fehler beim Ausführen des Quellflusses | Dieser Warnhinweis wird Trigger, wenn bei der Aufnahme von Daten aus einer Quellverbindung ein Fehler auftritt. | K. A. | K. A. |
| Erfolgreiche Ausführung des Quellenflusses | Dieser Warnhinweis wird Trigger, wenn Daten erfolgreich aus einer Quellverbindung erfasst werden. | K. A. | K. A. |

{style=&quot;table-layout:auto&quot;}