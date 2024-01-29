---
title: Erstellen einer Snowflake-Quellverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie eine Snowflake-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 17%

---

# Erstellen eines Quell-Connectors für [!DNL Snowflake] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Snowflake] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Snowflake] Quell-Connector über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldeinformationen

Sie müssen Werte für die folgenden Berechtigungseigenschaften angeben, um Ihre [!DNL Snowflake] -Quelle.

>[!BEGINTABS]

>[!TAB Kontoschlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Konto | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto eindeutig über verschiedene [!DNL Snowflake] Organisationen. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Informationen zu den Kontonamen finden Sie im Abschnitt [!DNL Snowflake] Dokumentation zu [Kontokennung](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an Platform übermitteln möchten. |
| Benutzername | Der Benutzername für die [!DNL Snowflake] -Konto. |
| Kennwort | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| Rolle | Die standardmäßige Zugriffssteuerungsrolle, die in der [!DNL Snowflake] Sitzung. Die Rolle sollte eine bestehende sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle lautet `PUBLIC`. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, über die die Verbindung zu Ihrem [!DNL Snowflake] -Instanz. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentifizierung mit Schlüsselpaaren]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann beim Erstellen eines Kontos für Ihre [!DNL Snowflake] -Quelle.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Konto | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto eindeutig über verschiedene [!DNL Snowflake] Organisationen. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Informationen zu den Kontonamen finden Sie im Abschnitt [!DNL Snowflake] Dokumentation zu [Kontokennung](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Benutzername | Der Benutzername Ihres [!DNL Snowflake] -Konto. |
| Privater Schlüssel | Die [!DNL Base64-]kodierter privater Schlüssel Ihres [!DNL Snowflake] -Konto. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie bei der Authentifizierung bei Experience Platform auch eine Passphrase für den privaten Schlüssel angeben. |
| Passphrase für privaten Schlüssel | Die Passphrase des privaten Schlüssels ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht bereitstellen, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank, die die Daten enthält, die Sie auf Experience Platform erfassen möchten. |
| Warehouse | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |

Weitere Informationen zu diesen Werten finden Sie unter [dieses Snowflake-Dokument](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Um auf Ihr Snowflake-Konto auf Experience Platform zugreifen zu können, müssen Sie den folgenden Authentifizierungswert angeben:

>[!NOTE]
>
>Sie müssen die `PREVENT_UNLOAD_TO_INLINE_URL` Markierung auf `FALSE` , um das Entladen von Daten aus Ihrem [!DNL Snowflake] Datenbank zu Experience Platform.

## Snowflake-Konto anschließen

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Datenbanken] category, select **[!UICONTROL Snowflake]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit [!DNL Snowflake] hervorgehoben.](../../../../images/tutorials/create/snowflake/catalog.png)

Die **[!UICONTROL Verbindung zu Snowflake herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL Snowflake] Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Nächste]** um fortzufahren.

![Die vorhandene Kontoschnittstelle im Ursprungs-Workflow.](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL Snowflake] -Konto.

![Die neue Kontoschnittstelle im Ursprungs-Workflow.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Kontoschlüsselauthentifizierung]

Um die Authentifizierung des Kontoschlüssels zu verwenden, geben Sie Ihre Verbindungszeichenfolge in das Formular ein und wählen Sie dann **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die Authentifizierungsschnittstelle für den Kontoschlüssel.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Authentifizierung mit Schlüsselpaaren]

Um die Authentifizierung mit Schlüsselpaaren zu verwenden, geben Sie Werte für Ihr Konto, Ihren Benutzernamen, Ihren privaten Schlüssel, Ihre Passphrase mit privatem Schlüssel, Ihre Datenbank und Ihr Warehouse an und wählen Sie dann **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Die Authentifizierungsschnittstelle für Konto-Schlüsselpaare.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md).
