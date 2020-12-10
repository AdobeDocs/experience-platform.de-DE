---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Erstellen eines SFTP-Quellconnectors in der Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden Schritte zum Erstellen eines SFTP-Quell-Connectors mithilfe der Plattform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 7%

---


# Erstellen eines SFTP-Quellconnectors in der Benutzeroberfläche

>[!NOTE]
>
>Der SFTP-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

In diesem Lernprogramm werden Schritte zum Erstellen eines SFTP-Quell-Connectors mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige SFTP-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung zu SFTP herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem SFTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren SFTP-Server. |
| `password` | Das Kennwort für Ihren SFTP-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Das Format des privaten SSH-Schlüssels OpenSSH (RSA/DSA). |
| `passPhrase` | Die Phrase oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Phrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues SFTP-Konto für die Verbindung mit der Plattform zu erstellen.

## Verbindung zum SFTP-Server herstellen

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den [!UICONTROL Quellarbeitsbereich] zuzugreifen. Im Anzeigebereich &quot; [!UICONTROL Katalog] &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Datenspeicherung] die Option **[!UICONTROL SFTP]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Wählen Sie andernfalls **[!UICONTROL Hinzufügen Daten]** aus, um eine neue SFTP-Verbindung zu erstellen.

![Katalog](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite **[!UICONTROL Verbindung mit SFTP]** herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

Der SFTP-Connector bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter **[!UICONTROL Kontoauthentifizierung]** **[!UICONTROL Kennwort]** , um eine kennwortbasierte Berechtigung zu verwenden.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Alternativ können Sie **[SSH-öffentlichen Schlüssel]** auswählen und Ihr SFTP-Konto mit einer Kombination aus [!UICONTROL privatem Schlüsselinhalt] und [!UICONTROL Passphrase]verbinden.

>[!IMPORTANT]
>
>Der SFTP-Connector unterstützt einen RSA/DSA OpenSSH-Schlüssel. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit Beginn `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`übereinstimmt. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um das PPK in das OpenSSH-Format zu konvertieren.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Inhalt privater Schlüssel | Ein Base64-kodierter SSH-Inhalt mit privatem Schlüssel. Der private SSH-Schlüssel sollte im OpenSSH-Format vorliegen. |
| Passphrase | Gibt den Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels an, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP- oder SFTP-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/sftp/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem FTP- oder SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md)zu übertragen.