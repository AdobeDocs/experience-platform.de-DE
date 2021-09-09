---
keywords: Experience Platform; Benutzeroberfläche; Benutzeroberfläche; Dashboards; Dashboard; Profile; Segmente; Ziele; Lizenzverwendung; Widgets; Metriken;
title: Erstellen benutzerdefinierter Widgets für Dashboards
description: 'Dieses Handbuch enthält schrittweise Anweisungen zum Erstellen benutzerdefinierter Widgets zur Verwendung in Adobe Experience Platform-Dashboards. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---


# Erstellen benutzerdefinierter Widgets für Dashboards

In Adobe Experience Platform können Sie die Daten Ihres Unternehmens mithilfe mehrerer Dashboards anzeigen und damit interagieren. Sie können bestimmte Dashboards auch aktualisieren, indem Sie Ihrer Dashboard-Ansicht neue Widgets hinzufügen. Zusätzlich zu den von Adobe bereitgestellten Standard-Widgets können Sie auch benutzerdefinierte Widgets erstellen und diese in Ihrem gesamten Unternehmen freigeben.

Dieses Handbuch enthält schrittweise Anweisungen zum Erstellen und Hinzufügen benutzerdefinierter Widgets zu den Dashboards [!UICONTROL Profile], [!UICONTROL Segmente] und [!UICONTROL Ziele] in der Platform-Benutzeroberfläche.

Weiterführende Informationen zu Standard-Widgets finden Sie im Handbuch zum Hinzufügen von Standard-Widgets zu Dashboards](standard-widgets.md).[

>[!NOTE]
>
>Die im Dashboard [!UICONTROL Lizenznutzung] angezeigten Widgets können nicht angepasst werden. Weitere Informationen zu diesem eindeutigen Dashboard finden Sie in der [Dashboard-Dokumentation zur Lizenzverwendung](../guides/license-usage.md).

## Widget-Bibliothek {#widget-library}

Dieses Handbuch erfordert Zugriff auf die [!UICONTROL Widget-Bibliothek] in Experience Platform. Um mehr über die Widget-Bibliothek und den Zugriff darauf über die Benutzeroberfläche zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](widget-library.md).

## Erste Schritte mit benutzerdefinierten Widgets

Innerhalb der Widget-Bibliothek können Sie mit dem Tab **[!UICONTROL Benutzerdefiniert]** Widgets erstellen und für andere Benutzer in Ihrer Organisation freigeben, um das Erscheinungsbild Ihrer Dashboards anzupassen.

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 benutzerdefinierte Widgets in der Widget-Bibliothek erstellen.

Wählen Sie die Registerkarte **[!UICONTROL Benutzerdefiniert]** aus, um mit der Erstellung benutzerdefinierter Widgets zu beginnen oder benutzerdefinierte Widgets anzuzeigen, die bereits von Ihrem Unternehmen erstellt wurden.

![](../images/customization/custom-widgets.png)

## Benutzerdefiniertes Widget erstellen

Um ein benutzerdefiniertes Widget zu erstellen, wählen Sie **[!UICONTROL Widget erstellen]** aus der oberen rechten Ecke der Widget-Bibliothek oder, wenn dies das erste benutzerdefinierte Widget Ihres Unternehmens ist, wählen Sie **[!UICONTROL Erstellen]** aus der Mitte der Widget-Bibliothek.

![](../images/customization/create-widget.png)

Geben Sie im Dialogfeld **[!UICONTROL Widget erstellen]** einen Titel und eine Beschreibung für Ihr neues Widget ein und wählen Sie das Attribut aus, das das Widget anzeigen soll.

>[!NOTE]
>
>Die Liste der verfügbaren Attribute hängt vom für Ihr Unternehmen konfigurierten Schema ab. Weitere Informationen zur Attributauswahl und zur Schemakonfiguration finden Sie im Handbuch zum [Bearbeiten des Schemas zum Erstellen benutzerdefinierter Widgets](edit-schema.md).

Um ein Attribut auszuwählen, wählen Sie das Optionsfeld neben dem Attribut aus, das Sie hinzufügen möchten.

>[!NOTE]
>
>Pro Widget kann nur ein Attribut ausgewählt und pro Attribut kann nur ein Widget erstellt werden. Wenn bereits ein Widget für ein Attribut erstellt wurde, wird das Attribut grau ausgeblendet angezeigt.

![](../images/customization/create-widget-dialog.png)

## Auswählen einer Visualisierung

Nach Auswahl eines Attributs wird eine Vorschau des neuen Widgets im Dialogfeld angezeigt. Künstliche Intelligenz wird verwendet, um automatisch eine Visualisierung auszuwählen, die den Attributdaten am besten entspricht, und um zusätzliche Visualisierungsoptionen bereitzustellen, die Sie manuell auswählen können.

