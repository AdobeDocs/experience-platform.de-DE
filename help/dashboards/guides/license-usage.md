---
keywords: Experience Platform; Benutzeroberfläche; UI; Anpassung; Dashboard zur Lizenznutzung; Dashboard; Lizenznutzung; Berechtigung; Verbrauch
title: Lizenznutzungs-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenznutzung Ihres Unternehmens aufrufen können.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 39%

---

# Lizenznutzungs-Dashboard {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Testdialogfeld, das nicht sichtbar sein sollte"
>abstract="Das Objekt {name} wird auf {date} angezeigt."

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
>abstract="Compute-Stunden messen die Zeit, die die Abfrage-Service-Engines beim Lesen, Verarbeiten und Schreiben von Daten benötigen, wenn sie Batch-Abfragen ausführen.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um Ihre Nutzung einzuschätzen oder zu reduzieren, navigieren Sie zu „Abfragen“ > „Protokoll“, um den Abfrageverlauf zu überprüfen. Wenn Sie über keinen Zugriff auf den Arbeitsbereich „Abfragen“ verfügen, wenden Sie sich an Ihre bzw. Ihren Admin."
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="Arbeitsbereich „Abfrageprotokoll“"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Prognostizierte ansprechbare Zielgruppe"
>abstract="Die ansprechbare Zielgruppe ist der Satz von Personenprofilen im Echtzeit-Kundenprofil, mit dem Ihr Unternehmen interagieren darf. Diese Metrik umfasst sowohl direkt identifizierbare als auch pseudonyme Profile.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Prognostizierte ansprechbare Profile"
>abstract="Ansprechbare Profile sind Personenprofile im Echtzeit-Kundenprofil, mit denen Ihr Unternehmen in den letzten 12 Monaten versucht hat, über Journey Optimizer zu interagieren.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Prognostiziertes Geschäftspersonenprofil"
>abstract="Geschäftspersonenprofile sind Datensätze im Echtzeit-Kundenprofil, die Einzelpersonen in einem B2B-Kontext darstellen.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Prognostizierte Kernstunden"
>abstract="Kernstunden stellen die Verarbeitungszeit dar, die in allen Experience Platform-Services verbraucht wird.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Prognostiziertes Gesamtdatenvolumen"
>abstract="Das Gesamtdatenvolumen ist die Menge an Daten, die im Echtzeit-Kundenprofil für die Verwendung in Interaktions- und Personalisierungs-Workflows verfügbar ist.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Prognostizierte verfügbare CJA-Zeilen"
>abstract="Verfügbare CJA-Zeilen bezieht sich auf die täglichen durchschnittlichen Datenzeilen, die in Customer Journey Analytics für die Analyse verfügbar sind.<br>Ihre Nutzung könnte die lizenzierte Menge erreichen. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_addressableaudience"
>title="Prognostizierte ansprechbare Zielgruppe"
>abstract="Die ansprechbare Zielgruppe ist der Satz von Personenprofilen im Echtzeit-Kundenprofil, mit dem Ihr Unternehmen interagieren darf. Dazu gehören sowohl direkt identifizierbare als auch pseudonyme Profile.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_engageableprofiles"
>title="Prognostizierte ansprechbare Profile"
>abstract="Ansprechbare Profile sind Personenprofile im Echtzeit-Kundenprofil, mit denen Ihr Unternehmen in den letzten 12 Monaten versucht hat, über Journey Optimizer zu interagieren.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_businesspersonprofile"
>title="Prognostiziertes Geschäftspersonenprofil"
>abstract="Geschäftspersonenprofile sind Datensätze im Echtzeit-Kundenprofil, die Einzelpersonen in einem B2B-Kontext darstellen.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_corehours"
>title="Prognostizierte Kernstunden"
>abstract="Kernstunden stellen die Verarbeitungszeit dar, die in allen Experience Platform-Services verbraucht wird.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_totaldatavolume"
>title="Prognostiziertes Gesamtdatenvolumen"
>abstract="Das Gesamtdatenvolumen ist die Menge an Daten, die im Echtzeit-Kundenprofil für die Verwendung in Interaktions- und Personalisierungs-Workflows verfügbar ist.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_cjaRowsAvailable"
>title="Prognostizierte verfügbare CJA-Zeilen"
>abstract="Verfügbare CJA-Zeilen bezieht sich auf die täglichen durchschnittlichen Datenzeilen, die in Customer Journey Analytics für die Analyse verfügbar sind.<br>Ihre Nutzung hat die lizenzierte Menge überschritten. Um die Nutzung zu reduzieren, konfigurieren Sie den Ablauf von Datensätzen oder Daten pseudonymer Profile."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=de" text="Gültigkeitsdauern von Erlebnisereignissen"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

