---
title: Konfigurieren von Warnhinweisen und IP-Zulassungsliste für Azure CMK
description: Auf die Zulassungsliste setzen Erfahren Sie, wie Sie die statische IP-Adresse von Adobe in Azure Key Vault ändern und verstehen, wie Experience Platform-Warnhinweise beim Erkennen und Beheben von Problemen beim Zugriff auf kundenverwaltete Schlüssel helfen.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Konfigurieren von Warnhinweisen und IP-Zulassungsliste für [!DNL Azure] CMK

Um die Transparenz zu verbessern, bietet Adobe einen [Überwachungsdienst](../../../../observability/alerts/ui.md){target="_blank"} der den Zugriffsstatus Ihres Schlüsseltresors überprüft und bei Problemen Trigger meldet. Diese Warnhinweise helfen Ihnen, schnell zu reagieren und Service-Unterbrechungen zu vermeiden. Auf die Zulassungsliste setzen Um diesen Service zu aktivieren, müssen Sie die statische IP-Adresse von Adobe ändern.

>[!IMPORTANT]
>
>Wenn Sie den Zugriff auf öffentliche Netzwerke deaktiviert oder Ihren [!DNL Azure]-Schlüsseltresor so konfiguriert haben, dass nur bestimmte Netzwerke zulässig sind, müssen Sie die statische IP-Adresse von Adobe auf die Zulassungsliste setzen zu Ihrer hinzufügen. Andernfalls werden Sie möglicherweise nicht über Zugriffsprobleme benachrichtigt, die sich auf Ihre Experience Platform-Instanz auswirken könnten.

## Zulassungsliste der statischen IP von Adobe in [!DNL Azure] Schlüsseltresor {#add-adobe-static-ip}

Um diese Warnhinweise unter Beibehaltung der Netzwerkbeschränkungen zu aktivieren, navigieren Sie zu Ihrem **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**. Wählen Sie auf der Registerkarte **[!DNL Firewalls and virtual networks]** die Option **[!DNL Allow public access from specific virtual networks and IP addresses]** aus.

![[!DNL Azure] Bildschirm Key Vault-Netzwerkeinstellungen zeigt an, wo die statische IP-Adresse von Adobe hinzugefügt werden soll, und die Option Zugriff erlauben ist hervorgehoben.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Statische IP-Adresse von Adobe

>[!IMPORTANT]
>
>Die von Adobe bereitgestellte statische IP-Adresse lautet: `20.88.123.53`.

Wählen Sie anschließend im Abschnitt **[!DNL Firewall]** die Option **[!DNL Add your current IP address]** aus und ersetzen Sie sie durch die statische IP-Adresse von Adobe. Alle ausgehenden Verbindungen werden als Produktionsumgebungen behandelt. Daher muss diese statische IP-Adresse auf die Zulassungsliste gesetzt werden, um in eingeschränkten Netzwerkkonfigurationen einen unterbrechungsfreien Zugriff auf Ihren Schlüsseltresor zu gewährleisten.

>[!NOTE]
>
>Nachdem Sie die statische IP-Adresse in Ihren Einstellungen für den [!DNL Azure]-Schlüsseltresor hinzugefügt oder aktualisiert haben, warten Sie bis zu 10 Minuten, bis die Änderung wirksam wird. Nachdem die IP hinzugefügt wurde, greift die CMK-App auf den Schlüsseltresor zu, um die Berechtigungen zu überprüfen.

Nach der Zulassungsauflistung der statischen IP-Adresse von Adobe kann Experience Platform den Zugriff auf Ihre wichtigsten Vault- und Trigger-Warnhinweise überwachen, wenn Probleme auftreten. Diese Warnhinweise bieten frühe Warnhinweise, damit Sie reagieren können, bevor der Service betroffen ist. Im nächsten Abschnitt werden die Arten von Warnhinweisen beschrieben, die Sie erhalten können und wie Sie reagieren.

## Überwachen von Warnhinweisen {#monitor-alerts}

Warnhinweise in Platform informieren Sie über Probleme, die den Schlüsselzugriff unterbrechen können, z **[!UICONTROL B. &quot;]** des Schlüsselzugriffs“ oder &quot;**[!UICONTROL deaktivieren]**. Diese Warnhinweise helfen Ihnen dabei, Probleme schnell zu identifizieren, z. B. eine entfernte statische IP-Adresse oder eine falsch konfigurierte Firewall. Um den Zugriff wiederherzustellen, überprüfen Sie Ihre [!DNL Azure] Firewall-Einstellungen und fügen Sie die erforderliche IP-Adresse erneut hinzu.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Abonnieren Sie Adobe I/O-Ereignisbenachrichtigungen, um in Echtzeit Warnhinweise in Ihren Überwachungs-Tools zu erhalten. Anweisungen zum Setup finden Sie unter [Abonnieren von Adobe I/O-Ereignisbenachrichtigungen](../../../../observability/alerts/subscribe.md). Informationen zum Anzeigen und Verwalten von Warnhinweisen in Experience Platform [ Sie auch ](../../../../observability/alerts/ui.md) Handbuch zur Warnhinweis-Benutzeroberfläche .

## Nächste Schritte

Sie haben jetzt die IP-Zulassungsauflistung und die Überwachung von Warnhinweisen für Ihren [!DNL Azure]-Schlüsseltresor konfiguriert. Um die Einrichtung für kundenverwaltete Schlüssel in [!DNL Azure] abzuschließen, folgen Sie diesen Konfigurationshandbüchern.

- [Konfigurieren eines  [!DNL Azure] -Schlüsseltresors](./azure-key-vault-config.md)
- [Verwenden der API zum Einrichten von CMK](./api-set-up.md)
- [Verwenden der Benutzeroberfläche zum Einrichten von CMK](./ui-set-up.md)
