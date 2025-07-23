---
title: SFTP-Hosts
description: Erfahren Sie, wie Sie Tags in Adobe Experience Platform so konfigurieren, dass Bibliotheks-Builds auf einem gesicherten, selbstgehosteten SFTP-Server bereitgestellt werden.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: a077d3a1b14d9b7786d3181a556c49e940a42c2f
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 37%

---

# SFTP-Hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Mit Experience Platform können Sie Builds von Tag-Bibliotheken auf einem gesicherten SFTP-Server bereitstellen, den Sie hosten, sodass Sie besser steuern können, wie Ihre Builds gespeichert und verwaltet werden. In diesem Handbuch wird beschrieben, wie Sie einen SFTP-Host für eine Tag-Eigenschaft in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche einrichten.

>[!NOTE]
>
>Sie können auch einen Host verwenden, der stattdessen von Adobe verwaltet wird. Weitere Informationen finden Sie im Handbuch zu [von Adobe verwalteten ](./managed-by-adobe-host.md).
>
>Informationen zu den Vorteilen und Einschränkungen von Self-Hosting-Bibliotheken finden Sie im [Handbuch zum Self-Hosting](./self-hosting-libraries.md).

## Einrichten eines Zugriffsschlüssels für den Server {#access-key}

Experience Platform stellt mithilfe eines verschlüsselten Schlüssels eine Verbindung zu Ihrer SFTP-Site her. Es sind einige Schritte nötig, um dies korrekt einzurichten:

### Erstellen eines Schlüsselpaars aus öffentlichem/privatem Schlüssel

Auf Ihrem SFTP-Server muss ein öffentliches/privates Schlüsselpaar installiert sein. Sie können diese Schlüssel auf Ihrem Server erstellen oder woanders generieren und auf Ihrem Server installieren. Weitere Informationen finden Sie in der GitHub-Dokumentation zum [Generieren von SSH-Schlüsseln](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key).

### Schlüssel verschlüsseln

Der private Schlüssel wird zum Verschlüsseln des öffentlichen Schlüssels verwendet. Sie müssen Ihren privaten Schlüssel während des Erstellungsprozesses des SFTP-Hosts angeben. Anweisungen zum Verschlüsseln [ öffentlichen Schlüsseln finden Sie ](../../../api/guides/encrypting-values.md) Abschnitt zum Verschlüsseln von Werten im Reactor-API-Handbuch. Verwenden Sie den GPG-Schlüssel der Produktionsumgebung, sofern Sie nicht wissen, dass Sie einen bestimmten Schlüssel benötigen. Sie können Ihren privaten Schlüssel auf jedem beliebigen Computer verschlüsseln. Sie müssen GPG also nicht auf Ihrem Server installieren, um diesen Schritt abzuschließen.

### Auf die Zulassungsliste setzen Experience Platforms-IP-Adressen

Möglicherweise müssen Sie eine Reihe von IP-Adressen genehmigen, die innerhalb Ihrer Unternehmens-Firewall verwendet werden, damit Experience Platform Ihren SFTP-Server erreichen und eine Verbindung zu ihm herstellen kann. Diese IP-Adressen lauten:

* `34.227.138.75`
* `44.194.43.191`
* `3.215.163.18`

>[!NOTE]
>
>Die Struktur der Tag-Builds hat sich im Laufe der Zeit geändert. Sie verwenden intern symbolische Links (Symlinks), um die Abwärtskompatibilität zu gewährleisten, sodass vorherige Einbettungs-Codes weiterhin mit der neuesten Build-Struktur funktionieren. Ihr SFTP-Server muss die Verwendung von Symlinks unterstützen, damit er ein gültiges Ziel für Tag-Builds ist.

