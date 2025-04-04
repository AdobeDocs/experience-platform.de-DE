---
title: Übersicht über den SFTP-Quell-Connector
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche einen SFTP-Server mit Adobe Experience Platform verbinden.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 45%

---

# SFTP-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Lesen Sie dieses Dokument über die erforderlichen Schritte, die Sie durchführen müssen, um Ihr [!DNL SFTP]-Konto erfolgreich mit Experience Platform zu verbinden.

>[!TIP]
>
>Sie müssen die interaktive Tastaturauthentifizierung in der SFTP-Server-Konfiguration vor der Verbindung deaktivieren. Durch Deaktivieren der Einstellung können Passwörter manuell eingegeben werden, im Gegensatz zur Eingabe über einen Dienst oder ein Programm.

## Voraussetzungen {#prerequisites}

In diesem Abschnitt finden Sie die erforderlichen Schritte, die Sie ausführen müssen, um Ihre [!DNL SFTP] erfolgreich mit Experience Platform zu verbinden.

### IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

### Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

* Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
* Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
* Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
* Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
* Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

### Einrichten eines Base64-kodierten privaten OpenSSH-Schlüssels für [!DNL SFTP]

Die [!DNL SFTP]-Quelle unterstützt die Authentifizierung mit dem [!DNL Base64]-kodierten privaten OpenSSH-Schlüssel. In den folgenden Schritten finden Sie Informationen zum Generieren Ihres Base64-kodierten privaten OpenSSH-Schlüssels und zum Verbinden von [!DNL SFTP] mit Experience Platform.

>[!BEGINTABS]

>[!TAB Windows]

### [!DNL Windows]-Benutzer

Wenn Sie ein [!DNL Windows]-Gerät verwenden, öffnen Sie das Menü **Start** und wählen Sie dann **Einstellungen**.

![Einstellungen](../../images/tutorials/create/sftp/settings.png)

Wählen Sie im angezeigten Menü **Einstellungen** die Option **Programme** aus.

![Programme](../../images/tutorials/create/sftp/apps.png)

Wählen Sie als Nächstes **Optionale Funktionen**.

![optional-features](../../images/tutorials/create/sftp/optional-features.png)

Eine Liste optionaler Funktionen wird angezeigt. Wenn der **OpenSSH-Client** bereits auf Ihrem Computer vorinstalliert ist, wird er in die Liste **Installierte Funktionen** unter **Optionale Funktionen** aufgenommen.

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

Falls nicht installiert, wählen Sie **Installieren** und öffnen Sie dann **[!DNL Powershell]** und führen Sie den folgenden Befehl aus, um Ihren privaten Schlüssel zu generieren:

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

Führen Sie als Nächstes den folgenden Befehl aus, während Sie den Dateipfad des privaten Schlüssels angeben, um Ihren privaten Schlüssel in [!DNL Base64] zu kodieren:

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

Der obige Befehl speichert den [!DNL Base64]-kodierten privaten Schlüssel in dem von Ihnen angegebenen Dateipfad. Sie können diesen privaten Schlüssel dann verwenden, um sich bei [!DNL SFTP] zu authentifizieren und eine Verbindung zu Experience Platform herzustellen.

>[!TAB Mac]

### [!DNL Mac]-Benutzer

Wenn Sie ein [!DNL Mac] verwenden, öffnen Sie **Terminal** und führen Sie den folgenden Befehl aus, um den privaten Schlüssel zu generieren (in diesem Fall wird der private Schlüssel in `/Documents/id_rsa` gespeichert):

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

Führen Sie als Nächstes den folgenden Befehl aus, um den privaten Schlüssel in [!DNL Base64] zu kodieren:

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Sobald Ihr [!DNL Base64]-kodierter privater Schlüssel in dem von Ihnen festgelegten Ordner gespeichert ist, müssen Sie den Inhalt Ihrer öffentlichen Schlüsseldatei zu einer neuen Zeile in den vom [!DNL SFTP]-Host autorisierten Schlüsseln hinzufügen. Führen Sie den folgenden Befehl in der Befehlszeile aus:

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

