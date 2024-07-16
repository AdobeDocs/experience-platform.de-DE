---
title: Erstellen einer SFTP-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine SFTP-Quellverbindung erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 21%

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

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zu [!DNL SFTP] herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die Ihrem [!DNL SFTP] -Server zugeordnet ist. |
| `port` | Der [!DNL SFTP] Server-Port, mit dem Sie eine Verbindung herstellen. Wenn nicht angegeben, wird der Wert standardmäßig auf `22` gesetzt. |
| `username` | Der Benutzername mit Zugriff auf Ihren [!DNL SFTP] -Server. |
| `password` | Das Kennwort für Ihren [!DNL SFTP] -Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `maxConcurrentConnections` | Mit diesem Parameter können Sie eine maximale Anzahl gleichzeitiger Verbindungen festlegen, die Platform beim Herstellen einer Verbindung zu Ihrem SFTP-Server erstellt. Sie müssen festlegen, dass dieser Wert kleiner als der von SFTP festgelegte Grenzwert ist. **Hinweis**: Wenn diese Einstellung für ein vorhandenes SFTP-Konto aktiviert ist, betrifft sie nur zukünftige Datenflüsse und nicht vorhandene Datenflüsse. |
| Ordnerpfad | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. [!DNL SFTP] -Quelle, können Sie den Ordnerpfad angeben, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues [!DNL SFTP]-Konto für die Verbindung mit Platform zu erstellen.

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

Um eine einfache Authentifizierung zu verwenden, wählen Sie **[!UICONTROL Kennwort]** und geben Sie dann neben Ihrem Benutzernamen und Kennwort die Host- und Anschlusswerte für die Verbindung an. Während dieses Schritts können Sie auch den Pfad zum Unterordner angeben, auf den Sie Zugriff gewähren möchten. Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![Der Bildschirm für das neue Konto für die SFTP-Quelle mit einfacher Authentifizierung](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Authentifizierung mit öffentlichen SSH-Schlüsseln]

Um die SSH-Anmeldeinformationen mit öffentlichem Schlüssel zu verwenden, wählen Sie **[!UICONTROL SSH-öffentlichen Schlüssel]** aus und geben Sie dann Ihre Host- und Anschlusswerte sowie Ihre privaten Schlüsselinhalte und Passphrase-Kombination an. Während dieses Schritts können Sie auch den Pfad zum Unterordner angeben, auf den Sie Zugriff gewähren möchten. Wählen Sie nach Abschluss **[!UICONTROL Mit Quelle verbinden]** aus.

![Der neue Kontobildschirm für die SFTP-Quelle mit dem öffentlichen SSH-Schlüssel.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.[
