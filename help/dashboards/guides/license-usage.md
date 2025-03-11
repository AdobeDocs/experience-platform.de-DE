---
keywords: Experience Platform; Benutzeroberfläche; UI; Anpassung; Dashboard zur Lizenznutzung; Dashboard; Lizenznutzung; Berechtigung; Verbrauch
title: Lizenznutzungs-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenznutzung Ihres Unternehmens aufrufen können.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 1c31ef58eec727638cab28202afc762da0e226a2
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 25%

---

# Lizenznutzungs-Dashboard {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Testdialogfeld, das nicht sichtbar sein sollte"
>abstract="Das Objekt {name} wird am {date} angezeigt."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Hauptprodukttabelle"
>abstract="Die in der Tabelle aufgeführten Hauptprodukte verfügen über eigene Metriken, ein eigenes Nutzungs-Tracking und eigene Drillthrough-Ansichten auf Sandbox-Ebene. Diese Hauptprodukte stellen die Schlüsselmetriken für das Tracking bereit. Alle Add-ons sind in diesen Metriken enthalten."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Add-ons-Tabelle"
>abstract="In der Add-ons-Tabelle werden Produkte aufgeführt, deren Lizenzanzahl mit den von Hauptprodukten unterstützten Metriken kombiniert wird. Diese Add-ons verfügen nicht über separate Metriken, sondern verbessern das Nutzungs-Tracking der Hauptprodukte, mit denen sie verknüpft sind."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Lizenznutzungs-Dashboard"
>abstract="Das Lizenznutzungs-Dashboard bietet Einblicke in die von Ihnen erworbenen Adobe Experience Platform-Produkte. In der Dashboard-Übersicht werden die primären Metriken für Ihre Produkte angezeigt, einschließlich Ihrer Nutzung für jede der primären Metriken, sowie Ihr vertraglich vereinbarter Lizenzbetrag. Im Arbeitsbereich „Details“ wird eine Aufschlüsselung Ihrer Metriken für jedes Produkt innerhalb bestimmter Sandboxes angezeigt."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Lizenznutzungs-Dashboard"
>abstract="Das Lizenznutzungs-Dashboard bietet Einblicke in die von Ihnen erworbenen Adobe Experience Platform-Produkte. In der Dashboard-Übersicht werden die primären Metriken für Ihre Produkte angezeigt, einschließlich Ihrer Nutzung für jede der primären Metriken, sowie Ihr vertraglich vereinbarter Lizenzbetrag. Im Arbeitsbereich „Details“ wird eine Aufschlüsselung Ihrer Metriken für jedes Produkt innerhalb bestimmter Sandboxes angezeigt."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="Prognostizierte Compute-Stunden"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um Ihre Compute-Stunden einzuschätzen oder zu reduzieren, navigieren Sie zu „Abfragen“ > „Protokoll“, um den Abfrageverlauf zu überprüfen. Wenn Sie nicht über die Berechtigung zum Zugriff auf den Arbeitsbereich „Abfragen“ verfügen, wenden Sie sich an Ihre bzw. Ihren Admin."
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="Arbeitsbereich „Abfrageprotokoll“"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Prognostizierte ansprechbare Zielgruppe"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Prognostizierte ansprechbare Profile"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Prognostiziertes Geschäftspersonenprofil"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Prognostizierte Kernstunden"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Prognostiziertes Gesamtdatenvolumen"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Prognostizierte verfügbare CJA-Zeilen"
>abstract="Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

Sie können wichtige Informationen zur Lizenznutzung Ihres Unternehmens im Dashboard Adobe Experience Platform [!UICONTROL Lizenznutzung] anzeigen. Die hier angezeigten Informationen werden während eines täglichen Schnappschusses Ihrer Platform-Instanz erfasst.

