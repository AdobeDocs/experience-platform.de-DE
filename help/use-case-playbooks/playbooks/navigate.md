---
solution: Experience Platform
title: Navigieren Sie zu "Anwendungsfall-Playbooks".
description: Erfahren Sie, wie Sie in einer Galerie mit Büchern navigieren und mit einer inspirierenden Sandbox beginnen.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Navigieren Sie zu &quot;Anwendungsfall-Playbooks&quot;.

Anwendungsfall-Playbooks sind für alle Adobe Experience Platform-Kunden kostenlos verfügbar. Um auf eine Rich-Galerie mit Anwendungsfallbüchern in der Experience Platform-Benutzeroberfläche zuzugreifen, wählen Sie im linken Navigationsbereich **[!UICONTROL Playbooks]** aus.

![Verwenden Sie die Bilderbuchgalerie.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Direkter Zugriff auf die Fallbücher in der linken Navigationsleiste.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Wählen Sie ein beliebiges Playbook aus, um zur Detailseite zu gelangen, und wählen Sie dann **[!UICONTROL Zu einer inspirierenden Sandbox wechseln]** aus. Ein Bestätigungsmodal wird angezeigt. Wählen Sie **Bestätigen** aus, um zur inspirierenden Sandbox zu wechseln, in der Sie die verschiedenen Anwendungsfälle untersuchen und testen können.

Wenn Sie nicht über die Berechtigung zum Erstellen von Sandboxes verfügen, wenden Sie sich an Ihren Administrator, um Unterstützung beim Erstellen einer inspirierenden Sandbox zu erhalten.

>[!TIP]
>
>Eine inspirierende Sandbox ist eine Entwicklungs-Sandbox in Adobe Experience Platform, in der Sie verschiedene Anwendungsfälle erstellen, testen und testen können, bevor Sie sie in eine Live-Produktionsumgebung implementieren.

![Navigieren Sie zur inspirierenden Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Wenn Sie noch keine inspirierenden Sandboxes eingerichtet haben, wählen Sie **[!UICONTROL Erstellen einer inspirierenden Sandbox]**. Ein Modal wird angezeigt. Geben Sie die Felder **Name** und **Titel** in die erforderlichen Felder ein und wählen Sie **Erstellen** aus. Nachdem Sie die inspirierende Sandbox erstellt haben, stellen Sie sicher, dass Sie [Berechtigungen definieren](/help/access-control/home.md) , bevor Sie zur Detailseite für die Anwendungsfälle-Playbooks zurückkehren, um eine Instanz zu erstellen.

![Erstellen Sie eine inspirierende Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Geben Sie Namen und Titel ein, um eine inspirierende Sandbox zu erstellen.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Wenn Sie ein Anwendungsfallbuch außerhalb einer inspirierenden Sandbox auswählen, können Sie keine Instanz erstellen. Wählen Sie auf der Detailseite **Zur inspirierenden Sandbox wechseln** aus, um zu einer vorhandenen inspirierenden Sandbox zu wechseln. Wählen Sie dann **[!UICONTROL Instanz erstellen]** aus.

Wenn Sie nicht über die Berechtigung zum Erstellen von Sandboxes verfügen, wenden Sie sich an Ihren Administrator, um Unterstützung beim Erstellen einer inspirierenden Sandbox zu erhalten.

![Keine Berechtigungen zum Erstellen einer Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Wenn Sie die Grenze für die Anzahl der Ihnen zugewiesenen Sandboxes erreicht haben, werden Sie in einer Meldung aufgefordert, Ihren Organisationsadministrator zu kontaktieren, um die Beschränkung zu erhöhen oder einige aktive Sandboxes zu deaktivieren oder zu entfernen. Nachdem Sie die Sandbox-Beschränkung angepasst oder die Anzahl der aktiven Sandboxes reduziert haben, können Sie mit der Erstellung der inspirierenden Sandbox fortfahren.

![Sandbox-Limit erreicht.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Beachten Sie, dass bei der Erstellung einer inspirierenden Sandbox Kanalflächen für E-Mail-, Push- und SMS-Benachrichtigungen nicht automatisch eingerichtet werden. Wenden Sie sich an Ihren IT-Administrator, um sie manuell zu konfigurieren. Andernfalls kann die Instanzerstellung fehlschlagen.

![Konfigurieren von Kanalvorgaben.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Konfigurieren von Sandbox- und Kanaloberflächen in Journey Optimizer {#configure-channel-surfaces}

Wenn Ihr Unternehmen für [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) lizenziert ist und Sie die für Journey Optimizer entwickelten Playbooks verwenden möchten, müssen Sie die Kanalvorgaben in Ihrer Sandbox konfigurieren, die die für Ihre Nachrichten erforderlichen technischen Parameter definieren. [Erfahren Sie, wie Sie in Adobe Journey Optimizer Kanaloberflächen einrichten.](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=de).

Um in Journey Optimizer Playbooks zu erstellen, müssen Sie Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen konfigurieren.

### E-Mail-Kanaloberfläche

Wechseln Sie in der Journey Optimizer-Benutzeroberfläche zu &quot;`Channels`&quot;. Konfigurieren Sie separate Subdomains und IP-Pools für Marketing-E-Mails und Transaktionsnachrichten, falls noch nicht konfiguriert. Dies sind Best Practices, um sicherzustellen, dass Transaktionsnachrichten wie Auftragsbestätigungs-E-Mails an Ihre Kunden weitergeleitet werden. Geben Sie Namen, E-Mail-Adressen und zusätzliche Einstellungen ein. Wählen Sie oben rechts auf der Seite **Senden** aus, um die Oberfläche des Marketing-Kanals zu erstellen. Lesen Sie die Dokumentation zu [Einrichten von E-Mail-Kanal-Oberflächen](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-Kanaloberfläche

Um eine SMS-Kanaloberfläche zu erstellen, erstellen Sie zunächst eine SMS-API-Berechtigung und wählen Sie den gewünschten Anbieter aus (z. B. Sinch). Benennen Sie die SMS-Kanaloberfläche (z. B. SMS Marketing), wählen Sie die Konfiguration aus und geben Sie eine Absendernummer ein. Wählen Sie oben rechts auf der Seite **Senden** aus, um die Oberfläche des SMS-Kanals zu speichern. Lesen Sie die Dokumentation zu [Einrichten von Oberflächen in SMS-Kanälen](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms).

Konfigurieren Sie außerdem Kanäle für Playbooks, die Transaktionsnachrichten wie Bestellbestätigungen enthalten.

### Push-Kanaloberfläche

Vergewissern Sie sich, dass die App über die Experience Platform- oder Datenerfassungs-Benutzeroberfläche konfiguriert ist. So sehen App-Oberflächen in der Umgebung &quot;Datenerfassungen&quot;aus.

## Nächste Schritte {#next-steps}

Nachdem Sie dieses Dokument gelesen haben, sollten Sie wissen, wie Sie eine inspirierende Sandbox einrichten und mit verschiedenen Möglichkeiten zum Zugriff auf Anwendungsfallbücher in Platform vertraut sein können. Lesen Sie als nächsten Schritt, wie Sie [das richtige Playbook auswählen](/help/use-case-playbooks/playbooks/choose.md).
