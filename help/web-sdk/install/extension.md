---
title: Installieren von Web SDK mithilfe der Tag-Erweiterung
description: Referenzieren Sie die Web-SDK-Bibliothek mithilfe der Adobe Experience Cloud-Datenerfassung.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Installieren von Web SDK mithilfe der Tag-Erweiterung

Adobe bietet eine dedizierte Tag-Erweiterung zur Implementierung und Konfiguration der Web-SDK. Diese Implementierungsmethode ist die von Adobe empfohlene primäre Methode zum Bereitstellen und Verwalten des Datenerfassungs-Codes.

Sobald Sie die [Voraussetzungen](overview.md) erfüllt haben, können Sie die Tag-Erweiterung für Web SDK wie folgt bereitstellen:

## Installieren der Erweiterung in einem -Tag

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus oder erstellen Sie eine Tag-Eigenschaft.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus.
1. Suchen Sie die Erweiterung **[!UICONTROL Adobe Experience Platform Web SDK]** und installieren Sie sie.
1. Wählen Sie die entsprechende Sandbox und den entsprechenden Datenstrom für jede Umgebung aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

Weitere Informationen finden Sie in der Dokumentation [ Konfigurieren der Tag](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)Erweiterung für Web SDK .

## Publish - Der Tag-Code für die Entwicklung

Für dieses Tag ist jetzt die Web SDK-Erweiterung installiert. Sie können den Tag-Code jetzt veröffentlichen, um ihn in einer Entwicklungsumgebung zu verwenden.

1. Navigieren Sie zu **[!UICONTROL Veröffentlichungsfluss]** und wählen Sie dann **[!UICONTROL Bibliothek hinzufügen]** aus.
1. Geben Sie dieser Bibliothek einen beliebigen Namen, z. B. „Web SDK Library hinzufügen“. Legen Sie [!UICONTROL &#x200B; Dropdown]Menü „Umgebung“ auf „Entwicklung“ fest.
1. Wählen Sie **[!UICONTROL Alle geänderten Ressourcen hinzufügen]** aus und klicken Sie dann auf **[!UICONTROL Speichern und für Entwicklung erstellen]**.

## Installieren des Ladercodes auf Ihrer Site

Nachdem der Tag-Code veröffentlicht wurde, können Sie den Tag-Loader-Code zu Ihrer Website hinzufügen.

1. Navigieren Sie zu **[!UICONTROL Umgebungen]** und klicken Sie dann auf das Kästchen neben „Entwicklung“, um ein modales Fenster mit Installationsanweisungen für diese Umgebung zu öffnen.
1. Kopieren Sie den Einbettungs-Code und fügen Sie ihn in das `<head>`-Tag Ihrer Website ein.

## Füllen Sie Ihre Implementierung aus und veröffentlichen Sie sie in der Produktionsumgebung

Weitere Informationen zur Erweiterung selbst finden Sie [Übersicht über die Web](../../tags/extensions/client/web-sdk/overview.md)SDK-Erweiterung) und [Übersicht über Tags](../../tags/home.md) finden Sie weitere Informationen zum Navigieren in der Tag-Oberfläche.
