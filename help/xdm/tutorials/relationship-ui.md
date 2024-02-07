---
keywords: Experience Platform; home; beliebte Themen; ui; UI; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schema Editor; Schema; Schema; Schemas; erstellen; Beziehung; Beziehung; Referenz; Referenz;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 26%

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

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Definieren dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM)-Schemas ermöglichen es Ihnen, komplexe Einblicke in Ihre Kundendaten zu erhalten.

Während Schemabeziehungen durch die Verwendung des Vereinigungsschemas und [!DNL Real-Time Customer Profile] abgeleitet werden können, gilt dies nur für Schemata einer gemeinsamen Klasse. Um eine Beziehung zwischen zwei Schemas herzustellen, die zu verschiedenen Klassen gehören, muss einem Quellschema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität des anderen verwandten Schemas verweist.

>[!NOTE]
>
>Wenn sowohl das Quell- als auch das Zielschema zur gleichen Klasse gehören, sollte ein dediziertes Beziehungsfeld **not** verwendet werden. Verwenden Sie in diesem Fall die Benutzeroberfläche des Vereinigungsschemas , um die Beziehung anzuzeigen. Anweisungen dazu finden Sie im Abschnitt [Anzeigen von Beziehungen](../../profile/ui/union-schema.md#view-relationships) Abschnitt des UI-Handbuchs für Vereinigungsschemas.

Dieses Dokument enthält eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors im [!DNL Experience Platform] -Benutzeroberfläche. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

>[!NOTE]
>
>Anweisungen zum Erstellen einer n:1-Beziehung in Adobe Real-time Customer Data Platform B2B Edition finden Sie im Handbuch unter [Erstellen von B2B-Beziehungen](./relationship-b2b.md).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von [!DNL XDM System] und dem Schema-Editor im [!DNL Experience Platform] Benutzeroberfläche. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und dessen Implementierung in [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemata.
* [Erstellen Sie ein Schema mit dem [!DNL Schema Editor]](create-schema-ui.md): Ein Tutorial zu den Grundlagen der Arbeit mit dem [!DNL Schema Editor].

## Quell- und Referenzschema definieren

Wir gehen davon aus, dass Sie die beiden Schemata, die in der Beziehung definiert werden sollen, bereits erstellt haben. Zu Demonstrationszwecken erstellt dieses Tutorial eine Beziehung zwischen Mitgliedern des Treueprogramms einer Organisation (definiert in einem[!DNL Loyalty Members]&quot; schema) und deren Lieblingshotel (definiert in einem &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schemas definierte primäre Identitäten aufweisen und für [!DNL Real-Time Customer Profile]. Siehe Abschnitt zu [Aktivieren eines Schemas zur Verwendung in Profil](./create-schema-ui.md#profile) im Tutorial zur Erstellung von Schemas , wenn Sie Anleitungen zur entsprechenden Konfiguration Ihrer Schemas benötigen.

Schemabeziehungen werden durch ein dediziertes Feld in einer **Quellschema** , das auf ein anderes Feld in einer **Referenzschema**. In den folgenden Schritten: &quot;[!DNL Loyalty Members]&quot; wird das Quellschema sein, während &quot;[!DNL Hotels]&quot; dient als Referenzschema.

In den folgenden Abschnitten wird die Struktur der einzelnen Schemas beschrieben, die in diesem Tutorial verwendet werden, bevor eine Beziehung definiert wurde.

### [!DNL Loyalty Members] schema

Das Quellschema &quot;[!DNL Loyalty Members]&quot; basiert auf der Variablen [!DNL XDM Individual Profile] -Klasse, die Feld enthält, das Mitglieder eines Treueprogramms beschreibt. Eines dieser Felder, `personalEmail.addess`dient als primäre Identität für das Schema unter [!UICONTROL Email] Namespace. Siehe unter **[!UICONTROL Schemaeigenschaften]** wurde dieses Schema zur Verwendung in [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Das Referenzschema &quot;[!DNL Hotels]&quot; basiert auf einem benutzerspezifischen &quot;[!DNL Hotels]&quot; und enthält Felder, die ein Hotel beschreiben. Um an einer Beziehung teilnehmen zu können, muss das Referenzschema auch über eine primäre Identität verfügen, die definiert und für [!UICONTROL Profil]. In diesem Fall `_tenantId.hotelId`fungiert als primäre Identität für das Schema und verwendet eine benutzerdefinierte[!DNL Hotel ID]&quot;Identitäts-Namespace.

![Profil aktivieren](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Informationen zum Erstellen benutzerdefinierter Identitäts-Namespaces finden Sie im Abschnitt [Dokumentation zu Identity Service](../../identity-service/features/namespaces.md#manage-namespaces).

## Erstellen einer Beziehungsfeldgruppe

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quellschema über kein dediziertes Zeichenfolgenfeld verfügt, das als Zeiger auf die primäre Identität des Referenzschemas verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das die primäre Identität des Referenzschemas angibt. Sie können dieses Feld zum Quellschema hinzufügen, indem Sie eine neue Schemafeldergruppe erstellen oder eine bestehende erweitern.

Im Falle der [!DNL Loyalty Members] Schema, ein neues `preferredHotel` wird hinzugefügt, um das von einem Mitglied des Treueprogramms bevorzugte Hotel für Unternehmensbesuche anzugeben. Wählen Sie zunächst das Pluszeichen (**+**) neben dem Namen des Quellschemas.

![](../images/tutorials/relationship/loyalty-add-field.png)

Auf der Arbeitsfläche wird ein neuer Feld-Platzhalter angezeigt. under **[!UICONTROL Feldeigenschaften]**, geben Sie einen Feldnamen und einen Anzeigenamen für das Feld ein und setzen Sie seinen Typ auf &quot;[!UICONTROL Zeichenfolge]&quot;. under **[!UICONTROL Zuweisen zu]**, wählen Sie eine vorhandene Feldergruppe aus, um sie zu erweitern, oder geben Sie einen eindeutigen Namen ein, um eine neue Feldergruppe zu erstellen. In diesem Fall wird eine neue[!DNL Preferred Hotel]&quot; Feldergruppe erstellt.

![](../images/tutorials/relationship/relationship-field-details.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![](../images/tutorials/relationship/relationship-field-apply.png)

Die aktualisierten `preferredHotel` wird auf der Arbeitsfläche unter einem `_tenantId` -Objekt, da es sich um ein benutzerdefiniertes Feld handelt. Auswählen **[!UICONTROL Speichern]** , um Ihre Schemaänderungen abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definieren eines Beziehungsfelds für das Quellschema {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

>[!NOTE]
>
>Die folgenden Schritte beschreiben, wie Sie ein Beziehungsfeld mithilfe der Steuerelemente in der rechten Leiste auf der Arbeitsfläche definieren. Wenn Sie Zugriff auf Real-Time CDP B2B Edition haben, können Sie auch eine Eins-zu-Eins-Beziehung mithilfe der [Dialogfeld](./relationship-b2b.md#relationship-field) wie beim Erstellen von 1:1-Beziehungen.

Wählen Sie die `preferredHotel` in der Arbeitsfläche und scrollen Sie dann nach unten **[!UICONTROL Feldeigenschaften]** bis zum **[!UICONTROL Beziehung]** wird angezeigt. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Wählen Sie das Dropdown-Menü für **[!UICONTROL Referenzschema]** und wählen Sie das Referenzschema für die Beziehung (&quot;[!DNL Hotels]&quot; in diesem Beispiel). under **[!UICONTROL Referenz-Identitäts-Namespace]**, wählen Sie den Namespace des Identitätsfelds des Referenzschemas aus (in diesem Fall &quot;[!DNL Hotel ID]&quot;). Auswählen **[!UICONTROL Anwenden]** wenn fertig.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Die `preferredHotel` -Feld wird nun auf der Arbeitsfläche als Beziehung hervorgehoben, die den Namen des Referenzschemas anzeigt. Auswählen **[!UICONTROL Speichern]** , um Ihre Änderungen zu speichern und den Workflow abzuschließen.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe der Funktion [!DNL Schema Editor]. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).
