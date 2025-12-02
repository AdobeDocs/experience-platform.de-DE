---
title: Adobe Experience Platform – Versionshinweise April 2024
description: Versionshinweise April 2024 für Adobe Experience Platform.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1893'
ht-degree: 25%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 30. April 2024**

>[!TIP]
>
>Verwenden Sie das [Adobe Experience Platform-Glossar](/help/landing/glossary.md) um sich mit der in Real-Time Customer Data Platform und Adobe Experience Platform verwendeten Terminologie vertraut zu machen. Wenn Sie einen bestimmten Begriff, den Sie suchen, nicht finden können, verwenden Sie die Feedback-Optionen auf der Seite, um anzufordern, dass neue Begriffe dem Glossar hinzugefügt werden.

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Identity Service](#identity-service)
- [Überwachung](#monitoring)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Real-Time Customer Data Platform B2B-Einblicke | Informieren Sie sich anhand der vorkonfigurierten [Real-Time CDP B2B-Dateneinblicke zu Accounts und Opportunities](../../dashboards/insights/account-profiles.md) damit Sie Ihre Daten besser verstehen und in Ihre Geschäftsentscheidungen einfließen können. Sie können auch [eigene Einblicke mithilfe des Real-Time CDP B2B-Datenmodells erstellen](../../dashboards/data-models/cdp-insights-data-model-b2c.md) um Ihre Daten zu visualisieren und zu untersuchen und Ihre benutzerdefinierten Visualisierungen in Ihrem Dashboard zu speichern. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an die Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterungen | [!DNL Acxiom Anonymous Visitor Insights] Tags-Erweiterung | Finden Sie heraus, woher Ihre Website-Besucher mit [!DNL Acxiom's Visitor Insights] kommen. Durch die Verwendung der Geo-IP-Lookup-Technologie kann Acxiom den Speicherort anonymer Browser ermitteln. Nach der Identifizierung liefert eine Suche in der organisierten Datenbank zusätzliche Einblicke, die an den Browser zurückgesendet werden. Ersteller von Inhalten können dadurch ihre Inhalte an diese Datenpunkte anpassen und Besuchern ein personalisierteres und ansprechenderes Erlebnis bieten, auch wenn sie anfangs als Fremde da waren. |
| Datenströme | [Edge Network-Bot-Erkennung](../../datastreams/bot-detection.md) | Traffic, der von nicht-menschlichen Entitäten stammt, wie z. B. automatisierten Programmen, Web-Scraptern, Spinnen, skriptgesteuerten Scannern, kann es schwieriger machen, Ereignisse zu identifizieren, die von menschlichen Besuchern stammen. Dieser Traffic kann sich negativ auf wichtige Geschäftsmetriken auswirken und zu falschen Traffic-Berichten führen. <br>Mit der Bot-Erkennung können Sie Ereignisse identifizieren, die von der [Adobe Experience Platform-Datenerfassung](/help/collection/home.md) generiert wurden, als von bekannten Spiders und Bots. Durch die Konfiguration der Bot-Erkennung für Ihre Datenströme können Sie bestimmte IP-Adressen, IP-Bereiche und Anfrage-Header identifizieren, die Sie als Bot-Ereignisse klassifizieren möchten. <br> Identifizierung des Bot-Traffics kann eine genauere Messung der Benutzeraktivität auf Ihrer Site oder in Ihrer Mobile App ermöglichen. |
| Mobile SDK | Hauptversion | Neue Hauptversionen der Mobile SDK wurden für die folgenden Plattformen veröffentlicht: iOS Mobile Core 5.x und kompatible iOS Extensions, Android Mobile Core 3.x und kompatible Android Extensions, React Native Core 6.x und kompatible React Native Extensions, Flutter Core 4.x und kompatible Flutter Extensions. Diese Versionen bieten mehrere neue Funktionen und Verbesserungen, einschließlich der Unterstützung in Android SDK für Jetpack Compose, Unterstützung für Adobe Journey Optimizer Code-basierte Erlebnisse und allgemeine Verfügbarkeit der Adobe Journey Optimizer Messaging-Erweiterung für Flutter. Weitere Versionshinweise finden Sie unter [Versionshinweise zu Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | Datenschutz | Aufgrund der Richtlinienaktualisierung von Apple, die am 1. Mai 2024 beginnt, müssen Entwicklerinnen und Entwickler neue Datenschutzfunktionen implementieren, um an App Store übermitteln zu können. Alle Adobe-Kunden, die die mobile SDK verwenden, müssen ein Upgrade auf Version 5.x der SDK durchführen, wenn sie nach dem 1. Mai die App Store-Genehmigung erhalten möchten. |
| Roku SDK | Roku SDK | Die erste Hauptversion des Roku SDK wurde veröffentlicht, mit Unterstützung für die Streaming-Medien für den Experience Platform Edge Network. |
| Tags und Ereignisweiterleitung | Produktinterne Anleitung | Experience Platform [Tags](../../tags/home.md) und [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) bieten eine neue Reihe von Erlebnissen, die Ihnen dabei helfen, schnell loszulegen und eine schnelle Wertschöpfungszeit zu erzielen. Zu diesen Erlebnissen gehören neue Onboarding-Bildschirme, produktinterne Tutorials und QuickInfos. <br>![Ereignisweiterleitung mit hervorgehobener produktinterner Anleitung.](../2024/assets/april/event-forwarding.png "Der Schemaeditor mit den hervorgehobenen Feldern Typ und Zuordnungswerttyp."){width="100" zoomable="yes"}<br> |
| Web SDK | Vereinfachte Web-SDK-Einführung für Audience Manager-Kunden | Mehrere Web-SDK-Updates vereinfachen jetzt die Übernahme von Web SDK ohne Verwendung des Experience-Datenmodells (XDM) für Experience Cloud-Lösungen wie Audience Manager, Analytics und Target. Weitere Informationen zur Verwendung von Audience Manager Web SDK erhalten Sie in den folgenden Handbüchern: <ul><li><a href="https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Aktualisieren Sie Ihre Datenerfassungsbibliothek für Audience Manager von der Audience Manager-Tag-Erweiterung auf die Web-Tag-Erweiterung für SDK</li><li><a href="https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Aktualisieren Sie Ihre Datenerfassungsbibliothek für Audience Manager von der AppMeasurement JavaScript-Bibliothek auf die Web SDK JavaScript-Bibliothek.</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](/help/collection/js/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](/help/collection/js/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/de/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Weitere Informationen zu Datenerfassungen finden Sie unter [Datenerfassung - Übersicht](../../collection/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| `isRequired` Parameter jetzt für verschachtelte Kundendatenfelder in Destination SDK verfügbar | Beim Konfigurieren eines Ziels in Destination SDK können Sie jetzt [verschachtelte Kundendatenfelder nach Bedarf festlegen](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Auf diese Weise können Benutzerinnen und Benutzer, die Ihr Ziel einrichten, mit ihrem Aktivierungsfluss erst fortfahren, wenn sie einen Wert für dieses Feld auswählen. |
| Beim Einrichten eines Adobe Target-Ziels mit Web SDK ist die Segmentierung durch Edge nicht mehr erforderlich | Beim Konfigurieren eines [Adobe Target-Ziels](/help/destinations/catalog/personalization/adobe-target-connection.md) mit Web SDK musste der Datenstrom zuvor für die Personalisierung und Edge-Segmentierung aktiviert werden. Die Anforderung, dass der Datenstrom für die Edge-Segmentierung aktiviert sein muss [wurde jetzt entfernt](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Beachten Sie, dass Sie bei diesem Integrationsmuster nur von einer Untergruppe von Personalisierungs-Anwendungsfällen profitieren können, wenn Sie Adobe Target mit Real-Time CDP verwenden. Lesen Sie mehr über die [Anwendungsfälle nach Integrationstyp aktiviert](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Mehrere Zielgruppen und Datensätze aus Aktivierungsflüssen entfernen | Sie können jetzt mehrere Zielgruppen und Datensätze aus Zielaktivierungsflüssen auswählen und entfernen. Weitere Informationen finden Sie [&#x200B; der &#x200B;](../../destinations/ui/destination-details-page.md#bulk-remove) „Zieldetails[&#x200B; und &#x200B;](../../destinations/ui/export-datasets.md)Datensatzexport . |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Identity Service {#identity-service}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Einstellung der `/orgs/{ORG}/`-Endpunkte in der API | Die folgenden Endpunkte in der [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) werden nicht mehr unterstützt:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Sie können die `/idnamespace/identities`- und `/idnamespace/identities/{ID}`-Endpunkte verwenden, um dieselben Aufgaben auszuführen und entweder alle Namespaces in einer Organisation oder einen bestimmten Namespace in einer Organisation abzurufen. |

{style="table-layout:auto"}

Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](../../identity-service/home.md).

## Überwachung {#monitoring}

Verwenden Sie das Überwachungs-Dashboard in der Experience Platform-Benutzeroberfläche, um das Journey Ihrer Daten aus Quellen, Identity Service, Echtzeit-Kundenprofil, Zielgruppen und Zielen zu überwachen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Überwachen der Dashboard-Erweiterung | Sie können jetzt das Überwachungs-Dashboard für verschiedene Datentypen basierend auf Ihrem geschäftlichen Anwendungsfall verwenden. Verwenden Sie das Überwachungs-Dashboard, um Datentypaktivitäten für Personen, Konten und Interessenten in Quellen, Audiences und Zielen zu überwachen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Handbuch unter [Verwenden des Überwachungs-Dashboards](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Abfragequarantäne | Fehlgeschlagene Abfrageausführungen automatisch isolieren, um Unterbrechungen zu verhindern und eine konsistente Leistung zu gewährleisten. Weitere Informationen finden Sie in [&#x200B; Dokumentation &#x200B;](../../query-service/ui/query-schedules.md#quarantine)Abfragequarantäne“. |
| Abfrage abbrechen | Übernehmen Sie die Kontrolle über die Ausführung von Abfragen und verbessern Sie Ihre Produktivität, indem Sie langwierige Abfragen abbrechen. Weitere Informationen finden Sie in der Dokumentation [Abfrage abbrechen](../../query-service/ui/user-guide.md#cancel-query) . |
| Warnhinweise für geplante Abfragen | Bleiben Sie mit proaktiven Benachrichtigungen auf dem Laufenden, während Sie Abfragen planen, um ein effizientes und zeitnahes Aufgabenmanagement zu gewährleisten. Sie können [&#x200B; Warnhinweise entweder beim Erstellen einer Abfrage oder &#x200B;](../../query-service/ui/query-schedules.md#alerts-for-query-status) Inline-Aktionen für vorhandene geplante Abfragen abonnieren. Weitere Informationen finden [&#x200B; in der Dokumentation &#x200B;](../../query-service/ui/monitor-queries.md#alert-subscription) Abonnieren von Warnhinweisen mit Inline-Aktionen . |
| Verbesserte Navigation bei geplanten Abfragen | Einfaches Navigieren zwischen Abfragevorlagen und geplanten Ausführungen für mehr Produktivität. Weitere Informationen finden Sie in [&#x200B; Dokumentation unter Anzeigen geplanter &#x200B;](../../query-service/ui/query-schedules.md#scheduled-query-runs) . |
| Erweiterte Abfrageausgabe | Greifen Sie in der Konsole auf bis zu 500 Zeilen mit Abfrageergebnissen zu, um Ihre Daten tiefer zu analysieren. Weitere Informationen finden Sie in der Dokumentation [Ergebnisanzahl](../../query-service/ui/user-guide.md#result-count) . |
| Veraltete Einstellung des Abfrage-Editors | Seit dem 30. April 2024 ist der erweiterte Abfrage-Editor zum Standard-Editor für alle Benutzer geworden. Der alte Editor wird am 24. Mai 2024 eingestellt und ist nicht mehr verfügbar. Weitere Informationen finden [&#x200B; im Benutzerhandbuch zum Abfrage](../../query-service/ui/user-guide.md)Editor . |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Sandbox-Werkzeuge](../../sandboxes/ui/sandbox-tooling.md) | Verwenden Sie die Sandbox[Tools , um &#x200B;](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) unterstützten Objekttypen in ein vollständiges Sandbox-Paket zu exportieren, und [&#x200B; das Paket dann &#x200B;](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) verschiedene Sandboxes zu importieren, um Objektkonfigurationen zu replizieren. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Experience Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Status des Zielgruppen-Lebenszyklus | Der Status des Zielgruppen-Lebenszyklus wurde optimiert, um das Lebenszyklus-Management zu vereinfachen. Weitere Informationen zu diesen Lebenszyklusstatus finden Sie in den häufig gestellten [&#x200B; zum Segmentierungs-Service](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Neue Quellen**

| Neue Quellen | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Verwenden Sie die [[!DNL PathFactory] Quelle](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md), um Ihre Besucher-, Sitzungs- und Seitenansichtsdaten aus [!DNL PathFactory] in Experience Platform zu integrieren. Informationen zu den ersten [[!DNL PathFactory]  finden &#x200B;](../../sources/connectors/marketing-automation/pathfactory.md) im Abschnitt „Übersicht“. |
| [!DNL Teradata Vantage] | Verwenden Sie die [[!DNL Teradata Vantage] Quelle](../../sources/tutorials/ui/create/databases/teradata-vantage.md) um Daten aus hybriden Multi-Cloud-Umgebungen in Experience Platform aufzunehmen. Informationen zu den ersten [[!DNL Teradata Vantage]  finden &#x200B;](../../sources/connectors/databases/teradata-vantage.md) im Abschnitt „Übersicht“. |

{style="table-layout:auto"}

**Neue und aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der IP-Adressen für die Zulassungsauflistung in VA7 | Die folgenden IP-Adressen wurden der Liste der IP-Adressen hinzugefügt, die Ihrer Zulassungsliste für VA7 (Nordamerika) hinzugefügt werden sollen: <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Eine umfassende Liste der IP-Adressen, die Sie Ihrer Zulassungsliste hinzufügen können, finden Sie im Dokument [Zulassungsliste von IP-Adressen](../../sources/ip-address-allow-list.md). |
| Unterstützung neuer Authentifizierungstypen mit der [!DNL Azure Event Hubs] | Sie können Ihre [!DNL Event Hubs] jetzt entweder über [!DNL Azure Active Directory Authentication] oder [!DNL Scoped Azure Active Directory Authentication] mit Experience Platform verbinden. Lesen Sie das Handbuch unter [Verbinden [!DNL Event Hubs] mit Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md), um weitere Informationen zu erhalten. |
| Aktualisierungen [!DNL Data Landing Zone] Abrufen von Anmeldeinformationen | Sie können jetzt die rechte Leiste im Arbeitsbereich „Quellen“ verwenden, um Ihre [!DNL Data Landing Zone] abzurufen. Sie können jetzt auch die rechte Leiste verwenden, um Ihre Anmeldeinformationen zu aktualisieren. Weitere Informationen finden [[!DNL Data Landing Zone]  im &#x200B;](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) zur Benutzeroberfläche . |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
