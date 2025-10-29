---
title: Übersicht über den Snowflake Streaming Source Connector
description: Erfahren Sie, wie Sie eine Quellverbindung und einen Datenfluss erstellen, um Streaming-Daten von Ihrer Snowflake-Instanz in Adobe Experience Platform aufzunehmen
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 6%

---

# Streaming-Quelle [!DNL Snowflake]

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] Streaming-Quelle ist in der API für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>* Sie können jetzt die [!DNL Snowflake] Streaming-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt das Streaming von Daten aus einer [!DNL Snowflake].

## Verstehen der [!DNL Snowflake] Streaming-Quelle

Die [!DNL Snowflake]-Streaming-Quelle lädt Daten durch periodisches Ausführen einer SQL-Abfrage und Erstellen eines Ausgabedatensatzes für jede Zeile im resultierenden Satz.

Durch Verwendung von [!DNL Kafka Connect] verfolgt die [!DNL Snowflake]-Streaming-Quelle den neuesten Datensatz, den sie von jeder Tabelle erhält, sodass sie an der richtigen Stelle für die nächste Iteration beginnen kann. Die Quelle verwendet diese Funktion zum Filtern von Daten und ruft bei jeder Iteration nur die aktualisierten Zeilen aus einer Tabelle ab.

## Voraussetzungen

