---
title: Erstellen einer SFTP-Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine SFTP-Quellverbindung erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 25%

---

# Erstellen einer [!DNL SFTP]-Quellverbindung über die Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL SFTP]-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Es wird empfohlen, bei der Aufnahme von JSON-Objekten mit einer [!DNL SFTP] Quellverbindung Zeilenumbrüche oder Zeilenumbrüche zu vermeiden. Um die Einschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden Sie mehrere Zeilen für nachfolgende Dateien.

Wenn Sie bereits über eine gültige [!DNL SFTP]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Lesen Sie [[!DNL SFTP] Authentifizierungshandbuch](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials), um ausführliche Schritte zum Abrufen Ihrer Authentifizierungsdaten zu erhalten.

## Herstellen einer Verbindung zu Ihrem [!DNL SFTP]

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud] die Option **[!UICONTROL SFTP]** und dann **[!UICONTROL Daten hinzufügen]**.

![Der Experience Platform-Quellkatalog mit der ausgewählten SFTP-Quelle.](../../../../images/tutorials/create/sftp/catalog.png)

Die **[!UICONTROL Verbindung zu SFTP herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![Liste der in der Experience Platform-Benutzeroberfläche vorhandenen SFTP-Konten.](../../../../images/tutorials/create/sftp/existing.png)

### Neues Konto

>[!TIP]
>
>* Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL SFTP] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.
>
>* SFTP unterstützt OpenSSH-Schlüssel vom Typ `ed25519`, `RSA` oder `DSA`. Stellen Sie sicher, dass Ihr Schlüsseldateiinhalt mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` beginnt und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine Datei im PPK-Format handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL SFTP]-Konto an.

![Der Bildschirm „Neues Konto“ für SFTP](../../../../images/tutorials/create/sftp/new.png)

Die [!DNL SFTP]-Quelle unterstützt sowohl die einfache Authentifizierung als auch die Authentifizierung über einen öffentlichen SSH-Schlüssel.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um die Standardauthentifizierung zu verwenden, wählen **[!UICONTROL Kennwort]** aus und geben Sie dann die entsprechenden Werte für die folgenden Anmeldeinformationen an:

* Host
* Port
* Benutzername
* Passwort

In diesem Schritt können Sie auch die maximale Anzahl gleichzeitiger Verbindungen konfigurieren, den Ordnerpfad definieren und das Chunking für Ihren [!DNL SFTP]-Server aktivieren oder deaktivieren. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt ist.

Weitere Informationen zur Authentifizierung finden Sie im Handbuch unter [Sammeln erforderlicher Anmeldeinformationen für [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Der Bildschirm für das neue Konto für die SFTP-Quelle mit einfacher Authentifizierung](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH-Authentifizierung mit öffentlichem Schlüssel]

Um SSH-Anmeldeinformationen mit öffentlichem Schlüssel zu verwenden, wählen Sie **[!UICONTROL SSH Public Key]** aus und geben Sie dann die entsprechenden Werte für die folgenden Anmeldeinformationen an:

* Host
* Port
* Benutzername
* Inhalt privater Schlüssel
* Passphrase

In diesem Schritt können Sie auch die maximale Anzahl gleichzeitiger Verbindungen konfigurieren, den Ordnerpfad definieren und das Chunking für Ihren [!DNL SFTP]-Server aktivieren oder deaktivieren. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt ist.

Weitere Informationen zur Authentifizierung finden Sie im Handbuch unter [Sammeln erforderlicher Anmeldeinformationen für [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Der Bildschirm mit dem neuen Konto für die SFTP-Quelle, die den öffentlichen SSH-Schlüssel verwendet.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
