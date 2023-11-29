---
title: Adobe Experience Platform – Versionshinweise, September 2022
description: Versionshinweise September 2022 zu Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 1e9d6b0c43461902c5b966aa1d0576103e872e0c
workflow-type: tm+mt
source-wordcount: '2938'
ht-degree: 99%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 28. September 2022**

Neue Funktionen in Adobe Experience Platform:

- [Attributbasierte Zugriffssteuerung](#abac)

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
>Die attributbasierte Zugriffssteuerung wird ab Oktober 2022 aktiviert. Wenn Sie ein frühzeitiger Anwendender sein möchten, wenden Sie sich an den Adobe-Support-Mitarbeiter.

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzenden in Ihrer Organisation den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit der attributbasierten Zugriffssteuerung können Administratoren bzw. Administratorinnen Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung | Mit der attributbasierten Zugriffssteuerung können Sie Schemafelder und Segmente des Experience-Datenmodells (XDM) mit Kennzeichnungen versehen, die unterschiedliche Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Administrierende die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien für XDM-Schemafelder und Segmente zu definieren. Damit kann der Zugriff durch Benutzende oder Benutzergruppen (interne, externe oder Drittparteien) besser verwaltet werden. Weitere Informationen finden Sie in der [Übersicht über die attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md). |
| Berechtigungen | Berechtigungen sind der Bereich von Experience Cloud, in dem Administrierende Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten. Über Berechtigungen können Sie Rollen erstellen und verwalten, die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen und Richtlinien erstellen, um Kennzeichnungen zu nutzen und zu definieren, welche Benutzerrollen Zugriff auf bestimmte Platform-Ressourcen haben. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzende verwalten, die einer bestimmten Rolle zugeordnet sind. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche für Berechtigungen](../../access-control/abac/ui/browse.md). |

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

KI/ML-Services ermöglichen es Marketing-Leuten und Fachleuten, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. Auf diese Weise können Marketing-Leute mithilfe von Konfigurationen auf Unternehmensebene Modelle erstellen, die speziell auf die Anforderungen eines Unternehmens zugeschnitten sind, ohne dass dafür datenwissenschaftliches Fachwissen erforderlich ist.

### Attributions-KI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Fachleuten genutzt werden, um auf diversen Customer Journeys die Auswirkungen jedes einzelnen Marketing-Touchpoints zu quantifizieren.

| Funktion | Beschreibung |
| --- | --- |
| Entwurfsinstanz speichern | Diese neue Funktion ermöglicht es Marketing-Analysten und -Analystinnen, eine Modellkonfiguration vor dem Training und Scoring als Entwurfsinstanz zu speichern und weiter zu bearbeiten. Diese Funktion ist beispielsweise dann hilfreich, wenn Benutzende mehrere Felder im Workflow definieren müssen, dies aber aus Zeitgründen nicht möglich ist. Diese Funktion ist auch nützlich, wenn eine oder mehrere Datensatzstatistiken gerade verarbeitet werden und noch nicht verfügbar sind. Lesen Sie für weitere Informationen das [Benutzerhandbuch zur Attributions-KI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies). |
| Governance-Richtlinien | Nachdem Benutzende die Erstellung einer Instanz über den Konfigurations-Workflow übermittelt haben, prüft der neue Service zur Richtliniendurchsetzung, ob Richtlinienverletzungen bei der Datennutzung vorliegen, und zeigt die Details in einem Popup an. Dadurch wird sichergestellt, dass Datenvorgänge und Marketing-Aktionen mit den in Adobe Experience Platform konfigurierten Datennutzungsrichtlinien konform sind. |

Weitere Informationen zur Attributions-KI finden Sie in der [Übersicht zur Attributions-KI](../../intelligent-services/attribution-ai/overview.md). Informationen über Richtlinien zur Daten-Governance finden Sie in der [Übersicht zu Richtlinien](../../data-governance/policies/overview.md).

### Kunden-KI

Die in Real-time Customer Data Platform verfügbare Kunden-KI dient dazu, in großem Umfang benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile zu generieren.