Um zu überprüfen, ob Ihr öffentlicher Schlüssel ordnungsgemäß hinzugefügt wurde, können Sie Folgendes über die Befehlszeile ausführen:

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### Sammeln erforderlicher Anmeldedaten {#credentials}

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihren [!DNL SFTP] mit Experience Platform zu verbinden.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen an, um Ihren [!DNL SFTP]-Server mit einfacher Authentifizierung zu authentifizieren.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem [!DNL SFTP]-Server verknüpft ist. |
| `port` | Der [!DNL SFTP] Server-Port, mit dem Sie eine Verbindung herstellen. Wenn kein Wert angegeben wird, ist der Standardwert `22`. |
| `username` | Der Benutzername mit Zugriff auf Ihren [!DNL SFTP]. |
| `password` | Das Kennwort für Ihren [!DNL SFTP]. |
| `maxConcurrentConnections` | Mithilfe dieses Parameters können Sie einen Maximalwert für die Anzahl gleichzeitiger Verbindungen festlegen, die Experience Platform beim Herstellen einer Verbindung mit Ihrem SFTP-Server erstellt. Sie müssen diesen Wert kleiner als das von SFTP festgelegte Limit festlegen. **Hinweis**: Wenn diese Einstellung für ein vorhandenes SFTP-Konto aktiviert ist, wirkt sie sich nur auf zukünftige Datenflüsse aus, nicht auf vorhandene Datenflüsse. |
| `folderPath` | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. [!DNL SFTP] -Quelle können Sie den Ordnerpfad bereitstellen, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| `disableChunking` | Während der Datenaufnahme kann die [!DNL SFTP] zunächst die Dateilänge abrufen, die Datei in mehrere Teile aufteilen und diese dann parallel lesen. Sie können diesen Wert aktivieren oder deaktivieren, um anzugeben, ob Ihr [!DNL SFTP] Dateilängen abrufen oder Daten von einem bestimmten Offset lesen kann. |
| `connectionSpec.id` | (Nur API) Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL SFTP] ist: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!TAB SSH-Authentifizierung mit öffentlichem Schlüssel]

Geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen ein, um Ihren [!DNL SFTP]-Server mithilfe der SSH-Authentifizierung mit öffentlichem Schlüssel zu authentifizieren.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem [!DNL SFTP]-Server verknüpft ist. |
| `port` | Der [!DNL SFTP] Server-Port, mit dem Sie eine Verbindung herstellen. Wenn kein Wert angegeben wird, ist der Standardwert `22`. |
| `username` | Der Benutzername mit Zugriff auf Ihren [!DNL SFTP]. |
| `password` | Das Kennwort für Ihren [!DNL SFTP]. |
| `privateKeyContent` | Der mit Base64 kodierte Inhalt des privaten SSH-Schlüssels. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Die Passphrase oder das Passwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Passphrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `maxConcurrentConnections` | Mithilfe dieses Parameters können Sie einen Maximalwert für die Anzahl gleichzeitiger Verbindungen festlegen, die Experience Platform beim Herstellen einer Verbindung mit Ihrem SFTP-Server erstellt. Sie müssen diesen Wert kleiner als das von SFTP festgelegte Limit festlegen. **Hinweis**: Wenn diese Einstellung für ein vorhandenes SFTP-Konto aktiviert ist, wirkt sie sich nur auf zukünftige Datenflüsse aus, nicht auf vorhandene Datenflüsse. |
| `folderPath` | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. [!DNL SFTP] -Quelle können Sie den Ordnerpfad bereitstellen, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| `disableChunking` | Während der Datenaufnahme kann die [!DNL SFTP] zunächst die Dateilänge abrufen, die Datei in mehrere Teile aufteilen und diese dann parallel lesen. Sie können diesen Wert aktivieren oder deaktivieren, um anzugeben, ob Ihr [!DNL SFTP] Dateilängen abrufen oder Daten von einem bestimmten Offset lesen kann. |
| `connectionSpec.id` | (Nur API) Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL SFTP] ist: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!ENDTABS]

## Verbinden von SFTP mit Experience Platform

Die folgende Dokumentation enthält Informationen zum Verbinden eines SFTP-Servers mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden der APIs

* [Erstellen einer SFTP-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/sftp.md)
* [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
* [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/sftp.md)
* [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
