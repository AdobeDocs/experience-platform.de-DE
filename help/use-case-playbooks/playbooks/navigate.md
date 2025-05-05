---
solution: Experience Platform
title: Navigieren zu Playbooks für Anwendungsfälle
description: Erfahren Sie, wie Sie durch eine Galerie mit Playbooks navigieren und beginnen Sie mit einer inspirierenden Sandbox.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Navigieren zu Playbooks für Anwendungsfälle

Playbooks für Anwendungsfälle sind für alle Adobe Experience Platform-Kunden kostenlos verfügbar. Um in der Benutzeroberfläche von Experience Platform auf eine umfangreiche Sammlung von Playbooks für Anwendungsfälle zuzugreifen, wählen Sie **[!UICONTROL linken Navigationsbereich die Option]** Playbooks“ aus.

![Anwendungsfall Playbook-Galerie.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Direkter Zugriff auf Playbooks für Anwendungsfälle in der linken Navigationsleiste.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Wählen Sie ein Playbook aus, um zur Detailseite zu gelangen, und wählen Sie dann **[!UICONTROL Zu einer inspirierenden Sandbox gehen]**. Ein Bestätigungs-Modal wird angezeigt. Wählen Sie **Bestätigen**, um zur inspirierenden Sandbox zu wechseln, in der Sie die verschiedenen Anwendungsfälle erkunden und mit ihnen experimentieren können.

Wenn Sie nicht über die Berechtigung zum Erstellen von Sandboxes verfügen, wenden Sie sich an Ihren Administrator, um Hilfe beim Erstellen einer inspirierenden Sandbox zu erhalten.

>[!TIP]
>
>Eine inspirierende Sandbox ist eine Entwicklungs-Sandbox in Adobe Experience Platform, in der Sie verschiedene Anwendungsfälle erstellen, testen und experimentieren können, bevor Sie sie in einer Live-Produktionsumgebung implementieren.

![Zu inspirierender Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Wenn Sie noch keine inspirierenden Sandboxes eingerichtet haben, wählen Sie **[!UICONTROL Erstellen einer inspirierenden Sandbox]** aus. Ein modales Fenster wird angezeigt. Geben Sie **Name** und **Titel** in die erforderlichen Felder ein und wählen Sie **Erstellen**. Nachdem Sie die inspirierende Sandbox erstellt haben, stellen Sie sicher[ dass Sie Berechtigungen definieren](/help/access-control/home.md) bevor Sie zurück zur Detailseite für Anwendungsfälle in Playbooks navigieren, um eine Instanz zu erstellen.

![Erstellen Sie eine inspirierende Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Geben Sie Namen und Titel ein, um eine inspirierende Sandbox zu erstellen.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Wenn Sie ein Playbook mit einem Anwendungsfall außerhalb einer inspirierenden Sandbox auswählen, können Sie keine Instanz erstellen. Wählen Sie auf der Detailseite die Option **Zu inspirierender Sandbox wechseln** aus, um zu einer vorhandenen inspirierenden Sandbox zu wechseln, und wählen Sie dann **[!UICONTROL Instanz erstellen]** aus.

Wenn Sie nicht über die Berechtigung zum Erstellen von Sandboxes verfügen, wenden Sie sich an Ihren Administrator, um Hilfe beim Erstellen einer inspirierenden Sandbox zu erhalten.

![Keine Berechtigungen zum Erstellen einer Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Wenn Sie das Limit für die Anzahl der Ihnen zugewiesenen Sandboxes erreicht haben, werden Sie in einer Meldung aufgefordert, den Administrator Ihrer Organisation zu kontaktieren, um das Limit zu erhöhen oder einige aktive Sandboxes zu deaktivieren oder zu entfernen. Nachdem Ihr Sandbox-Limit angepasst oder Ihre Anzahl aktiver Sandboxes reduziert wurde, können Sie mit der Erstellung der inspirierenden Sandbox fortfahren.

![Sandbox-Limit erreicht.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Beachten Sie, dass beim Erstellen einer inspirierenden Sandbox Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen nicht automatisch eingerichtet werden. Wenden Sie sich an Ihren IT-Administrator, um sie manuell zu konfigurieren, da ansonsten die Instanzerstellung fehlschlagen könnte.

![Konfigurieren von Kanalvorgaben.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Konfigurieren von Sandbox- und Kanaloberflächen in Journey Optimizer {#configure-channel-surfaces}

Wenn Ihr Unternehmen für [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) lizenziert ist und Sie die für Journey Optimizer entwickelten Playbooks verwenden möchten, müssen Sie die Kanalvorgaben in Ihrer Sandbox konfigurieren, die die für Ihre Nachrichten erforderlichen technischen Parameter definieren. [Erfahren Sie, wie Sie in Adobe Journey Optimizer Kanaloberflächen einrichten.](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/configuration/channel-surfaces).

Um Instanzen von Playbooks in Journey Optimizer zu erstellen, müssen Sie Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen konfigurieren.

### E-Mail-Kanaloberfläche

Navigieren Sie zu `Channels` in der Benutzeroberfläche von Journey Optimizer. Konfigurieren Sie separate Subdomains und IP-Pools für Marketing-E-Mails und Transaktionsnachrichten, falls noch nicht konfiguriert. Dies sind Best Practices, um sicherzustellen, dass Transaktionsnachrichten, wie z. B. E-Mails zur Bestellbestätigung, an Ihre Kunden gesendet werden. Geben Sie Namen, E-Mail-Adressen und zusätzliche Einstellungen ein. Wählen **oben rechts** der Seite „Senden“ aus, um die Marketing-Kanal-Oberfläche zu erstellen. Lesen Sie die Dokumentation [Einrichten von Oberflächen für E-Mail-Kanäle](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html?lang=de).

### SMS-Kanaloberfläche

Um eine SMS-Kanaloberfläche zu erstellen, erstellen Sie zunächst Anmeldedaten für die SMS-API und wählen Sie den bevorzugten Anbieter aus (z. B. Sinch). Benennen Sie die SMS-Kanaloberfläche (z. B. SMS-Marketing), wählen Sie die Konfiguration aus und geben Sie eine Absendernummer ein. Wählen **oben rechts** der Seite „Senden“ aus, um die SMS-Kanaloberfläche zu speichern. Lesen Sie die Dokumentation [Einrichten von Oberflächen für SMS-Kanäle](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms).

Konfigurieren Sie auch Kanäle für Playbooks, die Transaktionsnachrichten enthalten, z. B. Bestellbestätigungen.

### Kanaloberfläche per Push übertragen

Vergewissern Sie sich, dass die Kanalkonfigurationen entweder über die Experience Platform- oder die Datenerfassungsschnittstelle konfiguriert sind. So sehen Kanalkonfigurationen in der Datenerfassungsumgebung aus.

## Nächste Schritte {#next-steps}

Nachdem Sie dieses Dokument gelesen haben, sollten Sie wissen, wie Sie eine inspirierende Sandbox einrichten und mit verschiedenen Möglichkeiten für den Zugriff auf Anwendungsfall-Playbooks in Experience Platform vertraut sein. Lesen Sie als nächsten Schritt, wie Sie [ richtige Playbook ](/help/use-case-playbooks/playbooks/choose.md)wählen“.
