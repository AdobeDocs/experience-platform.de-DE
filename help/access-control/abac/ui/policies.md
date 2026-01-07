---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung;ABAC
title: Verwalten von Zugriffssteuerungsrichtlinien
description: Verwalten von Zugriffssteuerungsrichtlinien über die Benutzeroberfläche „Berechtigungen“ in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 10%

---

# Verwalten von Zugriffssteuerungsrichtlinien

Zugriffssteuerungsrichtlinien sind Anweisungen, die Attribute zusammenführen, um zulässige und unzulässige Aktionen festzulegen. Adobe bietet eine Standardrichtlinie, die sofort oder aktiviert werden kann, wenn Ihr Unternehmen bereit ist, den Zugriff auf bestimmte Objekte anhand von [Kennzeichnungen](./labels.md){target="_blank"} zu steuern. Die Standardrichtlinie **[!UICONTROL Default-Label-Based-Access-Control-Policy]** nutzt Kennzeichnungen, die auf Ressourcen angewendet werden, um den Zugriff zu verweigern, es sei denn, Benutzer befinden sich in einer Rolle mit einer entsprechenden Kennzeichnung.

>[!IMPORTANT]
>
>Zugriffssteuerungsrichtlinien sollten nicht mit Datennutzungsrichtlinien verwechselt werden, die steuern, wie Daten in Adobe Experience Platform verwendet werden. Weitere Informationen finden Sie im Handbuch [&#x200B; Erstellen &#x200B;](../../../data-governance/policies/create.md){target="_blank"} Datennutzungsrichtlinien .

## Konfigurieren von Sandboxes für eine Richtlinie {#configure-policy}

Richtlinien werden auf Sandbox-Ebene angewendet, um zu steuern, welche Sandboxes eine beschriftungsbasierte Zugriffssteuerung erzwingen. Standardmäßig ist die **[!UICONTROL Auto-include]**-Funktion aktiviert, d. h. alle aktuellen und zukünftigen Sandboxes werden automatisch zur Richtlinie hinzugefügt. Wenn **[!UICONTROL Auto-include]** deaktiviert ist, unterliegen nur die Sandboxes, die Sie manuell hinzufügen, den Zugriffssteuerungsregeln der Richtlinie.

>[!NOTE]
>
>Die **[!UICONTROL Default-Label-Based-Access-Control-Policy]** ist derzeit die einzige zur Konfiguration verfügbare Richtlinie.

Um mit der Konfiguration der Sandboxes einer Richtlinie zu beginnen, navigieren Sie zu **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Wählen Sie **[!UICONTROL Policies]** im linken Bereich und dann den **[!UICONTROL Default-Label-Based-Access-Control-Policy]** aus der Liste aus.

![Der Arbeitsbereich Richtlinien mit einer Liste vorhandener Richtlinien.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Der Arbeitsbereich Details der Richtlinie wird angezeigt. Wählen Sie die Registerkarte **[!UICONTROL Sandboxes]** aus, um die Liste der mit der Richtlinie verknüpften Sandboxes anzuzeigen und auf die Sandbox-Konfigurationsoptionen zuzugreifen.

![Der Sandbox-Arbeitsbereich der Richtlinie zeigt eine Liste der zugehörigen Sandboxes.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Automatisches Einschließen verwalten {#manage-auto-include}

>[!IMPORTANT]
>
>Standardmäßig ist **[!UICONTROL Auto-include]** aktiviert, d. h. alle aktuellen und zukünftigen Sandboxes werden automatisch zur Richtlinie hinzugefügt.

Um zu steuern, welche Sandboxes in einer Richtlinie enthalten sind, können Sie die **[!UICONTROL Auto-include]**-Funktion ein- oder ausschalten. Wenn Sie **[!UICONTROL Auto-include]** deaktivieren, werden zukünftige Sandboxes nicht automatisch zur Richtlinie hinzugefügt. Durch Deaktivieren der Funktion **werden jedoch** Sandboxes entfernt, die bereits in der Richtlinie enthalten sind.

![Die Sandbox-Registerkarte der Richtlinie mit dem hervorgehobenen Umschalter „Automatisch einschließen“ und im Status „Aus“.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Um **[!UICONTROL Auto-include]** wieder zu aktivieren, schalten Sie sie mit dem Umschalter wieder ein. Das Dialogfeld **[!UICONTROL Enable Auto-include]** wird angezeigt und Sie werden aufgefordert, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Enable]** aus, um die Konfigurationseinstellung abzuschließen.

>[!NOTE]
>
>Wenn Sie **[!UICONTROL Auto-include]** erneut aktivieren, werden alle Sandboxes, die Sie zuvor aus der Richtlinie entfernt haben, erneut hinzugefügt.

![Das Dialogfeld „Automatisches Einschließen aktivieren“ mit hervorgehobener Option „Aktivieren“.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Manuelles Verwalten von Sandboxes {#manually-manage-sandboxes}

Wenn **[!UICONTROL Auto-include]** deaktiviert ist, können Sie bestimmte Sandboxes manuell zur Richtlinie hinzufügen oder daraus entfernen. Dadurch erhalten Sie eine genaue Kontrolle darüber, welche Sandboxes die Zugriffssteuerungsregeln der Richtlinie durchsetzen.

>[!NOTE]
>
>Um Sandboxes manuell hinzuzufügen oder zu entfernen, muss der **[!UICONTROL Auto-include]** Umschalter **muss** deaktiviert sein.

**So fügen Sie Sandboxes hinzu:**

Wählen Sie **[!UICONTROL Add Sandboxes]** aus dem Sandbox-Arbeitsbereich der Richtlinie aus.

![Der Arbeitsbereich der Richtlinie mit der hervorgehobenen Option „Sandboxes hinzufügen“.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Das Dialogfeld **[!UICONTROL Add Sandboxes]** wird mit Ihrer Bibliothek verfügbarer Sandboxes angezeigt. Wählen Sie die Sandbox(es) aus, die Sie der Richtlinie hinzufügen möchten, und klicken Sie dann auf **[!UICONTROL Save]**.

![Das Dialogfeld „Sandboxes hinzufügen“ mit einer ausgewählten Sandbox und der hervorgehobenen Option „Speichern“.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Wenn alle verfügbaren Sandboxes bereits in der Richtlinie enthalten sind, wird im Dialogfeld die Meldung „Sie haben nichts in Ihrer Bibliothek“ angezeigt.

**So entfernen Sie Sandboxes:**

Suchen Sie die Sandbox, die Sie aus der Liste entfernen möchten, und wählen Sie das Symbol **X** neben dem Namen aus.

![Die Sandbox-Liste der Richtlinie mit einem hervorgehobenen „x“, um eine Sandbox zu entfernen.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Ein Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Confirm]** aus, um das Entfernen der Sandbox aus der Richtlinie abzuschließen.

![Das Bestätigungsdialogfeld einer Sandbox mit hervorgehobener Option „Bestätigen“.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Aktivieren von Richtlinien {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Was sind Richtlinien?"
>abstract="Richtlinien sind Anweisungen, die Attribute zusammenbringen, um zulässige und unzulässige Aktionen festzustellen. Jede Organisation verfügt über eine Standardrichtlinie, die Sie aktivieren müssen, um den Zugriff auf bestimmte Objekte anhand von Kennzeichnungen zu steuern. Auf Ressourcen angewendete Kennzeichnungen verweigern den Zugriff, es sei denn, Benutzende werden einer Rolle mit einer entsprechenden Kennzeichnung zugewiesen. Richtlinien können nicht bearbeitet oder gelöscht werden, sie können jedoch aktiviert oder deaktiviert werden."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Verwalten von Labels"

Um eine vorhandene Richtlinie zu aktivieren, wählen Sie die Richtlinie auf der Registerkarte **[!UICONTROL Policies]** in **[!UICONTROL Permissions]** aus. Der Aktivierungsstatus der Richtlinie wird im Abschnitt **[!UICONTROL Status]** angezeigt.

![Der Arbeitsbereich „Richtlinien“ mit hervorgehobenem Status einer Richtlinie.](../../images/ui/policies/policy-status.png){zoomable="yes"}

Der Arbeitsbereich Details der Richtlinie wird angezeigt. Wählen Sie **[!UICONTROL Activate]** aus.

![Der Arbeitsbereich mit den Details der Richtlinie, wobei die Option „Aktivieren“ hervorgehoben ist.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

Das Dialogfeld **[!UICONTROL Activate Policy]** wird angezeigt. Wählen Sie **[!UICONTROL Confirm]** aus, um die Aktivierung der Richtlinie abzuschließen.

![Das Dialogfeld „Richtlinie aktivieren“ mit hervorgehobener Option „Bestätigen“.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Nächste Schritte

Wenn eine Richtlinie aktiviert ist, können Sie mit dem nächsten Schritt fortfahren, um [Berechtigungen für eine Rolle verwalten](permissions.md).
