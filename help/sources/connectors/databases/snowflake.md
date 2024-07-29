---
title: Snowflake Source Connector - Übersicht
description: Erfahren Sie, wie Sie Snowflake über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8d6baef1549498e137d336ac2c8a42428496dedf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 21%

---

# [!DNL Snowflake] source

>[!IMPORTANT]
>
>* Die Quelle &quot;[!DNL Snowflake]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.
>* Standardmäßig interpretiert die Quelle [!DNL Snowflake] `null` als eine leere Zeichenfolge. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um sicherzustellen, dass Ihre `null` -Werte in Adobe Experience Platform korrekt als `null` geschrieben sind.
>* Damit Experience Platform Daten erfassen kann, müssen Zeitzonen für alle tabellenbasierten Batch-Quellen auf UTC konfiguriert werden. Der einzige Zeitstempel, der für die [!DNL Snowflake]-Quelle unterstützt wird, ist TIMESTAMP_NTZ mit UTC-Zeit.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter ist [!DNL Snowflake].

## Voraussetzungen {#prerequisites}

In diesem Abschnitt werden die Einrichtungsaufgaben beschrieben, die Sie ausführen müssen, bevor Sie Ihre [!DNL Snowflake]-Quelle mit Experience Platform verbinden können.

### Konto-ID abrufen {#retrieve-your-account-identifier}

Sie müssen Ihre Kontokennung vom Dashboard der Benutzeroberfläche [!DNL Snowflake] abrufen, da Sie die Kontokennung verwenden, um Ihre [!DNL Snowflake] -Instanz auf dem Experience Platform zu authentifizieren.

So rufen Sie Ihre Kontokennung ab:

* Navigieren Sie zu Ihrem Konto im Dashboard für die Benutzeroberfläche von [[!DNL Snowflake] Anwendungen](https://app.snowflake.com/).
* Wählen Sie im linken Navigationsbereich **[!DNL Accounts]**, gefolgt von **[!DNL Active Accounts]** aus der Kopfzeile.
* Wählen Sie als Nächstes das Informationssymbol aus und wählen Sie dann den Domänennamen der aktuellen URL aus und kopieren Sie ihn.

![Das Dashboard der Snowflake-Benutzeroberfläche mit dem ausgewählten Domänennamen.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Privaten Schlüssel abrufen {#retrieve-your-private-key}

Wenn Sie die Schlüsselpaar-Authentifizierung für Ihre [!DNL Snowflake]-Verbindung verwenden, müssen Sie auch Ihren privaten Schlüssel generieren, bevor Sie eine Verbindung zu Experience Platform herstellen.

>[!BEGINTABS]

>[!TAB Erstellen eines verschlüsselten privaten Schlüssels]

Um Ihren verschlüsselten privaten Schlüssel [!DNL Snowflake] zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

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

Um Ihren unverschlüsselten privaten Schlüssel [!DNL Snowflake] zu generieren, führen Sie den folgenden Befehl auf Ihrem Terminal aus:

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

Als Nächstes nehmen Sie Ihren privaten Schlüssel und kodieren ihn in [!DNL Base64]. Vergewissern Sie sich, dass Sie keine Transformationen oder Formatkonvertierungen an Ihrem privaten Schlüssel [!DNL Snowflake] vornehmen. Außerdem müssen Sie sicherstellen, dass am Ende Ihres privaten Schlüssels keine Zeilenumbruchzeichen folgen, bevor Sie ihn in [!DNL Base64] kodieren.

### Konfigurationen überprüfen

Bevor Sie eine Quellverbindung für Ihre [!DNL Snowflake] -Daten erstellen können, müssen Sie außerdem sicherstellen, dass die folgenden Konfigurationen erfüllt sind:

* Das einem bestimmten Benutzer zugewiesene Standard-Warehouse muss mit dem Warehouse übereinstimmen, das Sie bei der Authentifizierung bei Experience Platform eingeben.
* Die einem bestimmten Benutzer zugewiesene Standardrolle muss Zugriff auf dieselbe Datenbank haben, die Sie bei der Authentifizierung bei Experience Platform eingeben.

So überprüfen Sie Ihre Rolle und Ihr Warehouse:

* Wählen Sie im linken Navigationsbereich **[!DNL Admin]** und dann **[!DNL Users & Roles]** aus.
* Wählen Sie den entsprechenden Benutzer aus und wählen Sie dann oben rechts die Auslassungspunkte (`...`) aus.
* Navigieren Sie im angezeigten Fenster [!DNL Edit user] zu [!DNL Default Role] , um die dem jeweiligen Benutzer zugeordnete Rolle anzuzeigen.
* Navigieren Sie im selben Fenster zu &quot;[!DNL Default Warehouse]&quot;, um das dem jeweiligen Benutzer zugeordnete Warehouse anzuzeigen.

![Die Snowflake-Benutzeroberfläche, in der Sie Ihre Rolle und Ihr Warehouse überprüfen können.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Nach erfolgreicher Codierung können Sie diesen [!DNL Base64]-kodierten privaten Schlüssel auf dem Experience Platform zur Authentifizierung Ihres [!DNL Snowflake]-Kontos verwenden.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Snowflake] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Snowflake] mit Platform mithilfe von APIs

* [Erstellen einer Snowflake-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/snowflake.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Snowflake] mit Platform über die Benutzeroberfläche

* [Erstellen einer Snowflake-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/snowflake.md)
* [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
