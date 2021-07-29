---
title: SFTP-Hosts
description: Erfahren Sie, wie Sie Tags in Adobe Experience Platform konfigurieren, um Bibliotheks-Builds für einen gesicherten, selbstgehosteten SFTP-Server bereitzustellen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 44%

---

# SFTP-Hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Wenn Sie nicht möchten, dass Ihre gehosteten Bibliotheken von Adobe verwaltet werden, besteht die Möglichkeit, die Builds von Adobe Experience Platform an einen gesicherten SFTP-Server übermitteln zu lassen, den Sie selbst hosten.

Platform stellt mithilfe eines verschlüsselten Schlüssels eine Verbindung mit Ihrer SFTP-Site her. Es sind einige Schritte nötig, um dies korrekt einzurichten:

1. Auf Ihrem SFTP-Server muss ein öffentliches/privates Schlüsselpaar installiert sein. Sie können diese Schlüssel auf Ihrem Server generieren oder an einer anderen Stelle generieren und auf Ihrem Server installieren. Weitere Informationen finden Sie in der GitHub-Dokumentation zu [So generieren Sie SSH-Schlüssel](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) .
1. Der private Schlüssel wird zum Verschlüsseln des öffentlichen GPG-Schlüssels verwendet. Sie müssen Ihren privaten Schlüssel während des Erstellungsprozesses des SFTP-Hosts angeben. Anweisungen zum Verschlüsseln öffentlicher GPG-Schlüssel finden Sie im Abschnitt [Werte verschlüsseln](https://developer.adobelaunch.com/api/guides/encrypting_values/) in der Reactor-API-Dokumentation. Verwenden Sie den GPG-Schlüssel der Produktionsumgebung, sofern Sie nicht wissen, dass Sie einen bestimmten Schlüssel benötigen. Sie können Ihren privaten Schlüssel auf jedem beliebigen Computer verschlüsseln. Sie müssen GPG also nicht auf Ihrem Server installieren, um diesen Schritt abzuschließen.
1. Möglicherweise müssen Sie die mit Ihrer Unternehmens-Firewall verwendeten IP-Adressen genehmigen, damit Platform Ihren SFTP-Server erreichen und eine Verbindung mit ihm herstellen kann. Diese IP-Adressen lauten:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>Die Struktur der Tag-Builds hat sich im Laufe der Zeit geändert. Sie verwenden intern symbolische Links (Symlinks), um die Abwärtskompatibilität zu gewährleisten, sodass vorherige Einbettungs-Codes weiterhin mit der neuesten Build-Struktur funktionieren. Ihr SFTP-Server muss die Verwendung von Symlinks unterstützen, um als gültiges Ziel für Tag-Builds zu dienen.

Detaillierte Informationen finden Sie im folgenden Artikel von Medium zum Einrichten von SFTP-Servern für die Bereitstellung eines Builds](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).[

## Erstellen eines SFTP-Hosts

1. Öffnen Sie die Registerkarte [!UICONTROL Hosts].
1. Erstellen Sie den neuen Host.
1. Benennen Sie den Host.
1. Wählen Sie als Host-Typ **[!UICONTROL SFTP]** aus.
1. Geben Sie Host, Pfad, Port, Benutzernamen und den verschlüsselten privaten Schlüssel ein.

   Der Port muss einer der folgenden sein:

   * 21
   * 22
   * 80
   * 200–299
   * 443
   * 2000–2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Als bewährte Sicherheitsmethode beschränkt Adobe die Anzahl der Ports, die für den ausgehenden Datenverkehr verwendet werden können. Die ausgewählten Ports werden im Allgemeinen durch die Firewalls des Unternehmens zugelassen. Außerdem gewährleisten sie Flexibilität durch zusätzliche Bereiche.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

Wenn Sie **[!UICONTROL Speichern]** auswählen, werden die Verbindung und die Möglichkeit getestet, die Dateien an Ihren SFTP-Server zu senden. Platform erstellt einen Ordner, schreibt eine Datei in diesen Ordner, prüft, ob die Datei vorhanden ist, und löscht dann nach sich selbst. Wenn das Benutzerkonto auf Ihrem SFTP-Server (der mit dem sicheren Zertifikat verbunden ist, das Sie für Platform bereitgestellt haben) nicht über die erforderlichen Berechtigungen zum Ausführen dieser Aktion verfügt, wechselt der Host in den Status &quot;Fehlgeschlagen&quot;.
