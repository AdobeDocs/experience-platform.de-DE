---
title: Tutorial zum Implementieren von Website-Tags mit Adobe Launch
seo-title: Website-Tags mit Adobe Launch implementieren
description: Verwenden Sie Adobe Launch, um Website-Tags in Adobe Experience Platform zu implementieren.
seo-description: Verwenden Sie Adobe Launch, um Website-Tags in Adobe Experience Platform zu implementieren.
translation-type: tm+mt
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 100%

---


# Tutorial: Website-Tags mit Adobe Launch implementieren

In diesem Tutorial wird beschrieben, wie Sie mit Adobe Launch Website-Tags implementieren, um Daten an Adobe Experience Platform zu senden.

## Voraussetzungen

* Das erforderliche Schema und der erforderliche Datensatz wurden in Platform erstellt.
* Die erforderliche Konfiguration wurde in Experience Edge bereitgestellt und verfügt über die entsprechende Konfigurationskennung und Edge-Domäne.
* Das Unternehmens-CMS wurde bereits für die Bereitstellung eines JavaScript-Objekts auf jeder Seite mit den Daten konfiguriert, die Sie an Platform senden möchten.

## Schritte

Dieses Tutorial umfasst folgende Schritte:

1. Installieren der Adobe Experience Platform Web SDK-Erweiterung.
1. Erstellen einer Regel, um Launch darüber zu informieren, welche Daten gesendet werden sollen.
1. Bündeln der Erweiterung und Regel in einer Bibliothek.

## Adobe Experience Platform Web SDK-Erweiterung installieren

Installieren Sie zunächst die Adobe Experience Platform Web SDK-Erweiterung.

1. Öffnen Sie in Launch die Registerkarte **[!UICONTROL Erweiterungen]**.

   ![Bild](assets/launch-overview.png)

1. Wählen Sie im Launch-Erweiterungskatalog die Adobe Experience Platform Web SDK-Erweiterung aus. Der Konfigurationsbildschirm wird geöffnet.

   ![Bild](assets/launch-extension-install.png)

   Weiterführende Informationen finden Sie in der Launch-Dokumentation unter [Erweiterungen](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html).

1. Konfigurieren Sie die Erweiterung.

   Die einzigen Einstellungen, die Sie hier benötigen, sind:

   * **Konfigurationskennung:** Geben Sie die Konfigurationskennung an, die Sie von Ihrem Adobe-Support-Mitarbeiter erhalten haben.
   * **Edge-Domäne:** Geben Sie die Edge-Domäne an, die Sie von Ihrem Adobe-Support-Mitarbeiter erhalten haben.

1. Klicken Sie auf **[!UICONTROL Speichern]** und fahren Sie mit dem nächsten Schritt fort.

## Regel für Launch zum Festlegen der zu sendenden Daten erstellen

Anschließend erstellen Sie eine Regel, um Launch zu informieren, welche Daten Sie wann an Adobe Experience Platform senden möchten.

1. Konfigurieren Sie auf der Registerkarte **[!UICONTROL Regeln]** ein Ereignis, das auf jeder neuen Seite der Website ausgelöst wird, wenn die Launch-Bibliothek geladen wird.

   ![Bild](assets/launch-make-a-rule.png)

1. Fügen Sie eine Aktion hinzu.

   Teilen Sie Launch mit, wo Ihre Datenschicht zu finden ist, um die Aktion zu konfigurieren. Die Datenschicht ist ein JavaScript-Objekt, das auf der Seite vorhanden ist und von demselben CMS bereitgestellt wird, das die Web-Seite rendert. Geben Sie den JavaScript-Pfad zum Datenobjekt an.

   ![Bild](assets/launch-add-aep-action.png)

   Das von Ihnen gesendete Datenobjekt muss ein gültiges XDM-Objekt sein, das die Validierung anhand des Schemas übergibt, das vom mit Ihrer Konfigurationskennung verbundenen Datensatz verwendet wird.

1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]**.

Weiterführende Informationen finden Sie in der Launch-Dokumentation unter [Regeln](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Erweiterung und Regel in einer Bibliothek bündeln

Anschließend [bündeln Sie die Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/reference/publish/overview.html) und Ihre neue Regel in einer Bibliothek und testen Sie diese Änderungen in einer Entwicklungsumgebung.

![Bild](assets/launch-add-changes-to-library.png)

Nach Abschluss des Tests können Sie die Bibliothek über den Workflow freigeben, damit sie sich auf der Produktions-Site bereitstellen lässt. Nun fließen Daten von jedem einzelnen Anwender an Adobe Experience Platform.

![Bild](assets/launch-promote-library.png)

Weiterführende Informationen finden Sie in der Launch-Dokumentation unter [Bibliotheken](https://docs.adobe.com/content/help/de-DE/launch/using/reference/publish/libraries.html).