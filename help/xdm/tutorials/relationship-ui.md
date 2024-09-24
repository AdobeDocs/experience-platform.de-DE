---
keywords: Experience Platform; home; beliebte Themen; ui; UI; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schema Editor; Schema; Schema; Schemas; erstellen; Beziehung; Beziehung; Referenz; Referenz;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 21%

---

# Definieren einer 1:1-Beziehung zwischen zwei Schemata mithilfe des [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Schemabeziehungen"
>abstract="Schemata, die zu verschiedenen Klassen gehören, können über Beziehungsfelder kontextuell miteinander verknüpft werden und ermöglichen es Ihnen dadurch, komplexere Segmentierungsregeln zu erstellen. Weitere Informationen zu Schemabeziehungen finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Referenzschema"
>abstract="Wählen Sie das Schema aus, mit dem Sie eine Beziehung herstellen möchten. Dieses Schema kann eine andere Klasse sein als das aktuelle Schema. Weitere Informationen zu Schemabeziehungen finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Referenz-Identity-Namespace"
>abstract="Der Namespace (Typ) für das primäre Identitätsfeld des Referenzschemas. Das Referenzschema muss über ein festgelegtes primäres Identitätsfeld verfügen, um Teil einer Beziehung sein zu können. Weitere Informationen zu Schemabeziehungen finden Sie in der Dokumentation."

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Durch die Definition dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM)-Schemas können Sie komplexe Einblicke in Ihre Kundendaten gewinnen.

Während Schemabeziehungen durch die Verwendung des Vereinigungsschemas und [!DNL Real-Time Customer Profile] abgeleitet werden können, gilt dies nur für Schemata einer gemeinsamen Klasse. Um eine Beziehung zwischen zwei Schemas herzustellen, die zu verschiedenen Klassen gehören, muss einem Quellschema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität des anderen verwandten Schemas verweist.

