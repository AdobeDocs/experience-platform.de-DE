---
keywords: Experience Platform;Benutzeroberfläche;Anpassung;Lizenznutzung Dashboard;Dashboard;Lizenzverwendung;Berechtigungen;Verbrauch
title: Dashboard der Lizenzverwendung
description: Adobe Experience Platform bietet ein Dashboard zur Ansicht wichtiger Informationen zur Lizenznutzung in Ihrem Unternehmen.
topic-legacy: guide
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 3%

---

# (Beta) Dashboard zur Lizenzverwendung {#license-usage-dashboard}

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion befindet sich derzeit in der Beta-Version und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard, mit dem Sie wichtige Informationen zur Lizenznutzung in Ihrem Unternehmen, wie sie in einem täglichen Schnappschuss erfasst werden, Ansichten vornehmen können. In diesem Handbuch wird beschrieben, wie Sie auf das Lizenzverwendungs-Dashboard in der Benutzeroberfläche zugreifen und mit ihm arbeiten. Außerdem werden weitere Informationen zu den Visualisierungen im Dashboard bereitgestellt.

Eine allgemeine Übersicht über die Plattform-Benutzeroberfläche finden Sie im Handbuch [Experience Platform UI guide](../../landing/ui-guide.md).

## Daten zum Dashboard der Lizenzverwendung

Das Dashboard zur Lizenznutzung zeigt eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens zur Experience Platform an. Die Daten im Dashboard werden exakt so angezeigt, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Erstellung des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Dashboard zur Lizenznutzung

Um zum Dashboard zur Lizenzverwendung in der Plattform-Benutzeroberfläche zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Lizenzverwendung]**. Dies wird mit der Registerkarte **[!UICONTROL Übersicht]** geöffnet, auf der das Dashboard angezeigt wird.

![](../images/license-usage/dashboard-overview.png)

### Sandbox auswählen

Um eine zu Ansicht Sandbox im Dashboard auszuwählen, wählen Sie entweder [!UICONTROL Produktion] oder [!UICONTROL Entwicklung]. Die ausgewählte Sandbox wird durch das Optionsfeld neben dem Sandbox-Namen angezeigt.

>[!NOTE]
>
>Der Berichte &quot;Verbrauch&quot;für Sandboxen ist für alle Sandboxen desselben Typs kumulativ. Anders ausgedrückt, bietet die Auswahl von [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] Verbrauchsberichte für alle Produktions- bzw. Entwicklungs-Sandboxen.

![](../images/license-usage/select-sandbox.png)

### Datumsbereich auswählen

Nach Auswahl einer Sandbox können Sie mit der Dropdownliste Datumsbereich den Zeitraum auswählen, der im Dashboard angezeigt werden soll. Es stehen drei Optionen zur Verfügung: [!UICONTROL Letzte 30 Tage], [!UICONTROL Letzte 90 Tage] und [!UICONTROL Letzte 12 Monate]. Die letzten 30 Tage sind standardmäßig ausgewählt.

![](../images/license-usage/select-date-range.png)

## Widgets

Das Dashboard zur Lizenznutzung besteht aus Widgets, die schreibgeschützte Metriken anzeigen, die wichtige Informationen zur Lizenznutzung in Ihrem Unternehmen enthalten. Die sichtbaren Metriken hängen von der spezifischen Lizenzierung Ihres Unternehmens ab (Einzelheiten finden Sie im Abschnitt [Verfügbare Metriken](#available-metrics)).

Jedes Widget zeigt ein Liniendiagramm an, in dem die tatsächlichen Zahlen für Ihr Unternehmen mit den im Rahmen der Lizenzierung Ihres Unternehmens verfügbaren Gesamtwerten verglichen werden, und zeigt einen Prozentsatz der Gesamtnutzung an.

![](../images/license-usage/widgets.png)

## Verfügbare Metriken

Im Dashboard zur Lizenznutzung stehen derzeit vier Metriken zur Verfügung:

* [!UICONTROL Addressable Audience]  (gemessen nach Anzahl der Profil)
* [!UICONTROL Durchschnittlicher Reichtum des Profils]
* [!UICONTROL Konsumierte Datenspeicherung insgesamt]
* [!UICONTROL Daten gescannt nach Segmentierungsverhältnis]

Die Definition dieser Metriken hängt von der Lizenzierung ab, die Ihr Unternehmen erworben hat. Detaillierte Definitionen zu den einzelnen Metriken finden Sie in der entsprechenden Dokumentation zur Produktbeschreibung:

| Lizenz | Produktbeschreibung |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, App-Dienste und intelligente Dienste](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT-KUNDENDATENPLATTFORM:OD</li><li>RT-KUNDENDATENPLATTFORM:OD PRFL BIS 10 M</li><li>RT-KUNDENDATENPLATTFORM:OD PRFL BIS 50 M</li></ul> | [Echtzeit-Kundendatenplattform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVIERUNG</li><li>AEP:OD AKTIVIERUNG PRFL BIS 10 M</li><li>AEP:OD AKTIVIERUNG PRFL BIS ZU 50 M</li></ul> | [Adobe Experience Platform Aktivierung](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie das Dashboard zur Lizenznutzung suchen und eine zu Ansicht Sandbox auswählen. Weitere Informationen zu den verfügbaren Metriken für Ihr Unternehmen finden Sie auf der Grundlage der von Ihrem Unternehmen erworbenen Lizenzen.

Weitere Informationen zu anderen Funktionen in der Benutzeroberfläche der Experience Platform finden Sie im Handbuch [Plattformbenutzeroberfläche](../../landing/ui-guide.md).
