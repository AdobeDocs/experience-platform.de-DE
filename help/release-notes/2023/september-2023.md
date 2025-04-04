---
title: Adobe Experience Platform – Versionshinweise, September 2023
description: Versionshinweise September 2023 zu Adobe Experience Platform.
exl-id: ff7fb0c1-6941-4339-8648-58f9b9e9a91f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 28%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Freitag, 28. September 2023**

Neue Funktionen in Adobe Experience Platform:

- [Berechnete Attribute](#computed-attributes)

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Warnhinweise](#alerts)
- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection)
- [Data Governance](#data-governance)
- [Datenhygiene](#hygiene)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Abfrage-Service](#query-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Berechnete Attribute {#computed-attributes}

Berechnete Attribute ermöglichen es, Ereignisdaten über eine intuitive Benutzeroberfläche einfach in Profilattribute zusammenzufassen, um die verhaltensbasierte Segmentierung, Personalisierung und Aktivierung zu verbessern. Mit dieser Funktion können Sie berechnete Attribute im Self-Service-Modus erstellen, verwalten und in der Segmentierung, in Real-Time CDP-Zielen oder in Adobe Journey Optimizer verwenden. Darüber hinaus vereinfachen berechnete Attribute die Segmentierung und das Journey von Workflows, damit relevante Erlebnisse nahtlos bereitgestellt werden können. Weitere Informationen zu berechneten Attributen finden Sie unter [Berechnete Attribute - Übersicht](../../profile/computed-attributes/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Registerkarte „Warnhinweisverlauf“ | Die Registerkarte [!UICONTROL Warnhinweise] enthält jetzt alle Ereignisse, einschließlich Verzögerungen, Starts, Erfolg und Fehler. Weitere Informationen zur Registerkarte „Verlauf[ finden ](../../observability/alerts/ui.md) in der Dokumentation zur Warnhinweis-Benutzeroberfläche . |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie in der [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards], in denen basierend auf täglichen Schnappschüssen wichtige Informationen zu den Unternehmensdaten dargestellt werden.

| Funktion | Beschreibung |
| --- | --- |
| [Verbesserung des Lizenznutzungs-Dashboards](../../dashboards/guides/license-usage.md) | Behalten Sie die Kontrolle über Ihre Lizenzvereinbarungen mit verbesserten Berichten und Visualisierungen von Schlüsselmetriken zur Lizenznutzung Ihres Unternehmens bei. Diese Verbesserungen bieten einen hohen Grad an Granularität gegenüber Ihren Lizenznutzungsmetriken für alle Experience Platform-Produkte, die Sie erworben haben. |

{style="table-layout:auto"}

Weitere Informationen zum Lizenznutzungs-Dashboard finden Sie unter [Lizenznutzungs-Dashboard - Übersicht](../../dashboards/guides/destinations.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Datenströme | Unterstützung der Gerätesuche | Beim Konfigurieren eines Datenstroms können Sie jetzt die Ebene der Gerätesuchinformationen auswählen, die erfasst werden sollen. Gerätesuchinformationen enthalten Daten zu Gerät, Hardware, Betriebssystem und Browser, die für die Interaktion mit Ihrer Seite verwendet werden. <br> Gerätesuchinformationen können nicht zusammen mit Benutzeragenten- und Client-Hinweisen erfasst werden. Wenn Sie sich für die Erfassung von Geräteinformationen entscheiden, wird die Erfassung von Benutzeragenten- und Client-Hinweisen deaktiviert und umgekehrt. Alle Gerätesuchinformationen werden in der `xdm:device` Feldergruppe gespeichert. Weitere Informationen finden Sie in der Dokumentation unter [ von Datenströmen](../../datastreams/configure.md#geolocation-device-lookup). |
| Erweiterungen | API-Erweiterung für [!DNL TikTok]-Web-Ereignisse | Mit der [[!DNL TikTok] Web Events API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api)-Erweiterung können Sie die in Adobe Experience Platform Edge Network erfassten Daten nutzen und in Form von Server-seitigen Ereignissen mithilfe der [!DNL TikTok] Web Events API an [!DNL TikTok] senden. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie unter [Datenerfassung - Übersicht](../../tags/home.md).

## Data Governance {#data-governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffskontrolle für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Partner-Ökosystem-Kennzeichnungen für Drittanbieterdaten | Es sind neue Datennutzungskennzeichnungen für die Anreicherung und Interessentenakquise von Drittanbietern verfügbar. Weitere Informationen finden Sie in der [Dokumentation ](../../data-governance/labels/reference.md#partner) Partner-Ökosystem-Kennzeichnungen“. |

{style="table-layout:auto"}

Weitere Informationen zu Data Governance finden Sie im Abschnitt [Data Governance – Übersicht](../../data-governance/home.md).

## Datenhygiene {#hygiene}

Experience Platform bietet eine Reihe von Funktionen zur Datenhygiene, mit denen Sie Ihre gespeicherten Daten durch programmatische Löschungen der Datensätze von Privatkund*innen verwalten können. Mithilfe des Arbeitsbereichs [!UICONTROL Datenlebenszyklus] in der Benutzeroberfläche oder durch Aufrufe der Datenhygiene-API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet werden, aktualisiert werden, wenn falsche Daten korrigiert werden müssen, und gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} Löschen von Datensätzen (eingeschränkte Version) | Verwalten Sie Ihren Datenlebenszyklus in allen Datenspeichern, um Kundenverpflichtungen und Lizenzvereinbarungen mit erweiterten Funktionen für das Data Lifecycle Management in Adobe Experience Platform zu erfüllen: Automatisierte Gültigkeit von Datensätzen und Löschen von Datensätzen.<br>Mit der automatisierten Datensatzgültigkeit können Sie ganze Datensätze löschen und ein Datum und eine Uhrzeit für das Löschen des Datensatzes festlegen.<br>Mit dem Löschen von Datensätzen können Sie einzelne Verbraucherprofile löschen, indem Sie deren primäre Identitäten ansprechen. Sie können die primären Identitäten einzeln über die Benutzeroberfläche oder über den CSV-/JSON-Datei-Upload angeben. Weitere Informationen finden [ in der ](../../hygiene/ui/record-delete.md) zum Löschen von Datensätzen . |
| Datensatzgültigkeiten | Minimieren Sie Ihre Daten und behalten Sie die Kontrolle über Ihre Lizenzvereinbarungen mit automatisierter Datensatzgültigkeit. Verringern Sie das Datenvolumen, indem Sie ganze Datensätze löschen und ein Datum und eine Uhrzeit für das Löschen des Datensatzes festlegen. Weitere Informationen finden [ in der ](../../hygiene/ui/dataset-expiration.md) zur Datensatzgültigkeit . |

{style="table-layout:auto"}

Weitere Informationen zu den Datenhygiene-Funktionen von Experience Platform finden Sie im Abschnitt [Übersicht zur Datenhygiene](../../hygiene/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Neu | Aktivieren Sie Zielgruppen, die zuvor für die [!DNL LiveRamp] bei Premium-Publishern integriert wurden, über Mobilgeräte, Web, Display und vernetzte TV-Medien. <br> Nachdem Sie Zielgruppen über die Verbindung [LiveRamp - Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md) in Ihr [!DNL LiveRamp]-Konto integriert haben, verwenden Sie die neue [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md)-Verbindung, um die Zielgruppen für nachgelagerte Ziele zu aktivieren. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Neu | [[!DNL HubSpot]](https://www.hubspot.com) ist eine CRM-Plattform mit all der Software, Integrationen und Ressourcen, die Sie für die Verbindung von Marketing, Vertrieb, Content-Management und Kundendienst benötigen. Damit können Sie Ihre Daten, Teams und Kunden auf einer CRM-Plattform verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Aktualisiert | Es wurde Unterstützung für [!DNL Dynamics 365] benutzerdefinierte Feldpräfixe für benutzerdefinierte Felder hinzugefügt, die nicht innerhalb der Standardlösung in [!DNL Dynamics 365] erstellt wurden. Ein neues Eingabefeld, **[!UICONTROL Anpassungspräfix]**, wurde im Schritt [Ausfüllen der Zieldetails](#destination-details) hinzugefügt. |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Aktualisiert | Das Experience Cloud Audiences -Ziel ist jetzt allgemein verfügbar. Verwenden Sie dieses Ziel, um Zielgruppen von Real-Time CDP für Audience Manager und Adobe Analytics zu aktivieren. Sie benötigen eine Audience Manager-Lizenz, um Zielgruppen an Adobe Analytics zu senden. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Datenexporte in Real-Time CDP | Die [Datensatzexport](../../destinations/ui/export-datasets.md)-Funktion ist jetzt allgemein verfügbar. Sehen Sie [Welche Datensätze Sie basierend auf der von Ihnen erworbenen Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export)App exportieren können, und überprüfen Sie die [Leitplanken für den Export von Datensätzen](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Unterstützung für den Export von Objekten vom Typ Array | Exportieren Sie Arrays von primitiven Werten (Zeichenfolge, int oder boolesche Werte) als flache Schemadateien in Cloud-Speicher-Ziele. Weitere Informationen zur Funktion finden Sie in der [Dokumentation](../../destinations/ui/export-arrays-maps-objects.md). |
| Dynamische Dropdown-Selektoren in Destination SDK | Beim Erstellen eines Ziels über Destination SDK können Sie jetzt [dynamische Dropdown-Selektoren](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) verwenden, um die Felder einer Dropdown-Auswahl mit Werten zu füllen, die von einer API abgerufen werden. |

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Nutzen Sie die [Überwachungstransparenz](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations), die jetzt für Unternehmensziele ([HTTP-](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) und [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) auf der Datenfluss-Ausführungsebene verfügbar ist, um Aktivierungsmetriken und -status in der [Datenfluss-Detailansicht](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page) zu überwachen. Sie erhalten zusätzliche Informationen über Fehler-Codes und Meldungen zur Fehlerbehebung.
- Wenn Sie den Namen der Zielgruppen aktualisieren, die dem [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md) und anderen Zielen zugeordnet sind, die [Zielgruppen-Update-Vorlagen](../../destinations/destination-sdk/metadata-api/update-audience-template.md) verwenden, werden diese Namensänderungen jetzt nachgelagert im Ziel übernommen.

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Schnellaktionen zum Schema-Editor hinzugefügt | Der Arbeitsfläche des Schema-Editors wurden neue Schnellaktionen hinzugefügt. Sie können jetzt die JSON-Struktur kopieren oder das Schema direkt aus dem Editor löschen.<br>![Schnellaktionen im Schema-Editor.](../2023/assets/schema-editor-copy-json.png "Der Editor „Schemata“ mit hervorgehobenen Optionen „Mehr“ und „In JSON kopieren“."){width="100" zoomable="yes"} |
| Filtern von XDM-Ressourcen nach benutzerdefiniertem oder standardmäßigem Ersteller | Die Listen der verfügbaren Schemata, Feldergruppen, Datentypen und Klassen sind jetzt basierend auf ihrer Erstellungsmethode vorgefiltert. Auf diese Weise können Sie Ressourcen danach filtern, ob sie benutzerdefiniert erstellt oder von Adobe erstellt wurden.<br>![Die standardmäßigen und benutzerdefinierten Filter im Arbeitsbereich Schemata .](../2023/assets/standard-and-custom-classes.png "Der Arbeitsbereich „Schemata“ mit hervorgehobenen Standard- und benutzerdefinierten Filtern."){width="100" zoomable="yes"} <br> Weitere Informationen finden [ in der ](../../xdm/ui/resources/classes.md#filter.md) zum Erstellen und Bearbeiten von Ressourcen . |

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierter Workflow zur Schemaerstellung | Es wurde ein neuer Workflow zur Schemaerstellung implementiert, um den Prozess zu optimieren. <br> ![Die neue Benutzeroberfläche zur Schemaerstellung.](../2023/assets/schema-class-options.png "Auswahl „Neue Schemadetails“ hervorgehoben."){width="100" zoomable="yes"} <br> Weitere Informationen finden [ in der ](../../xdm/ui/resources/schemas.md#create) zur Schemaerstellung . |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Zurück]](https://github.com/adobe/xdm/pull/1773/files) | Die RMA (Return Merchandising Authorization). |
| Datentyp | [[!UICONTROL Rücksendung]](https://github.com/adobe/xdm/pull/1773/files) | Die Informationen des zurückgegebenen Artikels innerhalb der RMA (Return Merchandising Authorization). |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Erweiterung | [!UICONTROL AJO-Entitätsfelder] | Die [[!UICONTROL Markierung für Multi-Variante]](https://github.com/adobe/xdm/pull/1774/files) wurde [!UICONTROL AJO-] hinzugefügt, um anzugeben, ob die Variante eine Multi-Variante ist oder nicht. |
| Datentyp | [!UICONTROL Produktlistenelement] | [[!UICONTROL Artikel zurücksenden]](https://github.com/adobe/xdm/pull/1773/files) wurde hinzugefügt, um die Informationen zur Genehmigung für die Rücksendung von Waren einzuschließen. |
| Datentyp | Bestellung | [[!UICONTROL Return Info]](https://github.com/adobe/xdm/pull/1773/files) wurde hinzugefügt, um die ausgestellte RMA (Return Merchandise Authorization) einzuschließen. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md)

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Identity Service-Benutzeroberfläche | Verwenden Sie das verbesserte Tool zur Erstellung benutzerdefinierter Namespaces in der Experience Platform-Benutzeroberfläche, um Ihre benutzerdefinierten Namespaces und die zugehörigen Identitätstypen besser zu verwalten. Die erweiterte Identity Service-Benutzeroberfläche bietet Ihnen folgende Vorteile: <ul><li>Kontextuelles Erlebnis: Visuelle Hinweise, Klarheit und Kontext dazu, was ein Identity-Namespace ist und welche Identitätstypen es sind.</li><li>Genauigkeit: Bessere Fehlerbehandlung ohne doppelte Identitätsnamen.</li><li>Auffindbarkeit: Zugriff auf die Dokumentation über ein produktinternes Dialogfeld.</li></ul> Weitere Informationen finden Sie im Handbuch unter [Erstellen benutzerdefinierter Namespaces](../../identity-service/features/namespaces.md#create-namespaces). |
| Änderungen an den Beschränkungen für Identitätsdiagramme | Das Limit für Identitätsdiagramme wurde von 150 auf 50 Identitäten geändert. Wenn eine neue Identität in ein vollständiges Diagramm aufgenommen wird, wird die älteste Identität, die auf dem Aufnahmezeitstempel und dem Identitätstyp basiert, gelöscht. Cookie-Identitätstypen haben beim Löschen Priorität. Wenden Sie sich an Ihr Adobe-Konto-Team, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält: <ul><li>Ein benutzerdefinierter Namespace, in dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.</li><li>Ein benutzerdefinierter Namespace, in dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.</li></ul> Adobe Engineering verarbeitet diese Anfragen manuell. Weitere Informationen finden Sie in den [Leitplanken für Identity Service-Daten](../../identity-service/guardrails.md) und im Handbuch [Best Practices zur Verwaltung von Datenlizenzen](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Weitere Informationen zu Identity Service finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der Protokollfilter-Benutzeroberfläche | Verbesserte Filterung des Abfrageprotokolls verbessert die Sichtbarkeit für benutzergenerierte Protokolle zur Überwachung, Verwaltung und Fehlerbehebung. Sie können die Liste der Abfrageprotokolle nach verschiedenen Einstellungen filtern. <br> ![Die Filtereinstellungen für das Abfrageprotokoll.](../2023/assets/log-filter-settings.png "Neue Abfrageprotokollfilter sind hervorgehoben."){width="100" zoomable="yes"} <br> Weitere Informationen finden [ in der ](../../query-service/ui/query-logs.md#filter-logs) zu Abfrageprotokollen . |
| Mehrere Aktualisierungen der Benutzeroberfläche des Abfrage-Editors | Sie können jetzt mehrere sequenzielle Abfragen im Abfrage-Editor ausführen oder mehr als eine Abfrage schreiben und alle Abfragen sequenziell ausführen. Um der Ausführung Ihrer Abfrage mehr Flexibilität zu verleihen, können Sie die ausgewählte Abfrage markieren und auswählen, dass diese spezifische Abfrage unabhängig von den anderen ausgeführt werden soll. Weitere Informationen finden Sie [ Handbuch zur Benutzeroberfläche ](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) Abfrage-Editors . |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Experience Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Anpassbare Spalten | Sie können jetzt das Layout von Audience Portal mit in der Größe veränderbaren Spalten anpassen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Zielgruppenportal - Übersicht](../../segmentation/ui/audience-portal.md#customize). |
| Aufschlüsselung der Aktualisierungshäufigkeit | Jetzt können Sie eine Aufschlüsselung der Aktualisierungshäufigkeiten der Zielgruppen in Ihrer Organisation anzeigen. Weitere Informationen zu dieser Funktion finden Sie im [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#browse). |

Weitere Informationen zum Segmentierungs-Service finden Sie unter [Segmentierungs-Service - Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Parameter für die `offset` Paginierung in Selbstbedienungsquellen (Batch-SDK) | Sie können jetzt eine `endConditionName` und einen `endConditionValue` für Ihre Quelle angeben, wenn Sie `offset` Paginierung verwenden. Mit diesen Parametern können Sie die Bedingung angeben, die die Paginierungsschleife in der nächsten HTTP-Anfrage beendet. Weitere Informationen finden Sie im [Handbuch zur Paginierung für Selbstbedienungsquellen (Batch-SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
