---
title: Adobe Experience Platform - Versionshinweise, August 2022
description: Die Versionshinweise für Adobe Experience Platform vom August 2022.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: fb9fdc70aabb62cdc39888b1ff90557d8420c31b
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 99%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 24. August 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

KI/ML-Services ermöglichen es Marketing-Leuten und Fachleuten, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. Auf diese Weise können Marketing-Leute mithilfe von Konfigurationen auf Unternehmensebene Modelle erstellen, die speziell auf die Anforderungen eines Unternehmens zugeschnitten sind, ohne dass dafür datenwissenschaftliches Fachwissen erforderlich ist.

### Attributions-KI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für den Datenschutz | <ul><li> Die Attributions-KI unterstützt jetzt die Definition von Benutzerrollen und Zugriffsrichtlinien für die Verwaltung von [Berechtigungen](../../../help/access-control/abac/ui/permissions.md) für Funktionen und Objekte in einer Produktanwendung. </li><li>Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet.</li><li> Durch [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md), können Admins den Zugriff auf bestimmte Objekte und/oder Funktionen anhand bestimmter Attribute steuern. Dabei kann es sich um einem Objekt hinzugefügte Metadaten handeln, z. B. Beschriftungen. Admins können außerdem Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.</li><li>Die Attributions-KI nutzt Platform-Datensätze. Um Anfragen zu Verbraucherrechten zu unterstützen, die eine Marke erhalten kann, sollten Marken den Privacy Service von Platform nutzen, damit Verbraucher Anfragen zum Zugriff und zur Löschung ihrer Daten über den Data Lake, den Identity Service und das Echtzeit-Kundenprofil stellen können.  </li><li>Alle Datensätze, die für die Eingabe/Ausgabe von Modellen verwendet werden, folgen den Platform-Richtlinien. Die Platform-Datenverschlüsselung gilt für Daten in Ruhezeit und während der Übertragung. Weitere Informationen zur [Datenverschlüsselung](../../../help/landing/governance-privacy-security/encryption.md) finden Sie in der Dokumentation.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Hinweis**: Die Attributions-KI wird bis auf Weiteres nicht für bestehende Healthcare Shield- oder Privacy Shield-Kunden verfügbar sein.

Weitere Informationen zu Attributions-KI finden Sie in der Übersicht [Attributions-KI](../../intelligent-services/attribution-ai/overview.md).

### Kunden-KI

Kunden-KI in Real-time Customer Data Platform dient dazu, für einzelne Profile in gewünschten Umfang benutzerdefinierte Neigungswerte wie Abwanderung und Konversion zu generieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für den Datenschutz | <ul><li> Kunden-KI unterstützt jetzt die Definition von Benutzerrollen und Zugriffsrichtlinien, die der Verwaltung von [Berechtigungen](../../../help/access-control/abac/ui/permissions.md) für Funktionen und Objekte innerhalb einer Produktanwendung dienen. </li><li>Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet.</li><li> Durch [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md) können Admins den Zugriff auf bestimmte Objekte und/oder Funktionen auf der Grundlage bestimmter Attribute steuern. Bei diesen Attributen kann es sich um Metadaten handeln, die einem Objekt hinzugefügt werden, wie z. B. Beschriftungen. Admins können auch Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.</li><li>Die Kunden-KI nutzt die Platform-Datensätze. Um Anfragen zu Verbraucherrechten zu unterstützen, die eine Marke erhalten kann, sollten Marken den Privacy Service von Platform nutzen, damit Verbraucher Anfragen zum Zugriff und zur Löschung ihrer Daten über den Data Lake, den Identity Service und das Echtzeit-Kundenprofil stellen können. </li><li>Alle Datensätze, die für die Eingabe/Ausgabe von Modellen verwendet werden, folgen den Platform-Richtlinien. Die Platform-Datenverschlüsselung gilt für Daten in Ruhezeit und während der Übertragung. Weitere Informationen zur [Datenverschlüsselung](../../../help/landing/governance-privacy-security/encryption.md) finden Sie in der Dokumentation.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Hinweis**: Die Kunden-KI wird bis auf Weiteres nicht für bestehende Healthcare Shield- oder Privacy Shield-Kunden verfügbar sein.