| Funktion | Beschreibung |
| --- | --- |
| Entwurfsinstanz speichern | Diese neue Funktion ermöglicht es Marketing-Analysten und -Analystinnen, eine Modellkonfiguration vor dem Training und Scoring als Entwurfsinstanz zu speichern und weiter zu bearbeiten. Diese Funktion ist beispielsweise dann hilfreich, wenn Benutzende mehrere Felder im Workflow definieren müssen, dies aber aus Zeitgründen nicht möglich ist. Diese Funktion ist auch nützlich, wenn eine oder mehrere Datensatzstatistiken gerade verarbeitet werden und noch nicht verfügbar sind. Lesen Sie das [Benutzerhandbuch für Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies), um mehr zu erfahren. |
| Governance-Richtlinien | Nachdem Benutzende die Erstellung einer Instanz über den Konfigurations-Workflow übermittelt haben, prüft der neue Service zur Richtliniendurchsetzung, ob Richtlinienverletzungen bei der Datennutzung vorliegen, und zeigt die Details in einem Popup an. Dadurch wird sichergestellt, dass Datenvorgänge und Marketing-Aktionen mit den in Adobe Experience Platform konfigurierten Datennutzungsrichtlinien konform sind. |

Weitere Informationen zur Kunden-KI finden Sie in der [Übersicht zur Kunden-KI](../../intelligent-services/customer-ai/overview.md). Informationen über die Richtlinien zu Daten-Governance finden Sie unter [Richtlinien-Übersicht](../../data-governance/policies/overview.md).

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität in Verbindung mit verschiedenen Services und Funktionen überprüfen. Die Auditprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Aktualisierte Funktionen**

| Funktion | Name | Beschreibung |
| --- | --- | --- |
| Ressourcen hinzugefügt | <ul><li>Attributions-KI-Instanz</li><li>Kunden-KI-Instanz</li><li>Datenstrom</li></ul> | Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet. Wenn die Funktion aktiviert ist, müssen Sie die Protokollerfassung nicht manuell aktivieren. |

{style="table-layout:auto"}

