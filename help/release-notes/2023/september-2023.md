---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise September 2023 zu Adobe Experience Platform.
source-git-commit: 05136ca1a44fa0ecbf2fd9941d047c3a0899f2d1
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 30%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 28. September 2023**

Neue Funktionen in Adobe Experience Platform:

- [Berechnete Attribute](#computed-attributes)

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Warnhinweise](#alerts)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Identity Service](#identity-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Berechnete Attribute {#computed-attributes}

Berechnete Attribute ermöglichen eine einfache Zusammenfassung von Ereignisdaten in Profilattributen über eine intuitive Benutzeroberfläche für eine verbesserte verhaltensbasierte Segmentierung, Personalisierung und Aktivierung. Mit dieser Funktion können Sie berechnete Attribute selbstständig erstellen, verwalten und in Segmentierung, Real-Time CDP-Zielen oder Adobe Journey Optimizer verwenden. Darüber hinaus vereinfachen berechnete Attribute die Segmentierung und Journey-Workflows, damit Sie relevante Erlebnisse nahtlos bereitstellen können. Weitere Informationen zu berechneten Attributen finden Sie in der [Übersicht über berechnete Attribute](../../profile/computed-attributes/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Tab Verlauf der Warnhinweise | Die Warnhinweise [!UICONTROL Geschichte] enthält nun alle Ereignisse, einschließlich Verzögerungen, Starts, Erfolgen und Fehlern. Lesen Sie die [Dokumentation zur Warn-Benutzeroberfläche](../../observability/alerts/ui.md) für weitere Informationen zum Tab Verlauf. |

{style="table-layout:auto"}

Weitere Informationen zu Warnungen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Datenströme | Unterstützung der Gerätesuche | Beim Konfigurieren eines Datastreams können Sie jetzt die Ebene der zu erfassenden Gerätesuchinformationen auswählen. Informationen zur Gerätesuche umfassen Daten zum Gerät, zur Hardware, zum Betriebssystem und zum Browser, die für die Interaktion mit Ihrer Seite verwendet werden. <br>  Informationen zur Gerätesuche können nicht zusammen mit Benutzeragent und Client-Hinweisen erfasst werden. Wenn Sie auswählen, Geräteinformationen zu erfassen, wird die Erfassung von Benutzeragenten- und Client-Hinweisen deaktiviert und umgekehrt. Alle Gerätesucherinformationen werden im `xdm:device` Feldergruppe. Weitere Informationen finden Sie in der Dokumentation unter [Konfigurieren von Datenspeichern](../../datastreams/configure.md#geolocation-device-lookup). |
| Erweiterungen | [!DNL TikTok] Web Events API-Erweiterung | Die [[!DNL TikTok] Web Events API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) -Erweiterung ermöglicht es Ihnen, die im Adobe Experience Platform Edge Network erfassten Daten zu nutzen und an [!DNL TikTok] in Form von serverseitigen Ereignissen, bei denen die [!DNL TikTok] Web Events-API. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie im Abschnitt [Datenerfassung - Übersicht](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Neu | [[!DNL HubSpot]](https://www.hubspot.com) ist eine CRM-Plattform mit allen Software, Integrationen und Ressourcen, die Sie für die Verbindung von Marketing, Vertrieb, Content Management und Kundendienst benötigen. Dadurch können Sie Ihre Daten, Teams und Kunden auf einer CRM-Plattform verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Aktualisiert | Hinzugefügte Unterstützung für [!DNL Dynamics 365] benutzerdefinierte Feldpräfixe für benutzerdefinierte Felder, die nicht in der Standardlösung in [!DNL Dynamics 365]. ein neues Eingabefeld, **[!UICONTROL Anpasspräfix]** wurde im Abschnitt [Zieldetails ausfüllen](#destination-details) Schritt. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | New | Activate audiences previously onboarded to [!DNL LiveRamp] to premium publishers across mobile, web, display, and connected TV mediums. <br> After onboarding audiences to your [!DNL LiveRamp] account through the [LiveRamp - Onboarding](liveramp-onboarding.md) connection, use the new [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connection to activate the audiences to downstream destinations.  |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Updated | The Experience Cloud Audiences destination is now generally available. Use this destination to activate audiences from Real-Time CDP to Audience Manager and Adobe Analytics. You need an Audience Manager license to send audiences to Adobe Analytics. |

-->

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Datenexporte in Real-Time CDP | Die [Datensatzexport](../../destinations/ui/export-datasets.md) -Funktion ist jetzt allgemein verfügbar. Siehe [welche Datensätze Sie basierend auf der Experience Platform-App exportieren können](../../destinations/ui/export-datasets.md#datasets-to-export) Sie gekauft haben, und überprüfen Sie die [Limits für das Exportieren von Datensätzen](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Unterstützung für den Export von Array-Objekten | Exportieren Sie Arrays von Grundwerten (Zeichenfolge, int oder boolesche Werte) als flache Schemadateien in Cloud-Speicher-Ziele. Mehr über die Funktionen in [Dokumentation](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamische Dropdown-Selektoren in Destination SDK | Beim Erstellen eines Ziels mithilfe der Destination SDK können Sie jetzt Folgendes verwenden: [dynamische Dropdown-Selektoren](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) , um die Felder eines Dropdown-Selektors mit Werten zu füllen, die von einer API abgerufen wurden. |

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Nutzen Sie [Überwachung der Transparenz](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) jetzt für Unternehmensziele verfügbar ([HTTP-API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) und [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) auf der Datenfluss-Ausführungsebene, um die Aktivierungsmetriken und den Status im [Datenfluss-Detailansicht](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), mit zusätzlichen Informationen über Fehlercodes und Meldungen zur Fehlerbehebung.
- Wenn Sie den Namen der Zielgruppen aktualisieren, die dem [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)und anderen Zielen, die [Vorlagen für Zielgruppenaktualisierungen](../../destinations/destination-sdk/metadata-api/update-audience-template.md)festgelegt ist, werden diese Namensänderungen jetzt nachgelagert im Ziel angezeigt.

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen der Benutzeroberfläche von Identity Service | Verwenden Sie das verbesserte Tool zur Erstellung benutzerdefinierter Namespaces in der Experience Platform-Benutzeroberfläche, um Ihre benutzerdefinierten Namespaces und die zugehörigen Identitätstypen besser zu verwalten. Die erweiterte Identity Service-Benutzeroberfläche bietet Ihnen Folgendes: <ul><li>Kontextuelles Erlebnis: Visuelle Hinweise, Klarheit und Kontext zu dem, was ein Identitäts-Namespace ist und zu Identitätstypen gehören.</li><li>Genauigkeit: Besserer Umgang mit Fehlern, ohne doppelte Identitätsnamen.</li><li>Entdeckung: Zugriff auf die Dokumentation über ein in das Produkt integriertes Dialogfeld.</li></ul> Weitere Informationen finden Sie im Handbuch unter [Erstellen benutzerdefinierter Namespaces](../../identity-service/namespaces.md#create-namespaces). |
| Änderungen an den Identitätsdiagrammbeschränkungen | Die Grenze für Identitätsdiagramme wurde von 150 Identitäten zu 50 Identitäten geändert. Wenn eine neue Identität in ein vollständiges Diagramm aufgenommen wird, wird die älteste Identität, die auf dem Erfassungszeitstempel und Identitätstyp basiert, gelöscht. Cookie-Identitätstypen werden zum Löschen priorisiert. Wenden Sie sich an Ihr Adobe Account-Team, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält: <ul><li>einen benutzerdefinierten Namespace, bei dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.</li><li>einen benutzerdefinierten Namespace, bei dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.</li></ul> Adobe Engineering verarbeitet diese Anfragen manuell. Weitere Informationen finden Sie im Abschnitt [Limits für Identity Service-Daten](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Weitere Informationen zu Identity Service finden Sie im Abschnitt [Identity Service - Übersicht](../../identity-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Anpassbare Spalten | Sie können jetzt das Layout von Audience Portal mit neu skalierbaren Spalten anpassen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#customize). |
| Aufschlüsselung der Aktualisierungsfrequenz | Sie können jetzt eine Aufschlüsselung der Aktualisierungshäufigkeit der Zielgruppen in Ihrer Organisation anzeigen. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#browse). |

Weitere Informationen zu Quellen finden Sie unter [Quellen - Übersicht](../../sources/home.md).

Weitere Informationen zum Segmentierungsdienst finden Sie in der [Übersicht über den Segmentierungsdienst](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Parameter für `offset` Paginierung in Self-Serve-Quellen (Batch-SDK) | Sie können jetzt eine `endConditionName` und `endConditionValue` für Ihre Quelle verwenden `offset` Paginierung. Mit diesen Parametern können Sie die Bedingung angeben, die die Paginierungsschleife in der nächsten HTTP-Anforderung beendet. Weitere Informationen finden Sie im Abschnitt [Paginierungshandbuch für Self-Serve-Quellen (Batch SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie unter [Quellen - Übersicht](../../sources/home.md).