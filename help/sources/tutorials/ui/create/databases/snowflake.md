---
title: Erstellen einer Snowflake Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Adobe Experience Platform eine Snowflake-Quellverbindung erstellen.
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
>Die [!DNL Snowflake] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL Snowflake]-Quell-Connectors mithilfe der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Snowflake] zu authentifizieren.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Konto | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Platform einzeln aufgerufen werden. |
| Datenbank | Die [!DNL Snowflake]-Datenbank enthält die Daten, die Sie an Platform übermitteln möchten. |
| Benutzername | Der Benutzername für das [!DNL Snowflake]. |
| Kennwort | Das Kennwort für das [!DNL Snowflake] Benutzerkonto. |
| Rolle | Die in der [!DNL Snowflake]-Sitzung zu verwendende standardmäßige Zugriffssteuerungsrolle. Die Rolle sollte eine vorhandene sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle ist `PUBLIC`. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Schlüsselpaar-Authentifizierung]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann die folgenden Werte angeben, wenn Sie ein Konto für Ihre [!DNL Snowflake] erstellen.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Konto | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Benutzername | Der Benutzername Ihres [!DNL Snowflake]. |
| Privater Schlüssel | Der [!DNL Base64-]kodierte private Schlüssel Ihres [!DNL Snowflake]. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie auch eine Passphrase für den privaten Schlüssel angeben, wenn Sie sich gegen Experience Platform authentifizieren. Weitere Informationen finden Sie im Handbuch unter [Abrufen  [!DNL Snowflake]  privaten ](../../../../connectors/databases/snowflake.md)Schlüssels). |
| Passphrase für privaten Schlüssel | Die Passphrase für den privaten Schlüssel ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht angeben, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| Datenbank | Die [!DNL Snowflake], die die Daten enthält, die auf Experience Platform aufgenommen werden sollen. |
| Warehouse | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Platform einzeln aufgerufen werden. |

Weitere Informationen zu diesen Werten finden Sie [diesem Snowflake-Dokument](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Sie müssen das `PREVENT_UNLOAD_TO_INLINE_URL`-Flag auf `FALSE` setzen, um das Entladen von Daten aus Ihrer [!DNL Snowflake] auf Experience Platform zuzulassen.

## Snowflake-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter [!UICONTROL  Kategorie ] die Option **[!UICONTROL Snowflake]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog mit hervorgehobenen [!DNL Snowflake].](../../../../images/tutorials/create/snowflake/catalog.png)

Die **[!UICONTROL Mit Snowflake verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Snowflake] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Snowflake]-Konto an.

![Die neue Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Authentifizierung mit dem Kontoschlüssel zu verwenden, geben Sie Ihre Verbindungszeichenfolge in das Eingabeformular ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![Die Benutzeroberfläche zur Authentifizierung des Kontoschlüssels.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Schlüsselpaar-Authentifizierung]

Um die Schlüsselpaar-Authentifizierung zu verwenden, geben Sie Werte für Ihr Konto, Ihren Benutzernamen, Ihren privaten Schlüssel, die Passphrase für den privaten Schlüssel, Ihre Datenbank und Ihr Warehouse an und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![Die Authentifizierungsschnittstelle für das Konto-Schlüsselpaar.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

### Vorschau der Beispieldaten überspringen {#skip-preview-of-sample-data}

Während des Datenauswahlschritts kann es bei der Aufnahme großer Datentabellen oder -dateien zu einer Zeitüberschreitung kommen. Sie können die Datenvorschau überspringen, um die Zeitüberschreitung zu umgehen, und Ihr Schema dennoch anzeigen, wenn auch ohne Beispieldaten. Um die Datenvorschau zu überspringen, aktivieren Sie den Umschalter **[!UICONTROL Vorschau von Beispieldaten überspringen]**.

Der Rest des Workflows bleibt unverändert. Der einzige Nachteil besteht darin, dass das Überspringen der Datenvorschau verhindert, dass berechnete und erforderliche Felder während des Zuordnungsschritts automatisch validiert werden. Diese Felder müssen dann während der Zuordnung manuell validiert werden.

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in zu importieren [!DNL Platform]](../../dataflow/databases.md).
