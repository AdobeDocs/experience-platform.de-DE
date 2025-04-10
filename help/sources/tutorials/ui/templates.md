---
description: Erfahren Sie, wie Sie Vorlagen in der Adobe Experience Platform-Benutzeroberfläche verwenden können, um die Datenaufnahme für B2B-Daten zu beschleunigen.
title: Erstellen eines Quellen-Datenflusses mithilfe von Vorlagen in der Benutzeroberfläche
badge1: Beta
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2250'
ht-degree: 40%

---

# Erstellen eines Quellen-Datenflusses mithilfe von Vorlagen in der Benutzeroberfläche {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Vorlagen für Quellen in der Benutzeroberfläche von Experience Platform"
>abstract="Zu Vorlagen gehören automatisch generierte Assets wie Schemata, Datensätze, Identitäten, Zuordnungsregeln, Identity-Namespaces und Datenflüsse, die Sie beim Einbringen von Daten aus einer Quelle in Experience Platform verwenden können. Sie können automatisch generierte Assets aktualisieren, um sie an Anwendungsfälle anzupassen."

>[!IMPORTANT]
>
>Vorlagen befinden sich in der Beta-Phase und werden von den folgenden Quellen unterstützt:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>Dokumentation und Funktionalität können sich ändern.

Adobe Experience Platform stellt vorkonfigurierte Vorlagen bereit, mit denen Sie den Datenerfassungsprozess beschleunigen können. Zu Vorlagen gehören automatisch generierte Assets wie Schemata, Datensätze, Identitäten, Zuordnungsregeln, Identitäts-Namespaces und Datenflüsse, die Sie beim Einbringen von Daten aus einer Quelle in Experience Platform verwenden können.

Mit Vorlagen können Sie:

* die Amortisierungszeit der Datenaufnahme durch Beschleunigung der vorlagenbasierten Asset-Erstellung reduzieren.
* Fehler minimieren, die während der manuellen Datenerfassung auftreten können.
* automatisch generierte Assets zu jedem Zeitpunkt entsprechend Ihren Anwendungsfällen aktualisieren.

Das folgende Tutorial enthält Schritte zur Verwendung von Vorlagen in der Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Verwenden von Vorlagen in der Benutzeroberfläche von Experience Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Geschäftstyp auswählen"
>abstract="Wählen Sie den entsprechenden Geschäftstyp für Ihren Anwendungsfall aus. Ihr Zugriff variiert je nach Ihrem Real-time Customer Data Platform-Abonnementkonto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=de" text="Real-Time CDP – Übersicht"

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL linken Navigationsbereich die Option]** Quellen“ aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen und einen Quellkatalog anzuzeigen, der in Experience Platform verfügbar ist.

Verwenden Sie das Menü *[!UICONTROL Kategorien]*, um Quellen nach Kategorie zu filtern. Geben Sie alternativ einen Quellnamen in die Suchleiste ein, um eine bestimmte Quelle aus dem Katalog zu finden.

Gehen Sie zur Kategorie [!UICONTROL Adobe], um die [!DNL Marketo Engage] anzuzeigen, und klicken Sie dann auf [!UICONTROL Daten hinzufügen] um zu beginnen.

![Katalog des Quellarbeitsbereichs mit hervorgehobener Marketo Engage-Quelle.](../../images/tutorials/templates/catalog.png)

Es wird ein Popup-Fenster angezeigt, in dem Sie die Möglichkeit haben, Vorlagen zu durchsuchen oder vorhandene Schemata und Datensätze zu verwenden.

* **Vorlagen durchsuchen**: Quellvorlagen erstellen automatisch Schemata, Identitäten, Datensätze und Datenflüsse mit Zuordnungsregeln für Sie. Sie können diese Assets nach Bedarf anpassen.
* **Meine vorhandenen Assets verwenden**: Nehmen Sie Ihre Daten mit vorhandenen Datensätzen und Schemata auf, die Sie erstellt haben. Sie können bei Bedarf auch neue Datensätze und Schemata erstellen.

Um automatisch generierte Assets zu verwenden, wählen Sie **[!UICONTROL Vorlagen durchsuchen]** und dann **[!UICONTROL Auswählen]** aus.

![Ein Popup-Fenster mit Optionen, um Vorlagen zu durchsuchen oder vorhandene Assets zu verwenden.](../../images/tutorials/templates/browse-templates.png)

### Authentifizierung

