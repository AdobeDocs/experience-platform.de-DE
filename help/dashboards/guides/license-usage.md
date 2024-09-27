---
keywords: Experience Platform; Benutzeroberfläche; UI; Anpassung; Dashboard zur Lizenznutzung; Dashboard; Lizenznutzung; Berechtigung; Verbrauch
title: Lizenznutzungs-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen anzeigen können.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 67d4bcbf2a055d4427218ba7d98355f09d860a8c
workflow-type: tm+mt
source-wordcount: '2738'
ht-degree: 16%

---

# Lizenznutzungs-Dashboard {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Testdialogfeld, das nicht sichtbar sein sollte"
>abstract="Das Objekt {name} wird am {date} angezeigt."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Kernprodukttabelle"
>abstract="Die in der Tabelle aufgelisteten Hauptprodukte verfügen über eigene Metriken, Nutzungsverfolgung und Drillthrough-Ansichten auf Sandbox-Ebene. Diese Hauptprodukte stellen die Schlüsselmetriken für die Verfolgung bereit. Alle Add-ons sind in diesen Metriken enthalten."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Add-ons-Tabelle"
>abstract="In der Tabelle Add-ons werden Produkte aufgelistet, deren Lizenzmengen mit den von Kernprodukten unterstützten Metriken kombiniert werden. Diese Add-ons verfügen nicht über separate Metriken, sondern verbessern die Nutzungsverfolgung der Kernprodukte, mit denen sie verknüpft sind."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Lizenznutzungs-Dashboard"
>abstract="Das Lizenznutzungs-Dashboard bietet Einblicke in die von Ihnen erworbenen Adobe Experience Platform-Produkte. In der Dashboard-Übersicht werden die primären Metriken für Ihre Produkte angezeigt, einschließlich Ihrer Nutzung für jede der primären Metriken, sowie Ihr vertraglich vereinbarter Lizenzbetrag. Im Arbeitsbereich „Details“ wird eine Aufschlüsselung Ihrer Metriken für jedes Produkt innerhalb bestimmter Sandboxes angezeigt."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Datensatzablauffristen"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/profile/pseudonymous-profiles" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Lizenznutzungs-Dashboard"
>abstract="Das Lizenznutzungs-Dashboard bietet Einblicke in die von Ihnen erworbenen Adobe Experience Platform-Produkte. In der Dashboard-Übersicht werden die primären Metriken für Ihre Produkte angezeigt, einschließlich Ihrer Nutzung für jede der primären Metriken, sowie Ihr vertraglich vereinbarter Lizenzbetrag. Im Arbeitsbereich „Details“ wird eine Aufschlüsselung Ihrer Metriken für jedes Produkt innerhalb bestimmter Sandboxes angezeigt."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Datensatzablauffristen"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/profile/pseudonymous-profiles" text="Ablauf von Daten pseudonymer Profile"

Wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen finden Sie im Dashboard für die Adobe Experience Platform [!UICONTROL Lizenznutzung] . Die hier angezeigten Informationen werden während einer täglichen Momentaufnahme Ihrer Platform-Instanz erfasst.

Lizenzverwendungsberichte bieten eine hohe Granularität im Vergleich zu Ihren Lizenzverwendungsmetriken. Das Dashboard bietet Nutzungsmetriken für jedes gekaufte Produkt (und zugehörige Add-ons), die konsolidierte Verwendung von Metriken in allen Produktions- oder Entwicklungs-Sandboxes und die Nutzungsmetrik aus einer bestimmten Sandbox. Die folgenden Experience Platform-Anwendungen können mit Nutzungsmetriken verfolgt werden: Real-time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard zur Lizenzverwendung in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Eine allgemeine Übersicht über die Platform-Benutzeroberfläche finden Sie im [Experience Platform UI-Handbuch](../../landing/ui-guide.md).

## [!UICONTROL Nutzung der Lizenz] Dashboard-Daten

