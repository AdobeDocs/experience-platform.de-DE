---
title: Snowflake Streaming Source Connector - Übersicht
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten von Ihrer Snowflake-Instanz in Adobe Experience Platform aufzunehmen
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 11%

---

# [!DNL Snowflake] Streaming-Quelle

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] Streaming-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.
>* Die [!DNL Snowflake] Streaming-Quelle ist in der API für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt Streaming-Daten von einer [!DNL Snowflake] Datenbank.

## Grundlagen zum [!DNL Snowflake] Streaming-Quelle

Die [!DNL Snowflake] Streaming-Quelle funktioniert durch das Laden von Daten, indem regelmäßig eine SQL-Abfrage ausgeführt und für jede Zeile der Ergebnismenge ein Ausgabedatensatz erstellt wird.

Durch Verwendung von [!DNL Kafka Connect], die [!DNL Snowflake] Streaming-Quelle verfolgt den neuesten Datensatz, den sie von jeder Tabelle erhält, sodass er an der richtigen Stelle für die nächste Iteration beginnen kann. Die Quelle verwendet diese Funktion, um Daten zu filtern und bei jeder Iteration nur die aktualisierten Zeilen aus einer Tabelle zu erhalten.

## Voraussetzungen

Im folgenden Abschnitt werden die erforderlichen Schritte beschrieben, die durchgeführt werden müssen, bevor Sie Daten von Ihrem [!DNL Snowflake] Datenbank zu Experience Platform:

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] zur Verbindung mit [!DNL Snowflake]müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Der vollständige Kontoname, der mit Ihrem [!DNL Snowflake] -Konto. Eine vollqualifizierte [!DNL Snowflake] Der Kontoname enthält Ihren Kontonamen, Ihre Region und Ihre Cloud-Plattform. Beispiel: `cj12345.east-us-2.azure`. Weiterführende Informationen zu Kontonamen finden Sie in diesem [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| `database` | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an Platform übermitteln möchten. |
| `username` | Der Benutzername für die [!DNL Snowflake] -Konto. |
| `password` | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| `role` | (Optional) Eine benutzerdefinierte Rolle, die für einen Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn dieser Wert nicht angegeben wird, wird standardmäßig `public`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Snowflake] is `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |


### Rolleneinstellungen konfigurieren {#configure-role-settings}

Sie müssen Berechtigungen für eine Rolle konfigurieren, auch wenn die standardmäßige öffentliche Rolle zugewiesen ist, damit Ihre Quellverbindung auf die [!DNL Snowflake] Datenbank, Schema und Tabelle. Die verschiedenen Berechtigungen für verschiedene [!DNL Snowflake] -Entitäten lautet wie folgt:

| [!DNL Snowflake] entity | Berechtigung &quot;Rolle anfordern&quot; |
| --- | --- |
| Warehouse | OPERATE, USAGE |
| Datenbank | NUTZUNG |
| Schema | NUTZUNG |
| Tabelle | SELECT |

>[!NOTE]
>
>Die automatische Wiederaufnahme und das automatische Aussetzen müssen in der Konfiguration der erweiterten Einstellungen Ihres Warehouse aktiviert sein.

Weiterführende Informationen zur Verwaltung von Rollen und Berechtigungen finden Sie im Abschnitt [[!DNL Snowflake] API-Referenz](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Einschränkungen und häufig gestellte Fragen {#limitations-and-frequently-asked-questions}

* Der Datendurchsatz für die [!DNL Snowflake] -Quelle enthält 2000 Datensätze pro Sekunde.
* Die Preise variieren je nach der aktiven Lagerzeit und der Lagergröße. Für [!DNL Snowflake] Quell-Integration, die kleinste Größe, x-kleine Warehouse ist ausreichend. Es wird empfohlen, das automatische Aussetzen zu aktivieren, damit das Warehouse selbst ausgesetzt werden kann, wenn es nicht in Verwendung ist.
* Die [!DNL Snowflake] -Quelle fragt die Datenbank alle zehn Sekunden nach neuen Daten ab.
* Konfigurationsoptionen:
   * Sie können eine `backfill` boolesches Flag für Ihre [!DNL Snowflake] Quelle beim Erstellen einer Quellverbindung.
      * Wenn die Aufstockung auf &quot;true&quot;festgelegt ist, wird der Wert für timestamp.initial auf 0 gesetzt. Das bedeutet, dass Daten mit einer Zeitstempelspalte abgerufen werden, die größer als 0 Epochenzeit ist.
      * Wenn die Aufstockung auf &quot;false&quot;festgelegt ist, wird der Wert für timestamp.initial auf -1 gesetzt. Das bedeutet, dass Daten mit einer Zeitstempelspalte abgerufen werden, die größer ist als die aktuelle Zeit (der Zeitpunkt, zu dem die Quelle beginnt zu erfassen).
   * Die Spalte mit dem Zeitstempel sollte wie folgt formatiert sein: `TIMESTAMP_LTZ` oder `TIMESTAMP_NTZ`. Wenn die Spalte mit dem Zeitstempel auf `TIMESTAMP_NTZ`, sollte die entsprechende Zeitzone, in der die Werte gespeichert werden, über die `timezoneValue` -Parameter. Wenn nicht angegeben, wird für den Wert standardmäßig UTC verwendet.
      * `TIMESTAMP_TZ` kann nicht in einer Zeitstempelspalte oder einer Zuordnung verwendet werden.

## Nächste Schritte

Im folgenden Tutorial erfahren Sie, wie Sie Ihre [!DNL Snowflake] Streaming-Quelle an Experience Platform mithilfe der API:

* [Streamen von Daten aus einem [!DNL Snowflake] Datenbank zum Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Streamen von Daten aus einem [!DNL Snowflake] Datenbank zum Experience Platform mithilfe des Arbeitsbereichs &quot;Quellen&quot;in der Experience Platform-Benutzeroberfläche](../../tutorials/ui/create/databases/snowflake-streaming.md)