Der Authentifizierungsschritt wird angezeigt und Sie werden aufgefordert, entweder ein neues Konto zu erstellen oder ein vorhandenes Konto zu verwenden.

>[!BEGINTABS]

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie [!UICONTROL Vorhandenes Konto] und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die Auswahlseite für ein vorhandenes Konto mit einer Liste vorhandener Konten, auf die Sie zugreifen können.](../../images/tutorials/templates/existing-account.png)

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie dann Ihre Details zur Quellverbindung und Anmeldedaten für die Kontoauthentifizierung an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![Die Authentifizierungsseite für ein neues Konto mit Details zur Quellverbindung und Anmeldedaten zur Kontoauthentifizierung.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Vorlagen auswählen

Nachdem Ihr Konto authentifiziert wurde, können Sie jetzt die Vorlage auswählen, die Sie für Ihren Datenfluss verwenden möchten.

+++Vorlagen [!DNL Marketo Engage]
In der folgenden Tabelle sind die Vorlagen aufgeführt, die für die [!DNL Marketo Engage]-Quelle verfügbar sind.

| Vorlagen [!DNL Marketo Engage] | Beschreibung |
| --- | --- |
| Aktivitäten | Die Aktivitätsvorlage erfasst ereignisbasierte Momentaufnahmen von Aktivitäten wie E-Mail-Interaktionen, Website-Interaktionen und Verkaufsanrufen. |
| Firmen | Die Vorlage „Unternehmen“ erfasst Details zu Geschäftskonten wie firmografische Informationen, Standort und Abrechnungsinformationen. |
| Benannte Konten | Die Vorlage Benannte Konten erfasst Details für Konten, die als Zielkonten bestimmt wurden, die verfolgt werden sollen. |
| Opportunitys | Die Opportunities-Vorlage erfasst Details zu Geschäftschancen wie Typ, Verkaufsstufe und verwandte Konten. |
| Opportunity-Kontaktrollen | Die Vorlage „Opportunity-Kontaktrollen“ erfasst Details zu den Rollen für Leads, die mit einer bestimmten Opportunity verbunden sind. |
| Personen | Die Vorlage Personen erfasst Attribute für einzelne Personen wie demografische Details, Kontaktinformationen und Einverständnisvoreinstellungen. |
| Programmmitgliedschaften | Die Vorlage Programmmitgliedschaften erfasst Details zu Kontakten, die mit einer Unternehmenskampagne verbunden sind, einschließlich Pflegekadenzen und Kontaktantworten. |
| Programme | Die Vorlage „Programme“ erfasst Details zu Geschäftskampagnen wie Status, Kanäle, Timelines und Kosten. |
| Mitgliedschaften in statischen Listen | Die Vorlage für Zugehörigkeiten zu statischen Listen erfasst die Beziehungen zwischen Personen und deren Zugehörigkeit in statischen Listen. |
| Statische Listen | Die Vorlage Statische Liste erfasst instanziierte Personenlisten für bestimmte Anwendungsfälle. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2B-Vorlagen
In der folgenden Tabelle sind die B2B-Vorlagen aufgeführt, die für die [!DNL Salesforce]-Quelle verfügbar sind.

| [!DNL Salesforce] B2B-Vorlagen | Beschreibung |
| --- | --- |
| Account Contact Relation | Die Vorlage „Konto-Kontaktbeziehung“ erfasst die Beziehung zwischen einem Kontakt und einem oder mehreren Konten. |
| Konten | Die Kontovorlage erfasst Details des Geschäftskontos wie firmografische Informationen, Standort und Abrechnungsinformationen. |
| Kampagnenmitglieder | Die Vorlage Kampagnenmitglieder erfasst die Beziehung zwischen einem einzelnen Lead oder Kontakt und einer bestimmten [!DNL Salesforce]. |
| Kampagnen | Die Kampagnenvorlage erfasst Details des Geschäftskontos wie firmeninterne demografische Informationen, Standort und Abrechnungsinformationen. |
| Kontakte | Die Kontaktvorlage erfasst Attribute für Kontakte wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |
| Leads | Die Lead-Vorlage erfasst Attribute für Leads wie demografische Details, Kontaktinformationen und verwandte Geschäftseinheiten. |
| Opportunitys | Die Opportunities-Vorlage erfasst Details zu Geschäftschancen wie Typ, Verkaufsstufe und verwandtes Konto. |
| Opportunity-Kontaktrollen | Die Vorlage „Opportunity-Kontaktrollen“ erfasst Details zu den Rollen für Leads, die mit einer bestimmten Opportunity verbunden sind. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2C-Vorlagen
In der folgenden Tabelle sind die B2C-Vorlagen aufgeführt, die für die [!DNL Salesforce]-Quelle verfügbar sind.

| [!DNL Salesforce] B2C-Vorlagen | Beschreibung |
| --- | --- |
| Kontakt | Die Kontaktvorlage erfasst Attribute für Kontakte wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |
| Lead | Die Lead-Vorlage erfasst Attribute für Leads wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2B-Vorlagen
In der folgenden Tabelle sind die B2B-Vorlagen aufgeführt, die für die [!DNL Microsoft Dynamics]-Quelle verfügbar sind.

| [!DNL Microsoft Dynamics] B2B-Vorlagen | Beschreibung |
| --- | --- |
| Konten | Die Kontovorlage erfasst Details des Geschäftskontos wie firmografische Informationen, Standort und Abrechnungsinformationen. |
| Kampagnen | Die Kampagnenvorlage erfasst Details des Geschäftskontos wie firmeninterne demografische Informationen, Standort und Abrechnungsinformationen. |
| Kontakte | Die Kontaktvorlage erfasst Attribute für Kontakte wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |
| Leads | Die Lead-Vorlage erfasst Attribute für Leads wie demografische Details, Kontaktinformationen und verwandte Geschäftseinheiten. |
| Marketing-Liste | Die Marketing-Listenvorlage erfasst eine Gruppe von bestehenden oder potenziellen Kunden, die für eine Marketing-Kampagne oder andere Verkaufszwecke erstellt wurden. |
| Mitglieder der Marketing-Liste | Die Mitglieder der Marketing-Liste erfassen die Details einer bestimmten Art von Kundendatensätzen, wie Leads, Konten oder Kontakte, in einer Marketing-Liste. |
| Opportunitys | Die Opportunities-Vorlage erfasst Details zu Geschäftschancen wie Typ, Verkaufsstufe und verwandtes Konto. |
| Opportunity-Kontaktrollen | Die Vorlage „Opportunity-Kontaktrollen“ erfasst Details zu den Rollen für Leads, die mit einer bestimmten Opportunity verbunden sind. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2C-Vorlagen
In der folgenden Tabelle sind die B2C-Vorlagen aufgeführt, die für die [!DNL Microsoft Dynamics]-Quelle verfügbar sind.

| [!DNL Microsoft Dynamics] B2C-Vorlagen | Beschreibung |
| --- | --- |
| Kontakt | Die Kontaktvorlage erfasst Attribute für Kontakte wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |
| Lead | Die Lead-Vorlage erfasst Attribute für Leads wie demografische Details, Kontaktinformationen und zugehörige Geschäftsentitäten. |

{style="table-layout:auto"}

+++

Je nach ausgewähltem Geschäftstyp wird eine Liste von Vorlagen angezeigt. Wählen Sie das Vorschausymbol ![Vorschausymbol](/help/images/icons/preview.png) neben einem Vorlagennamen aus, um eine Vorschau der Beispieldaten aus der Vorlage anzuzeigen.

![Liste von Vorlagen mit hervorgehobenem Vorschausymbol.](../../images/tutorials/templates/templates.png)

Das Vorschaufenster wird angezeigt, in dem Sie Beispieldaten aus Ihrer Vorlage analysieren und überprüfen können. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verstanden]** aus.

