---
keywords: Experience Platform; Benutzeroberfläche; Benutzeroberfläche; Dashboards; Dashboard; Profile; Segmente; Ziele; Lizenzverwendung
title: Verwenden der Widget-Bibliothek zum Hinzufügen und Erstellen von Dashboard-Widgets
description: 'Dieses Handbuch enthält schrittweise Anweisungen zum Hinzufügen von Standard-Widgets und zum Erstellen benutzerdefinierter Widgets zur Visualisierung von Dashboard-Daten in Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 63f855d7dd3c3591da76a23ca8d673477378c1c3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# Widget-Bibliothek {#widget-library}

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Daten Ihres Unternehmens mithilfe mehrerer Dashboards anzeigen und damit interagieren. Sie können auch einige dieser Dashboards aktualisieren, indem Sie Ihrer Dashboard-Ansicht neue Widgets hinzufügen. Zusätzlich zu den von Adobe bereitgestellten Standard-Widgets können Sie auch benutzerdefinierte Widgets erstellen und diese unternehmensweit freigeben.

Dieses Handbuch enthält schrittweise Anweisungen zum Hinzufügen von Standard-Widgets und zum Erstellen benutzerdefinierter Widgets, um die Informationen anzupassen, die in den Dashboards [!UICONTROL Profile], [!UICONTROL Segmente] und [!UICONTROL Ziele] in der Platform-Benutzeroberfläche angezeigt werden.

Informationen zum Ändern des Speicherorts und der Größe von Widgets im Dashboard [!UICONTROL Profile], [!UICONTROL Ziele] und [!UICONTROL Segmente] finden Sie im Handbuch [Dashboards ändern](modify.md).

>[!NOTE]
>
>Die im Dashboard [!UICONTROL Lizenznutzung] angezeigten Widgets können nicht angepasst werden. Weitere Informationen zu diesem eindeutigen Dashboard finden Sie in der [Dashboard-Dokumentation zur Lizenzverwendung](guides/license-usage.md).

## Zugriff auf die Widget-Bibliothek

In jedem Dashboard (z. B. im Dashboard &quot;Profile&quot;) können Sie **[!UICONTROL Dashboard ändern]** und danach **[!UICONTROL Widget-Bibliothek]** auswählen, um auf die Widget-Bibliothek zuzugreifen.

>[!NOTE]
>
>Die Schaltfläche [!UICONTROL Widget-Bibliothek] wird nur angezeigt, wenn [!UICONTROL Dashboard ändern] ausgewählt wurde.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

## Widget-Bibliothek anzeigen

Die [!UICONTROL Widget-Bibliothek] enthält zwei Registerkarten: [!UICONTROL Standard] und [!UICONTROL Benutzerdefiniert].

