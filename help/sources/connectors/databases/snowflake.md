---
title: Übersicht über den Snowflake Source Connector
description: Erfahren Sie, wie Sie Snowflake mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# [!DNL Snowflake]

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.
>* Standardmäßig interpretiert die [!DNL Snowflake]-Quelle `null` als leere Zeichenfolge. Wenden Sie sich an den Adobe-Support-Mitarbeiter, um sicherzustellen, dass Ihre `null` wie `null` in Adobe Experience Platform geschrieben sind.
>* Damit Experience Platform Daten aufnehmen kann, müssen die Zeitzonen für alle tabellenbasierten Batch-Quellen als UTC konfiguriert werden. Der einzige Zeitstempel, der für die [!DNL Snowflake]-Quelle unterstützt wird, ist TIMESTAMP_NTZ mit UTC-Zeit.

[!DNL Snowflake] ist eine Cloud-basierte Data Warehouse-Plattform, mit der Unternehmen große Datenmengen effizient speichern, verarbeiten und analysieren können. Entwickelt für die Nutzung der Skalierbarkeit und Flexibilität der Cloud, unterstützt [!DNL Snowflake] die Datenintegration, erweiterte Analysen und die nahtlose gemeinsame Nutzung durch Teams. Als vollständig verwalteter Service eliminiert [!DNL Snowflake] komplexe Wartungsaufgaben, die mit herkömmlichen Datenbanken verbunden sind, und ermöglicht es Ihnen, sich auf die Ermittlung von Insights und Nutzen aus Ihren Daten zu konzentrieren.

Sie können die [!DNL Snowflake] verwenden, um eine Verbindung herzustellen und Ihre Daten von [!DNL Snowflake] in Adobe Experience Platform einzubringen. Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie Ihre [!DNL Snowflake] einrichten und eine Verbindung zu Experience Platform herstellen.

## Voraussetzungen {#prerequisites}

In diesem Abschnitt werden die Einrichtungsaufgaben beschrieben, die Sie ausführen müssen, bevor Sie Ihre [!DNL Snowflake] mit Experience Platform verbinden können.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Snowflake] zu authentifizieren.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel (Azure)]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um [!DNL Snowflake] mithilfe der Kontoschlüsselauthentifizierung mit Experience Platform auf Azure zu verbinden.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `myorg-myaccount.snowflakecomputing.com`. Weitere Anleitungen finden Sie im Abschnitt [Abrufen  [!DNL Snowflake]  Kontokennung](#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |
| `database` | Die [!DNL Snowflake]-Datenbank enthält die Daten, die Sie mit der Experience Platform verknüpfen möchten. |
| `username` | Der Benutzername für das [!DNL Snowflake]. |
| `password` | Das Kennwort für das [!DNL Snowflake] Benutzerkonto. |
| `role` | Die in der [!DNL Snowflake]-Sitzung zu verwendende standardmäßige Zugriffssteuerungsrolle. Die Rolle sollte eine vorhandene sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle ist `PUBLIC`. |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Schlüsselpaar-Authentifizierung (Azure)]

