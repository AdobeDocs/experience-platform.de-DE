---
keywords: Experience Platform; Benutzeroberfläche; Benutzeroberfläche; Dashboards; Dashboard; Profile; Segmente; Ziele; Lizenzverwendung
title: Schema bearbeiten, um benutzerdefinierte Dashboard-Widgets zu erstellen
description: 'Dieses Handbuch enthält schrittweise Anweisungen zum Auswählen von Attributen und Konfigurieren des Schemas Ihres Unternehmens, um benutzerdefinierte Widgets für Adobe Experience Platform-Dashboards zu erstellen. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 16a8764fd27e6b1ae32bc37b3abcd521aaf88887
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Schema-Bearbeitung zum Erstellen benutzerdefinierter Widgets

Um benutzerdefinierte Widgets für Adobe Experience Platform-Dashboards zu erstellen, müssen Sie zunächst die Echtzeit-Kundenprofilattribute identifizieren, auf denen die Widgets basieren.

Dieses Handbuch enthält schrittweise Anweisungen zum Bearbeiten des Schemas Ihres Unternehmens, indem Sie Attribute auswählen, um benutzerdefinierte Dashboard-Widgets zu erstellen.

Nachdem Attribute ausgewählt und das Schema konfiguriert wurde, können Sie mit den Schritten zum Erstellen von benutzerdefinierten Widgets für Ihre Dashboards](custom-widgets.md) fortfahren.[

>[!NOTE]
>
>Benutzern muss die Berechtigung &quot;Standard-Dashboards verwalten&quot;gewährt werden, damit sie das Schema bearbeiten können. Anweisungen zum Gewähren von Zugriffsberechtigungen für Dashboards finden Sie im [Dashboard-Berechtigungshandbuch](../permissions.md).

## Widget-Bibliothek {#widget-library}

Dieses Handbuch erfordert Zugriff auf die [!UICONTROL Widget-Bibliothek] in Experience Platform. Um mehr über die Widget-Bibliothek und den Zugriff darauf über die Benutzeroberfläche zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](widget-library.md).

## Schema-Bearbeitung

Innerhalb der Widget-Bibliothek können Sie mit dem Tab **[!UICONTROL Benutzerdefiniert]** Widgets erstellen und für andere Benutzer in Ihrer Organisation freigeben, um das Erscheinungsbild Ihrer Dashboards anzupassen.

Bevor Sie benutzerdefinierte Widgets erstellen können, müssen Echtzeit-Kundenprofilattribute ausgewählt werden, um sicherzustellen, dass die Daten als Teil der täglichen Momentaufnahme enthalten sind.

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 Attribute auswählen.

Wenn Ihr Unternehmen keine Profilattribute ausgewählt hat, wählen Sie zunächst **[!UICONTROL Schema bearbeiten]** in der oberen rechten Ecke der Widget-Bibliothek.

Wenn mindestens ein benutzerdefiniertes Attribut erstellt wurde, wählen Sie **[!UICONTROL Schema bearbeiten]** aus, um die ausgewählten Attribute anzuzeigen und weitere hinzuzufügen.

![](../images/customization/edit-schema.png)

## Attribut auswählen

Um ein Attribut im Dialogfeld **[!UICONTROL Vereinigungsschema auswählen]** auszuwählen, navigieren Sie zum Attribut im Vereinigungsschema (oder verwenden Sie die Suche) und aktivieren Sie das Kontrollkästchen neben dem Attribut. Wenn Sie das Kontrollkästchen aktivieren, wird das Attribut auch zur Liste **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds hinzugefügt.

>[!NOTE]
>
>Damit ein Attribut zur Auswahl sichtbar ist, muss es eines der folgenden sein: Zeichenfolge, Datum, Datum/Uhrzeit, Boolesch, kurz, lang, Ganzzahl oder Byte. Die Datentypen Zuordnung und Doppelte werden nicht unterstützt und sind grau dargestellt, sodass sie nicht ausgewählt werden können.

Nachdem Sie die Attribute ausgewählt haben, die Sie hinzufügen möchten, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Attribute zu speichern und zur Registerkarte &quot;Benutzerdefinierte Widgets&quot;zurückzukehren.

>[!WARNING]
>Neu ausgewählte Attribute werden nach dem nächsten täglichen Schnappschuss verfügbar, wenn die Daten aktualisiert werden.

![](../images/customization/select-attribute.png)

## Nächste Schritte

Nach dem Lesen dieses Handbuchs können Sie zur Widget-Bibliothek navigieren und Echtzeit-Kundenprofilattribute auswählen, um Ihr Schema zu konfigurieren. Wenn Sie Profilattribute ausgewählt haben, können Sie [mit dem Erstellen benutzerdefinierter Widgets für Ihre Dashboards](custom-widgets.md) beginnen.