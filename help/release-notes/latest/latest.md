---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 81c17a6ea07efbbea91e0d918d52ec96e0335152
workflow-type: tm+mt
source-wordcount: '3133'
ht-degree: 29%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 28. September 2022**

Neue Funktionen in Adobe Experience Platform:

- [Attributbasierte Zugriffssteuerung](#abac)
- [Datenhygiene](#data-hygiene)
- [[!UICONTROL Datenschutzkonsole]](#privacy-console)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Auditprotokolle](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Query Service](#query-service)
- [Quellen](#sources)

## Attributbasierte Zugriffssteuerung {#abac}

>[!IMPORTANT]
>
>Die attributbasierte Zugriffskontrolle wird ab Oktober 2022 aktiviert. Wenn Sie ein früherer Anwender sein möchten, wenden Sie sich an Ihren Kundenbetreuer bei der Adobe.

Die attributbasierte Zugriffskontrolle ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung des Benutzerzugriffs gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzern in Ihrer Organisation Zugriff auf einzelne Objekte gewähren oder sperren.

Mithilfe der attributbasierten Zugriffskontrolle können Administratoren Ihres Unternehmens den Zugriff der Benutzer auf personenbezogene Daten (EPPD), personenbezogene Daten (PII) und andere benutzerdefinierte Datentypen für alle Platform-Workflows und -Ressourcen steuern. Administrierende können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung | Mit der attributbasierten Zugriffskontrolle können Sie Experience-Datenmodell (XDM)-Schemafelder und -Segmente mit Bezeichnungen versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Administratoren die Benutzeroberfläche zur Verwaltung von Benutzern und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder und -Segmente abdecken, um den Zugriff, der Benutzern oder Benutzergruppen (interne, externe oder Drittanbieter-Benutzer) gewährt wird, besser zu verwalten. Weitere Informationen finden Sie in der [Übersicht über die attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md). |
| Berechtigungen | Berechtigungen sind der Bereich von Experience Cloud, in dem Administrierende Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten. Über Berechtigungen können Sie Rollen erstellen und verwalten, die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen und Richtlinien erstellen, um Beschriftungen zu nutzen und zu definieren, welche Benutzerrollen Zugriff auf bestimmte Platform-Ressourcen haben. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzer*innen verwalten, die einer bestimmten Rolle zugeordnet sind. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche für Berechtigungen](../../access-control/abac/ui/browse.md). |

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im Abschnitt [Handbuch zur attributbasierten Zugriffskontrolle - End-to-End](../../access-control/abac/end-to-end-guide.md).

## Datenhygiene {#data-hygiene}

Adobe Experience Platform bietet leistungsstarke Tools zur Verwaltung großer, komplizierter Datenvorgänge, was die Orchestrierung von Customer Experiences ermöglicht. Da im Laufe der Zeit Daten in das System aufgenommen werden, ist es wichtig, Ihre Datenspeicher so zu verwalten, dass Daten wie vorgesehen verwendet werden. So müssen Daten aktualisiert werden, um falsche Einträge zu korrigieren, und Daten gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

Mit den Datenhygienemöglichkeiten von Adobe Experience Platform können Sie Ihre Daten bereinigen, indem Sie automatisierte Datensatzabläufe planen und Kundendaten programmgesteuert nach Identität löschen.

>[!IMPORTANT]
>
>Die Möglichkeiten der Datenhygiene stehen nur Organisationen zur Verfügung, die Adobe Healthcare Shield oder Privacy Shield erworben haben.

Erste Schritte mit Datenhygiene finden Sie in der folgenden Dokumentation:

- [Übersicht über die Datenhygiene](../../hygiene/home.md): Erfahren Sie mehr über die Grundlagen der Datenhygiene-Funktionen von Platform.
- [[!UICONTROL Datenhygiene] UI-Handbuch](../../hygiene/ui/overview.md): Erfahren Sie, wie Sie in der Benutzeroberfläche von Platform den Ablauf von Datensätzen und Löschanfragen von Verbrauchern planen.
- [Data Hygiene API-Handbuch](../../hygiene/api/overview.md): Sämtliche in der Benutzeroberfläche verfügbaren Datenhygiene-Aktivitäten können ebenfalls programmgesteuert durchgeführt werden

## [!UICONTROL Datenschutzkonsole] {#privacy-console}

Die [!UICONTROL Datenschutzkonsole] -Registerkarte in der Experience Platform-Benutzeroberfläche bietet eine Dashboard-Ansicht mit wichtigen Einblicken aus datenschutzbezogenen Funktionen wie [Anfragen von Datensubjekten nach Privacy Service](../../privacy-service/home.md), [Datenhygiene](../../hygiene/home.md)und [Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md). Die Konsole enthält außerdem mehrere produktinterne Benutzerhandbücher, die Sie durch gängige Datenschutz-Workflows führen.

Siehe [Übersicht über die Datenschutzkonsole](../../landing/governance-privacy-security/privacy-console.md) für weitere Informationen zur Funktion.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

KI/ML-Services ermöglichen es Marketing-Leuten und Fachleuten, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. Auf diese Weise können Marketing-Leute mithilfe von Konfigurationen auf Unternehmensebene Modelle erstellen, die speziell auf die Anforderungen eines Unternehmens zugeschnitten sind, ohne dass dafür datenwissenschaftliches Fachwissen erforderlich ist.

### Attributions-KI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

| Funktion | Beschreibung |
| --- | --- |
| Entwurfsinstanz speichern | Diese neue Funktion ermöglicht es Marketing-Analysten, eine Modellkonfiguration als Entwurfsinstanz zu speichern und sie so lange zu bearbeiten, bis sie vor dem Training und Scoring abgeschlossen ist. Zu den Szenarien, in denen diese Funktion hilfreich ist, zählen Fälle, in denen ein Benutzer mehrere Felder definiert, die im Workflow definiert werden müssen, aber aufgrund von Zeitbeschränkungen nicht abgeschlossen werden können. Ein anderes Szenario ist, wenn eine oder mehrere Datensatzstatistiken verarbeitet werden und noch nicht verfügbar sind. Lesen Sie die [Attribution AI-Benutzerhandbuch](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) , um mehr zu erfahren. |
| Governance-Strategien | Nachdem sich Benutzer zum Erstellen einer Instanz über den Konfigurations-Workflow übermittelt haben, prüft der neue Richtliniendurchsetzungsdienst, ob Richtlinienverletzungen bei der Datennutzung vorliegen, und zeigt die Details in einem Popup an. Dadurch wird sichergestellt, dass Datenvorgänge und Marketing-Aktionen mit den in Adobe Experience Platform konfigurierten Datennutzungsrichtlinien konform sind. |

Weitere Informationen zu Attribution AI finden Sie unter [Attribution AI - Übersicht](../../intelligent-services/attribution-ai/overview.md). Informationen zu Data Governance-Richtlinien finden Sie im Abschnitt [Richtlinien - Übersicht](../../data-governance/policies/overview.md).

### Kunden-KI

Kunden-KI in Real-time Customer Data Platform dient dazu, für einzelne Profile in gewünschten Umfang benutzerdefinierte Neigungswerte wie Abwanderung und Konversion zu generieren.

| Funktion | Beschreibung |
| --- | --- |
| Entwurfsinstanz speichern | Diese neue Funktion ermöglicht es Marketing-Analysten, eine Modellkonfiguration als Entwurfsinstanz zu speichern und sie so lange zu bearbeiten, bis sie vor dem Training und Scoring abgeschlossen ist. Zu den Szenarien, in denen diese Funktion hilfreich ist, zählen Fälle, in denen ein Benutzer mehrere Felder definiert, die im Workflow definiert werden müssen, aber aufgrund von Zeitbeschränkungen nicht abgeschlossen werden können. Ein anderes Szenario ist, wenn eine oder mehrere Datensatzstatistiken verarbeitet werden und noch nicht verfügbar sind. Lesen Sie die [Benutzerhandbuch für Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) , um mehr zu erfahren. |
| Governance-Strategien | Nachdem sich Benutzer zum Erstellen einer Instanz über den Konfigurations-Workflow übermittelt haben, prüft der neue Richtliniendurchsetzungsdienst, ob Richtlinienverletzungen bei der Datennutzung vorliegen, und zeigt die Details in einem Popup an. Dadurch wird sichergestellt, dass Datenvorgänge und Marketing-Aktionen mit den in Adobe Experience Platform konfigurierten Datennutzungsrichtlinien konform sind. |

Weitere Informationen zu Customer AI finden Sie im [Customer AI - Übersicht](../../intelligent-services/customer-ai/overview.md). Informationen zu Data Governance-Richtlinien finden Sie im Abschnitt [Richtlinien - Übersicht](../../data-governance/policies/overview.md).

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität in Verbindung mit verschiedenen Services und Funktionen überprüfen. Die Auditprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Aktualisierte Funktionen**

| Funktion | Name | Beschreibung |
| --- | --- | --- |
| Ressourcen hinzugefügt | <ul><li>Attribution AI-Instanz</li><li>Customer AI-Instanz</li><li>Datastream</li></ul> | Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet. Wenn die Funktion aktiviert ist, müssen Sie die Protokollerfassung nicht manuell aktivieren. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu den verschiedenen ressourcenspezifischen Ereignistypen, die von Auditprotokollen in Platform verfolgt werden, finden Sie im Abschnitt [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke in die Daten Ihres Unternehmens erhalten, wie sie bei täglichen Momentaufnahmen erfasst werden.

| Funktion | Beschreibung |
| --- | --- |
| Beschriftung in Gebrauch | Bei der Anzeige in der Widget-Bibliothek erkennt die verwendete Bezeichnung einfach, ob in Ihrem Dashboard vorhandene Widgets vorhanden sind. Dadurch lässt sich die Duplizierung einfach vermeiden, obwohl Sie immer noch dasselbe Widget mehr als einmal hinzufügen können. |
| Benutzerdefinierte Dashboards | Benutzerdefinierte Dashboards helfen Ihnen, Einblicke zu beschleunigen und Visualisierungen anzupassen, indem Sie benutzerdefinierte Dashboards erstellen und verwalten können. Mit benutzerdefinierten Dashboards können Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten, um für Ihr Unternehmen relevante Schlüsselmetriken zu visualisieren. Lesen Sie die [Funktionshandbuch](../../dashboards/user-defined-dashboards.md) , um mehr zu erfahren. |
| Datenmodell der Customer Data Platform Insights | Die Funktion &quot;Customer Data Platform (CDP) Insights Data Model&quot;stellt die Datenmodelle und SQL bereit, die die Einblicke für verschiedene Profil-, Ziel- und Segmentierungs-Widgets ermöglichen. Sie können diese SQL-Abfragevorlagen anpassen, um CDP-Berichte für Ihre Marketing- und Key Performance Indicators zu erstellen. Diese Einblicke können dann als benutzerdefinierte Widgets für Ihre benutzerdefinierten Dashboards verwendet werden. Lesen Sie die [Handbuch zur Funktion &quot;CDP Insights Data Model&quot;](../../dashboards/cdp-insights-data-model.md) , um mehr zu erfahren. |
| Bericht-Widget &quot;Zielgruppenüberschneidung&quot; | Dieses Widget ist für beide verfügbar [!UICONTROL Profile] und [!UICONTROL Segmente] Dashboards. Der Bericht bietet eine geordnete Liste von Zielgruppen, die nach den höchsten oder niedrigsten Überschneidungsprozentsätzen für Ihr ausgewähltes Segment sortiert sind. Aus dem [!UICONTROL Profile] Dashboard können Sie Ihre Zielgruppenüberschneidung nach Zusammenführungsrichtlinien aus allen verfügbaren Segmenten filtern und anzeigen. Die [!UICONTROL Segmente] Mit Dashboards können Sie die Zielgruppenüberschneidung nach einem bestimmten Segment filtern.<br>Verwenden Sie diese Analyse, um neue Hochleistungssegmente zu erstellen und zu vermeiden, dass dieselbe Zielgruppe an verschiedene Ziele gesendet wird. Der Bericht hilft auch, versteckte Einblicke zu identifizieren, um die Segmentierung zu verbessern oder eindeutige Profile zu finden, die verfolgt werden sollen. Lesen Sie die entsprechenden [profiles](../../dashboards/guides/profiles.md#audience-overlap-report) und [Segmente](../../dashboards/guides/segments.md#audience-overlap-report) Widget-Handbücher , um mehr zu erfahren. |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Integration der linken Navigation in der Platform-Benutzeroberfläche | Alle Funktionen, die zuvor ausschließlich für die Datenerfassungs-Benutzeroberfläche galten (einschließlich Tags, Ereignisweiterleitung und Datastreams), sind jetzt auch über die linke Navigation in Experience Platform unter der Kategorie verfügbar. **[!UICONTROL Datenerfassung]**. Dadurch entfällt die Notwendigkeit, beim Arbeiten mit Datenerfassungsfunktionen in Platform zwischen Benutzeroberflächen zu wechseln. |
| Benutzerzuordnung in Tags und Ereignisweiterleitung | Wenn eine Liste verfügbar ist [!UICONTROL Eigenschaften] in Tags und Ereignisweiterleitung zeigt jede aufgelistete Eigenschaft jetzt an, wann sie zuletzt aktualisiert wurde und welcher Benutzer die Aktualisierung vorgenommen hat. |
| [[!DNL User-Agent Client Hints] im Web SDK](../../edge/fundamentals/user-agent-client-hints.md) | Das Web SDK unterstützt jetzt [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Clienthinweise ermöglichen es Website-Inhabern, auf einen Großteil der in der [!DNL User-Agent] -Zeichenfolge, aber auf eine mehr datenschutzfreundliche Weise. |
| [Seitenweise Migration des Web SDK](../../edge/home.md#migrating-to-web-sdk) | Sie können Ihre vorhandenen Webeigenschaften jetzt aus anderen Experience Cloud-Bibliotheken migrieren, z. B. [!DNL at.js], auf Web SDK, jeweils eine Seite. Dies ermöglicht einen stufenweisen Ansatz für die Web SDK-Migration, ohne dass alle Seiten gleichzeitig migriert werden müssen. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Destination SDK | Destination SDK bietet jetzt vollständige Unterstützung für Partner und Kunden, die Batch- (oder dateibasierte) produktive oder private Ziele erstellen. Weitere Informationen finden Sie auf den folgenden Dokumentationsseiten: <ul><li>[Übersicht über Destinationen SDK](/help/destinations/destination-sdk/overview.md)</li><li>[Dateibasiertes Ziel konfigurieren](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Testen Ihrer dateibasierten Ziele](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services bietet eine Plattform für die Konzeption kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Kampagnenorchestrierung, Interaktionsverwaltung in Echtzeit und die kanalübergreifende Ausführung. [Erste Schritte mit Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Beachten Sie, dass diese Integration mit Beachten funktioniert, dass diese Integration mit [Adobe Campaign-Version 8.4 oder höher](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | Die [!DNL Salesforce CRM] Das Ziel wurde aktualisiert, um sowohl Kontakt- als auch Lead-Aktualisierungen sowie Leistungsverbesserungen für schnellere Aktualisierungen zu unterstützen. |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Dokumentation**

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| Dokumentation zur API für Zielflussdienst-API | Die [Referenzdokumentation zur Ziel-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) wurde aktualisiert und enthält Anleitungen zum Ausführen von Vorgängen für dateibasierte Ziele. Vorgänge für Streaming-Ziele werden zu einem späteren Zeitpunkt hinzugefügt. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Benutzeroberflächenunterstützung für Auflistungen und empfohlene Werte | Zusätzlich zu den Auflistungen, die die Datenvalidierung ermöglichen, können Sie jetzt [vorgeschlagene Werte hinzufügen oder entfernen](../../xdm/ui/fields/enum.md) für standardmäßige oder benutzerdefinierte Zeichenfolgenfelder, sodass Platform-Benutzer über eine benutzerfreundliche Liste von Werten verfügen, aus denen sie beim Erstellen von Segmenten auswählen können. |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschaften eines bestimmten Elements, mit dem interagiert wurde, wodurch das Vorschlagsereignis ausgelöst wurde. |
| Feldergruppe | [[!UICONTROL Details zur MediaAnalytics-Interaktion]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Verfolgt Medieninteraktionen im Zeitverlauf. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Verfolgt Mediendetailinformationen. |
| Feldergruppe | [[!UICONTROL Adobe CJM ExperienceEvent - Oberflächen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschreibt Oberflächen für Erlebnisereignisse in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Verhalten | [[!UICONTROL Zeitreihen]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Werte hinzugefügt für `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Entfernte Werte für `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Feldergruppe | (Mehrfach) | [Mehrere Feldbeschreibungen wurden aktualisiert.](https://github.com/adobe/xdm/pull/1628/files) über Journey Orchestration-Komponenten hinweg. |
| Feldergruppe | (Mehrfach) | [Die Titel für mehrere Adobe Workfront-Komponenten wurden aktualisiert.](https://github.com/adobe/xdm/pull/1634/files) für Konsistenz. |
| Feldergruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Die Namespaces mehrerer Felder wurden in `xdm`. |
| Feldergruppe | [[!UICONTROL Gemeinsame Felder für Journey Orchestration-Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Es wurde ein neues Feld hinzugefügt. `isReadSegmentTriggerStartEvent`. |
| Feldergruppe | [[!UICONTROL Prognostizierte Wetter]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Die `xdm:uvIndex` -Feld zu einem ganzzahligen Typ hinzu und das `xdm` -Namespace in mehrere Felder, in denen fehlt. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` und `xdm:implementationDetails` wurden aus der Feldergruppe entfernt. |
| Datentyp | (Mehrfach) | [Mehrere Namen von Medieneigenschaften wurden aktualisiert](https://github.com/adobe/xdm/pull/1626/files) für Konsistenz über verschiedene Datentypen hinweg. |
| Datentyp | [[!UICONTROL Implementierungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Es wurden bekannte Namen für Flutter hinzugefügt. |
| Datentyp | [[!UICONTROL Details zum POI]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Der Datentyp kann jetzt eine Liste von Schlüssel-Wert-Paaren für Metadaten akzeptieren, die mit dem Zielpunkt verknüpft sind. |
| Datentyp | [[!UICONTROL Vorschlagsaktion]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion]. |
| Datentyp | [[!UICONTROL Vorschlagsereignistyp]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion]. |
| (Mehrfach) | (Mehrfach) | Experimentelle Eigenschaften wurden [stabilisiert über alle B2B-Komponenten hinweg](https://github.com/adobe/xdm/pull/1617/files). |
| (Mehrfach) | (Mehrfach) | Adobe Journey Optimizer-Entitäten wurden [stabilisiert](https://github.com/adobe/xdm/pull/1625/files). |
| (Mehrfach) | (Mehrfach) | Die Namespaces bestimmter Felder für verschiedene experimentelle Komponenten wurden [für Konsistenz aktualisiert](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Identity Service {#identity-service}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, wodurch jeder Kunde über mehrere &quot;Identitäten&quot;verfügt.

Mit Adobe Experience Platform Identity Service erhalten Sie einen besseren Überblick über Ihren Kunden und sein Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit für effektive, persönliche digitale Erlebnisse sorgen können.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Löschen von Datensätzen | Identity Service unterstützt jetzt das Löschen von Datensätzen, wenn über die [Catalog Service-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), Benutzeroberfläche oder Datenhygiene. Lesen Sie das Handbuch unter [Löschen von Datensätzen in der Benutzeroberfläche](../../catalog/datasets/user-guide.md#delete-a-dataset) für weitere Informationen. |

Weitere Informationen zum Identity Service finden Sie im Abschnitt [Identity Service - Übersicht](../../identity-service/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweis-API | Mit Adobe Experience Platform Query Service können Sie Warnhinweise für Ad-hoc-Abfragen und geplante Abfragen abonnieren. Warnhinweise können per E-Mail, über die Platform-Benutzeroberfläche oder beides empfangen werden. Zurzeit können Abfragewarnungen nur mit dem [Query Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/). Siehe [Dokumentation zu Abfragewarnungen](../../query-service/api/alert-subscriptions.md) , um mehr zu erfahren. |
| Datensatzbeispiele | Mit den Beispielen von Query Service-Datensätzen können Sie forschende Abfragen zu Big Data durchführen, wobei die Verarbeitungszeit auf Kosten der Genauigkeit der Abfrage erheblich verkürzt wird. Siehe [Beispiel-Handbuch für Datensätze](../../query-service/sql/dataset-samples.md) , um mehr zu erfahren. |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auswirkungen der Population des Audience Manager-Segments auf das Echtzeit-Kundenprofil | Die Erfassung umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mit der Audience Manager-Quelle an Platform senden. Das bedeutet, dass die Auswahl aller Segmente potenziell zu einer Profilanzahl führen kann, die über Ihrer Lizenznutzungsberechtigung liegt. Weitere Informationen finden Sie im Abschnitt [Übersicht über die Audience Manager-Quelle](../../sources/connectors/adobe-applications/audience-manager.md). Informationen zur Verwendung Ihrer Lizenz finden Sie in der Dokumentation unter [Verwenden des Dashboards zur Lizenznutzung](../../dashboards/guides/license-usage.md). |
| Unterstützung für Adobe Campaign Managed Cloud Service | Verwenden Sie die Adobe Campaign Managed Cloud Service-Quelle, um Ihre Adobe Campaign v8.4-Versand- und Trackinglog-Daten in die Experience Platform zu übertragen. Lesen Sie das Handbuch unter [Erstellen einer Adobe Campaign Managed Cloud Service-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/campaign.md) für weitere Informationen. |
| API-Unterstützung für On-Demand-Erfassung für Batch-Quellen | Verwenden Sie die On-Demand-Erfassung, um Ad-hoc-Fluss-Läufe für einen bestimmten Datenfluss mit dem [!DNL Flow Service] API. Die erstellten Flussläufe müssen auf eine einmalige Erfassung festgelegt werden. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der API](../../sources/tutorials/api/on-demand-ingestion.md) für weitere Informationen. |
| API-Unterstützung für Wiederholung fehlgeschlagener Datenflüsse für Batch-Quellen | Verwenden Sie die `re-trigger` -Vorgang verwenden, um Ihren fehlgeschlagenen Datenfluss über die API erneut auszuführen. Lesen Sie das Handbuch unter [Wiederholen fehlgeschlagener Datenfluss-Ausführungen mit der API](../../sources/tutorials/api/retry-flows.md) für weitere Informationen. |
| API-Unterstützung zum Filtern von Daten auf Zeilenebene für die [!DNL Google BigQuery] und [!DNL Snowflake] sources | Verwenden Sie logische und Vergleichsoperatoren, um Daten auf Zeilenebene für die [!DNL Google BigQuery] und [!DNL Snowflake] Quellen. Lesen Sie das Handbuch unter [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md) für weitere Informationen. |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).