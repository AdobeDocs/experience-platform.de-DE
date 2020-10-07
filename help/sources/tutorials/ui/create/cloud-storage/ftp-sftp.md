---
keywords: Experience Platform;home;popular topics;SFTP;FTP;ftp;sftp
solution: Experience Platform
title: Erstellen eines Quell-Connectors für FTP oder SFTP über die Benutzeroberfläche
topic: overview
type: Tutorial
description: Dieses Lernprogramm enthält Schritte zum Erstellen eines FTP- oder SFTP-Quellconnectors über die Plattform-Benutzeroberfläche.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 9%

---


# Erstellen eines Quell-Connectors für FTP oder SFTP über die Benutzeroberfläche

>[!NOTE]
>
>Die FTP- und SFTP-Anschlüsse befinden sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines FTP- oder SFTP-Quellconnectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige FTP- oder SFTP-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/batch/cloud-storage.md)fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die aus externen Quellen erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf durch Kommas getrennte Werte (CSV) beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die allgemeine DSV-Unterstützung soll in Zukunft bereitgestellt werden.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

Um auf Ihren FTP- oder SFTP-Server zugreifen zu können, müssen [!DNL Platform]Sie den Hostnamen, einen Benutzernamen und ein Kennwort des Servers angeben.

## Herstellen einer Verbindung mit dem FTP- oder SFTP-Server

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues FTP- oder SFTP-Konto für die Verbindung zu erstellen [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den **[!UICONTROL Quellarbeitsbereich]** zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verschiedene Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL SFTP]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie &quot; **[!UICONTROL Konfigurieren]**&quot;aus. Wählen Sie andernfalls **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen FTP- oder SFTP-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/sftp/catalog.png)

Die Seite **[!UICONTROL Verbindung mit SFTP]** herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie &quot; **[!UICONTROL Verbinden]** &quot;und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

Der SFTP-Connector bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter **[!UICONTROL Kontoauthentifizierung]** **[!UICONTROL Kennwort]** , um eine kennwortbasierte Berechtigung zu verwenden.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Alternativ können Sie **[SSH-öffentlichen Schlüssel]** auswählen und Ihr SFTP-Konto mit einer Kombination aus **[!UICONTROL privatem Schlüsselinhalt]** und **[!UICONTROL Passphrase]** verbinden.

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

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem FTP- oder SFTP-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in [!DNL Platform]](../../dataflow/batch/cloud-storage.md)zu importieren.