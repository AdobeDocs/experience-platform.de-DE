---
keywords: Experience Platform;Home;beliebte Themen;ui;XDM;XDM-System;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Schema;Schema;Schemas;Schemas;Erstellen;Datentyp;Datentypen;
solution: Experience Platform
title: Datentypen mithilfe der Benutzeroberfläche erstellen und bearbeiten
topic-legacy: tutorial
type: Tutorial
description: Erfahren Sie, wie Sie Datentypen in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Datentypen mithilfe der Benutzeroberfläche erstellen und bearbeiten

Im Erlebnis-Datenmodell (XDM) werden Datentypen in Klassen oder Schema-Feldgruppen ebenso wie einfache Literalfelder als Referenztypfelder verwendet, wobei der Hauptunterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Die Datentypen sind ähnlich wie Feldgruppen, da sie eine einheitliche Verwendung einer mehrfeldigen Struktur ermöglichen, flexibler, da sie an jeder beliebigen Stelle in der Schema-Struktur enthalten sein können, während Feldgruppen nur auf der Stammebene hinzugefügt werden können.

Adobe Experience Platform bietet viele Standarddatentypen, die für eine Vielzahl von Anwendungsfällen im Rahmen des Erlebnismanagements verwendet werden können. Sie können jedoch auch eigene benutzerdefinierte Datentypen definieren, um Ihren individuellen Geschäftsanforderungen gerecht zu werden.

In diesem Lernprogramm werden die Schritte zum Erstellen und Bearbeiten benutzerdefinierter Datentypen in der Benutzeroberfläche der Plattform beschrieben.

## Voraussetzungen 

Dieses Handbuch erfordert ein funktionierendes Verständnis des XDM-Systems. Eine Einführung in die Rolle von XDM innerhalb des Experience Platform-Ökosystems finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schema-Komposition](../../schema/composition.md), wie Datentypen zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Öffnen Sie [!DNL Schema Editor] für einen Datentyp

Wählen Sie in der Plattformbenutzeroberfläche **[!UICONTROL Schema]** in der linken Navigation aus, um den Arbeitsbereich [!UICONTROL Schema] zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Datentypen]**. Es wird eine Liste der verfügbaren Datentypen angezeigt, einschließlich der durch die Adobe definierten und der von Ihrem Unternehmen erstellten.

![](../../images/ui/resources/data-types/data-types-tab.png)

Von hier aus haben Sie zwei Möglichkeiten:

