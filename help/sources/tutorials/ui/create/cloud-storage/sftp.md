---
title: Erstellen einer SFTP-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine SFTP-Quellverbindung erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 9cd1232c9257d27b80ed57c26658b1e4058535e8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 25%

---

# Erstellen einer [!DNL SFTP]-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine 0-Quell-Verbindung erstellen.[!DNL SFTP]

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer Quellverbindung vom Typ [!DNL SFTP] Zeilenumbrüche oder Zeilenumbrüche zu vermeiden. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen für die darauf folgenden Dateien.

Wenn Sie bereits über eine gültige [!DNL SFTP]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Ausführliche Anweisungen zum Abrufen Ihrer Authentifizierungsberechtigungen finden Sie im [[!DNL SFTP] Authentifizierungshandbuch](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) .

## Mit Ihrem [!DNL SFTP]-Server verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL SFTP]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Experience Platform-Quellkatalog mit der ausgewählten SFTP-Quelle.](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite **[!UICONTROL Verbindung zu SFTP herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![Eine Liste der vorhandenen SFTP-Konten auf der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/sftp/existing.png)

### Neues Konto

>[!TIP]
>
>* Nach der Erstellung können Sie den Authentifizierungstyp einer Basis-Verbindung vom Typ [!DNL SFTP] nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.
>
>* SFTP unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt der Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` beginnt und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL SFTP]-Konto ein.

![Der Bildschirm für das neue Konto für SFTP](../../../../images/tutorials/create/sftp/new.png)

Die Quelle [!DNL SFTP] unterstützt sowohl die einfache Authentifizierung als auch die Authentifizierung über den öffentlichen SSH-Schlüssel.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um eine einfache Authentifizierung zu verwenden, wählen Sie **[!UICONTROL Kennwort]** und geben Sie dann die entsprechenden Werte für die folgenden Anmeldeinformationen ein:

* Host
* port
* Benutzername
* password

Während dieses Schritts können Sie auch Ihre maximalen gleichzeitigen Verbindungen konfigurieren, Ihren Ordnerpfad definieren und das Blockieren für Ihren [!DNL SFTP] -Server aktivieren oder deaktivieren. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt wird.

Weitere Informationen zur Authentifizierung finden Sie im Handbuch unter [ Erfassen erforderlicher Anmeldedaten für  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Der Bildschirm für das neue Konto für die SFTP-Quelle mit einfacher Authentifizierung](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Authentifizierung mit öffentlichen SSH-Schlüsseln]

Um auf SSH-öffentlichen Schlüssel basierende Anmeldeinformationen zu verwenden, wählen Sie **[!UICONTROL SSH public key]** aus und geben Sie dann die entsprechenden Werte für die folgenden Anmeldeinformationen ein:

* Host
* port
* Benutzername
* Inhalt privater Schlüssel
* Passphrase

Während dieses Schritts können Sie auch Ihre maximalen gleichzeitigen Verbindungen konfigurieren, Ihren Ordnerpfad definieren und das Blockieren für Ihren [!DNL SFTP] -Server aktivieren oder deaktivieren. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt wird.

Weitere Informationen zur Authentifizierung finden Sie im Handbuch unter [ Erfassen erforderlicher Anmeldedaten für  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Der neue Kontobildschirm für die SFTP-Quelle mit dem öffentlichen SSH-Schlüssel.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.[