Das Dashboard [!UICONTROL Lizenznutzung] enthält eine Liste aller von Ihnen erworbenen Experience Platform-Produkte sowie aller Add-ons für diese Produkte. In diesem Dashboard können Sie eine Momentaufnahme der lizenzbezogenen Daten Ihres Unternehmens zum Experience Platform in allen zugehörigen Sandboxes finden.

Die Daten in diesem Dashboard werden genau so angezeigt, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Dashboard zur Lizenznutzung {#explore}

Um in der Platform-Benutzeroberfläche zum Dashboard für die Lizenzverwendung zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Lizenzverwendung]** aus. Die Registerkarte [!UICONTROL Übersicht] wird geöffnet und enthält eine Liste der verfügbaren Produkte.

>[!NOTE]
>
>Das Dashboard zur Lizenznutzung ist standardmäßig nicht aktiviert. Benutzern muss die Berechtigung &quot;Dashboard zur Lizenznutzung anzeigen&quot;gewährt werden, damit sie das Dashboard anzeigen können. Anweisungen zum Gewähren von Zugriffsberechtigungen für die Anzeige des Dashboards zur Lizenznutzung finden Sie im [Dashboard-Berechtigungshandbuch](../permissions.md).

![Die Registerkarte Übersicht über das Dashboard zur Lizenzverwendung, wobei die Lizenznutzung in der linken Navigationsleiste hervorgehoben ist.](../images/license-usage/dashboard-overview.png)

## Registerkarte [!UICONTROL Übersicht] {#overview-tab}

Das Dashboard [!UICONTROL Lizenznutzung] enthält zwei separate Tabellen: **Core-Produkte** und **Add-ons**.

- **[!UICONTROL Kernprodukte] Tabelle**: In dieser Tabelle sind die wichtigsten Adobe Experience Platform-Produkte aufgeführt, die von Ihrem Unternehmen lizenziert wurden. Jedes Kernprodukt verfügt über eigene Metriken, Nutzungsverfolgung und Drillthrough-Ansichten auf Sandbox-Ebene. Diese Hauptprodukte stellen die Schlüsselmetriken für die Verfolgung bereit. Alle Add-ons sind in diesen Metriken enthalten.

- **[!UICONTROL Add-ons] table**: Diese Tabelle listet zusätzliche Produkte auf, deren Lizenzmengen mit den von den Kernprodukten unterstützten Metriken kombiniert werden. Add-ons verfügen nicht über separate Metriken, sondern verbessern die Nutzungsverfolgung der Kernprodukte, mit denen sie verknüpft sind.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Produkt]** | Die von Ihrem Unternehmen lizenzierte Adobe-Lösung. |
| **[!UICONTROL Primäre Metrik]** | Die primäre Metrik, die zur Verfolgung innerhalb dieses Produkts verwendet wird. |
| **[!UICONTROL Lizenzbetrag]** | Der vertraglich vereinbarte Wert für den Höchstbetrag der Primären Metrik, wie in Ihrem Produktlizenzvertrag vereinbart. |
| **[!UICONTROL Verwendung]** | Die Menge Ihrer verwendeten primären Metrik. Dieser Wert gibt die Gesamtverwendung dieser Metrik über alle Sandboxes hinweg an, entweder in der Produktion oder in der Entwicklung. |
| **[!UICONTROL Nutzung %]** | Der Prozentsatz Ihrer primären Metrik, der gemäß Ihrem Lizenzbetrag verwendet wird. |
| **[!UICONTROL Nutzung der Prognose]** | Der prognostizierte Nutzungsprozentsatz Ihrer primären Metrik entsprechend Ihrem Lizenzbetrag. |

>[!NOTE]
>
>Lizenzbeträge für Add-ons sind im [!UICONTROL Lizenzbetrag] der Kernprodukte enthalten. Wenn Sie beispielsweise eine Packung mit fünf Sandboxes als Add-on kaufen, wird der Betrag zum Basisprodukt hinzugefügt. Die Add-ons-Tabelle zeigt einen [!UICONTROL Lizenzbetrag] speziell für das Add-on an, die tatsächliche Verwendung wird jedoch über das Basisprodukt verfolgt.