>[!NOTE]
>
>Wenn sowohl das Quell- als auch das Zielschema zur gleichen Klasse gehören, sollte ein dediziertes Beziehungsfeld **nicht** verwendet werden. Verwenden Sie in diesem Fall die Benutzeroberfläche des Vereinigungsschemas , um die Beziehung anzuzeigen. Anweisungen dazu finden Sie im Abschnitt [Beziehungen anzeigen](../../profile/ui/union-schema.md#view-relationships) des UI-Handbuchs für Vereinigungsschemas.

Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Benutzeroberfläche von [!DNL Experience Platform]. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

>[!NOTE]
>
>Anweisungen zum Erstellen einer n:n-Beziehung in Adobe Real-time Customer Data Platform B2B Edition finden Sie im Handbuch zum Erstellen von B2B-Beziehungen [.](./relationship-b2b.md)

## Erste Schritte

Für dieses Tutorial sind ein grundlegendes Verständnis von [!DNL XDM System] und des Schema-Editors in der Benutzeroberfläche von [!DNL Experience Platform] erforderlich. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und dessen Implementierung in [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemata.
* [Erstellen Sie ein Schema mit dem  [!DNL Schema Editor]](create-schema-ui.md): Ein Tutorial, das die Grundlagen der Arbeit mit dem [!DNL Schema Editor] behandelt.

## Quell- und Referenzschema definieren

Wir gehen davon aus, dass Sie die beiden Schemata, die in der Beziehung definiert werden sollen, bereits erstellt haben. Zu Demonstrationszwecken erstellt dieses Tutorial eine Beziehung zwischen Mitgliedern des Treueprogramms einer Organisation (definiert in einem &quot;[!DNL Loyalty Members]&quot;-Schema) und ihrem Lieblingshotel (definiert in einem &quot;[!DNL Hotels]&quot;-Schema).

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schemas definierte primäre Identitäten aufweisen und für [!DNL Real-Time Customer Profile] aktiviert sein. Lesen Sie den Abschnitt zum Aktivieren eines Schemas für die Verwendung in Profil](./create-schema-ui.md#profile) im Tutorial zur Schemaerstellung , wenn Sie Anleitungen zum Konfigurieren Ihrer Schemas benötigen.[

Schemabeziehungen werden durch ein dediziertes Feld innerhalb eines **Quellschemas** dargestellt, das auf ein anderes Feld innerhalb eines **Referenzschemas** verweist. In den folgenden Schritten ist &quot;[!DNL Loyalty Members]&quot; das Quellschema, während &quot;[!DNL Hotels]&quot; als Referenzschema fungiert.

In den folgenden Abschnitten wird die Struktur der einzelnen Schemas beschrieben, die in diesem Tutorial verwendet werden, bevor eine Beziehung definiert wurde.

### [!DNL Loyalty Members] schema

Das Quellschema &quot;[!DNL Loyalty Members]&quot; basiert auf der Klasse [!DNL XDM Individual Profile] und enthält ein Feld, das Mitglieder eines Treueprogramms beschreibt. Eines dieser Felder, `personalEmail.addess`, dient als primäre Identität für das Schema unter dem Namespace [!UICONTROL E-Mail] . Wie unter **[!UICONTROL Schemaeigenschaften]** zu sehen ist, wurde dieses Schema für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Das Referenzschema &quot;[!DNL Hotels]&quot; basiert auf einer benutzerdefinierten Klasse &quot;[!DNL Hotels]&quot; und enthält Felder, die ein Hotel beschreiben. Um an einer Beziehung teilnehmen zu können, muss das Referenzschema auch über eine primäre Identität verfügen, die für [!UICONTROL Profil] definiert und aktiviert ist. In diesem Fall fungiert `_tenantId.hotelId`als primäre Identität für das Schema und verwendet einen benutzerdefinierten Identitäts-Namespace &quot;[!DNL Hotel ID]&quot;.

![Aktivieren für Profil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Informationen zum Erstellen benutzerdefinierter Identitäts-Namespaces finden Sie in der Dokumentation zum [Identitätsdienst](../../identity-service/features/namespaces.md#manage-namespaces) .

## Erstellen einer Beziehungsfeldgruppe

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quellschema über kein dediziertes Zeichenfolgenfeld verfügt, das als Zeiger auf die primäre Identität des Referenzschemas verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das die primäre Identität des Referenzschemas angibt. Sie können dieses Feld zum Quellschema hinzufügen, indem Sie eine neue Schemafeldergruppe erstellen oder eine bestehende erweitern.

Im Fall des Schemas [!DNL Loyalty Members] wird ein neues Feld `preferredHotel` hinzugefügt, das das bevorzugte Hotel des Treuemitglieds für Unternehmensbesuche angibt. Wählen Sie zunächst das Pluszeichen (**+**) neben dem Namen des Quellschemas aus.

![](../images/tutorials/relationship/loyalty-add-field.png)

Auf der Arbeitsfläche wird ein neuer Feld-Platzhalter angezeigt. Geben Sie unter &quot;**[!UICONTROL Feldeigenschaften]**&quot;einen Feldnamen und einen Anzeigenamen für das Feld ein und setzen Sie dessen Typ auf &quot;[!UICONTROL String]&quot;. Wählen Sie unter **[!UICONTROL Zuweisen zu]** eine vorhandene Feldergruppe aus, die erweitert werden soll, oder geben Sie einen eindeutigen Namen ein, um eine neue Feldergruppe zu erstellen. In diesem Fall wird eine neue Feldergruppe &quot;[!DNL Preferred Hotel]&quot; erstellt.

![](../images/tutorials/relationship/relationship-field-details.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![](../images/tutorials/relationship/relationship-field-apply.png)

Das aktualisierte `preferredHotel` -Feld wird auf der Arbeitsfläche unter einem `_tenantId` -Objekt angezeigt, da es sich um ein benutzerdefiniertes Feld handelt. Wählen Sie **[!UICONTROL Speichern]** aus, um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definieren eines Beziehungsfelds für das Quellschema {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

>[!NOTE]
>
>Beziehungen können nur für Zeichenfolgen- oder Zeichenfolgen-Array-Felder unterstützt werden.

Wählen Sie das Feld `preferredHotel` auf der Arbeitsfläche aus und wählen Sie dann **[!UICONTROL Beziehung hinzufügen]** in der Seitenleiste **[!UICONTROL Feldeigenschaften]** aus.

![Der Schema-Editor mit der Option Beziehung hinzufügen , die in der Seitenleiste für Feldeigenschaften hervorgehoben ist.](../images/tutorials/relationship/add-relationship.png)

Das Dialogfeld [!UICONTROL Beziehung hinzufügen] wird angezeigt. In diesem Dialogfeld können Sie die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds festlegen. Für Real-Time CDP-B2C-Benutzer können Sie **nur** eine Eins-zu-Eins-Beziehung zwischen dem Quell- und dem Referenzschema festlegen.

>[!NOTE]
>
>Wenn Sie Zugriff auf Real-Time CDP B2B Edition haben, können Sie die Steuerelemente in der rechten Leiste der Arbeitsfläche verwenden, um ein Beziehungsfeld zu definieren und mithilfe des [gleichen Dialogfelds](./relationship-b2b.md#relationship-field) eine n:n-Beziehung zu erstellen.

![Das Dialogfeld &quot;Beziehung hinzufügen&quot;.](../images/tutorials/relationship/add-relationship-dialog.png)

Verwenden Sie das Dropdown-Menü für **[!UICONTROL Referenzschema]** und wählen Sie das Referenzschema für die Beziehung aus (&quot;[!DNL Hotels]&quot; in diesem Beispiel).

>[!NOTE]
>
>Nur Schemas, die eine primäre Identität enthalten, werden im Dropdown-Menü des Referenzschemas eingeschlossen. Dieser Schutz verhindert, dass Sie versehentlich eine Beziehung mit einem Schema erstellen, das noch nicht ordnungsgemäß konfiguriert ist.

Der Identitäts-Namespace des Referenzschemas (in diesem Fall &quot;[!DNL Hotel ID]&quot;) wird automatisch unter **[!UICONTROL Referenz-Identitäts-Namespace]** ausgefüllt. Wählen Sie **[!UICONTROL Anwenden]** aus, wenn Sie fertig sind.

![Das Dialogfeld &quot;Beziehung hinzufügen&quot;mit den konfigurierten Beziehungsparametern und &quot;Anwenden&quot;wurde hervorgehoben.](../images/tutorials/relationship/apply-relationship.png)

Das Feld `preferredHotel` wird jetzt auf der Arbeitsfläche als Beziehung hervorgehoben und zeigt den Namen des Referenzschemas an. Wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu speichern und den Workflow abzuschließen.

![Der Schema-Editor mit den Verweisen auf die Beziehung und &quot;Speichern hervorgehoben&quot;](../images/tutorials/relationship/relationship-save.png).

### Vorhandenes Beziehungsfeld bearbeiten {#edit-relationship}

Um das Referenzschema zu ändern, wählen Sie ein Feld mit einer vorhandenen Beziehung aus und wählen Sie dann **[!UICONTROL Beziehung bearbeiten]** in der Seitenleiste **[!UICONTROL Feldeigenschaften]** aus.

![Der Schema-Editor mit hervorgehobener Bearbeitungsbeziehung.](../images/tutorials/relationship/edit-relationship.png)

Das Dialogfeld [!UICONTROL Beziehung bearbeiten] wird angezeigt. Von hier aus können Sie den unter [Definieren eines Beziehungsfelds](#relationship-field) beschriebenen Prozess ausführen oder die Beziehung löschen. Wählen Sie **[!UICONTROL Beziehung löschen]** aus, um die Beziehung zum Referenzschema zu entfernen.

![Das Dialogfeld &quot;Beziehung bearbeiten&quot;.](../images/tutorials/relationship/edit-relationship-dialog.png)

## Filtern und Suchen nach Beziehungen {#filter-and-search}

Sie können bestimmte Beziehungen innerhalb Ihrer Schemas über die Registerkarte [!UICONTROL Beziehungen] im Arbeitsbereich [!UICONTROL Schemas] filtern und nach ihnen suchen. Sie können diese Ansicht verwenden, um Ihre Beziehungen schnell zu finden und zu verwalten. Lesen Sie das Dokument unter [Erkunden von Schemaressourcen](../ui/explore.md#lookup) , um detaillierte Anweisungen zu den Filteroptionen zu erhalten.

![Die Registerkarte Beziehungen im Arbeitsbereich &quot;Schemas&quot;.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von [!DNL Schema Editor] erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).
