---
keywords: Experience Platform;Home;beliebte Themen;SFTP;SFTP
solution: Experience Platform
title: Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine SFTP-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 6%

---

# Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche

In diesem Lernprogramm werden Schritte zum Erstellen einer SFTP-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Einsetzen von JSON-Objekten mit einer SFTP-Quellverbindung Zeilenumbrüche oder Wagenrückgaben zu vermeiden. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden Sie mehrere Zeilen für die anschließenden Dateien.

Wenn Sie bereits über eine gültige SFTP-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung zu SFTP herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem SFTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren SFTP-Server. |
| `password` | Das Kennwort für Ihren SFTP-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Die Phrase oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Phrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues SFTP-Konto für die Verbindung mit der Plattform zu erstellen.

## Verbindung zum SFTP-Server herstellen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein eingehendes Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Datenspeicherung] **[!UICONTROL SFTP]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um eine neue SFTP-Verbindung zu erstellen.

![Katalog](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite **[!UICONTROL Mit SFTP verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

Der SFTP-Connector bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter **[!UICONTROL Kontoauthentifizierung]** **[!UICONTROL Kennwort]** aus, um eine kennwortbasierte Berechtigung zu verwenden.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Alternativ können Sie **[SSH-öffentlichen Schlüssel]** auswählen und Ihr SFTP-Konto mit einer Kombination aus [!UICONTROL Inhalt mit privatem Schlüssel] und [!UICONTROL Passphrase] verbinden.

>[!IMPORTANT]
>
>Der SFTP-Connector unterstützt einen RSA- oder DSA-Typ OpenSSH-Schlüssel. Stellen Sie sicher, dass der Inhalt der Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um das PPK in das OpenSSH-Format zu konvertieren.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Inhalt privater Schlüssel | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| Passphrase | Gibt den Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels an, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/sftp/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem FTP- oder SFTP-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.