Sie können wichtige Informationen zur Lizenznutzung Ihres Unternehmens im Dashboard Adobe Experience Platform [!UICONTROL Lizenznutzung] anzeigen. Die hier angezeigten Informationen werden während eines täglichen Schnappschusses Ihrer Experience Platform-Instanz erfasst.

Lizenznutzungsberichte bieten ein hohes Maß an Granularität. Die meisten Metriken werden über mehrere Produkte hinweg gemeinsam genutzt und spiegeln die aggregierte Nutzung über alle Produkte hinweg wider, die sie verwenden, nicht über die Gesamtwerte pro Produkt. Das Dashboard bietet eine konsolidierte Verwendung dieser Metriken in allen Produktions- oder Entwicklungs-Sandboxes sowie die Nutzungsmetrik aus einer bestimmten Sandbox. Die folgenden Experience Platform-Programme können mit Nutzungsmetriken verfolgt werden: Real-Time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

In diesem Handbuch wird beschrieben, wie Sie das Lizenznutzungs-Dashboard in der Benutzeroberfläche aufrufen und verwenden können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen allgemeinen Überblick über die Experience Platform-Benutzeroberfläche erhalten Sie im Handbuch zur Experience Platform-Benutzeroberfläche [](../../landing/ui-guide.md).

## [!UICONTROL Lizenznutzung] Dashboard-Daten

Das Dashboard [!UICONTROL Lizenznutzung] zeigt eine Liste aller von Ihnen erworbenen Experience Platform-Produkte und aller Add-ons für diese Produkte an. In diesem Dashboard finden Sie einen Schnappschuss der lizenzbezogenen Daten Ihres Unternehmens für Experience Platform in jeder zugehörigen Sandbox.

Die Daten in diesem Dashboard werden genau so angezeigt, wie sie zum Zeitpunkt der Momentaufnahme aufgetreten sind. Es handelt sich nicht um eine Annäherung oder Stichprobe, aber das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Die meisten Metriken im Dashboard werden täglich aktualisiert, basierend auf einer Momentaufnahme Ihrer Experience Platform-Instanz. [!UICONTROL Verfügbare CJA-]: bildet eine Ausnahme und wird monatlich aktualisiert. Mit „Packs“ gekennzeichnete Metriken wie [!UICONTROL Adhoc Query Service Users Packs], [!UICONTROL Profile Richness No of Packs] und [!UICONTROL Streaming Segmentation No of Packs] spiegeln Lizenzberechtigungen für Add-on-Angebote wider und verfolgen die laufende Nutzung nicht. Änderungen, die nach der Momentaufnahme vorgenommen werden, sind erst sichtbar, wenn die nächste Momentaufnahme erstellt wird.

## Genauere Informationen zum Lizenznutzungs-Dashboard {#explore}

Um in der Experience Platform-Benutzeroberfläche zum Lizenznutzungs-Dashboard zu navigieren, wählen **[!UICONTROL in der linken]** „Lizenznutzung“ aus. Das Dashboard enthält zwei Registerkarten: **[!UICONTROL Metriken]** und **[!UICONTROL Produkte]**.

