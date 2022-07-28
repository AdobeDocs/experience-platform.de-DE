---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7cb940019905240b36e96b834b9e5d0166c1324d
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 28%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 27. Juli 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenerfassung](#collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)

<!-- - [Real-time Customer Data Platform B2B Edition](#b2b) -->
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards], in denen basierend auf täglichen Momentaufnahmen der Daten wichtige Informationen zu den Unternehmensdaten dargestellt werden.

### Dashboards für Kontoprofile

Das Dashboard &quot;Kontoprofile&quot;zeigt eine Momentaufnahme der einheitlichen Kontoinformationen aus den verschiedenen Quellen für Ihre Marketingkanäle und die verschiedenen Systeme an, die Ihr Unternehmen derzeit zum Speichern von Kundenkontoinformationen verwendet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Gesamtkonten nach Branchen-Widget | Dieses Widget zeigt die Gesamtanzahl der Konten in einer einzelnen Metrik und verwendet ein Ringdiagramm, um die proportionalen Zählergrößen für die Branchen zu veranschaulichen, aus denen die Gesamtanzahl besteht. |
| Widget &quot;Kontoprofile hinzugefügt&quot; | Dieses Widget verwendet ein farbkodiertes Balkendiagramm, um die Anzahl der Profile, die einem Konto über einen bestimmten Zeitraum hinzugefügt wurden, und den Anteil der verschiedenen Branchen, aus denen diese hinzugefügten Profile bestehen, zu veranschaulichen. |

{style=&quot;table-layout:auto&quot;}

Siehe [Übersicht über die Echtzeit-Kundendatenplattform, B2B Edition](../../rtcdp/b2b-overview.md) , um mehr über die verfügbaren B2B-Funktionen zu erfahren, oder über die [End-to-End-Tutorial](../../rtcdp/b2b-tutorial.md) Erfahren Sie mehr darüber, wie Kontoprofile im Rahmen des B2B-Workflows erstellt werden.

Weitere Informationen zu den Widgets zur Visualisierung Ihrer Kontoprofilmetriken finden Sie in der [Dokumentation zu Kontoprofil-Widgets](../../dashboards/guides/account-profiles.md#standard-widgets).

### Profil-Dashboards

Im Dashboard „Profile“ wird eine Momentaufnahme der Attributdaten (Datensatzdaten) wiedergegeben, die sich in Ihrem Unternehmen im Profilspeicher in Experience Platform befinden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget &quot;Zugeordnete Zielgruppen&quot; | Dieses Widget zeigt die Gesamtzahl der zugeordneten Zielgruppen an, die für das im Dashboard &quot;Profile&quot;ausgewählte Ziel aktiviert werden können. |

Weitere Informationen zum Dashboard &quot;Profile&quot;finden Sie im Abschnitt [Profil-Dashboards - Übersicht](../../dashboards/guides/profiles.md).

### Ziele-Dashboards

Im Dashboard „Ziele“ finden Sie eine Momentaufnahme der Ziele, die Ihr Unternehmen in Experience Platform aktiviert hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zielgruppen-Widget | Dieses Widget stellt die Gesamtzahl der Segmente bereit, die entsprechend der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, aktiviert werden können. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Dashboard &quot;Ziele&quot;finden Sie unter [Übersicht über das Dashboard &quot;Ziele&quot;](../../dashboards/guides/destinations.md).

## Datenerfassung {#collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie clientseitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert, umgewandelt und an Ziele außerhalb der Adobe verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Berechtigungsverwaltung über Adobe Admin Console | Der Zugriff auf Datenerfassungsfunktionen wird jetzt über Adobe Admin Console unter der Karte für die Adobe Experience Platform-Datenerfassung verwaltet. Siehe Handbuch unter [Datenerfassungsberechtigungen](../../collection/permissions.md) für weitere Informationen.<br><br>Berechtigungen für Datastreams werden jetzt auch über die Admin Console unter der Karte für Adobe Experience Platform verwaltet, wodurch die Sicherheit gegenüber der vorherigen Methode, diese Berechtigungen manuell für jeden Benutzer festzulegen, verbessert wird. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen finden Sie im [Datenerfassung - Übersicht](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen an [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations ist jetzt schlauer und schneller. Neue Validierungsprüfungen reduzieren die häufigsten Zuordnungsfehler erheblich und verkürzen so die Wertschöpfungszeit. |
| Hierarchische Unterstützung für Streaming-Upsets | Sie können jetzt Funktionen verwenden `upsert_array_append` und `upsert_array_replace` um beim Streaming von Uploads an Profile Arrays und Objekte zu aktualisieren. Siehe [[!DNL Data Prep] Handbuch zu Zuordnungsfunktionen](../../data-prep/functions.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen finden Sie unter [!DNL Data Prep], siehe [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ----------- | ----------- |
| [Datei jetzt exportieren (Beta)](../../destinations/ui/export-file-now.md) | Exportieren Sie eine vollständige Datei, ohne den aktuellen Exportplan eines zuvor geplanten Segments zu unterbrechen. Dieser Export erfolgt zusätzlich zu den zuvor geplanten Exporten und ändert nicht die Exportfrequenz des Segments. <br> Der Dateiexport wird sofort ausgelöst und es werden die neuesten Ergebnisse aus der Experience Platform-Segmentierung abgerufen. <br> <br>Wenden Sie sich an Ihren Kundenbetreuer, um Zugriff auf diese Funktion zu erhalten. |

{style=&quot;table-layout:auto&quot;}

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Marketo V2](../../destinations/catalog/adobe/marketo-engage.md) | Das Marketo Engage-Ziel-Update ermöglicht es Ihnen, den Prozess der Erstellung statischer Listen mit Automatisierung zu optimieren und Benutzern zu ermöglichen, zusätzliche Felder in ihre Leads einzufügen. Weitere Informationen zu den Verbesserungen in Marketo V2 finden Sie unten: <br><ul><li>Im **[!UICONTROL Segment planen]** Schritt des Aktivierungs-Workflows: In Marketo V1 müssen Sie manuell einen **Zuordnungs-ID** , um Daten erfolgreich nach Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.</li><li>Im **[!UICONTROL Zuordnung]** -Schritt des Aktivierungs-Workflows in Marketo V1 konnten Sie XDM-Felder nur drei Zielfeldern in Marketo zuordnen: `firstName`, `lastName`und `companyName`. Mit der Marketo V2-Version können Sie jetzt XDM-Felder vielen weiteren Feldern in Marketo zuordnen. Weitere Informationen finden Sie unter [unterstützte Attribute in Marketo V2](../../destinations/catalog/adobe/marketo-engage.md#supported-attributes).  </li></ul> |
| [Pega Customer Decisioning Hub](../../destinations/catalog/personalization/pega.md) | Verwenden Sie Profilattribute und Segmentzugehörigkeitsinformationen aus Adobe Experience Platform in Pega Customer Decisioning Hub als Prädikatoren in adaptiven Modellen und helfen Sie bei der Entscheidungsfindung für die nächste beste Aktion. |
| [(API) Salesforce-Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) | Mit diesem Ziel können Marketing-Experten in Experience Platform erstellte Benutzersegmente in Momentaufnahmen-Anzeigen importieren und für das Targeting ihrer Anzeigen verwenden. |
| [Salesforce CRM](../../destinations/catalog/crm/salesforce.md) | Aktualisieren von Kontaktinformationen in Salesforce Marketing Cloud mit Profil- und Segmentinformationen in Experience Platform |
| [(Beta) [!DNL Snap Inc.]](../../destinations/catalog/advertising/snap-inc.md) | Mit diesem Ziel können Marketing-Experten in Experience Platform erstellte Benutzersegmente in Momentaufnahmen-Anzeigen importieren und für das Targeting ihrer Anzeigen verwenden. <br><br>Dieses Ziel befindet sich derzeit in der Betaversion. Dokumentation und Funktionalität können sich ändern. |
| [(Beta) Die [!DNL Trade Desk] - CRM-Verbindung](../../destinations/catalog/advertising/tradedesk-emails.md) | Verwendung [!DNL The Trade Desk] CRM-Ziel, Profile für Ihre [!DNL Trade Desk] Zielgruppen-Targeting und -Unterdrückung anhand von CRM-Daten. <br><br>Dieses Ziel befindet sich derzeit in der Betaversion. Dokumentation und Funktionalität können sich ändern. |

{style=&quot;table-layout:auto&quot;}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Datenmodell der Gesundheitsbranche | Ein Standarddatenmodell für Gesundheitsdaten wurde eingeführt, um fünf gängige Anwendungsfälle der Industrie zu unterstützen, die mit der zunehmenden digitalen Akquise, der Verbesserung der Programmregistrierung und der Förderung von Arzneimittelinformationen zusammenhängen. Die Übersicht finden Sie auf der [Datenmodell](../../xdm/schema/industries/healthcare.md) für weitere Informationen zu diesen Anwendungsfällen und den Standard-XDM-Komponenten, die sie unterstützen.<br><br>Ein neuer Branchenfilter wurde zum [!UICONTROL Schemas] Benutzeroberfläche, die Ihnen beim Durchsuchen von Komponenten im Zusammenhang mit der Gesundheitsfürsorge beim Erstellen benutzerdefinierter Schemata hilft. |

{style=&quot;table-layout:auto&quot;}

**Neue XDM-Komponenten**

>[!WARNING]
>
>Die in der folgenden Tabelle aufgelisteten neuen XDM-Komponenten sind experimentell und werden derzeit getestet. Diese Komponenten werden voraussichtlich mit brechenden Änderungen aktualisiert (falls erforderlich), bevor sie stabilisiert werden. Planen Sie Ihre Entwicklungsbemühungen bitte entsprechend.

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL Wetter]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Eine auf Aufzeichnungen basierende Klasse, die zur Erfassung von Wetterdaten verwendet wird. |
| Feldergruppe | [[!UICONTROL Aktuelles Wetter]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung der aktuellen Wetterbedingungen für eine Postleitzahl verwendet werden. |
| Feldergruppe | [[!UICONTROL Vorhergesagtes Wetter]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung der prognostizierten Wetterbedingungen für eine Postleitzahl verwendet werden. |
| Feldergruppe | [[!UICONTROL Produkt-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung produktspezifischer Trigger verwendet werden, die die Wetterbedingungen nutzen, die bekanntermaßen das Verbraucherverhalten beeinflussen. |
| Feldergruppe | [[!UICONTROL Relative Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung relativer Trigger verwendet werden, die die Wetterbedingungen nutzen, die bekanntermaßen das Verbraucherverhalten beeinflussen. |
| Feldergruppe | [[!UICONTROL Schwere Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung von Triggern verwendet werden, die mit schweren Wetterbedingungen arbeiten, die bekanntermaßen das Verbraucherverhalten beeinflussen. |
| Feldergruppe | [[!UICONTROL Wetter-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/weather-triggers.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] und [!UICONTROL Wetter] Klassen, die zur Erfassung allgemeiner Trigger verwendet werden, die die Wetterbedingungen nutzen, die bekanntermaßen das Verbraucherverhalten beeinflussen. |
| Feldergruppe | [[!UICONTROL MediaCollection Interaction-Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-collection.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] -Klasse, die Details zu einer Medieninteraktion erfasst. |
| Feldergruppe | [[!UICONTROL Details zur MediaReporting-Interaktion]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-reporting.schema.json) | Eine Feldergruppe für [!UICONTROL XDM ExperienceEvent] -Klasse, die Details zu einer Interaktion mit Medienberichten erfasst. |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Erfasst Details zu einem Anzeigen-Asset. |
| Datentyp | [[!UICONTROL Informationen zur Werbeunterbrechung]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json) | Erfasst Details zu einem Anzeigen-Pod. Hierbei handelt es sich um eine Folge mehrerer Anzeigen, die innerhalb einer Werbeunterbrechung wiedergegeben werden. |
| Datentyp | [[!UICONTROL Informationen zu Kapiteldetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) | Erfasst Details zu einem Kapitel oder Segment in einem Videoinhalt. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Erfasst Details zu einem Videowiedergabefehler. |
| Datentyp | [[!UICONTROL Informationen zu Player-Ereignissen]](https://github.com/adobe/xdm/blob/master/components/datatypes/playereventdetails.schema.json) | Erfasst ereignisbezogene Details zu einem Videoplayer, einschließlich Abspielposition und Sitzungs-ID. |
| Datentyp | [[!UICONTROL Player-Statusinformationen]](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) | Erfasst Statusbezogene Details zu einem Videoplayer. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Erfasst Details zur Erlebnisqualität (QoE) zu einem Videowiedergabeereignis. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Erfasst Sitzungsdetails zu einem Videowiedergabeereignis. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

<!-- ## Real-time Customer Data Platform B2B Edition {#b2b}

Built on Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition is purpose-built for marketers operating in a business-to-business service model. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

| Feature | Description |
| Lead to account matching | Lead to account matching allows you to use Real-time CDP B2B edition to match known person profiles to account profiles so that these profiles can be segmented and targeted with B2B context data like account, opportunity (and add something else like don't use etc. to the description). For more information, see the document on [lead to account matching](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md). For a guide on how to monitor profile enrichment, see the document on [monitoring profile enrichment in the UI](../../dataflows/ui/b2b/monitor-profile-enrichment.md). For instructions on how to use related accounts in segment definitions, see the guide on [Segmentation use cases for Real-time Customer Data Platform B2B Edition](../../rtcdp/segmentation/b2b.md#related-accounts)."|

{style="table-layout:auto"}

To learn more about Real-time CDP B2B Edition, see the [Real-time CDP B2B overview](../../rtcdp/overview.md). -->

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

| Funktion | Beschreibung |
| ------- | ----------- |
| Verwaiste Profilattributbereinigung (begrenzte Version) | Wenn Ihr Unternehmen Zugriff auf diese Funktion hat, entfernt der Profil-Service jetzt täglich die Attribute der übrig gebliebenen Benutzeraktivitätsregion, um eine genauere Darstellung Ihrer Profile in Ihrem System zu erhalten. Diese Bereinigung erfolgt, nachdem alle Profilfragmente für ein bestimmtes Profil gelöscht wurden, und sollte sich auf die Zusammenführung von Profilen aus Datensätzen auswirken, in denen `com_adobe_aep_profile_region_dataset` als &quot;true&quot;markiert ist. Dies kann einen Rückgang der Metrik &quot;Addressable audience&quot;im Dashboard zur Lizenznutzung anzeigen und einen Rückgang der Metrik &quot;Profilanzahl&quot;im Profil-Dashboard anzeigen, da diese Metriken vor dieser Version verbleibende Edge-Attributfragmente enthielten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit der [!DNL Azure Data Explorer] source | Verwenden Sie die Azure Data Explorer-Quelle, um Daten von Ihrem [!DNL Azure] -Instanz zu Experience Platform. Informationen dazu finden Sie in der [[!DNL Azure Data Explorer] Übersicht zu Quellen](../../sources/connectors/databases/data-explorer.md). |
| Allgemeine Verfügbarkeit [!DNL Generic OData] source | Verwenden Sie die [!DNL Generic OData] -Quelle, um Ressourcen von Systemen zu übertragen, die Open-Data-Protokoll unterstützen. Informationen dazu finden Sie in der [[!DNL Generic OData] Übersicht zu Quellen](../../sources/connectors/protocols/odata.md). |
| Unterstützung der automatischen Erkennung von Quelldateieigenschaften für [!DNL Data Landing Zone] in der Experience Platform-Benutzeroberfläche | Die [!DNL Data Landing Zone] -Quelle unterstützt jetzt die automatische Erkennung von Dateieigenschaften bei Verwendung der Experience Platform-Benutzeroberfläche. Weitere Informationen finden Sie in der Dokumentation zur [Erstellung einer  [!DNL Data Landing Zone] -Quellverbindung](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