Um die Schlüsselpaar-Authentifizierung zu verwenden, generieren Sie zunächst ein 2048-Bit-RSA-Schlüsselpaar. Geben Sie als Nächstes Werte für die folgenden Anmeldeinformationen an, um mithilfe der Schlüsselpaar-Authentifizierung eine Verbindung zu Experience Platform auf Azure herzustellen.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `myorg-myaccount.snowflakecomputing.com`. Weitere Anleitungen finden Sie im Abschnitt [Abrufen  [!DNL Snowflake]  Kontokennung](#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Der Benutzername Ihres [!DNL Snowflake]. |
| `privateKey` | Der [!DNL Base64-]kodierte private Schlüssel Ihres [!DNL Snowflake]. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie auch eine Passphrase für den privaten Schlüssel angeben, wenn Sie sich bei Experience Platform authentifizieren. Weitere Informationen finden Sie im Abschnitt [Abrufen Ihres privaten ](#retrieve-your-private-key)&quot;. |
| `privateKeyPassphrase` | Die Passphrase für den privaten Schlüssel ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht angeben, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| `port` | Die Port-Nummer, die von [!DNL Snowflake] verwendet wird, wenn eine Verbindung zu einem Server über das Internet hergestellt wird. |
| `database` | Die [!DNL Snowflake], die die Daten enthält, die in Experience Platform aufgenommen werden sollen. |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |

Weitere Informationen zu diesen Werten finden Sie im [[!DNL Snowflake] Handbuch zur Schlüsselpaar-Authentifizierung](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Einfache Authentifizierung (AWS)]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um [!DNL Snowflake] unter Verwendung der Standardauthentifizierung mit Experience Platform auf AWS zu verbinden.

>[!WARNING]
>
>Die Standardauthentifizierung (oder Kontoschlüsselauthentifizierung) für die [!DNL Snowflake] wird ab November 2025 eingestellt. Sie müssen zur schlüsselpaarbasierten Authentifizierung wechseln, um weiterhin die -Quelle verwenden und Daten aus Ihrer -Datenbank in Experience Platform aufnehmen zu können. Weitere Informationen zur Einstellung finden Sie im [[!DNL Snowflake] Handbuch mit Best Practices zum Minimieren der Risiken durch das Kompromittieren von Anmeldeinformationen](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Anmeldedaten | Beschreibung |
| --- | --- |
| `host` | Die Host-URL, mit der sich Ihr [!DNL Snowflake]-Konto verbindet. |
| `port` | Die Port-Nummer, die von [!DNL Snowflake] verwendet wird, wenn eine Verbindung zu einem Server über das Internet hergestellt wird. |
| `username` | Der Benutzername, der Ihrem [!DNL Snowflake]-Konto zugeordnet ist. |
| `password` | Das mit Ihrem [!DNL Snowflake]-Konto verknüpfte Kennwort. |
| `database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `schema` | Der Name des Schemas, das Ihrer [!DNL Snowflake]-Datenbank zugeordnet ist. Sie müssen sicherstellen, dass der Benutzer, dem Sie Datenbankzugriff gewähren möchten, auch Zugriff auf dieses Schema hat. |
| `warehouse` | Das [!DNL Snowflake] Warehouse, das Sie verwenden. |

>[!TAB Schlüsselpaar-Authentifizierung (AWS)]

Um die Schlüsselpaar-Authentifizierung zu verwenden, generieren Sie zunächst ein 2048-Bit-RSA-Schlüsselpaar. Geben Sie als Nächstes Werte für die folgenden Anmeldeinformationen an, um mithilfe der Schlüsselpaar-Authentifizierung eine Verbindung zu Experience Platform auf AWS herzustellen.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `http://myorg-myaccount.snowflakecomputing.com/`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](#etrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Der Benutzername Ihres [!DNL Snowflake]. |
| `privateKey` | Der private Schlüssel für Ihren [!DNL Snowflake]-Benutzer, base64-kodiert als einzelne Zeile ohne Kopfzeilen oder Zeilenumbrüche. Zur Vorbereitung kopieren Sie den Inhalt Ihrer PEM-Datei, entfernen Sie die `BEGIN`/`END` Zeilen und alle Zeilenumbrüche, und kodieren Sie dann das Ergebnis mit base64. Weitere Informationen finden Sie im Abschnitt [Abrufen Ihres privaten ](#retrieve-your-private-key)&quot;. **Hinweis:** Verschlüsselte private Schlüssel werden derzeit für eine AWS-Verbindung nicht unterstützt. |
| `port` | Die Port-Nummer, die von [!DNL Snowflake] verwendet wird, wenn eine Verbindung zu einem Server über das Internet hergestellt wird. |
| `database` | Die [!DNL Snowflake], die die Daten enthält, die in Experience Platform aufgenommen werden sollen. |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |

Weitere Informationen zu diesen Werten finden Sie im [[!DNL Snowflake] Handbuch zur Schlüsselpaar-Authentifizierung](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Kontokennung abrufen {#retrieve-your-account-identifier}

Sie müssen Ihre Kontokennung vom Dashboard der [!DNL Snowflake]-Benutzeroberfläche abrufen, da Sie sie zur Authentifizierung Ihrer [!DNL Snowflake] auf Experience Platform verwenden werden.

So rufen Sie Ihre Kontokennung ab:

* Verwenden Sie das [[!DNL Snowflake] Anwendungs-UI-Dashboard](https://app.snowflake.com/), um auf Ihr Konto zuzugreifen.
* Wählen Sie in der linken Navigation **[!DNL Accounts]** und anschließend **[!DNL Active Accounts]** aus der Kopfzeile aus.
* Klicken Sie anschließend auf das Informationssymbol und wählen Sie den Domain-Namen der aktuellen URL aus und kopieren Sie ihn.

![Das Dashboard der Snowflake-Benutzeroberfläche mit dem ausgewählten Domain-Namen.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Erzeugen des RSA-Schlüsselpaars

Verwenden Sie OpenSSL in der Befehlszeilenschnittstelle, um ein 2048-Bit-RSA-Schlüsselpaar im PKCS#8-Format zu generieren. Es empfiehlt sich, einen verschlüsselten privaten Schlüssel für die Sicherheit zu erstellen, wofür eine Passphrase erforderlich ist.

>[!BEGINTABS]

>[!TAB Generieren eines verschlüsselten privaten Schlüssels]

Um Ihren verschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Generieren eines unverschlüsselten privaten Schlüssels]

Um Ihren unverschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Generieren eines öffentlichen Schlüssels aus Ihrem privaten Schlüssel

Führen Sie als Nächstes den folgenden Befehl in Ihrer Befehlszeilenschnittstelle aus, um einen öffentlichen Schlüssel basierend auf Ihrem privaten Schlüssel zu erstellen.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Weisen Sie den öffentlichen Schlüssel dem [!DNL Snowflake] Benutzer zu

Sie müssen eine [!DNL Snowflake] Administratorrolle verwenden (z. B **SECURITYADMIN**), um den generierten öffentlichen Schlüssel mit dem [!DNL Snowflake] Service-Benutzer zu verknüpfen, den Experience Platform verwenden wird. Um den Inhalt des öffentlichen Schlüssels abzurufen, öffnen Sie die `rsa_key.pub` und kopieren Sie den gesamten Inhalt mit Ausnahme der `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`. Führen Sie als Nächstes die folgende SQL in [!DNL Snowflake] aus:

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Codieren des privaten Schlüssels in [!DNL Base64]

Experience Platform erfordert, dass der private Schlüssel [!DNL Base64] codiert ist und bei der Einrichtung der Verbindung als Zeichenfolge bereitgestellt wird. Verwenden Sie ein geeignetes Tool oder Skript, um den Inhalt der `rsa_key.p8`-Datei in eine einzelne [!DNL Base64]-Zeichenfolge zu kodieren.

>[!TIP]
>
>Stellen Sie sicher, dass vor oder nach dem Kodierungsprozess keine zusätzlichen Leerzeichen oder Zeilenumbrüche vorhanden sind, einschließlich der `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)` Kopf-/Fußzeilen, da dies zu Authentifizierungsfehlern führen kann.

### Überprüfen von Konfigurationen

Bevor Sie die [!DNL Snowflake]-Quellverbindung in Experience Platform erstellen, müssen Sie sicherstellen, dass die **[!DNL Default Role]** und **[!DNL Default Warehouse]** der Benutzenden mit den Werten übereinstimmen, die Sie in Experience Platform angeben. Sie können diese Einstellungen in der [!DNL Snowflake]-Benutzeroberfläche mit dem `DESCRIBE USER {USERNAME}` SQL-Befehl überprüfen.

Alternativ können Sie die folgenden Schritte ausführen, um Ihre Einstellungen zu überprüfen:

* Wählen Sie in der linken Navigationsleiste **[!DNL Admin]** und dann **[!DNL Users & Roles]** aus.
* Wählen Sie den entsprechenden Benutzer aus und klicken Sie dann oben rechts auf die Auslassungspunkte (`...`).
* Navigieren Sie im sich öffnenden [!DNL Edit user] zu [!DNL Default Role], um die Rolle anzuzeigen, die dem jeweiligen Benutzer zugeordnet ist.
* Navigieren Sie im selben Fenster zu [!DNL Default Warehouse] , um das mit dem jeweiligen Benutzer verknüpfte Warehouse anzuzeigen.

![Die Snowflake-Benutzeroberfläche, in der Sie Ihre Rolle und Ihr Warehouse überprüfen können.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Nächste Schritte

Nachdem Sie die Einrichtung abgeschlossen haben, können Sie nun mit dem Verbinden Ihres [!DNL Snowflake]-Kontos mit Experience Platform fortfahren. Weitere Informationen finden Sie in der folgenden Dokumentation:

### Verbinden von [!DNL Snowflake] mit Experience Platform mithilfe von APIs

* [Verbindung  [!DNL Snowflake]  Experience Platform über die API herstellen](../../tutorials/api/create/databases/snowflake.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verbinden von [!DNL Snowflake] mit Experience Platform über die Benutzeroberfläche

* [Verbindung  [!DNL Snowflake]  Experience Platform über die Benutzeroberfläche herstellen](../../tutorials/ui/create/databases/snowflake.md)
* [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