Die Tabellen zeigen die primäre Metrik für jedes Produkt an, da jedes Produkt zahlreiche Metriken verfolgen kann.

### Prognostizierte Nutzung {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden jeweils am 15. jedes Monats erstellt. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie für Sandboxes und Datensätze Ablaufzeiten für Datensätze oder pseudonyme Profildaten konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Datensatzablauffristen"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/profile/pseudonymous-profiles" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden jeweils am 15. jedes Monats erstellt. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie für Sandboxes und Datensätze Ablaufzeiten für Datensätze oder pseudonyme Profildaten konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Datensatzablauffristen"
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/profile/pseudonymous-profiles" text="Ablauf von Daten pseudonymer Profile"

Proaktive Verwaltung und Optimierung Ihrer Lizenzierungsressourcen auf der Grundlage aufschlussreicher Nutzungsvorhersagen. In der Spalte [!UICONTROL Erwartete Nutzung] wird die künftige Lizenznutzung auf Sandbox-Ebene für alle Produktions- und Entwicklungs-Sandboxes für all Ihre gekauften Produkte genau vorhergesagt. Diese Warnfunktion bietet eine Prognose der zukünftigen Lizenznutzung für sechs Wochen, basierend auf Ihrer Nutzung bis zum 15. dieses Kalendermonats. Prognosen werden mit einer unteren und einer oberen Grenze bereitgestellt.

>[!IMPORTANT]
>
>Prognosen werden monatlich aktualisiert. Das Datum der Aktualisierung ist in einem Infosymbol (![Dieses Infosymbol) enthalten.](../images/license-usage/info-icon.png)) über dem Spaltentitel.

Um eine Zusammenfassung der Berechtigungsnutzung eines Produkts anzuzeigen, wählen Sie ein Produkt aus der Tabelle [!UICONTROL Kernprodukte] aus.

<!-- update image ... -->
![Die [!UICONTROL Lizenznutzung] [!UICONTROL Überblick] mit einem Produkt und der Spalte mit der voraussichtlichen Verwendung sind hervorgehoben.](../images/license-usage/product-predicted-usage.png)

Die Registerkarte Zusammenfassung wird angezeigt. Sie können die auf den Registerkarten [!UICONTROL Zusammenfassung] und [!UICONTROL Details] verfügbaren detaillierten Prognosen verwenden, um eine fundierte Entscheidungsfindung für eine effiziente Lizenzverwendung sicherzustellen.

>[!NOTE]
>
>Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung Ihres Unternehmens zu verstehen und sicherzustellen, dass die Nutzung mit Adobe nicht über den Umfang der Lizenz Ihres Unternehmens hinausgeht.

<!-- update image ... -->
![Die Zusammenfassungsansicht eines Platform-Produkts mit hervorgehobener Spalte zur prognostizierten Nutzung.](../images/license-usage/summary-predicted-usage.png)

Der Prozentsatz der prognostizierten Nutzung wird wie folgt ermittelt:

- Wenn sich die unteren und oberen Grenzen deutlich unterscheiden, werden sie als Bereich angezeigt (z. B. 32 % - 35 %).
- Wenn die oberen und unteren Begrenzungen nahezu identisch sind und nicht null, werden sie als ungefährer Wert angezeigt (z. B. ~34 %).
- Wenn die oberen und unteren Begrenzungen nahezu identisch sind und null sind, werden sie als genau 0 % angezeigt.

>[!NOTE]
>
>&quot;Fast identisch&quot;bedeutet in diesem Zusammenhang, dass die Werte statistisch auf zwei Dezimalstellen signifikant sind (beispielsweise werden eine untere Grenze von 0,342 und eine obere Grenze von 0,344 auf 34 % gerundet).

Die prognostizierte Nutzungsfunktion unterstützt die folgenden Metriken:

- [!UICONTROL Addressable audience]
- [!UICONTROL Durchschnittliche Profilreichweite]
- [!UICONTROL  Berechnungsstunden]
- [!UICONTROL Kunden-Journey-Zielgruppenanzahl Zeilen]
- [!UICONTROL Gesamtspeicher]

## Registerkarte [!UICONTROL Zusammenfassung] {#summary-tab}

Um weitere Metriken und detaillierte Einblicke in die Nutzung Ihrer Produktlizenz anzuzeigen, wählen Sie einen Produktnamen aus der Liste aus. Die Ansicht [!UICONTROL Zusammenfassung] für dieses Produkt wird angezeigt. Alle verfügbaren Metriken werden auf der Registerkarte [!UICONTROL Zusammenfassung] angezeigt. Die verfügbaren Metriken hängen vom lizenzierten Produkt ab. Diese Ansicht bietet **eine konsolidierte Ansicht aller Metriken in allen Produktions- oder Entwicklungs-Sandboxes**. Die gleiche Analyseebene wird sowohl für Produktions- als auch für Entwicklungs-Sandboxes bereitgestellt.

![Die Zusammenfassungsansicht eines Platform-Produkts, die alle für dieses Produkt verfügbaren Metriken anzeigt.](../images/license-usage/summary-tab.png)

Auf der Registerkarte &quot;Zusammenfassung&quot;enthält die Tabelle die Spalte [!UICONTROL Metrik] . Diese für Menschen lesbaren Beschreibungen zeigen alle Metriken an, die für diesen Sandbox-Typ verwendet werden.

### Sandbox auswählen {#select-sandbox}

Um die Ansicht zwischen Produktions- und Entwicklungs-Sandbox-Typen zu ändern, wählen Sie entweder [!UICONTROL Produktions-Sandboxes] oder [!UICONTROL Entwicklungs-Sandboxes] aus. Der ausgewählte Sandbox-Typ wird durch das Optionsfeld neben dem Sandbox-Namen angezeigt.

Die Verbrauchsberichte für Sandboxes sind kumulativ für alle Sandboxes desselben Typs. Mit anderen Worten: Durch die Auswahl von [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] werden Verbrauchsberichte für alle Produktions- bzw. Entwicklungs-Sandboxes bereitgestellt.

