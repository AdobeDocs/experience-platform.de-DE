---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise Juli 2023 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3090b8a8eade564190dc32142c3fc71701007337
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 26. Juli 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Katalog-Service](#catalog-service)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Abfrage-Service](#query-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. Der Katalog wiederum speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

| Funktion | Beschreibung |
| --- | --- |
| Lagerbestandsverwaltung von Datensätzen | Die Benutzeroberfläche von Datensätzen bietet jetzt eine Sammlung von Inline-Aktionen, um Ihre Datensätze besser zu verwalten. Die erweiterte Datensatzverwaltung verbessert Ihre Arbeitseffizienz durch die Erstellung und Zuweisung von Ordnern und Tags zu Ihren Datensätzen, was eine Filterung und verbesserte Auffindbarkeit ermöglicht. Weitere Informationen finden Sie in der Dokumentation zu [Inline-Aktionen](../../catalog/datasets/user-guide.md#inline-actions), wie Sie [Datensätze suchen und filtern](../../catalog/datasets/user-guide.md#search-and-filter), und [Verschieben von Datensätzen in Ordner](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

Weitere Informationen zu Catalog Service finden Sie im Abschnitt [Catalog Service - Übersicht](../../catalog/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Tags und Ereignisweiterleitung | Auditprotokolle zur Datenerfassung | Sie können jetzt sehen, wann eine Aktion ausgeführt wurde und wer diese Aktion über Tags und Ereignisweiterleitung hinweg durchgeführt hat. Dies erleichtert die Fehlerbehebung bei Produkten, eine ordnungsgemäße Verwaltung und interne Auditaktivitäten. Diese Prüfdaten werden über kontextbezogene Slide-out-Menüs angezeigt, die auch Schnellaktionen und Aktualisierungen des Ressourcenstatus enthalten. Diese Daten sind in den folgenden Bildschirmen in der Benutzeroberfläche für Tags und Ereignisweiterleitung sichtbar:<br><ul><li>[Eigenschaftenübersicht](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Regeln](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Datenelemente](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Erweiterungen](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Bibliotheksüberprüfung](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Zuletzt erstellte und veröffentlichte Bibliothek](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Datenströme | [Geo-Suche](../../datastreams/configure.md#advanced-options) | Sie können jetzt die Geolocation und die Netzwerksuche für Datastreams konfigurieren, um Informationen wie folgende einzuschließen: <ul><li>Country</li><li>Postleitzahl</li><li>Bundesland/Provinz</li><li>DMA</li><li>Stadt</li><li>Breitengrad </li><li>Längengrad</li><li>Netzbetreiber</li><li>Domain</li><li>ISP</li></ul> Sie sind dafür verantwortlich, sicherzustellen, dass Sie alle erforderlichen Berechtigungen, Einverständnisse, Genehmigungen und Autorisierungen erhalten haben, die nach den geltenden Gesetzen und Vorschriften erforderlich sind, um personenbezogene Daten zu erfassen, zu verarbeiten und zu übermitteln, einschließlich präziser Geolocation-Informationen. <br> Ihre Auswahl der Verschleierung von IP-Adressen wirkt sich nicht auf die Ebene der Geolocation-Informationen aus, die von der IP-Adresse abgeleitet und an Ihre konfigurierten Adobe-Lösungen gesendet werden. Die Geolocation-Suche muss begrenzt oder separat deaktiviert sein. <br> Siehe [Dokumentation zu Datenastreams](../../datastreams/configure.md#advanced-options) für weitere Details. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie im [Datenerfassungen - Übersicht](../../tags/home.md).
<!-- 
## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions | You can now use the following functions when mapping objects in Data Prep: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

For more information on Data Prep, please read the [Data Prep overview](../../data-prep/home.md). -->

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | Neu | Integrierte Identitäten von Adobe Experience Platform in [!DNL LiveRamp Connect] , damit Sie Benutzer auf Mobilgeräten, im Web, in sozialen Netzwerken und [!DNL CTV] Plattformen, die die [!DNL Ramp ID] Kennung. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Neu | Stellen Sie eine aktive ausgehende Verbindung zu [!DNL Azure Data Lake Storage Gen2] her, um Datendateien aus Adobe Experience Platform regelmäßig zu dem von Ihnen festgelegten Datenspeicherort zu exportieren. Dieses neue Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Neu | [!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien aus Platform zu exportieren. Dieses neue Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Neu | Stellen Sie eine aktive ausgehende Verbindung zu [!DNL Google Cloud Storage] her, um Datendateien aus Adobe Experience Platform regelmäßig in Ihre eigenen Behälter zu exportieren. Dieses neue Ziel bietet eine verbesserte Dateiexportfunktion und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL Amazon S3] Aktualisieren](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Aktualisierung von   | Mit dieser Aktualisierung bietet das Ziel erweiterte Dateiexportfunktionen und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL Azure Blob] Aktualisieren](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Aktualisierung von   | Mit dieser Aktualisierung bietet das Ziel erweiterte Dateiexportfunktionen und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL SFTP] Aktualisieren](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Aktualisierung von   | Mit dieser Aktualisierung bietet das Ziel erweiterte Dateiexportfunktionen und unterstützt [!BADGE Beta]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] -Verbindung](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Aktualisierung von   | Die [!DNL Adobe Campaign Managed Services] Die Integration mit Adobe Experience Platform unterstützt jetzt unterschiedliche Typen der Zielgruppensynchronisierung. Verwenden Sie das Steuerelement Synchronisierungstyp auswählen , um zu bestimmen, ob Sie Zielgruppen in Adobe Campaign oder Zielgruppen und deren Profilattribute exportieren möchten. <br> ![Neu Auswahl des Synchronisierungstypselektors markiert.](/help/release-notes/2023/assets/acms-destination-export-type.png "Neu Auswahl des Synchronisierungstypselektors markiert."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

Das Update und die allgemeine Verfügbarkeit der sechs oben genannten Cloud-Speicher-Ziele bieten die folgenden Funktionen:

- Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- Anpassungsfähigkeit der [Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md).


**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Es wurde ein Problem mit dem Salesforce-Marketing Cloud-Ziel (API) behoben, bei dem im Zuordnungsschritt nicht alle verfügbaren Zielattribute von Salesforce zurückgegeben wurden. Es gibt jetzt eine [Obergrenze von 2000 Zielattributen](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) aus Salesforce , die angezeigt werden kann.
- Es wurde ein Problem mit dem Microsoft Dynamics 365-Ziel behoben. Das Ziel unterstützt jetzt das regionale Routing von Daten über die [Regionsauswahl](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate), damit Sie Ihre Datenexporte entsprechend der Region weiterleiten können, in der Ihr Unternehmen im Microsoft-Ökosystem bereitgestellt wird. <br> ![Neuer Regionsselektor hervorgehoben.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "Neuer Regionsselektor hervorgehoben."){width="100" zoomable="yes"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Abfrage-Service {#query-service}

Der Abfrage-Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Erweiterter Abfrage-Editor-Umschalter | Der erweiterte Umschalter &quot;Abfrage-Editor&quot;bietet bessere Barrierefreiheit und Unterstützung für mehrere Designs. Erweiterte Editor-Einstellungen ermöglichen die Aktivierung von dunklen oder hellen Designs. Weitere Informationen finden Sie in der [Dokumentation](../../query-service/ui/user-guide.md#enhanced-editor-toggle). |
| Aliasname für berechnete Statistiken | Sie können jetzt einen Aliasnamen angeben, um die Ergebnisse Ihrer in Ihren berechneten Statistiken in SQL-Abfragen beschreibend zu referenzieren. Informationen zu diesem und anderen Aktualisierungen des Befehls COMPUTE STATISTICS finden Sie in der Dokumentation . Weitere Informationen finden Sie in der [Dokumentation](../../query-service/essential-concepts/dataset-statistics.md#alias-name). |

{style="table-layout:auto"}

Weitere Informationen über Query Service finden Sie im Abschnitt [Query Service – Übersicht](../../query-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht Ihnen das Segmentieren von Daten, die in gespeichert sind. [!DNL Experience Platform] , die sich auf Einzelanwender (z. B. Kunden, Interessenten, Benutzer oder Organisationen) in Zielgruppen bezieht. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile] Daten. Diese Zielgruppen werden zentral konfiguriert und verwaltet in [!DNL Platform]und für jede Adobe leicht zugänglich sind.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zielgruppe  Portal | Audience Portal bietet ein neues Browsing-Erlebnis für den Zugriff auf, die Erstellung und die Verwaltung von Zielgruppen in Adobe Experience Platform. In Audience Portal können Sie Platform-generierte und extern generierte Zielgruppen anzeigen, Ihre Arbeitseffizienz durch Filtern, Ordner und Tags verbessern, Platform-generierte Zielgruppen erstellen und extern generierte Zielgruppen über CSV-Dateien importieren. Weitere Informationen zu Audience Portal finden Sie im [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md). |
| Zielgruppenkomposition | Die Zielgruppenkomposition bietet einen benutzerfreundlichen Arbeitsbereich zum Erstellen und Bearbeiten von Zielgruppen mithilfe von Bausteinen, die zur Darstellung verschiedener Aktionen verwendet werden. Weitere Informationen zur Zielgruppenkomposition finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](../../segmentation/ui/audience-composition.md). |

Weitere Informationen unter [!DNL Segmentation Service], lesen Sie bitte die [Segmentierungsübersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | Sie können jetzt die [[!DNL SAP Commerce] source](../../sources/connectors/ecommerce/sap-commerce.md) , um Abrechnungsdaten für Abonnements von Ihrem [!DNL SAP Commerce] -Konto in die Experience Platform. |
| Unterstützung für [!DNL Phoenix] | Sie können jetzt die [[!DNL Phoenix] source](../../sources/connectors/databases/phoenix.md) Daten von [!DNL Phoenix] Datenbank zu Experience Platform. |
| Authentifizierungsaktualisierungen für [!DNL Salesforce] und [!DNL Salesforce Service Cloud] | Sie können jetzt die API-Version Ihrer [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) und [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) Quelle bei der Authentifizierung eines neuen Kontos mit der Experience Platform-Benutzeroberfläche oder der [!DNL Flow Service] API. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