- [Neuen Datentyp erstellen](#create)
- [Wählen Sie einen vorhandenen Datentyp zur Bearbeitung](#edit)

### Neuen Datentyp {#create} erstellen

Wählen Sie auf der Registerkarte **[!UICONTROL Datentypen]** **[!UICONTROL Datentyp erstellen]**.

![](../../images/ui/resources/data-types/create.png)

Das Symbol [!DNL Schema Editor] wird angezeigt und zeigt die aktuelle Struktur des neuen Datentyps auf der Arbeitsfläche an. Auf der rechten Seite des Editors können Sie einen Anzeigenamen und eine optionale Beschreibung für den Datentyp angeben. Stellen Sie sicher, dass Sie einen eindeutigen und präzisen Namen für Ihren Datentyp angeben, damit er beim Hinzufügen zu einem Schema identifiziert werden kann.

In diesem Lernprogramm wird ein Datentyp erstellt, der eine Restauranteigenschaft beschreibt, sodass der Datentyp den Anzeigenamen &quot;Restaurant&quot;erhält.

![](../../images/ui/resources/data-types/data-type-properties.png)

Von hier aus können Sie mit dem [nächsten Abschnitt](#add-fields) fortfahren, um dem neuen Datentyp Beginn hinzuzufügen.

### Vorhandenen Datentyp bearbeiten

Es können nur benutzerdefinierte Datentypen bearbeitet werden, die von Ihrem Unternehmen definiert wurden. Um die angezeigte Liste einzuschränken, wählen Sie das Filtersymbol (![Filtersymbol](../../images/ui/resources/data-types/filter.png)) aus, um Steuerelemente zum Filtern anzuzeigen, die auf [!UICONTROL Inhaber] basieren. Wählen Sie **[!UICONTROL Kunde]** aus, um nur benutzerdefinierte Datentypen anzuzeigen, die Ihrem Unternehmen gehören.

Wählen Sie in der Liste den zu bearbeitenden Datentyp aus, um die rechte Leiste mit den Details des Datentyps zu öffnen. Wählen Sie den Namen des Datentyps in der rechten Leiste aus, um seine Struktur in [!DNL Schema Editor] zu öffnen.

![](../../images/ui/resources/data-types/edit.png)

## hinzufügen Felder zum Datentyp {#add-fields}

Um dem Datentyp Beginn hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Stammfeld auf der Arbeitsfläche aus. Darunter wird ein neues Feld angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente für das neue Feld anzuzeigen.

![](../../images/ui/resources/data-types/new-field.png)

Verwenden Sie die Steuerelemente in der rechten Leiste, um die Details des neuen Felds zu konfigurieren. Genaue Schritte zum Konfigurieren und Hinzufügen des Felds zum Datentyp finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define).

Der Restaurantdatentyp erfordert ein Zeichenfolgenfeld, um den Namen des Restaurants anzugeben. Daher wird [!UICONTROL Feldname] als &quot;name&quot;und [!UICONTROL Typ] als &quot;[!UICONTROL String]&quot;festgelegt. Wählen Sie **[!UICONTROL Anwenden]**, um die Änderungen auf das Feld anzuwenden.

![](../../images/ui/resources/data-types/name-field.png)

Fügen Sie dem Datentyp nach Bedarf weitere Felder hinzu. Der Beispieldatentyp Restaurant verfügt jetzt über zusätzliche Felder für Marke, Sitzkapazität und Bodenfläche.

![](../../images/ui/resources/data-types/more-fields.png)

Neben einfachen Feldern können Sie auch weitere Datentypen innerhalb Ihres benutzerdefinierten Datentyps verschachteln. Der Datentyp &quot;Restaurant&quot;erfordert beispielsweise ein Feld, das die physische Adresse der Eigenschaft darstellt. In diesem Szenario können Sie ein neues Adressfeld hinzufügen, dem der Standarddatentyp &quot;[!UICONTROL Postadresse]&quot;zugewiesen ist.

![](../../images/ui/resources/data-types/address-field.png)

Dies zeigt, wie flexible Datentypen im Hinblick auf die Beschreibung Ihrer Daten sein können: Datentypen können Felder verwenden, die auch Datentypen sind, die wiederum weitere Datentypen enthalten können usw. Dadurch können Sie allgemeine Datenmuster in allen XDM-Schemas abstrahieren und wiederverwenden, was die Darstellung komplexer Datenstrukturen erleichtert.

Nachdem Sie die Felder zum Datentyp hinzugefügt haben, wählen Sie **[!UICONTROL Speichern]**, um die Änderungen zu speichern, und fügen Sie den Datentyp zum [!DNL Schema Library] hinzu.

## hinzufügen des Datentyps zu einer Klasse oder Feldgruppe

Nachdem Sie einen Datentyp erstellt haben, können Sie ihn in Ihren Schemas verwenden. Da XDM-Schema aus einer Klasse und null oder mehr Feldgruppen bestehen, können von einem Datentyp bereitgestellte Felder nicht direkt zu einem Schema hinzugefügt werden. Stattdessen müssen sie in eine Klasse oder Feldgruppe aufgenommen werden.

Beginn, indem Sie die Schritte ausführen, die beim Hinzufügen eines Felds zu einer Klasse](./classes.md#add-fields) oder [Hinzufügen eines Felds zu einer Feldgruppe](./field-groups.md#add-fields) erforderlich sind. [ Wenn Sie für das neue Feld **[!UICONTROL Typ]** wählen, wählen Sie den Namen Ihres Datentyps aus dem Dropdown-Menü.

## Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp {#convert}

Wenn Sie ein Objekt-Typ-Feld mit mehreren Unterfeldern in [!DNL Schema Editor] erstellen, können Sie dieses Feld in einen Datentyp konvertieren, sodass Sie dieselbe Feldstruktur in einer anderen Klasse oder Feldgruppe verwenden können.

Um ein Objekttypfeld in einen Datentyp zu konvertieren, wählen Sie das Feld auf der Arbeitsfläche aus. Bevor Sie das Feld konvertieren, stellen Sie sicher, dass der **[!UICONTROL Anzeigename]** die Daten beschreibt, die das Objekt enthalten soll, da dies der Name des Datentyps wird. Wenn Sie bereit sind, das Feld zu konvertieren, wählen Sie in der rechten Leiste **[!UICONTROL In neuen Datentyp]** konvertieren.

![](../../images/ui/resources/data-types/convert-object.png)

Die Arbeitsfläche aktualisiert den Datentyp des Felds von &quot;[!UICONTROL Object]&quot;auf den neuen Datentyp. Neben den Unterfeldern befinden sich auch kleine Sperrsymbole, die darauf hinweisen, dass es sich nicht mehr um einzelne Felder, sondern um einen Datentyp mit mehreren Feldern handelt. Diese Struktur kann jetzt in anderen Klassen und Feldgruppen wiederverwendet werden, indem dieser Datentyp aus der Dropdownliste **[!UICONTROL Typ]** ausgewählt wird, wenn ein neues Feld definiert wird.

![](../../images/ui/resources/data-types/converted.png)

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie Datentypen mithilfe der Plattform-Benutzeroberfläche erstellen und bearbeiten. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](../overview.md).

Informationen zum Verwalten von Datentypen mit der API finden Sie im [!DNL Schema Registry]-Endpunktleitfaden [Datentypen](../../api/data-types.md).
