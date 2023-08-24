---
keywords: Experience Platform; Benutzeroberfläche; UI; Anpassung; Dashboard zur Lizenznutzung; Dashboard; Lizenznutzung; Berechtigung; Verbrauch
title: Lizenznutzungs-Dashboard Handbuch
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen anzeigen können.
type: Documentation
hide: true
hidefromtoc: true
source-git-commit: c1ad20def39ef58253e8486ca4dcfcce2501510b
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 7%

---

# Dashboard zur Lizenznutzung (begrenzte Version) {#license-usage-dashboard-limited-release}

>[!IMPORTANT]
>
>Die aktualisierten [!UICONTROL Lizenzverwendung] Das Dashboard ist derzeit in einer **Nur begrenzte Version** und ist nicht für alle Kunden verfügbar.

Sie können wichtige Informationen zur Lizenznutzung Ihres Unternehmens über die Adobe Experience Platform anzeigen [!UICONTROL Lizenzverwendung] Dashboard. Die hier angezeigten Informationen werden während einer täglichen Momentaufnahme Ihrer Platform-Instanz erfasst.

Lizenzverwendungsberichte bieten eine hohe Granularität im Vergleich zu Ihren Lizenzverwendungsmetriken. Das Dashboard bietet Nutzungsmetriken für jedes gekaufte Produkt, die konsolidierte Verwendung von Metriken in allen Produktions- oder Entwicklungs-Sandboxes und die Nutzungsmetrik aus einer bestimmten Sandbox. Die folgenden Experience Platform-Anwendungen können mit Nutzungsmetriken verfolgt werden: Echtzeit-Kundendatenprofil, Adobe Journey Optimizer und Customer Journey Analytics.

In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard zur Lizenzverwendung in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Eine allgemeine Übersicht über die Platform-Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Experience Platform-Benutzeroberfläche](../../landing/ui-guide.md).

## [!UICONTROL Lizenzverwendung] Dashboard-Daten

Die [!UICONTROL Lizenzverwendung] Dashboard zeigt eine Liste aller von Ihnen erworbenen Experience Platform-Produkte an. Aus dieser Liste können Sie eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens zum Experience Platform in allen zugehörigen Sandboxes finden.

Die Daten in diesem Dashboard werden genau so angezeigt, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Erkunden des Lizenznutzungs-Dashboards {#explore}

Um in der Platform-Benutzeroberfläche zum Dashboard zur Lizenzverwendung zu navigieren, wählen Sie **[!UICONTROL Lizenzverwendung]** in der linken Leiste. Die [!UICONTROL Übersicht] -Tab mit einer Liste der verfügbaren Produkte öffnen.

>[!NOTE]
>
>Das Dashboard zur Lizenznutzung ist standardmäßig nicht aktiviert. Benutzer müssen[!UICONTROL Anzeigen des Dashboards zur Lizenznutzung]&quot;, um das Dashboard anzeigen zu können. Anweisungen zum Gewähren von Zugriffsberechtigungen für die Anzeige des Dashboards zur Lizenznutzung finden Sie im Abschnitt [Dashboard-Berechtigungshandbuch](../permissions.md).

![Die Registerkarte Übersicht über die Lizenznutzung des Dashboards mit der Lizenznutzung, wobei die Lizenznutzung in der linken Navigationsleiste hervorgehoben ist.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Registerkarte „Überblick“] {#overview-tab}

In diesem Dashboard werden alle lizenzierten Adobe Experience Platform-Produkte, einschließlich Add-ons, in Tabellenformat angezeigt. Die Tabelle enthält wichtige Informationen zur Nutzung Ihrer Lizenz für alle verfügbaren Profile.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Produkt]** | Die von Ihrem Unternehmen lizenzierte Adobe-Lösung. |
| **[!UICONTROL Primäre Metrik]** | Die primäre Metrik, die zur Verfolgung in für dieses Produkt verwendet wird. |
| **[!UICONTROL Lizenzbetrag]** | Der vertraglich vereinbarte Wert für den Höchstbetrag der Primären Metrik, wie in Ihrem Produktlizenzvertrag vereinbart. |
| **[!UICONTROL Verwendung]** | Die Menge Ihrer verwendeten primären Metrik. Dieser Wert gibt die Gesamtverwendung dieser Metrik über alle Sandboxes hinweg an, entweder in der Produktion oder in der Entwicklung. |
| **[!UICONTROL Verwendung %]** | Der Prozentsatz Ihrer primären Metrik, der gemäß Ihrem Lizenzbetrag verwendet wird. |

>[!NOTE]
>
>Hinzufügungen zum [!UICONTROL Lizenzbetrag] als Ergebnis von Add-ons werden über dem [!UICONTROL Lizenzbetrag] für die Basisprodukte wie Echtzeit-Kundendatenprofil, Adobe Journey Optimizer und Customer Journey Analytics. Die Verwendung dieses lizenzierten Betrags (nach den Add-ons) wird durch die Basisprodukte verfolgt. Wenn Sie beispielsweise eine Packung mit fünf Sandboxes kaufen, wird die Menge von fünf weiteren Sandboxes der Menge des Basisprodukts hinzugefügt. In diesem Fall zeigt das Add-on eine [!UICONTROL Lizenzbetrag] und die Verwendung für dieses Add-on &quot;leer&quot;ist, da die Verwendung durch das Basisprodukt verfolgt wird.

Die Tabelle zeigt die primäre Metrik für jedes Produkt an, da jedes Produkt zahlreiche Metriken verfolgen kann. Um weitere Metriken und detaillierte Einblicke in die Nutzung Ihrer Produktlizenz anzuzeigen, wählen Sie einen Produktnamen aus der Liste aus. Die [!UICONTROL Zusammenfassung] -Ansicht für dieses Produkt angezeigt.

## [!UICONTROL Registerkarte „Zusammenfassung“] {#summary-tab}

Alle verfügbaren Metriken werden auf der Seite [!UICONTROL Zusammenfassung] Registerkarte. Die verfügbaren Metriken hängen vom lizenzierten Produkt ab. Diese Ansicht bietet **eine konsolidierte Ansicht aller Metriken in allen Produktions- oder Entwicklungs-Sandboxes**. Die gleiche Analyseebene wird sowohl für Produktions- als auch für Entwicklungs-Sandboxes bereitgestellt.

![Die Zusammenfassungsansicht eines Platform-Produkts, in der alle für dieses Produkt verfügbaren Metriken angezeigt werden.]()

Im Tab Zusammenfassung enthält die Tabelle die [!UICONTROL Metrik] Spalte. Diese für Menschen lesbaren Beschreibungen zeigen alle Metriken an, die für diesen Sandbox-Typ verwendet werden.

### Sandbox auswählen {#select-sandbox}

Um die Ansicht zwischen Produktions- und Entwicklungs-Sandbox-Typen zu ändern, wählen Sie entweder [!UICONTROL Produktions-Sandboxes] oder [!UICONTROL Entwicklungs-Sandboxes]. Der ausgewählte Sandbox-Typ wird durch das Optionsfeld neben dem Sandbox-Namen angezeigt.

Die Verbrauchsberichte für Sandboxes sind kumulativ für alle Sandboxes desselben Typs. Anders ausgedrückt: durch Auswahl von [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] stellt Verbrauchsberichte für alle Produktions- bzw. Entwicklungs-Sandboxes bereit.

![Die Zusammenfassungsansicht eines Platform-Produkts mit Produktions-Sandboxes und Entwicklungs-Sandboxes hervorgehoben.](../images/license-usage/summary-tab.png)

>[!WARNING]
>
>Die Berechtigung zum Anzeigen des Dashboards zur Lizenznutzung muss auf Sandbox-Ebene angegeben werden. Sie müssen jeder einzelnen Sandbox Berechtigungen hinzufügen, damit sie im Dashboard angezeigt werden kann. Diese Einschränkung wird in einer zukünftigen Version behoben. In der Zwischenzeit ist die folgende Problemumgehung verfügbar:
>
>1. Erstellen Sie ein Produktprofil in der Adobe Admin Console.
>2. Fügen Sie unter Berechtigungen in der Kategorie Sandbox alle Sandboxes hinzu, die Sie im Dashboard zur Lizenznutzung anzeigen möchten.
>3. Fügen Sie unter der Kategorie Berechtigungen für Benutzer-Dashboard die Berechtigung &quot;Dashboard zur Nutzung der Lizenz anzeigen&quot;hinzu.

## Die [!UICONTROL Details] tab {#details-tab}

Zum Anzeigen **eine bestimmte Nutzungsmetrik aus einer bestimmten Sandbox**, navigieren Sie zum [!UICONTROL Details] Registerkarte. Die [!UICONTROL Details] -Registerkarte zeigt alle verfügbaren Sandboxes entweder in den Produktions- oder Entwicklungs-Sandboxes an.

![Registerkarte Details des Dashboards zur Lizenzverwendung.](../images/license-usage/details-tab.png)

In dieser Ansicht können Sie ![Das Inspektionssymbol.](../images/license-usage/inspect-icon.png) neben einem Sandbox-Namen, um die Visualisierung für diese Metrik anzuzeigen. Ein Dialogfeld mit einer Visualisierung für diese Metrik wird geöffnet.

### Visualisierungen {#visualizations}

Jedes Visualisierungs-Widget umfasst die folgenden Aspekte:

- Ein Liniendiagramm, das die Änderung der Metrik im Zeitverlauf verfolgt
- Ein Schlüssel für das Liniendiagramm
- den Sandbox-Namen
- Ein Dropdown-Menü zum Anpassen des Zeitraums für das Liniendiagramm

Die Liniendiagramme vergleichen die Nutzungszahlen für Ihr Unternehmen mit der Gesamtsumme, die für die Lizenzierung Ihres Unternehmens zur Verfügung steht, und geben einen Prozentsatz der Gesamtnutzung an.

![Die Visualisierung einer Metrik.](../images/license-usage/visualization.png)

Der Lookback-Zeitraum der Analyse kann über das Dropdown-Menü angepasst werden. Der Standardwert der letzten 30 Tage

Um einen Datumsbereich auszuwählen, können Sie über das Dropdown-Menü Datumsbereich den Zeitraum auswählen, der im Dashboard angezeigt werden soll. Es stehen mehrere Optionen zur Verfügung, darunter der Standardwert der letzten 30 Tage.

![Das Visualisierungsdialogfeld mit der Dropdown-Liste Datumsbereich wurde hervorgehoben.](../images/license-usage/date-range.png)

Sie können auch **[!UICONTROL Benutzerdefiniertes Datum]** , um den angezeigten Zeitraum auszuwählen.

![Im Dashboard Übersicht zur Lizenznutzung werden die benutzerdefinierten Datumsbereichsoptionen hervorgehoben.](../images/license-usage/custom-date-range.png)

## Verfügbare Metriken

Das Dashboard zur Lizenznutzung enthält Berichte zu verschiedenen eindeutigen Metriken, die für mehrere Produkte in der Organisation gelten. Die verfügbaren Metriken sind:

- [!UICONTROL Anzahl der Sandboxes]
- [!UICONTROL Addressable Audience]
- [!UICONTROL Durchschnittliche Profiltiefe]
- [!UICONTROL Hauptstunden]
- [!UICONTROL Data Lake-Speicherung]
- [!UICONTROL Daten werden pro Segmentierungsverhältnis gescannt]
- [!UICONTROL Interagierbare Zielgruppe]
- [!UICONTROL Verbrauchter Gesamtspeicher]
- [!UICONTROL Gesamtspeicher]
- [!UICONTROL Berechnungszeiten für Query Service]

Die Verfügbarkeit und spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab. Detaillierte Definitionen zu den einzelnen Metriken finden Sie in der entsprechenden Dokumentation zur Produktbeschreibung:

| Lizenz | Produktbeschreibung |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services und Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL BIS 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL BIS 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVIERUNG</li><li>AEP:OD ACTIVATION PRFL BIS 10 M</li><li>AEP:OD ACTIVATION PRFL BIS ZU 50 M</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/de/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/de/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Das Dashboard zur Lizenznutzung zeigt nur die neueste Lizenz an, die für Ihr Unternehmen bereitgestellt wurde. Wenn die neueste für Ihre Organisation bereitgestellte Lizenz nicht in der obigen Tabelle angezeigt wird, wird das Dashboard zur Lizenzverwendung möglicherweise nicht ordnungsgemäß angezeigt. Die Unterstützung für zusätzliche Lizenzen und mehrere Lizenzen in einer Organisation ist für eine künftige Version geplant.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie das Dashboard zur Lizenznutzung finden und Nutzungsmetriken für jedes gekaufte Produkt, für alle Produktions- oder Entwicklungs-Sandboxes sowie für eine bestimmte Sandbox anzeigen. Weitere Informationen zu verfügbaren Metriken für Ihr Unternehmen finden Sie auf der Grundlage der von Ihrem Unternehmen erworbenen Lizenzierung.

Weitere Informationen zu anderen in der Experience Platform-Benutzeroberfläche verfügbaren Funktionen finden Sie im Abschnitt [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).
