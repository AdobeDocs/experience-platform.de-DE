---
title: Adobe Experience Platform – Versionshinweise April 2023
description: Versionshinweise April 2023 für Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: c95d2ab1a6f104c18c491d3a533ee2c304a0aa68
workflow-type: tm+mt
source-wordcount: '2095'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

>[!IMPORTANT]
>
>Ab dem 15. Mai 2023 wird der Status `Existing` in der Segmentzugehörigkeitszuordnung nicht mehr unterstützt, um Redundanz im Lebenszyklus der Segmentzugehörigkeit zu entfernen. Nach dieser Änderung werden in einem Segment qualifizierte Profile als `Realized` und disqualifizierte Profile weiterhin als `Exited` dargestellt. Weitere Informationen zu dieser Änderung finden Sie im Abschnitt [Segmentierungs-Service](#segmentation).

**Veröffentlichungsdatum: 26. April 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
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
| OAuth JWT-Geheimnis | Das [OAuth JWT-Geheimnis](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=de) ermöglicht Kundinnen und Kunden die Verwendung von Adobe- und Google-Service-Token zur Unterstützung von Server-zu-Server-Interaktionen bei der Ereignisweiterleitung. |
| [!DNL Pinterest Conversions API]-Erweiterung  | Mit der Ereignisweiterleitungserweiterung [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=de) können die im Adobe Experience Platform Edge Network erfassten Daten genutzt und in Form von Server-seitigen Ereignissen mithilfe der [!DNL Pinterest Conversions API] an [!DNL Pinterest] gesendet werden. |

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
| Schema | [[!UICONTROL Adobe Target-Klassifizierungsfelder]](https://github.com/adobe/xdm/pull/1719/files) | Ein neues XDM-Schema für Target-Klassifizierungsdatensätze, das eine Reihe von Metadatenfeldern enthält, um Target-Aktivitäten und -Erlebnisse zu klassifizieren. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL Adobe Unified Profile Service-Kontovereinigungserweiterung]](https://github.com/adobe/xdm/pull/1696/files) | Es wurde eine Feldergruppe zur Kontoerweiterung für das Echtzeit-Kundenprofil hinzugefügt, mit der Benutzerinnen und Benutzer eine Segmentmitgliedschaft zur Kontovereinigung hinzufügen können. |
| Schema | [[!UICONTROL Systemschema für berechnete Attribute]](https://github.com/adobe/xdm/pull/1696/files) | Die Feldergruppe „Berechnete Attribute“, die vom Echtzeit-Kundenprofil verwendet wird, wurde zu einem schreibgeschützten globalen Schema des Systems aktualisiert. |
| Feldergruppe | Mehrfach | Es wurden mehrere Ereignisse als Felder für das [[!UICONTROL Zeitreihenschema] hinzugefügt](https://github.com/adobe/xdm/pull/1718/files). |
| Feldergruppe | Details zur Profiltreue | [Titel korrigiert](https://github.com/adobe/xdm/pull/1717/files) für `xdm:upgradeDate` von „Programmname“ zu „Upgrade-Datum“. |
| Feldergruppe | Mehrfach | Mehrere Felder aus [[!UICONTROL Entscheidungselement]](https://github.com/adobe/xdm/pull/1714/files) wurden aktualisiert, um die doppelte verschachtelte Hierarchie zu entfernen. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Real-Time Customer Data Platform

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Startseite der erweiterten Real-Time CDP | Die [Startseite der Real-Time CDP](https://experience.adobe.com) hat ein aktualisiertes Design und eine verbesserte Leistung erhalten. Die Startseite ist jetzt berechtigungsorientiert und enthält Widgets, die für die Funktionen relevant sind, auf die Sie Zugriff haben. Weitere Informationen finden Sie im Abschnitt [Übersicht über das Dashboard der Real-Time CDP-Startseite](../../rtcdp/home-page-dashboards.md). |
| Umfrage zur Selbstidentifizierung | Die Umfrage zur Selbstidentifizierung ist ein kurzer Fragebogen, der auf der Startseite der Adobe Experience Platform-Benutzeroberfläche vorgestellt wird. Verwenden Sie die Umfrage zur Selbstidentifizierung, um Ihr persönliches Profil von Experience Platform zu erstellen, und erhalten Sie auf Ihre Auswahl abgestimmte Richtlinien. Weitere Informationen finden Sie im [Überblick der Umfrage zur Selbstidentifizierung](../../landing/self-identification.md). |

Weitere Informationen zu [!DNL Real-Time CDP] finden Sie im [[!DNL Real-Time CDP] Überblick](../../rtcdp/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Ablauf pseudonymer Profildaten | Der Ablauf pseudonymer Profildaten ist jetzt allgemein verfügbar! Mit dieser Version werden veraltete pseudonyme Profile kontinuierlich aus Ihrer Experience Platform-Instanz entfernt, sobald sie aktiviert wurden. Weitere Informationen zu dieser Funktion und pseudonymen Profilen finden Sie im [Handbuch zum Ablauf pseudonymer Profildaten](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Segmentzugehörigkeitszuordnung | Als Folgemaßnahme zur Ankündigung vom Februar wird seit dem 15. Mai 2023 der Status `Existing` in der Segmentzugehörigkeitszuordnung nicht mehr unterstützt, um Redundanz im Lebenszyklus der Segmentzugehörigkeit zu entfernen. Nach dieser Änderung werden in einem Segment qualifizierte Profile als `Realized` und disqualifizierte Profile weiterhin als `Exited` dargestellt. <br/><br/> Diese Änderung könnte sich auf Sie auswirken, wenn Sie [Unternehmensziele](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) verwenden und automatisierte nachgelagerte Prozesse basierend auf dem Status `Existing` anwenden. Wenn dies der Fall ist, überprüfen Sie Ihre nachgelagerten Integrationen. Wenn Sie über einen bestimmten Zeitraum hinaus an der Identifizierung neu qualifizierter Profile interessiert sind, sollten Sie eine Kombination des `Realized`-Status und der `lastQualificationTime` bei Ihrer Segmentzugehörigkeitszuordnung erwägen. Weitere Informationen erhalten Sie von Ihren Adobe-Support-Mitarbeitenden. |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

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