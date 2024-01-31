---
solution: Experience Platform
title: Erste Schritte
description: Erfahren Sie, wie Sie die ersten Schritte mit der Funktion „Playbooks für Anwendungsfälle“ ausführen.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 15%

---


# Erste Schritte

Erfahren Sie, wie Sie Ihr Konto für Anwendungsfall-Playbooks einrichten, die für Real-time Customer Data Platform und Adobe Journey Optimizer entwickelt wurden. Die drei Hauptkonfigurationsschritte sind:

* Sandbox erstellen
* Benutzerberechtigungen konfigurieren
* Konfigurieren der Journey Optimizer-Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen (falls Sie vorhaben, Journey Optimizer-Playbooks zu verwenden)

## Anwendungsbeispiele konfigurieren - Videoeinführung {#video}

In diesem Video erfahren Sie, wie Sie Ihre Sandbox erstellen, Berechtigungen konfigurieren und Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen in Journey Optimizer konfigurieren.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Erstellen einer Entwicklungs-Sandbox {#create-development-sandbox}

Anwendungsfall-Playbooks verwenden eine spezielle Entwicklungs-Sandbox. Zum Ausführen der ersten Schritte und Zugreifen auf die Funktion [[!UICONTROL Playbooks für Anwendungsfälle]](/help/use-case-playbooks/playbooks/overview.md) [erstellen Sie eine neue Entwicklungs-Sandbox](/help/sandboxes/ui/user-guide.md#create) (keine Produktions-Sandbox auswählen!), deren Namen (nicht deren Titel) entweder `-ucp` oder `-UCP` im Suffix enthält, wie unten dargestellt.

![Erstellen einer Entwicklungs-Sandbox für Playbooks für Anwendungsfälle](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Sie sollten jetzt [!UICONTROL Playbooks] in der linken Leiste unter [!UICONTROL Anwendungsbeispiele für Playbooks].

![Verwenden der Option „Playbooks für Anwendungsfälle“ in der Benutzeroberfläche nach dem Erstellen einer Sandbox.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Wenn [!UICONTROL Playbooks] nicht wie oben gezeigt in der linken Leiste zu sehen ist, verwenden Sie diesen Link `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`, um direkt dorthin zu navigieren. Im Link ist `<YOUR_ORG>` der Name Ihres Unternehmens und `<YOUR_SANDBOX_NAME>` der Name der von Ihnen erstellten Entwicklungs-Sandbox.

## Erteilen der erforderlichen Zugriffsberechtigungen für Ihr Team {#grant-access-permissions}

Erste Schritte mit [!UICONTROL Anwendungsbeispiele für Playbooks]benötigen Mitglieder Ihres Marketing-Teams die richtigen Berechtigungen, damit sie die Liste der erstellten Playbooks ansehen oder selbst Playbooks erstellen können.

**Erforderliche Berechtigungen**

Um die erforderlichen Berechtigungen hinzuzufügen, fügen Sie in der Benutzeroberfläche &quot;Berechtigungen&quot;die neue Sandbox für die Anwendungsfallwiedergabe in [bereits konfigurierte Rollen](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), einschließlich derjenigen, die für andere Entwicklungs-Sandboxes verwendet werden.

![Playbook-Sandbox für bereits konfigurierte Rollen](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Richten Sie eine Rolle für Playbooks ein:**

Alternativ können Sie auch neue Rollen mit [die erforderlichen Berechtigungen](/help/access-control/home.md#sandboxes-and-permissions).

[Einrichten einer neuen Rolle](/help/access-control/abac/ui/permissions.md) mit den erforderlichen Berechtigungen für wichtige Aufgaben des Playbooks. Erstellen Sie eine Rolle und fügen Sie ihr die neue Sandbox hinzu, wie unten dargestellt.

![Erstellen einer Rolle und Hinzufügen zur Sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Berechtigungen für Playbook-Instanzen**

Im Rahmen von &quot;Anwendungsfall-Playbooks&quot;erstellen Sie verschiedene Assets wie Schemas, Zielgruppen, Ziele und Journey. Sie und andere Benutzer benötigen die richtigen Berechtigungen, um diese Objekte zu erstellen.

**Berechtigungen für Schemata**

Verwenden Sie zum Erstellen und Verwalten von Schemas die Datenmodellierungsberechtigungen . **[!UICONTROL Verwalten von Schemas]**, **[!UICONTROL Anzeigen von Schemas]**, **[!UICONTROL Beziehungen verwalten]**, **[!UICONTROL Verwalten von Identitätsmetadaten]**

**Berechtigungen für Ziele**

Verwenden Sie zum Erstellen und Verwalten von Zielen die Berechtigungen Ziele . **[!UICONTROL Verwalten]**, **[!UICONTROL Ziele]**, **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL DataSet-Ziel verwalten und aktivieren]**, **[!UICONTROL Destination Authoring]**.

**Berechtigungen für Journey**

Verwenden Sie zum Erstellen und Verwalten von Journey die Berechtigungen &quot;Journey&quot;. **[!UICONTROL Verwalten von Journey]**, **[!UICONTROL Journey anzeigen]**, **[!UICONTROL Bericht &quot;Journey anzeigen&quot;]**, **[!UICONTROL Verwalten von Journey]**, **[!UICONTROL Veranstaltungen]**, **[!UICONTROL Data Sources und Aktionen]**, **[!UICONTROL Journey anzeigen]**, **[!UICONTROL Veranstaltungen]**, **[!UICONTROL Data Sources und Aktionen, Journey veröffentlichen]**.

Das folgende Bild zeigt eine Momentaufnahme der empfohlenen Berechtigungen für Benutzer zum Anzeigen, Erstellen und Verwalten von Playbooks und der von Playbooks generierten Assets.

![Momentaufnahme aller Berechtigungselemente, die zum Erstellen aller Instanzen der Playbooks erforderlich sind](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Benutzer zur Rolle hinzufügen**

Sobald du [eine neue Rolle erstellt](/help/access-control/abac/ui/permissions.md#managing-users-for-role) wie oben beschrieben, fügen Sie sich selbst als Benutzer hinzu. Wenn Sie eine Rolle mit eingeschränktem Zugriff für andere Benutzer mit schreibgeschütztem Zugriff erstellen, schließen Sie nur die erforderlichen Ansichtselemente ein, die mit diesen Berechtigungen verknüpft sind.

## Konfigurieren von Sandbox- und Kanaloberflächen in Journey Optimizer {#configure-channel-surfaces}

Wenn Ihr Unternehmen für [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de)und Sie die für Journey Optimizer entworfenen Playbooks verwenden möchten, müssen Sie die Kanalvorgaben in Ihrer Sandbox konfigurieren, die die für Ihre Nachrichten erforderlichen technischen Parameter definieren. [Erfahren Sie, wie Sie in Adobe Journey Optimizer Kanaloberflächen einrichten.](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=de).

Um in Journey Optimizer Playbooks zu erstellen, müssen Sie Kanaloberflächen für E-Mail-, Push- und SMS-Benachrichtigungen konfigurieren.

### E-Mail-Kanaloberfläche

Navigieren Sie zu `Channels` in der Journey Optimizer-Benutzeroberfläche. Konfigurieren Sie separate Subdomains und IP-Pools für Marketing-E-Mails und Transaktionsnachrichten, falls noch nicht konfiguriert. Dies sind Best Practices, um sicherzustellen, dass Transaktionsnachrichten wie Auftragsbestätigungs-E-Mails an Ihre Kunden weitergeleitet werden. Geben Sie Namen, E-Mail-Adressen und zusätzliche Einstellungen ein. Auswählen **Einsenden** oben rechts auf der Seite, um die Oberfläche des Marketing-Kanals zu erstellen. Lesen Sie die Dokumentation unter [Einrichten von E-Mail-Kanal-Oberflächen](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-Kanaloberfläche

Um eine SMS-Kanaloberfläche zu erstellen, erstellen Sie zunächst eine SMS-API-Berechtigung und wählen Sie den gewünschten Anbieter aus (z. B. Sinch). Benennen Sie die SMS-Kanaloberfläche (z. B. SMS Marketing), wählen Sie die Konfiguration aus und geben Sie eine Absendernummer ein. Auswählen **Einsenden** oben rechts auf der Seite, um die Oberfläche des SMS-Kanals zu speichern. Lesen Sie die Dokumentation unter [Einrichten der Oberflächen von SMS-Kanälen](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms).

Konfigurieren Sie außerdem Kanäle für Playbooks, die Transaktionsnachrichten wie Bestellbestätigungen enthalten.

### Push-Kanaloberfläche

Vergewissern Sie sich, dass die App über die Experience Platform- oder Datenerfassungs-Benutzeroberfläche konfiguriert ist. So sehen App-Oberflächen in der Umgebung &quot;Datenerfassungen&quot;aus.

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Wählen Sie anschließend den Kanal, die Plattformen und Apps aus, die Sie in den Konfigurationen der App-Oberfläche angesehen haben. Auswählen **Einsenden** , um die Push-Kanaloberfläche zu erstellen.

Lesen Sie die Dokumentation unter [Einrichten von Push-Kanal-Oberflächen](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Nächste Schritte {#next-steps}

Nachdem Sie alle Schritte in diesem Dokument ausgeführt haben, sollten Sie eine Entwicklungs-Sandbox mit &quot;Anwendungsfall-Playbooks&quot;erstellt haben, die im linken Navigationsbereich verfügbar sind. Sie wissen jetzt auch, wie Sie Ihren Teammitgliedern die erforderlichen Berechtigungen zum Anzeigen und Verwalten von Playbooks und zum Generieren von Assets gewähren. Lesen Sie als nächsten Schritt, wie Sie [Entdecken Sie das richtige Playbook](/help/use-case-playbooks/playbooks/discover.md) für Sie und dann [Instanzen daraus erstellen](/help/use-case-playbooks/playbooks/create-share-reuse.md).