![Das Vorschaufenster mit Beispieldaten.](../../images/tutorials/templates/preview-sample-data.png)

Wählen Sie als Nächstes aus der Liste die Vorlage aus, die Sie verwenden möchten. Sie können mehrere Vorlagen auswählen und mehrere Datenflüsse gleichzeitig erstellen. Eine Vorlage kann jedoch nur einmal pro Konto verwendet werden. Nachdem Sie Ihre Vorlagen ausgewählt haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit, um die Assets zu generieren.

Wenn Sie ein oder mehrere Elemente aus der Liste der verfügbaren Vorlagen auswählen, werden weiterhin alle B2B-Schemata und Identitäts-Namespaces generiert, um sicherzustellen, dass B2B-Beziehungen zwischen Schemata korrekt konfiguriert sind.

>[!NOTE]
>
>Bereits verwendete Vorlagen werden von der Auswahl ausgeschlossen.

![Die Liste der Vorlagen mit der ausgewählten Vorlage „Rolle von Opportunity-Kontakt“.](../../images/tutorials/templates/select-template.png)

### Zeitplan festlegen

Die [!DNL Microsoft Dynamics]- und die [!DNL Salesforce] unterstützen beide die Planung von Datenflüssen.

Verwenden Sie die Zeitplanungs-Oberfläche, um einen Aufnahmezeitplan für Ihre Datenflüsse zu konfigurieren. Legen Sie die Aufnahmefrequenz auf **Einmal** fest, um eine einmalige Aufnahme zu erstellen.

