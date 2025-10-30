---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffskontrolle;attributbasierte Zugriffskontrolle;
title: End-to-End-Handbuch zur attributbasierten Zugriffssteuerung
description: Dieses Dokument enthält eine durchgängige Anleitung zur attributbasierten Zugriffssteuerung in Adobe Experience Platform
role: Developer
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 12%

---

# End-to-End-Handbuch zur attributbasierten Zugriffssteuerung

Verwenden Sie die attributbasierte Zugriffssteuerung auf Adobe Experience Platform, um sich selbst und anderen datenschutzbewussten Kunden mit mehreren Marken mehr Flexibilität bei der Verwaltung des Benutzerzugriffs zu geben. Der Zugriff auf einzelne Objekte, z. B. Schemafelder und Zielgruppen, kann mit Richtlinien gewährt werden, die auf den Attributen und der Rolle des Objekts basieren. Mit dieser Funktion können Sie bestimmten Experience Platform-Benutzenden in Ihrem Unternehmen den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit dieser Funktion können Sie Schemafelder, Zielgruppen usw. mit Bezeichnungen kategorisieren, die Organisations- oder Datennutzungsbereiche definieren. Sie können dieselben Beschriftungen auf Journey, Angebote und andere Objekte in Adobe Journey Optimizer anwenden. Parallel dazu können Admins Zugriffsrichtlinien für XDM-Schemafelder (Experience-Datenmodell) definieren und besser verwalten, welche Benutzenden oder Gruppen (interne, externe oder Drittanbieter-Benutzende) auf diese Felder zugreifen können.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf den Anwendungsfall von Richtlinien zur Zugriffssteuerung. Wenn Sie Richtlinien einrichten möchten, um die **Verwendung** von Daten zu steuern und nicht darauf, welche Experience Platform-Benutzenden Zugriff haben, lesen Sie stattdessen das End-to-End-Handbuch [Data Governance](../../data-governance/e2e.md).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Experience Platform-Komponenten voraus:

