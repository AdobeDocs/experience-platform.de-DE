---
title: Adobe Experience Platform - Versionshinweise, August 2022
description: Die Versionshinweise für Adobe Experience Platform vom August 2022.
source-git-commit: 925991d58c3cdd84e13b12a095e9681b8f4b254b
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 35%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 24. August 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenvorbereitung](#data-prep)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für die Aufnahme von Datensätzen mit Warnungen | Die Datenvorbereitung lokalisiert nun Warnungen (nicht kritische Fehler) in die Felder und ermöglicht die Erfassung des restlichen Teils der Zeile. Alle Mapper-Transformationsfehler werden jetzt als Warnungen und teilweise aufgenommene Zeilen als erfolgreich gemeldet, mit einer Warnung.  Die Überwachung wird auch für Datensätze mit Warnungen und Diagnosedetails unterstützt. Die partielle Erfassung von Datensätzen mit Warnungen ist derzeit nur für Streaming-Daten verfügbar. Lesen Sie die Dokumentation unter [Erfassen von Datensätzen mit Warnungen](../../sources/tutorials/ui/monitor-streaming.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL AJO-Entitätsschema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Beschreibt denormalisierte Entitäten für Adobe Journey Optimizer. |
| Klasse | [[!UICONTROL AJO-Ausführungsentitäten]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Beschreibt Ausführungsentitäten von Adobe Journey Optimizer zur Verwendung in der Segmentierung. |
| Feldergruppe | [[!UICONTROL Workfront-Arbeitsobjekte]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Eine Wrapper-Feldergruppe, die auf alle objektspezifischen Feldergruppen der unteren Ebene für Adobe Workfront verweist. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Allgemeine Felder für Journey Orchestration Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Zwei neue Eigenschaften wurden hinzugefügt: `origTimeStamp` und `experienceID`. |
| Feldergruppe | [[!UICONTROL Details zur Segmentzugehörigkeit]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Zusätzlich zu [!UICONTROL XDM Individual Profile]festgelegt ist, kann diese Feldergruppe jetzt auch in Schemas verwendet werden, die auf der XDM Business Account-Klasse basieren. |
| Feldergruppe | (Mehrere) | Mehrere Feldergruppen im Zusammenhang mit Marketo B2B-Aktivitäten wurden auf den Status &quot;stabil&quot;aktualisiert. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1593/files) für Details. |
| Feldergruppe | (Mehrere) | Mehrere wetterbezogene Feldergruppen wurden aktualisiert, um Fehler zu beheben, die bei `uvIndex` und `sunsetTime`. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1602/files) für Details. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Eine neue Eigenschaft `productImageUrl` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Eine neue Eigenschaft `framesPerSecond` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` wurde in `appVersion` umbenannt. `meta:enum` und `description` -Felder wurden ebenfalls aktualisiert. |
| Datentypen und Feldergruppen | (Mehrere) | Mehrere Mediendaten und Feldergruppen verfügen über neue Felder und aktualisierte Beschreibungen. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1582/files) für Details. |
| (Alle) | (Mehrere) | Alle Schemaobjekte, die eine `enum` -Feld enthält jetzt auch die entsprechende `meta:enum` -Feld, um die Anzeigewerte für jede Begrenzung anzugeben. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1601/files) für Details. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von Self-Serve-Quellen (Batch-SDK) | Entwickeln, testen und integrieren Sie Ihre REST API-basierte Datenquelle, um Batch-Daten mithilfe einfacher Quellspezifikationen in Experience Platform zu erfassen. Mit dem Sources-SDK können Sie: <ul><li>Konfigurieren Sie eine neue Quelle für den Experience Platform-Katalog.</li><li>Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen, Planung und Art und Weise, wie Ressourcendaten abgerufen werden.</li><li>Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.</li></ul> Weitere Informationen finden Sie in der Dokumentation unter [Self-Serve-Quellen (Batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allgemeine Verfügbarkeit der [!DNL Google BigQuery]-Quelle | Verwenden Sie die [!DNL Google BigQuery] -Quelle, um Daten aus Ihrem [!DNL Google BigQuery] Data Warehouse in Experience Platform. Weitere Informationen finden Sie in der Dokumentation unter [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (Beta) | Verwenden Sie die [!DNL Teradata Vantage] -Quelle, um Daten aus hybriden Multi-Cloud-Umgebungen in Experience Platform zu erfassen. Weitere Informationen finden Sie in der Dokumentation unter [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Regionsübergreifende Unterstützung für Adobe Analytics-Quellen | Sie können jetzt Report Suites aus einer beliebigen Region (USA, Großbritannien oder Singapur) erfassen. Report Suites müssen derselben Organisation wie die Experience Platform-Sandbox-Instanz zugeordnet sein, in der die Quellverbindung erstellt wird. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| API-Unterstützung für On-Demand-Erfassung | Verwenden Sie die On-Demand-Erfassung, um Ad-hoc-Fluss-Läufe für einen bestimmten Datenfluss mit dem [!DNL Flow Service] API. Die erstellten Flussläufe müssen auf eine einmalige Erfassung festgelegt werden. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der API](../../sources/tutorials/api/on-demand-ingestion.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