>[!NOTE]
>
>Das Lizenznutzungs-Dashboard ist standardmäßig nicht aktiviert. Benutzern muss die Berechtigung „Anzeigen des Lizenznutzungs-Dashboards“ gewährt werden, um das Dashboard anzeigen zu können. Anweisungen zum Gewähren von Zugriffsberechtigungen finden Sie im [Handbuch zu Dashboard-Berechtigungen](../permissions.md).

## Registerkarte [!UICONTROL Metriken] {#metrics-tab}

Die **[!UICONTROL Metriken]** bietet eine zentrale Ansicht aller Lizenznutzungsmetriken in Ihrem Unternehmen. Da die meisten Metriken produktübergreifend verwendet werden, gibt es keine separate Aufschlüsselung pro Produkt für diese Metriken.

Die Tabelle Metriken enthält die folgenden Spalten:

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Metrikname]** | Der Name der Lizenznutzungsmetrik. Jeder Eintrag enthält ein Informationssymbol (`ⓘ`), das eine Beschreibung und eine Liste der zugehörigen Produkte anzeigt. |
| **[!UICONTROL Lizenziert]** | Die Anzahl der Einheiten, zu deren Nutzung Ihr Unternehmen berechtigt ist, wie in Ihrem Vertrag definiert. Diese Metrik ist derselbe Wert wie der **Lizenzbetrag** auf der Registerkarte Produkte . |
| **[!UICONTROL Gemessen]** | Die Menge der Metrik, die derzeit von Ihrer Organisation verwendet wird. |
| **[!UICONTROL Nutzung %]** | Der Prozentsatz Ihres lizenzierten Werts, der derzeit verwendet wird. |
| **[!UICONTROL Prognostizierte Nutzung %]** | Der prognostizierte Bereich der Metriknutzung über die nächsten 6 Wochen. |

Verwenden Sie den Umschalter **[!UICONTROL Produktion]** oder **[!UICONTROL Entwicklung]** Sandbox , um die von Sandboxes angezeigten Metriken zu filtern.

>[!NOTE]
>
>Berichte zum Verbrauch sind kumulativ nach Sandbox-Typ. Wenn Sie [!UICONTROL Produktion] oder [!UICONTROL Entwicklung] auswählen, wird die kombinierte Nutzung in allen Sandboxes dieses Typs angezeigt.

![Die Registerkarte Metriken im Lizenznutzungs-Dashboard mit einer Liste von Metriken, Lizenzbeträgen und Nutzungsdaten.](../images/license-usage/metrics-tab.png)

>[!WARNING]
>
>Die Berechtigung zum Anzeigen des Lizenznutzungs-Dashboards muss auf Sandbox-Ebene angegeben werden. Fügen Sie jeder einzelnen Sandbox Berechtigungen hinzu, um sie im Dashboard anzuzeigen. Diese Einschränkung wird in einer zukünftigen Version behoben. In der Zwischenzeit steht die folgende Problemumgehung zur Verfügung:
>
>1. Erstellen Sie ein Produktprofil in der Adobe Admin Console.
>2. Fügen Sie unter „Berechtigung“ in der Kategorie „Sandbox“ alle Sandboxes hinzu, die Sie im Lizenznutzungs-Dashboard anzeigen möchten.
>3. Fügen Sie unter der Kategorie „Berechtigung für das Benutzer-Dashboard“ die Berechtigung „Dashboard zur Lizenznutzung anzeigen“ hinzu.

### Anzeigen von Metrikdetails {#view-metric-details}

Um Nutzungsdetails für eine bestimmte Metrik anzuzeigen, wählen Sie einen Metriknamen in der Liste aus. Eine detaillierte Ansicht der Metrik wird angezeigt, einschließlich:

- Ein historisches Liniendiagramm, das die Nutzung im Zeitverlauf anzeigt
- Ein Vergleich von lizenzierten und gemessenen Werten
- Verwendung nach individueller Sandbox
- Ein Sandbox-Selektor zum Filtern von Daten
- Eine Exportoption für den CSV-Download

