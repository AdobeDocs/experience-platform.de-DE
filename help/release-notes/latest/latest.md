---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 184ead059533d2706a5d3fca96dc082248955afe
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 70%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 26. Oktober 2022**

Neue Funktionen in Adobe Experience Platform:

- [Kundenverwaltete Schlüssel](#cmk)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Quellen](#sources)

## Kundenverwaltete Schlüssel {#cmk}

Alle in Adobe Experience Platform gespeicherten Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Platform aufbaut, können Sie jetzt stattdessen eigene Verschlüsselungsschlüssel verwenden, was Ihnen mehr Kontrolle über Ihre Datensicherheit gibt.

Details zur Funktion finden Sie in der Übersicht [Kundenverwaltete Schlüssel](../../landing/governance-privacy-security/customer-managed-keys.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umgang mit sensiblen Daten für Datenströme | Datenströme nutzen jetzt verschiedene Platform-Technologien, um sensible Daten angemessen zu handhaben, wie es durch Vorschriften wie den Health Insurance Portability and Accounability Act (HIPAA) erzwungen wird. Weitere Informationen finden Sie im Abschnitt [Umgang mit sensiblen Daten in Datenströmen](../../edge/datastreams/overview.md#sensitive). |
| [!DNL Splunk]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Splunk] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Splunk] Übersicht der Erweiterungen](../../tags/extensions/web/splunk/overview.md). |
| [!DNL Zendesk]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Zendesk] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Zendesk] Übersicht der Erweiterungen](../../tags/extensions/web/zendesk/overview.md). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| (Beta) Datensatzexporte | Die [Datensatzexporte Beta-Funktionalität](/help/destinations/ui/export-datasets.md) ermöglicht den Export von Daten der ersten Generation (wie in der Variablen [Real-time Customer Data Platform-Produktbeschreibung](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) von Adobe Experience Platform zu Ihren eigenen externen Kundensystemen über die Benutzeroberfläche &quot;Ziele&quot;. So können Sie Daten aus der Experience Platform mit einem Nicht-Code-/Niedrigcode-Workflow an sechs Cloud-Speicher-Ziele (in der folgenden Tabelle aufgeführt) für analytische Anwendungsfälle und Compliance-Anwendungsfälle übertragen. |
| (Beta) Verbesserte Dateiexport-Funktionen | Sie können jetzt von der erweiterten Anpassungsfunktion profitieren, wenn Sie Dateien aus Experience Platform exportieren: <br><ul><li>Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Möglichkeit, benutzerdefinierte Dateikopfzeilen in Ihren exportierten Dateien über die [Verbesserter Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möglichkeit, die Formatierung exportierter CSV-Datendateien anzupassen](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Diese Funktion wird von den sechs neuen Beta-Cloud-Speicherkarten unterstützt, die in der folgenden Tabelle aufgeführt sind. |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line ist eine beliebte Kommunikationsplattform, die Menschen, Dienstleistungen und Informationen verbindet und sich von einer Chat-App zu einem Zentrum für Unterhaltung, soziale Aktivitäten und tägliche Aktivitäten entwickelt hat. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 ist eine Cloud-basierte Plattform für geschäftliche Anwendungen, die Enterprise Resource Planning (ERP) und Customer Relationship Management (CRM) mit Produktivitätsanwendungen und KI-Tools kombiniert, um einen rundum reibungsloseren und besser kontrollierten Betrieb, besseres Wachstumspotenzial und Kostenreduzierungen zu erzielen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Mit dem [!DNL (Beta) Adobe Commerce]-Ziel-Connector können Sie ein oder mehrere Real-Time CDP-Segmente auswählen, die Sie in Ihrem [!DNL Adobe Commerce]-Konto aktivieren, um Ihren Kunden ein dynamisches, personalisiertes Erlebnis zu bieten. Innerhalb von [!DNL Adobe Commerce] können Sie dann diese Real-Time CDP-Segmente auswählen, um einzigartige Angebote im Warenkorb zu personalisieren, wie beispielsweise „Kaufen Sie zwei, erhalten Sie eins gratis“. Sie können auch Hero-Banner anzeigen und die Produktpreise durch Werbeangebote ändern, die alle auf Adobe Real-Time CDP-Segmente zugeschnitten sind. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Erstellen Sie eine ausgehende Live-Verbindung zu [!DNL Azure Data Lake Storage Gen2] , um Datendateien aus Adobe Experience Platform regelmäßig in Ihren eigenen Speicherort zu exportieren. Dieses neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] ist [!DNL Azure Blob] von Adobe Experience Platform bereitgestellte Speicherschnittstelle, über die Sie Zugriff auf eine sichere, Cloud-basierte Dateispeicheranlage erhalten, über die Dateien aus Platform exportiert werden können. Dieses neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Erstellen Sie eine ausgehende Live-Verbindung zu [!DNL Google Cloud Storage] , um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Buckets zu exportieren. Dieses neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta-Teilnehmer sehen jetzt zwei [!DNL Amazon S3] Zielkarten im Zielkatalog nebeneinander angezeigt. Das neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta-Teilnehmer sehen jetzt zwei [!DNL Azure Blob] Zielkarten im Zielkatalog nebeneinander angezeigt. Das neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta-Teilnehmer sehen jetzt zwei [!DNL SFTP] Zielkarten im Zielkatalog nebeneinander angezeigt. Das neue Beta-Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt Datensatzexporte. |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Dokumentation**

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| [Leitlinien für Ziele](../../destinations/guardrails.md) | Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Das Feld `authorized` wurde von einem booleschen Typ in eine Zeichenfolge geändert. `season` und `episode` wurden von Ganzzahlen in Zeichenfolgen geändert. |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` wurde in `friendlyName` und `ID` in `name` umbenannt. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` wurde in `name` umbenannt.  |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Überwachen von Abfragen über die Platform-Benutzeroberfläche | Query Service [!UICONTROL Geplante Abfragen] bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit für den Status aller Abfrageaufträge. Wichtige Informationen zum Status Ihrer Abfrageausführungen, einschließlich Fehlermeldungen und Codes bei Fehlern, finden Sie jetzt unter [!UICONTROL Geplante Abfragen] Registerkarte. Sie können Warnhinweise auch über die Benutzeroberfläche für jede dieser Abfragen auf Grundlage ihres Status abonnieren. Siehe [Dokument zur Überwachung von Abfragen](../../query-service/monitor-queries.md) , um mehr über diese Funktion zu erfahren. |
| Datenmodell für die Abfrage von beschleunigten Berichtseinblicken | Im Rahmen der Data Distiller SKU können Sie mit dem abfragebeschleunigten Speicher die Zeit und Verarbeitungsleistung reduzieren, die erforderlich sind, um wichtige Einblicke aus Ihren Daten zu gewinnen. Mit dem abfragebeschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder vorhandene Adobe Real-time Customer Data Platform-Datenmodelle erweitern, um Ihre Reporting-Insights und deren Visualisierungen zu verbessern. Siehe das Dokument [Reporting-Insights des abfragebeschleunigten Speichers](../../query-service/query-accelerated-store/reporting-insights-data-model.md), um mehr über diese Funktion zu erfahren. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).
Neue Funktionen in Adobe Experience Platform:

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- | 
| Beta-Verfügbarkeit der Adobe Workfront-Quelle | Verwenden Sie die [Adobe Workfront-Quelle](../../sources/connectors/adobe-applications/workfront.md), um Ihre Workfront-Daten in die Experience Platform zu bringen und bestimmte Anwendungsfälle auszuführen, z. B. die Kombination Ihrer Arbeitsdatensätze mit Drittanbieterdaten, die Anwendung von Verlaufs- und Zeitreihenanalysen auf Arbeitsdatensätze und das Abfragen von Arbeitsdaten mit standardmäßiger SQL. Weitere Informationen finden Sie im Handbuch zum [Erstellen einer Workfront-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

Weiterführende Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
