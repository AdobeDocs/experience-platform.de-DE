---
title: Adobe Experience Platform Web SDK-Konfiguration
description: Erfahren Sie mehr über die Adobe Experience Platform Web SDK-Tag-Erweiterung.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 8%

---

# Übersicht

Die Adobe Experience Platform Web SDK-Erweiterung sendet Daten aus Webeigenschaften über das Adobe Experience Platform Edge Network an Adobe Experience Cloud. Mit der Erweiterung können Sie Daten in Platform streamen, Identitäten synchronisieren, Zustimmungssignale von Kunden verarbeiten und automatisch Kontextdaten erfassen.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung in der Datenerfassungs-Benutzeroberfläche konfigurieren.

## Konfigurieren Sie die Erweiterung

Wenn die Platform Web SDK-Erweiterung bereits für eine Eigenschaft installiert wurde, öffnen Sie die Eigenschaft in der Datenerfassungs-Benutzeroberfläche und wählen Sie die Registerkarte **[!UICONTROL Erweiterungen]** aus. Wählen Sie unter dem Platform Web SDK **[!UICONTROL Configure]** aus.

![](../images/extension/overview/configure.png)

Wenn Sie die Erweiterung noch nicht installiert haben, wählen Sie die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie in der Liste der verfügbaren Erweiterungen die Platform Web SDK-Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![](../images/extension/overview/install.png)

In beiden Fällen gelangen Sie zur Konfigurationsseite für das Platform Web SDK. In den folgenden Abschnitten werden die Konfigurationsoptionen der Erweiterung beschrieben.

![](../images/extension/overview/config-screen.png)

## Allgemeine Konfigurationsoptionen

Die Konfigurationsoptionen oben auf der Seite geben Adobe Experience Platform an, wohin die Daten weitergeleitet werden sollen und welche Konfigurationen auf dem Server verwendet werden sollen.

### [!UICONTROL Name]

Die Adobe Experience Platform Web SDK-Erweiterung unterstützt mehrere Instanzen auf der Seite. Der Name wird verwendet, um Daten mit einer Tag-Konfiguration an mehrere Organisationen zu senden.

Der Name der Erweiterung wird standardmäßig auf &quot;[!DNL alloy]&quot;festgelegt. Sie können den Instanznamen jedoch in einen beliebigen anderen gültigen JavaScript-Objektnamen ändern.

### **[!UICONTROL IMS-Organisations-ID]**

Die [!UICONTROL IMS-Organisations-ID] ist die Organisation, an die die Daten zur Adobe gesendet werden sollen. Meistens verwenden Sie den Standardwert, der automatisch ausgefüllt wird. Wenn sich auf der Seite mehrere Instanzen befinden, geben Sie in dieses Feld den Wert der zweiten Organisation ein, an die Sie Daten senden möchten.

### **[!UICONTROL Edge-Domäne]**

Die [!UICONTROL Edge-Domäne] ist die Domäne, von der die Adobe Experience Platform-Erweiterung Daten sendet und empfängt. Für die Erweiterung ist es erforderlich, dass Sie einen Erstanbieter-CNAME für den Produktions-Traffic verwenden. Die standardmäßige Drittanbieterdomäne funktioniert in Entwicklungsumgebungen, ist jedoch nicht für Produktionsumgebungen geeignet. Anweisungen zum Einrichten eines Erstanbieter-CNAME finden Sie [hier](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=de).

## [!UICONTROL Datenströme]

Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, wird eine Datastraam-ID verwendet, um auf die serverseitige Konfiguration zu verweisen. Sie können die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Weitere Informationen finden Sie im Handbuch zu [datastreams](../fundamentals/datastreams.md) .


## [!UICONTROL Datenschutz]

![](../images/extension/overview/privacy.png)

Im Abschnitt [!UICONTROL Datenschutz] können Sie konfigurieren, wie das SDK Zustimmungssignale von Benutzern von Ihrer Website verarbeitet. Insbesondere können Sie damit das standardmäßige Zustimmungsniveau auswählen, das von einem Benutzer angenommen wird, wenn keine andere explizite Zustimmungsvoreinstellung angegeben wurde. Die standardmäßige Zustimmungsstufe wird nicht im Profil des Benutzers gespeichert. In der folgenden Tabelle wird aufgeschlüsselt, was jede Option beinhaltet:

| [!UICONTROL Standardmäßige Zustimmungsstufe] | Beschreibung |
| --- | --- |
| [!UICONTROL Enthalten] | Erfassen Sie Ereignisse, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. |
| [!UICONTROL Out] | Verwerfen Sie Ereignisse, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. |
| [!UICONTROL Ausstehend] | Einreihen von Ereignissen in die Warteschlange, die auftreten, bevor der Benutzer Zustimmungsvoreinstellungen bereitstellt. Wenn Zustimmungsvoreinstellungen angegeben werden, werden die Ereignisse abhängig von den bereitgestellten Voreinstellungen erfasst oder verworfen. |
| [!UICONTROL Wird vom Datenelement bereitgestellt] | Die standardmäßige Zustimmungsstufe wird durch ein eigenes Datenelement bestimmt, das Sie definieren. Bei Verwendung dieser Option müssen Sie das Datenelement über das bereitgestellte Dropdown-Menü angeben. |

Verwenden Sie &quot;Out&quot;oder &quot;Ausstehend&quot;, wenn Sie eine ausdrückliche Benutzerzustimmung für Ihre Geschäftsvorgänge benötigen.

## [!UICONTROL Identität]

![](../images/extension/overview/identity.png)

### [!UICONTROL Migrieren der ECID aus der VisitorAPI]

Standardmäßig ist diese Option aktiviert. Wenn diese Funktion aktiviert ist, kann das SDK die AMCV- und s_ecid-Cookies lesen und das von Visitor.js verwendete AMCV-Cookie festlegen. Diese Funktion ist bei der Migration zum Adobe Experience Platform Web SDK wichtig, da einige Seiten möglicherweise noch Visitor.js verwenden. Dadurch kann das SDK weiterhin dieselbe ECID verwenden, sodass Benutzer nicht als zwei separate Benutzer identifiziert werden.

### [!UICONTROL Verwenden von Drittanbieter-Cookies]

Mit dieser Option kann das SDK versuchen, eine Benutzer-ID in einem Drittanbieter-Cookie zu speichern. Bei erfolgreicher Ausführung wird der Benutzer als einzelner Benutzer identifiziert, der über mehrere Domänen navigiert, anstatt für jede Domäne als separater Benutzer identifiziert zu werden. Wenn diese Option aktiviert ist, kann das SDK die Benutzer-ID möglicherweise weiterhin nicht in einem Drittanbieter-Cookie speichern, wenn der Browser keine Drittanbieter-Cookies unterstützt oder vom Benutzer so konfiguriert wurde, dass keine Drittanbieter-Cookies zugelassen werden. In diesem Fall speichert das SDK die Kennung nur in der Erstanbieterdomäne.

## [!UICONTROL Personalisierung]

![](../images/extension/overview/personalization.png)

Wenn Sie bestimmte Teile ausblenden möchten, wenn Ihre Site beim Laden personalisierter Inhalte geladen wird, können Sie die Elemente angeben, die im Stil-Editor zum Vorab-Ausblenden ausgeblendet werden sollen. Anschließend können Sie das Ihnen bereitgestellte standardmäßige Codefragment zur Vorab-Ausblendung kopieren und in das Element `<head>`Ihrer HTML-Site einfügen.

## [!UICONTROL Datenerfassung]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL Callback-Funktion]

Die in der Erweiterung bereitgestellte Rückruffunktion wird in der Bibliothek auch als [`onBeforeEventSend` Funktion](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) bezeichnet. Mit dieser Funktion können Sie Ereignisse global ändern, bevor sie an Adobe Edge Network gesendet werden. Ausführlichere Informationen zur Verwendung dieser Funktion finden Sie unter [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Klickdatenerfassung]

Das SDK kann automatisch Link-Klickinformationen für Sie erfassen. Standardmäßig ist diese Funktion aktiviert, kann jedoch über diese Option deaktiviert werden. Links werden auch als Downloadlinks bezeichnet, wenn sie einen der im Textfeld [!UICONTROL Download-Link-Qualifizierer] aufgelisteten Download-Ausdrücke enthalten. Adobe bietet einige standardmäßige Downloadlink-Kennungen, die jedoch jederzeit bearbeitet werden können.

### [!UICONTROL Automatisch erfasste Kontextdaten]

Standardmäßig erfasst das SDK bestimmte Kontextdaten in Bezug auf Gerät, Web, Umgebung und Ortskontext. Wenn Sie eine Liste der von der Adobe erfassten Informationen sehen möchten, finden Sie diese [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Wenn Sie diese Daten nicht erfassen möchten oder nur bestimmte Datenkategorien erfassen möchten, können Sie diese Optionen ändern.

## [!UICONTROL Erweiterte Einstellungen]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL Edge-Basispfad]

Verwenden Sie dieses Feld, wenn Sie den Basispfad für die Interaktion mit dem Adobe Edge-Netzwerk ändern müssen. Dies sollte keine Aktualisierung erfordern, aber falls Sie an einer Beta- oder Alpha-Phase teilnehmen, kann die Adobe Sie bitten, dieses Feld zu ändern.