Mit dieser Visualisierung können Sie Trends verfolgen, verstehen, wie jede Sandbox zur Gesamtnutzung beiträgt, und die Daten für die Offline-Analyse exportieren.

Jedes Diagramm enthält Dropdown-Menüs zum Filtern der Daten. Verwenden Sie das Dropdown-Menü für den Datumsbereich, um den Lookback-Zeitraum anzupassen (Standard: letzte 30 Tage), oder verwenden Sie das Dropdown-Menü der Sandbox, um die Nutzung für eine bestimmte Produktions- oder Entwicklungs-Sandbox anzuzeigen.

![Die Detailansicht der adressierbaren Zielgruppenmetrik mit historischem Nutzungsdiagramm, Sandbox-Tabelle und Exportschaltfläche.](../images/license-usage/metric-details-view.png)

Sie können auch ein **[!UICONTROL Benutzerdefiniertes Datum]** auswählen, um den angezeigten Zeitraum auszuwählen.

![Die Registerkarte „Übersicht“ des Lizenznutzungs-Dashboards mit hervorgehobenen benutzerdefinierten Datumsbereichsoptionen.](../images/license-usage/custom-date-range.png)

### CSV-Export {#export-metric-usage-data}

Sie können historische Nutzungsdaten für die ausgewählte Metrik und Sandbox direkt aus der Detailansicht der Metrik als CSV-Datei exportieren. Wählen Sie das **[!UICONTROL Exportieren]**, um die Diagrammdaten im Tabellenformat herunterzuladen. Die exportierte CSV-Datei erleichtert die Offline-Analyse von Trends oder die Freigabe von Nutzungseinblicken über Teams hinweg.

## Registerkarte [!UICONTROL Produkte] {#products-tab}

Auf **[!UICONTROL Registerkarte]** Produkte“ werden Lizenznutzungsdaten nach gekauften Produkten und zugehörigen Add-ons gruppiert angezeigt. Die [!UICONTROL Produkte] enthält zwei Tabellen:

- **[!UICONTROL Kernprodukte] Tabelle**: In dieser Tabelle sind die wichtigsten von Ihrem Unternehmen lizenzierten Adobe Experience Platform-Produkte aufgeführt. Jedes Produkt listet seine primäre Metrik, Nutzungsverfolgung und prognostizierte Nutzung auf.
- **[!UICONTROL Add-ons] Tabelle**: Listet zusätzliche Elemente auf, deren Lizenzbeträge zu Kernproduktmetriken beitragen. Add-ons verfügen nicht über separate Metriken, sondern verbessern die Nutzungsverfolgung der Kernprodukte, mit denen sie verknüpft sind.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Produkt]** | Die von Ihrem Unternehmen lizenzierte Adobe-Lösung. |
| **[!UICONTROL Primäre Metrik]** | Die primäre Metrik, die für das Tracking innerhalb dieses Produkts verwendet wird. |
| **[!UICONTROL Lizenzbetrag]** | Der kontrahierte Wert für den Höchstbetrag der primären Metrik. |
| **[!UICONTROL Verwendung]** | Der Betrag Ihrer primären Metrik, der verwendet wird. |
| **[!UICONTROL Nutzung %]** | Der Prozentsatz Ihrer primären Metrik, der entsprechend Ihrem Lizenzbetrag verwendet wird. |
| **[!UICONTROL Prognostizierte Nutzung]** | Der prognostizierte Nutzungsprozentsatz Ihrer primären Metrik. |

>[!NOTE]
>
>Der [!UICONTROL Lizenzbetrag] für Add-ons ist im Gesamtlizenzbetrag des Kernprodukts enthalten. Add-ons werden nicht separat verfolgt, sondern erweitern die Funktionen der zugehörigen Produkte. Wenn Sie beispielsweise ein Paket mit fünf Sandboxes als Add-on kaufen, wird der Betrag zu dem des Basisprodukts hinzugefügt. Die Tabelle „Add-ons[!UICONTROL  zeigt einen für das Add]on spezifischen „Lizenzbetrag“ an, aber die tatsächliche Nutzung wird über das Basisprodukt verfolgt.

