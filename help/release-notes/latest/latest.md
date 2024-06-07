---
title: Adobe Experience Platform – Versionshinweise Mai 2024
description: Versionshinweise Mai 2024 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 24%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 21. Mai 2024**

>[!TIP]
>
>Die [Dokumentation zur Experience Platform-API](https://developer.adobe.com/experience-platform-apis/) ist jetzt interaktiv. Erkunden Sie die API-Endpunkte direkt auf den Dokumentationsseiten, um sofort Feedback zu erhalten und Ihre technische Implementierung zu beschleunigen. [Mehr dazu](#interactive-api-documentation) über die neue Funktion.

Aktualisierungen vorhandener Funktionen im Experience Platform:

- [Katalog-Service](#catalog-service)
- [Dashboards](#dashboards)
- [Data Governance](#governance)
- [Ziele](#destinations)
- [Abfrage-Service](#query-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

Weitere Updates in Adobe Experience Platform:

- [Dokumentation – Aktualisierungen](#documentation-updates)

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Während alle Daten, die in Experience Platform aufgenommen werden, als Dateien und Ordner im Data Lake gespeichert sind, enthält der Katalog die Metadaten und Beschreibungen dieser Dateien und Ordner zu Such- und Überwachungszwecken.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Massenaktionen | Das Datensatzinventar unterstützt jetzt Massenaktionen. Optimieren Sie Ihre Datenverwaltungsprozesse und sorgen Sie mit Massenaktionen für eine effiziente Verwaltung Ihrer Datensätze. Verwenden Sie Massenaktionen, um Zeit zu sparen, indem Sie mehrere Aktionen für zahlreiche Datensätze gleichzeitig ausführen.  Massenaktionen umfassen [In Ordner verschieben](../../catalog/datasets/user-guide.md#move-to-folders), [Tags bearbeiten](../../catalog/datasets/user-guide.md#manage-tags), und [Löschen](../../catalog/datasets/user-guide.md#delete) Datensätze. <br> ![Massenaktionen in der Benutzeroberfläche &quot;Datensätze&quot;.](../2024/assets/may/bulk-actions.png "Massenaktionen in der Benutzeroberfläche &quot;Datensätze&quot;."){width="100" zoomable="yes"} <br> Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Datensätzen](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anpassbare Insights für erweiterte App-Berichte | Nahtlos [die Ausgabe der SQL-Analyse in verständliche, unternehmensfreundliche visuelle Formate überführen](../../dashboards/data-distiller/customizable-insights/overview.md). Verwenden Sie benutzerdefinierte SQL-Abfragen zur präzisen Datenbearbeitung und zur Erstellung dynamischer Diagramme aus diversen strukturierten Datensätzen. Sie können den Abfragepro-Modus verwenden, um eine komplexe Analyse mit SQL durchzuführen und diese Analyse dann über Diagramme in Ihrem benutzerdefinierten Dashboard für nicht technische Benutzer freizugeben oder in CSV-Dateien zu exportieren. |

{style="table-layout:auto"}

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| mTLS-Unterstützung für HTTP-API-Ziele und benutzerdefinierte Adobe Journey Optimizer-Aktionen | Bauen Sie mit den verstärkten Sicherheitsmaßnahmen des Protokolls &quot;Mutual Transport Layer Security (mTLS)&quot;das Kundenvertrauen auf. Die [Experience Platform-HTTP-API-Ziel](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) und [Benutzerdefinierte Adobe Journey Optimizer-Aktionen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) unterstützt jetzt das mTLS-Protokoll beim Senden von Daten an konfigurierte Endpunkte. Für Ihre benutzerdefinierte Aktion oder Ihr HTTP-API-Ziel ist keine zusätzliche Konfiguration erforderlich, um mTLS zu aktivieren. Dieser Prozess erfolgt automatisch, wenn ein mTLS-fähiger Endpunkt erkannt wird. Sie können [Das öffentliche Adobe Journey Optimizer-Zertifikat hier herunterladen](../../landing/governance-privacy-security/encryption.md#download-certificates) und [Öffentliches Zertifikat für den Zieldienst hier](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>Siehe [Dokumentation zur Experience Platform-Datenverschlüsselung](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) für weitere Informationen zu Netzwerkverbindungsprotokollen beim Exportieren von Daten in Systeme von Drittanbietern. |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Neuanordnen von Zuordnungsfeldern für Batch-Ziele | Sie können jetzt die Reihenfolge der Spalten in Ihren CSV-Exporten ändern, indem Sie die Zuordnungsfelder per Drag-and-Drop in die [Zuordnungsschritt](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Die Reihenfolge der zugeordneten Felder in der Benutzeroberfläche entspricht der Reihenfolge der Spalten in der exportierten CSV-Datei von oben nach unten, wobei die oberste Zeile die ganz links in der CSV-Datei ist. <br> ![Erfahren Sie, wie Zuordnungen neu angeordnet werden können.](../2024/assets/may/reorder-mappings.gif "Erfahren Sie, wie Zuordnungen neu angeordnet werden können."){width="100" zoomable="yes"} |
| Vorgewählte standardmäßige Exportzeitpläne für Batch-Ziele | Experience Platform legt nun automatisch einen Standardzeitplan für jeden Dateiexport fest. Siehe die Dokumentation unter [Zielgruppenexporte planen](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) , um zu erfahren, wie Sie den Standardzeitplan ändern. |
| Mehrere Zielgruppenaktivierungszeitpläne für Batch-Ziele bearbeiten | Sie können jetzt den Aktivierungsplan für mehrere Zielgruppen bearbeiten, die aus dem **[!UICONTROL Aktivierungsdaten]** des [Zieldetailseite](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br> ![Hier erfahren Sie, wie Sie mehrere Zielgruppen auswählen und den Zeitplan für den Dateiexport bearbeiten.](../2024/assets/may/bulk-edit-schedule.gif "Hier erfahren Sie, wie Sie mehrere Zielgruppen auswählen und den Zeitplan für den Dateiexport bearbeiten."){width="100" zoomable="yes"} |
| Mehrere Zielgruppen On-Demand an Batch-Ziele exportieren | Sie können jetzt mehrere Zielgruppen über die [Exportieren von Dateien On-Demand](../../destinations/ui/export-file-now.md) Funktionalität. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Veralteter Editor veraltet | Der alte Editor wird nicht mehr unterstützt und kann nicht mehr verwendet werden. An seiner Stelle können Sie die [erweiterte Funktionen des Abfrage-Editors](../../query-service/ui/user-guide.md#query-authoring) zum Schreiben, Validieren und Ausführen Ihrer Abfragen. |
| Verzögerung der Abfrageausführung | Halten Sie die Kontrolle über Ihre Berechnungszeiten, indem Sie Warnhinweise für Verzögerungen bei der Ausführung Ihrer Abfragen einrichten. Sie können Warnungen erhalten, wenn sich der Status einer Abfrage nach einem bestimmten Zeitraum nicht ändert. Legen Sie einfach die gewünschte Verzögerungszeit in der Platform-Benutzeroberfläche fest, um über den Fortschritt Ihrer Abfrage auf dem Laufenden zu bleiben. Informationen zum Festlegen dieses Warnhinweises in der Benutzeroberfläche finden Sie im Abschnitt [Dokumentation zu Abfrageplänen](../../query-service/ui/query-schedules.md#alerts-for-query-status) oder [Anleitung zu Inline-Abfrageaktionen](../../query-service/ui/monitor-queries.md#query-run-delay). |
| Optimiertes Abfrageloginventar | Sie können jetzt eine verbesserte Effizienz bei der Fehlerbehebung und Aufgabenüberwachung mit einer [optimierte Benutzeroberfläche für Abfrageprotokolle](../../query-service/ui/query-logs.md#filter-logs): <ul><li> In der Platform-Benutzeroberfläche werden jetzt standardmäßig alle &quot;Systemabfragen&quot;aus der Registerkarte &quot;Protokolle&quot;ausgeschlossen. </li><li> Systemabfragen anzeigen, deaktivieren **Systemabfragen ausschließen**. </li></ul> <br> ![Registerkarte &quot;Protokolle&quot;in der Benutzeroberfläche &quot;Abfragen&quot;.](../2024/assets/may/query-log.png "Registerkarte &quot;Protokolle&quot;in der Benutzeroberfläche &quot;Abfragen&quot;."){width="100" zoomable="yes"} <br> Verwenden Sie die optimierte Benutzeroberfläche für Abfrageprotokolle, um eine genauere Ansicht zu erhalten, mit der Sie die relevanten Protokolle schnell identifizieren und analysieren können. |
| Datenbankauswahl | Verwenden Sie das neue Dropdown-Menü für die Datenbankauswahl, um [bequemer Zugriff auf Customer Journey Analytics-Datenansichten von Power BI oder Tableau](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). Sie können jetzt Ihre gewünschte Datenbank direkt über die Platform-Benutzeroberfläche auswählen, um eine nahtlosere Integration Ihrer BI-Tools zu erreichen. <br> ![Registerkarte &quot;Anmeldeinformationen&quot;in der Benutzeroberfläche &quot;Abfragen&quot;.](../2024/assets/may/database-selector.png "Registerkarte &quot;Anmeldeinformationen&quot;in der Benutzeroberfläche &quot;Abfragen&quot;."){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Importieren von extern generierten Zielgruppen | Für den Import extern generierter Zielgruppen ist nun die Berechtigung &quot;Zielgruppe importieren&quot;erforderlich. Weitere Informationen zu Berechtigungen finden Sie im Abschnitt [Handbuch zur Berechtigungs-UI](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen im Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern zu erfassen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| OAuth2 Client Credential authentication for [!DNL Salesforce] source | Sie können jetzt OAuth2 Client Credential verwenden, um Ihre [!DNL Salesforce] -Konto auf Experience Platform. Lesen Sie die [!DNL Salesforce] source [API-Handbuch](../../sources/tutorials/api/create/crm/salesforce.md) und [UI-Handbuch](../../sources/tutorials/ui/create/crm/salesforce.md) für weitere Informationen. |
| Unterstützung für Beispiel-Datenfluss für [!DNL Marketo Engage] source | Die [!DNL Marketo Engage] -Quelle unterstützt jetzt Beispiel-Datenflüsse. Aktivieren Sie die Beispieldatenflusskonfiguration, um Ihre Erfassungsrate zu begrenzen, und testen Sie dann Experience Platform-Funktionen, ohne große Datenmengen aufnehmen zu müssen. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Datenflusses für [!DNL Marketo Engage] in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| Aktualisierungen der IP-Adressen-Zulassungsliste | Abhängig von Ihrem Standort müssen Sie Ihrer Zulassungsliste eine Reihe neuer IP-Adressen hinzufügen, um Streaming-Quellen erfolgreich verwenden zu können. Eine umfassende Liste der neuen IP-Adressen finden Sie im [Handbuch zur Zulassungsliste von IP-Adressen](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Aktualisierte Dokumentation | Beschreibung |
| --- | --- |
| Dokumentationsaktualisierungen für [!DNL Google PubSub] | Die [!DNL Google PubSub] Die Quelldokumentation wurde mit einem umfassenden Anleitung für die Voraussetzungen aktualisiert. Verwenden Sie den neuen Abschnitt &quot;Voraussetzungen&quot;, um zu erfahren, wie Sie Ihr Dienstkonto erstellen, Berechtigungen auf Themen- oder Abonnementebene gewähren und Konfigurationen festlegen, um Ihre Nutzung der [!DNL Google PubSub] -Quelle. Lesen Sie die [[!DNL Google PubSub] Übersicht](../../sources/connectors/cloud-storage/google-pubsub.md) für weitere Informationen. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).

## Dokumentation – Aktualisierungen {#documentation-updates}

### Dokumentation zur interaktiven Experience Platform-API {#interactive-api-documentation}

Die [Dokumentation zur Experience Platform-API](https://developer.adobe.com/experience-platform-apis/) ist jetzt interaktiv. Alle API-Referenzseiten verfügen jetzt über eine **Testen** .funktionale, die Sie verwenden können, um API-Aufrufe direkt auf der Dokumentations-Website zu testen. [Abrufen der erforderlichen Authentifizierungsberechtigungen](/help/landing/api-authentication.md) und beginnen Sie mit der Verwendung der -Funktion, um die API-Endpunkte zu untersuchen.

Verwenden Sie diese neue Funktion, um die Anfragen an und Antworten von API-Endpunkten zu untersuchen, um sofort Feedback zu erhalten und Ihre technische Implementierung zu beschleunigen. Besuchen Sie beispielsweise die [Identity Service-API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) oder [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) Endpunkte zur Erforschung der neuen **Testen** in der rechten Leiste.

![Bildschirmaufzeichnung mit einem API-Aufruf, der direkt von der Dokumentations-Website aus durchgeführt wird.](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>Beachten Sie, dass Sie durch die Verwendung der interaktiven API-Funktion auf den Dokumentationsseiten echte API-Aufrufe an die Endpunkte durchführen. Beachten Sie dies beim Experimentieren mit Produktions-Sandboxes.

### Personalisierte Einblicke und Interaktion {#personalized-insights-engagement}

Eine neue Dokumentationsseite für durchgängige Anwendungsfälle für [Entwicklung eines einmaligen Werts zum Lebenszeitwert](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) ist jetzt live. In dieser Dokumentation erfahren Sie, wie Sie mit Real-Time CDP und Adobe Journey Optimizer sporadische Besucher in Ihre Webeigenschaften in treue Kunden konvertieren können.
