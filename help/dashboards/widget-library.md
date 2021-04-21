---
keywords: Experience Platform;Benutzeroberfläche;Benutzeroberfläche;Dashboards;Dashboard;Profil;Segmente;Ziele;Lizenzverwendung
title: Verwenden der Widget-Bibliothek zum Hinzufügen und Erstellen von Dashboard-Widgets
description: 'Dieses Handbuch enthält schrittweise Anleitungen zum Hinzufügen von Standard-Widgets und zum Erstellen benutzerdefinierter Widgets zur Visualisierung von Dashboard-Daten in Adobe Experience Platform. '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 1%

---

# (Beta) Widget-Bibliothek {#widget-library}

>[!IMPORTANT]
>
>Die Dashboard-Funktionalität befindet sich derzeit in der Beta-Version und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Auf der Adobe Experience Platform-Benutzeroberfläche können Sie die Daten Ihres Unternehmens mit mehreren Dashboards Ansicht und Interaktion ausführen. Sie können einige dieser Dashboard auch aktualisieren, indem Sie Ihrer Dashboard-Ansicht neue Widgets hinzufügen. Zusätzlich zu den von der Adobe bereitgestellten Standard-Widgets können Sie benutzerdefinierte Widgets erstellen und sie in Ihrem gesamten Unternehmen freigeben.

Dieses Handbuch enthält schrittweise Anleitungen zum Hinzufügen von Standard-Widgets und zum Erstellen benutzerdefinierter Widgets, um die Informationen anzupassen, die in den Dashboards [!UICONTROL Profil] und [!UICONTROL Segmente] in der Plattform-Benutzeroberfläche angezeigt werden.

Informationen zum Ändern der Position und Größe von Widgets in den Dashboards [!UICONTROL Profil], [!UICONTROL Ziele] und [!UICONTROL Segmente] finden Sie im Handbuch [Dashboard ändern](modify.md).

>[!NOTE]
>
>Die im Dashboard [!UICONTROL Lizenzverwendung] angezeigten Widgets können nicht angepasst werden. Weitere Informationen zu diesem eindeutigen Dashboard finden Sie in der [Dashboard-Dokumentation zur Lizenznutzung](guides/license-usage.md).

## Zugriff auf die Widget-Bibliothek

Sie können aus jedem Dashboard (z. B. dem Profil-Dashboard) **[!UICONTROL Dashboard]** ändern, gefolgt von **[!UICONTROL Widget-Bibliothek]** auswählen, um auf die Widget-Bibliothek zuzugreifen.

>[!NOTE]
>
>Die Schaltfläche [!UICONTROL Widget library] wird nur angezeigt, wenn [!UICONTROL Dashboard ändern] ausgewählt wurde.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

Die [!UICONTROL Widget-Bibliothek] enthält zwei Registerkarten: [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert].

