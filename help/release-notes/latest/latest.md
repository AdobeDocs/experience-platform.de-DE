---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise März 2023 für Adobe Experience Platform.
source-git-commit: 582305583aa5869d8cc29f871aeb3fa0ef0b6ab1
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 41%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 29. März 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Abfrage-Service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Insights zu den Daten Ihres Unternehmens erhalten, die in täglichen Snapshots erfasst werden.

**Neue oder aktualisierte Funktionen** {#dashboards-new-updated-features}

| Funktion | Beschreibung |
| --- | --- |
| Benutzerdefinierte Dashboards | Sie können jetzt **Beispielattributwerte** vor dem Hinzufügen eines Attributs zu einem Widget im benutzerdefinierten Widget-Composer für Dashboards. Einige Beispielwerte aus dieser Attributspalte sind für einzelne Attribute beim Erstellen eines Widgets verfügbar.<br>Sie können jetzt **X- und Y-Achse tauschen** auf Ihrem Widget mit der Schaltfläche Achse austauschen . Dadurch sparen Sie Zeit und erhalten beim Hinzufügen von Attributen zu Widgets ein ergonomischeres Erlebnis. Dadurch müssen Sie beide Attribute erneut im Attributbereich finden.<br>Sie können jetzt **Speicherort und Titel der Legende ändern** in Ihren Widgets. Nachdem eine Legende in einem Widget vorhanden ist, können Sie diese Legende an eine beliebige Stelle im Diagramm verschieben und den Legendentitel wie bei Achsenbeschriftungen und dem Widget-Titel umbenennen. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neuer Schnellstart-Workflow für die Meta Conversions-API (Beta) | Greifen Sie über den Startseite der Datenerfassung auf neue Schnellstartarbeitsabläufe unter &quot;Erste Schritte&quot;zu! Die [Schnellstart-Workflow für die Meta Conversions-API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) ermöglicht Kunden die schnelle Erfassung und Weiterleitung von Ereignisdaten, serverseitig zu Meta für Anzeigenkonversionen in nur wenigen einfachen Schritten. |
| [!DNL Braze] Ereignisweiterleitungs-Erweiterung | Die [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Mit der Ereignisweiterleitungs-Erweiterung können Sie die im Adobe Experience Platform Edge Network erfassten Daten nutzen und an senden. [!DNL Braze] in Form von serverseitigen Ereignissen, bei denen die [!DNL Braze] APIs für die Benutzerverfolgung. |
| [!DNL Mixpanel] Ereignisweiterleitungs-Erweiterung | Die [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) -Erweiterung ermöglicht es Kunden, die Ereignisweiterleitung zu nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und über die Track Events-API an Mixpanel zu senden. |

{style="table-layout:auto"}

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit der Filterung von Adobe Analytics-Daten | Sie können jetzt Datenvorbereitung verwenden, um Regeln und Bedingungen zum Filtern Ihrer Analytics-Daten anzuwenden, bevor Sie sie in das Echtzeit-Kundenprofil aufnehmen. Weitere Informationen finden Sie im Handbuch unter [Filtern von Analytics-Daten für die Profilaufnahme](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Neue Funktionen für die Kodierung und Dekodierung von URL-Zeichenfolgen | <ul><li>Die `get_url_encoded` -Funktion verwendet eine URL als Eingabe und ersetzt oder kodiert Sonderzeichen durch ASCII-Zeichen.</li><li>Die `get_url_decoded` nimmt eine URL als Eingabe und dekodiert ASCII-Zeichen in Sonderzeichen.</li></ul> Weitere Informationen finden Sie im Abschnitt [Handbuch zu Datenvorbereitung-Funktionen](../../data-prep/functions.md). Eine umfassende Liste der reservierten Zeichen und der zugehörigen kodierten Zeichen finden Sie im Handbuch unter [Sonderzeichen](../../data-prep/functions.md#special-characters). |

Weitere Informationen zur Datenvorbereitung finden Sie im [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] Verbindung GA](../../destinations/catalog/personalization/adobe-commerce.md) | Die [!DNL Adobe Commerce] Mit dem Ziel-Connector (jetzt allgemein verfügbar) können Sie eine oder mehrere Real-Time CDP-Zielgruppen auswählen, die für Ihre [!DNL Adobe Commerce] -Konto ein dynamisches personalisiertes Erlebnis für Ihre Kunden bereitstellen. |
| [[!DNL Snap Inc] Verbindung GA](../../destinations/catalog/advertising/snap-inc.md) | Die [!DNL Snap Inc] Mit dem Ziel-Connector (jetzt allgemein verfügbar) können Marketing-Experten in Experience Platform erstellte Benutzersegmente in importieren [!DNL Snapchat Ads] und verwenden sie zum Targeting ihrer Anzeigen. |
| [(API) Oracle Eloqua-Verbindung](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Verwenden Sie die API-basierte Verbindung, um [!DNL Oracle Eloqua] Planung und Ausführung von Kampagnen bei Bereitstellung eines personalisierten Kundenerlebnisses für potenzielle Kunden in [!DNL Oracle Eloqua]. |
| [(Beta)  [!DNL Amazon Ads] -Verbindung](../../destinations/catalog/advertising/amazon-ads.md) | Die [!DNL Amazon Ads] Integration mit Adobe Experience Platform bietet eine schlüsselfertige Integration in [!DNL Amazon Ads] Produkte, einschließlich [!DNL Amazon DSP (ADSP)]. Verwenden der [!DNL Amazon Ads] Zielgruppe in Adobe Experience Platform können Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung auf der [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] -Verbindung](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (ehemals Bizible) gibt Marketing-Experten Einblicke, welche Marketing-Maßnahmen bei der Steigerung des Umsatzes und der Maximierung der Kapitalrendite für ihr Unternehmen am effektivsten sind. Das Ziel ermöglicht den B2B-Datenfluss (Business-to-Business) von Adobe Experience Platform nach [!DNL Marketo Measure]. Die Karte steht nur zur Verfügung für [!DNL Marketo Measure Ultimate] -Kunden. |
| [TikTok-Verbindung](../../destinations/catalog/social/tiktok.md) | Erstellen Sie benutzerdefinierte Zielgruppen in TikTok mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. |
| [Zendesk-Verbindung](../../destinations/catalog/crm/zendesk.md) | Verwenden Sie dieses Ziel, um Identitäten innerhalb eines Segments als Kontakte innerhalb von zu erstellen und zu aktualisieren. [!DNL Zendesk]. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Neue Zugriffssteuerungsberechtigung für Ziele: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | Die neue Berechtigung gibt Benutzern die Möglichkeit, Segmente für vorhandene Ziele zu aktivieren, ohne die [Zuordnungsschritt](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Benutzer können in Aktivierungs-Workflows Segmente hinzufügen und entfernen, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

Wir veröffentlichen eine Fehlerbehebung für die PGP/GPG-Verschlüsselung in dateibasierten Zielen für die Echtzeit-Kundendatenplattform. Mit dieser Änderung generieren vorhandene dateibasierte Ziele, die derzeit die Verschlüsselung verwenden, einen Dateinamen mit einer anderen Erweiterung als zuvor.

- Aktuelle Erweiterung bei Verwendung der Verschlüsselung: `filename.csv`
- Zukünftige Erweiterung bei Verwendung der Verschlüsselung: `filename.csv.gpg`

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| CSV zur Schemaempfehlung | Sie können jetzt Ihre lokalen Dateien hochladen, um durch maschinelles Lernen generierte Schemas zu erstellen, die die manuelle Erstellung eines Schemas ersparen. Aus dem [!UICONTROL Quellen] Arbeitsbereich, laden Sie eine CSV-Beispieldatei hoch und die Algorithmen für maschinelles Lernen von Adobe schlagen Ihnen basierend auf den Zielfeldern ein Schema vor. Weitere Informationen finden Sie in der [Dokumentation.&quot;](../../ingestion/tutorials/map-csv/recommendations.md) |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung auf dem beschleunigten Speicher | Verwenden Sie die attributbasierte Zugriffssteuerung mit Data Distiller , um die Zugriffskontrolle für alle Datensätze im beschleunigten Speicher zu definieren. Dadurch wird der Zugriff auf die benutzerdefinierten Datenmodelle gesteuert, die von Benutzern erstellt und in einem beschleunigten Speicher gespeichert werden, um benutzerdefinierte Dashboards zu erstellen. |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition basiert auf Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketingexpertinnen und -experten mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Bugfix | Um eine genauere Darstellung der Profile in Ihrem System zu gewährleisten, enthält das System keine internen Profile mehr in der Gesamtprofilanzahl oder der adressierbaren Zielgruppenmetrik für die Real-time Customer Data Platform B2B Edition. Ab heute kann es zu einem einmaligen Rückgang der Metrik für die Gesamtzahl der Profile/adressierbaren Zielgruppen kommen. Keine Ihrer Daten wurde gelöscht. Dies ist lediglich eine Änderung der Anzahl. Wenden Sie sich bei Fragen an Ihren Ansprechpartner bei Ihrer Adobe. |

{style="table-layout:auto"}

Weitere Informationen über Real-Time CDP B2B Edition finden Sie in der [Übersicht zu Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Profilmetriken | Um eine genauere Darstellung der Profilmetriken zu erhalten, werden Mitgliedschaftsaufschlüsselungen und Abwanderungsmetriken kombiniert und jetzt über einen Zeitraum von 24 Stunden berechnet. Weitere Informationen finden Sie im [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verfügbarkeit der Betaversion von [!DNL Chatlio] | Die [!DNL Chatlio] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Chatlio] Quelle zum Streamen Ihrer [!DNL Chatlio] Ereignisdaten in Experience Platform. Weitere Informationen finden Sie im [[!DNL Chatlio] Überblick](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Customer.io] | Die [!DNL Customer.io] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Customer.io] -Quelle, um Ihre Kundenereignisdaten an Experience Platform zu streamen. Weitere Informationen finden Sie im [[!DNL Customer.io] Überblick](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Pendo] | Die [!DNL Pendo] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Pendo] -Quelle, um Ihre Produktanalysedaten an Experience Platform zu streamen. Weitere Informationen finden Sie im [[!DNL Pendo] Überblick](../../sources/connectors/analytics/pendo-webhook.md). |
| Unterstützung für Datenflussentwürfe | Sie können jetzt die Flow Service-API verwenden, um Ihre Datenflüsse auf den Entwurfsstatus festzulegen. Entworfene Datenflüsse können später aktualisiert und mit neuen Informationen veröffentlicht werden. Weitere Informationen finden Sie im Handbuch unter [Festlegen der Datenflüsse für Quellen als Entwürfe](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