Im folgenden Abschnitt werden die erforderlichen Schritte beschrieben, die ausgeführt werden müssen, bevor Sie Daten aus Ihrer [!DNL Snowflake] an Experience Platform streamen können:

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Amazon Redshift] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Snowflake] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Die vollständige Kontokennung (Kontoname oder Konto-Locator) Ihres [!DNL Snowflake] Kontos, an die das Suffix `snowflakecomputing.com` angehängt ist. Die Kontokennung kann in verschiedenen Formaten vorliegen: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (z. B. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (z. B. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (z. B. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Weitere Informationen finden Sie im [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |
| `database` | Die [!DNL Snowflake]-Datenbank enthält die Daten, die Sie mit der Experience Platform verknüpfen möchten. |
| `username` | Der Benutzername für das [!DNL Snowflake]. |
| `password` | Das Kennwort für das [!DNL Snowflake] Benutzerkonto. |
| `role` | (Optional) Eine benutzerdefinierte Rolle, die für einen Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn kein Wert angegeben wird, ist dieser Standardwert `public`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Snowflake] ist `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Schlüsselpaar-Authentifizierung]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann die folgenden Werte angeben, wenn Sie ein Konto für Ihre [!DNL Snowflake] erstellen.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](./snowflake.md#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Der Benutzername Ihres [!DNL Snowflake]. |
| `privateKey` | Der [!DNL Base64-]kodierte private Schlüssel Ihres [!DNL Snowflake]. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie auch eine Passphrase für den privaten Schlüssel angeben, wenn Sie sich bei Experience Platform authentifizieren. Weitere Informationen finden Sie im Handbuch unter [Abrufen  [!DNL Snowflake]  privaten ](./snowflake.md)Schlüssels). |
| `passphrase` | Die Passphrase ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht angeben, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| `database` | Die [!DNL Snowflake], die die Daten enthält, die in Experience Platform aufgenommen werden sollen. |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |

Weitere Informationen zu diesen Werten finden Sie im [[!DNL Snowflake] Handbuch zur Schlüsselpaar-Authentifizierung](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Kontokennung abrufen {#retrieve-your-account-identifier}

Um Ihre [!DNL Snowflake]-Instanz bei Experience Platform zu authentifizieren, müssen Sie Ihre Kontokennung über das Dashboard der [!DNL Snowflake]-Benutzeroberfläche abrufen.

Gehen Sie wie folgt vor, um Ihre Kontokennung zu finden:

* Navigieren Sie im Dashboard der [[!DNL Snowflake] -Benutzeroberfläche zu Ihrem ](https://app.snowflake.com/).
* Wählen Sie in der linken Navigationsleiste **[!DNL Accounts]** und dann **[!DNL Active Accounts]** aus der Kopfzeile aus.
* Klicken Sie anschließend auf das Informationssymbol und wählen Sie den Domain-Namen der aktuellen URL aus und kopieren Sie ihn.

### Privaten Schlüssel abrufen {#retrieve-your-private-key}

Wenn Sie die Schlüsselpaar-Authentifizierung für Ihre [!DNL Snowflake]-Verbindung verwenden möchten, müssen Sie einen privaten Schlüssel generieren, bevor Sie eine Verbindung mit Experience Platform herstellen.

>[!BEGINTABS]

>[!TAB Erstellen eines verschlüsselten privaten Schlüssels]

Um Ihren verschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Bei Erfolg sollten Sie Ihren privaten Schlüssel im PEM-Format erhalten.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Erstellen eines unverschlüsselten privaten Schlüssels]

Um Ihren unverschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Bei Erfolg sollten Sie Ihren privaten Schlüssel im PEM-Format erhalten.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

Nachdem Sie den privaten Schlüssel generiert haben, kodieren Sie ihn direkt in [!DNL Base64], ohne Änderungen an seinem Format oder Inhalt vorzunehmen. Stellen Sie vor der Kodierung sicher, dass am Ende des privaten Schlüssels keine zusätzlichen Leerzeichen oder Leerzeilen (einschließlich nachfolgender Zeilenumbrüche) vorhanden sind.

### Überprüfen von Konfigurationen

Bevor Sie eine Quellverbindung für Ihre [!DNL Snowflake] erstellen können, müssen Sie auch sicherstellen, dass die folgenden Konfigurationen erfüllt sind:

* Das einem bestimmten Benutzer zugewiesene Standard-Warehouse muss mit dem Warehouse identisch sein, das Sie bei der Authentifizierung bei Experience Platform eingegeben haben.
* Die Standardrolle, die einem bestimmten Benutzer zugewiesen ist, muss Zugriff auf dieselbe Datenbank haben, die Sie bei der Authentifizierung bei Experience Platform eingegeben haben.

So überprüfen Sie Ihre Rolle und Ihr Warehouse:

* Wählen Sie in der linken Navigationsleiste **[!DNL Admin]** und dann **[!DNL Users & Roles]** aus.
* Wählen Sie den entsprechenden Benutzer aus und klicken Sie dann oben rechts auf die Auslassungspunkte (`...`).
* Navigieren Sie im sich öffnenden [!DNL Edit user] zu [!DNL Default Role], um die Rolle anzuzeigen, die dem jeweiligen Benutzer zugeordnet ist.
* Navigieren Sie im selben Fenster zu [!DNL Default Warehouse] , um das mit dem jeweiligen Benutzer verknüpfte Warehouse anzuzeigen.

Nach erfolgreicher Kodierung können Sie diesen [!DNL Base64] privaten Schlüssel auf Experience Platform zur Authentifizierung Ihres [!DNL Snowflake]-Kontos verwenden.

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

## Unix-Zeit in Datumsfelder konvertieren

Die [!DNL Snowflake Streaming] analysiert und schreibt ` DATE` Felder als die Anzahl der Tage seit der Unix-Epoche (1970-01-01). Beispiel: Ein `DATE` von 0 bedeutet den 1. Januar 1970, während ein Wert von 1 den 2. Januar 1970 bedeutet. Stellen Sie daher beim Vorbereiten der Datei zum Erstellen von Zuordnungen in der [!DNL Snowflake Streaming] sicher, dass die `DATE` Spalte als Ganzzahl dargestellt wird.

Sie können [Datenvorbereitungs- und Zeitfunktionen](../../../data-prep/functions.md#date-and-time-functions) verwenden, um Unix-Zeit in Datumsfelder zu konvertieren, die in Experience Platform aufgenommen werden können. Beispiel:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

In dieser Funktion:

* `{DATE_COLUMN}` ist die Datumsspalte, die die Ganzzahl für den Epochentag enthält.
* Durch Multiplizieren mit 86400000 werden die Epochentage in Millisekunden umgewandelt.
* &#39;JJJJ-MM-TT&#39; gibt das gewünschte Datumsformat an.

Diese Konvertierung stellt sicher, dass das Datum in Ihrem Datensatz korrekt dargestellt wird.


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

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Snowflake]-Streaming-Quelle mithilfe der -API mit Experience Platform verbinden:

* [Streamen von Daten aus einer  [!DNL Snowflake]  an Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Streamen von Daten aus  [!DNL Snowflake]  Datenbank an Experience Platform mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
