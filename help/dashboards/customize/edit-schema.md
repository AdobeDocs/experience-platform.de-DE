---
keywords: Experience Platform;Benutzeroberfläche;UI;Dashboards;Dashboard;Profile;Segmente;Ziele;Lizenzverwendung
title: Bearbeiten eines Schemas, um benutzerdefinierte Dashboard-Widgets zu erstellen
description: Dieses Handbuch enthält schrittweise Anweisungen zum Auswählen von Attributen und Konfigurieren des Schemas Ihres Unternehmens, um benutzerdefinierte Widgets für Adobe Experience Platform-Dashboards zu erstellen.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 74%

---

# Bearbeiten eines Schemas zum Erstellen benutzerdefinierter Widgets

Um benutzerdefinierte Widgets für Adobe Experience Platform-Dashboards zu erstellen, müssen Sie zunächst die Echtzeit-Kundenprofilattribute identifizieren, auf denen die Widgets basieren.

Dieses Handbuch enthält schrittweise Anweisungen zum Bearbeiten des Schemas Ihres Unternehmens, indem Sie Attribute auswählen, um benutzerdefinierte Dashboard-Widgets zu erstellen.

Nachdem Attribute ausgewählt wurden und das Schema konfiguriert worden ist, können Sie mit den Schritten zum [Erstellen von benutzerdefinierten Widgets für Ihre Dashboards](custom-widgets.md) fortfahren.

>[!NOTE]
>
>Benutzern muss die Berechtigung „Standard-Dashboards verwalten“ gewährt werden, damit sie das Schema bearbeiten können. Anweisungen zum Gewähren von Zugriffsberechtigungen für Dashboards finden Sie im [Handbuch zu Dashboard-Berechtigungen](../permissions.md).

## Widget-Bibliothek {#widget-library}

Dieses Handbuch erfordert Zugriff auf die [!UICONTROL Widget-Bibliothek] in Experience Platform. Um mehr über die Widget-Bibliothek und den Zugriff darauf über die Benutzeroberfläche zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](widget-library.md).

## Schema-Bearbeitung

Innerhalb der Widget-Bibliothek können Sie mit der Registerkarte **[!UICONTROL Benutzerdefiniert]** Widgets erstellen und für andere Benutzer in Ihrer Organisation freigeben, um das Erscheinungsbild Ihrer Dashboards anzupassen.

Bevor Sie benutzerdefinierte Widgets erstellen können, müssen Echtzeit-Kundenprofilattribute ausgewählt werden, um sicherzustellen, dass die Daten als Teil der täglichen Momentaufnahme enthalten sind.

>[!IMPORTANT]
>
>Ihr Unternehmen kann maximal 20 Attribute auswählen.

Wenn Ihr Unternehmen keine Profilattribute ausgewählt hat, wählen Sie zunächst **[!UICONTROL Konfigurieren]** in der Mitte des Bildschirms.

![Die Registerkarte &quot;Benutzerdefiniert&quot;im Arbeitsbereich der Widget-Bibliothek mit hervorgehobener Option &quot;Konfigurieren&quot;.](../images/customization/configure-schema.png)

Wenn mindestens ein benutzerdefiniertes Attribut erstellt wurde, wählen Sie **[!UICONTROL Schema bearbeiten]** aus, um die ausgewählten Attribute anzuzeigen und weitere hinzuzufügen.

![Die Registerkarte &quot;Benutzerdefiniert&quot;im Arbeitsbereich der Widget-Bibliothek mit hervorgehobenem Bearbeitungsschema.](../images/customization/edit-schema.png)

## Auswählen eines Attributs

Um ein Attribut im Dialogfeld **[!UICONTROL Vereinigungsschemafeld auswählen]** auszuwählen, navigieren Sie zum Attribut im Vereinigungsschema (oder verwenden Sie die Suche) und aktivieren Sie das Kontrollkästchen neben dem Attribut. Wenn Sie das Kontrollkästchen aktivieren, wird das Attribut auch zur Liste **[!UICONTROL Ausgewählte Attribute]** auf der rechten Seite des Dialogfelds hinzugefügt.

>[!NOTE]
>
>Damit ein Attribut zur Auswahl sichtbar ist, muss es eines der folgenden sein: Zeichenfolge, Datum, Datum/Uhrzeit, Boolesch, kurz, lang, Ganzzahl oder Byte. Die Datentypen „Zuordnung“ und „Doppelt“ werden nicht unterstützt und sind grau dargestellt, sodass sie nicht ausgewählt werden können.

Nachdem Sie die Attribute ausgewählt haben, die Sie hinzufügen möchten, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Attribute zu speichern und zur Registerkarte „Benutzerdefinierte Widgets“ zurückzukehren.

>[!WARNING]
>Neu ausgewählte Attribute werden nach dem nächsten täglichen Schnappschuss verfügbar, wenn die Daten aktualisiert werden.

![Das Dialogfeld zum Auswählen von Schemaattributen mit Attributen und hervorgehobenem Speichern.](../images/customization/select-attribute.png)

## Nächste Schritte

Nach dem Lesen dieses Handbuchs können Sie zur Widget-Bibliothek navigieren und Echtzeit-Kundenprofilattribute auswählen, um Ihr Schema zu konfigurieren. Wenn Sie Profilattribute ausgewählt haben, können Sie mit dem [Erstellen benutzerdefinierter Widgets für Ihre Dashboards](custom-widgets.md) beginnen.
