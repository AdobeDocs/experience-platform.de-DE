---
keywords: Experience Platform; Startseite; beliebte Themen; Zugriffskontrolle; attributbasierte Zugriffskontrolle;
title: Anleitung zur attributbasierten Zugriffssteuerung (End-to-End)
description: Dieses Dokument bietet eine durchgängige Anleitung zur attributbasierten Zugriffskontrolle in Adobe Experience Platform
source-git-commit: 0035f4611f2c269bb36f045c3c57e6e7bad7c013
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 5%

---

# Handbuch zur attributbasierten Zugriffskontrolle von Ende zu Ende

Die attributbasierte Zugriffskontrolle ist eine Funktion von Adobe Experience Platform, die es Kunden mit mehreren Marken und datenschutzbewussten Kunden ermöglicht, den Benutzerzugriff flexibler zu verwalten. Der Zugriff auf einzelne Objekte wie Schemafelder und Segmente kann mit Richtlinien gewährt/verweigert werden, die auf den Attributen und der Rolle des Objekts basieren. Mit dieser Funktion können Sie bestimmten Platform-Benutzern in Ihrer Organisation Zugriff auf einzelne Objekte gewähren oder sperren.

Mit dieser Funktion können Sie Schemafelder, Segmente usw. mit Bezeichnungen kategorisieren, die Organisations- oder Datennutzungsbereiche definieren. Sie können diese Beschriftungen auf Journey, Angebote und andere Objekte in Adobe Journey Optimizer anwenden. Parallel dazu können Administratoren Zugriffsrichtlinien für XDM-Schemafelder definieren und besser verwalten, welche Benutzer oder Gruppen (interne, externe oder Drittanbieter-Benutzer) auf diese Felder zugreifen können.


## Erste Schritte

Für dieses Tutorial werden Kenntnisse der folgenden Platform-Komponenten benötigt:

