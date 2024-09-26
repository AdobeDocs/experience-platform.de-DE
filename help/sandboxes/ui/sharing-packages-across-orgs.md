---
title: Freigeben von Paketen in der gesamten Organisation mithilfe von Sandbox Tooling
description: Erfahren Sie, wie Sie mit Sandbox Tooling in Adobe Experience Platform Pakete unternehmensübergreifend freigeben können.
badge: Beta
source-git-commit: 492f1d9dc08965dba3f1c5b6e1d479ef645afd04
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---

# Freigeben von Paketen in Unternehmen mithilfe von Sandbox Tooling

>[!NOTE]
>
>Die organisationsübergreifende Freigabe von Paketen befindet sich derzeit in der Beta-Phase und steht nur ausgewählten Beta-Kunden zur Verfügung.

In diesem Dokument wird beschrieben, wie Sie Sandbox-Tools in Adobe Experience Platform verwenden, um Pakete unternehmensübergreifend freizugeben.

Dank der Sandbox-Tool-Funktion können Sie die Konfigurationsgenauigkeit über Sandboxes hinweg verbessern und Sandbox-Konfigurationen zwischen Sandboxes nahtlos exportieren und importieren. Es gibt zwei Typen von freigegebenen Paketen:

**Privates Paket**

Private Pakete können nur für Organisationen freigegeben werden, die die Freigabeanfrage von der Quellorganisation über eine Opt-in-Zulassungsliste genehmigt haben.

**Öffentliches Paket**

Öffentliche Packages können ohne zusätzliche Validierung importiert werden. Diese Pakete können auf der Website, dem Blog oder der Plattform eines Partners freigegeben werden. Mit der Paket-Payload können Pakete kopiert und aus diesen Kanälen in die Zielorganisation eingefügt werden.

## Private Pakete

>[!NOTE]
>
>Um eine Freigabeanforderung zu starten und zu genehmigen und Pakete unternehmensübergreifend freizugeben, benötigen Sie die rollenbasierte Zugriffssteuerungsberechtigung **package-share** .

Die Sandbox-Tool-Funktion bietet Ihnen die Möglichkeit, Unternehmenspartnerschaften zu erstellen, den Status einer Partneranfrage zu verfolgen, bestehende Partnerschaften zu verwalten und Pakete mit Partnerorganisationen zu teilen.

### Erstellen einer Partnerschaft für eine Organisation

Navigieren Sie zum Erstellen einer Anforderung für eine Partnerschaft innerhalb der Organisation zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Partner-Organisationen]** . Wählen Sie dann **[!UICONTROL Partnerorganisationen verwalten]** aus.

![Die Sandbox-Benutzeroberfläche, wobei die Registerkarte &quot;Partner-Organisationen&quot;und &quot;Partnerorganisationen verwalten&quot;hervorgehoben sind.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Geben Sie im Dialogfeld [!UICONTROL Package Partner Management] die Organisations-ID in **[!UICONTROL Enter Org ID]** ein und drücken Sie die Eingabetaste. Die Organisations-ID wird im Abschnitt **[!UICONTROL Ausgewählte Organisations-IDs]** unten angezeigt. Wählen Sie nach dem Hinzufügen der IDs **[!UICONTROL Bestätigen]** aus.

>[!TIP]
>
>Sie können mehrere Organisations-IDs gleichzeitig mithilfe kommagetrennter Listen oder durch Eingabe jeder Organisations-ID und anschließender Eingabe eingeben.

![Das Dialogfeld &quot;Partner-Paketorganisation&quot;mit der Option &quot;Organisations-ID eingeben&quot;, &quot;Ausgewählte Organisations-IDs&quot;und &quot;Bestätigen&quot;wurde hervorgehoben.](../images/ui/sandbox-tooling/private-enter-org-id.png)

Die Freigabeanforderung wurde erfolgreich an die Partnerorganisation gesendet und Sie werden zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Partner-Organisationen]** zurückgeleitet, auf der die **[!UICONTROL Ausgehende Anforderung]** angezeigt wird.

