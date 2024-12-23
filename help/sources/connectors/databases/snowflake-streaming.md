---
title: Snowflake Streaming Source Connector - Übersicht
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten von Ihrer Snowflake-Instanz in Adobe Experience Platform aufzunehmen
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 34b1676ebb5405d73cf37cd786d1e6c26cb8fdaa
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 18%

---

# [!DNL Snowflake] Streaming-Quelle

>[!IMPORTANT]
>
> Die Streaming-Quelle [!DNL Snowflake] steht in der API Benutzern zur Verfügung, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt Streaming-Daten aus einer [!DNL Snowflake] -Datenbank.

## Grundlegendes zur Streaming-Quelle [!DNL Snowflake]

Die Streaming-Quelle [!DNL Snowflake] funktioniert durch das Laden von Daten, indem regelmäßig eine SQL-Abfrage ausgeführt und für jede Zeile in der Ergebnismenge ein Ausgabedatensatz erstellt wird.

Durch die Verwendung von [!DNL Kafka Connect] zeichnet die Streaming-Quelle [!DNL Snowflake] den neuesten Datensatz auf, den sie von jeder Tabelle erhält, sodass sie an der richtigen Stelle für die nächste Iteration beginnen kann. Die Quelle verwendet diese Funktion, um Daten zu filtern und bei jeder Iteration nur die aktualisierten Zeilen aus einer Tabelle zu erhalten.

## Voraussetzungen

Im folgenden Abschnitt werden die erforderlichen Schritte beschrieben, die ausgeführt werden müssen, bevor Sie Daten von Ihrer [!DNL Snowflake]-Datenbank an Experience Platform streamen können:

### Aktualisieren der IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources).

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Amazon Redshift] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Snowflake] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Die vollständige Kontokennung (Kontoname oder Kontostandort) Ihres [!DNL Snowflake]-Kontos, das mit dem Suffix `snowflakecomputing.com` angehängt wird. Die Kontokennung kann in verschiedenen Formaten verwendet werden: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (z. B. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (z. B. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (z. B. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Weitere Informationen finden Sie unter [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Das [!DNL Snowflake]-Warehouse verwaltet den Abfrageausführungsprozess für die Anwendung. Jedes [!DNL Snowflake]-Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| `database` | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an die Plattform übermitteln möchten. |
| `username` | Der Benutzername für das [!DNL Snowflake]-Konto. |
| `password` | Das Kennwort für das [!DNL Snowflake] -Benutzerkonto. |
| `role` | (Optional) Eine benutzerdefinierte Rolle, die für einen Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn dieser Wert nicht angegeben wird, wird standardmäßig `public` verwendet. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Snowflake] ist `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

### Rolleneinstellungen konfigurieren {#configure-role-settings}

Sie müssen Berechtigungen für eine Rolle konfigurieren, auch wenn die standardmäßige öffentliche Rolle zugewiesen ist, damit Ihre Quellverbindung auf die relevante [!DNL Snowflake] -Datenbank, das Schema und die Tabelle zugreifen kann. Die verschiedenen Berechtigungen für verschiedene [!DNL Snowflake] -Entitäten lauten wie folgt:

| [!DNL Snowflake] entity | Berechtigung &quot;Rolle anfordern&quot; |
| --- | --- |
| Warehouse | OPERATE, USAGE |
| Datenbank | NUTZUNG |
| Schema | NUTZUNG |
| Tabelle | SELECT |

>[!NOTE]
>
>Die automatische Wiederaufnahme und das automatische Aussetzen müssen in der Konfiguration der erweiterten Einstellungen Ihres Warehouse aktiviert sein.

Weiterführende Informationen zur Rollen- und Berechtigungsverwaltung finden Sie in der [[!DNL Snowflake] API-Referenz](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Einschränkungen und häufig gestellte Fragen {#limitations-and-frequently-asked-questions}

* Der Datendurchsatz für die Quelle [!DNL Snowflake] beträgt 2000 Datensätze pro Sekunde.
* Die Preise variieren je nach der aktiven Lagerzeit und der Lagergröße. Für die Quell-Integration von [!DNL Snowflake] ist das kleinste, x-kleine Warehouse ausreichend. Es wird empfohlen, das automatische Aussetzen zu aktivieren, damit das Warehouse selbst ausgesetzt werden kann, wenn es nicht in Verwendung ist.
* Die [!DNL Snowflake] -Quelle fragt die Datenbank alle 10 Sekunden nach neuen Daten ab.
* Konfigurationsoptionen:
   * Sie können beim Erstellen einer Quellverbindung eine boolesche Markierung `backfill` für Ihre [!DNL Snowflake] Quelle aktivieren.
      * Wenn die Aufstockung auf &quot;true&quot;festgelegt ist, wird der Wert für timestamp.initial auf 0 gesetzt. Das bedeutet, dass Daten mit einer Zeitstempelspalte abgerufen werden, die größer als 0 Epochenzeit ist.
      * Wenn die Aufstockung auf &quot;false&quot;festgelegt ist, wird der Wert für timestamp.initial auf -1 gesetzt. Das bedeutet, dass Daten mit einer Zeitstempelspalte abgerufen werden, die größer ist als die aktuelle Zeit (der Zeitpunkt, zu dem die Quelle beginnt zu erfassen).
   * Die Spalte mit dem Zeitstempel sollte wie folgt formatiert sein: `TIMESTAMP_LTZ` oder `TIMESTAMP_NTZ`. Wenn die Zeitstempelspalte auf `TIMESTAMP_NTZ` gesetzt ist, sollte die entsprechende Zeitzone, in der die Werte gespeichert werden, über den Parameter `timezoneValue` übergeben werden. Wenn nicht angegeben, wird für den Wert standardmäßig UTC verwendet.
      * `TIMESTAMP_TZ` kann nicht in einer Zeitstempelspalte oder einer Zuordnung verwendet werden.

## Nächste Schritte

Im folgenden Tutorial erfahren Sie, wie Sie mithilfe der API Ihre [!DNL Snowflake]-Streaming-Quelle mit Experience Platform verbinden:

* [Streamen von Daten aus einer [!DNL Snowflake] Datenbank an die Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Streamen von Daten aus einer [!DNL Snowflake] Datenbank an das Experience Platform mithilfe des Arbeitsbereichs &quot;Quellen&quot;in der Experience Platform-Benutzeroberfläche](../../tutorials/ui/create/databases/snowflake-streaming.md)