![Die Zusammenfassungsansicht eines Platform-Produkts mit Produktions-Sandboxes und Entwicklungs-Sandboxes hervorgehoben.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>Die Berechtigung zum Anzeigen des Dashboards zur Lizenznutzung muss auf Sandbox-Ebene angegeben werden. Fügen Sie den einzelnen Sandboxes Berechtigungen hinzu, um sie im Dashboard anzuzeigen. Diese Einschränkung wird in einer zukünftigen Version behoben. In der Zwischenzeit ist die folgende Problemumgehung verfügbar:
>
>1. Erstellen Sie ein Produktprofil in der Adobe Admin Console.
>2. Fügen Sie unter Berechtigungen in der Kategorie Sandbox alle Sandboxes hinzu, die Sie im Dashboard zur Lizenznutzung anzeigen möchten.
>3. Fügen Sie unter der Kategorie Berechtigungen für das Benutzer-Dashboard die Berechtigung &quot;Dashboard zur Nutzung der Lizenz anzeigen&quot;hinzu.

## Registerkarte [!UICONTROL Details] {#details-tab}

Um **eine bestimmte Nutzungsmetrik aus einer bestimmten Sandbox anzuzeigen, navigieren Sie zur Registerkarte [!UICONTROL Details] .** Auf der Registerkarte [!UICONTROL Details] werden alle verfügbaren Sandboxes entweder in den Produktions- oder Entwicklungs-Sandboxes angezeigt.

![Die Registerkarte Details des Dashboards zur Lizenzverwendung.](../images/license-usage/details-tab.png)

In dieser Ansicht können Sie das Symbol &quot;![Überprüfen&quot;auswählen.](/help/images/icons/inspect.png) neben einem Sandbox-Namen klicken, um die Visualisierung für diese Metrik anzuzeigen. Ein Dialogfeld mit einer Visualisierung für diese Metrik wird geöffnet.

### Visualisierungen {#visualizations}

Jedes Visualisierungs-Widget umfasst die folgenden Aspekte:

- Ein Liniendiagramm, das die Änderung der Metrik im Zeitverlauf verfolgt
- Ein Schlüssel für das Liniendiagramm
- Der Sandbox-Name
- Ein Dropdown-Menü zum Anpassen des Zeitraums für das Liniendiagramm

Die Liniendiagramme vergleichen die Nutzungszahlen für Ihr Unternehmen mit der Gesamtsumme, die für die Lizenzierung Ihres Unternehmens zur Verfügung steht, und geben einen Prozentsatz der Gesamtnutzung an.

![Die Visualisierung einer Metrik.](../images/license-usage/visualization.png)

Der Lookback-Zeitraum der Analyse kann über das Dropdown-Menü angepasst werden. Der Standardwert der letzten 30 Tage

Um einen Datumsbereich auszuwählen, können Sie über das Dropdown-Menü Datumsbereich den Zeitraum auswählen, der im Dashboard angezeigt werden soll. Es stehen mehrere Optionen zur Verfügung, darunter der Standardwert der letzten 30 Tage.

![Das Visualisierungsdialogfeld mit dem Dropdown-Menü für den Datumsbereich wurde hervorgehoben.](../images/license-usage/date-range.png)

Sie können auch **[!UICONTROL Benutzerdefiniertes Datum]** auswählen, um den angezeigten Zeitraum auszuwählen.

![Die Registerkarte Übersicht über die Lizenznutzung des Dashboards mit den benutzerdefinierten Datumsbereichsoptionen hervorgehoben.](../images/license-usage/custom-date-range.png)

## Verfügbare Metriken {#available-metrics}

Das Dashboard zur Lizenznutzung enthält Berichte zu verschiedenen eindeutigen Metriken, die für mehrere Produkte in der Organisation gelten. Die verfügbaren Metriken sind:

| Metrik | Beschreibung |
|---|---|
| [!UICONTROL Audience Activation Size] | Die Gesamtgröße der Profile, die in einem Jahr für ein dateibasiertes Ziel aktiviert wurden. Hinweis: Dies umfasst keine Profile, die über Streaming-Ziele gesendet werden. |
| [!UICONTROL Addressable Audience] | Die Summe der Berechtigungen Ihrer geschäftlichen Zielgruppe und der Berechtigung für die Verbraucher-Zielgruppe. Eine Audience vom Verbraucher wird definiert als die Anzahl der Personenprofile, die in der Bestellung als &quot;Zielgruppe des Verbrauchers&quot;identifiziert werden. Eine Business-Audience ist definiert als die Anzahl der Geschäftspersonenprofile, die in der Bestellung als &quot;Business Audience&quot;identifiziert werden. |
| [!UICONTROL  Adhoc Query Service Users Packs] | Ein Add-on zur Erhöhung der Berechtigung für gleichzeitige Query Service-Benutzer um fünf zusätzliche gleichzeitige Query Service-Benutzer und eine zusätzliche gleichzeitige Ausführung von Ad-hoc-Abfragen pro Pack. Es können mehrere zusätzliche Ad Hoc Query User Packs lizenziert sein. |
| [!UICONTROL Verfügbare CJA-Zeilen] | Die täglichen durchschnittlichen Datenzeilen, die in Customer Journey Analytics zur Analyse verfügbar sind. |
| [!UICONTROL Berechnete Attribute] | Die Gesamtanzahl der aggregierten Profilverhaltensdaten. Aggregierte Profilverhaltensdaten basieren auf Erlebnisereignissen, die in ein Profilattribut konvertiert werden und in ein Personenprofil oder ein Geschäftsprofil aufgenommen werden können. |
| [!UICONTROL Consumer Audience] | Die Anzahl der Personenprofile, die in der Bestellung als &quot;Zielgruppe für Verbraucher&quot;identifiziert wurden. |
| [!UICONTROL Datenexportgröße] | Die Menge der Daten, die durch Datensatzaktivierungen in einem Jahr gesendet werden. |
| [!UICONTROL Datenexporte] | Die Gesamtgröße der Datensätze, die in einem Jahr (direkt oder indirekt) in eine Nicht-Adobe-Lösung exportiert werden können. |
| [!UICONTROL  Data Lake Storage] | Die Menge, die für den Analysedatenspeicher in Adobe Experience Platform verwendet wird. |
| [!UICONTROL Interagierbare Zielgruppe] | Diese Metrik bezieht sich auf die Zielgruppe von interagierbaren Profilen. Ein ansprechbares Profil ist ein Eintrag mit Informationen, die einen Kontakt repräsentieren und im Profil-Service dargestellt werden. Diese Einträge sind Profile, mit denen Sie in den letzten 12 Monaten mithilfe der Authoring-, Entscheidungs-, Versand-, Experimentierungs- oder Orchestrierungsfunktionen von Journey Optimizer interagiert haben. |
| [!UICONTROL Look-alike-Zielgruppen] | Zählung der Zielgruppen, die durch Modellierung einer bestehenden Verbraucherzielgruppe generiert werden, um Personenprofile zu identifizieren, die der vorhandenen Verbraucherzielgruppe ähnlich sind. |
| [!UICONTROL Anzahl der AMM-Modelle] | Zählung des maschinellen Lernmodells (integrierter Adobe Mix Modeler), mit dem ein bestimmtes, auf Ihren Investitionen basierendes Ergebnis gemessen und/oder vorhergesagt werden kann. |
| [!UICONTROL Anzahl der Sandboxes] | Zählung der logischen Trennungen innerhalb Ihrer Instanz eines Adobe On-Demand-Dienstes, der auf Adobe Experience Platform-Isolationsdaten und -Vorgänge zugreift. |
| [!UICONTROL Profilreichhaltigkeitsnummer der Pakete] | Eine Steigerung des zulässigen Gesamtdatenvolumens um 25 KB pro Profil für jedes zusätzliche Profil-Rich-ness-Paket. |
| [!UICONTROL Berechnungsstunden des Query Service] | Eine Maßeinheit für die Zeit, die die Query Service-Engines zum Lesen, Verarbeiten und Zurückschreiben von Daten in den Data Lake benötigen, wenn eine Batch-Abfrage ausgeführt wird. |
| [!UICONTROL Streaming-Segmentierungsnummer der Pakete] | Die Pakete aktualisieren die Segmentzugehörigkeit für ein Personenprofil, wenn neue Daten über einen Streaming-Fluss in den Segmentierungsdienst gelangen. Die Segmentzugehörigkeit wird auf der Grundlage der aktuellen Personenprofilattribute und des Werts des aktuellen Ereignisses ausgewertet, ohne das historische Verhalten zu berücksichtigen. Streaming-Segmentierung ist eine gemeinsame Funktion. |
| [!UICONTROL Datenvolumen insgesamt] | Die Gesamtanzahl der Daten, die für Adobe Experience Platform Profile Service zur Verwendung in Interaktionsarbeitsabläufen verfügbar sind. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Sie können Ihre Lizenzberechtigungen in Ihrem Kundenauftrag überprüfen, um Metriken wie Ihre &quot;Speicherzulage&quot;zu berechnen.<br>Beispiel:<ul><li>Speicherzulage = Die Anzahl der &quot;autorisierten Profile&quot;in Ihrem Vertrag X Durchschnittliche Profilreichweite</li></ul>

Die Verfügbarkeit dieser Metriken und die spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab. Detaillierte Definitionen zu den einzelnen Metriken finden Sie in der entsprechenden Dokumentation zur Produktbeschreibung:

| Lizenz | Produktbeschreibung |
| --- | --- |
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

Weitere Informationen zu anderen in der Experience Platform-Benutzeroberfläche verfügbaren Funktionen finden Sie im [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).