Lizenznutzungsberichte bieten ein hohes Maß an Granularität gegenüber Ihren Lizenznutzungsmetriken. Das Dashboard enthält Nutzungsmetriken für jedes gekaufte Produkt (und die zugehörigen Add-ons), die konsolidierte Verwendung von Metriken in allen Produktions- oder Entwicklungs-Sandboxes und die Nutzungsmetrik aus einer bestimmten Sandbox. Die folgenden Experience Platform-Programme können mit Nutzungsmetriken verfolgt werden: Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

In diesem Handbuch wird beschrieben, wie Sie das Lizenznutzungs-Dashboard in der Benutzeroberfläche aufrufen und verwenden können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen allgemeinen Überblick über die Platform-Benutzeroberfläche erhalten Sie im Handbuch zur Benutzeroberfläche von [Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Lizenznutzung] Dashboard-Daten

Das Dashboard [!UICONTROL Lizenznutzung] zeigt eine Liste aller von Ihnen erworbenen Experience Platform-Produkte und aller Add-ons für diese Produkte an. In diesem Dashboard finden Sie einen Schnappschuss der lizenzbezogenen Daten Ihres Unternehmens für Experience Platform in jeder zugehörigen Sandbox.

Die Daten in diesem Dashboard werden genau so angezeigt, wie sie zum Zeitpunkt der Momentaufnahme angezeigt wurden. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Genauere Informationen zum Lizenznutzungs-Dashboard {#explore}

Um in der Platform-Benutzeroberfläche zum Dashboard zur Lizenznutzung zu navigieren, wählen **[!UICONTROL in der linken Leiste]** Lizenznutzung“ aus. Die [!UICONTROL Übersicht] wird geöffnet und zeigt eine Liste der verfügbaren Produkte an.

>[!NOTE]
>
>Das Lizenznutzungs-Dashboard ist standardmäßig nicht aktiviert. Benutzern muss die Berechtigung „Anzeigen des Lizenznutzungs-Dashboards“ gewährt werden, damit sie das Dashboard anzeigen können. Anweisungen zum Gewähren von Zugriffsberechtigungen für die Anzeige des Lizenznutzungs-Dashboards finden Sie im [Handbuch zu Dashboard-Berechtigungen](../permissions.md).

![Die Registerkarte „Übersicht“ des Lizenznutzungs-Dashboards mit hervorgehobener Lizenznutzung in der linken Navigationsleiste.](../images/license-usage/dashboard-overview.png)

## Registerkarte [!UICONTROL Übersicht] {#overview-tab}

Das Dashboard [!UICONTROL Lizenznutzung] zeigt zwei separate Tabellen an: **Kernprodukte** und **Add-ons**.

- **[!UICONTROL Kernprodukte] Tabelle**: In dieser Tabelle sind die wichtigsten von Ihrem Unternehmen lizenzierten Adobe Experience Platform-Produkte aufgeführt. Jedes Kernprodukt verfügt auf Sandbox-Ebene über eigene Metriken, Nutzungsverfolgung und Drill-Through-Ansichten. Diese Hauptprodukte stellen die Schlüsselmetriken für das Tracking bereit. Alle Add-ons sind in diesen Metriken enthalten.

- **[!UICONTROL Add-ons] Tabelle**: In dieser Tabelle werden zusätzliche Produkte aufgeführt, deren Lizenzbeträge mit den von den Kernprodukten unterstützten Metriken kombiniert sind. Add-ons verfügen nicht über separate Metriken, sondern verbessern die Nutzungsverfolgung der Kernprodukte, mit denen sie verknüpft sind.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Produkt]** | Die von Ihrem Unternehmen lizenzierte Adobe-Lösung. |
| **[!UICONTROL Primäre Metrik]** | Die primäre Metrik, die für das Tracking innerhalb dieses Produkts verwendet wird. |
| **[!UICONTROL Lizenzbetrag]** | Der vertraglich vereinbarte Wert für den Höchstbetrag der Primären Metrik, wie in Ihrer Produktlizenzvereinbarung vereinbart. |
| **[!UICONTROL Verwendung]** | Der Betrag Ihrer primären Metrik, der verwendet wird. Dieser Wert gibt die Gesamtverwendung dieser Metrik in allen Sandboxes an, entweder Produktion oder Entwicklung. |
| **[!UICONTROL Nutzung %]** | Der Prozentsatz Ihrer primären Metrik, der entsprechend Ihrem Lizenzbetrag verwendet wird. |
| **[!UICONTROL Prognoseverwendung]** | Der prognostizierte Nutzungsprozentsatz Ihrer primären Metrik entsprechend Ihrem Lizenzbetrag. |

