---
title: Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine SFTP-Quellverbindung erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 23%

---

# Erstellen Sie eine [!DNL SFTP] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen eines [!DNL SFTP] Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer [!DNL SFTP] Quellverbindung. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen für die darauf folgenden Dateien.

Wenn Sie bereits über eine gültige [!DNL SFTP]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zu [!DNL SFTP]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrer [!DNL SFTP] Server. |
| `port` | Die [!DNL SFTP] Serveranschluss, mit dem Sie eine Verbindung herstellen. Wenn der Wert nicht angegeben wird, wird standardmäßig `22`. |
| `username` | Der Benutzername mit Zugriff auf Ihre [!DNL SFTP] Server. |
| `password` | Das Kennwort für Ihre [!DNL SFTP] Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `maxConcurrentConnections` | Mit diesem Parameter können Sie eine maximale Anzahl gleichzeitiger Verbindungen festlegen, die Platform beim Herstellen einer Verbindung zu Ihrem SFTP-Server erstellt. Sie müssen festlegen, dass dieser Wert kleiner als der von SFTP festgelegte Grenzwert ist. **Hinweis**: Wenn diese Einstellung für ein vorhandenes SFTP-Konto aktiviert ist, betrifft sie nur zukünftige Datenflüsse und nicht vorhandene Datenflüsse. |
| Ordnerpfad | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. [!DNL SFTP] -Quelle können Sie den Ordnerpfad angeben, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um eine neue [!DNL SFTP] -Konto, um eine Verbindung mit Platform herzustellen.

## Verbinden Sie Ihre [!DNL SFTP] server

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL SFTP]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Experience Platform-Quellkatalog mit der ausgewählten SFTP-Quelle.](../../../../images/tutorials/create/sftp/catalog.png)

Die **[!UICONTROL Verbindung zu SFTP herstellen]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Nächste]** um fortzufahren.

![Eine Liste der vorhandenen SFTP-Konten auf der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/sftp/existing.png)

### Neues Konto

>[!TIP]
>
>* Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL SFTP] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.
>
>* SFTP unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und endet mit `"-----END [RSA/DSA] PRIVATE KEY-----"`. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL SFTP] -Konto.

![Der neue Kontobildschirm für SFTP](../../../../images/tutorials/create/sftp/new.png)

Die [!DNL SFTP] -Quelle unterstützt sowohl einfache Authentifizierung als auch Authentifizierung über einen öffentlichen SSH-Schlüssel.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um die einfache Authentifizierung zu verwenden, wählen Sie **[!UICONTROL Passwort]** und geben Sie dann die Werte für Host und Anschluss an, mit denen eine Verbindung hergestellt werden soll, zusammen mit Ihrem Benutzernamen und Kennwort an. Während dieses Schritts können Sie auch den Pfad zum Unterordner angeben, auf den Sie Zugriff gewähren möchten. Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Der Bildschirm für das neue Konto für die SFTP-Quelle mit einfacher Authentifizierung](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Authentifizierung mit öffentlichen SSH-Schlüsseln]

Um die öffentlichen SSH-Schlüsselanmeldeinformationen zu verwenden, wählen Sie **[!UICONTROL Öffentlichen SSH-Schlüssel]**  und geben Sie dann Ihre Host- und Port-Werte sowie Ihren privaten Schlüsselinhalt und Ihre Passphrase-Kombination an. Während dieses Schritts können Sie auch den Pfad zum Unterordner angeben, auf den Sie Zugriff gewähren möchten. Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]**.

![Der neue Kontobildschirm für die SFTP-Quelle mit dem öffentlichen SSH-Schlüssel.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
