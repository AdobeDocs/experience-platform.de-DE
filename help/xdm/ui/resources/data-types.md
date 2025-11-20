---
keywords: Experience Platform;Startseite;beliebte Themen;UI;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Schema Registry;Schema;Schemas;Schemas;erstellen;Datentyp;Datentypen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform Datentypen erstellen und bearbeiten.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 7%

---

# Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Standard- oder benutzerdefinierte Datentypfilter"
>abstract="Die Liste der verfügbaren Datentypen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Option „Standard“ zeigt die von Adobe erstellten Entitäten an und die Option „Benutzerdefiniert“ zeigt die in Ihrem Unternehmen erstellten Entitäten an. Weitere Informationen zum Erstellen und Bearbeiten von Datentypen finden Sie in der Dokumentation."

Im Experience-Datenmodell (XDM) sind Datentypen wiederverwendbare Felder, die mehrere Unterfelder enthalten. Datentypen ähneln zwar den Schemafeldgruppen insofern, als sie die konsistente Verwendung einer Struktur mit mehreren Feldern ermöglichen, sind aber flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldgruppen nur auf der Stammebene hinzugefügt werden können.

Adobe Experience Platform bietet viele Standarddatentypen, mit denen eine Vielzahl gängiger Anwendungsfälle für die Erlebnisverwaltung abgedeckt werden können. Sie können jedoch auch eigene benutzerdefinierte Datentypen definieren, um Ihre individuellen Geschäftsanforderungen zu erfüllen.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp in einem anderen Schema nicht erstellen. Diese Einschränkung gilt für den Mandanten Ihrer Organisation.