* Der Tab **[!UICONTROL Standard]** enthält von Adobe erstellte Widgets und ermöglicht Ihnen die Aktualisierung Ihres Dashboards mithilfe dieser Standardmetriken. Weitere Informationen zum Hinzufügen von Standard-Widgets zu Dashboards finden Sie im Abschnitt [Standard-Widgets](#standard-widgets) in diesem Handbuch.
* Mit dem Tab **[!UICONTROL Benutzerdefiniert]** können Sie Widgets innerhalb Ihres Unternehmens erstellen und freigeben. Die vollständigen Schritte zum Erstellen Ihrer eigenen Widgets finden Sie im Abschnitt [Benutzerdefinierte Widgets](#custom-widgets) in diesem Handbuch.

![](images/customization/widget-library.png)

## Standard-Widgets {#standard-widgets}

Der Tab **[!UICONTROL Standard]** enthält von Adobe erstellte Widgets, die basierend auf den verfügbaren Dashboards in Kategorien unterteilt sind. Die ausgewählte Kategorie entspricht dem Dashboard, über das Sie die Widget-Bibliothek aufgerufen haben. Anders ausgedrückt: Wenn Sie die Widget-Bibliothek im Dashboard [!UICONTROL Profile] ausgewählt haben, wird die Kategorie [!UICONTROL Profile] ausgewählt und die anderen Kategorien werden ausgegraut angezeigt.

Die verfügbaren Widgets für die ausgewählte Kategorie werden angezeigt. Jedes Widget wird als Karte mit dem Titel, der Beschreibung und einer Beispielvisualisierung der Metrik angezeigt.

>[!NOTE]
>
>Widgets dürfen nur zum Dashboard hinzugefügt werden, das der ausgewählten Kategorie entspricht. Beispielsweise können nur Widgets aus der Kategorie [!UICONTROL Profile] zum Dashboard [!UICONTROL Profile] hinzugefügt werden.

![](images/customization/standard-widgets.png)

### Standard-Widget zum Dashboard hinzufügen

Um ein Standard-Widget zum Dashboard auszuwählen, markieren Sie das Widget und aktivieren Sie das Kontrollkästchen für das Widget. Wenn mindestens ein Widget ausgewählt ist, wird die Schaltfläche **[!UICONTROL Widget hinzufügen]** beleuchtet.

>[!NOTE]
>
>Der Zähler in der oberen rechten Ecke der Widget-Bibliothek zeigt die Gesamtzahl der ausgewählten Widgets an.

Wählen Sie **[!UICONTROL Widget]** hinzufügen aus, um die ausgewählten Widgets zu Ihrem Dashboard hinzuzufügen.

![](images/customization/add-widget.png)

## Benutzerdefinierte Widgets {#custom-widgets}

Um das Erscheinungsbild von Dashboards in Experience Platform weiter anzupassen, können Sie Widgets erstellen und diese an andere Benutzer in Ihrer Organisation weitergeben.

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 benutzerdefinierte Widgets in der Widget-Bibliothek erstellen.

Wählen Sie in der Widget-Bibliothek die Registerkarte **[!UICONTROL Benutzerdefiniert]** aus, um mit der Erstellung benutzerdefinierter Widgets zu beginnen oder um benutzerdefinierte Widgets anzuzeigen, die Ihr Unternehmen bereits erstellt hat.

![](images/customization/custom-widgets.png)

### Schema-Bearbeitung

Um benutzerdefinierte Widgets zu erstellen, müssen Echtzeit-Kundenprofilattribute identifiziert werden, um sicherzustellen, dass die Daten als Teil der täglichen Momentaufnahme enthalten sind. Wenn Ihr Unternehmen keine Profilattribute ausgewählt hat, wird die Schaltfläche [!UICONTROL Schema] konfigurieren oben rechts in der Widget-Bibliothek angezeigt.

Wenn mindestens ein benutzerdefiniertes Attribut ausgewählt wurde, wird die Schaltfläche [!UICONTROL Schema bearbeiten] in der oberen rechten Ecke der Widget-Bibliothek angezeigt. Wählen Sie **[!UICONTROL Schema]** bearbeiten aus, um das Dialogfeld **[!UICONTROL Vereinigungsschema-Feld auswählen]** zu öffnen, um die ausgewählten Attribute anzuzeigen und weitere Attribute hinzuzufügen.

>[!IMPORTANT]
>
>Eine Organisation kann maximal 20 Attribute auswählen.

![](images/customization/edit-schema.png)

Um ein Attribut auszuwählen, navigieren Sie zum Attribut im Vereinigungsschema (oder verwenden Sie die Suche) und aktivieren Sie das Kontrollkästchen neben dem Attribut. Wenn Sie das Kontrollkästchen aktivieren, wird das Attribut auch zur Liste **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds hinzugefügt.

>[!NOTE]
>
>Damit ein Attribut zur Auswahl sichtbar ist, muss es eines der folgenden sein: Zeichenfolge, Datum, Datum/Uhrzeit, Boolesch, kurz, lang, Ganzzahl oder Byte. Die Datentypen Zuordnung und Doppelte werden nicht unterstützt und sind grau dargestellt, sodass sie nicht ausgewählt werden können.

Nachdem Sie die Attribute ausgewählt haben, die Sie hinzufügen möchten, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Attribute zu speichern und zur Registerkarte &quot;Benutzerdefinierte Widgets&quot;zurückzukehren.

Neu ausgewählte Attribute sind nach der täglichen Momentaufnahme bei der Aktualisierung der Daten verfügbar.

![](images/customization/select-attribute.png)

### Benutzerdefiniertes Widget erstellen

Um ein benutzerdefiniertes Widget zu erstellen, wählen Sie **[!UICONTROL Erstellen]** aus der Mitte der Widget-Bibliothek aus. Wenn benutzerdefinierte Widgets bereits erstellt wurden, wählen Sie **[!UICONTROL Widget erstellen]** aus der oberen rechten Ecke der Widget-Bibliothek aus.

![](images/customization/create-widget.png)

Im Dialogfeld **[!UICONTROL Widget erstellen]** können Sie einen Titel und eine Beschreibung für Ihr neues Widget angeben und das Attribut auswählen, das vom Widget angezeigt werden soll. Um ein Attribut auszuwählen, wählen Sie das Optionsfeld neben dem Attribut aus, das Sie hinzufügen möchten.

>[!NOTE]
>
>Pro Widget kann nur ein Attribut ausgewählt werden. Wenn bereits ein Widget für ein Attribut erstellt wurde, wird das Attribut grau ausgeblendet angezeigt.

![](images/customization/create-widget-dialog.png)

Im Dialogfeld wird eine Vorschau des neuen Widgets angezeigt, in der ein horizontales Balkendiagramm mit nachgeahmten Daten angezeigt wird.

>[!NOTE]
>
>Die einzige Metrik, die derzeit für alle Attribute unterstützt wird, ist die Anzahl der Profile und die einzige Visualisierung, die derzeit für benutzerdefinierte Widgets unterstützt wird, ist ein horizontales Balkendiagramm.
>
>Die im Beispiel-Widget angezeigten Daten dienen nur zu Veranschaulichungszwecken. Die Vorschau zeigt keine tatsächlichen Daten aus Ihrer Organisation an.

![](images/customization/create-widget-select-attribute.png)

Um Ihr neues Widget zu speichern und zur Registerkarte [!UICONTROL Benutzerdefiniert] zurückzukehren, wählen Sie **[!UICONTROL Erstellen]** aus. Ihr neues Widget kann jetzt zu einem Dashboard hinzugefügt werden, indem Sie das Widget aus der Bibliothek auswählen und **[!UICONTROL Widget hinzufügen]** auswählen.

### Benutzerdefiniertes Widget archivieren

Nachdem ein Widget zur Bibliothek hinzugefügt wurde, kann es mithilfe der Schaltfläche **[!UICONTROL Archivieren]** archiviert werden. Sie können das Widget auch bearbeiten, um die Titel- oder Beschreibungsfelder zu aktualisieren.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie jetzt auf die [!UICONTROL Widget-Bibliothek] zugreifen und sie verwenden, um Widgets zu einem Dashboard hinzuzufügen oder benutzerdefinierte Widgets für Ihre Organisation zu erstellen. Informationen zum Ändern der Größe und Position von Widgets im Dashboard finden Sie im Handbuch [Dashboards ändern](modify.md).
