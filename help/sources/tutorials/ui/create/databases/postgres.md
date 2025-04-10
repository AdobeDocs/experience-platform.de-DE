---
title: Verbinden von PostgreSQL mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre PostgreSQL-Datenbank mithilfe des Quellarbeitsbereichs in der Benutzeroberfläche von Experience Platform mit Experience Platform verbinden.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: 8cabf1cb86993fdde37d0b9d957f6c8ec23bb237
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 18%

---

# Verbinden von [!DNL PostgreSQL] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL PostgreSQL]-Datenbank mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL PostgreSQL]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Weitere Informationen zur Authentifizierung [[!DNL PostgreSQL]  Sie ](../../../../connectors/databases/postgres.md) „Übersicht“.

### Aktivieren der SSL-Verschlüsselung für die Verbindungszeichenfolge

Sie können die SSL-Verschlüsselung für Ihre [!DNL PostgreSQL] Verbindungszeichenfolge aktivieren, indem Sie Ihre Verbindungszeichenfolge mit den folgenden Eigenschaften anhängen:

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `EncryptionMethod` | Ermöglicht die Aktivierung der SSL-Verschlüsselung Ihrer [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(deaktiviert)</li><li>`EncryptionMethod=1`(aktiviert)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validiert das Zertifikat, das bei der Anwendung von `EncryptionMethod` von Ihrer [!DNL PostgreSQL]-Datenbank gesendet wird. | <uL><li>`ValidationServerCertificate=0`(deaktiviert)</li><li>`ValidationServerCertificate=1`(aktiviert)</li></ul> |

Im Folgenden finden Sie ein Beispiel für eine [!DNL PostgreSQL] Verbindungszeichenfolge, die mit SSL-Verschlüsselung angehängt wird: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Navigieren im Quellkatalog {#navigate}

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Wählen Sie die entsprechende Kategorie im Bedienfeld *[!UICONTROL Kategorien]* aus Alternativ können Sie die Suchleiste verwenden, um zur gewünschten Quelle zu navigieren.

Um [!DNL PostgreSQL] zu verwenden, wählen Sie die Quellkarte **[!UICONTROL PostgreSQL]** unter *[!UICONTROL Datenbanken]* und dann **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Nachdem ein authentifiziertes Konto erstellt wurde, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.



## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL PostgreSQL] Konto aus, das Sie verwenden möchten.

![Die vorhandene Kontoschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/postgresql/catalog.png)

## Neues Konto erstellen {#create}

Wenn Sie noch kein -Konto haben, müssen Sie ein neues Konto erstellen, indem Sie die Authentifizierungsdaten angeben, die Ihrer Quelle entsprechen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu.

![Die neue Kontoschnittstelle im Quell-Workflow mit einem Kontonamen und einer optionalen Beschreibung.](../../../../images/tutorials/create/postgresql/existing.png)

### Verbindung zu Experience Platform auf Azure herstellen {#azure}

Sie können Ihr [!DNL PostgreSQL]-Konto mit Experience Platform auf Azure verbinden, indem Sie entweder den Kontoschlüssel oder die Standardauthentifizierung verwenden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Kontoschlüsselauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Kontoschlüsselauthentifizierung]**, geben Sie Ihre [Verbindungszeichenfolge](../../../../connectors/databases/postgres.md#azure) an und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]**.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Authentifizierung des Kontoschlüssels“.](../../../../images/tutorials/create/postgresql/account-key.png)

>[!TAB Einfache Authentifizierung]

Um die Standardauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Standardauthentifizierung]** aus, geben Sie Werte für Ihre [Authentifizierungsdaten](../../../../connectors/databases/postgres.md#azure) ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus.

![Die neue Kontoschnittstelle im Quell-Workflow mit ausgewählter „Standardauthentifizierung“.](../../../../images/tutorials/create/postgresql/basic-auth.png)

>[!ENDTABS]

### Verbinden mit Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Um ein neues [!DNL PostgreSQL]-Konto zu erstellen und eine Verbindung zu Experience Platform auf AWS herzustellen, stellen Sie sicher, dass Sie sich in einer VA6-Sandbox befinden, und geben Sie dann die erforderlichen [ (Anmeldeinformationen für die Authentifizierung) ](../../../../connectors/databases/postgres.md#aws).

![Die neue Kontoschnittstelle im Quell-Workflow zum Herstellen einer Verbindung mit AWS.](../../../../images/tutorials/create/postgresql/basic-auth.png)

## Erstellen eines Datenflusses für Ihre [!DNL PostgreSQL]

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL MariaDB]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](../../dataflow/databases.md).