![Die Planungsschnittstelle für Dynamics- und Salesforce-Vorlagen.](../../images/tutorials/templates/schedule.png)

Alternativ können Sie Ihre Aufnahmefrequenz auf **Minute**, **Stunde**, **Tag** oder **Woche** einstellen. Wenn Sie Ihren Datenfluss für mehrere Aufnahmen planen, müssen Sie ein Intervall festlegen, um einen Zeitrahmen zwischen jeder Aufnahme festzulegen. Wenn beispielsweise die Aufnahmefrequenz auf **Stunde** und das Intervall auf **15) eingestellt ist** bedeutet dies, dass Ihr Datenfluss alle **15 Stunden Daten aufnehmen soll**.

In diesem Schritt können Sie auch **Aufstockung“ aktivieren** eine Spalte für die inkrementelle Aufnahme von Daten definieren. Die Aufstockung wird verwendet, um historische Daten aufzunehmen, während die Spalte, die Sie für die inkrementelle Aufnahme definieren, es ermöglicht, neue Daten von vorhandenen Daten zu unterscheiden.

Nachdem Sie die Konfiguration Ihres Aufnahmezeitplans abgeschlossen haben, klicken Sie auf **[!UICONTROL Beenden]**.

![Die Planungsschnittstelle für Dynamics- und Salesforce-Vorlagen mit aktivierter Aufstockung.](../../images/tutorials/templates/backfill.png)

### Überprüfen von Assets {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Überprüfen der automatisch generierten Assets"
>abstract="Die Generierung aller Assets kann bis zu fünf Minuten dauern. Wenn Sie die Seite verlassen möchten, erhalten Sie die Benachrichtigung zum Zurückkehren, wenn die Assets abgeschlossen sind. Sie können die Assets überprüfen, sobald sie generiert wurden, und jederzeit zusätzliche Konfigurationen an Ihrem Datenfluss vornehmen."

Die Seite [!UICONTROL Vorlagen-Assets überprüfen] zeigt die Assets an, die automatisch als Teil Ihrer Vorlage generiert wurden. Auf dieser Seite können Sie die automatisch generierten Schemata, Datensätze, Identitäts-Namespaces und Datenflüsse anzeigen, die mit Ihrer Quellverbindung verknüpft sind. Die Generierung aller Assets kann bis zu fünf Minuten dauern. Wenn Sie die Seite verlassen möchten, erhalten Sie die Benachrichtigung zum Zurückkehren, wenn die Assets abgeschlossen sind. Sie können die Assets überprüfen, sobald sie generiert wurden, und jederzeit zusätzliche Konfigurationen an Ihrem Datenfluss vornehmen.

Standardmäßig werden automatisch generierte Datenflüsse in einen Entwurfsstatus versetzt, um weitere Anpassungen der Konfigurationen zu ermöglichen, z. B. Zuordnungsregeln oder geplante Häufigkeiten. Klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie **[!UICONTROL Zuordnungen in Vorschau anzeigen]**, um die für Ihren Datenflussentwurf erstellten Zuordnungssätze anzuzeigen.

![Ein Dropdown-Fenster mit ausgewählter Option für die Zuordnungsvorschau.](../../images/tutorials/templates/preview.png)

Eine Vorschauseite wird angezeigt, auf der Sie die Zuordnungsbeziehung zwischen Ihren Quelldatenfeldern und den Zielschemafeldern überprüfen können. Nachdem Sie die Zuordnungen Ihres Datenflusses angezeigt haben. Klicken Sie auf **[!UICONTROL Verstanden]**.

![Das Zuordnungsvorschaufenster.](../../images/tutorials/templates/preview-mappings.png)

