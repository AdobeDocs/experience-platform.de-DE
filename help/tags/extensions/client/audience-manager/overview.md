---
title: Adobe Audience Manager-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Audience Manager“ in Adobe Experience Platform vertraut.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 100%

---

# Adobe Audience Manager-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Mit der Audience Manager-Tag-Erweiterung können Sie den von Audience Manager verwendeten DIL-Code mit Ihren Eigenschaften in Adobe Experience Platform integrieren.

Verwenden Sie diese Referenz, um Informationen zu den verfügbaren Optionen beim Erstellen einer Regel mithilfe dieser Erweiterung zu erhalten.

>[!NOTE]
>
>Diese Erweiterung ist nicht für die Ereignisweiterleitung von Adobe Analytics-Daten vorgesehen. Verwenden Sie für die Ereignisweiterleitung die [Adobe Analytics-Erweiterung](../analytics/overview.md).

## Konfigurieren der Adobe Audience Manager-Erweiterung

Wenn die Adobe Audience Manager-Erweiterung noch nicht installiert ist, öffnen Sie Ihre Eigenschaft, klicken Sie auf **[!UICONTROL Erweiterungen > Katalog]**, bewegen Sie den Mauszeiger über die Adobe Audience Manager-Erweiterung und klicken Sie auf **[!UICONTROL Installieren]**.

Öffnen Sie zum Konfigurieren der Erweiterung die Registerkarte [!UICONTROL Erweiterungen], bewegen Sie den Mauszeiger über die Erweiterung und wählen Sie dann **[!UICONTROL Konfigurieren]** aus.

### DIL-Einstellungen

Konfigurieren Sie Ihre DIL-Einstellungen. Die folgenden Konfigurationsoptionen sind verfügbar:

![](../../../images/ext-aam-config.png)

#### DIL-Version

Zeigt die Version der Datenintegrationsbibliothek (DIL) an.

Diese Einstellung kann nicht geändert werden.

#### Ausschließen spezifischer Pfade

Wenn die URL mit einem der ausgeschlossenen Pfade übereinstimmt, wird die Erweiterung nicht geladen.

Klicken Sie auf **[!UICONTROL Pfad hinzufügen]**, um eine ausgeschlossene URL anzugeben.

Aktivieren Sie reguläre Ausdrücke, wenn die URL ein regulärer Ausdruck ist.

#### DIL Site Catalyst-Modul verwenden

Das [SiteCatalyst-Modul](https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_dil_sc_init.html) verwendet DIL, um Analytics-Tag-Elemente an Audience Manager zu senden.

Konfigurieren Sie die Datei „siteCatalyst.init“ mithilfe des Code-Editors.

Sie können auch einen Hinweis mit Informationen zu dieser Konfiguration erstellen.

#### DIL Google Analytics-Modul verwenden

Aktivieren Sie das [Google Analytics-Modul](https://experiencecloud.adobe.com/resources/help/de_DE/aam/dil-google-universal-analytics.html).

#### Initialisierungseigenschaften von „DIL.create“

Fügen Sie die von [DIL.create](https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_dil_create.html) verwendeten Initialisierungseigenschaften und die Namespace-Untereigenschaft für das [visitorService-Objekt](https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_dil_visitor_service.html) hinzu. Die Code-Kommentare des Code-Editors enthalten zwei Beispielanwendungsfälle.

Wählen Sie **[!UICONTROL Element auswählen]**, um weitere Eigenschaften hinzuzufügen.

Bewegen Sie den Mauszeiger über die „i“-Symbole, um zu erfahren, welche Funktion die einzelnen Eigenschaften haben. Weitere Informationen zu den Eigenschaften finden Sie in der [Audience Manager-DIL-Dokumentation](https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_dil_create.html).

Klicken Sie auf **[!UICONTROL Speichern]**, wenn Sie mit der Konfiguration der Erweiterung fertig sind.

## Aktionstypen der Adobe Audience Manager-Erweiterung

In diesem Thema werden die in der Audience Manager-Erweiterung verfügbaren Aktionstypen beschrieben.

Die Adobe Audience Manager-Erweiterung enthält die folgenden Aktionen im Dann-Teil einer Regel:

### Benutzerdefinierten Code ausführen

Führen Sie den im Code-Editor konfigurierten benutzerdefinierten Code aus.

Geben Sie den gewünschten Code in den Code-Editor ein. Geben Sie dann einen Namen für den Code an. Dieser Code ist anschließend im Then-Teil des Regel-Builders verfügbar.

![](../../../images/ext-aam-then.png)

Sie können auch einen Hinweis mit Informationen zu der Konfiguration hinzufügen.