Je nach Attribut empfiehlt die KI verschiedene Visualisierungsoptionen. Die vollständige Liste der Visualisierungen umfasst:

* Horizontales Balkendiagramm: Horizontale Linien dienen zur Darstellung von Werten.
* Vertikales Balkendiagramm: Zur Darstellung von Werten werden vertikale Linien verwendet.
* Ringdiagramm: Ähnlich wie bei einem Tortendiagramm werden Werte als Teile oder Teile eines Ganzen angezeigt.
* Streudiagramm: Verwendet eine horizontale und vertikale Achse zur Angabe von Werten.
* Liniendiagramm: Die Werte werden in einer einzelnen Zeile angezeigt, um Änderungen über einen bestimmten Zeitraum hinweg anzuzeigen.
* Zahlenkarte: Zeigt eine Zusammenfassungsnummer an, die einen einzelnen Schlüsselwert darstellt.
* Datentabelle: Werte werden als Zeilen in einer Tabelle angezeigt.

>[!NOTE]
>
>Die einzige Metrik, die derzeit für alle Attribute unterstützt wird, ist die Anzahl der Profile.
>
>Die im Beispiel-Widget angezeigten Daten dienen nur zu Veranschaulichungszwecken. Die Vorschau zeigt keine tatsächlichen Daten aus Ihrer Organisation an.

Um Ihr neues Widget zu speichern und zur Registerkarte [!UICONTROL Benutzerdefiniert] zurückzukehren, wählen Sie **[!UICONTROL Erstellen]** aus.

![](../images/customization/create-widget-select-attribute.png)

Ihr neues Widget kann jetzt zu einem Dashboard hinzugefügt werden, indem Sie das Widget aus der Bibliothek auswählen und **[!UICONTROL Widget hinzufügen]** auswählen.

![](../images/customization/custom-widgets-new.png)

## Ausblenden eines benutzerdefinierten Widgets

Nachdem ein Widget zur Bibliothek hinzugefügt wurde, kann es ausgeblendet werden, indem Sie die Auslassungszeichen (`...`) auf der Widget-Karte auswählen und dann **[!UICONTROL Widget ausblenden]** auswählen. Sie können das Widget auch in derselben Dropdown-Liste in der Vorschau anzeigen und bearbeiten.

Um ausgeblendete Widgets anzuzeigen, wählen Sie **[!UICONTROL Verborgene Widgets anzeigen]** aus der oberen rechten Ecke der Widget-Bibliothek aus.

>[!WARNING]
>
>Durch das Ausblenden eines Widgets in der Bibliothek wird das Widget nicht aus den Dashboards einzelner Benutzer entfernt. Sollte ein Widget nicht mehr in Ihrer Organisation verwendet werden, stellen Sie sicher, dass Sie dies allen Platform-Benutzern direkt mitteilen, da das Widget aus ihren Dashboards entfernt werden muss.

![](../images/customization/hide-widget.png)

## Benutzerdefiniertes Widget bearbeiten

Sie können benutzerdefinierte Widgets in der Widget-Bibliothek bearbeiten, indem Sie die Auslassungszeichen (`...`) auf der Widget-Karte auswählen und dann **[!UICONTROL Bearbeiten]** aus dem Dropdown-Menü auswählen.

![](../images/customization/custom-widget-edit.png)

Im Dialogfeld **[!UICONTROL Widget bearbeiten]** können Sie den Titel und die Beschreibung des Widgets bearbeiten sowie eine Vorschau anzeigen und verschiedene Visualisierungen auswählen. Nachdem Sie Ihre Änderungen vorgenommen haben, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu speichern und zur Registerkarte &quot;Benutzerdefinierte Widgets&quot;zurückzukehren.

>[!WARNING]
>
>Beim Bearbeiten eines Widgets in der Bibliothek wird das Widget nicht für einzelne Benutzer aktualisiert. Wenn ein Widget aktualisiert wurde, stellen Sie sicher, dass Sie dies allen Platform-Benutzern direkt mitteilen, da diese das veraltete Widget aus ihren Dashboards entfernen und dann das aktualisierte Widget auswählen und aus der Widget-Bibliothek hinzufügen müssen.

![](../images/customization/edit-widget.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie auf die Widget-Bibliothek zugreifen und sie zum Erstellen und Hinzufügen benutzerdefinierter Widgets für Ihre Organisation verwenden. Informationen zum Ändern der Größe und Position von Widgets, die im Dashboard angezeigt werden, finden Sie im Handbuch [Dashboards ändern](modify.md).
