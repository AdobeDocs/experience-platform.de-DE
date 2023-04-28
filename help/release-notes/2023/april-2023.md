---
title: Adobe Experience Platform – Versionshinweise April 2023
description: Versionshinweise April 2023 für Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: a8e59d6386a51c4d5d3173be16ee45311f8d2929
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 26. April 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen** {#dashboards-new-updated-features}

| Funktion | Beschreibung |
| --- | --- |
| Benutzerdefinierte Dashboards | Sie können jetzt **historische Daten filtern** aus Ihren Widget-Einblicken und verwenden Sie entweder aktuelle Daten oder einen benutzerdefinierten Analysezeitraum. Siehe [Benutzerhandbuch zu benutzerdefinierten Dashboards](../../dashboards/user-defined-dashboards.md#filter-historical-data) für weitere Informationen.<br>Sie können jetzt auch **vorhandene Widgets duplizieren**. Wenn Sie ein Duplikat anpassen und dessen Attribute bearbeiten, können Sie vermeiden, bei der Erstellung eines neuen, eindeutigen Widgets von Anfang an neu zu beginnen. Lesen Sie die [Widget-Duplizierungshandbuch](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) , um mehr zu erfahren. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen des Aufstockungszeitraums für Adobe Analytics in Nicht-Produktions-Sandboxes | Die Aufstockungszeit für Adobe Analytics in Nicht-Produktions-Sandboxes wurde auf drei Monate reduziert. Die Aufstockung für Produktions-Sandboxes bleibt nach 13 Monaten unverändert. Diese Änderung gilt nur für neue Flüsse und hat keine Auswirkungen auf bestehende Flüsse. Weitere Informationen finden Sie im Abschnitt [Übersicht über Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Neue Zuordnungsfunktion zum Konvertieren von FPID-Zeichenfolgen in ECID | Verwenden Sie die `fpid_to_ecid` -Funktion zum Konvertieren von FPID-Zeichenfolgen in ECID zur Verwendung in Experience Platform- und Experience Cloud-Anwendungen. Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Übersicht zur Datenvorbereitung](../../data-prep/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verschleierung von IP-Adressen für Datastreams | Sie können jetzt Optionen für die IP-Verschleierung auf der Ebene eines partiellen oder vollständigen Datenspeichers im [Benutzeroberfläche für die Datenspeicherkonfiguration](../../edge/datastreams/configure.md). <br><br>Die Einstellung für die IP-Verschleierung auf Datenasterebene hat Vorrang vor jeder in Adobe Target und Audience Manager konfigurierten IP-Verschleierung. <br><br>An Adobe Analytics gesendete Daten sind von der Datenasterebene nicht betroffen [!UICONTROL IP-Verschleierung] -Einstellung. Adobe Analytics erhält derzeit nicht verschleierte IP-Adressen. Damit Analytics verschleierte IP-Adressen empfangen kann, müssen Sie die IP-Verschleierung separat in Adobe Analytics konfigurieren. Dieses Verhalten wird in zukünftigen Versionen aktualisiert.<br><br> Weitere Informationen zur IP-Verschleierung und Anweisungen zur Konfiguration finden Sie unter [Dokumentation zur Datastream-Konfiguration](../../edge/datastreams/configure.md#advanced-options). |
| [Überschreibungen der Datastream-Konfiguration](../../edge/datastreams/overrides.md) | Sie können jetzt zusätzliche Konfigurationsoptionen für Datastreams definieren, mit denen Sie bestimmte Einstellungen wie Ereignis-Datensätze, Target-Eigenschafts-Token, ID-Synchronisierungs-Container und Analytics-Report Suites überschreiben können. <br><br>Das Überschreiben von Datenspeicherkonfigurationen ist ein zweistufiger Prozess: <ol><li>Zunächst müssen Sie Ihre Überschreibungen der Datastream-Konfiguration im [Datastream-Konfigurationsseite](../../edge/datastreams/configure.md).</li><li>Anschließend müssen Sie die Überschreibungen entweder über einen Web SDK-Befehl oder mithilfe des Web SDK an das Edge-Netzwerk senden [Tag-Erweiterung](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] -Verbindung](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Verwenden Sie das Salesforce Marketing Cloud Account Engagement (ehemals Pardot)-Ziel, um Leads zu erfassen, zu verfolgen, zu bewerten und zu bewerten. Verwenden Sie dieses Ziel für B2B-Anwendungsfälle, an denen mehrere Abteilungen und Entscheidungsträger beteiligt sind, die längere Verkaufs- und Entscheidungszyklen benötigen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Dataflow-Überwachung für [!DNL Custom Personalization] und [!DNL Adobe Commerce] Ziele | <p> Sie können nun Aktivierungsmetriken für die [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md) und [Benutzerdefinierte Personalisierung mit Attributen](../../destinations/catalog/personalization/custom-personalization.md) Verbindungen. </p> <p>![Adobe Commerce-Bild](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce-Metriken"){width="100" zoomable="yes"}</p>  Siehe [Überwachen von Datenflüssen im Arbeitsbereich &quot;Ziele&quot;](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) für weitere Details. |
| Neu **[!UICONTROL Segment-ID an Segmentname anhängen]** -Feld für [!DNL Google Ad Manager] und [!DNL Google Ad Manager 360] Ziele | <p>Sie können jetzt den Segmentnamen in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) und [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) schließen Sie die Segment-ID aus Experience Platform wie folgt ein: `Segment Name (Segment ID)`.</p><p>![Segment-ID-Bild anhängen](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Neue Segment-ID an Feld für Segmentname anhängen "){width="100" zoomable="yes"}</p> |
| Backfilets für geplante Zielgruppen | <p>Für [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) Ziel, wird die Aktivierung von Zielgruppen-Backfilets zum Ziel 24-48 Stunden nach der erstmaligen Zuordnung eines Segments zu einer Zielverbindung geplant. Diese Aktualisierung entspricht der Google-Richtlinie, 24 Stunden bis zur Aufnahme von Daten zu warten, und verbessert die Übereinstimmungsraten zwischen der Echtzeit-Kundendatenplattform und [!DNL Google Display & Video 360].</p> <p>Beachten Sie, dass es sich hierbei um eine Backend-Konfiguration handelt, die nur für dieses Ziel gilt und nicht mit kundenkonfigurierbaren Planungsoptionen in der Benutzeroberfläche in Zusammenhang steht.</p> |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Wir haben ein Problem in der **Ausgeschlossene Identitäten** Berichtsmetriken für dateibasierte Zielexporte. Kunden erhielten wie erwartet alle exportierten IDs aus dem aktivierten Export. Die Variable **Ausgeschlossene Identitäten** -Berichtsmetrik in der Benutzeroberfläche zeigte fälschlicherweise eine hohe Anzahl ausgeschlossener Identitäten an, da Identitäten falsch gezählt wurden, die nie exportiert werden sollten. (PLAT-149774)
- Wir haben ein Problem in der **Planung** Schritt des Aktivierungs-Workflows. Für Ziele, für die eine Zuordnungs-ID erforderlich ist, konnten Kunden keine Zuordnungs-ID für Segmente hinzufügen, die zu vorhandenen Zielverbindungen hinzugefügt wurden. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umschalten zwischen Anzeigenamen | Der Schema Editor bietet jetzt einen Schalter zum Ändern zwischen den ursprünglichen Feldnamen und den für Menschen lesbareren Anzeigenamen.<br>![Der Schema Editor mit dem Anzeigenamen wird hervorgehoben.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Anzeigename im Schema Editor umschalten"){width="100" zoomable="yes"}<br>Diese Flexibilität ermöglicht eine verbesserte Erkennung und Bearbeitung von Feldern Ihrer Schemata. Die Anzeigenamen für Standardfeldgruppen werden systemgeneriert, können aber bei Bedarf auch über die Benutzeroberfläche angepasst werden. Bitte lesen Sie die [Umschalten zwischen Anzeige-Namen und Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) , um mehr zu erfahren. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Ablauf der Profildaten | Der Ablauf der pseudonymen Profildaten ist jetzt allgemein verfügbar! Mit dieser Version werden alte pseudonyme Profile kontinuierlich aus Ihrer Experience Platform-Instanz entfernt, sobald sie aktiviert wurden. Weitere Informationen zu dieser Funktion und den Pseudonymen Profilen finden Sie im Abschnitt [Anleitung zum Ablauf von Pseudonymen Profildaten](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| API-Unterstützung zum Filtern von Daten auf Zeilenebene für Microsoft Dynamics-, Salesforce-CRM- und Salesforce-Marketing Cloud | Verwenden Sie logische Operatoren und Vergleichsoperatoren, um Daten auf Zeilenebene für die Microsoft Dynamics-, Salesforce CRM- und Salesforce-Marketing Cloud-Quellen zu filtern. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md). |
| Beta-Verfügbarkeit von Shopify Streaming | Die [Streaming-Quelle kaufen](../../sources/connectors/ecommerce/shopify-streaming.md) ist jetzt als Beta verfügbar. Verwenden Sie die Streaming-Quelle Shopify , um Daten von Ihrem Konto für Shopify-Partner an Experience Platform zu streamen. |
| Allgemeine Verfügbarkeit der OneTrust-Integration | Die [OneTrust-Integrationsquelle](../../sources/connectors/consent-and-preferences/onetrust.md) ist jetzt allgemein verfügbar. Verwenden Sie die OneTrust-Integrationsquelle, um Einwilligungs- und Voreinstellungsdaten aus Ihrem OneTrust-Integrationskonto in die Experience Platform zu übertragen. |
| Allgemeine Verfügbarkeit von Oracle Service Cloud | Die [Oracle Service Cloud-Quelle](../../sources/connectors/customer-success/oracle-service-cloud.md) ist jetzt allgemein verfügbar. Verwenden Sie die Oracle Service Cloud-Quelle, um Ihre Oracle Service Cloud-Daten in die Experience Platform zu übertragen. |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
