---
title: Adobe Experience Platform Web SDK-Erweiterung Übersicht
description: Weitere Informationen zur Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 53%

---


# Übersicht über die Adobe Experience Platform Web SDK-Erweiterung

Die Adobe Experience Platform Web SDK Extension sendet Daten aus Webeigenschaften über das Adobe Experience Platform Edge Network an das Adobe Experience Cloud. Die Adobe Experience Platform Web SDK-Erweiterung ermöglicht das Streamen von Daten zu Platform, die Synchronisierung von Identitäten, das Opt-in und die automatische Erfassung von Kontextdaten.

## Konfigurieren Sie die Erweiterung

Dieser Abschnitt bietet eine Referenz zu den verfügbaren Optionen beim Konfigurieren der Adobe Experience Platform Web SDK-Erweiterung.

Wenn die Adobe Experience Platform Web SDK-Erweiterung noch nicht installiert ist, öffnen Sie Ihre Eigenschaft, wählen Sie **[!UICONTROL Erweiterungen > Katalog]**, halten Sie den Mauszeiger über die Adobe Experience Platform Web SDK-Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

Um die Erweiterung zu konfigurieren, öffnen Sie die Registerkarte **[!UICONTROL Erweiterungen]**, halten Sie den Mauszeiger über die Erweiterung und wählen Sie **[!UICONTROL Konfigurieren]**.

![](./assets/ext-aep-config.png)

### Name der Instanz

Die Adobe Experience Platform Web SDK-Erweiterung unterstützt mehrere Instanzen auf der Seite. Dadurch können Daten mit einer einzigen Adobe Experience Platform Launch-Konfiguration an mehrere Organisationen gesendet werden. Der Standardwert für **[!UICONTROL Name]** ist Legierung. Sie können den Instanznamen jedoch in einen beliebigen anderen gültigen JavaScript-Objektnamen ändern. Für die Adobe Experience Platform-Erweiterung ist es erforderlich, dass jede Instanz über eine andere **[!UICONTROL Konfigurations-ID]** und eine andere **[!UICONTROL Organisations-ID]** verfügt.

## **[!UICONTROL Konfigurations-ID]**

Die **[!UICONTROL Konfigurations-ID]** gibt Adobe Experience Platform an, wohin die Daten geleitet werden sollen und welche Konfigurationen auf dem Server verwendet werden sollen. Dies ist unbedingt erforderlich, damit die Adobe Experience Platform-Erweiterung funktioniert. Wenn Sie eine Konfigurations-ID benötigen, wenden Sie sich an die Kundenunterstützung.


### **[!UICONTROL Organisations-ID]**

Die **[!UICONTROL Organisations-ID]** ist das Unternehmen, an das die Daten zur Adobe gesendet werden sollen. Meistens können Sie den Standardwert verwenden, der automatisch eingefügt wird. Wenn Sie mehrere Instanzen auf der Seite haben, geben Sie hier den Wert der zweiten Organisation ein, an die Sie Daten senden möchten.

### **[!UICONTROL Edge-Domäne]**

Die **[!UICONTROL Edge-Domäne]** ist die Domäne, von der die Adobe Experience Platform-Erweiterung Daten sendet und empfängt. Für die Erweiterung ist es erforderlich, dass Sie einen Erstanbieter-CNAME für den Produktions-Traffic verwenden. Die standardmäßige Drittanbieterdomäne funktioniert in Entwicklungsumgebungen, ist jedoch nicht für Produktionsumgebungen geeignet. Anweisungen zum Einrichten eines Erstanbieter-CNAME finden Sie [hier](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Fehler aktivieren]**

Wenn bei der Erweiterung ein Fehler auftritt, wird dieser standardmäßig in der Konsole protokolliert. Wenn Sie die Fehler in einer Produktions-Umgebung ausblenden möchten, können Sie das Kontrollkästchen **[!UICONTROL Fehler aktivieren]** deaktivieren. Wenn das Debugging in Platform Launch aktiviert ist, werden Fehler aber weiterhin ausgegeben.

### **[!UICONTROL Teilnahme aktivieren]**

Wenn **[!UICONTROL Opt-in aktivieren]** aktiviert ist, kann die Erweiterung Treffer halten, bis die Teilnahme empfangen wird. In der Erweiterung ist eine Aktion zum Einrichten der Opt-in-Einstellungen vorhanden.

### **[!UICONTROL ECID migrieren aktivieren]**

Die Platform Web SDK-Erweiterung verwendet ein neues Cookie, um die ECID zu speichern. Diese Einstellung ermöglicht die Kompatibilität zwischen dem neuen und alten Cookie zu Migrationszwecken. Adobe empfiehlt dringend, diese Option zu aktivieren, es sei denn, Sie haben keine vorhandenen Besucher mit einer ECID.

### **[!UICONTROL Drittanbieter-Cookies verwenden]**

Adobe Experience Platform speichert ein Cookie immer in der Erstanbieterdomäne. Mit dieser Option können Sie neben dem Cookie in der Erstanbieterdomäne auch ein Drittanbieter-Cookie verwenden, das in demdex.net eingerichtet wurde. Dies kann hilfreich sein, wenn Benutzer zwischen mehreren Domänen wechseln. Dadurch werden Aufrufe von demdex.net deaktiviert.

### **[!UICONTROL Kontext]**

Die Erweiterung erfasst automatisch Informationen zum Kontext der Anfrage (z.. B. Details zur URL und zum Browser). Dies kann durch das Deselektieren einzelner Kontexte deaktiviert werden.

- **[!UICONTROL web]**  - Details zur Webseite wie URL, Werber usw.
- **[!UICONTROL device]**  - Details zum Gerät, z. B. Bildschirmausrichtung, Bildschirmhöhe und Bildschirmbreite.
- **[!UICONTROL Umgebung]**  - Informationen zur Computing-Umgebung (Browser, Verbindung usw.)
- **[!UICONTROL location]**  - Begrenzte Informationen zum Standort des Benutzers

## Nächste Schritte

1. Legen Sie [Aktionstypen](action-types.md) fest.
2. Stellen Sie [Datenelementtypen](data-element-types.md) ein.
