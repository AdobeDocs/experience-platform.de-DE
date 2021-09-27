---
keywords: Experience Platform; Startseite; beliebte Themen; SFTP; SFTP
solution: Experience Platform
title: Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine SFTP-Quellverbindung erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 8%

---

# Erstellen einer [!DNL SFTP]-Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL SFTP]-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer [!DNL SFTP]-Quellverbindung Zeilenumbrüche oder Zeilenumbrüche zu vermeiden. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen für die darauf folgenden Dateien.

Wenn Sie bereits über eine gültige [!DNL SFTP]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/batch/cloud-storage.md)

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung zu [!DNL SFTP] herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem [!DNL SFTP]-Server verknüpft ist. |
| `port` | Der [!DNL SFTP] Server-Port, mit dem Sie eine Verbindung herstellen. Wenn kein Wert angegeben wird, wird standardmäßig `22` verwendet. |
| `username` | Der Benutzername mit Zugriff auf Ihren [!DNL SFTP]-Server. |
| `password` | Das Kennwort für Ihren [!DNL SFTP]-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL SFTP]-Konto für die Verbindung mit Platform zu erstellen.

## Verbindung zu Ihrem [!DNL SFTP]-Server herstellen

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein eingehendes Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL SFTP]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite **[!UICONTROL Verbindung zu SFTP]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/sftp/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL SFTP]-Konto ein.

#### Authentifizierung mit Kennwort

[!DNL SFTP] unterstützt verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter **[!UICONTROL Kontoauthentifizierung]** **[!UICONTROL Kennwort]** und geben Sie dann die Host- und Anschlusswerte für die Verbindung zusammen mit Ihrem Benutzernamen und Kennwort an.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Authentifizieren mit dem öffentlichen SSH-Schlüssel

Um die öffentlichen SSH-Schlüsselanmeldeinformationen zu verwenden, wählen Sie **[!UICONTROL SSH public key]** aus und geben Sie dann Ihre Host- und Anschlusswerte sowie Ihre privaten Schlüsselinhalte und Passphrase-Kombination an.

>[!IMPORTANT]
>
>SFTP unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` beginnt und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Inhalt privater Schlüssel | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| Passphrase | Gibt den Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels an, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase des PrivateKeyContent als Wert verwendet werden. |


## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.