>[!NOTE]
>
>Lizenzbeträge für Add-ons sind im [!UICONTROL Lizenzbetrag] der Kernprodukte enthalten. Wenn Sie beispielsweise ein Paket mit fünf Sandboxes als Add-on kaufen, wird der Betrag zu dem des Basisprodukts hinzugefügt. Die Tabelle „Add-ons[!UICONTROL  zeigt einen für das Add]on spezifischen „Lizenzbetrag“ an, aber die tatsächliche Nutzung wird über das Basisprodukt verfolgt.

Die Tabellen zeigen die primäre Metrik für jedes Produkt an, da jedes Produkt zahlreiche Metriken verfolgen kann.

### Prognostizierte Nutzung {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden jeweils am 15. jedes Monats erstellt. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden jeweils am 15. jedes Monats erstellt. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder Pseudonymprofile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

Proaktive Verwaltung und Optimierung Ihrer Lizenzressourcen auf der Grundlage aufschlussreicher Nutzungsprognosen. Die Spalte [!UICONTROL Prognostizierte Nutzung] sagt die zukünftige Lizenznutzung auf Sandbox-Ebene, über alle Produktions- und Entwicklungs-Sandboxes hinweg, für alle Ihre gekauften Produkte genau voraus. Diese Warnfunktion bietet eine Prognose der Lizenznutzung für einen Zeitraum von sechs Wochen in der Zukunft, basierend auf Ihrer Nutzung bis zum 15. dieses Kalendermonats. Prognosen werden mit einer unteren und einer oberen Grenze bereitgestellt.

>[!IMPORTANT]
>
>Die Prognosen werden monatlich aktualisiert. Das Datum der Aktualisierung ist in einem Infosymbol enthalten (![Dieses Infosymbol.](../images/license-usage/info-icon.png)) über dem Spaltentitel.

Um eine Zusammenfassung der Nutzung von Berechtigungen für ein Produkt anzuzeigen, wählen Sie ein Produkt aus der Tabelle [!UICONTROL Kernprodukte] aus.

![Die [!UICONTROL Lizenznutzung] [!UICONTROL Übersicht] mit einem Produkt und der hervorgehobenen Spalte „Prognostizierte Nutzung“.](../images/license-usage/product-predicted-usage.png)

Die Registerkarte Zusammenfassung wird angezeigt. Sie können die granularen Prognosen auf den Registerkarten [!UICONTROL Zusammenfassung] und [!UICONTROL Details] verwenden, um eine fundierte Entscheidungsfindung für eine effiziente Lizenznutzung sicherzustellen.

>[!NOTE]
>
>Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung Ihres Unternehmens zu verstehen und sicherzustellen, dass die Nutzung nicht über den Rahmen der Lizenzvereinbarung Ihres Unternehmens mit Adobe hinausgeht.

![Die Zusammenfassungsansicht eines Platform-Produkts mit hervorgehobener Spalte für die prognostizierte Nutzung.](../images/license-usage/summary-predicted-usage.png)

Der Prozentsatz der prognostizierten Nutzung wird wie folgt bestimmt:

- Wenn sich die unteren und oberen Grenzen deutlich unterscheiden, werden sie als Bereich angezeigt (z. B. 32 % bis 35 %).
- Wenn die unteren und oberen Grenzen nahezu identisch und nicht gleich null sind, werden sie als annähernder Wert angezeigt (z. B. ~34 %).
- Wenn die unteren und oberen Grenzen nahezu identisch und gleich null sind, werden sie als genau 0 % angezeigt.

