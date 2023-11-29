---
keywords: Experience Platform;Benutzeroberfläche;UI;Dashboards;Dashboard;Profile;Segmente;Ziele;Lizenznutzung;Widgets;Metriken;
title: Erstellen benutzerdefinierter Widgets für Dashboards
description: Dieses Handbuch enthält Schritt-für-Schritt-Anweisungen zum Erstellen benutzerdefinierter Widgets zur Verwendung in Adobe Experience Platform-Dashboards.
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 90%

---

# Erstellen benutzerdefinierter Widgets für Dashboards

In Adobe Experience Platform können Sie die Daten Ihres Unternehmens mithilfe mehrerer Dashboards anzeigen und damit interagieren. Sie können bestimmte Dashboards auch aktualisieren, indem Sie Ihrer Dashboard-Ansicht neue Widgets hinzufügen. Zusätzlich zu den von Adobe bereitgestellten Standard-Widgets können Sie auch benutzerdefinierte Widgets erstellen und diese in Ihrem gesamten Unternehmen freigeben.

Dieses Handbuch enthält Schritt-für-Schritt-Anweisungen zum Erstellen und Hinzufügen benutzerdefinierter Widgets zu den Dashboards [!UICONTROL Profile], [!UICONTROL Segmente] und [!UICONTROL Ziele] in der Platform-Benutzeroberfläche.

>[!NOTE]
>
>An den Dashboards vorgenommene Aktualisierungen erfolgen nach Organisation und Sandbox.

Weiterführende Informationen zu Standard-Widgets finden Sie im Handbuch zum [Hinzufügen von Standard-Widgets zu Ihren Dashboards](standard-widgets.md).

## Widget-Bibliothek {#widget-library}

Dieses Handbuch erfordert Zugriff auf die [!UICONTROL Widget-Bibliothek] in Experience Platform. Um mehr über die Widget-Bibliothek und den Zugriff darauf über die Benutzeroberfläche zu erfahren, lesen Sie zunächst den [Überblick über die Widget-Bibliothek](widget-library.md).

## Erste Schritte mit benutzerdefinierten Widgets

Innerhalb der Widget-Bibliothek können Sie mithilfe der Registerkarte **[!UICONTROL Benutzerdefiniert]** Widgets erstellen und für andere Benutzer in Ihrer Organisation freigeben, um das Erscheinungsbild Ihrer Dashboards anzupassen.

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 benutzerdefinierte Widgets in der Widget-Bibliothek erstellen.

Wählen Sie die Registerkarte **[!UICONTROL Benutzerdefiniert]** aus, um mit der Erstellung benutzerdefinierter Widgets zu beginnen oder benutzerdefinierte Widgets anzuzeigen, die bereits von Ihrem Unternehmen erstellt wurden.

![Der Arbeitsbereich für die Widget-Bibliothek mit der Registerkarte &quot;Benutzerdefiniert&quot;.](../images/customization/custom-widgets.png)

## Erstellen eines benutzerdefinierten Widgets

Um ein benutzerdefiniertes Widget zu erstellen, wählen Sie **[!UICONTROL Widget erstellen]** in der oberen rechten Ecke der Widget-Bibliothek oder, falls dies das erste benutzerdefinierte Widget Ihres Unternehmens ist, wählen Sie **[!UICONTROL Erstellen]** in der Mitte der Widget-Bibliothek.

![Die Registerkarte &quot;Benutzerdefiniert&quot;im Arbeitsbereich der Widget-Bibliothek mit hervorgehobener Option &quot;Erstellen&quot;.](../images/customization/create-widget.png)

Geben Sie im Dialogfeld **[!UICONTROL Widget erstellen]** einen Titel und eine Beschreibung für Ihr neues Widget ein und wählen Sie das Attribut aus, das das Widget anzeigen soll.

>[!NOTE]
>
>Die Liste der verfügbaren Attribute hängt vom für Ihr Unternehmen konfigurierten Schema ab. Weitere Informationen zur Attributauswahl und zur Schemakonfiguration finden Sie im Handbuch zum [Bearbeiten des Schemas zum Erstellen benutzerdefinierter Widgets](edit-schema.md).

Um ein Attribut auszuwählen, wählen Sie das Optionsfeld neben dem Attribut aus, das Sie hinzufügen möchten.

>[!NOTE]
>
>Pro Widget kann nur ein Attribut ausgewählt und pro Attribut kann nur ein Widget erstellt werden. Wenn bereits ein Widget für ein Attribut erstellt wurde, wird das Attribut ausgegraut angezeigt.

![Das Dialogfeld Widget erstellen .](../images/customization/create-widget-dialog.png)

## Auswählen einer Visualisierung

Nach Auswahl eines Attributs wird im Dialogfeld eine Vorschau des neuen Widgets angezeigt. Es wird Künstliche Intelligenz verwendet, um automatisch eine Visualisierung auszuwählen, die den Attributdaten am besten entspricht, und um zusätzliche Visualisierungsoptionen bereitzustellen, unter denen Sie manuell wählen können.

Je nach Attribut empfiehlt die KI verschiedene Visualisierungsoptionen. Die vollständige Liste der Visualisierungen umfasst:

