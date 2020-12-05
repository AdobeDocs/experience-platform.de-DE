---
keywords: Experience Platform;home;popular topics;ui;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create;data type;data types;
solution: Experience Platform
title: Datentypen mithilfe der Benutzeroberfläche der Schema Registry erstellen und bearbeiten
topic: tutorial
type: Tutorial
description: Dieses Lernprogramm verwendet die Benutzeroberfläche der Experience Platform, um Sie durch die Schritte zur Erstellung eines benutzerdefinierten Datentyps zu führen.
translation-type: tm+mt
source-git-commit: 9008b49e1eb5e32b0f4cda7049bf873c689f6442
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---


# Datentypen mithilfe der Benutzeroberfläche &quot;Experience Platform&quot;erstellen und bearbeiten

Im Erlebnis-Datenmodell (XDM) werden Datentypen als Referenztypfelder in Klassen oder Mixins auf die gleiche Weise wie grundlegende Literalfelder verwendet, wobei der Hauptunterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Ähnlich wie Mixins, da sie die einheitliche Verwendung einer Mehrfeldstruktur ermöglichen, sind die Datentypen flexibler, da sie an jeder beliebigen Stelle in der Schema-Struktur enthalten sein können, während Mixins nur auf der Stammebene hinzugefügt werden können.

Adobe Experience Platform bietet viele Standarddatentypen, die für eine Vielzahl von Anwendungsfällen im Rahmen des Erlebnismanagements verwendet werden können. Sie können jedoch auch eigene benutzerdefinierte Datentypen definieren, um Ihren individuellen Geschäftsanforderungen gerecht zu werden.

In diesem Lernprogramm werden die Schritte zum Erstellen und Bearbeiten benutzerdefinierter Datentypen in der Benutzeroberfläche der Plattform beschrieben.

## Voraussetzungen 

Dieses Tutorial erfordert ein funktionierendes Verständnis von XDM System. In der [XDM-Übersicht](../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und die [Grundlagen der Schema-Komposition](../schema/composition.md) , wie Datentypen zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](./-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen des Tutorials vertraut zu machen, obwohl dies für dieses Tutorial nicht erforderlich ist [!DNL Schema Editor].

## Öffnen Sie die [!DNL Schema Editor] für einen Datentyp

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich die Option &quot; **[!UICONTROL Schema]** &quot;, um den Arbeitsbereich &quot; [!UICONTROL Schemas] &quot;zu öffnen, und wählen Sie dann die Registerkarte &quot; **[!UICONTROL Datentypen]** &quot;aus. Es wird eine Liste der verfügbaren Datentypen angezeigt, einschließlich der durch die Adobe definierten und der von Ihrem Unternehmen erstellten.

![](../images/tutorials/create-datatype/data-types-tab.png)

Von hier aus haben Sie zwei Möglichkeiten:

* [Neuen Datentyp erstellen](#create)
* [Wählen Sie einen vorhandenen Datentyp zur Bearbeitung](#edit)

### Create a new data type {#create}

Wählen Sie auf der Registerkarte **[!UICONTROL Datentypen]** die Option Datentyp **[!UICONTROL erstellen]**.

![](../images/tutorials/create-datatype/create.png)

Das [!DNL Schema Editor] Symbol wird angezeigt und zeigt die aktuelle Struktur des neuen Datentyps auf der Arbeitsfläche an. Auf der rechten Seite des Editors können Sie einen Anzeigenamen und eine optionale Beschreibung für den Datentyp angeben. Stellen Sie sicher, dass Sie einen eindeutigen und präzisen Namen für Ihren Datentyp angeben, damit er beim Hinzufügen zu einem Schema identifiziert werden kann.

In diesem Lernprogramm wird ein Datentyp erstellt, der eine Restauranteigenschaft beschreibt, sodass der Datentyp den Anzeigenamen &quot;Restaurant&quot;erhält.

![](../images/tutorials/create-datatype/data-type-properties.png)

Fahren Sie mit dem [nächsten Abschnitt](#add-fields) fort, um dem Datentyp Felder hinzuzufügen.

### Vorhandenen Datentyp bearbeiten

Es können nur benutzerdefinierte Datentypen bearbeitet werden, die von Ihrem Unternehmen definiert wurden. Um die angezeigte Liste einzuschränken, wählen Sie das Filtersymbol (![Filtersymbol](../images/tutorials/create-datatype/filter.png)) aus, um Steuerelemente zum Filtern nach [!UICONTROL Inhaber]anzuzeigen. Wählen Sie **[!UICONTROL Kunde]** , um nur benutzerdefinierte Datentypen anzuzeigen, die Ihrem Unternehmen gehören.

Wählen Sie in der Liste den zu bearbeitenden Datentyp aus, um die rechte Leiste mit den Details des Datentyps zu öffnen. Wählen Sie den Namen des Datentyps in der rechten Leiste aus, um seine Struktur in der [!DNL Schema Editor].

![](../images/tutorials/create-datatype/edit.png)

## hinzufügen von Feldern zum Datentyp {#add-fields}

Um dem Datentyp Beginn hinzuzufügen, wählen Sie auf der Arbeitsfläche das **Pluszeichen (+)** neben dem Stammfeld aus. Darunter wird ein neues Feld angezeigt, und die rechte Leiste wird aktualisiert, um Steuerelemente für das neue Feld anzuzeigen.

![](../images/tutorials/create-datatype/new-field.png)

Verwenden Sie die Steuerelemente in der rechten Leiste, um einen **[!UICONTROL Feldnamen]**, einen **[!UICONTROL Anzeigenamen]** und einen **[!UICONTROL Typ]** für das Feld anzugeben. Beachten Sie, dass der Feldtyp ein einfacher Skalartyp sein kann (z. B. eine Zeichenfolge, eine Ganzzahl oder ein boolescher Typ), oder dass er ein anderer, von der Adobe oder Ihrem Unternehmen definierter Multifield-Datentyp sein kann.

Der Restaurantdatentyp erfordert ein Zeichenfolgenfeld, um den Namen des Restaurants anzugeben. Daher wird der [!UICONTROL Feldname] als &quot;name&quot;und der [!UICONTROL Typ] als [!UICONTROL Zeichenfolge]festgelegt. Wählen Sie &quot; **[!UICONTROL Anwenden]** &quot;, um die Änderungen auf das Feld anzuwenden.

![](../images/tutorials/create-datatype/name-field.png)

Fahren Sie mit demselben Vorgang fort, um weitere Felder hinzuzufügen. Wählen Sie dazu zunächst das **Pluszeichen (+)** neben dem Feld auf der Stammebene und geben Sie die Konfigurationsdetails in der rechten Leiste ein.

Der Datentyp Restaurant verfügt jetzt über zusätzliche Felder für Marke, Sitzkapazität und Bodenfläche.

![](../images/tutorials/create-datatype/more-fields.png)

Neben einfachen Feldern können Sie auch weitere Datentypen innerhalb Ihres benutzerdefinierten Datentyps verschachteln. Der Datentyp &quot;Restaurant&quot;erfordert beispielsweise ein Feld, das die physische Adresse der Eigenschaft darstellt. In diesem Szenario können Sie ein neues Adressfeld hinzufügen, dem der Standarddatentyp &quot;[!UICONTROL Postanschrift]&quot;zugewiesen wurde.

![](../images/tutorials/create-datatype/address-field.png)

Dies zeigt, wie flexible Datentypen im Hinblick auf die Beschreibung Ihrer Daten sein können: Datentypen können Felder verwenden, die auch Datentypen sind, die wiederum weitere Datentypen enthalten können usw. Dadurch können Sie allgemeine Datenmuster in allen XDM-Schemas abstrahieren und wiederverwenden, was die Darstellung komplexer Datenstrukturen erleichtert.

Nachdem Sie alle Felder zum Datentyp hinzugefügt haben, wählen Sie &quot; **[!UICONTROL Speichern]** &quot;, um die Änderungen zu speichern, und fügen Sie den Datentyp zum Datentyp hinzu [!DNL Schema Library].

## hinzufügen des Datentyps zu einer Mischung

Nachdem Sie einen Datentyp erstellt haben, können Sie ihn in Ihren Schemas verwenden. Da XDM-Schema aus einer Klasse und Null oder mehr Mixins bestehen, können von einem Datentyp bereitgestellte Felder einem Schema nicht direkt hinzugefügt werden. Stattdessen müssen sie in eine Klasse oder ein Mixin einbezogen werden.

>[!NOTE]
>
>Dieser Abschnitt konzentriert sich darauf, einen Datentyp zu einer Mischung hinzuzufügen, da dies das häufigste Muster für benutzerdefinierte Datentypen ist. Sie können jedoch auch dieselben Schritte anwenden, um Ihren Datentyp stattdessen einer Klasse hinzuzufügen.

Sie können den Datentyp zu einer vorhandenen Mischung hinzufügen oder eine neue Mischung komplett erstellen. In beiden Fällen müssen Sie die [!DNL Schema Editor] für ein Schema öffnen, dem Sie den neuen Datentyp hinzufügen möchten, entweder durch Auswahl eines vorhandenen Schemas auf der Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;oder durch Erstellung eines neuen Schemas.

Nachdem Sie das Schema in der Leiste geöffnet haben, wählen Sie die Mischung aus, der Sie den Datentyp in der linken Leiste hinzufügen möchten. [!DNL Schema Editor] Wenn das Schema über keine geeignete Mischung verfügt, führen Sie die Schritte aus, um eine neue Mischung [zu](./create-schema-ui.md#define-mixin) erstellen, die dem Schema hinzugefügt werden soll, und stellen Sie sicher, dass die Mischung in der linken Leiste ausgewählt ist.

![](../images/tutorials/create-datatype/mixin-selected.png)

Wählen Sie das **Pluszeichen (+)** neben dem Namen des Schemas aus, um dem ausgewählten Mixin ein neues Feld hinzuzufügen. Wenn Sie die **[!UICONTROL Type]** -Eigenschaft für das Feld auswählen, ist der Name des zuvor erstellten Datentyps jetzt in der Dropdown-Liste verfügbar. Sie können den Beginn eingeben, um den Datentyp einfacher zu finden.

![](../images/tutorials/create-datatype/add-data-type.png)

Wählen Sie Ihren Datentyp aus der Liste und dann **[!UICONTROL Übernehmen]**. Das Feld &quot;Schema&quot;wird auf der Arbeitsfläche aktualisiert und zeigt die vom Datentyp bereitgestellten strukturierten Unterfelder an. Wenn Sie das Schema speichern, indem Sie &quot; **[!UICONTROL Speichern]**&quot;wählen, wird das Mixin ebenfalls gespeichert, sodass Sie das Mixin in weiteren Schemas derselben Klasse wiederverwenden können.

![](../images/tutorials/create-datatype/data-type-added.png)

>[!NOTE]
>
>Mixins sind nur mit einer Klasse kompatibel. Wenn Sie Ihren Datentyp in zusätzlichen Schemas verwenden möchten, die auf unterschiedlichen Klassen basieren, müssen Sie die oben genannten Schritte ausführen, um den Datentyp zu zusätzlichen Mixins hinzuzufügen, die dazu gedacht sind, diese Klassen zu erweitern.

## Nächste Schritte

In diesem Lernprogramm wurde beschrieben, wie Sie Datentypen erstellen und bearbeiten und sie mit der [!DNL Schema Editor]Methode zu Mixins hinzufügen. Weitere Informationen zum Arbeiten mit Datentypen in der Benutzeroberfläche, einschließlich zum Konvertieren eines Objekts mit mehreren Feldern in einen Datentyp, finden Sie im Lernprogramm zur Erstellung von [Schemas](./create-schema-ui.md#datatype).

Informationen zum Erstellen eines Datentyps mithilfe der Schema Registry-API finden Sie im Handbuch [Datentypen-Endpunkt](../api/data-types.md#create).