Weitere Informationen zu den verschiedenen ressourcenspezifischen Ereignistypen, die von Audit-Protokollen in Platform verfolgt werden, finden Sie in der [Übersicht zu Audit-Protokollen](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Insights zu den Daten Ihres Unternehmens erhalten, die in täglichen Snapshots erfasst werden.

| Funktion | Beschreibung |
| --- | --- |
| Kennzeichnung „In Verwendung“ | Wenn Sie in der Widget-Bibliothek nachschauen, können Sie anhand der Kennzeichnung „In Verwendung“ leicht erkennen, ob Widgets in Ihrem Dashboard vorhanden sind. Dadurch lässt sich die Duplizierung einfach vermeiden. Trotzdem können Sie dasselbe Widget mehr als einmal hinzufügen. |
| Benutzerdefinierte Dashboards | Benutzerdefinierte Dashboards helfen Ihnen, Insights schneller anzuzeigen und Visualisierungen anzupassen, indem Sie benutzerdefinierte Dashboards erstellen und verwalten. Mit benutzerdefinierten Dashboards können Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten, um für Ihr Unternehmen relevante Schlüsselmetriken zu visualisieren. Weitere Informationen finden Sie im [Funktionshandbuch](../../dashboards/user-defined-dashboards.md). |
| Datenmodell von Customer Data Platform Insights | Die Insights-Datenmodell-Funktion von Customer Data Platform (CDP) stellt die Datenmodelle und SQL zur Verfügung, die den Insights für verschiedene Profil-, Ziel- und Segmentierungs-Widgets zugrunde liegen. Sie können diese SQL-Abfragevorlagen anpassen, um CDP-Berichte für Marketing-Zwecke und Key Performance Indicators zu erstellen. Diese Insights können dann als benutzerdefinierte Widgets für benutzerdefinierte Dashboards verwendet werden. Weitere Informationen finden Sie im [Handbuch zu Funktionen des CDP-Insights-Datenmodells](../../dashboards/cdp-insights-data-model.md). |
| Widget für Bericht zur Zielgruppenüberschneidung | Dieses Widget ist sowohl für [!UICONTROL Profil-] als auch für [!UICONTROL Segment]-Dashboards verfügbar. Der Bericht bietet eine geordnete Liste von Zielgruppen, die nach den höchsten oder niedrigsten Überschneidungsprozentsätzen für Ihr ausgewähltes Segment sortiert sind. Vom [!UICONTROL Profil]-Dashboard aus können Sie Zielgruppenüberschneidungen nach Zusammenführungsrichtlinien aus allen verfügbaren Segmenten filtern und anzeigen. Mit [!UICONTROL Segment]-Dashboards können Sie Zielgruppenüberschneidungen nach einem bestimmten Segment filtern.<br>Verwenden Sie diese Analyse, um neue leistungsstarke Segmente zu erstellen und um zu vermeiden, dass dieselbe Zielgruppe an verschiedene Ziele gesendet wird. Der Bericht hilft auch, versteckte Insights zu identifizieren. So können Sie die Segmentierung verbessern oder eindeutige Profile finden, die verfolgt werden sollen. Weitere Informationen zu [Profilen](../../dashboards/guides/profiles.md#audience-overlap-report) und [Segmenten](../../dashboards/guides/audiences.md#audience-overlap-report) finden Sie in den Widget-Handbüchern. |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Integration der linken Navigation in der Platform-Benutzeroberfläche | Alle Funktionen, die bisher ausschließlich in der Benutzeroberfläche für die Datenerfassung enthalten waren (einschließlich Tags, Ereignisweiterleitung und Datenströme), sind jetzt auch über die linke Navigationsleiste von Experience Platform unter der Kategorie **[!UICONTROL Datenerfassung]** verfügbar Dadurch entfällt die Notwendigkeit, beim Arbeiten mit Datenerfassungsfunktionen in Platform zwischen Benutzeroberflächen zu wechseln. |
| Benutzerattribution in Tags und Ereignisweiterleitung | Bei der Auflistung verfügbarer [!UICONTROL Eigenschaften] in Tags und bei der Ereignisweiterleitung wird jetzt für jede aufgelistete Eigenschaft angezeigt, wann sie zuletzt aktualisiert wurde und von welchem Benutzenden die Aktualisierung vorgenommen wurde. |
| [[!DNL Snap Conversions API] Erweiterung](https://exchange.adobe.com/apps/ec/108550) für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an die [!DNL Snapchat Conversions API] senden. Weitere Informationen zur Authentifizierung und Verwendung der API finden Sie in der [[!DNL Snapchat Marketing API] Dokumentation](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] im Web SDK](../../edge/fundamentals/user-agent-client-hints.md) | Web-SDK unterstützt jetzt [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Mit Client-Hinweisen können Website-Besitzer auf viele der Informationen zugreifen, die auch in der [!DNL User-Agent]-Zeichenfolge enthalten sind, allerdings auf eine Weise, die die Privatsphäre besser schützt. |
| [Seitenweise Migration zu Web SDK](../../edge/home.md#migrating-to-web-sdk) | Sie können jetzt Ihre vorhandenen Web-Eigenschaften aus anderen Bibliotheken von Experience Cloud, wie etwa [!DNL at.js], Seite für Seite ins Web-SDK migrieren. Dies ermöglicht einen stufenweisen Ansatz für die Web-SDK-Migration, sodass nicht alle Seiten gleichzeitig migriert werden müssen. |
| [[!DNL Adobe Journey Optimizer] Unterstützung für Datenströme](../../datastreams/overview.md#aep) | Der Adobe Experience Platform-Service für Datenströme unterstützt jetzt [!DNL Adobe Journey Optimizer]. Mit dieser Option können Sie Web- und App-basierte eingehende Kanäle in [!DNL Adobe Journey Optimizer] verwenden. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| Destination SDK | Destination SDK bietet jetzt vollständige Unterstützung für Partner und Kunden, die Batch- oder dateibasierte produktbezogene oder private Ziele erstellen. Weitere Informationen finden Sie auf den folgenden Dokumentationsseiten: <ul><li>[Übersicht über Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Konfigurieren eines dateibasierten Ziels](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Testen von dateibasierten Zielen](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services bietet eine Plattform für die Gestaltung kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Orchestrierung von Kampagnen, das Management von Interaktionen in Echtzeit und die kanalübergreifende Ausführung. [Erste Schritte mit Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=de). Beachten Sie, dass diese Integration mit [Adobe Campaign-Version 8.4 oder höher](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1) kompatibel ist. |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | Das Ziel [!DNL Salesforce CRM] wurde aktualisiert und unterstützt jetzt sowohl Kontakt- als auch Lead-Aktualisierungen sowie Leistungsverbesserungen für schnellere Aktualisierungen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| Dokumentation zur Destinations Flow Service-API | Die [Referenzdokumentation zur Destinations API](https://developer.adobe.com/experience-platform-apis/references/destinations/) wurde aktualisiert und enthält jetzt Anleitungen zum Ausführen von Vorgängen für dateibasierte Ziele. Vorgänge für Streaming-Ziele werden zu einem späteren Zeitpunkt hinzugefügt. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Benutzeroberflächenunterstützung für Auflistungen und empfohlene Werte | Zusätzlich zu den Auflistungen, die die Datenvalidierung ermöglichen, können Sie jetzt [vorgeschlagene Werte für standardmäßige oder benutzerdefinierte Zeichenfolgenfelder hinzufügen oder entfernen](../../xdm/ui/fields/enum.md). Damit verfügen Platform-Benutzer über eine benutzerfreundliche Liste von Werten, aus denen sie beim Erstellen von Segmenten auswählen können. |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldgruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschaften eines bestimmten Elements, mit dem interagiert wurde, wodurch das Vorschlagsereignis ausgelöst wurde. |
| Feldergruppe | [[!UICONTROL Details zur MediaAnalytics-Interaktion]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Verfolgt Medieninteraktionen im Zeitverlauf. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Verfolgt Informationen zu Mediendetails. |
| Feldergruppe | [[!UICONTROL Adobe CJM ExperienceEvent – Oberflächen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschreibt Oberflächen für Erlebnisereignisse in Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Verhalten | [[!UICONTROL Zeitreihe]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Hinzugefügte Werte für `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Entfernte Werte für `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Feldgruppe | (Mehrfach) | [Mehrere Feldbeschreibungen](https://github.com/adobe/xdm/pull/1628/files) wurden in Journey-Orchestration-Komponenten aktualisiert. |
| Feldgruppe | (Mehrfach) | [Titel mehrerer Komponenten von Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) wurden aus Konsistenzgründen aktualisiert. |
| Feldergruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Die Namespaces mehrerer Felder wurden auf `xdm` aktualisiert. |
| Feldergruppe | [[!UICONTROL Gemeinsame Felder für Journey Orchestration-Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Neues Feld `isReadSegmentTriggerStartEvent` hinzugefügt. |
| Feldergruppe | [[!UICONTROL Prognostiziertes Wetter]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Das Feld `xdm:uvIndex` wurde in einen ganzzahligen Typ geändert und der Namespace `xdm` wurde zu mehreren Feldern hinzugefügt, in denen er gefehlt hat. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` und `xdm:implementationDetails` wurden aus der Feldergruppe entfernt. |
| Datentyp | (Mehrfach) | [Mehrere Namen von Medieneigenschaften](https://github.com/adobe/xdm/pull/1626/files) wurden aus Konsistenzgründen in verschiedenen Datentypen aktualisiert. |
| Datentyp | [[!UICONTROL Implementierungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Bekannte Namen für Flutter hinzugefügt. |
| Datentyp | [[!UICONTROL Interessenspunktdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Der Datentyp akzeptiert jetzt eine Liste von Schlüssel-Wert-Paaren für Metadaten, die mit dem Interessenspunkt verknüpft sind. |
| Datentyp | [[!UICONTROL Vorschlagsaktion]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion] umbenannt. |
| Datentyp | [[!UICONTROL Vorschlagsereignistyp]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion] umbenannt. |
| (Mehrfach) | (Mehrfach) | Experimentelle Eigenschaften wurden [in allen B2B-Komponenten stabilisiert](https://github.com/adobe/xdm/pull/1617/files). |
| (Mehrfach) | (Mehrfach) | Adobe Journey Optimizer-Entitäten wurden [stabilisiert](https://github.com/adobe/xdm/pull/1625/files). |
| (Mehrfach) | (Mehrfach) | Die Namespaces bestimmter Felder für verschiedene experimentelle Komponenten wurden [aktualisiert, um Konsistenz zu gewährleisten](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Identity Service {#identity-service}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten auf unterschiedliche Systeme verteilt gespeichert werden, sodass jeder Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und Kundinnen und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle, persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Löschen von Datensätzen | Identity Service unterstützt jetzt das Löschen von Datensätzen über die [Katalog-Service-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), die Benutzeroberfläche oder eine Datenhygieneanfrage. Weitere Informationen finden Sie im Handbuch unter [Löschen von Datensätzen in der Benutzeroberfläche](../../catalog/datasets/user-guide.md#delete-a-dataset). |

Weitere Informationen zu Identity Service finden Sie im Abschnitt [Identity Service – Übersicht](../../identity-service/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweis-Abonnement-API | Mit dem Adobe Experience Platform-Abfrage-Service können Sie Warnhinweise für ungeplante und geplante Abfragen abonnieren. Warnhinweise können per E-Mail, über die Platform-Benutzeroberfläche oder über beide empfangen werden. Zurzeit können Abfrage-Warnhinweise nur mit der [Abfrage-Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/) abonniert werden. |
| Datensatzbeispiele | Mit den Muster-Datensätzen des Abfrage-Service können Sie explorative Abfragen zu Big Data durchführen. Dies verkürzt die Verarbeitungszeit, während die Abfragegenauigkeit verringert wird. Weitere Informationen erhalten Sie im [Handbuch zu Datensatzmustern](../../query-service/key-concepts/dataset-samples.md). |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

Weitere Informationen erhalten Sie in der [Dokumentation zu Abfrage-Warnhinweisen](../../query-service/api/alert-subscriptions.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auswirkungen der Audience Manager-Segmentpopulation auf das Echtzeit-Kundenprofil | Die Aufnahme umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mithilfe der Audience Manager-Quelle an Platform senden. Das bedeutet, dass die Auswahl aller Segmente eine Profilanzahl ergeben kann, die über Ihrer Lizenznutzungsberechtigung liegt. Weitere Informationen finden Sie im Abschnitt [Übersicht über die Audience Manager-Quelle](../../sources/connectors/adobe-applications/audience-manager.md). Informationen zur Lizenznutzung finden Sie in der Dokumentation unter [Verwenden des Dashboards zur Lizenznutzung](../../dashboards/guides/license-usage.md). |
| Unterstützung für Adobe Campaign Managed Cloud Service | Verwenden Sie die Adobe Campaign Managed Cloud Service-Quelle, um Ihre Versand- und Trackinglog-Daten von Adobe Campaign v8.4 nach Experience Platform zu übertragen. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Adobe Campaign Managed Cloud Service-Quellverbindung über die Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/campaign.md). |
| API-Unterstützung für On-Demand-Aufnahme bei Batch-Quellen | Verwenden Sie die On-Demand-Aufnahme, um mit der [!DNL Flow Service]-API für einen bestimmten Datenfluss Ad-hoc-Flussausführungen zu erstellen. Die erstellten Flussausführungen müssen auf eine einmalige Aufnahme eingestellt sein. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Flussausführung für die On-Demand-Aufnahme mithilfe der API](../../sources/tutorials/api/on-demand-ingestion.md). |
| API-Unterstützung für die Wiederholung fehlgeschlagener Datenflussausführungen für Batch-Quellen | Verwenden Sie den Vorgang `re-trigger`, um Ihren fehlgeschlagenen Datenfluss über die API erneut zu versuchen. Weitere Informationen finden Sie im Handbuch unter [Wiederholen fehlgeschlagener Datenflussausführungen mithilfe der API](../../sources/tutorials/api/retry-flows.md). |
| API-Unterstützung bei der Filterung von Daten auf Zeilenebene, die von den Quellen [!DNL Google BigQuery] und [!DNL Snowflake] stammen | Verwenden Sie zum Filtern von Daten auf Zeilenebene, die von den Quellen [!DNL Google BigQuery] und [!DNL Snowflake] stammen, logische Operatoren und Vergleichsoperatoren. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md). |

Weiterführende Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