* Horizontales Balkendiagramm: Zur Darstellung von Werten werden horizontale Linien verwendet.
* Vertikales Balkendiagramm: Zur Darstellung von Werten werden vertikale Linien verwendet.
* Ringdiagramm: Ähnlich wie bei einem Tortendiagramm werden Werte als Teile oder Teile eines Ganzen angezeigt.
* Streudiagramm: Verwendet eine horizontale und eine vertikale Achse zur Angabe von Werten.
* Liniendiagramm: Die Werte werden in einer einzelnen Zeile angezeigt, um Änderungen über einen bestimmten Zeitraum hinweg anzuzeigen.
* Zahlenkarte: Zeigt eine Zusammenfassungsnummer an, die einen einzelnen Schlüsselwert darstellt.
* Datentabelle: Werte werden als Zeilen in einer Tabelle angezeigt.

>[!NOTE]
>
>Die einzige Metrik, die derzeit für alle Attribute unterstützt wird, ist die Anzahl der Profile.
>
>Die im Beispiel-Widget angezeigten Daten dienen nur zu Veranschaulichungszwecken. Die Vorschau zeigt keine tatsächlichen Daten aus Ihrer Organisation an.

Um Ihr neues Widget zu speichern und zur Registerkarte [!UICONTROL Benutzerdefiniert] zurückzukehren, wählen Sie **[!UICONTROL Erstellen]** aus.

![Das Dialogfeld &quot;Widget erstellen&quot;mit den Visualisierungsoptionen und &quot;Erstellen&quot;hervorgehoben.](../images/customization/create-widget-select-attribute.png)

Ihr neues Widget kann jetzt zu einem Dashboard hinzugefügt werden, indem Sie das Widget aus der Bibliothek auswählen und auf **[!UICONTROL Widget hinzufügen]** klicken.

![Die Registerkarte &quot;Benutzerdefiniert&quot;im Arbeitsbereich der Widget-Bibliothek, wobei das neue Widget und das Widget hinzufügen hervorgehoben sind.](../images/customization/custom-widgets-new.png)

## Ausblenden eines benutzerdefinierten Widgets

Nachdem ein Widget zur Bibliothek hinzugefügt wurde, kann es ausgeblendet werden, indem Sie die Auslassungszeichen (`...`) auf der Widget-Karte auswählen und dann **[!UICONTROL Widget ausblenden]** auswählen. Sie können das Widget auch in derselben Dropdown-Liste in der Vorschau anzeigen und bearbeiten.

Um ausgeblendete Widgets anzuzeigen, wählen Sie **[!UICONTROL Ausgeblendete Widgets anzeigen]** in der rechten oberen Ecke der Widget-Bibliothek aus.

>[!WARNING]
>
>Durch das Ausblenden eines Widgets in der Bibliothek wird das Widget nicht aus den Dashboards einzelner Benutzer entfernt. Sollte ein Widget nicht mehr in Ihrer Organisation verwendet werden, stellen Sie sicher, dass Sie dies allen Platform-Benutzern direkt mitteilen, da sie das Widget aus ihren Dashboards entfernen müssen.

![Die Registerkarte &quot;Benutzerdefiniert&quot;im Arbeitsbereich der Widget-Bibliothek mit den Dropdown-Menüoptionen &quot;Widget&quot;und &quot;Verborgene Widgets anzeigen&quot;hervorgehoben.](../images/customization/hide-widget.png)

## Bearbeiten eines benutzerdefinierten Widgets

Sie können benutzerdefinierte Widgets in der Widget-Bibliothek bearbeiten, indem Sie die Auslassungszeichen (`...`) auf der Widget-Karte auswählen und dann **[!UICONTROL Bearbeiten]** aus dem Dropdown-Menü auswählen.

![Die Dropdown-Menüoptionen des Widgets mit hervorgehobenen Auslassungspunkten und hervorgehobenen Bearbeitungen.](../images/customization/custom-widget-edit.png)

Im Dialogfeld **[!UICONTROL Widget bearbeiten]** können Sie den Titel und die Beschreibung des Widgets bearbeiten sowie eine Vorschau anzeigen und verschiedene Visualisierungen auswählen. Nachdem Sie Ihre Änderungen vorgenommen haben, klicken Sie auf **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern und zur Registerkarte „Benutzerdefinierte Widgets“ zurückzukehren.

>[!WARNING]
>
>Beim Bearbeiten eines Widgets in der Bibliothek wird das Widget nicht für einzelne Benutzer aktualisiert. Wenn ein Widget aktualisiert wurde, stellen Sie sicher, dass Sie dies allen Platform-Benutzern direkt mitteilen, da diese das veraltete Widget aus ihren Dashboards entfernen und dann das aktualisierte Widget aus der Widget-Bibliothek auswählen und hinzufügen müssen.

![Dialogfeld &quot;Widget bearbeiten&quot;.](../images/customization/edit-widget.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie, wie Sie auf die Widget-Bibliothek zugreifen und sie zum Erstellen und Hinzufügen benutzerdefinierter Widgets für Ihre Organisation verwenden können. Informationen zum Ändern der Größe und Position von Widgets, die im Dashboard angezeigt werden, finden Sie im [Handbuch zum Ändern von Dashboards](modify.md).
