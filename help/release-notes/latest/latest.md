---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 0e23475fd120858b59794742860b7afececfece2
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 36%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 24. August 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Experience-Datenmodell (XDM)](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

KI/ML-Services ermöglichen es Marketing-Analysten und -Praktikern, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Modelle für die Anforderungen eines Unternehmens einrichten, ohne dass datenwissenschaftliche Kenntnisse erforderlich sind.

### Attributions-KI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Datenschutz | <li>Attribution AI unterstützt jetzt die Definition von Benutzerrollen und Zugriffsrichtlinien für die Verwaltung von [Berechtigungen](../../../help/access-control/abac/ui/permissions.md) für Funktionen und Objekte in einer Produktanwendung.</li><li>Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet.</li><li>bis [attributbasierte Zugriffssteuerung](../../../help/access-control/abac/overview.md), können Administratoren den Zugriff auf bestimmte Objekte und/oder Funktionen anhand bestimmter Attribute steuern. Dabei kann es sich um einem Objekt hinzugefügte Metadaten handeln, z. B. Beschriftungen. Administratoren können außerdem Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.</li><li>[Datenhygiene](../../../help/hygiene/home.md) -Funktionen innerhalb von Attribution AI ermöglichen es Ihnen, aktualisierte Daten nur für Weiterbildung und Scoring zu verwenden. Wenn Sie Daten löschen möchten, verwendet Attribution AI auch nicht die gelöschten Daten.</li><li>Attribution AI nutzt Platform-Datensätze. Um die Einhaltung der DSGVO zu erleichtern, können Sie mit Adobe Experience Platform Privacy Service Protokolle einrichten, um Kundenanfragen beim Zugriff auf und Löschen ihrer Daten im Data Lake, Identity Service und Echtzeit-Kundenprofil zu berücksichtigen. Alle Daten werden im Transit und im Ruhezustand verschlüsselt.</li> |

{style=&quot;table-layout:auto&quot;}

**Hinweis**: Attribution AI wird erst Ende 4. Quartal 2022 für Kunden des Gesundheitsschilds verfügbar sein.

Weitere Informationen zu Attribution AIS finden Sie im [Attribution AI](../../intelligent-services/attribution-ai/overview.md) Übersicht.

### Kunden-KI

Kunden-KI in Real-time Customer Data Platform dient dazu, für einzelne Profile in gewünschten Umfang benutzerdefinierte Neigungswerte wie Abwanderung und Konversion zu generieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Datenschutz | <li>Customer AI unterstützt jetzt die Definition von Benutzerrollen und Zugriffsrichtlinien zur Verwaltung [Berechtigungen](../../../help/access-control/abac/ui/permissions.md) für Funktionen und Objekte in einer Produktanwendung.</li><li>Die Administratorprotokoll-Ressourcen werden automatisch aufgezeichnet, wenn die Aktivität stattfindet.</li><li> bis [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md), können Administratoren den Zugriff auf bestimmte Objekte und/oder Funktionen anhand bestimmter Attribute steuern. Diese Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. Beschriftungen. Administratoren können auch Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.</li><li>[Datenhygiene](../../../help/hygiene/home.md) Funktionen innerhalb von Customer AI ermöglichen Ihnen, aktualisierte Daten nur für Weiterbildung und Scoring zu verwenden. Auf ähnliche Weise verzichtet Customer AI bei der Anforderung, Daten zu löschen, auf die Verwendung der gelöschten Daten.</li><li>Customer AI nutzt Platform-Datensätze. Um die Einhaltung der DSGVO zu erleichtern, können Sie mit Adobe Experience Platform Privacy Service Protokolle einrichten, um Kundenanfragen beim Zugriff auf und Löschen ihrer Daten im Data Lake, Identity Service und Echtzeit-Kundenprofil zu berücksichtigen. Alle Daten werden im Transit und im Ruhezustand verschlüsselt.</li> |

{style=&quot;table-layout:auto&quot;}

**Hinweis**: Kunden-KI wird erst Ende 4. Quartal 2022 für Kunden von Health Care Shield verfügbar sein.

Weitere Informationen zu Customer AI finden Sie im [Customer AI](../../intelligent-services/customer-ai/overview.md) Übersicht.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards] durch die Sie wichtige Einblicke in die Daten Ihres Unternehmens anzeigen können, wie sie bei täglichen Momentaufnahmen erfasst werden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget zur geplanten Aktivierung | Die [!UICONTROL Geplante Aktivierungen] -Widget bietet eine tabellarisierte Ansicht der zuletzt aktivierten Ziele. Sie enthält für jedes Segment den Namen, die Zielplattform sowie das Start- und Enddatum der Aktivierung. Mit diesem Widget können Sie auf einen Blick erkennen, wo und wann die Audience aktiviert wird, und doppelte oder unnötige Aktivierungen transparenter machen. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden. |

