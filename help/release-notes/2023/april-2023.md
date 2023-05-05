---
title: Adobe Experience Platform – Versionshinweise April 2023
description: Versionshinweise April 2023 für Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: da28de44fc8ab37d530c2f9b3c167e365f00dca6
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 82%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 26. April 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen** {#dashboards-new-updated-features}

| Funktion | Beschreibung |
| --- | --- |
| Benutzerdefinierte Dashboards | Sie können jetzt aus Ihren Widget-Einblicken **historische Daten filtern** und entweder aktuelle Daten oder einen benutzerdefinierten Analysezeitraum verwenden. Weiterführende Informationen finden Sie im [Handbuch zu benutzerdefinierten Profilen](../../dashboards/user-defined-dashboards.md#filter-historical-data).<br>Sie können jetzt auch **vorhandene Widgets duplizieren**. Wenn Sie ein Duplikat anpassen und dessen Attribute bearbeiten, können Sie dadurch vermeiden, bei der Erstellung eines neuen, eindeutigen Widgets vollständig von vorne zu beginnen. Weitere Informationen finden Sie im [Handbuch zur Widget-Duplizierung](../../dashboards/user-defined-dashboards.md#duplicate-a-widget).  |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen am Aufstockungszeitraum für Adobe Analytics in Nicht-Produktions-Sandboxes | Der Aufstockungszeitraum für Adobe Analytics in Nicht-Produktions-Sandboxes wurde auf drei Monate reduziert. Der Aufstockungszeitraum für Produktions-Sandboxes bleibt mit 13 Monaten unverändert. Diese Änderung gilt nur für neue Flüsse und hat keine Auswirkungen auf bestehende Flüsse. Weitere Informationen finden Sie in der [Übersicht zu Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Neue Zuordnungsfunktion zum Konvertieren von FPID-Zeichenfolgen in ECID | Verwenden Sie die `fpid_to_ecid`-Funktion zur Konvertierung von FPID-Zeichenfolgen in ECID, um sie in Experience Platform- und Experience Cloud-Anwendungen zu verwenden. Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Übersicht zur Datenvorbereitung](../../data-prep/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verschleierung von IP-Adressen für Datenströme | Sie können jetzt in der [Benutzeroberfläche für die Datenstromkonfiguration](../../edge/datastreams/configure.md) Optionen für die partielle oder vollständige IP-Verschleierung auf der Ebene eines Datenstroms festlegen. <br><br>Die Einstellung für die IP-Verschleierung auf Datenstromebene hat Vorrang vor jeder in Adobe Target und Audience Manager konfigurierten IP-Verschleierung. <br><br>An Adobe Analytics gesendete Daten sind von der Einstellung für [!UICONTROL IP-Verschleierung] auf Datenstromebene nicht betroffen. Adobe Analytics empfängt derzeit nicht-verschleierte IP-Adressen. Damit Analytics verschleierte IP-Adressen empfangen kann, müssen Sie die IP-Verschleierung separat in Adobe Analytics konfigurieren. Dieses Verhalten wird in zukünftigen Versionen aktualisiert.<br><br> Weitere Informationen zur IP-Verschleierung und Anweisungen zur Konfiguration finden Sie in der [Dokumentation zur Datenstromkonfiguration](../../edge/datastreams/configure.md#advanced-options). |
| [Überschreibungen der Datenstromkonfiguration](../../edge/datastreams/overrides.md) | Sie können jetzt zusätzliche Konfigurationsoptionen für Datenströme festlegen, mit denen Sie bestimmte Einstellungen wie Ereignis-Datensätze, Target-Eigenschafts-Token, ID-Synchronisierungs-Container und Analytics-Report Suites überschreiben können. <br><br>Das Überschreiben von Datenstromkonfigurationen ist ein zweistufiger Prozess: <ol><li>Zunächst müssen Sie Ihre Überschreibungen der Datenstromkonfiguration auf der Seite [Datenstromkonfiguration](../../edge/datastreams/configure.md) definieren.</li><li>Anschließend müssen Sie die Überschreibungen entweder über einen Web SDK-Befehl oder mithilfe der [Tag-Erweiterung](../../edge/extension/web-sdk-extension-configuration.md) des Web SDK an das Edge-Netzwerk senden.</li></ol> |
| OAuth JWT Secret | Die [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) ermöglicht Kunden die Verwendung von Adobe- und Google Service-Token zur Unterstützung von Server-zu-Server-Interaktionen bei der Ereignisweiterleitung. |
| [!DNL Pinterest Conversions API]-Erweiterung  | Die [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) Mit der Ereignisweiterleitungs-Erweiterung können Sie die im Adobe Experience Platform Edge Network erfassten Daten nutzen und an senden. [!DNL Pinterest] in Form von serverseitigen Ereignissen, bei denen die [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] -Verbindung](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Verwenden Sie das Ziel von Salesforce Marketing Cloud Account Engagement (ehemals Pardot), um Leads zu erfassen, nachzuverfolgen, zu bewerten und einzustufen. Verwenden Sie dieses Ziel für B2B-Anwendungsfälle, an denen mehrere Abteilungen und Entscheidungsträgerinnen bzw. -träger beteiligt sind, die längere Verkaufs- und Entscheidungszyklen benötigen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Monitoring von Datenflüssen für [!DNL Custom Personalization]- und [!DNL Adobe Commerce]-Ziele | <p> Sie können nun Aktivierungsmetriken für die Verbindungen [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md) und [Benutzerdefinierte Personalisierung mit Attributen](../../destinations/catalog/personalization/custom-personalization.md) sehen. </p> <p>![Adobe Commerce-Bild](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce-Metriken"){width="100" zoomable="yes"}</p>  Weitere Informationen sind verfügbar unter [Überwachen von Datenflüssen im Arbeitsbereich „Ziele“](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace). |
| Neues Feld **[!UICONTROL Segment-ID an Segmentname anhängen]** für [!DNL Google Ad Manager]- und [!DNL Google Ad Manager 360]-Ziele | <p>Sie können jetzt in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) und [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) den Segmentnamen die Segment-ID aus Experience Platform einschließen lassen, wie hier zu sehen: `Segment Name (Segment ID)`.</p><p>![Bild zu „Segment-ID anhängen“](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Neues Feld „Segment-ID an Segmentnamen anhängen“"){width="100" zoomable="yes"}</p> |
| Geplante Audience-Auffüllungen | <p>Für das [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics)-Ziel, wird die Aktivierung von Audience-Auffüllungen zum Ziel 24–48 Stunden nach der erstmaligen Zuordnung eines Segments zu einer Zielverbindung geplant. Diese Aktualisierung ist eine Antwort auf die Google-Richtlinie, 24 Stunden bis zur Aufnahme von Daten zu warten, und verbessert die Übereinstimmungsraten zwischen Real-time CDP und [!DNL Google Display & Video 360].</p> <p>Beachten Sie, dass es sich hierbei um eine Backend-Konfiguration handelt, die nur für dieses Ziel gilt und nicht mit kundenkonfigurierbaren Planungsoptionen in der Benutzeroberfläche in Zusammenhang steht.</p> |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

- Es wurde ein Problem bei der Berichtsmetrik **Ausgeschlossene Identitäten** für dateibasierte Zielexporte behoben. Kundinnen und Kunden erhielten wie erwartet alle exportierten IDs aus dem aktivierten Export. Die Berichtsmetrik **Ausgeschlossene Identitäten** in der Benutzeroberfläche zeigte jedoch fälschlicherweise eine hohe Anzahl ausgeschlossener Identitäten an, da fälschlicherweise Identitäten gezählt wurden, die nie exportiert werden sollten. (PLAT-149774)
- Es wurde ein Problem im Schritt **Planung** des Aktivierungs-Workflows behoben. Für Ziele, für die eine Zuordnungs-ID erforderlich ist, konnten Kundinnen und Kunden keine Zuordnungs-ID für Segmente hinzufügen, die zu vorhandenen Zielverbindungen hinzugefügt wurden. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umschalten zwischen Anzeigenamen | Der Schema-Editor bietet jetzt einen Umschalter zum Wechseln zwischen den ursprünglichen Feldnamen und den für Menschen besser lesbaren Anzeigenamen.<br>![Der Schema-Editor mit hervorgehobenem Umschalter für den Anzeigenamen.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Umschalten des Anzeigenamens im Schema-Editor"){width="100" zoomable="yes"}<br>Diese Flexibilität ermöglicht eine verbesserte Erkennung und Bearbeitung von Feldern Ihrer Schemata. Die Anzeigenamen für Standardfeldgruppen werden vom System generiert, können aber bei Bedarf auch über die Benutzeroberfläche angepasst werden. Bitte lesen Sie die [Dokumentation zum Umschalten zwischen Anzeigenamen](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=de#display-name-toggle), um mehr zu erfahren. |

{style="table-layout:auto"}

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Schema | [[!UICONTROL Adobe Target-Klassifizierungsfelder]](https://github.com/adobe/xdm/pull/1719/files) | Ein neues XDM-Schema für Target Classification-Datensätze, das eine Reihe von Metadatenfeldern enthält, um Target-Aktivitäten und -Erlebnisse zu klassifizieren. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Adobe Unified Profile Service-Kontovereinigung-Erweiterung]](https://github.com/adobe/xdm/pull/1696/files) | Es wurde eine Feldergruppe zur Kontoerweiterung für das Echtzeit-Kundenprofil hinzugefügt, mit der Benutzer eine Segmentmitgliedschaft zur Kontounion hinzufügen können. |
| Schema | [[!UICONTROL Systemschema für berechnete Attribute]](https://github.com/adobe/xdm/pull/1696/files) | Die Feldergruppe Berechnete Attribute , die vom Echtzeit-Kundenprofil verwendet wird, wurde in ein schreibgeschütztes globales Schema des Systems aktualisiert. |
| Feldergruppe | Mehrfach | Es wurden mehrere Ereignisse als Felder für [[!UICONTROL Zeitreihenschema]](https://github.com/adobe/xdm/pull/1718/files). |
| Feldergruppe | Details zur Profilloyalität | [Titel korrigiert](https://github.com/adobe/xdm/pull/1717/files) für `xdm:upgradeDate` von &quot;Programmname&quot;zu &quot;Upgrade-Datum&quot;. |
| Feldergruppe | Mehrfach | Mehrere Felder aus [[!UICONTROL Entscheidungselement]](https://github.com/adobe/xdm/pull/1714/files) wurden aktualisiert, um die doppelte verschachtelte Hierarchie zu entfernen. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Real-Time Customer Data Platform

Basierend auf Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Erweiterte Real-Time CDP-Startseite | Die [Real-Time CDP-Homepage](https://experience.adobe.com) wurde um einen aktualisierten Look und eine verbesserte Leistung erweitert. Die Startseite ist jetzt berechtigungsorientiert und enthält Widgets, die für die Funktionen relevant sind, auf die Sie Zugriff haben. Weitere Informationen finden Sie im Abschnitt [Übersicht über das Dashboard der Real-Time CDP-Startseite](../../rtcdp/home-page-dashboards.md). |
| Umfrage zur Selbstidentifizierung | Die Umfrage zur Selbstidentifizierung ist ein kurzer Fragebogen, der auf der Startseite der Adobe Experience Platform-Benutzeroberfläche vorgestellt wird. Verwenden Sie die Umfrage zur Identifizierung Ihrer Experience Platform, um Ihr persönliches Profil zu erstellen und auf Ihre Auswahl abgestimmte Richtlinien zu erhalten. Weitere Informationen finden Sie im Abschnitt [Selbstidentifizierungs-Umfrage - Überblick](../../landing/self-identification.md). |

Weitere Informationen finden Sie unter [!DNL Real-Time CDP], siehe [[!DNL Real-Time CDP] Übersicht](../../rtcdp/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Ablauf pseudonymer Profildaten | Der Ablauf pseudonymer Profildaten ist jetzt allgemein verfügbar! Mit dieser Version werden veraltete pseudonyme Profile kontinuierlich aus Ihrer Experience Platform-Instanz entfernt, sobald sie aktiviert wurden. Weitere Informationen zu dieser Funktion und pseudonymen Profilen finden Sie im [Handbuch zum Ablauf pseudonymer Profildaten](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| API-Unterstützung zum Filtern von Daten auf Zeilenebene für Microsoft Dynamics, Salesforce CRM und Salesforce Marketing Cloud | Verwenden Sie logische Operatoren und Vergleichsoperatoren, um Daten auf Zeilenebene für die Quellen Microsoft Dynamics, Salesforce CRM und Salesforce Marketing Cloud zu filtern. Weitere Informationen finden Sie im Handbuch zum [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md). |
| Beta-Verfügbarkeit von Shopify Streaming | Die [Quelle Shopify Streaming](../../sources/connectors/ecommerce/shopify-streaming.md) ist jetzt in der Beta-Version verfügbar. Verwenden Sie die Quelle Shopify Streaming, um Daten von Ihrem Shopify-Partnerkonto zu Experience Platform zu streamen. |
| Allgemeine Verfügbarkeit von OneTrust Integration | Die [Quelle OneTrust Integration](../../sources/connectors/consent-and-preferences/onetrust.md) ist jetzt allgemein verfügbar. Verwenden Sie die Quelle OneTrust Integration, um Einverständnis- und Voreinstellungsdaten aus Ihrem OneTrust Integration-Konto zu Experience Platform zu übertragen. |
| Allgemeine Verfügbarkeit von Oracle Service Cloud | Die [Quelle Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) ist jetzt allgemein verfügbar. Verwenden Sie die Quelle Oracle Service Cloud, um Daten aus Ihrem Oracle Service Cloud-Konto in Experience Platform aufzunehmen. |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).