![Die Registerkarte Partner-Organisationen mit hervorgehobener ausgehender Anfrage.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Partnerschaftserfordernis genehmigen

Navigieren Sie zum Autorisieren einer Partneranfrage für eine Organisation zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Partner-Organisationen]** . Wählen Sie als Nächstes **[!UICONTROL Eingehende Anforderung]** aus.

![Die Sandbox-Benutzeroberfläche mit der Registerkarte &quot;Partner-Organisationen&quot;und der eingehenden Anforderung hervorgehoben.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Der aktuelle **[!UICONTROL Status]** für die Anfrage lautet **Ausstehend**. Um die Anforderung zu genehmigen, wählen Sie die Auslassungszeichen (`...`) neben der ausgewählten Anforderung aus und wählen Sie dann **[!UICONTROL Genehmigen]** aus der Dropdown-Liste aus.

![Liste der eingehenden Anforderungen, die das Dropdown-Menü mit hervorgehobener Genehmigung anzeigen.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Das Dialogfeld **[!UICONTROL Anfrage zur Partnerorg überprüfen]** enthält Details zur Anforderung der Unternehmenspartnerschaft. Geben Sie einen [!UICONTROL Grund] für die Genehmigung ein und wählen Sie dann **[!UICONTROL Genehmigen]** aus.

![Überprüfen Sie das Dialogfeld für die Anforderung der Partner-Organisation mit Grund und Genehmigen hervorgehoben.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Sie werden zur Seite [!UICONTROL Eingehende Anfrage] zurückgeleitet und der Status der Anfrage wurde auf **[!UICONTROL Genehmigt]** aktualisiert.

![ Liste der eingehenden Anforderungen mit hervorgehobener Genehmigt.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Sie können jetzt Pakete zwischen Ihrer Organisation und der Quellorganisation freigeben.

### Freigeben von Paketen für Partnerorganisationen

>[!NOTE]
>
>Es können nur Pakete mit dem Status **Veröffentlicht** freigegeben werden.

Um ein Paket für eine genehmigte Partnerorganisation freizugeben, navigieren Sie zur Registerkarte [!UICONTROL Sandboxes] **[!UICONTROL Pakete]** . Wählen Sie als Nächstes das Auslassungszeichen (`...`) neben dem Paket und dann **[!UICONTROL Paket freigeben]** aus dem Dropdown-Menü aus.

![Liste der Pakete, die das Dropdown-Menü mit hervorgehobenem Freigabepaket anzeigen.](../images/ui/sandbox-tooling/private-share-package.png)

Wählen Sie im Dialogfeld **[!UICONTROL Package freigeben]** das freizugebende Paket aus der Dropdown-Liste **[!UICONTROL Freigabeeinstellungen]** und dann **[!UICONTROL Bestätigen]** aus.

![Geben Sie das Dialogfeld &quot;Package freigeben&quot;mit den Freigabeeinstellungen frei und bestätigen Sie die Markierung.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

>[!TIP]
>
>Es ist möglich, mehrere Organisationen auszuwählen. Ausgewählte Organisationen werden unter dem Dropdown-Menü [!UICONTROL Freigabeeinstellungen] angezeigt.

## Nächste Schritte

In diesem Dokument erfahren Sie, wie Sie mit der Sandbox-Tool-Funktion Pakete unternehmensübergreifend freigeben können. Weitere Informationen finden Sie im [Sandbox-Tool-Handbuch](../ui/sandbox-tooling.md).

Anweisungen zum Ausführen verschiedener Vorgänge mit der Sandbox-API finden Sie im [Sandbox-Entwicklerhandbuch](../api/getting-started.md). Eine allgemeine Übersicht über Sandboxes im Experience Platform finden Sie in der [Übersichtsdokumentation](../home.md).