Weitere Informationen zu [!DNL Dashboards] finden Sie in der [[!DNL Dashboards] Übersicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für die Aufnahme von Datensätzen mit Warnungen | Die Datenvorbereitung lokalisiert nun Warnungen (nicht kritische Fehler) in die Felder und ermöglicht die Erfassung des restlichen Teils der Zeile. Alle Mapper-Transformationsfehler werden jetzt als Warnungen und teilweise aufgenommene Zeilen als erfolgreich gemeldet, mit einer Warnung.  Die Überwachung wird auch für Datensätze mit Warnungen und Diagnosedetails unterstützt. Die partielle Erfassung von Datensätzen mit Warnungen ist derzeit nur für Streaming-Daten verfügbar. Lesen Sie die Dokumentation unter [Erfassen von Datensätzen mit Warnungen](../../sources/tutorials/ui/monitor-streaming.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen über [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Globales Schema | [[!UICONTROL AJO-Entitätsschema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Beschreibt denormalisierte Entitäten für Adobe Journey Optimizer. |
| Klasse | [[!UICONTROL AJO-Ausführungsentitäten]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Beschreibt Ausführungsentitäten von Adobe Journey Optimizer zur Verwendung in der Segmentierung. |
| Feldergruppe | [[!UICONTROL Workfront-Arbeitsobjekte]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Eine Wrapper-Feldergruppe, die auf alle objektspezifischen Feldergruppen der unteren Ebene für Adobe Workfront verweist. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Allgemeine Felder für Journey Orchestration Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Zwei neue Eigenschaften wurden hinzugefügt: `origTimeStamp` und `experienceID`. |
| Feldergruppe | [[!UICONTROL Details zur Segmentzugehörigkeit]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Zusätzlich zu [!UICONTROL XDM Individual Profile]festgelegt ist, kann diese Feldergruppe jetzt auch in Schemas verwendet werden, die auf der XDM Business Account-Klasse basieren. |
| Feldergruppe | (Mehrere) | Mehrere Feldergruppen im Zusammenhang mit Marketo B2B-Aktivitäten wurden auf den Status &quot;stabil&quot;aktualisiert. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1593/files) für Details. |
| Feldergruppe | (Mehrere) | Mehrere wetterbezogene Feldergruppen wurden aktualisiert, um Fehler zu beheben, die bei `uvIndex` und `sunsetTime`. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1602/files) für Details. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Eine neue Eigenschaft `productImageUrl` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Eine neue Eigenschaft `framesPerSecond` wurde hinzugefügt. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` wurde in `appVersion` umbenannt. `meta:enum` und `description` -Felder wurden ebenfalls aktualisiert. |
| Datentypen und Feldergruppen | (Mehrere) | Mehrere Mediendaten und Feldergruppen verfügen über neue Felder und aktualisierte Beschreibungen. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1582/files) für Details. |
| (Alle) | (Mehrere) | Alle Schemaobjekte, die eine `enum` -Feld enthält jetzt auch die entsprechende `meta:enum` -Feld, um die Anzeigewerte für jede Begrenzung anzugeben. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1601/files) für Details. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Bereinigung der verwaisten Profilattribute | Für alle Organisationen entfernt der Profildienst jetzt täglich die Attribute der Region der Benutzeraktivität, die übrig geblieben sind, um eine genauere Darstellung Ihrer Profile in Ihrem System zu erhalten. Diese Bereinigung erfolgt, nachdem alle Profilfragmente für ein bestimmtes Profil gelöscht wurden, und sollte sich auf die Zusammenführung von Profilen aus Datensätzen auswirken, in denen `com_adobe_aep_profile_region_dataset` als `true`. Dies kann zu einem Rückgang der Metrik „Adressierbare Zielgruppe“ im Lizenznutzungs-Dashboard und zu einem Rückgang der Metrik „Profilanzahl“ im Profil-Dashboard führen, da diese Metriken vor der Einführung dieser Version übrig gebliebene Randattributfragmente einbezogen haben. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für 4000 Segmente | Alle Organisationen mit Platform können jetzt bis zu 4000 Segmentdefinitionen unterstützen. Weitere Informationen dazu, wie sich diese Änderung auf die APIs für Segmentaufträge auswirkt, finden Sie im Abschnitt [Handbuch zum Segmentauftragsendpunkt](../../segmentation/api/segment-jobs.md) |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von Self-Serve-Quellen (Batch-SDK) | Entwickeln, testen und integrieren Sie Ihre REST API-basierte Datenquelle, um Batch-Daten mithilfe einfacher Quellspezifikationen in Experience Platform zu erfassen. Mit dem Sources-SDK können Sie: <ul><li>Konfigurieren Sie eine neue Quelle für den Experience Platform-Katalog.</li><li>Definieren Sie Spezifikationen für Ihre Quelle, einschließlich Informationen zu unterstützten Authentifizierungstypen, Planung und Art und Weise, wie Ressourcendaten abgerufen werden.</li><li>Erstellen Sie eine benutzerfreundliche Dokumentation für Ihre neue Quelle.</li></ul> Weitere Informationen finden Sie in der Dokumentation unter [Self-Serve-Quellen (Batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allgemeine Verfügbarkeit der [!DNL Google BigQuery]-Quelle | Verwenden Sie die [!DNL Google BigQuery] -Quelle, um Daten aus Ihrem [!DNL Google BigQuery] Data Warehouse in Experience Platform. Weitere Informationen finden Sie in der Dokumentation unter [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (Beta) | Verwenden Sie die [!DNL Teradata Vantage] -Quelle, um Daten aus hybriden Multi-Cloud-Umgebungen in Experience Platform zu erfassen. Weitere Informationen finden Sie in der Dokumentation unter [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Regionsübergreifende Unterstützung für Adobe Analytics-Quellen | Sie können jetzt Report Suites aus einer beliebigen Region (USA, Großbritannien oder Singapur) erfassen. Report Suites müssen derselben Organisation wie die Experience Platform-Sandbox-Instanz zugeordnet sein, in der die Quellverbindung erstellt wird. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| API-Unterstützung für On-Demand-Erfassung | Verwenden Sie die On-Demand-Erfassung, um Ad-hoc-Fluss-Läufe für einen bestimmten Datenfluss mit dem [!DNL Flow Service] API. Die erstellten Flussläufe müssen auf eine einmalige Erfassung festgelegt werden. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Flusslaufs für die On-Demand-Erfassung mithilfe der API](../../sources/tutorials/api/on-demand-ingestion.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).