* Die Registerkarte **[!UICONTROL Standard]** enthält Widgets, die von der Adobe erstellt wurden, und ermöglicht es Ihnen, Ihr Dashboard mithilfe dieser Standardmetriken zu aktualisieren. Weitere Informationen zum Hinzufügen von Standard-Widgets zu Ihrem Dashboard finden Sie im Abschnitt [Standard-Widgets](#standard-widgets) in diesem Handbuch.
* Mit der Registerkarte **[!UICONTROL Benutzerdefiniert]** können Sie Widgets in Ihrem Unternehmen erstellen und freigeben. Vollständige Schritte zum Erstellen eigener Widgets finden Sie im Abschnitt [Benutzerdefinierte Widgets](#custom-widgets) in diesem Handbuch.

![](images/customization/widget-library.png)

## Standard-Widgets {#standard-widgets}

Die Registerkarte **[!UICONTROL Standard]** enthält Widgets, die von der Adobe erstellt wurden und in Kategorien unterteilt sind. Wenn Sie eine Kategorie auswählen, werden die für dieses Dashboard verfügbaren Widgets angezeigt. Jedes Widget wird als Karte angezeigt und enthält den Titel, die Beschreibung und eine Beispielvisualisierung der Metrik.

>[!NOTE]
>
>Widgets dürfen nur dem Dashboard hinzugefügt werden, das der ausgewählten Kategorie entspricht. Beispielsweise können dem Dashboard [!UICONTROL Profil] nur Widgets aus der Kategorie [!UICONTROL Profil] hinzugefügt werden.

![](images/customization/standard-widgets.png)

Um ein Standard-Widget auszuwählen, das Sie Ihrem Dashboard hinzufügen möchten, markieren Sie das Widget und aktivieren Sie das Kontrollkästchen für das Widget. Wenn mindestens ein Widget ausgewählt ist, wird die Schaltfläche **[!UICONTROL Hinzufügen Widget]** beleuchtet.

>[!NOTE]
>
>Der Zähler in der oberen rechten Ecke der Widget-Bibliothek zeigt die Gesamtanzahl der ausgewählten Widgets an.

Wählen Sie **[!UICONTROL Hinzufügen Widget]** aus, um dem Dashboard ausgewählte Widgets hinzuzufügen.

![](images/customization/add-widget.png)

## Benutzerdefinierte Widgets {#custom-widgets}

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 benutzerdefinierte Widgets in der Widget-Bibliothek erstellen.

Um das Aussehen von Dashboards in der Experience Platform weiter anzupassen, können Sie Widgets erstellen und diese für andere Benutzer in Ihrem Unternehmen freigeben. Wählen Sie in der Widget-Bibliothek die Registerkarte **[!UICONTROL Benutzerdefiniert]**, um mit der Erstellung benutzerdefinierter Widgets zu beginnen. Auf der Registerkarte [!UICONTROL Benutzerdefiniert] sind alle von Ihrem Unternehmen erstellten Widgets sichtbar. In diesem Beispiel wurden noch keine benutzerdefinierten Widgets erstellt.

![](images/customization/custom-widgets.png)

### Attribute auswählen

Um benutzerdefinierte Widgets zu erstellen, müssen Kundenattribute in Echtzeit identifiziert werden, um sicherzustellen, dass die Daten als Teil des täglichen Schnappschusses enthalten sind. Wenn Ihr Unternehmen keine Profil-Attribute ausgewählt hat, wird die Schaltfläche [!UICONTROL Schema konfigurieren] oben rechts in der Widget-Bibliothek angezeigt.

Wenn mindestens ein benutzerdefiniertes Attribut ausgewählt wurde, wird die Schaltfläche [!UICONTROL Schema bearbeiten] oben rechts in der Widget-Bibliothek angezeigt. Wählen Sie **[!UICONTROL Schema bearbeiten]**, um das Dialogfeld **[!UICONTROL Vereinigung-Schema auswählen]** zu öffnen, um die ausgewählten Attribute Ansicht und weitere Attribute hinzuzufügen.

>[!IMPORTANT]
>
>Eine Organisation kann maximal 20 Attribute auswählen.

![](images/customization/edit-schema.png)

Um ein Attribut auszuwählen, navigieren Sie zum Attribut im Schema &quot;Vereinigung&quot;(oder verwenden Sie die Suche) und aktivieren Sie das Kontrollkästchen neben dem Attribut. Wenn Sie das Kontrollkästchen aktivieren, wird das Attribut auch der Liste **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds hinzugefügt.

>[!NOTE]
>
>Damit ein Attribut zur Auswahl sichtbar sein kann, muss es eine der folgenden Eigenschaften haben: Zeichenfolge, Datum, Datum/Uhrzeit, Boolescher Wert, Kurz, Lang, Ganzzahl oder Byte. Die Datentypen &quot;Zuordnung&quot;und &quot;Dublette&quot;werden nicht unterstützt und sind grau hervorgehoben, sodass sie nicht ausgewählt werden können.

Wählen Sie nach Auswahl der hinzuzufügenden Attribute **[!UICONTROL Speichern]**, um Ihre Attribute zu speichern und zur Registerkarte &quot;Benutzerdefinierte Widgets&quot;zurückzukehren.

Neu ausgewählte Attribute sind nach dem täglichen Schnappschuss verfügbar, wenn die Daten aktualisiert werden.

![](images/customization/select-attribute.png)

### Erstellen eines benutzerdefinierten Widgets

Um ein benutzerdefiniertes Widget zu erstellen, wählen Sie **[!UICONTROL Erstellen]** aus der Mitte der Widget-Bibliothek oder, falls bereits benutzerdefinierte Widgets erstellt wurden, wählen Sie **[!UICONTROL Widget erstellen]** aus der oberen rechten Ecke der Widget-Bibliothek.

![](images/customization/create-widget.png)

Im Dialogfeld **[!UICONTROL Widget erstellen]** können Sie einen Titel und eine Beschreibung für Ihr neues Widget angeben und das Attribut auswählen, das vom Widget angezeigt werden soll. Um ein Attribut auszuwählen, klicken Sie auf das Optionsfeld neben dem Attribut, das Sie hinzufügen möchten.

>[!NOTE]
>
>Pro Widget kann nur ein Attribut ausgewählt werden. Wenn für ein Attribut bereits ein Widget erstellt wurde, erscheint das Attribut grau abgeblendet.

![](images/customization/create-widget-dialog.png)

Im Dialogfeld wird eine Vorschau des neuen Widgets angezeigt, die ein horizontales Balkendiagramm mit Musterdaten enthält.

>[!NOTE]
>
>Die einzige Metrik, die derzeit für alle Attribute unterstützt wird, ist die Anzahl der Profil, und die einzige Visualisierung, die derzeit für benutzerdefinierte Widgets unterstützt wird, ist ein horizontales Balkendiagramm.
>
>Die im Beispiel-Widget angezeigten Daten dienen nur zur Veranschaulichung. Die Vorschau zeigt keine tatsächlichen Daten aus Ihrem Unternehmen an.

![](images/customization/create-widget-select-attribute.png)

Um Ihr neues Widget zu speichern und zur Registerkarte [!UICONTROL Benutzerdefiniert] zurückzukehren, wählen Sie **[!UICONTROL Erstellen]**. Ihr neues Widget kann nun einem Dashboard hinzugefügt werden, indem Sie das Widget aus der Bibliothek auswählen und **[!UICONTROL Hinzufügen Widget]** auswählen.

### Benutzerdefiniertes Widget archivieren

Nachdem der Bibliothek ein Widget hinzugefügt wurde, kann es mithilfe der Schaltfläche **[!UICONTROL Archivieren]** archiviert werden. Sie können das Widget auch bearbeiten, um die Titel- oder Beschreibungsfelder zu aktualisieren.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie jetzt auf die Widget-Bibliothek [!UICONTROL zugreifen und sie verwenden, um einem Dashboard Widgets hinzuzufügen oder benutzerdefinierte Widgets für Ihr Unternehmen zu erstellen. ] Um die Größe und Position von Widgets im Dashboard zu ändern, lesen Sie bitte das [Handbuch Dashboard ändern](modify.md).