In diesem Tutorial werden die Schritte zum Erstellen und Bearbeiten benutzerdefinierter Datentypen in der Benutzeroberfläche von Experience Platform beschrieben.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Grundverständnis des XDM-Systems voraus. Unter [XDM-Übersicht](../../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und in die [Grundlagen der Schemakomposition](../../schema/composition.md) wie Datentypen zu XDM-Schemata beitragen.

Obwohl dies für dieses Handbuch nicht erforderlich ist, wird empfohlen, auch das Tutorial zum Erstellen [&#x200B; Schemas in der Benutzeroberfläche zu befolgen](../../tutorials/create-schema-ui.md) um sich mit den verschiedenen Funktionen des [!DNL Schema Editor] vertraut zu machen.

## Öffnen der [!DNL Schema Editor] für einen Datentyp {#data-type}

Klicken Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich auf **[!UICONTROL Schemas]** , um den [!UICONTROL Schemas]-Arbeitsbereich zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Data types]** aus. Eine Liste der verfügbaren Datentypen wird angezeigt. Die Liste der Datentypen wird automatisch nach der Art ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die von Adobe definierten Datentypen an. Sie können die Liste auch so filtern, dass die von Ihrem Unternehmen erstellten Listen angezeigt werden.

![Der Arbeitsbereich &quot;[!UICONTROL Schemas]&quot; mit hervorgehobenem [!UICONTROL Schemas] in der linken Navigation und [!UICONTROL Data types].](../../images/ui/resources/data-types/data-types-tab.png)

Von hier aus haben Sie die folgenden Optionen:

- [Erstellen eines neuen Datentyps](#create)
- [Filtern von Datentypen](#filter)
- [Einen vorhandenen Datentyp zum Bearbeiten auswählen](#edit)

### Erstellen eines neuen Datentyps {#create}

Wählen Sie auf der Registerkarte **[!UICONTROL Data types]** die Option **[!UICONTROL Create data type]** aus.

![Die Registerkarte &quot;[!UICONTROL Schemas] Workspace-[!UICONTROL Data types]&quot; mit hervorgehobenem [!UICONTROL Create data type].](../../images/ui/resources/data-types/create.png)

Das [!DNL Schema Editor] wird angezeigt und zeigt die aktuelle Struktur des neuen Datentyps auf der Arbeitsfläche an. Auf der rechten Seite des Editors können Sie einen Anzeigenamen und eine optionale Beschreibung für den Datentyp angeben. Stellen Sie sicher, dass Sie einen eindeutigen und knappen Namen für Ihren Datentyp angeben, da er auf diese Weise identifiziert wird, wenn Sie ihn einem Schema hinzufügen.

In diesem Tutorial wird ein Datentyp erstellt, der eine Restauranteigenschaft beschreibt, sodass dem Datentyp der Anzeigename „Restaurant“ zugewiesen wird.

![](../../images/ui/resources/data-types/data-type-properties.png)

Von hier aus können Sie mit dem [&#x200B; Abschnitt fortfahren](#add-fields) um Felder zum neuen Datentyp hinzuzufügen.

### Filtern von Datentypen {#filter}

Die Liste der verfügbaren Datentypen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen [!UICONTROL Standard] und [!UICONTROL Custom] auszuwählen. Die Option [!UICONTROL Standard] zeigt Entitäten an, die von Adobe erstellt wurden, und die Option [!UICONTROL Custom] zeigt Entitäten an, die in Ihrem Unternehmen erstellt wurden.

![Die Registerkarte &quot;[!UICONTROL Data types]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit hervorgehobenen [!UICONTROL Standard] und [!UICONTROL Custom].](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Bearbeiten eines vorhandenen Datentyps {#edit}

>[!NOTE]
>
>Sobald ein vorhandener Datentyp in einem Schema verwendet wird, das für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, können anschließend nur noch zerstörungsfreie Änderungen an diesem Datentyp vorgenommen werden. Weitere Informationen finden [&#x200B; unter „Regeln &#x200B;](../../schema/composition.md#evolution) Schemaentwicklung“.

Es können nur benutzerdefinierte Datentypen bearbeitet werden, die von Ihrer Organisation definiert wurden. Wählen Sie **[!UICONTROL Custom]** aus, um nur benutzerdefinierte Datentypen anzuzeigen, die Ihrem Unternehmen gehören.

Wählen Sie in der Liste den Datentyp aus, den Sie bearbeiten möchten, um die rechte Leiste mit den Details des Datentyps zu öffnen. Im Detailbereich können Sie auch eine Beispieldatei herunterladen, die JSON-Struktur kopieren oder den Datentyp zu einem Paket hinzufügen.

Wählen Sie den Namen des Datentyps in der rechten Leiste aus, um seine Struktur im [!DNL Schema Editor] zu öffnen.

![Die Registerkarte &quot;[!UICONTROL Data types]&quot; des Arbeitsbereichs &quot;[!UICONTROL Schemas]&quot; mit einem hervorgehobenen Datentyp, [!UICONTROL Custom] und [!UICONTROL Name] Datentyp.](../../images/ui/resources/data-types/edit.png)

## Hinzufügen von Feldern zum Datentyp {#add-fields}

Um Felder zum Datentyp hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **plus (+)** neben dem Feld auf der Stammebene aus. Darunter wird ein neues Feld angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente für das neue Feld anzuzeigen.

![](../../images/ui/resources/data-types/new-field.png)

Verwenden Sie die Steuerelemente in der rechten Leiste, um die Details des neuen Felds zu konfigurieren. Spezifische Schritte zum Konfigurieren [&#x200B; Hinzufügen des Felds zum Datentyp finden &#x200B;](../fields/overview.md#define) im Handbuch unter „Definieren von Feldern in der“.

Der Datentyp Restaurant erfordert ein Zeichenfolgenfeld, das den Namen des Restaurants darstellt. Daher wird der [!UICONTROL Field name] als „Name“ und der [!UICONTROL Type] als &quot;[!UICONTROL String]&quot; festgelegt. Wählen Sie **[!UICONTROL Apply]** aus, um die Änderungen auf das Feld anzuwenden.

![](../../images/ui/resources/data-types/name-field.png)

Fügen Sie dem Datentyp nach Bedarf weitere Felder hinzu. Der Datentyp „Beispiel-Restaurant“ verfügt jetzt über zusätzliche Felder für die Marke, die Sitzplatzkapazität und die Bodenfläche.

![](../../images/ui/resources/data-types/more-fields.png)

Zusätzlich zu den grundlegenden Feldern können Sie auch zusätzliche Datentypen in Ihrem benutzerdefinierten Datentyp verschachteln. Der Datentyp Restaurant erfordert beispielsweise ein Feld, das die physische Adresse der Eigenschaft darstellt. In diesem Szenario können Sie ein neues Feld „Adresse“ hinzufügen, dem der Standarddatentyp &quot;[!UICONTROL Postal address]&quot; zugewiesen ist.

![](../../images/ui/resources/data-types/address-field.png)

Dies zeigt, wie flexibel Datentypen in Bezug auf die Beschreibung Ihrer Daten sein können: Datentypen können Felder verwenden, die auch Datentypen sind, die selbst weitere Datentypen enthalten können usw. Auf diese Weise können Sie gängige Datenmuster in Ihren XDM-Schemata abstrahieren und wiederverwenden, was die Darstellung komplexer Datenstrukturen erleichtert.

Nachdem Sie dem Datentyp Felder hinzugefügt haben, wählen Sie **[!UICONTROL Save]** aus, um Ihre Änderungen zu speichern und den Datentyp zum [!DNL Schema Library] hinzuzufügen.

## Hinzufügen des Datentyps zu einem Schema {#add-data-type}

Nachdem Sie einen Datentyp erstellt haben, können Sie ihn in Ihren Schemata verwenden. Da XDM-Schemata aus einer Klasse und keiner oder mehreren Feldergruppen bestehen, können von einem Datentyp bereitgestellte Felder nicht direkt zu einem Schema hinzugefügt werden. Stattdessen müssen sie in eine Klasse oder Feldergruppe aufgenommen werden.

Führen Sie zunächst die Schritte aus, die mit dem [Hinzufügen eines Felds zu einer &#x200B;](./classes.md#add-fields) oder [Hinzufügen eines Felds zu einer Feldergruppe“ &#x200B;](./field-groups.md#add-fields) sind. Alternativ können Sie mit dem [Hinzufügen eines Felds direkt zu einem Schema](./schemas.md#add-individual-fields) beginnen und dort die übergeordnete Klasse oder Feldergruppe auswählen. Wenn Sie die **[!UICONTROL Type]** für das neue Feld auswählen, wählen Sie den Namen Ihres Datentyps aus dem Dropdown-Menü aus.

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#convert}

Wenn Sie ein Feld vom Typ „Objekt“ mit mehreren Unterfeldern im [!DNL Schema Editor] erstellen, können Sie dieses Feld in einen Datentyp konvertieren, damit Sie dieselbe Feldstruktur in einer anderen Klasse oder Feldergruppe verwenden können.

Um ein Feld vom Typ „Objekt“ in einen Datentyp zu konvertieren, wählen Sie das Feld auf der Arbeitsfläche aus. Bevor Sie das Feld konvertieren, stellen Sie sicher, dass die **[!UICONTROL Display name]** die Daten beschreibt, die das Objekt enthalten wird, da dies der Name des Datentyps wird. Wenn Sie bereit sind, das Feld zu konvertieren, wählen Sie **[!UICONTROL Convert to new data type]** in der rechten Leiste aus.

![](../../images/ui/resources/data-types/convert-object.png)

Die Arbeitsfläche aktualisiert den Datentyp des Felds von &quot;[!UICONTROL Object]&quot; auf den neuen Datentyp. Diese Struktur kann jetzt in anderen Klassen und Feldergruppen wiederverwendet werden, indem dieser Datentyp beim Definieren eines neuen Felds aus dem Dropdown-Menü &quot;**[!UICONTROL Type]**&quot; ausgewählt wird.

![](../../images/ui/resources/data-types/converted.png)

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Datentypen mithilfe der Experience Platform-Benutzeroberfläche erstellen und bearbeiten. Weiterführende Informationen zu den Funktionen von [!UICONTROL Schemas] Workspace finden Sie in der Übersicht zu [[!UICONTROL Schemas] Workspace &#x200B;](../overview.md).

Informationen zum Verwalten von Datentypen mit der [!DNL Schema Registry]-API finden Sie im [Handbuch zu Datentypendpunkten](../../api/data-types.md).
