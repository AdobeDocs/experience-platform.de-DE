---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: def32d9667c4630de760d228c88676eb9d5a6de4
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 37%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 22. Juni 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Collection]](#data-collection)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Konfiguration des Zugriffstyps für Datenspeicher](../../edge/datastreams/overview.md#create) | Beim Erstellen eines neuen Datastreams können Sie jetzt auswählen, welche Art von Anforderungen das Edge-Netzwerk akzeptieren soll: <ul><li>**[!UICONTROL Gemischte Authentifizierung]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network sowohl authentifizierte als auch nicht authentifizierte Anfragen. Wählen Sie diese Option, wenn Sie das Web SDK oder das [Mobile SDK](https://aep-sdks.gitbook.io/docs/) zusammen mit der [Server-API](../../server-api/overview.md) verwenden möchten. </li><li>**[!UICONTROL Nur authentifiziert]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network nur authentifizierte Anfragen. Wählen Sie diese Option aus, wenn Sie nur die Server-API verwenden und verhindern möchten, dass nicht authentifizierte Anforderungen vom [!DNL Edge Network] verarbeitet werden. </li></ul> |
| [Vorschläge rendern](../../edge/personalization/rendering-personalization-content.md#applypropositions) in Einzelseitenanwendungen ohne Erhöhung der Metriken. | Die neu hinzugefügte `applyPropositions` -Befehl ermöglicht es Ihnen, ein Array von Vorschlägen aus [!DNL Target] in Einzelseitenanwendungen, ohne die [!DNL Analytics] und [!DNL Target] Metriken. Dies erhöht die Genauigkeit der Berichterstellung. |
| [Freigabe von Mobilgeräte für das Internet und domänenübergreifende IDs](../../edge/identity/id-sharing.md) | Das Adobe Experience Platform Web SDK unterstützt jetzt Funktionen zur Freigabe von Besucher-IDs, mit denen Sie personalisierte Erlebnisse präziser zwischen mobilen Apps und mobilen Webinhalten sowie domänenübergreifend bereitstellen können. |

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## [!DNL Data Science Workspace] {#dsw}

 Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Eine der Möglichkeiten, dies mit Data Science Workspace zu erreichen, ist die Verwendung von JupyterLab. JupyterLab ist eine Web-basierte Benutzeroberfläche für <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten.

| Funktion | Beschreibung |
| --- | --- |
| JupyterLab Launcher | Der JupyterLab Launcher enthält jetzt Starter für Spark 3.2 Notebooks. Spark 2.4 Notebook-Starter werden jetzt durch Spark 3.2 Notebooks ersetzt und werden Teil dieser Version sein. |
| Spark 3.2 | Neue Scala (Spark)- und PySpark-Rezepte verwenden jetzt Spark 3.2 |
| Kernels | Scala (Spark) Notebooks werden jetzt über den Scala-Kernel erstellt. PySpark-Notebooks werden jetzt über den Python-Kernel erstellt. Der Spark- und PySpark-Kernel sind veraltet und werden in einer nachfolgenden Version entfernt. |
| Rezepte | Neue PySpark- und Spark-Rezepte folgen jetzt dem Docker-Workflow ähnlich wie Python- und R-Rezepte. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Data Science Workspace finden Sie unter [Übersichtsdokumentation](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| (Beta) Destination SDK-Unterstützung für [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) dateibasierte Ziele und [konfigurierbare Dateinamen](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | Sie können jetzt die Destination SDK verwenden, um Google Cloud-Speicher-Ziele zu erstellen und benutzerdefinierte Dateinamen für exportierte Dateien über Dateinamenmakros zu definieren. <br><br> Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern. |
| Segmentspalte im Datenfluss führt zu Batch-Zielen aus. | Für Datenflüsse, die zu Batch-Zielen ausgeführt werden, zeigt die Benutzeroberfläche jetzt den Namen des Segments an, das mit jedem Datenfluss verknüpft ist. Mehr dazu [Datenfluss wird zu Batch-Zielen ausgeführt](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | Die [!DNL Google Ad Manager 360] Verbindung aktiviert Batch-Upload für [!DNL publisher provided identifiers] (PPID) nach [!DNL Google Ad Manager 360]über [!DNL Google Cloud Storage] <br><br>Dieses Ziel befindet sich derzeit in der Betaversion und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. So fordern Sie Zugriff auf die [!DNL Google Ad Manager 360] Verbindung herstellen, kontaktieren Sie Ihren Kundenbetreuer und geben Sie Ihre [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Aktivieren Sie Profile für zielgerichtete Media-Umfragen und Feedback-Erfassung, um Kundenanforderungen und Erwartungen besser zu verstehen. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Die Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) Mit dem Ziel können Sie authentifizierte Erstanbietersegmente für zugelassene Advertiser und Benutzer freigeben, damit die Kampagne für DSP aktiviert werden kann. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL Medizin]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | Eine Klasse der Gesundheitsindustrie, die Details über einen Stoff erfasst, der für die medizinische Behandlung verwendet wird, insbesondere ein Arzneimittel oder ein Medikament. |
| Klasse | [[!UICONTROL Plan]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | Eine Klasse der Gesundheitsbranche, die Details zu einem medizinischen Plan erfasst, wie z. B. einen Krankenversicherungsplan oder einen Versicherungsplan. |
| Klasse | [[!UICONTROL Anbieter]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | Eine Klasse der Gesundheitsbranche, die Details über einen Gesundheitsdienstleister erfasst. |
| Klasse | [[!UICONTROL Player]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | Eine Klasse der Gesundheitsbranche, die Details über ein Versicherungsunternehmen erfasst. |
| Klasse | [[!UICONTROL Live-Ereigniszeitplan]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | Eine Sport- und Unterhaltungsbranchenklasse, die Details zu einem Live-Veranstaltungskalender erfasst, wie z. B. einen Fahrplan für ein Reisekonzert oder den Zeitplan eines Sportteams. |
| Klasse | [[!UICONTROL Ort ]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | Eine Sport- und Unterhaltungsindustrie, die den Standort einer Live-Veranstaltung erfasst, wie z. B. einen Konzerthaus oder eine Sportarena. |
| Feldergruppe | [[!UICONTROL Arzneimittel]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | Eine Feldergruppe für [!UICONTROL Medizin] -Klasse, die Details über die Medikation erfasst, wie z. B. Markenname, Losnummer und Menge. |
| Feldergruppe | [[!UICONTROL Details zum Gesundheitsplan]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | Eine Feldergruppe für [!UICONTROL Plan] -Klasse, die Details wie Netzwerk, Typ und aktiven Status erfasst. |
| Feldergruppe | [[!UICONTROL Gesundheitsdienstleister]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Eine Feldergruppe für [!UICONTROL Anbieter] -Klasse, die Details eines individuellen Gesundheitsberufs oder einer Gesundheitseinrichtung erfasst, die für die Erbringung von Gesundheitsdiagnosen und -therapiediensten zugelassen ist. |
| Feldergruppe | [[!UICONTROL Details zum Gesundheitsbetreuer]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Eine Feldergruppe für [!UICONTROL XDM Individual Profile] -Klasse, die Informationen zu einer Person erfasst, die über eine Dienstleistung oder Betreuung verfügt oder empfangen wird, wie Kontaktinformationen, medizinische Grundversorgung und Planinformationen. |
| Feldergruppe | [[!UICONTROL Sitetool-Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] -Klasse, die Informationen erfasst, die von Sitools wie Chatbot, Umfrage usw. erfasst werden. |
| Feldergruppe | [[!UICONTROL Kauf eines Live-Ereignis-Tickets]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] -Klasse, die die Einkaufsgeschichte für Eintrittskarten zu einer Live-Veranstaltung wie einem Konzert oder einem Sportspiel erfasst. |
| Feldergruppe | [[!UICONTROL Veranstaltungskalender für Sport und Unterhaltung]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | Eine Feldergruppe für [!UICONTROL Live-Ereigniszeitplan] -Klasse, die weitere Details zum Zeitplan erfasst, wie z. B. den Namen der Attraktion, Öffnungszeiten der Tür und mehr. |
| Feldergruppe | [[!UICONTROL Veranstaltungsort für Sportunterhaltung]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | Eine Feldergruppe für [!UICONTROL Standort] -Klasse, die weitere Details zum Veranstaltungsort erfasst, wie Sitzplatzkapazität und Designated Market Areas (DMAs). |
| Globales Schema | (Mehrere) | Für Zielmetriken für RTCDP Insights stehen neue globale Schemata zur Verfügung. Siehe Folgendes [Pull-Anfrage](https://github.com/adobe/xdm/pull/1560) für weitere Details. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Verhalten | [[!UICONTROL Time-series Schema]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | Es wurde ein Ereignistyp zum Aktualisieren von Medienstatus hinzugefügt. |
| Feldergruppe | [[!UICONTROL Unterkunftsreservierung]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | Es wurde eine Eigenschaft zum Checkout für die Unterkunft hinzugefügt. |
| Datentyp | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Es wurden Felder für den Statusstart und das Statusende hinzugefügt. |
| Erweiterung | [[!UICONTROL Workfront-Änderungsereignis]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Es wurden zwei Felder hinzugefügt, die zum Speichern von Attributen verwendet werden, um den Benutzer und den Zeitpunkt eines Erstellungsereignisses zu identifizieren. |
| Erweiterung | [[!UICONTROL Adobe CJM ExperienceEvent - Details zur Nachrichteninteraktion]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | Dem Landingpage-Objekt wurden Abonnement-, Einverständnis-, benutzerdefinierte E-Mail- und zusätzliche Dateninformationen hinzugefügt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Beschriftung von Ad-hoc-Schemata | Verwalten Sie den Zugriff auf vertrauliche Daten, indem Sie Beschriftungen auf Datenfelder von Ad-hoc-Schemata anwenden, die automatisch durch CTAS-Abfragen von Query Service generiert werden. Sie können die Verwendung bestimmter Felder oder Datensätze von Ad-hoc-Schemata einschränken, um den Zugriff auf vertrauliche personenbezogene Daten und persönlich identifizierbare Informationen zu steuern. Mithilfe der attributbasierten Zugriffssteuerungsfunktion können Sie Ad-hoc-Schemafelder über die Platform-Benutzeroberfläche beschriften. |
| `FLATTEN` Einstellung | Wenn Sie über BI-Tools von Drittanbietern eine Verbindung zu einer Datenbank herstellen, wird die `FLATTEN` Durch die Einstellung werden verschachtelte Datenstrukturen in separate Spalten reduziert, wobei der Attributname zum Spaltennamen wird, der die Zeilenwerte enthält. Dies verbessert die Benutzerfreundlichkeit von Ad-hoc-Schemata und verringert den erforderlichen Arbeitsaufwand zum Abrufen, Analysieren, Transformieren und Berichten von Daten in BI-Tools, die keine verschachtelten Datenstrukturen unterstützen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Query Services finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Beta-Version der [!DNL Mixpanel]-Quelle | Sie können jetzt die [!DNL Mixpanel] zur Erfassung von Analysedaten aus Ihrer [!DNL Mixpanel] -Konto auf Experience Platform. Siehe [[!DNL Mixpanel] Quelldokumentation](../../sources/connectors/analytics/mixpanel.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
