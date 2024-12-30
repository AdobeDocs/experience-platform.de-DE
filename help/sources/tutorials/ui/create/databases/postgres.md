---
keywords: Experience Platform;Startseite;beliebte Themen;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Erstellen einer PostgreSQL Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine PostgreSQL-Quellverbindung erstellen.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 47%

---

# Erstellen eines Quell-Connectors für [!DNL PostgreSQL] in der Benutzeroberfläche

Source-Connectoren in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen nach einem bestimmten Zeitplan aufzunehmen. In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL PostgreSQL]-Quell-Connectors mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL PostgreSQL]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL PostgreSQL]-Konto in [!DNL Platform] zugreifen zu können, müssen Sie den folgenden Wert angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die mit Ihrem [!DNL PostgreSQL]-Konto verknüpfte Verbindungszeichenfolge. Das [!DNL PostgreSQL]-Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL PostgreSQL] Dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivieren der SSL-Verschlüsselung für die Verbindungszeichenfolge

Sie können die SSL-Verschlüsselung für Ihre [!DNL PostgreSQL] Verbindungszeichenfolge aktivieren, indem Sie Ihre Verbindungszeichenfolge mit den folgenden Eigenschaften anhängen:

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `EncryptionMethod` | Ermöglicht die Aktivierung der SSL-Verschlüsselung Ihrer [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(deaktiviert)</li><li>`EncryptionMethod=1`(aktiviert)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validiert das Zertifikat, das bei der Anwendung von `EncryptionMethod` von Ihrer [!DNL PostgreSQL]-Datenbank gesendet wird. | <uL><li>`ValidationServerCertificate=0`(deaktiviert)</li><li>`ValidationServerCertificate=1`(aktiviert)</li></ul> |

Im Folgenden finden Sie ein Beispiel für eine [!DNL PostgreSQL] Verbindungszeichenfolge, die mit SSL-Verschlüsselung angehängt wird: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Verbinden Ihres [!DNL PostgreSQL]-Kontos

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PostgreSQL]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter **[!UICONTROL Kategorie]** die Option **[!UICONTROL PostgreSQL DB]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Wählen Sie andernfalls **[!UICONTROL Daten hinzufügen]** aus, um einen neuen [!DNL PostgreSQL]-Connector zu erstellen.

![](../../../../images/tutorials/create/postgresql/catalog.png)

Die **[!UICONTROL Verbindung zu[!DNL PostgreSQL]]** herstellen“ wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL PostgreSQL] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen **[!UICONTROL Verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/postgresql/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL PostgreSQL] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL PostgreSQL]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in zu importieren [!DNL Platform]](../../dataflow/databases.md).