>[!NOTE]
>
>„Nahezu identisch“ bedeutet in diesem Zusammenhang, dass die Werte auf zwei Dezimalstellen statistisch signifikant sind (z. B. werden eine Untergrenze von 0,342 und eine Obergrenze von 0,344 jeweils auf 34 % gerundet).

Die Funktion „Prognostizierte Nutzung“ unterstützt die folgenden Metriken:

- [!UICONTROL Adressierbare Zielgruppe]
- [!UICONTROL Stunden berechnen]
- [!UICONTROL Kunden-Journey-Zielgruppe - Anzahl der Zeilen]
- [!UICONTROL Gesamtdatenvolumen]

## Registerkarte [!UICONTROL Zusammenfassung] {#summary-tab}

Um weitere Metriken und detaillierte Einblicke in die Nutzung Ihrer Produktlizenz anzuzeigen, wählen Sie einen Produktnamen aus der Liste aus. Die [!UICONTROL Zusammenfassung] für dieses Produkt wird angezeigt. Alle verfügbaren Metriken werden auf der Registerkarte &quot;[!UICONTROL &quot; ]. Die verfügbaren Metriken hängen vom lizenzierten Produkt ab. Diese Ansicht bietet **eine konsolidierte Ansicht aller Metriken über alle Produktions- oder Entwicklungs-Sandboxes hinweg**. Der gleiche Analysegrad wird sowohl für Produktions- als auch für Entwicklungs-Sandboxes bereitgestellt.

![Die Zusammenfassungsansicht eines Platform-Produkts, in der alle verfügbaren Metriken für dieses Produkt angezeigt werden.](../images/license-usage/summary-tab.png)

Auf der Registerkarte Zusammenfassung enthält die Tabelle die Spalte [!UICONTROL Metrik]. Diese für Menschen lesbaren Beschreibungen geben alle Metriken an, die für diesen Sandbox-Typ verwendet werden.

### Sandbox auswählen {#select-sandbox}

Um die Ansicht zwischen Produktions- und Entwicklungs-Sandbox-Typen zu ändern, wählen Sie entweder [!UICONTROL Produktions-Sandboxes] oder [!UICONTROL Entwicklungs-Sandboxes]. Der ausgewählte Sandbox-Typ wird durch die Optionsschaltfläche neben dem Sandbox-Namen angezeigt.

Das Reporting zur Nutzung für Sandboxes ist für alle Sandboxes desselben Typs kumulativ. Mit anderen Worten: Die Auswahl [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] liefert Verbrauchsberichte für alle Produktions- bzw. Entwicklungs-Sandboxes.

