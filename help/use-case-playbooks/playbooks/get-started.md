---
solution: Experience Platform
title: Erste Schritte mit Playbooks für Anwendungsfälle
description: Erfahren Sie, wie Sie die ersten Schritte mit der Funktion „Playbooks für Anwendungsfälle“ ausführen.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 703c84e61af105bc3933e4750a3cb27df8ac19fe
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 14%

---


# Erste Schritte

Erfahren Sie, wie Sie Ihr -Konto für Anwendungsfall-Playbooks einrichten, die für Real-time Customer Data Platform und Adobe Journey Optimizer entwickelt wurden, wenn es nicht automatisch eingerichtet wird. Die drei Hauptkonfigurationsschritte sind:

* Erstellen einer Sandbox
* Konfigurieren von Benutzerberechtigungen
* Konfigurieren von Journey Optimizer-Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen (wenn Sie Journey Optimizer-Playbooks verwenden möchten)

Um auf eine umfangreiche Sammlung von Anwendungsfall-Playbooks in der Experience Platform-Benutzeroberfläche zuzugreifen, wählen Sie **[!UICONTROL Playbooks]** in der linken Navigationsleiste aus. Lesen Sie die Dokumentation zum Navigieren [&#x200B; Playbooks für Anwendungsfälle &#x200B;](../playbooks/navigate.md) und beginnen Sie mit einer [inspirierenden Sandbox](../playbooks/navigate.md).

## Konfigurieren von Playbooks für Anwendungsfälle - Videoeinführung {#video}

In diesem Video erfahren Sie, wie Sie Ihre Sandbox erstellen, Berechtigungen konfigurieren und Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen in Journey Optimizer konfigurieren.

>[!VIDEO](https://video.tv.adobe.com/v/3449835?learn=on&captions=ger)

## Erstellen einer Entwicklungs-Sandbox {#create-development-sandbox}

Anwendungsfall Playbooks verwendet einen speziellen Typ von Entwicklungs-Sandbox. Zum Ausführen der ersten Schritte und Zugreifen auf die Funktion [[!UICONTROL Playbooks für Anwendungsfälle]](/help/use-case-playbooks/playbooks/overview.md) [erstellen Sie eine neue Entwicklungs-Sandbox](/help/sandboxes/ui/user-guide.md#create) (keine Produktions-Sandbox auswählen!), deren Namen (nicht deren Titel) entweder `-ucp` oder `-UCP` im Suffix enthält, wie unten dargestellt.

>[!IMPORTANT]
>
>Stellen Sie beim Erstellen einer neuen Entwicklungs-Sandbox sicher, dass der Name `-ucp` oder `-UCP` im Suffix enthält.


![Erstellen einer Entwicklungs-Sandbox für Playbooks für Anwendungsfälle](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

In der linken Leiste unter [!UICONTROL Anwendungsfall-Playbooks] sollte nun „Playbooks[!UICONTROL &#x200B; angezeigt &#x200B;].

![Verwenden der Option „Playbooks für Anwendungsfälle“ in der Benutzeroberfläche nach dem Erstellen einer Sandbox.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Wenn [!UICONTROL Playbooks] nicht wie oben gezeigt in der linken Leiste zu sehen ist, verwenden Sie diesen Link `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`, um direkt dorthin zu navigieren. Im Link ist `<YOUR_ORG>` der Name Ihres Unternehmens und `<YOUR_SANDBOX_NAME>` der Name der von Ihnen erstellten Entwicklungs-Sandbox.

## Erteilen der erforderlichen Zugriffsberechtigungen für Ihr Team {#grant-access-permissions}

Um mit Playbooks für [!UICONTROL Anwendungsfälle] zu beginnen, benötigen Mitglieder Ihres Marketing-Teams die richtigen Berechtigungen, damit sie die Liste der erstellten Playbooks anzeigen oder selbst Playbooks erstellen können.

**Erforderliche Berechtigungen**

Um die erforderlichen Berechtigungen hinzuzufügen, fügen Sie in der Benutzeroberfläche „Berechtigungen“ den neuen Anwendungsfall Playbook-Sandbox in [Rollen“ ein, die Sie bereits konfiguriert haben](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role) einschließlich der für andere Entwicklungs-Sandboxes verwendeten Rollen.

![Playbook-Sandbox für bereits konfigurierte Rollen](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Richten Sie eine Rolle für Playbooks ein:**

Alternativ können Sie auch erwägen, neue Rollen mit [den erforderlichen Berechtigungen) &#x200B;](/help/access-control/home.md#sandboxes-and-permissions).

[Richten Sie eine neue Rolle ein](/help/access-control/abac/ui/permissions.md) mit den erforderlichen Berechtigungen für wesentliche Playbook-Aufgaben. Erstellen Sie eine Rolle und fügen Sie ihr die neue Sandbox hinzu, wie unten dargestellt.

![Erstellen Sie eine Rolle und fügen Sie sie zur Sandbox hinzu](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Berechtigungen für Playbook-Instanzen**

Im Rahmen von Anwendungsfall-Playbooks erstellen Sie verschiedene Assets wie Schemata, Zielgruppen, Ziele und Journey. Sie und andere Benutzer benötigen die entsprechenden Berechtigungen, um diese Objekte zu erstellen.

**Berechtigungen für Schemata**

Verwenden Sie zum Erstellen und Verwalten von Schemata die Berechtigungen für die Datenmodellierung: **[!UICONTROL Schemata verwalten]**, **[!UICONTROL Schemata anzeigen]**, **[!UICONTROL Beziehungen verwalten]** **[!UICONTROL Identitätsmetadaten verwalten]**

**Berechtigungen für Ziele**

Um Ziele zu erstellen und zu verwalten, verwenden Sie die Berechtigungen Ziele **[!UICONTROL Verwalten]**, **[!UICONTROL Ziele]**, **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Datensatzziel verwalten und aktivieren]**, **[!UICONTROL Zielerstellung]**.

**Berechtigungen für Journey**

Verwenden Sie zum Erstellen und Verwalten von Journey die Berechtigungen der Journey: **[!UICONTROL Journey verwalten]**, **[!UICONTROL Journey anzeigen]**, **[!UICONTROL Journey-Bericht anzeigen]**, **[!UICONTROL Journey verwalten]**, **[!UICONTROL Events]**, **[!UICONTROL Datenquellen und Aktionen]**, **[!UICONTROL Journey anzeigen]**, **[!UICONTROL Events]**, **[!UICONTROL Datenquellen und Aktionen, Publish Journey]**.

Die folgende Abbildung zeigt eine Momentaufnahme der empfohlenen Berechtigungen für Benutzer zum Anzeigen, Erstellen und Verwalten von Playbooks und der von Playbooks generierten Assets.

![Momentaufnahme aller Berechtigungselemente, die zum Erstellen aller Instanzen der Playbooks erforderlich sind](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Benutzer zur Rolle hinzufügen**

Nachdem Sie [neue Rolle erstellt haben](/help/access-control/abac/ui/permissions.md#managing-users-for-role) wie oben beschrieben, fügen Sie sich selbst als Benutzer hinzu. Wenn Sie eine Rolle mit eingeschränktem Zugriff für eine andere Benutzergruppe mit schreibgeschütztem Zugriff erstellen, schließen Sie nur die erforderlichen, mit diesen Berechtigungen verknüpften Anzeigeelemente ein.

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

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Wählen Sie als Nächstes den Kanal, die Plattformen und Apps aus, die Sie in den Kanalkonfigurationen betrachtet haben. Wählen Sie **Senden** aus, um die Oberfläche des Push-Kanals zu erstellen.

Lesen Sie die Dokumentation [Einrichten von Oberflächen für Push-Kanäle](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=de).

## Nächste Schritte {#next-steps}

Nachdem Sie alle Schritte in diesem Dokument ausgeführt haben, sollten Sie eine Entwicklungs-Sandbox mit Playbooks für Anwendungsfälle in der linken Navigation erstellt haben. Jetzt wissen Sie auch, wie Sie Ihren Team-Mitgliedern die erforderlichen Berechtigungen zum Anzeigen und Verwalten von Playbooks und zum Generieren von Assets gewähren. Lesen Sie als nächsten Schritt, wie [&#x200B; das richtige Playbook &#x200B;](/help/use-case-playbooks/playbooks/choose.md) und dann [Instanzen daraus erstellen](/help/use-case-playbooks/playbooks/create-share-reuse.md).
