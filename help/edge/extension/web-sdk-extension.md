---
title: Adobe Experience Platform Web SDK-Erweiterung Übersicht
description: Weitere Informationen zur Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 19%

---


# Übersicht über die Adobe Experience Platform Web SDK-Erweiterung

Die Adobe Experience Platform Web SDK-Erweiterung sendet Daten aus Webeigenschaften über das Adobe Experience Platform Edge Network an Adobe Experience Cloud. Mit der Erweiterung können Sie Daten in Plattform streamen, Identitäten synchronisieren, Signale für die Zustimmung des Kunden verarbeiten und automatisch Kontextdaten erfassen.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung in der Adobe Experience Platform Launch-Benutzeroberfläche konfigurieren.

## Konfigurieren Sie die Erweiterung

Wenn die Platform Web SDK-Erweiterung bereits für eine Eigenschaft installiert wurde, öffnen Sie die Eigenschaft in der Benutzeroberfläche der Platform launch und wählen Sie die Registerkarte **[!UICONTROL Erweiterungen]**. Wählen Sie unter Plattform-Web-SDK **[!UICONTROL Konfigurieren]**.

![](../images/extension/overview/configure.png)

Wenn Sie die Erweiterung noch nicht installiert haben, wählen Sie die Registerkarte **[!UICONTROL Katalog]**. Suchen Sie in der Liste der verfügbaren Erweiterungen die Plattform-Web-SDK-Erweiterung und wählen Sie **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

In beiden Fällen gelangen Sie zur Konfigurationsseite für das Platform Web SDK. Die folgenden Abschnitte erläutern die Konfigurationsoptionen der Erweiterung.

![](../images/extension/overview/config-screen.png)

## Allgemeine Konfigurationsoptionen

Die Konfigurationsoptionen oben auf der Seite geben Adobe Experience Platform an, wohin die Daten weitergeleitet werden sollen und welche Konfigurationen auf dem Server verwendet werden sollten.

### [!UICONTROL Name]

Die Adobe Experience Platform Web SDK-Erweiterung unterstützt mehrere Instanzen auf der Seite. Dadurch können Daten mit einer einzigen Platform Launch-Konfiguration an mehrere Organisationen gesendet werden.

Der Name der Erweiterung lautet standardmäßig &quot;[!DNL alloy]&quot;. Sie können den Instanznamen jedoch in einen beliebigen anderen gültigen JavaScript-Objektnamen ändern.

### **[!UICONTROL IMS-Organisations-ID]**

Die [!UICONTROL IMS-Organisations-ID] ist das Unternehmen, an das die Daten zur Adobe gesendet werden sollen. Meistens können Sie den Standardwert verwenden, der automatisch eingefügt wird. Wenn Sie mehrere Instanzen auf der Seite haben, füllen Sie dieses Feld mit dem Wert der zweiten Organisation, an die Sie Daten senden möchten.

### **[!UICONTROL Edge-Domäne]**

Die [!UICONTROL Edge-Domäne] ist die Domäne, von der die Adobe Experience Platform-Erweiterung Daten sendet und empfängt. Für die Erweiterung ist es erforderlich, dass Sie einen Erstanbieter-CNAME für den Produktions-Traffic verwenden. Die standardmäßige Drittanbieterdomäne funktioniert in Entwicklungsumgebungen, ist jedoch nicht für Produktionsumgebungen geeignet. Anweisungen zum Einrichten eines Erstanbieter-CNAME finden Sie [hier](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge-Konfigurationen]

Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, wird eine Edge-Konfigurations-ID verwendet, um auf die serverseitige Konfiguration zu verweisen. Dadurch können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Weitere Informationen finden Sie im Handbuch [Edge-Konfigurationen](../fundamentals/edge-configuration.md).

## [!UICONTROL Datenschutz]

Im Abschnitt [!UICONTROL Privatsphäre] können Sie konfigurieren, wie das SDK mit den Signalen für die Kundengenehmigung von Ihrer Website umgeht. Sie ermöglicht es Ihnen insbesondere, das Standardniveau der Zustimmung auszuwählen, das von einem Kunden angenommen wird, wenn keine andere ausdrückliche Zustimmung angegeben wurde. Die folgende Tabelle zeigt, was jede Option beinhaltet:

| [!UICONTROL Standardebene für Zustimmung] | Beschreibung |
| --- | --- |
| [!UICONTROL Enthalten] | Anmelden. Verwenden Sie diese Option, wenn Sie die Zustimmung des Kunden standardmäßig und nur Ausschlusssignale annehmen. |
| [!UICONTROL Ausstehend] | Kunden mit &quot;ausstehender&quot;Zustimmung werden bis zum Senden eines Opt-in-Signals abgemeldet. Verwenden Sie diese Option, wenn Sie eine ausdrückliche Zustimmung des Kunden für Ihre Geschäftsvorgänge benötigen. |
| [!UICONTROL Von Datenelement bereitgestellt] | Die standardmäßige Ebene der Zustimmung wird durch ein gesondertes Datenelement bestimmt, das Sie definieren. Wenn Sie diese Option verwenden, müssen Sie das Datenelement über das Dropdown-Menü angeben. |