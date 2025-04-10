---
title: Adobe Experience Platform – Versionshinweise, Oktober 2022
description: Versionshinweise von Oktober 2022 für Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 90%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 26. Oktober 2022**

- [Kundenverwaltete Schlüssel](#cmk)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Abfrage-Service](#query-service)

## Kundenverwaltete Schlüssel {#cmk}

Alle in Adobe Experience Platform gespeicherten Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Experience Platform aufbaut, können Sie jetzt stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

Details zur Funktion finden Sie in der Übersicht [Kundenverwaltete Schlüssel](../../landing/governance-privacy-security/customer-managed-keys/overview.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umgang mit sensiblen Daten für Datenströme | Datenströme nutzen jetzt mehrere Experience Platform-Technologien, um sensible Daten entsprechend den Vorschriften wie dem Health Insurance Portability and Accountability Act (HIPAA) zu behandeln. Weitere Informationen finden Sie im Abschnitt [Umgang mit sensiblen Daten in Datenströmen](../../datastreams/overview.md#sensitive). |
| [!DNL Splunk]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Splunk] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Splunk] Übersicht der Erweiterungen](../../tags/extensions/server/splunk/overview.md). |
| [!DNL Zendesk]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Zendesk] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Zendesk] Übersicht der Erweiterungen](../../tags/extensions/server/zendesk/overview.md). |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| (Beta) Datensatzexporte | Die [Beta-Funktion für Datensatzexporte](/help/destinations/ui/export-datasets.md) ermöglicht Ihnen den Export von Daten der ersten Generation (wie in der [Real-Time Customer Data Platform-Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) definiert) aus Adobe Experience Platform in Ihre eigenen externen Kundensysteme, und zwar über die Ziel-Benutzeroberfläche. Damit können Sie Daten aus Experience Platform mit einem Code-freien/Code-armen Workflow an sechs Cloud-Speicherziele (in der folgenden Tabelle aufgeführt) für analytische und Compliance-Anwendungsfälle übertragen. |
| (Beta) Verbesserte Dateiexport-Funktionen | Sie können jetzt beim Exportieren von Dateien aus Experience Platform von erweiterten Anpassungsfunktionen profitieren: <br><ul><li>Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möglichkeit, die Formatierung von exportierten CSV-Datendateien anzupassen](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Diese Funktionalität wird von den sechs neuen Beta-Cloud-Speicherkarten unterstützt, die in der folgenden Tabelle aufgeführt sind. |

{style="table-layout:auto"}

**Neue oder aktualisierte Ziele** {#new-or-updated-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line ist eine beliebte Kommunikationsplattform, die Menschen, Dienstleistungen und Informationen verbindet und sich von einer Chat-App zu einem Zentrum für Unterhaltung, soziale Aktivitäten und tägliche Aktivitäten entwickelt hat. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 ist eine Cloud-basierte Plattform für geschäftliche Anwendungen, die Enterprise Resource Planning (ERP) und Customer Relationship Management (CRM) mit Produktivitätsanwendungen und KI-Tools kombiniert, um einen rundum reibungsloseren und besser kontrollierten Betrieb, besseres Wachstumspotenzial und Kostenreduzierungen zu erzielen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Mit dem [!DNL (Beta) Adobe Commerce]-Ziel-Connector können Sie ein oder mehrere Real-Time CDP-Segmente auswählen, die Sie in Ihrem [!DNL Adobe Commerce]-Konto aktivieren, um Ihren Kunden ein dynamisches, personalisiertes Erlebnis zu bieten. Innerhalb von [!DNL Adobe Commerce] können Sie dann diese Real-Time CDP-Segmente auswählen, um einzigartige Angebote im Warenkorb zu personalisieren, wie beispielsweise „Kaufen Sie zwei, erhalten Sie eins gratis“. Sie können auch Hero-Banner anzeigen und die Produktpreise durch Werbeangebote ändern, die alle auf Adobe Real-Time CDP-Segmente zugeschnitten sind. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Stellen Sie eine aktive ausgehende Verbindung zu [!DNL Azure Data Lake Storage Gen2] her, um Datendateien aus Adobe Experience Platform regelmäßig zu dem von Ihnen festgelegten Datenspeicherort zu exportieren. Dieses neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Experience Platform zu exportieren. Dieses neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Stellen Sie eine aktive ausgehende Verbindung zu [!DNL Google Cloud Storage] her, um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Behälter zu exportieren. Dieses neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Wenn Sie die Betaversion verwenden, sehen Sie jetzt im Zielkatalog zwei [!DNL Amazon S3]-Zielkarten nebeneinander. Das neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Wenn Sie die Betaversion verwenden, sehen Sie jetzt im Zielkatalog zwei [!DNL Azure Blob]-Zielkarten nebeneinander. Das neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Wenn Sie die Betaversion verwenden, sehen Sie jetzt im Zielkatalog zwei [!DNL SFTP]-Zielkarten nebeneinander. Das neue Beta-Ziel bietet eine erweiterte Dateiexportfunktionalität und unterstützt Datensatzexporte. |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| [Leitplanken für Ziele](../../destinations/guardrails.md) | Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Das Feld `authorized` wurde von einem booleschen Typ in eine Zeichenfolge geändert. `season` und `episode` wurden von Ganzzahlen in Zeichenfolgen geändert. |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` wurde in `friendlyName` und `ID` in `name` umbenannt. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` wurde in `name` umbenannt.  |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Überwachen von Abfragen über die Experience Platform-Benutzeroberfläche | Die Abfrage-Service-Registerkarte [!UICONTROL Geplante Abfragen] bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit des Status aller Abfrageaufträge. Wichtige Informationen zum Status Ihrer Abfrageausführungen, einschließlich Fehlermeldungen und -Codes, falls sie fehlschlagen, finden Sie jetzt auf der Registerkarte [!UICONTROL Geplante Abfragen]. Sie können über die Benutzeroberfläche für jede dieser Abfragen auch Warnhinweise auf der Grundlage des Abfragestatus abonnieren. Weitere Informationen zu dieser Funktion finden Sie im Dokument [Überwachen von Abfragen](../../query-service/ui/monitor-queries.md). |
| Datenmodell für die Abfrage von beschleunigten Berichtseinblicken | Im Rahmen der Data Distiller SKU können Sie mit dem abfragebeschleunigten Speicher die Zeit und Verarbeitungsleistung reduzieren, die erforderlich sind, um wichtige Einblicke aus Ihren Daten zu gewinnen. Mit dem abfragebeschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder vorhandene Adobe Real-time Customer Data Platform-Datenmodelle erweitern, um Ihre Reporting-Insights und deren Visualisierungen zu verbessern. Siehe das Dokument [Reporting-Insights des abfragebeschleunigten Speichers](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md), um mehr über diese Funktion zu erfahren. |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).
Neue Funktionen in Adobe Experience Platform:

