---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise September 2023 zu Adobe Experience Platform.
exl-id: ff7fb0c1-6941-4339-8648-58f9b9e9a91f
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 31%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Freitag, 28. September 2023**

Neue Funktionen in Adobe Experience Platform:

- [Berechnete Attribute](#computed-attributes)

Aktualisierungen vorhandener Funktionen im Experience Platform:

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

Berechnete Attribute ermöglichen eine einfache Zusammenfassung von Ereignisdaten in Profilattributen über eine intuitive Benutzeroberfläche für eine verbesserte verhaltensbasierte Segmentierung, Personalisierung und Aktivierung. Mit dieser Funktion können Sie berechnete Attribute selbstständig erstellen, verwalten und in Segmentierung, Real-Time CDP-Zielen oder Adobe Journey Optimizer verwenden. Darüber hinaus vereinfachen berechnete Attribute die Segmentierung und Journey-Workflows, damit Sie relevante Erlebnisse nahtlos bereitstellen können. Weitere Informationen zu berechneten Attributen finden Sie in der [Übersicht über berechnete Attribute](../../profile/computed-attributes/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Tab Verlauf der Warnhinweise | Der Tab Warnhinweise [!UICONTROL Verlauf] enthält jetzt alle Ereignisse, einschließlich Verzögerungen, Starts, Erfolgen und Fehlern. Weitere Informationen zur Verlaufs-Registerkarte finden Sie in der Dokumentation zur Benutzeroberfläche von [Warnhinweisen](../../observability/alerts/ui.md) . |

{style="table-layout:auto"}

Weitere Informationen zu Warnungen finden Sie in der [[!DNL Observability Insights] Übersicht](../../observability/home.md) .

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards], in denen basierend auf täglichen Schnappschüssen wichtige Informationen zu den Unternehmensdaten dargestellt werden.

| Funktion | Beschreibung |
| --- | --- |
| [Verbesserung des Lizenzverwendungs-Dashboards](../../dashboards/guides/license-usage.md) | Verwalten Sie die Kontrolle über Ihre Lizenzvereinbarungen mit verbesserten Berichten und wichtigen Metrikvisualisierungen bezüglich der Lizenznutzung in Ihrem Unternehmen. Diese Verbesserungen bieten eine hohe Granularität gegenüber den Metriken zur Lizenznutzung für alle Experience Platform-Produkte, die Sie erworben haben. |

{style="table-layout:auto"}

Weitere Informationen zum Dashboard zur Lizenznutzung finden Sie in der Übersicht über das Dashboard zur Lizenznutzung [1 .](../../dashboards/guides/destinations.md)

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Datenströme | Unterstützung der Gerätesuche | Beim Konfigurieren eines Datastreams können Sie jetzt die Ebene der zu erfassenden Gerätesuchinformationen auswählen. Informationen zur Gerätesuche umfassen Daten zum Gerät, zur Hardware, zum Betriebssystem und zum Browser, die für die Interaktion mit Ihrer Seite verwendet werden. <br> Informationen zur Gerätesuche können nicht zusammen mit Benutzeragent und Client-Hinweisen erfasst werden. Wenn Sie auswählen, Geräteinformationen zu erfassen, wird die Erfassung von Benutzeragenten- und Client-Hinweisen deaktiviert und umgekehrt. Alle Gerätesucherinformationen werden in der Feldergruppe `xdm:device` gespeichert. Weitere Informationen finden Sie in der Dokumentation zu [Konfigurieren von Datenastreams](../../datastreams/configure.md#geolocation-device-lookup). |
| Erweiterungen | [!DNL TikTok] Web-Events-API-Erweiterung | Mit der Erweiterung [[!DNL TikTok] Web Events API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) können Sie im Adobe Experience Platform-Edge Network erfasste Daten nutzen und in Form von serverseitigen Ereignissen mithilfe der [!DNL TikTok] Web Events API an [!DNL TikTok] senden. |

{style="table-layout:auto"}

Weiterführende Informationen zur Datenerfassung finden Sie in der [Übersicht zur Datenerfassung](../../tags/home.md).

## Data Governance {#data-governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in Experience Platform auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffskontrolle für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Partner Ecosystem-Beschriftungen für Drittanbieterdaten | Es stehen neue Datennutzungsbezeichnungen für die Anreicherung und Prospektion durch Drittanbieter zur Verfügung. Weitere Informationen finden Sie in der [Dokumentation zu Partner Ecosystem-Beschriftungen](../../data-governance/labels/reference.md#partner) . |

{style="table-layout:auto"}

Weitere Informationen zu Data Governance finden Sie im Abschnitt [Data Governance – Übersicht](../../data-governance/home.md).

## Datenhygiene {#hygiene}

Experience Platform bietet eine Reihe von Funktionen zur Datenhygiene, mit denen Sie Ihre gespeicherten Daten durch programmatische Löschungen der Datensätze von Privatkund*innen verwalten können. Mit dem Arbeitsbereich [!UICONTROL Data Lifecycle] in der Benutzeroberfläche oder über Aufrufe der Data Hygiene API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet, aktualisiert werden, wenn falsche Datenanforderungen behoben werden müssen, und gelöscht wird, wenn organisatorische Richtlinien dies für erforderlich halten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} Löschen von Datensätzen (begrenzte Version) | Verwalten Sie Ihren Datenlebenszyklus in allen Datenspeichern, um Kundenverpflichtungen und Lizenzvereinbarungen mit erweiterten Funktionen für das Data Lifecycle Management in Adobe Experience Platform zu erfüllen: Automatisierter Ablauf von Datensätzen und Löschen von Datensätzen.<br>Mit automatisiertem Datensatzablauf können Sie ganze Datensätze löschen und ein Datum und eine Uhrzeit für das Löschen des Datensatzes festlegen.<br>Löschen von Datensätzen ermöglicht das Löschen einzelner Verbraucherprofile durch die Zielgruppenbestimmung ihrer primären Identitäten. Sie können die primären Identitäten einzeln über die Benutzeroberfläche oder per CSV/JSON-Datei-Upload bereitstellen. Weitere Informationen finden Sie in der Dokumentation zum Löschen von [Datensätzen](../../hygiene/ui/record-delete.md) . |
| Datensatzgültigkeiten | Minimieren Sie Ihre Daten und behalten Sie die Kontrolle über Ihre Lizenzvereinbarungen mit automatisiertem Datensatzablauf. Reduzieren Sie das Datenvolumen, indem Sie ganze Datensätze löschen und ein Datum und eine Uhrzeit für das Löschen des Datensatzes festlegen. Weitere Informationen finden Sie in der Dokumentation zu den [Datensatzabläufen](../../hygiene/ui/dataset-expiration.md) . |

{style="table-layout:auto"}

Weiterführende Informationen zu den Datenhygiene-Funktionen von Platform finden Sie in der [Übersicht zur Datenhygiene](../../hygiene/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Neu | Aktivieren Sie Zielgruppen, die zuvor mit [!DNL LiveRamp] integriert wurden, für Premium-Herausgeber über mobile, Web-, Display- und vernetzte TV-Medien hinweg. <br> Nachdem Sie Zielgruppen über die Verbindung [LiveRamp - Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md) in Ihr [!DNL LiveRamp]-Konto integriert haben, verwenden Sie die neue Verbindung [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) , um die Zielgruppen für nachgelagerte Ziele zu aktivieren. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Neu | [[!DNL HubSpot]](https://www.hubspot.com) ist eine CRM-Plattform mit allen Software, Integrationen und Ressourcen, die Sie für die Verbindung von Marketing, Vertrieb, Content Management und Kundendienst benötigen. Dadurch können Sie Ihre Daten, Teams und Kunden auf einer CRM-Plattform verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Aktualisiert | Unterstützung für benutzerdefinierte Feldpräfixe mit [!DNL Dynamics 365] für benutzerdefinierte Felder hinzugefügt, die nicht in der Standardlösung in [!DNL Dynamics 365] erstellt wurden. Im Schritt [Zieldetails ausfüllen](#destination-details) wurde ein neues Eingabefeld hinzugefügt, das **[!UICONTROL Anpasspräfix]**. |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Aktualisiert | Das Ziel &quot;Experience Cloud-Zielgruppen&quot;ist jetzt allgemein verfügbar. Verwenden Sie dieses Ziel, um Zielgruppen von Real-Time CDP zu Audience Manager und Adobe Analytics zu aktivieren. Sie benötigen eine Audience Manager-Lizenz, um Zielgruppen an Adobe Analytics senden zu können. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Datenexporte in Real-Time CDP | Die Funktion [zum Exportieren von Datensätzen](../../destinations/ui/export-datasets.md) ist jetzt allgemein verfügbar. Siehe [, welche Datensätze Sie basierend auf der von Ihnen erworbenen Experience Platform App exportieren können, und überprüfen Sie die [Limits für den Export von Datensätzen](/help/destinations/guardrails.md#dataset-exports).](../../destinations/ui/export-datasets.md#datasets-to-export) |
| (Beta) Unterstützung für den Export von Array-Objekten | Exportieren Sie Arrays von Grundwerten (Zeichenfolge, int oder boolesche Werte) als flache Schemadateien in Cloud-Speicher-Ziele. Weitere Informationen zur Funktionalität finden Sie in der [Dokumentation](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamische Dropdown-Selektoren in Destination SDK | Beim Erstellen eines Ziels durch Destination SDK können Sie jetzt [dynamische Dropdown-Selektoren](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) verwenden, um die Felder eines Dropdown-Selektors mit Werten zu füllen, die von einer API abgerufen werden. |

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Verwenden Sie [Überwachung der Transparenz](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations), die jetzt für Unternehmensziele ([HTTP-API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) und [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) auf Datenflusslaufebene verfügbar ist, um Aktivierungsmetriken und -status in der [Datenfluss-Detailansicht](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page) zu überwachen, einschließlich zusätzlicher Informationen über Fehlercodes und Meldungen zur Fehlerbehebung.
- Wenn Sie den Namen der Zielgruppen aktualisieren, die dem [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md) und anderen Zielen, die [Vorlagen für Zielgruppenaktualisierungen](../../destinations/destination-sdk/metadata-api/update-audience-template.md) verwenden, zugeordnet sind, werden diese Namensänderungen jetzt nachgelagert im Ziel angezeigt.

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Schnellaktionen im Schema Editor hinzugefügt | Der Arbeitsfläche des Schema-Editors wurden neue Schnellaktionen hinzugefügt. Sie können jetzt die JSON-Struktur kopieren oder das Schema direkt aus dem Editor löschen.<br>![Die Schnellaktionen im Schema-Editor.](../2023/assets/schema-editor-copy-json.png "Der Schema-Editor mit &quot;Mehr&quot;und &quot;In JSON kopieren&quot;ist hervorgehoben."){width="100" zoomable="yes"} |
| Filtern von XDM-Ressourcen nach benutzerdefinierten oder standardmäßigen Erstellern | Die Listen der verfügbaren Schemas, Feldergruppen, Datentypen und Klassen werden nun nach ihrer Erstellungsmethode vorab gefiltert. Auf diese Weise können Sie Ressourcen danach filtern, ob sie von Adobe erstellt oder benutzerdefiniert wurden.<br>![Die standardmäßigen und benutzerdefinierten Filter im Arbeitsbereich &quot;Schemas&quot;.](../2023/assets/standard-and-custom-classes.png "Der Arbeitsbereich &quot;Schemas&quot;mit hervorgehobenen Standard- und benutzerdefinierten Filtern."){width="100" zoomable="yes"} <br> Weitere Informationen finden Sie in der Dokumentation zum Erstellen und Bearbeiten von Ressourcen](../../xdm/ui/resources/classes.md#filter.md) .[ |

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierter Workflow für die Schemaerstellung | Es wurde ein neuer Workflow zur Schemaerstellung implementiert, um den Prozess zu optimieren. <br> ![Die Benutzeroberfläche für die Erstellung des neuen Schemas.](../2023/assets/schema-class-options.png "Die Auswahl der neuen Schemadetails wurde hervorgehoben."){width="100" zoomable="yes"} <br> Weitere Informationen finden Sie in der Dokumentation zur Schemaerstellung [3} .](../../xdm/ui/resources/schemas.md#create) |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL return]](https://github.com/adobe/xdm/pull/1773/files) | RMA (Return Merchandise Authorization) ausgestellt. |
| Datentyp | [[!UICONTROL Rückgabewert]](https://github.com/adobe/xdm/pull/1773/files) | Die Informationen des zurückgegebenen Elements innerhalb der RMA (Return Merchandise Authorization). |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Erweiterung | [!UICONTROL AJO-Entitätsfelder] | Das [[!UICONTROL Flag für mehrere Varianten]](https://github.com/adobe/xdm/pull/1774/files) wurde zu [!UICONTROL AJO-Entitätsfeldern] hinzugefügt, um zu ermitteln, ob es sich bei der Variante um eine Variante mit mehreren Varianten handelt oder nicht. |
| Datentyp | [!UICONTROL Produktlistenelement] | [[!UICONTROL Rückgabeelement]](https://github.com/adobe/xdm/pull/1773/files) wurde hinzugefügt, um die Informationen zur Autorisierung der RückkehrMerchandise einzuschließen. |
| Datentyp | Bestellung | [[!UICONTROL Return Info]](https://github.com/adobe/xdm/pull/1773/files) wurde hinzugefügt, um die ausgestellte RMA (Return Merchandise Authorization) einzuschließen. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md)

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Benutzeroberfläche von Identity Service | Verwenden Sie das verbesserte Tool zur Erstellung benutzerdefinierter Namespaces in der Experience Platform-Benutzeroberfläche, um Ihre benutzerdefinierten Namespaces und die zugehörigen Identitätstypen besser zu verwalten. Die erweiterte Identity Service-Benutzeroberfläche bietet Ihnen Folgendes: <ul><li>Kontextuelles Erlebnis: Visuelle Hinweise, Klarheit und Kontext zu dem, was ein Identitäts-Namespace ist und zu Identitätstypen gehören.</li><li>Genauigkeit: Besserer Umgang mit Fehlern, ohne doppelte Identitätsnamen.</li><li>Entdeckung: Zugriff auf die Dokumentation über ein in das Produkt integriertes Dialogfeld.</li></ul> Weitere Informationen finden Sie in der Anleitung zum Erstellen benutzerdefinierter Namespaces ](../../identity-service/features/namespaces.md#create-namespaces).[ |
| Änderungen an den Identitätsdiagrammbeschränkungen | Die Grenze für Identitätsdiagramme wurde von 150 Identitäten zu 50 Identitäten geändert. Wenn eine neue Identität in ein vollständiges Diagramm aufgenommen wird, wird die älteste Identität, die auf dem Erfassungszeitstempel und Identitätstyp basiert, gelöscht. Cookie-Identitätstypen werden zum Löschen priorisiert. Wenden Sie sich an Ihr Adobe Account-Team, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält: <ul><li>einen benutzerdefinierten Namespace, bei dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.</li><li>einen benutzerdefinierten Namespace, bei dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.</li></ul> Adobe Engineering verarbeitet diese Anfragen manuell. Weitere Informationen finden Sie in den [Limits für Identity Service-Daten](../../identity-service/guardrails.md) und im Handbuch [Best Practices für die Lizenzberechtigungen für Data Management](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Weiterführende Informationen zum Identity Service finden Sie in der [Übersicht zum Identity Service](../../identity-service/home.md) .

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der Benutzeroberfläche für die Protokollfilterung | Die verbesserte Filterung von Abfrageprotokollen verbessert die Sichtbarkeit für benutzergenerierte Protokolle zur Überwachung, Verwaltung und Fehlerbehebung. Sie können die Liste der Abfrageprotokolle anhand verschiedener Einstellungen filtern. <br> ![Die Filtereinstellungen des Abfrageprotokolls.](../2023/assets/log-filter-settings.png "Neue Abfrageprotokollfilter werden hervorgehoben."){width="100" zoomable="yes"} <br> Weitere Informationen finden Sie in der Dokumentation zu den [Abfrageprotokollen](../../query-service/ui/query-logs.md#filter-logs) . |
| Mehrere UI-Aktualisierungen des Abfrage-Editors | Sie können jetzt mehrere sequenzielle Abfragen im Abfrage-Editor ausführen oder mehr als eine Abfrage schreiben und alle Abfragen sequenziell ausführen. Um Ihre Abfrageausführung flexibler zu gestalten, können Sie Ihre ausgewählte Abfrage markieren und diese Abfrage unabhängig von den anderen auswählen. Weitere Informationen finden Sie im [UI-Handbuch für den Abfrage-Editor](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) . |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Anpassbare Spalten | Sie können jetzt das Layout von Audience Portal mit neu skalierbaren Spalten anpassen. Weitere Informationen zu dieser Funktion finden Sie in der [Übersicht über Audience Portal](../../segmentation/ui/audience-portal.md#customize) . |
| Aufschlüsselung der Aktualisierungsfrequenz | Sie können jetzt eine Aufschlüsselung der Aktualisierungshäufigkeit der Zielgruppen in Ihrer Organisation anzeigen. Weitere Informationen zu dieser Funktion finden Sie im Handbuch [zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#browse). |

Weiterführende Informationen zu Segmentation Service finden Sie in der [Segmentation Service - Übersicht](../../segmentation/home.md) .

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Parameter für die Paginierung von `offset` in Self-Serve-Quellen (Batch-SDK) | Sie können jetzt für Ihre Quelle `offset` Seitenumbrüche mit `endConditionName` und `endConditionValue` festlegen. Mit diesen Parametern können Sie die Bedingung angeben, die die Paginierungsschleife in der nächsten HTTP-Anforderung beendet. Weitere Informationen finden Sie im [Paginierungshandbuch für Self-Serve-Quellen (Batch-SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).
