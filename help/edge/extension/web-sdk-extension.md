---
title: Adobe Experience Platform Web SDK-Erweiterung – Übersicht
description: Erfahren Sie mehr über die Adobe Experience Platform Web SDK-Erweiterung für Adobe Experience Platform Launch
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 13%

---

# Adobe Experience Platform Web SDK-Erweiterung – Übersicht

Die Adobe Experience Platform Web SDK-Erweiterung sendet Daten aus Webeigenschaften über das Adobe Experience Platform Edge Network an Adobe Experience Cloud. Mit der Erweiterung können Sie Daten in Platform streamen, Identitäten synchronisieren, Zustimmungssignale von Kunden verarbeiten und automatisch Kontextdaten erfassen.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung in der Benutzeroberfläche von Adobe Experience Platform Launch konfigurieren.

## Konfigurieren Sie die Erweiterung

Wenn die Platform Web SDK-Erweiterung bereits für eine Eigenschaft installiert wurde, öffnen Sie die Eigenschaft in der Platform launch-Benutzeroberfläche und wählen Sie die Registerkarte **[!UICONTROL Erweiterungen]** aus. Wählen Sie unter dem Platform Web SDK **[!UICONTROL Configure]** aus.

![](../images/extension/overview/configure.png)

Wenn Sie die Erweiterung noch nicht installiert haben, wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie in der Liste der verfügbaren Erweiterungen die Platform Web SDK-Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![](../images/extension/overview/install.png)

In beiden Fällen gelangen Sie zur Konfigurationsseite für das Platform Web SDK. In den folgenden Abschnitten werden die Konfigurationsoptionen der Erweiterung beschrieben.

![](../images/extension/overview/config-screen.png)

## Allgemeine Konfigurationsoptionen

Die Konfigurationsoptionen oben auf der Seite geben Adobe Experience Platform an, wohin die Daten weitergeleitet werden sollen und welche Konfigurationen auf dem Server verwendet werden sollen.

### [!UICONTROL Name]

Die Adobe Experience Platform Web SDK-Erweiterung unterstützt mehrere Instanzen auf der Seite. Der Name wird verwendet, um Daten mit einer einzigen Platform launch-Konfiguration an mehrere Unternehmen zu senden.

Der Name der Erweiterung wird standardmäßig auf &quot;[!DNL alloy]&quot;festgelegt. Sie können den Instanznamen jedoch in einen beliebigen anderen gültigen JavaScript-Objektnamen ändern.

### **[!UICONTROL IMS-Organisations-ID]**

Die [!UICONTROL IMS-Organisations-ID] ist die Organisation, an die die Daten zur Adobe gesendet werden sollen. Meistens verwenden Sie den Standardwert, der automatisch ausgefüllt wird. Wenn sich auf der Seite mehrere Instanzen befinden, geben Sie in dieses Feld den Wert der zweiten Organisation ein, an die Sie Daten senden möchten.

### **[!UICONTROL Edge-Domäne]**

Die [!UICONTROL Edge-Domäne] ist die Domäne, von der die Adobe Experience Platform-Erweiterung Daten sendet und empfängt. Für die Erweiterung ist es erforderlich, dass Sie einen Erstanbieter-CNAME für den Produktions-Traffic verwenden. Die standardmäßige Drittanbieterdomäne funktioniert in Entwicklungsumgebungen, ist jedoch nicht für Produktionsumgebungen geeignet. Anweisungen zum Einrichten eines Erstanbieter-CNAME finden Sie [hier](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datenspeicher]

Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, wird eine Datastraam-ID verwendet, um auf die serverseitige Konfiguration zu verweisen. Sie können die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Weitere Informationen finden Sie im Handbuch zu [datastreams](../fundamentals/datastreams.md) .


## [!UICONTROL Datenschutz]

Im Abschnitt [!UICONTROL Datenschutz] können Sie konfigurieren, wie das SDK Zustimmungssignale von Benutzern von Ihrer Website verarbeitet. Insbesondere können Sie damit das standardmäßige Zustimmungsniveau auswählen, das von einem Benutzer angenommen wird, wenn keine andere explizite Zustimmungsvoreinstellung angegeben wurde. Die standardmäßige Zustimmungsstufe wird nicht im Profil des Benutzers gespeichert. In der folgenden Tabelle wird aufgeschlüsselt, was jede Option beinhaltet:

| [!UICONTROL Standardmäßige Zustimmungsstufe] | Beschreibung |
| --- | --- |
| [!UICONTROL Enthalten] | Erfassen Sie Ereignisse, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. |
| [!UICONTROL Out] | Verwerfen Sie Ereignisse, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. |
| [!UICONTROL Ausstehend] | Einreihen von Ereignissen in die Warteschlange, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. Wenn Zustimmungsvoreinstellungen angegeben werden, werden die Ereignisse abhängig von den bereitgestellten Voreinstellungen erfasst oder verworfen. |
| [!UICONTROL Wird vom Datenelement bereitgestellt] | Die standardmäßige Zustimmungsstufe wird durch ein eigenes Datenelement bestimmt, das Sie definieren. Bei Verwendung dieser Option müssen Sie das Datenelement über das bereitgestellte Dropdown-Menü angeben. |

Verwenden Sie &quot;Out&quot;oder &quot;Ausstehend&quot;, wenn Sie eine ausdrückliche Benutzerzustimmung für Ihre Geschäftsvorgänge benötigen.
