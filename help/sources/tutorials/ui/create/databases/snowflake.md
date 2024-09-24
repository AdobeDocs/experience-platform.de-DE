---
title: Erstellen einer Snowflake Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie eine Snowflake-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 16%

---

# Erstellen eines Quell-Connectors für [!DNL Snowflake] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Snowflake]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für [!DNL Snowflake] mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die folgenden Berechtigungseigenschaften angeben, um Ihre [!DNL Snowflake] -Quelle zu authentifizieren.

>[!BEGINTABS]

>[!TAB Authentifizierung des Kontoschlüssels]

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Konto | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto für verschiedene [!DNL Snowflake] -Organisationen eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Lesen Sie das Handbuch zum Abrufen der [!DNL Snowflake] Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) von [für weitere Hinweise. Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | Das [!DNL Snowflake]-Warehouse verwaltet den Abfrageausführungsprozess für die Anwendung. Jedes [!DNL Snowflake]-Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an die Plattform übermitteln möchten. |
| Benutzername | Der Benutzername für das [!DNL Snowflake]-Konto. |
| Kennwort | Das Kennwort für das [!DNL Snowflake] -Benutzerkonto. |
| Rolle | Die standardmäßige Zugriffssteuerungsrolle, die in der [!DNL Snowflake] -Sitzung verwendet werden soll. Die Rolle sollte eine bestehende sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle ist `PUBLIC`. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentifizierung mit Schlüsselpaaren]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann beim Erstellen eines Kontos für Ihre [!DNL Snowflake]-Quelle die folgenden Werte angeben.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Konto | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto für verschiedene [!DNL Snowflake] -Organisationen eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Lesen Sie das Handbuch zum Abrufen der [!DNL Snowflake] Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) von [für weitere Hinweise. Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Benutzername | Der Benutzername Ihres [!DNL Snowflake]-Kontos. |
| Privater Schlüssel | Der [!DNL Base64-]kodierte private Schlüssel Ihres [!DNL Snowflake]-Kontos. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie bei der Authentifizierung bei Experience Platform auch eine Passphrase für den privaten Schlüssel angeben. Weitere Informationen finden Sie im Handbuch zum Abrufen des  [!DNL Snowflake] privaten Schlüssels](../../../../connectors/databases/snowflake.md) von [. |
| Passphrase für privaten Schlüssel | Die Passphrase des privaten Schlüssels ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht bereitstellen, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank, die die Daten enthält, die Sie auf Experience Platform erfassen möchten. |
| Warehouse | Das [!DNL Snowflake]-Warehouse verwaltet den Abfrageausführungsprozess für die Anwendung. Jedes [!DNL Snowflake]-Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Snowflake-Dokument](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Sie müssen die `PREVENT_UNLOAD_TO_INLINE_URL` -Markierung auf `FALSE` setzen, damit das Entladen von Daten aus Ihrer [!DNL Snowflake]-Datenbank auf Experience Platform zugelassen wird.

## Snowflake-Konto anschließen

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Datenbanken] die Option **[!UICONTROL Snowflake]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog mit [!DNL Snowflake] hervorgehoben.](../../../../images/tutorials/create/snowflake/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Snowflake]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Snowflake]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![Die vorhandene Kontoschnittstelle im Quellen-Workflow.](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Snowflake]-Konto ein.

![Die neue Kontoschnittstelle im Ursprungs-Workflow.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Authentifizierung des Kontoschlüssels]

Um die Authentifizierung des Kontoschlüssels zu verwenden, geben Sie Ihre Verbindungszeichenfolge im Formular ein und wählen Sie dann **[!UICONTROL Verbindung zur Quelle herstellen]** aus.

![ Die Authentifizierungsschnittstelle für den Kontoschlüssel.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Authentifizierung mit Schlüsselpaaren]

Um die Schlüsselpaar-Authentifizierung zu verwenden, geben Sie Werte für Ihr Konto, Ihren Benutzernamen, Ihren privaten Schlüssel, die Passphrase des privaten Schlüssels, Ihre Datenbank und Ihr Warehouse an und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus.

![Die Authentifizierungsschnittstelle für Kontoschlüssel-Paare.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

### Vorschau der Beispieldaten überspringen {#skip-preview-of-sample-data}

Während des Datenauswahlschritts kann es bei der Aufnahme großer Tabellen oder Datendateien zu einer Zeitüberschreitung kommen. Sie können die Datenvorschau überspringen, um die Zeitüberschreitung zu umgehen und Ihr Schema weiterhin anzuzeigen, wenn auch ohne Beispieldaten. Um die Datenvorschau zu überspringen, aktivieren Sie den Umschalter **[!UICONTROL Vorschau der Beispieldaten überspringen]** .

Der Rest des Workflows bleibt unverändert. Der einzige Nachteil besteht darin, dass das Überspringen der Datenvorschau verhindern kann, dass berechnete und erforderliche Felder während des Zuordnungsschritts automatisch validiert werden. Anschließend müssen Sie diese Felder während der Zuordnung manuell validieren.

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Daten in  [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
