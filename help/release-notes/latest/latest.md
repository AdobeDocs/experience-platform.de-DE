---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: cf8f630360c2cdbba1082913b179e719156183f4
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 47%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 26. Oktober 2022**

Neue Funktionen in Adobe Experience Platform:

- [Vom Kunden verwaltete Schlüssel](#cmk)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Quellen](#sources)

## Vom Kunden verwaltete Schlüssel {#cmk}

Alle in Adobe Experience Platform gespeicherten Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie eine Anwendung verwenden, die auf Platform aufbaut, können Sie jetzt stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

Siehe Übersicht unter [kundenverwaltete Schlüssel](../../landing/governance-privacy-security/customer-managed-keys.md) für Details zur Funktion.

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umgang mit sensiblen Daten für Datastreams | Datastreams nutzt jetzt verschiedene Platform-Technologien, um sensible Daten, wie sie durch Vorschriften wie den Health Insurance Portability and Accounability Act (HIPAA) durchgesetzt werden, angemessen zu handhaben. Siehe Abschnitt zu [Umgang mit sensiblen Daten in Datenströmen](../../edge/datastreams/overview.md#sensitive) für weitere Informationen. |
| [!DNL Splunk] Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an senden [!DNL Splunk] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Splunk] Erweiterungsübersicht](../../tags/extensions/web/splunk/overview.md) für weitere Informationen. |
| [!DNL Zendesk] Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an senden [!DNL Zendesk] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Zendesk] Erweiterungsübersicht](../../tags/extensions/web/zendesk/overview.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line ist eine beliebte Kommunikationsplattform, die Menschen, Dienstleistungen und Informationen verbindet und sich von einer Chat-App zu einem Zentrum für Unterhaltung, soziale Aktivitäten und tägliche Aktivitäten entwickelt hat. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 ist eine Cloud-basierte Business-Anwendungsplattform, die Enterprise Resource Planning (ERP) und Customer Relationship Management (CRM) mit Produktivitätsanwendungen und AI-Tools kombiniert, um reibungslosere und besser kontrollierte Vorgänge, ein besseres Wachstumspotenzial und Kostensenkungen zu ermöglichen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Die [!DNL (Beta) Adobe Commerce] Mit dem Ziel-Connector können Sie ein oder mehrere Real-Time CDP-Segmente auswählen, die für Ihre [!DNL Adobe Commerce] -Konto ein dynamisches personalisiertes Erlebnis für Ihre Kunden bereitstellen. Within [!DNL Adobe Commerce]können Sie dann diese Real-Time CDP-Segmente auswählen, um individuelle Angebote im Warenkorb zu personalisieren, z. B. &quot;Kauf 2 erhält 1 kostenlos&quot;. Sie können Hero-Banner auch anzeigen und die Produktpreise über Werbeangebote ändern, die alle auf Adobe Real-Time CDP-Segmente zugeschnitten sind. |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Dokumentation**

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| [Limits für Ziele](../../destinations/guardrails.md) | Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Die `authorized` von einem booleschen Typ in eine Zeichenfolge. `season` und `episode` wurden von Ganzzahlen in Zeichenfolgen geändert. |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` wurde in `friendlyName`und `ID` wurde in `name`. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` wurde in `name` umbenannt.  |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Überwachen von Abfragen über die Platform-Benutzeroberfläche | Query Service [!UICONTROL Geplante Abfragen] bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit für den Status aller Abfrageaufträge. Wichtige Informationen zum Status Ihrer Abfrageausführungen, einschließlich Fehlermeldungen und Codes bei Fehlern, finden Sie jetzt unter [!UICONTROL Geplante Abfragen] Registerkarte. Sie können Warnhinweise auch über die Benutzeroberfläche für jede dieser Abfragen auf Grundlage ihres Status abonnieren. Siehe [Dokument zur Überwachung von Abfragen](../../query-service/monitor-queries.md) , um mehr über diese Funktion zu erfahren. |
| Datenmodell für Query Accelerated Reporting Insights | Im Rahmen der Data Distiller-SKU können Sie mit dem Abfrage-beschleunigten Store die Zeit und Verarbeitungsleistung reduzieren, die erforderlich sind, um wichtige Einblicke aus Ihren Daten zu gewinnen. Mit dem Abfrage-beschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder vorhandene Adobe Real-time Customer Data Platform-Datenmodelle erweitern, um Ihre Berichterstellungseinblicke und deren Visualisierungen zu verbessern. Siehe [Dokument mit Einblicken aus beschleunigten Speicherberichten abfragen](../../query-service/query-accelerated-store/reporting-insights-data-model.md) , um mehr über diese Funktion zu erfahren. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).
Neue Funktionen in Adobe Experience Platform:

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- | 
| Beta-Verfügbarkeit der Adobe Workfront-Quelle | Verwenden Sie die [Adobe Workfront-Quelle](../../sources/connectors/adobe-applications/workfront.md) , um Ihre Workfront-Daten in die Experience Platform zu bringen und Anwendungsfälle auszuführen, z. B. die Kombination Ihrer Arbeitsdatensätze mit Drittanbieterdaten, die Anwendung von Verlaufs- und Zeitreihenanalysen auf Arbeitsdatensätze und die Abfrage von Arbeitsdaten mit SQL. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Workfront-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Beta-Verfügbarkeit der Oracle Service Cloud-Quelle | Verwenden Sie die Oracle Service Cloud-Quelle, um Daten aus Ihrem Oracle Service Cloud-Konto in Experience Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation unter [Oracle Service Cloud-Quelle](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Weiterführende Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