* [[!DNL Experience Data Model (XDM)] System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Die Segmentierungsmaschine, die in [!DNL Platform] verwendet wird, um Zielgruppensegmente aus Ihren Kundenprofilen basierend auf Kundenverhalten und -attributen zu erstellen.

### Anwendungsfallübersicht

Im Folgenden wird ein Beispiel für einen attribut-basierten Zugriffssteuerungs-Workflow beschrieben, in dem Sie Rollen, Titel und Richtlinien erstellen und zuweisen, um zu konfigurieren, ob Ihre Benutzer auf bestimmte Ressourcen in Ihrer Organisation zugreifen können oder nicht. In diesem Handbuch wird ein Beispiel für die Beschränkung des Zugriffs auf vertrauliche Daten zur Veranschaulichung des Workflows verwendet. Dieser Anwendungsfall wird nachfolgend beschrieben:

Sie sind Gesundheitsdienstleister und möchten den Zugriff auf Ressourcen in Ihrem Unternehmen konfigurieren.

* Ihr internes Marketing-Team sollte auf **[!UICONTROL PHI/Reguläre Gesundheitsdaten]** Daten.
* Ihre externe Agentur sollte nicht in der Lage sein, auf **[!UICONTROL PHI/Reguläre Gesundheitsdaten]** Daten.

Dazu müssen Sie Rollen, Ressourcen und Richtlinien konfigurieren.

Sie werden:

* [Rollen für Ihre Benutzer beschriften](#label-roles): Verwenden Sie das Beispiel eines Gesundheitsdienstleisters (ACME Business Group), dessen Marketinggruppe mit externen Agenturen zusammenarbeitet.
* [Ressourcen beschriften (Schemafelder und Segmente)](#label-resources): Zuweisen der **[!UICONTROL PHI/Reguläre Gesundheitsdaten]** -Beschriftung für Schemaressourcen und -segmente.
* [Erstellen Sie die Richtlinie, die sie miteinander verknüpft](#policy): Erstellen Sie eine Richtlinie, um die Beschriftungen in Ihren Ressourcen mit den Beschriftungen in Ihrer Rolle zu verknüpfen und den Zugriff auf Schemafelder und Segmente zu verweigern. Dadurch wird Benutzern ohne übereinstimmende Beschriftungen der Zugriff auf das Schemafeld und das Segment in allen Sandboxes verweigert.

## Berechtigungen

[!UICONTROL Berechtigungen] ist der Bereich des Experience Cloud, in dem Administratoren Benutzerrollen und Richtlinien definieren können, um Berechtigungen für Funktionen und Objekte in einer Produktanwendung zu verwalten.

bis [!UICONTROL Berechtigungen]können Sie Rollen erstellen und verwalten und die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. [!UICONTROL Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzer*innen verwalten, die einer bestimmten Rolle zugeordnet sind.]

Wenden Sie sich an Ihren Systemadministrator, um Zugriff zu erhalten, wenn Sie nicht über Administratorberechtigungen verfügen.

Sobald Sie über Administratorberechtigungen verfügen, wechseln Sie zu [Adobe Experience Cloud](https://experience.adobe.com/) und melden Sie sich mit Ihren Adobe-Anmeldedaten an. Nach der Anmeldung muss die **[!UICONTROL Übersicht]** für Ihre Organisation angezeigt, für die Sie Administratorrechte haben. Auf dieser Seite werden die Produkte angezeigt, für die sich Ihr Unternehmen angemeldet hat, sowie weitere Steuerelemente zum Hinzufügen von Benutzern und Administratoren zur Organisation. Auswählen **[!UICONTROL Berechtigungen]** , um den Arbeitsbereich für Ihre Platform-Integration zu öffnen.

![Bild mit dem ausgewählten Berechtigungsprodukt in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Der Arbeitsbereich &quot;Berechtigungen&quot;für die Platform-Benutzeroberfläche wird angezeigt und öffnet sich im **[!UICONTROL Rollen]** Seite.

## Anwenden von Beschriftungen auf eine Rolle {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Was sind Beschriftungen?"
>abstract="Mit Beschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Platform bietet verschiedene Adobe-definierte &quot;Core&quot;-Datennutzungsbezeichnungen, die eine Vielzahl gemeinsamer Einschränkungen für Data Governance abdecken. Mit vertraulichen S-Beschriftungen wie RHD (Regulated Health Data) können Sie beispielsweise Daten kategorisieren, die auf geschützte Gesundheitsinformationen (PHI) verweisen. Sie können auch eigene benutzerdefinierte Beschriftungen definieren, die den Anforderungen Ihres Unternehmens entsprechen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Datennutzungsbeschriftungen – Übersicht"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Neue Bezeichnung erstellen"
>abstract="Sie können eigene benutzerdefinierte Beschriftungen erstellen, die den Anforderungen Ihres Unternehmens entsprechen. Benutzerdefinierte Beschriftungen können verwendet werden, um sowohl Data Governance- als auch Zugriffssteuerungskonfigurationen auf Ihre Daten anzuwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Verwalten von benutzerdefinierten Kennzeichnungen"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Welche Rollen gibt es?"
>abstract="Rollen sind Möglichkeiten, die Typen von Benutzern zu kategorisieren, die mit Ihrer Platform-Instanz interagieren und Bausteine von Richtlinien zur Zugriffssteuerung sind. Eine Rolle verfügt über bestimmte Berechtigungen und Mitglieder Ihrer Organisation können je nach dem Umfang der Ansicht oder des Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Rollen verwalten"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Neue Rolle erstellen"
>abstract="Sie können eine neue Rolle erstellen, um Benutzer, die auf Ihre Platform-Instanz zugreifen, besser zu kategorisieren. Sie können beispielsweise eine Rolle für ein internes Marketing-Team erstellen und die RHD-Bezeichnung auf diese Rolle anwenden, sodass Ihr internes Marketing-Team auf geschützte Gesundheitsinformationen (PHI) zugreifen kann. Alternativ können Sie auch eine Rolle für eine externe Agentur erstellen und diesen Rollenzugriff auf PHI-Daten verweigern, indem Sie die RHD-Beschriftung nicht auf diese Rolle anwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Erstellen Sie eine neue Rolle"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Rollenübersicht"
>abstract="Im Dialogfeld Rollenübersicht werden die Ressourcen und Sandboxes angezeigt, auf die eine bestimmte Rolle zugreifen darf."

Rollen dienen der Kategorisierung der Arten von Benutzern, die mit Ihrer Platform-Instanz interagieren, und bilden Bausteine von Richtlinien zur Zugriffssteuerung. Eine Rolle verfügt über bestimmte Berechtigungen und Mitglieder Ihrer Organisation können je nach Umfang des benötigten Zugriffs einer oder mehreren Rollen zugewiesen werden.

Wählen Sie zunächst **[!UICONTROL ACME Business Group]** aus dem **[!UICONTROL Rollen]** Seite.

![Bild, das die in Rollen ausgewählte ACME-Geschäftsrolle anzeigt](../images/abac-end-to-end-user-guide/abac-select-role.png)

Wählen Sie als Nächstes **[!UICONTROL Bezeichnungen]** und wählen Sie **[!UICONTROL Hinzufügen von Bezeichnungen]**.

![Bild mit Auswahl von Beschriftungen hinzufügen auf der Registerkarte &quot;Beschriftungen&quot;](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Eine Liste aller Beschriftungen in Ihrer Organisation wird angezeigt. Auswählen **[!UICONTROL RHD]** , um die Bezeichnung für **[!UICONTROL PHI/Reglementierte Gesundheitsdaten]**. Lassen Sie einige Augenblicke zu, bis ein blaues Häkchen neben der Beschriftung angezeigt wird, und wählen Sie dann **[!UICONTROL Speichern]**.

![Bild mit der ausgewählten und gespeicherten RHD-Beschriftung](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Beim Hinzufügen einer Organisationsgruppe zu einer Rolle werden alle Benutzer dieser Gruppe zur Rolle hinzugefügt. Änderungen an der Organisationsgruppe (Benutzer werden entfernt oder hinzugefügt) werden automatisch in der Rolle aktualisiert.

## Anwenden von Bezeichnungen auf Schemafelder {#label-resources}

Sie haben jetzt eine Benutzerrolle mit der [!UICONTROL RHD] -Beschriftung verwenden, besteht der nächste Schritt darin, denselben Titel zu den Ressourcen hinzuzufügen, die Sie für diese Rolle steuern möchten.

Auswählen **[!UICONTROL Schemas]** aus der linken Navigation und wählen Sie dann **[!UICONTROL ACME Gesundheitsfürsorge]** aus der Liste der angezeigten Schemas.

![Bild, das das im Tab Schemas ausgewählte ACME-Schema für die Gesundheitsfürsorge anzeigt](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Wählen Sie als Nächstes **[!UICONTROL Bezeichnungen]** um eine Liste anzuzeigen, die die mit Ihrem Schema verknüpften Felder anzeigt. Von hier aus können Sie einem oder mehreren Feldern gleichzeitig Beschriftungen zuweisen. Wählen Sie die **[!UICONTROL BloodGlucose]** und **[!UICONTROL InsulinLevel]** und wählen Sie **[!UICONTROL Anwenden von Zugriffs- und Data Governance-Beschriftungen]**.

![Bild, das die ausgewählten Blutzuckerbezeichnungen und InsulinLevel anzeigt und die ausgewählten Zugriffs- und Data Governance-Bezeichnungen anwendet](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

Die **[!UICONTROL Bearbeiten von Bezeichnungen]** angezeigt, in dem Sie die Titel auswählen können, die Sie auf die Schemafelder anwenden möchten. Wählen Sie für diesen Anwendungsfall die **[!UICONTROL PHI/Reguläre Gesundheitsdaten]** Beschriftung und wählen Sie **[!UICONTROL Speichern]**.

![Bild mit der ausgewählten und gespeicherten RHD-Beschriftung](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Wenn einem Feld eine Beschriftung hinzugefügt wird, wird diese Beschriftung auf die übergeordnete Ressource dieses Felds angewendet (entweder auf eine Klasse oder eine Feldergruppe). Wenn die übergeordnete Klasse oder Feldergruppe von anderen Schemas verwendet wird, übernehmen diese Schemas dieselbe Beschriftung.

## Anwenden von Bezeichnungen auf Segmente

Nachdem Sie die Beschriftung Ihrer Schemafelder abgeschlossen haben, können Sie jetzt mit der Kennzeichnung Ihrer Segmente beginnen.

Auswählen **[!UICONTROL Segmente]** über die linke Navigation. Eine Liste der in Ihrem Unternehmen verfügbaren Segmente wird angezeigt. In diesem Beispiel sind die folgenden beiden Segmente zu kennzeichnen, da sie sensible Gesundheitsdaten enthalten:

* Blutzucker > 100
* Insulin &lt;50

Auswählen **[!UICONTROL Blutzucker > 100]** , um das Segment zu kennzeichnen.

![Bild, das die im Tab Segmente ausgewählte Blutglukose > 100 anzeigt](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Das Segment **[!UICONTROL Details]** angezeigt. Auswählen **[!UICONTROL Zugriff verwalten]**.

![Bild, das die Auswahl des Managed Access-Zugriffs anzeigt](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

Die **[!UICONTROL Bearbeiten von Bezeichnungen]** angezeigt, sodass Sie die Beschriftungen auswählen können, die Sie auf das Segment anwenden möchten. Wählen Sie für diesen Anwendungsfall die **[!UICONTROL PHI/Reguläre Gesundheitsdaten]** Beschriftung und wählen Sie **[!UICONTROL Speichern]**.

![Bild, das die Auswahl des ausgewählten RHD-Titels und des ausgewählten Speichervorgangs anzeigt](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Wiederholen Sie die obigen Schritte mit **[!UICONTROL Insulin &lt;50]**.

## Zugriffskontrollrichtlinie erstellen {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Was sind politische Maßnahmen?"
>abstract="Richtlinien sind Aussagen, die Attribute zusammenbringen, um zulässige und unzulässige Handlungen festzustellen. Jede Organisation verfügt über eine Standardrichtlinie, die Sie aktivieren müssen, um Regeln für Ressourcen wie Segmente und Schemafelder zu definieren. Standardrichtlinien können weder bearbeitet noch gelöscht werden. Standardrichtlinien können jedoch aktiviert oder deaktiviert werden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Richtlinien verwalten"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Erstellen einer Richtlinie"
>abstract="Erstellen Sie eine Richtlinie, um die Aktionen zu definieren, die Ihre Benutzer für Ihre Segmente und Schemafelder ausführen können und nicht."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Erstellen einer Richtlinie"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Zulässige und unzulässige Aktionen für eine Richtlinie konfigurieren"
>abstract="A <b>Zugriff auf verweigern</b> -Richtlinie verweigert Benutzern den Zugriff, wenn die Kriterien erfüllt sind. Kombiniert mit <b>Folgendes ist falsch</b> - allen Benutzern wird der Zugriff verweigert, es sei denn, sie erfüllen die entsprechenden Kriterien. Mit dieser Art von Richtlinie können Sie eine sensible Ressource schützen und nur den Zugriff auf Benutzer mit entsprechenden Beschriftungen zulassen. <br>A <b>den Zugriff auf</b> -Richtlinie ermöglicht Benutzern den Zugriff, wenn die Kriterien erfüllt sind. Bei Kombination mit <b>Folgendes ist wahr</b> - Benutzer erhalten Zugriff, wenn sie die entsprechenden Kriterien erfüllen. Dadurch wird Benutzern nicht explizit der Zugriff verweigert, sondern der Zugriff auf eine Genehmigung hinzugefügt. Mit dieser Art von Richtlinie können Sie zusätzlichen Zugriff auf Ressourcen und zusätzlich zu den Benutzern gewähren, die bereits über Rollenberechtigungen Zugriff haben.&quot;</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Richtlinie bearbeiten"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Berechtigungen für Ressourcen konfigurieren"
>abstract="Eine Ressource ist das Asset oder Objekt, auf das ein Benutzer zugreifen kann oder nicht. Ressourcen können Segmente oder Schemafelder sein. Sie können Berechtigungen zum Schreiben, Lesen oder Löschen für Segmente und Schemafelder konfigurieren."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Bedingungen bearbeiten"
>abstract="Wenden Sie bedingte Anweisungen auf Ihre Richtlinie an, um den Benutzerzugriff auf bestimmte Ressourcen zu konfigurieren. Wählen Sie &quot;Übereinstimmung mit allen&quot;aus, damit Benutzer Rollen mit denselben Bezeichnungen wie eine Ressource erhalten, für die der Zugriff gestattet werden soll. Wählen Sie Entsprechung für alle aus, damit Benutzer nur eine Rolle mit einer Bezeichnung haben müssen, die einer Ressource entspricht. Beschriftungen können entweder als Kern- oder benutzerdefinierte Beschriftungen definiert werden. Kernbeschriftungen stellen von Adobe erstellte und bereitgestellte Beschriftungen dar und stellen benutzerdefinierte Beschriftungen dar, die von Ihnen für Ihr Unternehmen erstellte Beschriftungen darstellen."

Zugriffssteuerungsrichtlinien nutzen Beschriftungen, um zu definieren, welche Benutzerrollen Zugriff auf bestimmte Platform-Ressourcen haben. Richtlinien können lokal oder global sein und andere Richtlinien überschreiben. In diesem Beispiel wird der Zugriff auf Schemafelder und Segmente in allen Sandboxes Benutzern verweigert, die nicht über die entsprechenden Beschriftungen im Schemafeld verfügen.

>[!NOTE]
>
>Es wird eine &quot;Richtlinie zum Verweigern&quot;erstellt, um Zugriff auf sensible Ressourcen zu gewähren, da die Rolle den Personen Berechtigungen erteilt. Die geschriebene Richtlinie in diesem Beispiel **Leugnungen** Sie greifen auf zu, wenn Sie die erforderlichen Beschriftungen fehlen.

Um eine Zugriffskontrollrichtlinie zu erstellen, wählen Sie **[!UICONTROL Berechtigungen]** aus der linken Navigation und wählen Sie dann **[!UICONTROL Richtlinien]**. Wählen Sie als Nächstes **[!UICONTROL Richtlinie erstellen]**.

![Bild mit der Option Richtlinie erstellen , die in den Berechtigungen ausgewählt wird](../images/abac-end-to-end-user-guide/abac-create-policy.png)

Die **[!UICONTROL Neue Richtlinie erstellen]** angezeigt, in dem Sie aufgefordert werden, einen Namen und eine optionale Beschreibung einzugeben. Auswählen **[!UICONTROL Bestätigen]** wenn fertig.

![Bild mit dem Dialogfeld Neue Richtlinie erstellen und Bestätigen auswählen](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Um den Zugriff auf die Schemafelder zu verweigern, verwenden Sie den Dropdown-Pfeil und wählen Sie **[!UICONTROL Zugriff auf verweigern]** und wählen Sie **[!UICONTROL Keine Ressource ausgewählt]**. Wählen Sie als Nächstes **[!UICONTROL Schemafeld]** und wählen Sie **[!UICONTROL Alle]**.

![Bild mit Auswahl von Zugriff und Ressourcen verweigern](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

Die folgende Tabelle zeigt die Bedingungen, die beim Erstellen einer Richtlinie verfügbar sind:

| Bedingungen | Beschreibung |
| --- | --- |
| Folgendes ist falsch | Wenn &quot;Zugriff auf verweigern&quot;festgelegt ist, wird der Zugriff eingeschränkt, wenn der Benutzer die ausgewählten Kriterien nicht erfüllt. |
| Folgendes ist wahr | Wenn die Option &quot;Zugriff auf gewähren&quot;festgelegt ist, ist der Zugriff zulässig, wenn der Benutzer die ausgewählten Kriterien erfüllt. |
| Entspricht allen | Der Benutzer verfügt über eine Beschriftung, die allen auf eine Ressource angewendeten Bezeichnungen entspricht. |
| Entspricht allen | Der Benutzer verfügt über alle Bezeichnungen, die mit allen Bezeichnungen übereinstimmen, die auf eine Ressource angewendet werden. |
| Core-Bezeichnung | Eine Kernbeschriftung ist eine von der Adobe definierte Bezeichnung, die in allen Platform-Instanzen verfügbar ist. |
| Eigene Bezeichnung | Eine benutzerdefinierte Bezeichnung ist eine Bezeichnung, die von Ihrem Unternehmen erstellt wurde. |

Auswählen **[!UICONTROL Folgendes ist falsch]** und wählen Sie **[!UICONTROL Kein Attribut ausgewählt]**. Wählen Sie als Nächstes den Benutzer aus. **[!UICONTROL Core-Bezeichnung]**, wählen Sie **[!UICONTROL Entspricht allen]**. Ressource auswählen **[!UICONTROL Core-Bezeichnung]** und wählen Sie schließlich **[!UICONTROL Ressource hinzufügen]**.

![Bild mit den ausgewählten Bedingungen und der ausgewählten Ressource hinzufügen](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Eine Ressource ist das Asset oder Objekt, auf das ein Betreff zugreifen kann oder nicht. Ressourcen können Segmente oder Schemata sein.

Um den Zugriff auf die Segmente zu verweigern, verwenden Sie den Dropdown-Pfeil und wählen Sie **[!UICONTROL Zugriff auf verweigern]** und wählen Sie **[!UICONTROL Keine Ressource ausgewählt]**. Wählen Sie als Nächstes **[!UICONTROL Segment]** und wählen Sie **[!UICONTROL Alle]**.

Auswählen **[!UICONTROL Folgendes ist falsch]** und wählen Sie **[!UICONTROL Kein Attribut ausgewählt]**. Wählen Sie als Nächstes den Benutzer aus. **[!UICONTROL Core-Bezeichnung]**, wählen Sie **[!UICONTROL Entspricht allen]**. Ressource auswählen **[!UICONTROL Core-Bezeichnung]** und wählen Sie schließlich **[!UICONTROL Speichern]**.

![Bild mit ausgewählten Bedingungen und ausgewähltem Speichern](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Auswählen **[!UICONTROL Aktivieren]** um die Richtlinie zu aktivieren. Daraufhin wird ein Dialogfeld angezeigt, in dem Sie zur Bestätigung der Aktivierung aufgefordert werden. Auswählen **[!UICONTROL Bestätigen]** und wählen Sie **[!UICONTROL Schließen]**.

![Bild mit der aktivierten Richtlinie ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Nächste Schritte

Sie haben die Anwendung von Bezeichnungen auf eine Rolle, Schemafelder und Segmente abgeschlossen. Die externe Agentur, die diesen Rollen zugewiesen ist, kann diese Beschriftungen und ihre Werte in der Schema-, Datensatz- und Profilansicht anzeigen. Diese Felder können bei Verwendung von Segment Builder auch nicht in der Segmentdefinition verwendet werden.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](./overview.md).