![Die Zusammenfassungsansicht eines Platform-Produkts mit hervorgehobenen Produktions-Sandboxes und Entwicklungs-Sandboxes.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>Die Berechtigung zum Anzeigen des Lizenznutzungs-Dashboards muss auf Sandbox-Ebene angegeben werden. Fügen Sie jeder einzelnen Sandbox Berechtigungen hinzu, um sie im Dashboard anzuzeigen. Diese Einschränkung wird in einer zukünftigen Version behoben. In der Zwischenzeit steht die folgende Problemumgehung zur Verfügung:
>
>1. Erstellen Sie ein Produktprofil in der Adobe Admin Console.
>2. Fügen Sie unter „Berechtigung“ in der Kategorie „Sandbox“ alle Sandboxes hinzu, die Sie im Lizenznutzungs-Dashboard anzeigen möchten.
>3. Fügen Sie unter der Kategorie „Berechtigung für das Benutzer-Dashboard“ die Berechtigung „Dashboard zur Lizenznutzung anzeigen“ hinzu.

## [!UICONTROL Details] Registerkarte {#details-tab}

Um **eine bestimmte Nutzungsmetrik aus einer bestimmten Sandbox anzuzeigen** navigieren Sie zur Registerkarte [!UICONTROL Details] . Auf [!UICONTROL  Registerkarte ]Details“ werden alle verfügbaren Sandboxes innerhalb der Produktions- oder Entwicklungs-Sandboxes angezeigt.

![Die Registerkarte „Details“ im Dashboard zur Lizenznutzung.](../images/license-usage/details-tab.png)

In dieser Ansicht können Sie auf das Symbol ![Überprüfen“ klicken.](/help/images/icons/inspect.png) neben einem Sandbox-Namen, um die Visualisierung für diese Metrik anzuzeigen. Ein Dialogfeld mit einer Visualisierung für diese Metrik wird geöffnet.

### Visualisierungen {#visualizations}

Jedes Visualisierungs-Widget umfasst die folgenden Aspekte:

- Ein Liniendiagramm, das die Änderung der Metrik im Zeitverlauf verfolgt
- Ein Schlüssel für das Liniendiagramm
- Der Sandbox-Name
- Ein Dropdown-Menü zum Anpassen des Zeitraums für das Liniendiagramm

Die Liniendiagramme vergleichen die Nutzungszahlen für Ihr Unternehmen mit der Gesamtzahl der verfügbaren Lizenzen Ihres Unternehmens und geben einen Prozentsatz der Gesamtnutzung an.

![Die Visualisierung einer Metrik.](../images/license-usage/visualization.png)

Der Lookback-Zeitraum der Analyse kann über das Dropdown-Menü angepasst werden. Der Standardwert der letzten 30 Tage

Um einen Datumsbereich auszuwählen, können Sie das Dropdown-Menü für den Datumsbereich verwenden, um den Zeitraum auszuwählen, der im Dashboard angezeigt werden soll. Es stehen mehrere Optionen zur Verfügung, darunter der Standardwert der letzten 30 Tage.

![Das Visualisierungsdialogfeld mit hervorgehobener Dropdown-Liste „Datumsbereich“.](../images/license-usage/date-range.png)

Sie können auch **[!UICONTROL Benutzerdefiniertes Datum]** auswählen, um den angezeigten Zeitraum auszuwählen.

![Die Registerkarte „Übersicht“ des Lizenznutzungs-Dashboards mit hervorgehobenen benutzerdefinierten Datumsbereichsoptionen.](../images/license-usage/custom-date-range.png)

## Verfügbare Metriken {#available-metrics}

>[!IMPORTANT]
>
>Ab dem 20. August sahen Kundinnen und Kunden mit Berechtigungen für [!UICONTROL Durchschnittliche Profilreichhaltigkeit] und [!UICONTROL Gesamtspeicher] stattdessen &quot;[!UICONTROL Gesamtdatenvolumen]&quot; im Lizenznutzungs-Dashboard. Es gab keine Änderung bei den Kundenberechtigungen, sondern nur eine Vereinfachung der Tracking-Metriken. [!UICONTROL Gesamtdatenvolumen] stellt die Daten dar, die im Adobe Experience Platform-Profildienst für Interaktions- und Personalisierungs-Workflows verfügbar sind. Diese vereinfachte Metrik verbesserte die Verwaltung und Messung der Nutzung des Profil-Service. Kunden wurden aufgefordert, sich an ihren Adobe-Support-Mitarbeiter zu wenden, um weitere Informationen zu dieser Änderung zu erhalten.

Das Lizenznutzungs-Dashboard enthält Berichte zu verschiedenen eindeutigen Metriken, die für mehrere Produkte in der Organisation gelten. Die verfügbaren Metriken sind:

| Metrik | Beschreibung |
|---|---|
| [!UICONTROL Audience Activation-Größe] | Die Gesamtgröße der Profile, die in einem Jahr für ein beliebiges dateibasiertes Ziel aktiviert wurden. Hinweis: Dies umfasst keine Profile, die über Streaming-Ziele gesendet werden. |
| [!UICONTROL Addressable Audience] | Die Summe aus Ihrer Berechtigung für Geschäftszielgruppen und der Berechtigung für Privatkunden-Zielgruppen. Eine Verbraucherzielgruppe wird als die Anzahl der Personenprofile definiert, die im Kundenauftrag als „Verbraucherzielgruppe“ gekennzeichnet sind. Eine Business-Audience wird als die Anzahl der Geschäftspersonenprofile definiert, die im Auftrag als „Business-Audience“ identifiziert werden. |
| [!UICONTROL Ad-hoc-Query Service-Benutzerpakete] | Ein Add-on zur Erhöhung Ihrer Berechtigung für autorisierte gleichzeitige Abfrage-Service-Benutzer um fünf zusätzliche gleichzeitige Abfrage-Service-Benutzer und eine zusätzliche gleichzeitig ausgeführte Ad-hoc-Abfrage pro Paket. Es können mehrere zusätzliche Ad Hoc Query-Benutzerpakete lizenziert werden. |
| [!UICONTROL Durchschnittliche Profilreichhaltigkeit] | **Veraltet** - Die Summe aller Produktionsdaten, die zu einem beliebigen Zeitpunkt im Hub-Profil-Service gespeichert sind, dividiert durch die fünffache Anzahl der Profile autorisierter Geschäftspersonen. [!UICONTROL Durchschnittliche Profilreichhaltigkeit] ist eine gemeinsam genutzte Funktion. |
| [!UICONTROL CJA-Zeilen verfügbar] | Die täglichen durchschnittlichen Datenzeilen, die in Customer Journey Analytics für die Analyse verfügbar sind. |
| [!UICONTROL Berechnete Attribute] | Die Gesamtzahl der aggregierten Profilverhaltensdaten. Aggregierte Profilverhaltensdaten basieren auf Erlebnisereignissen, die in ein Profilattribut umgewandelt werden und in ein Personenprofil oder ein Geschäftspersonenprofil aufgenommen werden können. |
| [!UICONTROL Privatkunden-Zielgruppe] | Die Anzahl der Personenprofile, die im Kundenauftrag als „Consumer Audience“ identifiziert wurden. |
| [!UICONTROL Größe des Datenexports] | Die Datenmenge, die durch Datensatzaktivierungen in einem Jahr gesendet wird. |
| [!UICONTROL Datenexporte] | Die Gesamtgröße der Datensätze, die in einem Jahr (direkt oder indirekt) in eine Nicht-Adobe-Lösung exportiert werden können. |
| [!UICONTROL Data Lake Storage] | Die verwendete Menge des Analytics-Datenspeichers in Adobe Experience Platform. |
| [!UICONTROL Ansprechbare Zielgruppe] | Diese Metrik bezieht sich auf die Zielgruppe von kontaktierbaren Profilen. Ein ansprechbares Profil ist ein Eintrag mit Informationen, die einen Kontakt repräsentieren und im Profil-Service dargestellt werden. Diese Einträge sind Profile, mit denen Sie in den letzten 12 Monaten mithilfe der Authoring-, Entscheidungs-, Versand-, Experimentierungs- oder Orchestrierungsfunktionen von Journey Optimizer interagiert haben. |
| [!UICONTROL Lookalike-Zielgruppen] | Die Anzahl der Zielgruppen, die durch Modellierung einer bestehenden Privatkunden-Zielgruppe generiert werden, um Personenprofile zu identifizieren, die der bestehenden Privatkunden-Zielgruppe ähnlich sind. |
| [!UICONTROL Anzahl der AMM-Modelle] | Eine Zählung des in Adobe Mix Modeler integrierten maschinellen Lernmodells, mit dem ein bestimmtes Ergebnis basierend auf Ihren Investitionen gemessen und/oder vorhergesagt wird. |
| [!UICONTROL Anzahl der Sandboxes] | Die Anzahl der logischen Trennungen innerhalb Ihrer Instanz jedes Adobe On-Demand-Service, der auf Adobe Experience Platform zugreift und Daten und Vorgänge isoliert. |
| [!UICONTROL Reichhaltigkeit des Profils - Anzahl der Packungen] | Eine Erhöhung des autorisierten Gesamtdatenvolumens um 25 KB pro Profil für jedes zusätzliche Reichweitenpaket für Profile. |
| [!UICONTROL Query Service Compute Hours] | Ein Maß für die Zeit, die die Abfrage-Service-Engines zum Lesen, Verarbeiten und Zurückschreiben von Daten in den Data Lake benötigen, wenn eine Batch-Abfrage ausgeführt wird. |
| [!UICONTROL Streaming-Segmentierung: Anzahl der Packs] | Die Packs aktualisieren die Segmentzugehörigkeit für ein Personenprofil, wenn neue Daten über einen Streaming-Fluss in den Segmentierungs-Service eintreten. Die Segmentzugehörigkeit wird anhand der Profilattribute der aktuellen Person und des Werts des aktuellen Ereignisses bewertet, ohne das historische Verhalten zu berücksichtigen. Die Streaming-Segmentierung ist eine gemeinsam genutzte Funktion. |
| [!UICONTROL Gesamtdatenvolumen] | Die Gesamtmenge der für den Adobe Experience Platform-Profil-Service verfügbaren Daten, die in Interaktions-Workflows verwendet werden können. Weitere Informationen finden [ unter „Häufig gestellte Fragen zum ](../../landing/license-usage-and-guardrails/total-data-volume.md) Datenvolumen insgesamt“. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Sie können Ihre Lizenzberechtigungen in Ihrem Kundenauftrag überprüfen, um Metriken wie z. B. Ihre „Speicherzulage“ zu berechnen.<br>Zum Beispiel<ul><li>Speicherzuschlag = Anzahl der „autorisierten Profile“ in Ihrem Vertrag X Durchschnittliche Profilreichhaltigkeit</li></ul>

Die Verfügbarkeit und spezifische Definition dieser Metriken hängen von der von Ihrem Unternehmen erworbenen Lizenz ab. Detaillierte Definitionen der einzelnen Metriken finden Sie in der entsprechenden Produktbeschreibungsdokumentation:

| Lizenz | Produktbeschreibung |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD-STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services und Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM:OD</li><li>RT KUNDENDATENPLATTFORM:OD PRFL BIS 10M</li><li>RT KUNDENDATENPLATTFORM:OD PRFL BIS 50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVIERUNG</li><li>AEP:OD ACTIVATION PRFL BIS 10M</li><li>AEP:OD ACTIVATION PRFL BIS ZU 50M</li></ul> | [Adobe Experience Platform-Aktivierung](https://helpx.adobe.com/de/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD-PROFILORCHESTRIERUNG</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/de/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Das Lizenznutzungs-Dashboard enthält nur Berichte zur neuesten Lizenz, die für Ihr Unternehmen bereitgestellt wurde. Wenn die neueste für Ihr Unternehmen bereitgestellte Lizenz nicht in der obigen Tabelle angezeigt wird, wird das Lizenznutzungs-Dashboard möglicherweise nicht ordnungsgemäß angezeigt. Die Unterstützung für zusätzliche Lizenzen und mehrere Lizenzen in einer einzigen Organisation ist für eine zukünftige Version geplant.

## Nächste Schritte

Nach dem Lesen dieses Dokuments können Sie das Lizenznutzungs-Dashboard finden und Nutzungsmetriken für jedes gekaufte Produkt, für alle Produktions- oder Entwicklungs-Sandboxes und für eine bestimmte Sandbox anzeigen. Weitere Informationen zu verfügbaren Metriken für Ihr Unternehmen, die auf der von Ihrem Unternehmen erworbenen Lizenz basieren, finden Sie.

Weitere Informationen zu anderen in der Experience Platform-Benutzeroberfläche verfügbaren Funktionen finden Sie im [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).