* [[!DNL Experience Data Model (XDM)] System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Die Segmentierungsmaschine, die in [!DNL Experience Platform] verwendet wird, um Zielgruppensegmente aus Ihren Kundenprofilen basierend auf Kundenverhalten und -attributen zu erstellen.

### Anwendungsfall - Übersicht

Sie durchlaufen einen beispielhaften attributbasierten Zugriffssteuerungs-Workflow, in dem Sie Rollen, Kennzeichnungen und Richtlinien erstellen und zuweisen, um zu konfigurieren, ob Ihre Benutzer auf bestimmte Ressourcen in Ihrer Organisation zugreifen können oder nicht. In diesem Handbuch wird ein Beispiel für die Einschränkung des Zugriffs auf vertrauliche Daten verwendet, um den Workflow zu demonstrieren. Dieser Anwendungsfall wird unten beschrieben:

Sie sind ein Gesundheitsdienstleister und möchten den Zugriff auf Ressourcen in Ihrer Organisation konfigurieren.

* Ihr internes Marketing-Team sollte auf **[!UICONTROL PHI/ Regulated Health Data]** Daten zugreifen können.
* Ihre externe Agentur sollte nicht in der Lage sein, auf **[!UICONTROL PHI/ Regulated Health Data]** Daten zuzugreifen.

Dazu müssen Sie Rollen, Ressourcen und Richtlinien konfigurieren.

Sie werden:

* [Kennzeichnen der Rollen für Ihre Benutzer](#label-roles): Verwenden Sie das Beispiel eines Gesundheitsdienstleisters (ACME Business Group), dessen Marketing-Gruppe mit externen Agenturen zusammenarbeitet.
* [Beschriften von Ressourcen (Schemafelder und Zielgruppen)](#label-resources): Weisen Sie den **[!UICONTROL PHI/ Regulated Health Data]**-Titel Schemaressourcen und Zielgruppen zu.
* [Aktivieren der Richtlinie, die sie miteinander verknüpft](#policy): Aktivieren Sie die Standardrichtlinie, um den Zugriff auf Schemafelder und Zielgruppen zu verhindern, indem Sie die Kennzeichnungen auf Ihren Ressourcen mit den Kennzeichnungen in Ihrer Rolle verbinden. Benutzende mit entsprechenden Kennzeichnungen erhalten dann Zugriff auf das Schemafeld und das Segment in allen Sandboxes.

## Berechtigungen

[!UICONTROL Permissions] ist der Bereich von Experience Cloud, in dem Admins Benutzerrollen und Richtlinien definieren können, um Berechtigungen für Funktionen und Objekte innerhalb einer Produktanwendung zu verwalten.

Über [!UICONTROL Permissions] können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. [!UICONTROL Permissions] können Sie auch die Bezeichnungen, Sandboxes und Benutzende verwalten, die einer bestimmten Rolle zugeordnet sind.

Wenden Sie sich an Ihren Systemadministrator, um Zugriff zu erhalten, wenn Sie keine Administratorrechte haben.

Sobald Sie über Administratorrechte verfügen, wechseln Sie zu [Adobe Experience Cloud](https://experience.adobe.com/) und melden Sie sich mit Ihren Adobe-Anmeldeinformationen an. Nach der Anmeldung wird die Seite **[!UICONTROL Overview]** für Ihr Unternehmen angezeigt, für das Sie Administratorrechte haben. Auf dieser Seite werden die Produkte angezeigt, die Ihr Unternehmen abonniert hat, sowie andere Steuerelemente zum Hinzufügen von Benutzern und Administratoren zur Organisation. Wählen Sie **[!UICONTROL Permissions]** aus, um den Arbeitsbereich für Ihre Experience Platform-Integration zu öffnen.

![Bild mit dem in Adobe Experience Cloud ausgewählten Berechtigungsprodukt](../images/flac-ui/flac-select-product.png)

Der Arbeitsbereich Berechtigungen für die Experience Platform-Benutzeroberfläche wird auf der Seite **[!UICONTROL Overview]** geöffnet.

## Anwenden von Kennzeichnungen auf eine Rolle {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Was sind Kennzeichnungen?"
>abstract="Mit Kennzeichnungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungs- und Zugrffsrichtlinien kategorisieren. Adobe Experience Platform bietet verschiedene, von Adobe definierte <strong>Kern</strong>-Labels für die Datennutzung, die eine Vielzahl gängiger Einschränkungen für Data Governance abdecken. Mit <strong>S</strong>-Kennzeichnungen (für „sensibel“) wie RHD (Regulated Health Data, regulierte Gesundheitsdaten) können Sie beispielsweise Daten kategorisieren, die sich auf geschützte Gesundheitsinformationen (Protected Health Information, PHI) beziehen. Sie können auch eigene Kennzeichnungen entsprechend den Anforderungen Ihres Unternehmens definieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=de#understanding-data-usage-labels" text="Datennutzungs-Labels – Übersicht"

Rollen sind Möglichkeiten, die Typen von Benutzenden zu kategorisieren, die mit Ihrer Experience Platform-Instanz interagieren, und sind Bausteine von Richtlinien zur Zugriffssteuerung. Eine Rolle verfügt über bestimmte Berechtigungen, und Mitglieder Ihrer Organisation können je nach dem Umfang des Zugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden.

Wählen Sie zunächst im linken Navigationsbereich die Option **[!UICONTROL Roles]** und dann **[!UICONTROL ACME Business Group]** aus.

![Bild, das die ausgewählte ACME-Unternehmensgruppe in den Rollen zeigt](../images/abac-end-to-end-user-guide/abac-select-role.png)

Wählen Sie als Nächstes **[!UICONTROL Labels]** und dann **[!UICONTROL Add Labels]** aus.

![Bild mit der Auswahl von Kennzeichnungen hinzufügen auf der Registerkarte Kennzeichnungen](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Eine Liste aller Kennzeichnungen in Ihrer Organisation wird angezeigt. Wählen Sie **[!UICONTROL RHD]** aus, um den Titel für **[!UICONTROL PHI/Regulated Health Data]** hinzuzufügen, und wählen Sie dann **[!UICONTROL Save]** aus.

![Bild, das die ausgewählte und gespeicherte RHD-Kennzeichnung anzeigt](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Beim Hinzufügen einer Organisationsgruppe zu einer Rolle werden alle Benutzenden in dieser Gruppe zur Rolle hinzugefügt. Alle Änderungen an der Organisationsgruppe (entfernte oder hinzugefügte Benutzer) werden innerhalb der Rolle automatisch aktualisiert.

## Anwenden von Kennzeichnungen auf Schemafelder {#label-resources}

Nachdem Sie nun eine Benutzerrolle mit der [!UICONTROL RHD]-Kennzeichnung konfiguriert haben, müssen Sie dieselbe Kennzeichnung zu den Ressourcen hinzufügen, die Sie für diese Rolle steuern möchten.

Wählen Sie in der oberen Navigation das Symbol **Programmumschalter** aus, dargestellt durch das Symbol ![Programmumschalter](/help/images/icons/apps.png) und klicken Sie dann auf **[!UICONTROL Experience Platform]**.

![Bild mit der Auswahl von Experience Platform aus dem Dropdown-Menü des Programmumschalters](../images/abac-end-to-end-user-guide/abac-select-experience-platform.png)

Wählen Sie in der linken Navigationsleiste die Option **[!UICONTROL Schemas]** und dann in der Liste der angezeigten Schemata die Option **[!UICONTROL ACME Healthcare]** aus.

![Bild, das das ausgewählte ACME-Gesundheitsschema auf der Registerkarte Schemata zeigt](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Wählen Sie als Nächstes **[!UICONTROL Labels]** aus, um eine Liste mit den Feldern anzuzeigen, die mit Ihrem Schema verknüpft sind. Von hier aus können Sie Kennzeichnungen einem oder mehreren Feldern gleichzeitig zuweisen. Wählen Sie die Felder **[!UICONTROL BloodGlucose]** und **[!UICONTROL InsulinLevel]** und dann **[!UICONTROL Apply access and data governance labels]** aus.

![Bild, das die ausgewählten Blutzucker- und Insulin-Spiegel zeigt und die ausgewählten Zugriffs- und Data Governance-Kennzeichnungen anwendet](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

Das Dialogfeld **[!UICONTROL Edit labels]** wird angezeigt, in dem Sie die Kennzeichnungen auswählen können, die Sie auf die Schemafelder anwenden möchten. Wählen Sie für diesen Anwendungsfall die **[!UICONTROL PHI/ Regulated Health Data]** und dann **[!UICONTROL Save]** aus.

![Bild, das die ausgewählte und gespeicherte RHD-Kennzeichnung anzeigt](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Wenn einem Feld eine Kennzeichnung hinzugefügt wird, wird diese Kennzeichnung auf die übergeordnete Ressource dieses Felds angewendet (entweder eine Klasse oder eine Feldergruppe). Wenn die übergeordnete Klasse oder Feldergruppe von anderen Schemata verwendet wird, erben diese Schemata dieselbe Kennzeichnung.

## Anwenden von Kennzeichnungen auf Zielgruppen

>[!NOTE]
>
>Jede Zielgruppe, die ein gekennzeichnetes Attribut verwendet, muss ebenfalls gekennzeichnet werden, wenn dieselben Zugriffsbeschränkungen für sie gelten sollen.

Nachdem Sie die Beschriftung Ihrer Schemafelder abgeschlossen haben, können Sie jetzt mit der Beschriftung Ihrer Zielgruppen beginnen.

Wählen Sie **[!UICONTROL Audiences]** in der linken Navigation unter dem Abschnitt **[!UICONTROL Customers]** aus. Eine Liste der in Ihrer Organisation verfügbaren Zielgruppen wird angezeigt. In diesem Beispiel sind die beiden folgenden Zielgruppen zu kennzeichnen, da sie sensible Gesundheitsdaten enthalten:

* Blutzucker >100
* Insulin &lt; 50

Wählen Sie **[!UICONTROL Blood Glucose >100]** aus (durch den Namen der Zielgruppe, nicht das Kontrollkästchen), um mit der Beschriftung der Zielgruppe zu beginnen.

![Bild, das die Blutzuckerwerte >100 zeigt, die auf der Registerkarte Zielgruppen ausgewählt wurden](../images/abac-end-to-end-user-guide/abac-select-audience.png)

Der Bildschirm **[!UICONTROL Details]** Segmentzuordnung wird angezeigt. Wählen Sie **[!UICONTROL Manage Access]** aus.

![Bild, das die Auswahl von „Zugriff verwalten“ zeigt](../images/abac-end-to-end-user-guide/abac-audience-fields-manage-access.png)

Das Dialogfeld **[!UICONTROL Apply access and data governance labels]** wird angezeigt, in dem Sie die Beschriftungen auswählen können, die Sie auf die Zielgruppe anwenden möchten. Wählen Sie für diesen Anwendungsfall die **[!UICONTROL PHI/ Regulated Health Data]** und dann **[!UICONTROL Save]** aus.

![Bild, das die Auswahl der RHD-Kennzeichnung und des ausgewählten Speichers zeigt](../images/abac-end-to-end-user-guide/abac-select-audience-labels.png)

Wiederholen Sie die obigen Schritte mit **[!UICONTROL Insulin <50]**.

>[!NOTE]
>
> Weisen Sie verschiedenen Objekten in Adobe Journey Optimizer im [!UICONTROL Permissions] Workspace erstellte Beschriftungen (z. B. die Segmentbeschriftungen oben) mithilfe der [Zugriffssteuerung auf Objektebene“ &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/object-based-access).

## Aktivieren der Zugriffssteuerungsrichtlinie {#policy}

Die standardmäßige Zugriffssteuerungsrichtlinie nutzt Kennzeichnungen, um zu definieren, welche Benutzerrollen Zugriff auf bestimmte Experience Platform-Ressourcen haben. In diesem Beispiel wird Benutzenden, die sich nicht in einer Rolle mit den entsprechenden Kennzeichnungen im Schemafeld befinden, der Zugriff auf Schemafelder und Zielgruppen in allen Sandboxes verweigert.

Um die Richtlinie für die Zugriffssteuerung zu aktivieren, wählen Sie in der linken Navigationsleiste [!UICONTROL Permissions] und dann **[!UICONTROL Policies]** aus.

![Liste der angezeigten Richtlinien](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Klicken Sie als Nächstes auf das Auslassungszeichen (`...`) neben dem **[!UICONTROL Default-Field-Level-Access-Control-Policy]**. In einem Dropdown-Menü werden dann Steuerelemente zum Bearbeiten, Aktivieren, Löschen oder Duplizieren der Rolle angezeigt. Wählen Sie **[!UICONTROL Activate]** aus dem Dropdown-Menü aus.

![Dropdown zur Aktivierung der Richtlinie](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Das Dialogfeld Richtlinie aktivieren wird angezeigt, in dem Sie aufgefordert werden, die Aktivierung zu bestätigen. Wählen Sie **[!UICONTROL Confirm]** aus.

![Dialogfeld „Richtlinie aktivieren](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Es wird eine Bestätigung der Richtlinienaktivierung empfangen und Sie werden zur Seite [!UICONTROL Policies] zurückgeleitet.

![Richtlinienbestätigung aktivieren](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Experience Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.
a
To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Experience Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Nächste Schritte

Sie haben die Anwendung von Kennzeichnungen auf eine Rolle, Schemafelder und Zielgruppen abgeschlossen. Die externe Agentur, die diesen Rollen zugewiesen ist, darf diese Beschriftungen und deren Werte nicht in Schema, Datensatz und Profilansicht anzeigen. Diese Felder können auch nicht in der Segmentdefinition verwendet werden, wenn Sie den Segment Builder verwenden.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](./overview.md).

Das folgende Video soll Ihnen dabei helfen, die attributbasierte Zugriffssteuerung zu verstehen, und beschreibt, wie Sie Rollen, Ressourcen und Richtlinien konfigurieren.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
