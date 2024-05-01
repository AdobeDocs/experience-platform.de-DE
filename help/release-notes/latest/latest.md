---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise April 2024 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4ec4335d19695e8d6e26390358356dedd048594e
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 22%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 30. April 2024**

>[!TIP]
>
>Verwenden Sie die [Glossar zu Adobe Experience Platform](/help/landing/glossary.md) , um sich mit der in Real-time Customer Data Platform und Adobe Experience Platform verwendeten Terminologie vertraut zu machen. Wenn Sie einen bestimmten Begriff, den Sie suchen, nicht finden können, verwenden Sie die Feedback-Optionen auf der Seite, um die Hinzufügung neuer Begriffe zum Glossar anzufordern.

Aktualisierungen vorhandener Funktionen im Experience Platform:

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

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Real-time Customer Data Platform B2B-Einblicke | Erfahren Sie mehr über vorkonfigurierte Real-Time CDP B2B-Dateneinblicke zu Konten und Möglichkeiten, Ihnen beim Verständnis Ihrer Daten und bei der Information Ihrer Geschäftsentscheidungen zu helfen. Sie können auch mithilfe des B2B-Datenmodells von Real-Time CDP eigene Einblicke erstellen, um Ihre Daten zu visualisieren und zu untersuchen und Ihre benutzerdefinierten Visualisierungen in Ihrem Dashboard zu speichern. |