Detaillierte Informationen finden Sie im folgenden Artikel von Medium zum [Einrichten von SFTP-Servern für die Bereitstellung eines Builds](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Erstellen eines SFTP-Hosts {#create}

Wählen **[!UICONTROL Hosts]** im linken Navigationsbereich aus, gefolgt von **[!UICONTROL Host hinzufügen]**.

![Bild, das die ausgewählte Schaltfläche „Host hinzufügen“ in der Benutzeroberfläche zeigt](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

Das Dialogfeld „Host-Erstellung“ wird angezeigt. Geben Sie einen Namen für den Host ein und wählen Sie unter **[!UICONTROL Type]** die Option **[!UICONTROL SFTP]** aus.

![Bild, das die ausgewählte SFTP-Hosting-Option zeigt](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### SFTP-Host konfigurieren {#configure}

Das Dialogfeld wird erweitert und enthält zusätzliche Konfigurationsoptionen für den SFTP-Host. Diese werden nachfolgend erläutert.

![Bild mit den erforderlichen Details für eine SFTP-Host-Verbindung](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Konfigurationsfeld | Beschreibung |
| --- | --- |
| [!UICONTROL Verwenden Sie keine Symlinks] | Standardmäßig verwenden alle SFTP-Hosts symbolische Links (Symlinks), um auf Bibliotheks-[ (Builds](../builds.md) zu verweisen, die auf dem Server gespeichert werden. Nicht alle Server unterstützen jedoch die Verwendung von Symlinks. Wenn diese Option ausgewählt ist, verwendet der Host einen Kopiervorgang, um die Build-Assets direkt zu aktualisieren, anstatt Symlinks zu verwenden. |
| [!UICONTROL SFTP-Server-URL] | Der URL-Basispfad für Ihren Server. |
| [!UICONTROL Pfad] | Der Pfad, der an die Basis-Server-URL für diesen Host angehängt werden soll. |
| [!UICONTROL Port] | Der Port muss einer der folgenden sein:<ul><li>`21`</li><li>`22`</li><li>`201`</li><li>`200`</li><li>`2002`</li><li>`2018`</li><li>`2022`</li><li>`2200`</li><li>`2222`</li><li>`2333`</li><li>`2939`</li><li>`443`</li><li>`4343`</li><li>`80`</li><li>`8080`</li><li>`8888`</li></ul>Als Best Practice im Hinblick auf die Sicherheit beschränkt Adobe die Anzahl der Ports, die für den ausgehenden Datenverkehr verwendet werden können. Die ausgewählten Ports werden in der Regel über Unternehmens-Firewalls zugelassen und enthalten aus Gründen der Flexibilität einige Bereiche. |
| [!UICONTROL Benutzername] | Der Benutzername, der beim Zugriff auf den Server verwendet wird. |
| [!UICONTROL Verschlüsselter privater Schlüssel] | Der verschlüsselte private Schlüssel, den Sie in einem [ Schritt erstellt ](#access-key). |

Wählen Sie **[!UICONTROL Speichern]**, um den Host mit der ausgewählten Konfiguration zu erstellen.

![Bild, das den zu speichernden SFTP-Host anzeigt](../../../images/ui/publishing/sftp-hosts/save-host.png)

Wenn Sie **[!UICONTROL Speichern]** auswählen, werden die Verbindung und die Möglichkeit getestet, die Dateien an Ihren SFTP-Server zu senden. Experience Platform erstellt einen Ordner, schreibt eine Datei in diesen Ordner, prüft, ob die Datei dort vorhanden ist, und bereinigt sie anschließend selbst. Wenn das Benutzerkonto auf Ihrem SFTP-Server (das an das sichere Zertifikat angehängt ist, das Sie Experience Platform bereitgestellt haben) nicht über die erforderlichen Berechtigungen zum Ausführen dieser Aktion verfügt, wechselt der Host in den Status „Fehlgeschlagen“.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie einen selbst gehosteten SFTP-Server für die Verwendung in Tags einrichten. Sobald der Host eingerichtet wurde, können Sie ihn mit einer oder mehreren Ihrer [Umgebungen) verknüpfen, ](../environments.md) Tag-Bibliotheken zu veröffentlichen. Weitere Informationen zum allgemeinen Prozess der Aktivierung von Tag-Funktionen in Ihren Web- oder mobilen Eigenschaften finden Sie in der [Publishing-Übersicht](../overview.md).
