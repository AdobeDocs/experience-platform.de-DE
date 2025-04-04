---
title: Übersicht über den Snowflake Streaming Source Connector
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten von Ihrer Snowflake-Instanz in Adobe Experience Platform aufzunehmen
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 12%

---

# Streaming-Quelle [!DNL Snowflake]

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] Streaming-Quelle ist in der API für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>* Sie können jetzt die [!DNL Snowflake] Streaming-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).


Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt das Streaming von Daten aus einer [!DNL Snowflake].

## Verstehen der [!DNL Snowflake] Streaming-Quelle

Die [!DNL Snowflake]-Streaming-Quelle lädt Daten durch periodisches Ausführen einer SQL-Abfrage und Erstellen eines Ausgabedatensatzes für jede Zeile im resultierenden Satz.

Durch Verwendung von [!DNL Kafka Connect] verfolgt die [!DNL Snowflake]-Streaming-Quelle den neuesten Datensatz, den sie von jeder Tabelle erhält, sodass sie an der richtigen Stelle für die nächste Iteration beginnen kann. Die Quelle verwendet diese Funktion zum Filtern von Daten und ruft bei jeder Iteration nur die aktualisierten Zeilen aus einer Tabelle ab.

## Voraussetzungen

Im folgenden Abschnitt werden die erforderlichen Schritte beschrieben, die ausgeführt werden müssen, bevor Sie Daten aus Ihrer [!DNL Snowflake] an Experience Platform streamen können:

### Zulassungsliste der IP-Adressen aktualisieren

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources).

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Amazon Redshift] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Snowflake] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Die vollständige Kontokennung (Kontoname oder Konto-Locator) Ihres [!DNL Snowflake] Kontos, an die das Suffix `snowflakecomputing.com` angehängt ist. Die Kontokennung kann in verschiedenen Formaten vorliegen: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (z. B. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (z. B. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (z. B. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Weitere Informationen finden Sie im [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |
| `database` | Die [!DNL Snowflake]-Datenbank enthält die Daten, die Sie mit der Experience Platform verknüpfen möchten. |
| `username` | Der Benutzername für das [!DNL Snowflake]. |
| `password` | Das Kennwort für das [!DNL Snowflake] Benutzerkonto. |
| `role` | (Optional) Eine benutzerdefinierte Rolle, die für einen Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn kein Wert angegeben wird, ist dieser Standardwert `public`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Snowflake] ist `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

### Konfigurieren von Rolleneinstellungen {#configure-role-settings}

Sie müssen Berechtigungen für eine Rolle konfigurieren, auch wenn die standardmäßige öffentliche Rolle zugewiesen ist, damit Ihre Quellverbindung auf die entsprechende [!DNL Snowflake]-Datenbank, das Schema und die entsprechende Tabelle zugreifen kann. Die verschiedenen Berechtigungen für verschiedene [!DNL Snowflake]-Entitäten lauten wie folgt:

| Entität [!DNL Snowflake] | Rollenberechtigung verlangen |
| --- | --- |
| Warehouse | BEDIENEN, NUTZUNG |
| Datenbank | GEBRAUCH |
| Schema | GEBRAUCH |
| Tabelle | AUSWÄHLEN |

>[!NOTE]
>
>Die Funktion zum automatischen Fortsetzen und automatischen Aussetzen muss in den erweiterten Einstellungen Ihres Warehouse aktiviert sein.

Weitere Informationen zur Rollen- und Berechtigungsverwaltung finden Sie in der [[!DNL Snowflake] API-Referenz](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Einschränkungen und häufig gestellte Fragen {#limitations-and-frequently-asked-questions}

* Der Datendurchsatz für die [!DNL Snowflake] beträgt 2000 Datensätze pro Sekunde.
* Die Preise variieren je nach der Zeit, die ein Lager aktiv ist, und der Größe des Lagers. Für die [!DNL Snowflake]-Quellintegration genügt ein kleinstes X-kleines Warehouse. Es wird empfohlen, das automatische Aussetzen zu aktivieren, damit das Warehouse bei Nichtverwendung selbstständig aussetzen kann.
* Die [!DNL Snowflake] fragt alle 10 Sekunden die Datenbank nach neuen Daten ab.
* Konfigurationsoptionen:
   * Sie können beim Erstellen einer Quellverbindung ein `backfill` boolesches Flag für Ihre [!DNL Snowflake]-Quelle aktivieren.
      * Wenn die Aufstockung auf „true“ gesetzt ist, wird der Wert für „timestamp.initial“ auf 0 gesetzt. Das bedeutet, dass Daten mit einer Zeitstempelspalte größer als 0 Epochenzeit abgerufen werden.
      * Wenn die Aufstockung auf „false“ festgelegt ist, wird der Wert für „timestamp.initial“ auf -1 festgelegt. Das bedeutet, dass Daten mit einer Zeitstempelspalte abgerufen werden, die größer ist als die aktuelle Zeit (die Zeit, in der die Quelle mit der Aufnahme beginnt).
   * Die Zeitstempelspalte sollte als Typ formatiert sein: `TIMESTAMP_LTZ` oder `TIMESTAMP_NTZ`. Wenn die Zeitstempelspalte auf `TIMESTAMP_NTZ` gesetzt ist, sollte die entsprechende Zeitzone, in der die Werte gespeichert sind, über den `timezoneValue` Parameter weitergeleitet werden. Wenn kein Wert angegeben wird, wird standardmäßig UTC verwendet.
      * `TIMESTAMP_TZ` kann weder in einer Zeitstempelspalte noch in einer Zuordnung verwendet werden.

## Nächste Schritte

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Snowflake]-Streaming-Quelle mithilfe der -API mit Experience Platform verbinden:

* [Streamen von Daten aus einer  [!DNL Snowflake]  an Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Streamen von Daten aus  [!DNL Snowflake]  Datenbank an Experience Platform mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