{style=“table-layout:auto”}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie clientseitige Kundenerlebnisdaten erfassen und an das Experience Platform-Edge Network senden können, wo sie angereichert, transformiert und an Adobe- oder Nicht-Adobe-Ziele verteilt werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Insights | [!DNL Acxiom] Anonyme Besuchereinblicke | Erfahren Sie, woher Ihre Website-Besucher kommen. [!DNL Acxiom's] Besuchereinblicke. Durch die Verwendung der Geo-IP-Suchtechnologie bestimmen wir den Standort anonymer Browser. Nach der Identifizierung liefert eine Schnellsuche in unserer organisierten Datenbank zusätzliche Einblicke, die an den Browser zurückgesendet werden. Für Ersteller von Inhalten bedeutet dies eine einmalige Gelegenheit, ihren Inhalt an diese Datenpunkte anzupassen und so ein personalisierteres und ansprechenderes Erlebnis für Besucher zu bieten, selbst wenn sie als Fremde begannen. |
| Datenströme | [Edge Network-Bot-Erkennung](../../datastreams/bot-detection.md) | Traffic, der von unmenschlichen Entitäten stammt, wie z. B. automatisierten Programmen, Webcrapers, Spider, Skriptscannern, kann es erschweren, Ereignisse von Besuchern zu identifizieren. Dieser Traffic-Typ kann sich negativ auf wichtige Geschäftsmetriken auswirken und zu falschen Traffic-Berichten führen. <br>Mit der Bot-Erkennung können Sie Ereignisse identifizieren, die von der [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) und [[!DNL Server API]](../../server-api/overview.md) als von bekannten Spiders und Bots generiert wurde. Durch die Konfiguration der Bot-Erkennung für Ihre Datenspeicher können Sie bestimmte IP-Adressen, IP-Bereiche und Anforderungsheader identifizieren, die Sie als Bot-Ereignisse klassifizieren möchten. <br> Die Identifizierung des Bot-Traffics kann Ihnen eine präzisere Messung der Benutzeraktivität auf Ihrer Site oder in Ihrer mobilen Anwendung ermöglichen. |
| Mobile SDK | Hauptversion | Für die folgenden Plattformen wurden neue Hauptversionen des Mobile SDK veröffentlicht: iOS Mobile Core 5.x und kompatible iOS-Erweiterungen, Android Mobile Core 3.x und kompatible Android-Erweiterungen, React Native Core 6.x und kompatible React Native Extensions, Flutter Core 4.x und kompatible Flutter-Erweiterungen. Diese Version bietet verschiedene neue Funktionen und Verbesserungen, einschließlich Unterstützung im Android SDK für Jetpack Compose, Unterstützung für code-basierte Adobe Journey Optimizer-Erlebnisse und allgemeine Verfügbarkeit der Adobe Journey Optimizer Messaging-Erweiterung für Flutter. Weitere Informationen zu den Versionshinweisen finden Sie unter [Versionshinweise zum Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | Datenschutz    | Aufgrund der Richtlinienaktualisierung von Apple müssen Entwickler ab dem 1. Mai 2024 neue Datenschutzfunktionen implementieren, um die Informationen an App Store übermitteln zu können. Alle Adobe-Kunden, die das Mobile SDK verwenden, müssen ein Upgrade auf Version 5.x des SDK durchführen, wenn sie nach dem 1. Mai die App Store-Genehmigung erhalten möchten. |
| Roku SDK | Roku SDK | Die erste Hauptversion des Roku-SDK wurde mit Unterstützung für die Streaming-Medien für das Platform-Edge Network veröffentlicht. |
| Tags und Ereignisweiterleitung | Produktinterne Anleitung | Experience Platform [Tags](../../tags/home.md) und [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) bieten eine neue Reihe von Erlebnissen, die Ihnen dabei helfen, schnell zu beginnen und eine schnelle Amortisierungszeit zu erreichen. Zu diesen Erlebnissen gehören neue Onboarding-Bildschirme, produktinterne Tutorials und QuickInfos. <br>![Ereignisweiterleitung mit hervorgehobenen produktinternen Anleitungen.](../2024/assets/april/event-forwarding.png "Der Schemaeditor mit den Feldern Typ und Typ Zuordnungs-Wert hervorgehoben."){width="100" zoomable="yes"}<br> |
| Web SDK | Vereinfachtes Web SDK für Audience Manager-Kunden | Mehrere Web SDK-Updates vereinfachen jetzt die Übernahme des Web SDK, ohne Experience-Datenmodell (XDM) für Experience Cloud-Lösungen wie Audience Manager, Analytics und Target zu verwenden. Weitere Informationen zur Übernahme des Audience Manager Web SDK finden Sie in den folgenden Handbüchern: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Aktualisieren Sie Ihre Datenerfassungsbibliothek für den Audience Manager von der Audience Manager-Tag-Erweiterung auf die Web SDK-Tag-Erweiterung</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Aktualisieren Sie Ihre Datenerfassungsbibliothek für Audience Manager aus der JavaScript-AppMeasurement-Bibliothek in die JavaScript-Bibliothek des Web SDK.</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Weitere Informationen zu Datenerfassungen finden Sie im Abschnitt [Datenerfassung - Übersicht](../../collection/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| `isRequired` -Parameter jetzt für verschachtelte Kundendatenfelder in Destination SDK verfügbar | Beim Konfigurieren eines Ziels in Destination SDK können Sie jetzt [stellen Sie verschachtelte Kundendatenfelder nach Bedarf ein.](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Auf diese Weise können Benutzer, die Ihr Ziel einrichten, ihren Aktivierungsfluss erst fortsetzen, wenn sie einen Wert für dieses Feld auswählen. |
| Die Edge-Segmentierung ist bei der Einrichtung eines Adobe Target-Ziels mit dem Web SDK nicht mehr erforderlich. | Bisher wurde beim Konfigurieren von [Adobe Target-Ziel](/help/destinations/catalog/personalization/adobe-target-connection.md) mit Web SDK musste der Datastream für die Personalisierung und Kantensegmentierung aktiviert werden. Die Anforderung, dass der Datastream für die Kantensegmentierung aktiviert werden muss [wurde entfernt](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Beachten Sie, dass dieses Integrationsmuster nur Ihnen ermöglicht, bei der Verwendung von Adobe Target mit Real-Time CDP von einer Untergruppe von Anwendungsfällen zur Personalisierung zu profitieren. Mehr über [Anwendungsfälle, die vom Integrationstyp aktiviert wurden](/help/destinations/catalog/personalization/adobe-target-connection.md#parameters). |
| [!BADGE Beta]{type=Informative} Entfernen Sie mehrere Zielgruppen und Datensätze aus Aktivierungsabläufen | Sie können jetzt mehrere Zielgruppen und Datensätze auswählen und aus den Zielaktivierungsflüssen entfernen. Siehe [Zieldetails](../../destinations/ui/destination-details-page.md#bulk-remove) und [Datensatzexport](../../destinations/ui/export-datasets.md) Dokumentation für weitere Details. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Identity Service {#identity-service}

Verwenden Sie Adobe Experience Platform Identity Service, um eine umfassende Übersicht über Ihre Kunden und deren Verhalten zu erstellen, indem Sie Identitäten geräteübergreifend zusammenführen und so effektive, persönliche digitale Erlebnisse in Echtzeit bereitstellen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Einstellung der `/orgs/{ORG}/` -Endpunkte in der API | Die folgenden Endpunkte im [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) sind veraltet:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Sie können `/idnamespace/identities` und `/idnamespace/identities/{ID}` -Endpunkte zum Ausführen derselben Aufgaben und Abrufen entweder aller Namespaces in einer Organisation oder eines bestimmten Namespace in einer Organisation. |

{style="table-layout:auto"}

Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](../../identity-service/home.md).

## Überwachung {#monitoring}

Verwenden Sie das Monitoring-Dashboard in der Experience Platform-Benutzeroberfläche, um die Journey Ihrer Daten aus Quellen, Identitätsdienst, Echtzeit-Kundenprofil, Zielgruppen und Zielen zu überwachen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Dashboard-Erweiterung überwachen | Sie können jetzt das Monitoring-Dashboard für verschiedene Datentypen basierend auf Ihrem geschäftlichen Anwendungsfall verwenden. Verwenden Sie das Monitoring-Dashboard, um Aktivitäten vom Typ Person, Konto und Interessent in Quellen, Zielgruppen und Zielen zu überwachen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Handbuch unter [über das Monitoring-Dashboard](../../dataflows/ui/monitor.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Abfrage-Quarantäne | Automatische Isolierung fehlgeschlagener Abfrageausführungen, um Unterbrechungen zu vermeiden und eine konsistente Leistung zu gewährleisten. |
| Abfrage abbrechen | Übernehmen Sie die Kontrolle über die Ausführung von Abfragen und verbessern Sie Ihre Produktivität, indem Sie langwierige Abfragen abbrechen. |
| Warnhinweise zu geplanten Abfragen | Halten Sie sich während der Planung von Abfragen über proaktive Benachrichtigungen auf dem Laufenden, um eine effiziente und zeitnahe Aufgabenverwaltung zu gewährleisten. Sie können Warnhinweise entweder bei der Erstellung einer Abfrage oder bei der Verwendung der Inline-Aktionen für bestehende geplante Abfragen abonnieren. |
| Verbesserte geplante Abfragennavigation | Für eine höhere Produktivität können Sie einfach zwischen Abfragevorlagen und geplanten Ausführungen navigieren. |
| Erweiterte Abfrageausgabe | Greifen Sie in der Konsole auf bis zu 500 Zeilen mit Abfrageergebnissen zu, um Ihre Daten eingehender zu analysieren. |
| Veraltete Abmeldung des Abfrage-Editors | Ab dem 30. April 2024 ist der erweiterte Abfrage-Editor für alle Benutzer zum Standardeditor geworden. Der alte Editor wird vom 30. Mai 2024 eingestellt und ist nicht mehr zur Verwendung verfügbar. |

{style=“table-layout:auto”}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Sandbox-Werkzeuge](../../sandboxes/ui/sandbox-tooling.md) | Verwenden der Sandbox-Tools für [export](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) alle unterstützten Objekttypen in ein vollständiges Sandbox-Paket einschließen und [importieren](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) das -Paket über verschiedene Sandboxes hinweg, um Objektkonfigurationen zu replizieren. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie im Abschnitt [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Status des Zielgruppen-Lebenszyklus | Der Status des Zielgruppen-Lebenszyklus wurde optimiert, um die Lebenszyklusverwaltung zu vereinfachen. Weitere Informationen zu diesen Lebenszyklusstatus finden Sie im Abschnitt [Häufig gestellte Fragen zum Segmentierungsdienst](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen im Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern zu erfassen.

**Neue Quellen**

| Neue Quellen | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Verwenden Sie die [[!DNL PathFactory] source](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) zur Integration Ihrer Besucher-, Sitzungs- und Seitenansichtsdaten aus [!DNL PathFactory] auf Experience Platform. Lesen Sie die [[!DNL PathFactory] Übersicht](../../sources/connectors/marketing-automation/pathfactory.md) für Informationen zu den ersten Schritten. |
| [!DNL Teradata Vantage] | Verwenden Sie die [[!DNL Teradata Vantage] source](../../sources/tutorials/ui/create/databases/teradata-vantage.md) , um Daten von hybriden Multi-Cloud-Umgebungen auf Experience Platform zu erfassen. Lesen Sie die [[!DNL Teradata Vantage] Übersicht](../../sources/connectors/databases/teradata-vantage.md) für Informationen zu den ersten Schritten. |

{style="table-layout:auto"}

**Neue und aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen von IP-Adressen für die Zulassungsauflistung in VA7 | Die folgenden IP-Adressen wurden zur Liste der IP-Adressen hinzugefügt, um sie zu Ihrer Zulassungsliste für VA7 (Nordamerika) hinzuzufügen: <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Eine umfassende Liste der zu Ihrer Zulassungsliste hinzuzufügenden IP-Adressen finden Sie im Abschnitt [Dokument zur Zulassungsliste von IP-Adressen](../../sources/ip-address-allow-list.md). |
| Unterstützung neuer Authentifizierungstypen mit der [!DNL Azure Event Hubs] source | Sie können jetzt Ihre [!DNL Event Hubs] -Quelle zu Experience Platform mithilfe von [!DNL Azure Active Directory Authentication] oder [!DNL Scoped Azure Active Directory Authentication]. Lesen Sie das Handbuch unter [Verbindung [!DNL Event Hubs] auf Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) für weitere Informationen. |
| Aktualisierungen für [!DNL Data Landing Zone] Anmeldedaten abrufen | Sie können jetzt die rechte Leiste im Arbeitsbereich &quot;Quellen&quot;verwenden, um Ihre [!DNL Data Landing Zone] Anmeldedaten. Sie können jetzt auch die rechte Leiste verwenden, um Ihre Anmeldedaten zu aktualisieren. Lesen Sie die [[!DNL Data Landing Zone] UI-Handbuch](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) für weitere Informationen. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