Weitere Informationen zu Kunden-KI finden Sie in der Übersicht [Kunden-KI](../../intelligent-services/customer-ai/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards], mit denen Sie wichtige Einblicke in die Daten Ihrer Organisation erhalten, die in täglichen Snapshots erfasst werden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Geplante Aktivierungen-Widget | Das [!UICONTROL Geplante Aktivierungen]-Widget bietet eine tabellarische Übersicht über die zuletzt aktivierten Ziele. Für jedes Segment werden der Name, die Zielplattform sowie das Start- und Enddatum der Aktivierung angegeben. Mit diesem Widget können Sie auf einen Blick erkennen, wo und wann die Zielgruppe aktiviert wird, und es macht doppelte oder unnötige Aktivierungen transparenter. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden. |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Aufnehmen von Datensätzen mit Warnungen | Bei der Datenvorbereitung werden nun Warnungen (unkritische Fehler) in den Feldern lokalisiert, und der Rest der Zeile kann aufgenommen werden. Alle Mapper-Umwandlungsfehler werden jetzt als Warnungen gemeldet, und Zeilen, die teilweise aufgenommen wurden, werden als erfolgreich betrachtet, jedoch mit einer Warnung.  Die Überwachung wird auch für Datensätze mit Warnungen und Diagnosedetails unterstützt. Die teilweise Aufnahme von Datensätzen mit Warnungen ist derzeit nur für Streaming-Daten verfügbar. Weitere Informationen finden Sie in der Dokumentation zum [Aufnehmen von Datensätzen mit Warnungen](../../sources/tutorials/ui/monitor-streaming.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| (Beta) Attribut-basierte Personalisierungsunterstützung für Personalisierungsziele | Mit der Beta-Version der Attribut-basierten Personalisierung werden Sie zwei neue Karten im [Zielkatalog](../../destinations/catalog/overview.md) sehen: <ul><li>**[!UICONTROL Adobe Target V2]**: Dieser Connector befindet sich derzeit in der Beta-Phase und steht nur einer ausgewählten Zahl von Kunden zur Verfügung. Zusätzlich zu den Funktionen der Adobe Target V1-Karte fügt der Target V2-Connector dem Aktivierungs-Workflow einen [Zuordnungsschritt](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) hinzu, mit dem Sie Adobe Target Profilattribute zuordnen können, um eine Attribut-basierte Personalisierung auf derselben Seite und auf der nächsten Seite zu ermöglichen.</li><li>**[!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]**: Dieser Connector befindet sich derzeit in der Beta-Phase und steht nur einer ausgewählten Zahl von Kunden zur Verfügung. Zusätzlich zu den Funktionen der **[!UICONTROL benutzerdefinierten Personalisierung]** fügt der Connector **[!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]** dem Aktivierungs-Workflow einen optionalen [Zuordnungsschritt](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) hinzu, mit dem Sie Profilattribute Ihrem benutzerdefinierten Personalisierungsziel zuordnen können, was eine Attribut-basierte Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht.</li></ul> <br> Profilattribute können vertrauliche Daten enthalten. Um diese Daten zu schützen, erfordert das Ziel **[!UICONTROL Benutzerdefinierte Personalisierung mit Attributen]**, dass für die Datenerfassung die [Edge Network Server-API](../../server-api/overview.md) verwendet wird. Außerdem müssen alle Aufrufe der Server-API in einem [authentifizierten Kontext](../../server-api/authentication.md) erfolgen. |

{style=&quot;table-layout:auto&quot;}

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) ist eine Sales Execution-Plattform mit den weltweit meisten Daten zu B2B-Käufer-Verkäufer-Interaktionen und erheblichen Investitionen in proprietäre KI-Technologien zur Umwandlung von Verkaufsdaten in Intelligenz. [!DNL Outreach] unterstützt Unternehmen bei der Automatisierung des Vertriebsengagements und der Nutzung von Umsatzdaten, um ihre Effizienz, Vorhersagbarkeit und ihr Wachstum zu verbessern. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL AJO-Entitätsschema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Beschreibt denormalisierte Entitäten für Adobe Journey Optimizer. |
| Klasse | [[!UICONTROL AJO-Ausführungsentitäten]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Beschreibt Ausführungsentitäten von Adobe Journey Optimizer zur Verwendung in der Segmentierung. |
| Feldergruppe | [[!UICONTROL Workfront-Arbeitsobjekte]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Eine Wrapper-Feldergruppe, die auf alle objektspezifischen Feldgruppen der unteren Ebene für Adobe Workfront verweist. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Gemeinsame Felder für Journey Orchestration-Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Es wurden zwei neue Eigenschaften hinzugefügt: `origTimeStamp` und `experienceID`. |
| Feldergruppe | [[!UICONTROL Details zur Segmentzugehörigkeit]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Zusätzlich zum [!UICONTROL XDM-Individualprofil] kann diese Feldergruppe nun auch in Schemata verwendet werden, die auf der Klasse XDM Business Account basieren. |
| Feldergruppe | (Mehrfach) | Mehrere Feldergruppen, die sich auf Marketo B2B-Aktivitäten beziehen, wurden auf einen stabilen Status aktualisiert. Siehe die folgende [Pull-Anfrage](https://github.com/adobe/xdm/pull/1593/files) für weitere Details. |
| Feldergruppe | (Mehrfach) | Mehrere wetterbezogene Feldergruppen wurden aktualisiert, um Fehler zu beheben, die bei `uvIndex` und `sunsetTime` auftraten. Siehe die folgende [Pull-Anfrage](https://github.com/adobe/xdm/pull/1602/files) für weitere Details. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Eine neue Eigenschaft `productImageUrl` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Eine neue Eigenschaft `framesPerSecond` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` wurde in `appVersion` umbenannt. Die Felder `meta:enum` und `description` wurden ebenfalls aktualisiert. |
| Datentypen und Feldergruppen | (Mehrfach) | Mehrere Mediendatentypen und Feldergruppen verfügen über neue Felder und aktualisierte Beschreibungen. Siehe die folgende [Pull-Anfrage](https://github.com/adobe/xdm/pull/1582/files) für weitere Details. |
| (Alle) | (Mehrfach) | Alle Schemaobjekte, die ein `enum`-Feld enthalten, enthalten jetzt auch ein entsprechendes `meta:enum`-Feld, um die Anzeigewerte für jede Begrenzung anzugeben. Siehe die folgende [Pull-Anfrage](https://github.com/adobe/xdm/pull/1601/files) für weitere Details. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Feste Grenze für Zusammenführungsrichtlinien | Platform erzwingt jetzt eine feste Grenze von **fünf** Zusammenführungsrichtlinien pro Sandbox. Wenn Ihre Sandbox derzeit mehr als fünf Zusammenführungsrichtlinien hat, können Sie **keine** neuen Zusammenführungsrichtlinien erstellen, bis die Sandbox weniger als fünf Zusammenführungsrichtlinien hat. |
| Bereinigung verwaister Profilrandattribute | Für alle Organisationen entfernt der Profil-Service jetzt täglich übrig gebliebene Randattribute der Benutzeraktivitätsregion, um eine genauere Darstellung der Profile in Ihrem System zu erhalten. Diese Bereinigung erfolgt, nachdem alle Profilfragmente für ein bestimmtes Profil gelöscht wurden, und sollte sich auf Profile auswirken, die aus Datensätzen zusammengeführt werden, in denen `com_adobe_aep_profile_region_dataset` als `true` markiert ist. Dies kann zu einem Rückgang der Metrik „Adressierbare Zielgruppe“ im Lizenznutzungs-Dashboard und zu einem Rückgang der Metrik „Profilanzahl“ im Profil-Dashboard führen, da diese Metriken vor dieser Version übrig gebliebene Randattributfragmente einbezogen haben. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für 4000 Segmente | Für alle Organisationen mit Platform können jetzt bis zu 4000 Segmentdefinitionen unterstützt werden. Weitere Informationen darüber, wie sich diese Änderung auf die Segmentauftrags-APIs auswirkt, finden Sie im [Leitfaden für Segmentauftragsendpunkte](../../segmentation/api/segment-jobs.md). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von Selbstbedienungsquellen (Batch-SDK) | Entwickeln, testen und integrieren Sie Ihre REST-API-basierte Datenquelle, um Batch-Daten mithilfe einfacher Quellspezifikationen in Experience Platform aufzunehmen. Mit dem Quellen-SDK können Sie Folgendes tun: <ul><li>Konfigurieren Sie eine neue Quelle für den Experience Platform-Katalog.</li><li>Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen bezüglich der unterstützten Authentifizierungstypen, der Zeitplanung und der Art und Weise, wie Ressourcendaten abgerufen werden.</li><li>Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.</li></ul> Weitere Informationen finden Sie in der Dokumentation unter [Selbstbedienungsquellen (Batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allgemeine Verfügbarkeit der [!DNL Google BigQuery]-Quelle | Verwenden Sie die [!DNL Google BigQuery]-Quelle, um Daten aus Ihrem [!DNL Google BigQuery] Data Warehouse in Experience Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation zur [[!DNL Google BigQuery]  Quelle](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage]-Quelle (Beta) | Verwenden Sie die [!DNL Teradata Vantage]-Quelle, um Daten aus hybriden Multi-Cloud-Umgebungen in Experience Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation zur [[!DNL Teradata Vantage]  Quelle](../../sources/connectors/databases/teradata-vantage.md). |
| Regionsübergreifende Unterstützung für die Adobe Analytics-Quelle | Sie können jetzt Report Suites aus jeder Region (Vereinigte Staaten, Vereinigtes Königreich oder Singapur) aufnehmen. Report Suites müssen derselben Organisation zugeordnet sein wie die Experience Platform Sandbox-Instanz, in der die Quellverbindung erstellt wird. Weitere Informationen finden Sie im Handbuch zum [Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
