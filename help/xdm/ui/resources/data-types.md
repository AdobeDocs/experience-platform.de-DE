---
keywords: Experience Platform; Startseite; beliebte Themen; ui; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Schemaregistrierung; Schema; Schema; Schemas; Erstellen; Datentyp; Datentypen
solution: Experience Platform
title: Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche
topic-legacy: tutorial
type: Tutorial
description: Erfahren Sie, wie Sie Datentypen in der Benutzeroberfläche von Experience Platform erstellen und bearbeiten.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 14128b247b003a54cb0d91167bb46fccf16ed799
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Erstellen und Bearbeiten von Datentypen über die Benutzeroberfläche

Im Experience-Datenmodell (XDM) sind Datentypen wiederverwendbare Felder, die mehrere Unterfelder enthalten. Auch wenn sie Schemafeldgruppen insofern ähneln, als sie die konsistente Verwendung einer Mehrfeld-Struktur ermöglichen, sind Datentypen flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldergruppen nur auf der Stammebene hinzugefügt werden können.

Adobe Experience Platform bietet viele Standarddatentypen, mit denen eine Vielzahl gängiger Anwendungsfälle für das Erlebnismanagement abgedeckt werden kann. Sie können jedoch auch eigene benutzerdefinierte Datentypen definieren, um Ihren individuellen Geschäftsanforderungen gerecht zu werden.

In diesem Tutorial werden die Schritte zum Erstellen und Bearbeiten benutzerdefinierter Datentypen in der Benutzeroberfläche von Platform beschrieben.

## Voraussetzungen  

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , wie Datentypen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Öffnen Sie [!DNL Schema Editor] für einen Datentyp.

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Schemas]** im linken Navigationsbereich aus, um den Arbeitsbereich [!UICONTROL Schemas] zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Datentypen]** aus. Es wird eine Liste der verfügbaren Datentypen angezeigt, einschließlich der von der Adobe definierten und der von Ihrer Organisation erstellten Datentypen.

![](../../images/ui/resources/data-types/data-types-tab.png)

Von hier aus haben Sie zwei Möglichkeiten:

- [Neuen Datentyp erstellen](#create)
- [Wählen Sie einen vorhandenen Datentyp aus, um ihn zu bearbeiten](#edit)

### Neuen Datentyp erstellen {#create}

Wählen Sie auf der Registerkarte **[!UICONTROL Datentypen]** die Option **[!UICONTROL Datentyp erstellen]**.

![](../../images/ui/resources/data-types/create.png)

Der [!DNL Schema Editor] wird angezeigt und zeigt die aktuelle Struktur des neuen Datentyps auf der Arbeitsfläche an. Auf der rechten Seite des Editors können Sie einen Anzeigenamen und eine optionale Beschreibung für den Datentyp angeben. Stellen Sie sicher, dass Sie einen eindeutigen und präzisen Namen für Ihren Datentyp angeben, da dieser beim Hinzufügen zu einem Schema identifiziert wird.

In diesem Tutorial wird ein Datentyp erstellt, der eine Restauranteigenschaft beschreibt, sodass der Datentyp den Anzeigenamen &quot;Restaurant&quot;erhält.

![](../../images/ui/resources/data-types/data-type-properties.png)

Von hier aus können Sie zum nächsten Abschnitt [](#add-fields) überspringen, um Felder zum neuen Datentyp hinzuzufügen.

### Vorhandenen Datentyp bearbeiten

>[!NOTE]
>
>Sobald ein vorhandener Datentyp in einem Schema verwendet wird, das für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, können anschließend nur zerstörungsfreie Änderungen an diesem Datentyp vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Es können nur benutzerdefinierte Datentypen bearbeitet werden, die von Ihrem Unternehmen definiert wurden. Um die angezeigte Liste einzuschränken, wählen Sie das Filtersymbol (![Filtersymbol](../../images/ui/resources/data-types/filter.png)) aus, um die Steuerelemente zum Filtern anhand von [!UICONTROL Inhaber] anzuzeigen. Wählen Sie **[!UICONTROL Customer]** aus, um nur benutzerdefinierte Datentypen anzuzeigen, die Ihrem Unternehmen gehören.

Wählen Sie in der Liste den zu bearbeitenden Datentyp aus, um die rechte Leiste mit Details zum Datentyp zu öffnen. Wählen Sie den Namen des Datentyps in der rechten Leiste aus, um seine Struktur in [!DNL Schema Editor] zu öffnen.

![](../../images/ui/resources/data-types/edit.png)

## Felder zum Datentyp {#add-fields} hinzufügen

Um dem Datentyp Felder hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **plus (+)** neben dem Feld auf der Stammebene aus. Unten wird ein neues Feld angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente für das neue Feld anzuzeigen.

![](../../images/ui/resources/data-types/new-field.png)

Verwenden Sie die Steuerelemente in der rechten Leiste, um die Details des neuen Felds zu konfigurieren. Spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zum Datentyp finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) .

Der Datentyp Restaurant erfordert ein Zeichenfolgenfeld, das den Namen des Restaurants darstellt. Daher wird [!UICONTROL Feldname] als &quot;name&quot;und [!UICONTROL Typ] als &quot;[!UICONTROL String]&quot;festgelegt. Wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderungen auf das Feld anzuwenden.

![](../../images/ui/resources/data-types/name-field.png)

Fügen Sie dem Datentyp nach Bedarf weitere Felder hinzu. Der Beispieldatentyp Restaurant enthält jetzt zusätzliche Felder für Marke, Sitzkapazität und Bodenfläche.

![](../../images/ui/resources/data-types/more-fields.png)

Zusätzlich zu den grundlegenden Feldern können Sie auch zusätzliche Datentypen in Ihrem benutzerdefinierten Datentyp verschachteln. Beispielsweise erfordert der Datentyp Restaurant ein Feld, das die physische Adresse der Eigenschaft darstellt. In diesem Szenario können Sie ein neues Feld &quot;Adresse&quot;hinzufügen, dem der Standarddatentyp &quot;[!UICONTROL Postanschrift]&quot;zugewiesen ist.

![](../../images/ui/resources/data-types/address-field.png)

Dies zeigt, wie flexible Datentypen in Bezug auf die Beschreibung Ihrer Daten sein können: -Datentypen können Felder verwenden, die auch Datentypen sind, die wiederum weitere Datentypen enthalten können, usw. Auf diese Weise können Sie allgemeine Datenmuster in Ihren XDM-Schemas abstrahieren und wiederverwenden, um die Darstellung komplexer Datenstrukturen zu vereinfachen.

Nachdem Sie die Felder zum Datentyp hinzugefügt haben, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu speichern und den Datentyp zum [!DNL Schema Library] hinzuzufügen.

## Hinzufügen des Datentyps zu einer Klasse oder Feldergruppe

Nachdem Sie einen Datentyp erstellt haben, können Sie ihn in Ihren Schemata verwenden. Da XDM-Schemas aus einer Klasse und null oder mehr Feldgruppen bestehen, können von einem Datentyp bereitgestellte Felder nicht direkt zu einem Schema hinzugefügt werden. Stattdessen müssen sie in eine Klasse oder Feldergruppe eingeschlossen sein.

Führen Sie zunächst die Schritte aus, die für das Hinzufügen eines Felds zu einer Klasse](./classes.md#add-fields) oder [Hinzufügen eines Felds zu einer Feldergruppe](./field-groups.md#add-fields) erforderlich sind. [ Wenn Sie **[!UICONTROL Typ]** für das neue Feld auswählen, wählen Sie den Namen Ihres Datentyps aus dem Dropdown-Menü aus.

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#convert}

Wenn Sie ein Feld vom Typ Objekt mit mehreren Unterfeldern im [!DNL Schema Editor] erstellen, können Sie dieses Feld in einen Datentyp konvertieren, sodass Sie dieselbe Feldstruktur in einer anderen Klasse oder Feldergruppe verwenden können.

Um ein Feld vom Typ Objekt in einen Datentyp zu konvertieren, wählen Sie das Feld auf der Arbeitsfläche aus. Stellen Sie vor dem Konvertieren des Felds sicher, dass der **[!UICONTROL Anzeigename]** die Daten beschreibt, die das Objekt enthalten wird, da dies zum Namen des Datentyps wird. Wenn Sie bereit sind, das Feld zu konvertieren, wählen Sie in der rechten Leiste **[!UICONTROL In neuen Datentyp konvertieren]** aus.

![](../../images/ui/resources/data-types/convert-object.png)

Die Arbeitsfläche aktualisiert den Datentyp des Felds von &quot;[!UICONTROL Object]&quot;auf den neuen Datentyp. Neben den Unterfeldern befinden sich auch kleine Sperrsymbole, die darauf hinweisen, dass es sich nicht mehr um einzelne Felder, sondern um Bereiche mit mehreren Feldern handelt. Diese Struktur kann jetzt in anderen Klassen und Feldergruppen wiederverwendet werden, indem Sie diesen Datentyp beim Definieren eines neuen Felds aus der Dropdown-Liste **[!UICONTROL Typ]** auswählen.

![](../../images/ui/resources/data-types/converted.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datentypen mithilfe der Platform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie unter [[!UICONTROL Schemas] Workspace - Übersicht](../overview.md).

Informationen zum Verwalten von Datentypen mithilfe der [!DNL Schema Registry]-API finden Sie im [Endpunkthandbuch für Datentypen](../../api/data-types.md).