![Die Registerkarte „Produkte“ im Lizenznutzungs-Dashboard mit Tabellen zu Kernprodukten und Add-ons.](../images/license-usage/products-tab.png)

### Prognostizierte Nutzung {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden wöchentlich jeden Freitag generiert. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder pseudonyme Profile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Prognostizierte Nutzung"
>abstract="Die Prognosen basieren auf der Nutzung der letzten sechs bis sieben Monate und werden jeweils am 15. jedes Monats erstellt. Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung durch Ihr Unternehmen zu verstehen und sicherzustellen, dass die Nutzung nicht über den Umfang der Lizenz Ihres Unternehmens mit Adobe hinausgeht. Um die Nutzung zu reduzieren, können Sie die Datenablaufzeiten für Datensätze oder pseudonyme Profile für Sandboxes und Datensätze konfigurieren."
>additional-url="https://experienceleague.adobe.com/de/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Automatisierte Ablauffristen für Datensätze"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=de" text="Ablauf von Daten pseudonymer Profile"

Proaktive Verwaltung und Optimierung Ihrer Lizenzierungsressourcen mit präzisen, aktuellen Nutzungsprognosen. Die Spalte [!UICONTROL Prognostizierte Nutzung] prognostiziert die zukünftige Lizenznutzung auf Sandbox-Ebene für alle gekauften Produkte in allen Produktions- und Entwicklungs-Sandboxes. Die Prognosen werden jetzt wöchentlich aktualisiert und bieten eine sechswöchige Prognose auf der Grundlage der neuesten Nutzungsdaten. Jede Prognose umfasst sowohl eine untere als auch eine obere Grenze, um eine informierte Planung zu unterstützen.

>[!IMPORTANT]
>
>Die Prognosen werden wöchentlich jeden Freitag aktualisiert. Das Datum der Aktualisierung ist in einem Infosymbol enthalten (![Dieses Infosymbol.](../images/license-usage/info-icon.png)) über dem Spaltentitel.

Zeigen Sie auf der Registerkarte „Produkt“ unter der Tabelle [!UICONTROL Kernprodukte] eine Zusammenfassung der Nutzung [!UICONTROL  Produktberechtigungen ].

![Die Registerkarte [!UICONTROL Lizenznutzung] [!UICONTROL Produkt] mit einem hervorgehobenen Produkt und der Spalte „Prognostizierte Nutzung“.](../images/license-usage/product-predicted-usage.png)

>[!NOTE]
>
>Beachten Sie, dass die Prognosen zur Lizenznutzung anhand der bisherigen Nutzung als Näherungswert betrachtet werden sollten. Sie sind dafür verantwortlich, die tatsächliche Nutzung Ihres Unternehmens zu verstehen und sicherzustellen, dass die Nutzung nicht über den Rahmen der Lizenzvereinbarung Ihres Unternehmens mit Adobe hinausgeht.

Der Prozentsatz der prognostizierten Nutzung wird wie folgt bestimmt:

- Wenn sich die unteren und oberen Grenzen deutlich unterscheiden, werden sie als Bereich angezeigt (z. B. 32 % bis 35 %).
- Wenn die unteren und oberen Grenzen nahezu identisch und nicht gleich null sind, werden sie als annähernder Wert angezeigt (z. B. ~34 %).
- Wenn die unteren und oberen Grenzen nahezu identisch und gleich null sind, werden sie als genau 0 % angezeigt.

>[!NOTE]
>
>„Nahezu identisch“ bedeutet in diesem Zusammenhang, dass die Werte auf zwei Dezimalstellen statistisch signifikant sind (z. B. werden eine Untergrenze von 0,342 und eine Obergrenze von 0,344 jeweils auf 34 % gerundet).

Die Funktion „Prognostizierte Nutzung“ unterstützt die folgenden Metriken:

- [!UICONTROL Adressierbare Zielgruppe]
- [!UICONTROL Profile von Geschäftspersonen]
- [!UICONTROL Stunden berechnen]
- [!UICONTROL Kunden-Journey-Zielgruppe - Anzahl der Zeilen]
- [!UICONTROL Ansprechbare Profile]
- [!UICONTROL Gesamtdatenvolumen]

## Verfügbare Metriken {#available-metrics}

>[!IMPORTANT]
>
>Ab dem 20. August sahen Kundinnen und Kunden mit Berechtigungen für [!UICONTROL Durchschnittliche Profilreichhaltigkeit] und [!UICONTROL Gesamtspeicher] stattdessen &quot;[!UICONTROL Gesamtdatenvolumen]&quot; im Lizenznutzungs-Dashboard. Es gab keine Änderung bei den Kundenberechtigungen, sondern nur eine Vereinfachung der Tracking-Metriken. [!UICONTROL Gesamtdatenvolumen] stellt die Daten dar, die im Echtzeit-Kundenprofil für Interaktions- und Personalisierungs-Workflows verfügbar sind. Diese vereinfachte Metrik verbesserte die Verwaltung und Messung der Verwendung von Echtzeit-Kundenprofilen. Kunden wurden gebeten, sich an ihren Adobe-Support-Mitarbeiter zu wenden, um weitere Informationen zu dieser Änderung zu erhalten.

Das Lizenznutzungs-Dashboard enthält Berichte zu verschiedenen eindeutigen Metriken, die für mehrere Produkte in der Organisation gelten. Die verfügbaren Metriken sind:

| Metrik | Beschreibung |
|---|---|
| [!UICONTROL Audience Activation-Größe] | Die Gesamtgröße der für ein dateibasiertes Ziel aktivierten Profile in einem Jahr. Hinweis: Dies beinhaltet keine Profile, die über Streaming-Ziele gesendet werden. |
| [!UICONTROL Addressable Audience] | Die Gruppe von Personenprofilen im Echtzeit-Kundenprofil, mit denen Ihr Unternehmen interagieren darf, einschließlich direkt identifizierbarer und pseudonymer Profile. Diese Profile können Attribute, Verhaltensweisen und Segmentzugehörigkeitsdaten enthalten. Profilvolumina werden mithilfe des standardmäßigen deterministischen Identitätsdiagramms von Adobe Experience Platform berechnet und werden als freigegebene Funktion betrachtet. |
| [!UICONTROL Ad-hoc-Query Service-Benutzerpakete] | Ein Add-on, um die Berechtigung für autorisierte gleichzeitige Abfrage-Service-Benutzende um fünf zusätzliche gleichzeitige Abfrage-Service-Benutzende und eine zusätzliche gleichzeitig ausgeführte ungeplante Abfrage pro Paket zu erhöhen. Es können mehrere Pakete mit zusätzlichen ungeplanten Abfrage-Benutzenden lizenziert werden. |
| [!UICONTROL Durchschnittliche Profilreichhaltigkeit] | **Veraltet** - Die Summe aller Produktionsdaten, die zu einem beliebigen Zeitpunkt im Hub-Profil-Service gespeichert sind, dividiert durch die fünffache Anzahl der Profile autorisierter Geschäftspersonen. [!UICONTROL Durchschnittliche Profilreichhaltigkeit] ist eine gemeinsam genutzte Funktion. |
| [!UICONTROL CJA-Zeilen verfügbar] | Die täglichen durchschnittlichen Datenzeilen, die für die Analyse in Customer Journey Analytics verfügbar sind. |
| [!UICONTROL Berechnete Attribute] | Aggregierte Profilverhaltensdaten basierend auf Erlebnisereignissen, die in ein Profilattribut konvertiert werden und in ein Personenprofil aufgenommen werden können. |
| [!UICONTROL Privatkunden-Zielgruppe] | Die Anzahl der Personenprofile, die im Kundenauftrag als „Consumer Audience“ identifiziert wurden. |
| [!UICONTROL Größe des Datenexports] | Die Datenmenge, die über Datensatzaktivierungen in einem Jahr gesendet wird. |
| [!UICONTROL Datenexporte] | Die Gesamtgröße der Datensätze, die (direkt oder indirekt) in einem Jahr in eine beliebige Nicht-Adobe-Lösung exportiert werden können. |
| [!UICONTROL Data Lake Storage] | Die vom analytischen Datenspeicher in Adobe Experience Platform verwendete Menge. |
| [!UICONTROL Ansprechbare Zielgruppe] | Eine Gruppe von Personenprofilen im Echtzeit-Kundenprofil, an die Sie in den letzten 12 Monaten mithilfe der Authoring-, Entscheidungs-, Bereitstellungs-, Experimentier- oder Orchestrierungsfunktionen von Journey Optimizer versucht haben zu interagieren. |
| [!UICONTROL Lookalike-Zielgruppen] | Eine Verbraucher-Lookalike-Zielgruppe ist eine Zielgruppe, die durch die Modellierung einer vorhandenen Verbraucher-Zielgruppe generiert wird, um Personenprofile mit ähnlichen Attributen oder Verhaltensweisen zu identifizieren. |
| [!UICONTROL Anzahl der AMM-Modelle] | Eine Zählung des Modells für maschinelles Lernen (integriert in Adobe Mix Modeler), mit dem ein bestimmtes Ergebnis auf Grundlage Ihrer Investitionen gemessen und/oder vorhergesagt wird. |
| [!UICONTROL Anzahl der Sandboxes] | Die Anzahl der logischen Trennungen eines On-Demand-Services von Adobe innerhalb Ihrer Instanz, der auf Adobe Experience Platform zugreift und Daten und Vorgänge isoliert. |
| [!UICONTROL Reichhaltigkeit des Profils - Anzahl der Packungen] | Eine Erhöhung des autorisierten Gesamtdatenvolumens um 25 KB pro Profil für jedes Paket mit zusätzlichem Profilumfang. |
| [!UICONTROL Query Service Compute Hours] | Ein Maß für die Zeit, die die Abfrage-Service-Engines benötigen, um Daten bei Ausführung einer Batch-Abfrage im Data Lake zu lesen, dort zu verarbeiten und dorthin zurückzuschreiben. |
| [!UICONTROL Streaming-Segmentierung: Anzahl der Packs] | Die Pakete aktualisieren die Segmentzugehörigkeit für ein Personenprofil, wenn neue Daten über einen Streaming-Fluss in den Segmentierungs-Service gelangen. Die Segmentzugehörigkeit wird basierend auf den aktuellen Personenprofilattributen und dem Wert des aktuellen Ereignisses bewertet, ohne das historische Verhalten zu berücksichtigen. Streaming-Segmentierung ist eine gemeinsam genutzte Funktion. |
| [!UICONTROL Gesamtdatenvolumen] | Die Gesamtmenge der für das Echtzeit-Kundenprofil verfügbaren Daten, die in Interaktions-Workflows verwendet werden können. Das Gesamtdatenvolumen wird anhand der folgenden Formel berechnet: **Gesamtdatenvolumen = Adressierbare Zielgruppe × Durchschnittliche Profilreichhaltigkeit**. Diese Metrik spiegelt Daten wider, die nur im Profilspeicher gespeichert sind, und schließt den Data-Lake-Speicher aus. Sie bietet eine fokussiertere Ansicht von Daten, die für die profilbasierte Interaktion relevant sind. Weitere Informationen finden [ unter „Häufig gestellte Fragen zum ](../../landing/license-usage-and-guardrails/total-data-volume.md) Datenvolumen insgesamt“. |
| [!UICONTROL Gesamtvolumen des Datenausgangs] | Das kumulative Jahresvolumen der aus Adobe Experience Platform in Data Warehouses von Drittanbietern exportierten Daten. |

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

Weitere Informationen zu anderen in der Experience Platform-Benutzeroberfläche verfügbaren Funktionen finden Sie im Handbuch zur Experience Platform-Benutzeroberfläche [](../../landing/ui-guide.md).
