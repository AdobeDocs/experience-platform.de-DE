---
title: Übung Website-Tags mit Adobe Launch implementieren
seo-title: Implementieren von Website-Tags mit Adobe Launch
description: Verwenden Sie Adobe Launch, um Website-Tags in Adobe Experience Platform zu implementieren
seo-description: Verwenden Sie Adobe Launch, um Website-Tags in Adobe Experience Platform zu implementieren
translation-type: tm+mt
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3

---


# Übung:Implementieren von Website-Tags mit Adobe Launch

In diesem Lernprogramm wird beschrieben, wie Sie Ihre Website-Tags implementieren, um Daten mit Adobe Launch an Adobe Experience Platform zu senden.

## Voraussetzungen

* Das erforderliche Schema und der erforderliche Datensatz werden in Platform erstellt.
* Die erforderliche Konfiguration wurde in Experience Edge bereitgestellt und verfügt über die entsprechende Konfigurations-ID und Edge-Domäne.
* Das Unternehmens-CMS wurde bereits für die Bereitstellung eines JavaScript-Objekts auf jeder Seite mit den Daten konfiguriert, die Sie an Platform senden müssen.

## Schritte

Dieses Lernprogramm enthält die folgenden Schritte:

1. Installieren Sie die Adobe Experience Platform Web SDK-Erweiterung.
1. Erstellen Sie eine Regel, um Launch mitzuteilen, welche Daten gesendet werden sollen.
1. Bündeln Sie die Erweiterung und Regel in einer Bibliothek.

## Adobe Experience Platform Web SDK-Erweiterung installieren

Installieren Sie zunächst die Adobe Experience Platform Web SDK-Erweiterung.

1. In Launch, open the **[!UICONTROL Extensions]** tab.

   ![„image“](assets/launch-overview.png)

1. Wählen Sie die Adobe Experience Platform Web SDK-Erweiterung aus dem Starterweiterungskatalog. Der Konfigurationsbildschirm wird geöffnet.

   ![„image“](assets/launch-extension-install.png)

   Weitere Informationen finden Sie unter [Erweiterungen](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) in der Dokumentation zum Starten.

1. Erweiterungen konfigurieren.

   Die einzigen Einstellungen, die Sie jetzt benötigen, sind:

   * **** Konfigurations-ID: Geben Sie die Configuration-ID an, die Sie von Ihrem Adobe-Kundenbetreuer erhalten haben.
   * **** Edge-Domäne: Geben Sie die Edge-Domäne an, die Sie von Ihrem Adobe-Kundenbetreuer erhalten haben.

1. Klicken Sie auf **[!UICONTROL Speichern]** und fahren Sie mit dem nächsten Schritt fort.

## Regel zum Festlegen der zu sendenden Daten für Launch erstellen

Anschließend erstellen Sie eine Regel, die Launch informiert, welche Daten Sie an Adobe Experience Platform senden möchten und wann Sie sie senden möchten.

1. Konfigurieren Sie auf der Registerkarte &quot; **[!UICONTROL Regeln]** &quot;ein Ereignis, das auf jeder neuen Seite der Website ausgelöst wird, wenn die Startbibliothek geladen wird.

   ![„image“](assets/launch-make-a-rule.png)

1. Hinzufügen einer Aktion.

   Um die Aktion zu konfigurieren, teilen Sie Launch mit, wo die Datenschicht gefunden werden soll. Die Datenschicht ist ein JavaScript-Objekt, das auf der Seite vorhanden ist und von demselben CMS bereitgestellt wird, das die Webseite rendert. Geben Sie den JavaScript-Pfad zum Datenobjekt an.

   ![„image“](assets/launch-add-aep-action.png)

   Das von Ihnen gesendete Datenobjekt muss ein gültiges XDM sein, das die Validierung anhand des Schemas übergibt, das vom Datensatz verwendet wird, der mit Ihrer Konfigurations-ID verbunden ist.

1. Click **[!UICONTROL Keep Changes]**.

Weitere Informationen finden Sie unter [Regeln](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) in der Dokumentation zum Starten.

## Bündeln der Erweiterung und Regel in einer Bibliothek

Anschließend [bündeln Sie die Erweiterung](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) und Ihre neue Regel in einer Bibliothek und testen Sie diese Änderungen in einer Entwicklungsumgebung.

![„image“](assets/launch-add-changes-to-library.png)

Nach Abschluss des Tests können Sie die Bibliothek über den Workflow bewerben, damit sie auf der Produktions-Site bereitgestellt werden kann. Die Daten fließen nun von jedem einzelnen Benutzer zur Adobe Experience Platform.

![„image“](assets/launch-promote-library.png)

Weitere Informationen finden Sie unter [Bibliotheken](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) in der Dokumentation zum Starten.