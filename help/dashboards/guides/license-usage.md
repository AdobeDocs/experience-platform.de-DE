---
keywords: Experience Platform; Benutzeroberfläche; UI; Anpassung; Dashboard zur Lizenznutzung; Dashboard; Lizenznutzung; Berechtigung; Verbrauch
title: Lizenznutzungs-Dashboard Handbuch
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen anzeigen können.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: d3a1d4a65d1e5810bbc37fa9d3d230557bec39ee
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 18%

---

# Lizenznutzungs-Dashboard {#license-usage-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche verfügt über ein Dashboard, über das Sie wichtige Informationen zur Lizenznutzung Ihres Unternehmens aufrufen können. Diese Informationen werden in Form eines täglichen Snapshots erfasst. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard zur Lizenzverwendung in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Eine allgemeine Übersicht über die Platform-Benutzeroberfläche finden Sie unter [Handbuch zur Benutzeroberfläche von Experience Platform](../../landing/ui-guide.md).

## Dashboard-Daten zur Lizenznutzung

Das Dashboard zur Lizenznutzung zeigt eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens zur Experience Platform an. Die Daten im Dashboard werden genau so angezeigt, wie sie zu dem Zeitpunkt erscheinen, an dem der Snapshot erstellt wurde. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Dashboard zur Lizenznutzung

Um in der Platform-Benutzeroberfläche zum Dashboard zur Lizenzverwendung zu navigieren, wählen Sie **[!UICONTROL Lizenzverwendung]** in der linken Leiste. Dadurch wird die Registerkarte **[!UICONTROL Überblick]** mit dem Dashboard angezeigt.

>[!NOTE]
>
>Das Dashboard zur Lizenznutzung ist standardmäßig nicht aktiviert. Benutzern muss die Berechtigung &quot;Dashboard zur Lizenznutzung anzeigen&quot;gewährt werden, damit sie das Dashboard anzeigen können. Anweisungen zum Gewähren von Zugriffsberechtigungen für die Anzeige des Dashboards zur Lizenznutzung finden Sie im Abschnitt [Dashboard-Berechtigungshandbuch](../permissions.md).

![](../images/license-usage/dashboard-overview.png)

### Sandbox auswählen

Um eine Sandbox auszuwählen, die im Dashboard angezeigt werden soll, wählen Sie entweder [!UICONTROL Produktion] oder [!UICONTROL Entwicklung]. Die ausgewählte Sandbox wird durch das Optionsfeld neben dem Sandbox-Namen angezeigt.

Die Verbrauchsberichte für Sandboxes sind kumulativ für alle Sandboxes desselben Typs. Anders ausgedrückt: durch Auswahl von [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] stellt Verbrauchsberichte für alle Produktions- bzw. Entwicklungs-Sandboxes bereit.

![](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>Die Berechtigung zum Anzeigen des Dashboards zur Lizenznutzung muss auf Sandbox-Ebene angegeben werden. Das bedeutet, dass jeder einzelnen Sandbox die Berechtigung zum Anzeigen des Dashboards hinzugefügt werden muss. Diese Einschränkung wird in einer zukünftigen Version behoben. In der Zwischenzeit ist die folgende Problemumgehung verfügbar:
>
>1. Erstellen Sie ein Produktprofil in der Adobe Admin Console.
>2. Fügen Sie unter Berechtigungen in der Kategorie Sandbox alle Sandboxes hinzu, die Sie im Dashboard zur Lizenznutzung anzeigen möchten.
>3. Fügen Sie unter der Kategorie Berechtigungen für Benutzer-Dashboard die Berechtigung &quot;Dashboard zur Nutzung der Lizenz anzeigen&quot;hinzu.


### Datumsbereich auswählen

Nachdem Sie eine Sandbox ausgewählt haben, können Sie über das Dropdown-Menü Datumsbereich den Zeitraum auswählen, der im Dashboard angezeigt werden soll. Es stehen mehrere Optionen zur Verfügung, darunter der Standardwert der letzten 30 Tage.

![](../images/license-usage/select-date-range.png)

Sie können auch **[!UICONTROL Benutzerdefiniertes Datum]** , um den angezeigten Zeitraum auszuwählen.

![](../images/license-usage/select-custom-date.png)

## Widgets

Das Dashboard zur Lizenznutzung besteht aus Widgets, die schreibgeschützte Metriken anzeigen, die wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen enthalten. Die sichtbaren Metriken hängen von der spezifischen Lizenzierung Ihres Unternehmens ab (siehe [verfügbare Metriken](#available-metrics) Details).

Jedes Widget zeigt ein Liniendiagramm an, in dem die tatsächlichen Zahlen für Ihr Unternehmen mit den im Rahmen der Lizenzierung Ihres Unternehmens insgesamt verfügbaren Zahlen verglichen werden, und zeigt einen Prozentsatz der Gesamtnutzung an.

![](../images/license-usage/widgets.png)

## Verfügbare Metriken

Das Dashboard zur Lizenznutzung enthält Berichte zu vier Schlüsselmetriken, wobei weitere Metriken in nachfolgenden Versionen hinzugefügt werden müssen. Die verfügbaren Metriken sind:

* [!UICONTROL Addressable Audience]
* [!UICONTROL Durchschnittliche Profiltiefe]
* [!UICONTROL Daten werden pro Segmentierungsverhältnis gescannt]
* [!UICONTROL Verbrauchter Gesamtspeicher]

Die Verfügbarkeit und spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab. Detaillierte Definitionen der einzelnen Metriken finden Sie in der entsprechenden Dokumentation zur Produktbeschreibung:

| Lizenz | Produktbeschreibung |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, App Services und Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL BIS 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL BIS 50M</li></ul> | [Real-time Customer Data Platform](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVIERUNG</li><li>AEP:OD ACTIVATION PRFL BIS 10 M</li><li>AEP:OD ACTIVATION PRFL BIS ZU 50 M</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/de/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT:OD</li><li>Journey Optimizer PRIME:OD</li><li>Journey Optimizer ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP RTCDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Das Dashboard zur Lizenznutzung zeigt nur die neueste Lizenz an, die für Ihr Unternehmen bereitgestellt wurde. Wenn die neueste für Ihre Organisation bereitgestellte Lizenz nicht in der obigen Tabelle angezeigt wird, wird das Dashboard zur Lizenzverwendung möglicherweise nicht ordnungsgemäß angezeigt. Die Unterstützung für zusätzliche Lizenzen und mehrere Lizenzen in einer Organisation ist für eine künftige Version geplant.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie das Dashboard zur Lizenznutzung suchen und eine Sandbox auswählen, die angezeigt werden soll. Weitere Informationen zu verfügbaren Metriken für Ihr Unternehmen finden Sie auf der Grundlage der von Ihrem Unternehmen erworbenen Lizenz.

Weitere Informationen zu anderen in der Experience Platform-Benutzeroberfläche verfügbaren Funktionen finden Sie im Abschnitt [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).
