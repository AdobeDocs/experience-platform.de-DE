---
title: Installieren des Web SDK mit der Tag-Erweiterung
description: Referenzieren Sie die Web SDK-Bibliothek mithilfe der Adobe Experience Cloud-Datenerfassung.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Installieren des Web SDK mit der Tag-Erweiterung

Adobe bietet eine dedizierte Tag-Erweiterung zur Implementierung und Konfiguration des Web SDK. Diese Implementierungsmethode ist die von Adobe empfohlene primäre Methode zur Bereitstellung und Pflege des Datenerfassungscodes.

Sobald Sie die [Voraussetzungen](overview.md)können Sie die Web SDK-Tag-Erweiterung mithilfe der folgenden Schritte bereitstellen:

## Installieren der Erweiterung in einem -Tag

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus oder erstellen Sie eine Tag-Eigenschaft.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und wählen Sie dann die **[!UICONTROL Katalog]** Registerkarte.
1. Suchen und installieren Sie die **[!UICONTROL Adobe Experience Platform Web SDK]** -Erweiterung.
1. Wählen Sie für jede Umgebung die entsprechende Sandbox und den entsprechenden Datastream aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

Weitere Informationen finden Sie in der Dokumentation [Konfigurieren der Web SDK-Tag-Erweiterung](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) für weitere Informationen.

## Tag-Code in der Entwicklung veröffentlichen

Die Web SDK-Erweiterung ist jetzt für dieses Tag installiert. Sie können jetzt den Tag-Code zur Verwendung in einer Entwicklungsumgebung veröffentlichen.

1. Navigieren Sie zu **[!UICONTROL Veröffentlichungsfluss]**, wählen Sie **[!UICONTROL Bibliothek hinzufügen]**.
1. Geben Sie dieser Bibliothek den gewünschten Namen, z. B. &quot;Web SDK-Bibliothek hinzufügen&quot;. Legen Sie die [!UICONTROL Umgebung] Dropdown-Menü zu &quot;Entwicklung&quot;.
1. Auswählen **[!UICONTROL Alle geänderten Ressourcen hinzufügen]** Klicken Sie auf **[!UICONTROL Speichern und in Entwicklung erstellen]**.

## Installieren Sie den Lader-Code auf Ihrer Site

Nachdem der Tag-Code veröffentlicht wurde, können Sie den Tag-Lader-Code zu Ihrer Website hinzufügen.

1. Navigieren Sie zu **[!UICONTROL Umgebungen]** und klicken Sie dann auf das Kästchensymbol neben &quot;Entwicklung&quot;, um ein modales Fenster mit Installationsanweisungen für diese Umgebung zu öffnen.
1. Kopieren Sie den Einbettungscode und fügen Sie ihn in den `<head>` -Tag Ihrer Website.

## Füllen Sie Ihre Implementierung aus und veröffentlichen Sie sie in der Produktion.

Siehe [Übersicht über die Web SDK-Erweiterung](../../tags/extensions/client/web-sdk/overview.md) für weitere Informationen zur Erweiterung selbst und [Übersicht über Tags](../../tags/home.md) für weitere Informationen zum Navigieren in der Tags-Oberfläche.
