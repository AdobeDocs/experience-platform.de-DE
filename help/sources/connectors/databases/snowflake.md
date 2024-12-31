---
title: Snowflake Source Connector - Übersicht
description: Erfahren Sie, wie Sie Snowflake mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8d6baef1549498e137d336ac2c8a42428496dedf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 21%

---

# [!DNL Snowflake]

>[!IMPORTANT]
>
>* Die [!DNL Snowflake] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.
>* Standardmäßig interpretiert die [!DNL Snowflake]-Quelle `null` als leere Zeichenfolge. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um sicherzustellen, dass Ihre `null` wie in Adobe Experience Platform `null` geschrieben sind.
>* Damit Experience Platform Daten aufnehmen kann, müssen die Zeitzonen für alle tabellenbasierten Batch-Quellen auf UTC konfiguriert werden. Der einzige Zeitstempel, der für die [!DNL Snowflake]-Quelle unterstützt wird, ist TIMESTAMP_NTZ mit UTC-Zeit.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Datenbanktypen herstellen, z. B. relationale Datenbanken, NoSQL oder Data Warehouses. Die Unterstützung für Datenbankanbieter umfasst [!DNL Snowflake].

## Voraussetzungen {#prerequisites}

In diesem Abschnitt werden die Einrichtungsaufgaben beschrieben, die Sie durchführen müssen, bevor Sie Ihre [!DNL Snowflake] mit Experience Platform verbinden können.

### Kontokennung abrufen {#retrieve-your-account-identifier}

Sie müssen Ihre Kontokennung vom Dashboard der [!DNL Snowflake]-Benutzeroberfläche abrufen, da Sie die Kontokennung zur Authentifizierung Ihrer [!DNL Snowflake]-Instanz auf dem Experience Platform verwenden werden.

So rufen Sie Ihre Kontokennung ab:

* Navigieren Sie im Dashboard der [[!DNL Snowflake] -Benutzeroberfläche zu Ihrem ](https://app.snowflake.com/).
* Wählen Sie in der linken Navigationsleiste **[!DNL Accounts]** und dann **[!DNL Active Accounts]** aus der Kopfzeile aus.
* Klicken Sie anschließend auf das Informationssymbol und wählen Sie den Domain-Namen der aktuellen URL aus und kopieren Sie ihn.

![Das Dashboard der Snowflake-Benutzeroberfläche mit dem ausgewählten Domain-Namen.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Privaten Schlüssel abrufen {#retrieve-your-private-key}

Wenn Sie die Schlüsselpaar-Authentifizierung für Ihre [!DNL Snowflake]-Verbindung verwenden, müssen Sie auch Ihren privaten Schlüssel generieren, bevor Sie eine Verbindung zu Experience Platform herstellen.

>[!BEGINTABS]

>[!TAB Erstellen eines verschlüsselten privaten Schlüssels]

Um Ihren verschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Bei Erfolg sollten Sie Ihren privaten Schlüssel im PEM-Format erhalten.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Erstellen eines unverschlüsselten privaten Schlüssels]

Um Ihren unverschlüsselten [!DNL Snowflake] privaten Schlüssel zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Bei Erfolg sollten Sie Ihren privaten Schlüssel im PEM-Format erhalten.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Nehmen Sie als Nächstes Ihren privaten Schlüssel und kodieren Sie ihn in [!DNL Base64]. Stellen Sie sicher, dass Sie auf Ihrem [!DNL Snowflake] privaten Schlüssel keine Umwandlungen oder Formatkonvertierungen vornehmen. Darüber hinaus müssen Sie sicherstellen, dass am Ende des privaten Schlüssels keine nachfolgenden Zeilenumbruchzeichen vorhanden sind, bevor Sie ihn in [!DNL Base64] kodieren.

### Überprüfen von Konfigurationen

Bevor Sie eine Quellverbindung für Ihre [!DNL Snowflake] erstellen können, müssen Sie auch sicherstellen, dass die folgenden Konfigurationen erfüllt sind:

* Das einem Benutzer zugewiesene Standard-Warehouse muss dem Warehouse entsprechen, das Sie bei der Authentifizierung auf Experience Platform eingegeben haben.
* Die einem Benutzer zugewiesene Standardrolle muss Zugriff auf dieselbe Datenbank haben, die Sie bei der Authentifizierung auf Experience Platform eingegeben haben.

So überprüfen Sie Ihre Rolle und Ihr Warehouse:

* Wählen Sie in der linken Navigationsleiste **[!DNL Admin]** und dann **[!DNL Users & Roles]** aus.
* Wählen Sie den entsprechenden Benutzer aus und klicken Sie dann oben rechts auf die Auslassungspunkte (`...`).
* Navigieren Sie im sich öffnenden [!DNL Edit user] zu [!DNL Default Role], um die Rolle anzuzeigen, die dem jeweiligen Benutzer zugeordnet ist.
* Navigieren Sie im selben Fenster zu [!DNL Default Warehouse] , um das mit dem jeweiligen Benutzer verknüpfte Warehouse anzuzeigen.

![Die Snowflake-Benutzeroberfläche, in der Sie Ihre Rolle und Ihr Warehouse überprüfen können.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Nach erfolgreicher Kodierung können Sie diesen [!DNL Base64] privaten Schlüssel auf dem Experience Platform zur Authentifizierung Ihres [!DNL Snowflake]-Kontos verwenden.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Snowflake] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Snowflake] mit Platform mithilfe von APIs

* [Erstellen einer Snowflake-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Snowflake] mit Platform über die Benutzeroberfläche

* [Erstellen einer Snowflake-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/snowflake.md)
* [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