Sie können Ihre Datenflüsse jederzeit nach der Ausführung aktualisieren. Klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und dann auf **[!UICONTROL Datenfluss aktualisieren]**. Sie gelangen auf die Seite mit dem Quellen-Workflow, auf der Sie Ihre Datenflussdetails aktualisieren können, einschließlich der Einstellungen für die partielle Aufnahme, Fehlerdiagnose und Warnbenachrichtigungen sowie der Zuordnung Ihres Datenflusses.

Sie können die Ansicht des Schema-Editors verwenden, um am automatisch erstellten Schema Aktualisierungen vorzunehmen. Besuchen Sie das Handbuch unter [Verwenden des Schema-Editors](../../../xdm/tutorials/create-schema-ui.md) für weitere Informationen.

![Ein Dropdown-Fenster mit aktivierter Option „Datenflüsse aktualisieren“.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>Sie können auf Ihren Datenflussentwurf über die [!UICONTROL Datenflüsse] im Arbeitsbereich Quellen zugreifen. Wählen Sie **[!UICONTROL Datenflüsse]** in der oberen Kopfzeile und wählen Sie dann den Datenfluss, den Sie aktualisieren möchten, aus der Liste aus.
>
>![Eine Liste der vorhandenen Datenflüsse im Datenflusskatalog des Arbeitsbereichs „Quellen“.](../../images/tutorials/templates/dataflows.png)

### Veröffentlichen des Datenflusses

Beginnen Sie den Veröffentlichungsprozess, indem Sie den Quell-Workflow durchlaufen. Nachdem Sie [!UICONTROL Datenfluss aktualisieren] ausgewählt haben, gelangen Sie zum Schritt *[!UICONTROL Daten hinzufügen]* des Workflows. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Schritt „Daten hinzufügen“ für einen Datenfluss-Entwurf](../../images/tutorials/templates/continue-draft.png)

Bestätigen Sie anschließend Ihre Datenflussdetails und konfigurieren Sie Einstellungen für Fehlerdiagnose, partielle Aufnahme und Warnbenachrichtigungen. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ für einen Datenflussentwurf.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>Sie können **[!UICONTROL Als Entwurf speichern]** jederzeit auswählen, um die an Ihrem Datenfluss vorgenommenen Änderungen anzuhalten und zu speichern.

Der Schritt Zuordnung wird angezeigt. In diesem Schritt können Sie die Zuordnungskonfigurationen Ihres Datenflusses neu konfigurieren. Eine umfassende Anleitung zu den für die Zuordnung verwendeten Datenvorbereitungsfunktionen finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../data-prep/ui/mapping.md).

![Der Zuordnungsschritt für einen Datenfluss-Entwurf.](../../images/tutorials/templates/mapping.png)

Überprüfen Sie abschließend die Details Ihres Datenflusses und wählen Sie dann **[!UICONTROL Speichern und Aufnehmen]** aus, um Ihren Entwurf zu veröffentlichen.

![Der Überprüfungsschritt für einen Datenflussentwurf.](../../images/tutorials/templates/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie jetzt Datenflüsse sowie Assets wie Schemata, Datensätze und Identitäts-Namespaces mithilfe von Vorlagen erstellt. Allgemeine Informationen zu Quellen finden Sie unter [Quellen – Übersicht](../../home.md).

## Warnhinweise und Benachrichtigungen {#alerts-and-notifications}

Vorlagen werden von Adobe Experience Platform-Warnhinweisen unterstützt. Sie können im Benachrichtigungsbereich Aktualisierungen zum Status Ihrer Assets erhalten und zur Überprüfungsseite zurückkehren.

Wählen Sie das Benachrichtigungssymbol in der oberen Kopfzeile der Experience Platform-Benutzeroberfläche und wählen Sie dann die Statuswarnung aus, um die Assets anzuzeigen, die Sie überprüfen möchten.

![Der Benachrichtigungsbereich in der Experience Platform-Benutzeroberfläche mit einer hervorgehobenen Benachrichtigung, die einen fehlgeschlagenen Datenfluss meldet.](../../images/tutorials/templates/notifications.png)

Sie können die Warnhinweiseinstellungen Ihrer Vorlagen aktualisieren, um sowohl E-Mail- als auch In-Experience Platform-Benachrichtigungen zum Status Ihrer Datenflüsse zu erhalten. Weitere Informationen zum Konfigurieren von Warnhinweisen finden Sie im Handbuch [Abonnieren von Warnhinweisen für Datenflüsse zu Quellen](../ui/alerts.md).