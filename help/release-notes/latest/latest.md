---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise vom Juni 2023 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a03d0eeab5ca42225705fdeab692020b1641395d
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 28%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 21. Juni 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Authentifizierung für Experience Platform-APIs](#authentication-platform-apis)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Query Service](#query-service)
- [Quellen](#sources)

## Authentifizierung für Experience Platform-APIs {#authentication-platform-apis}

Für Experience Platform-API-Benutzer ist die Methode zum Abrufen erforderlicher Zugriffstoken zur Authentifizierung und zum Aufrufen von API-Endpunkten jetzt vereinfacht. Die JWT-Methode zum Abrufen von Zugriffstoken wird nicht mehr unterstützt und durch eine einfachere OAuth-Server-zu-Server-Authentifizierungsmethode ersetzt.<p>![Neue OAuth-Authentifizierungsmethode, um Zugriffstoken hervorgehoben zu bekommen.](/help/landing/images/api-authentication/oauth-authentication-method.png "Neue OAuth-Authentifizierungsmethode, um Zugriffstoken hervorgehoben zu bekommen."){width="100" zoomable="yes"}</p>

Während bestehende API-Integrationen, die die JWT-Authentifizierungsmethode verwenden, bis zum 1. Januar 2025 weiterhin funktionieren, empfiehlt Adobe dringend, vorhandene Integrationen vor diesem Datum auf die neue OAuth Server-zu-Server-Methode zu migrieren. Lesen Sie das Handbuch unter [Migration von JWT-Anmeldedaten (Service Account) zu OAuth-Server-zu-Server-Anmeldedaten](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Aktualisieren lesen [Tutorial zur Experience Platform-Authentifizierung](/help/landing/api-authentication.md) für weitere Informationen.

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterung | [!DNL Google Cloud Platform]-Erweiterung zur Ereignisweiterleitung | Die [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) Mit der Ereignisweiterleitungs-Erweiterung können Sie Ereignisdaten zur Aktivierung an Google weiterleiten über [!DNL Google Pub/Sub]. |
| Erweiterung | [!DNL Cloud connector for Google Analytics 4 (ga4)]-Erweiterung  | Die [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) Mit der Ereignisweiterleitungs-Erweiterung können Sie Analysen über die neue [!DNL Google Analytics 4 (ga4)] Standard. |
| Geheimnis | OAuth 2 JWT Secret | Die [OAuth 2 JWT Secret](../../tags/ui/event-forwarding/secrets.md) ermöglicht Ihnen die Verwendung von Adobe und [!DNL Google] Dienst-Token zur Unterstützung von Server-Server-Interaktionen bei der Ereignisweiterleitung. |
| Tags und Ereignisweiterleitung | Benutzerzuordnung | Die Benutzerzuordnung liefert wichtige Aktivitätsdaten über die [Tags](../../tags/home.md) und [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) Benutzeroberfläche.<br><br>Die Daten enthalten, wer welche Änderungen vorgenommen hat und zu welchem Zeitpunkt. Diese Daten sind in den folgenden Bildschirmen in der Benutzeroberfläche für Tags und Ereignisweiterleitung sichtbar:<br><ul><li> Eigenschaftenübersicht</li><li> Installierte Erweiterungen</li><li>Vergleich und Überprüfung von Regeln</li><li>Datenelemente - Vergleich</li><li>Übersicht über Erweiterungsvergleiche</li><li>Änderungen an Bibliotheksressourcen</li><li>Bibliothek zuletzt erstellt und veröffentlicht</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie im Abschnitt [Datenerfassung - Übersicht](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | Die [!DNL Amazon Ads] Integration mit Adobe Experience Platform unterstützt jetzt die regionale Weiterleitung zu den verschiedenen [!DNL Amazon Ads] Marktplätze. Mehr dazu im [Zielchangelog](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Workspace-Unterstützung für [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) Ziele. | Sie können jetzt beim Konfigurieren einer neuen Adobe Target-Zielverbindung den Adobe Target-Arbeitsbereich auswählen, für den Sie Zielgruppen freigeben möchten. Siehe [Verbindungsparameter](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) für weitere Informationen. Weitere Informationen finden Sie im Tutorial unter [Konfigurieren von Arbeitsbereichen](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) in Adobe Target finden Sie weitere Informationen zu Arbeitsbereichen. |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Abfrage-Service {#query-service}

Mit Query Service können Sie SQL-Standarddaten in Adobe Experience Platform Data Lake abfragen. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.
&#x200B;
**Aktualisierte Funktionen**
&#x200B; | Funktion | Beschreibung | | — | — | | &#x200B; Inline-Vorlagen | Query Service unterstützt jetzt die Verwendung von Vorlagen, die auf andere Vorlagen in Ihrer SQL verweisen. Reduzieren Sie den Arbeitsaufwand und vermeiden Sie Fehler, indem Sie Inline-Vorlagen in Ihren Abfragen verwenden. Sie können Anweisungen oder Bedingungen wiederverwenden und verschachtelte Vorlagen referenzieren, um die Flexibilität in Ihrer SQL zu erhöhen. Die Größe von Abfragen, die als Vorlagen gespeichert werden können, oder die Anzahl der Vorlagen, auf die über Ihre ursprüngliche Abfrage verwiesen werden kann, ist unbegrenzt. Weitere Informationen finden Sie im Abschnitt [Inline-Vorlagenhandbuch](../../query-service/essential-concepts/inline-templates.md). | | Aktualisierungen der Benutzeroberfläche für geplante Abfragen | Verwalten Sie alle geplanten Abfragen von einem Ort in der Benutzeroberfläche mit der [[!UICONTROL Registerkarte &quot;Geplante Abfragen&quot;]](../../query-service/ui/monitor-queries.md#inline-actions). Die [!UICONTROL Geplante Abfragen] Die Benutzeroberfläche wurde durch das Hinzufügen von Inline-Abfrageaktionen und der neuen Spalte mit dem Abfragestatus verbessert. Die kürzlich hinzugefügten Funktionen umfassen die Möglichkeit, einen Zeitplan zu aktivieren, zu deaktivieren und zu löschen oder Warnhinweise für kommende Abfragen zu abonnieren, die direkt über die [!UICONTROL Geplante Abfragen] anzeigen. <p>![Inline-Aktionen, die im [!UICONTROL Geplante Abfragen] anzeigen.](../../query-service/images/ui/monitor-queries/disable-inline.png "Inline-Aktionen, die im [!UICONTROL Geplante Abfragen] anzeigen."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
&#x200B; Weitere Informationen zu Query Service finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Sie können Daten aus verschiedenen Quellen erfassen, z. B. aus Adobe Apps, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Adobe Analytics Classification-Quell-Datenflüsse unterstützen das Löschen | Sie können jetzt Quelldatensätze löschen, die Adobe Analytics-Klassifizierungen als Quelle verwenden. under **[!UICONTROL Quellen]** > **[!UICONTROL Datenflüsse]**, wählen Sie den gewünschten Datenfluss aus und klicken Sie dann auf Löschen. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Quellverbindung für Adobe Analytics-Klassifizierungsdaten](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Filterunterstützung für [!DNL Microsoft Dynamics] Verwendung der API | Verwenden Sie logische und Vergleichsoperatoren, um Daten auf Zeilenebene für die [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) -Quelle. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md). |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | Sie können jetzt die [!DNL RainFocus] Integration von Quellen , um Ereignismanagement- und Analysedaten aus Ihren [!DNL RainFocus] -Konto auf Experience Platform. Weitere Informationen finden Sie im Abschnitt [[!DNL RainFocus] Quellübersicht](../../sources/connectors/analytics/rainfocus.md). |
| Unterstützung für Adobe Commerce | Sie können jetzt die Adobe Commerce-Quellenintegration verwenden, um Daten aus Ihrem Adobe Commerce-Konto in die Experience Platform zu übertragen. Weitere Informationen finden Sie im Abschnitt [Adobe Commerce-Quellübersicht](../../sources/connectors/adobe-applications/commerce.md). |
| Unterstützung für [!DNL Mixpanel] | Sie können jetzt die [!DNL Mixpanel] Integration von Quellen , um Analysedaten aus Ihrer [!DNL Mixpanel] -Konto zur Experience Platform mithilfe von APIs oder der -Benutzeroberfläche. Weitere Informationen finden Sie im Abschnitt [[!DNL Mixpanel] Quellübersicht](../../sources/connectors/analytics/mixpanel.md). |
| Unterstützung für [!DNL Zendesk] | Sie können jetzt die [!DNL Zendesk] Quellenintegration zur Einbindung von Kundenerfolgsdaten aus Ihrer [!DNL Zendesk] -Konto zur Experience Platform mithilfe von APIs oder der -Benutzeroberfläche. Weitere Informationen finden Sie im Abschnitt [[!DNL Zendesk] Quellübersicht](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
