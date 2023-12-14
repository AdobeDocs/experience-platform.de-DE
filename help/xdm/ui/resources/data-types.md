---
keywords: Experience Platform; home; beliebte Themen; ui; XDM; XDM; XDM-System; Erlebnisdatenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema; Schema; Schemas; Schemas; erstellen; Datentyp; Datentypen
solution: Experience Platform
title: Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie Datentypen in der Experience Platform-Benutzeroberfläche erstellen und bearbeiten.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 6%

---

# Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Standard- oder benutzerdefinierte Datentypfilter"
>abstract="Die Liste der verfügbaren Datentypen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen den Optionen „Standard“ und „Benutzerdefiniert“ zu wählen. Die Option „Standard“ zeigt die von Adobe erstellten Entitäten an und die Option „Benutzerdefiniert“ zeigt die in Ihrem Unternehmen erstellten Entitäten an. Weitere Informationen zum Erstellen und Bearbeiten von Datentypen finden Sie in der Dokumentation."

Im Experience-Datenmodell (XDM) sind Datentypen wiederverwendbare Felder, die mehrere Unterfelder enthalten. Auch wenn sie Schemafeldgruppen insofern ähneln, als sie die konsistente Verwendung einer Mehrfeld-Struktur ermöglichen, sind Datentypen flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldgruppen nur auf der Stammebene hinzugefügt werden können.

Adobe Experience Platform bietet viele Standarddatentypen, mit denen eine Vielzahl gängiger Anwendungsfälle für das Erlebnismanagement abgedeckt werden kann. Sie können jedoch auch eigene benutzerdefinierte Datentypen definieren, um Ihren individuellen Geschäftsanforderungen gerecht zu werden.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp nicht in einem anderen Schema erstellen. Diese Einschränkung gilt für den gesamten Mandanten Ihres Unternehmens.

In diesem Tutorial werden die Schritte zum Erstellen und Bearbeiten benutzerdefinierter Datentypen in der Benutzeroberfläche von Platform beschrieben.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und [Grundlagen der Schemakomposition](../../schema/composition.md) für den Beitrag von Datentypen zu XDM-Schemas.

Für dieses Handbuch ist zwar nicht erforderlich, es wird jedoch empfohlen, auch das Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) sich mit den verschiedenen Fähigkeiten der [!DNL Schema Editor].

## Öffnen Sie die [!DNL Schema Editor] für einen Datentyp {#data-type}

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Schemas]** im linken Navigationsbereich, um die [!UICONTROL Schemas] Arbeitsbereich und wählen Sie dann die **[!UICONTROL Datentypen]** Registerkarte. Eine Liste der verfügbaren Datentypen wird angezeigt. Die Liste der Datentypen wird automatisch nach ihrer Erstellung gefiltert. Die Standardeinstellung zeigt die durch Adobe definierten Datentypen an. Sie können die Liste auch filtern, um die von Ihrer Organisation erstellten anzuzeigen.

![Die [!UICONTROL Schemas] Arbeitsbereich mit [!UICONTROL Schemas] in der linken Navigation und [!UICONTROL Datentypen] hervorgehoben.](../../images/ui/resources/data-types/data-types-tab.png)

Von hier aus haben Sie die folgenden Optionen:

- [Neuen Datentyp erstellen](#create)
- [Datentypen filtern](#filter)
- [Wählen Sie einen vorhandenen Datentyp aus, um ihn zu bearbeiten](#edit)

### Neuen Datentyp erstellen {#create}

Aus dem **[!UICONTROL Datentypen]** Registerkarte auswählen **[!UICONTROL Erstellen eines Datentyps]**.

![Die [!UICONTROL Schemas] Arbeitsbereich [!UICONTROL Datentypen] Registerkarte mit [!UICONTROL Erstellen eines Datentyps] hervorgehoben.](../../images/ui/resources/data-types/create.png)

Die [!DNL Schema Editor] angezeigt, was die aktuelle Struktur des neuen Datentyps auf der Arbeitsfläche anzeigt. Auf der rechten Seite des Editors können Sie einen Anzeigenamen und eine optionale Beschreibung für den Datentyp angeben. Stellen Sie sicher, dass Sie einen eindeutigen und präzisen Namen für Ihren Datentyp angeben, da dieser beim Hinzufügen zu einem Schema identifiziert wird.

In diesem Tutorial wird ein Datentyp erstellt, der eine Restauranteigenschaft beschreibt, sodass der Datentyp den Anzeigenamen &quot;Restaurant&quot;erhält.

![](../../images/ui/resources/data-types/data-type-properties.png)

Von hier aus können Sie zum [nächster Abschnitt](#add-fields) , um dem neuen Datentyp Felder hinzuzufügen.

### Datentypen filtern {#filter}

Die Liste der verfügbaren Datentypen wird je nach ihrer Erstellung vorab gefiltert. Wählen Sie das Optionsfeld aus, um zwischen dem [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] Optionen. Die [!UICONTROL Standard] -Option zeigt die von Adobe erstellten Entitäten an und [!UICONTROL Benutzerdefiniert] -Option zeigt Entitäten an, die innerhalb Ihres Unternehmens erstellt wurden.

![Die [!UICONTROL Datentypen] des [!UICONTROL Schemas] Arbeitsbereich mit [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert] hervorgehoben.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Vorhandenen Datentyp bearbeiten {#edit}

>[!NOTE]
>
>Sobald ein vorhandener Datentyp in einem Schema verwendet wird, das für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, können anschließend nur zerstörungsfreie Änderungen an diesem Datentyp vorgenommen werden. Siehe [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) für weitere Informationen.

Es können nur benutzerdefinierte Datentypen bearbeitet werden, die von Ihrem Unternehmen definiert wurden. Auswählen **[!UICONTROL Benutzerdefiniert]** , um nur benutzerdefinierte Datentypen anzuzeigen, die Ihrem Unternehmen gehören.

Wählen Sie in der Liste den zu bearbeitenden Datentyp aus, um die rechte Leiste mit Details zum Datentyp zu öffnen. Im Detailbereich können Sie auch eine Beispieldatei herunterladen, die JSON-Struktur kopieren oder den Datentyp zu einem Paket hinzufügen.

Wählen Sie den Namen des Datentyps in der rechten Leiste aus, um seine Struktur in der [!DNL Schema Editor].

![Die [!UICONTROL Datentypen] des [!UICONTROL Schemas] Arbeitsbereich mit Datentyp, [!UICONTROL Benutzerdefiniert] und dem Datentyp [!UICONTROL Name] hervorgehoben.](../../images/ui/resources/data-types/edit.png)

## Felder zum Datentyp hinzufügen {#add-fields}

Um dem Datentyp Felder hinzuzufügen, wählen Sie die **plus (+)** neben dem Feld der Stammebene auf der Arbeitsfläche. Unten wird ein neues Feld angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente für das neue Feld anzuzeigen.

![](../../images/ui/resources/data-types/new-field.png)

Konfigurieren Sie mithilfe der Steuerelemente in der rechten Leiste die Details des neuen Felds. Siehe Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) für spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zum Datentyp.

Der Datentyp Restaurant erfordert ein Zeichenfolgenfeld, das den Namen des Restaurants darstellt. Die [!UICONTROL Feldname] auf &quot;name&quot;festgelegt ist und die [!UICONTROL Typ] festgelegt als[!UICONTROL Zeichenfolge]&quot;. Auswählen **[!UICONTROL Anwenden]** , um die Änderungen auf das Feld anzuwenden.

![](../../images/ui/resources/data-types/name-field.png)

Fügen Sie dem Datentyp nach Bedarf weitere Felder hinzu. Der Beispieldatentyp Restaurant enthält jetzt zusätzliche Felder für Marke, Sitzkapazität und Bodenfläche.

![](../../images/ui/resources/data-types/more-fields.png)

Zusätzlich zu den grundlegenden Feldern können Sie auch zusätzliche Datentypen in Ihrem benutzerdefinierten Datentyp verschachteln. Beispielsweise erfordert der Datentyp Restaurant ein Feld, das die physische Adresse der Eigenschaft darstellt. In diesem Szenario können Sie ein neues Feld &quot;Adresse&quot;hinzufügen, dem der Standarddatentyp &quot;[!UICONTROL Postanschrift]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Dies zeigt, wie flexible Datentypen in Bezug auf die Beschreibung Ihrer Daten sein können: Datentypen können Felder verwenden, die auch Datentypen sind, die wiederum weitere Datentypen enthalten können usw. Auf diese Weise können Sie allgemeine Datenmuster in Ihren XDM-Schemas abstrahieren und wiederverwenden, um die Darstellung komplexer Datenstrukturen zu vereinfachen.

Nachdem Sie alle Felder zum Datentyp hinzugefügt haben, wählen Sie **[!UICONTROL Speichern]** , um Ihre Änderungen zu speichern und den Datentyp zum [!DNL Schema Library].

## Datentyp zu einem Schema hinzufügen

Nachdem Sie einen Datentyp erstellt haben, können Sie ihn in Ihren Schemata verwenden. Da XDM-Schemas aus einer Klasse und null oder mehr Feldgruppen bestehen, können von einem Datentyp bereitgestellte Felder nicht direkt zu einem Schema hinzugefügt werden. Stattdessen müssen sie in eine Klasse oder Feldergruppe eingeschlossen sein.

Führen Sie zunächst die mit [Hinzufügen eines Felds zu einer Klasse](./classes.md#add-fields) oder [Feld zu einer Feldergruppe hinzufügen](./field-groups.md#add-fields). Alternativ können Sie [Hinzufügen eines Felds direkt zu einem Schema](./schemas.md#add-individual-fields) und wählen Sie dort die übergeordnete Klasse oder Feldergruppe aus. Wenn Sie die **[!UICONTROL Typ]** für das neue Feld den Namen Ihres Datentyps aus dem Dropdown-Menü auswählen.

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#convert}

Wenn Sie ein Objekt mit mehreren Unterfeldern im [!DNL Schema Editor]können Sie dieses Feld in einen Datentyp konvertieren, sodass Sie dieselbe Feldstruktur in einer anderen Klasse oder Feldergruppe verwenden können.

Um ein Feld vom Typ Objekt in einen Datentyp zu konvertieren, wählen Sie das Feld auf der Arbeitsfläche aus. Stellen Sie vor dem Konvertieren des Felds sicher, dass die Variable **[!UICONTROL Anzeigename]** beschreibt die Daten, die das Objekt enthalten wird, da dies zum Namen des Datentyps wird. Wenn Sie bereit sind, das Feld zu konvertieren, wählen Sie **[!UICONTROL In neuen Datentyp konvertieren]** in der rechten Leiste.

![](../../images/ui/resources/data-types/convert-object.png)

Die Arbeitsfläche aktualisiert den Datentyp des Felds von[!UICONTROL Objekt]&quot; auf den neuen Datentyp hinzu. Diese Struktur kann jetzt in anderen Klassen und Feldergruppen wiederverwendet werden, indem Sie diesen Datentyp aus der **[!UICONTROL Typ]** bei der Definition eines neuen Felds.

![](../../images/ui/resources/data-types/converted.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datentypen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).

Informationen zum Verwalten von Datentypen mithilfe des [!DNL Schema Registry] API, siehe [Endleitfaden für Datentypen](../../api/data-types.md).
