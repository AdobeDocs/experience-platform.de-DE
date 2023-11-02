---
title: Adobe Experience Platform – Versionshinweise März 2023
description: Versionshinweise März 2023 für Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2204'
ht-degree: 85%

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

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen** {#dashboards-new-updated-features}

| Funktion | Beschreibung |
| --- | --- |
| Benutzerdefinierte Dashboards | Vor dem Hinzufügen eines Attributs zu einem Widget im benutzerdefinierten Widget-Composer für Dashboards können jetzt **Attributwerte ausprobiert** werden. Einige Beispielwerte aus dieser Attributspalte sind für einzelne Attribute beim Erstellen eines Widgets verfügbar.<br>In einem Widget können mit der Schaltfläche „Achse vertauschen“ die **X- und Y-Achse vertauscht** werden. Dadurch lässt sich Zeit sparen, und das Hinzufügen von Attributen zu Widgets wird ergonomischer. Dadurch müssen beide Attribute nicht erneut im Attributbereich gesucht werden.<br> Jetzt können in Widgets **Speicherort und Titel der Legende geändert werden**. Wenn eine Legende in einem Widget vorhanden ist, kann diese Legende an eine beliebige Stelle im Diagramm verschoben und der Legendentitel ebenso wie Achsenbeschriftungen und der Widget-Titel umbenannt werden. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neuer Schnellstart-Workflow für die Meta Conversions-API (Beta) | Greifen Sie über die Startseite der Datenerfassung unter „Erste Schritte“ auf neue Schnellstart-Workflows zu! Der [Schnellstart-Workflow für die Meta Conversions-API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start) ermöglicht es, Ereignisdaten schnell zu erfassen und in wenigen einfachen Schritten Server-seitig an Meta für Anzeigenkonversionen weiterzuleiten. |
| Neuer Schnellstart-Workflow für das Mobile SDK (Beta) | Greifen Sie über die Startseite der Datenerfassung unter „Erste Schritte“ auf neue Schnellstart-Workflows zu! Der [Schnellstart-Workflow für das Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) ermöglicht die schnelle Implementierung des Mobile SDK und die Validierung einfacher Ereignisse auf Mobilgeräten in nur wenigen einfachen Schritten. |
| [!DNL Braze]-Erweiterung zur Ereignisweiterleitung | Mit der Ereignisweiterleitungserweiterung [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=de) können die im Adobe Experience Platform Edge Network erfassten Daten genutzt und in Form von Server-seitigen Ereignissen mithilfe der [!DNL Braze]-APIs für die Benutzernachverfolgung an [!DNL Braze] gesendet werden. |
| [!DNL Epsilon]-Erweiterung zur Ereignisweiterleitung | Die [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=de) Mit der -Erweiterung können Sie die Ereignisweiterleitung nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und an zu senden. [!DNL Epsilon] mithilfe der [!DNL Epsilon] Ereignis-API. |
| [!DNL Mixpanel]-Erweiterung zur Ereignisweiterleitung | Die [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=de)-Erweiterung ermöglicht es, die Ereignisweiterleitung zu nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und über die API zur Nachverfolgung von Ereignissen an Mixpanel zu senden. |

{style="table-layout:auto"}

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit der Filterung von Adobe Analytics-Daten | Mithilfe von Funktionen zur Datenvorbereitung können Regeln und Bedingungen zum Filtern von Analytics-Daten angewendet werden, bevor diese in das Echtzeit-Kundenprofil aufgenommen werden. Weitere Informationen finden Sie im Handbuch zum [Filtern von Analytics-Daten für die Profilaufnahme](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Neue Funktionen für die Codierung und Decodierung von URL-Zeichenfolgen | <ul><li>Die Funktion `get_url_encoded` verwendet eine URL als Eingabe und ersetzt oder codiert Sonderzeichen durch ASCII-Zeichen.</li><li>Die Funktion `get_url_decoded` nimmt eine URL als Eingabe und decodiert ASCII-Zeichen in Sonderzeichen.</li></ul> Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md). Eine umfassende Liste der reservierten Zeichen und der zugehörigen codierten Zeichen finden Sie im Handbuch zu [Sonderzeichen](../../data-prep/functions.md#special-characters). |

Weitere Informationen zur Datenvorbereitung finden Sie in der [Übersicht zur Datenvorbereitung](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] -Verbindung allgemein verfügbar](../../destinations/catalog/personalization/adobe-commerce.md) | Mit dem Ziel-Connector für [!DNL Adobe Commerce] (jetzt allgemein verfügbar) können Sie ein oder mehrere Real-Time CDP-Zielgruppen auswählen, die Sie in Ihrem [!DNL Adobe Commerce]-Konto aktivieren, um Kundinnen und Kunden ein dynamisches, personalisiertes Erlebnis zu bieten. |
| [[!DNL Snap Inc] -Verbindung allgemein verfügbar](../../destinations/catalog/advertising/snap-inc.md) | Mit dem Ziel-Connector für [!DNL Snap Inc] (jetzt allgemein verfügbar) können Marketing-Fachleute Benutzersegmente, die in Experience Platform erstellt wurden, in [!DNL Snapchat Ads] importieren und für das Targeting von Anzeigen verwenden. |
| [(API) Oracle Eloqua-Verbindung](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Verwenden Sie die API-basierte Verbindung zu [!DNL Oracle Eloqua], um Kampagnen zu planen und auszuführen und dabei ein personalisiertes Kundenerlebnis für deren potenzielle Kundinnen und Kunden in [!DNL Oracle Eloqua] zu liefern. |
| [(Beta)  [!DNL Amazon Ads] -Verbindung](../../destinations/catalog/advertising/amazon-ads.md) | Die [!DNL Amazon Ads]-Integration in Adobe Experience Platform bietet eine schlüsselfertige Integration für [!DNL Amazon Ads]-Produkte, einschließlich [!DNL Amazon DSP (ADSP)]. Mithilfe des [!DNL Amazon Ads]-Ziels in Adobe Experience Platform können Benutzerinnen und Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung in [!DNL Amazon DSP] definieren. |
| [[!DNL Marketo Measure Ultimate] -Verbindung](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (ehemals Bizible) bietet Marketing-Fachleuten einen Einblick in die Frage, welche Marketing-Maßnahmen zur Steigerung des Umsatzes und der Maximierung des ROI für ihr Unternehmen am effektivsten sind. Das Ziel ermöglicht Business-to-Business-Datenflüsse (B2B) von Adobe Experience Platform zu [!DNL Marketo Measure]. Die Karte steht nur Kundinnen und Kunden von [!DNL Marketo Measure Ultimate] zur Verfügung. |
| [TikTok-Verbindung](../../destinations/catalog/social/tiktok.md) | Erstellen Sie auf TikTok benutzerdefinierte Zielgruppen mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. |
| [Zendesk-Verbindung](../../destinations/catalog/crm/zendesk.md) | Verwenden Sie dieses Ziel, um Identitäten innerhalb eines Segments als Kontakte innerhalb von [!DNL Zendesk] zu erstellen und zu aktualisieren. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Neue Zugriffssteuerungsberechtigung für Ziele: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | Die neue Berechtigung gibt Benutzerinnen und Benutzern die Möglichkeit, Segmente für vorhandene Ziele zu aktivieren, ohne den [Zuordnungsschritt](../../destinations/ui/activate-batch-profile-destinations.md#mapping) anzuzeigen. Benutzerinnen  und Bbenutzer können in Aktivierungs-Workflows Segmente, jedoch keine zugeordneten Attribute oder Identitäten hinzufügen oder entfernen. |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

Wir veröffentlichen eine Fehlerbehebung für die PGP/GPG-Verschlüsselung in dateibasierten Zielen für Real-Time CDP. Mit dieser Änderung generieren vorhandene dateibasierte Ziele, die derzeit eine Verschlüsselung verwenden, einen Dateinamen mit einer anderen Erweiterung als zuvor.

- Aktuelle Erweiterung bei Verwendung einer Verschlüsselung: `filename.csv`
- Zukünftige Erweiterung bei Verwendung einer Verschlüsselung: `filename.csv.gpg`

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| CSV-zu-Schema-Empfehlung | Sie können jetzt Ihre lokalen Dateien hochladen, um durch maschinelles Lernen generierte Schemata zu erstellen, die die manuelle Erstellung eines Schemas überflüssig machen. Laden Sie eine CSV-Beispieldatei aus dem Arbeitsbereich [!UICONTROL Quellen] hoch, und die Algorithmen für maschinelles Lernen von Adobe schlagen ein Schema auf der Grundlage der Zielfelder vor. Weitere Informationen finden Sie in der [Dokumentation](../../ingestion/tutorials/map-csv/recommendations.md).“ |

{style="table-layout:auto"}

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL Angebotselement]](https://github.com/adobe/xdm/pull/1678/files) | Klasse, die ein Angebot darstellt. |
| Klasse | [[!UICONTROL Entscheidungselement]](https://github.com/adobe/xdm/pull/1678/files) | Ein Element, das einer Entscheidung unterzogen werden kann. Die Ausgabe eines Entscheidungsprozesses ist ein oder mehrere Entscheidungselemente. |
| Klasse | [[!UICONTROL Zeitüberschreitung des Mediensitzungs-Servers]](https://github.com/adobe/xdm/pull/1676/files) | Dies gibt die Zeit in Sekunden an, die zwischen der letzten bekannten Interaktion des Benutzers und dem Zeitpunkt, zu dem die Sitzung geschlossen wurde, vergangen ist. |
| Feldergruppe | [[!UICONTROL Berechnete XDM-Profilattribute]](https://github.com/adobe/xdm/pull/1686/files) | Dadurch werden berechnete Attribute aus internen Adobe-Diensten zu eingehenden Kundendaten hinzugefügt. Dies sollte von Kunden nicht zur Aufnahme von Daten verwendet werden. |
| Datentyp | [[!UICONTROL Erstattungsbetrag]](https://github.com/adobe/xdm/pull/1685/files) | Gibt an, ob eine Erstattung mit einer Bestellung verbunden ist, und definiert die Art der Erstattung, den Betrag und die zugehörige Währung. |
| Datentyp | [[!UICONTROL Kategoriedaten]](https://github.com/adobe/xdm/pull/1677/files) | Dieser neue Datentyp stellt die Kategorie eines Produkts dar. |
| Schema | [[!UICONTROL Adobe Target-Klassifizierungsfelder]](https://github.com/adobe/xdm/pull/1682/files) | Für Target Classification-Datensätze wurde ein neues XDM-Schema erstellt. Es enthält eine Reihe von Metadatenfeldern, die Target-Aktivitäten und -Erlebnisse klassifizieren. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldgruppe | [[!UICONTROL Details der Inhaltskomponente]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` wurde entfernt von [!UICONTROL Details der Inhaltskomponente] |
| Feldergruppe | [[!UICONTROL AJO Entity-Tags]](https://github.com/adobe/xdm/pull/1672/files) | AJO Entity-Tags wurden zu [!UICONTROL AJO-Entitätsfelder], die einer Journey oder Kampagne entsprechen |
| Feldgruppe | (Mehrfach) | Es wurden mehrere Felder für [[!UICONTROL Allgemeine Felder für Journey Orchestration Step-Ereignisse]](https://github.com/adobe/xdm/pull/1671/files) |
| Feldgruppe | (Mehrfach) | [Es wurden mehrere XDM-Ereignistypen für [!UICONTROL Medienberichte]](https://github.com/adobe/xdm/pull/1670/files). |
| Feldergruppe | [!UICONTROL Workfront-Änderungsereignis] | Die `Full Record` und `Accessor Employee Ids` Feldergruppen hinzugefügt. |
| Datentyp | [[!UICONTROL Produktlistenelement]](https://github.com/adobe/xdm/pull/1685/files) | Die [!UICONTROL Erstattungsbetrag] wurde hinzugefügt, um den gegebenenfalls für den Posten rückerstatteten Betrag anzugeben. |
| Datentyp | [[!UICONTROL Order ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Erstattungsliste] wurde der Liste der Erstattungen für diese Bestellung hinzugefügt. |
| Datentyp | [[!UICONTROL Produktlistenelement ]](https://github.com/adobe/xdm/pull/1677/files) | Produktkategorien wurden zur Liste der Kategoriedaten dieses Produkts hinzugefügt. |
| Datentyp | [!UICONTROL Informationen zu Sitzungsdetails] | Der `pev3` Zeichenfolgenfeld, das [gibt den Typ des für die Berichterstellung verwendeten Medien-Streams an](https://github.com/adobe/xdm/pull/1676/files). Außerdem wurde `pccr` -Eigenschaft gibt an, ob eine Umleitung erfolgt ist. |
| Datentyp | [!UICONTROL Anforderungsliste] | Stellt die [Eigenschaften der Anforderungsliste](https://github.com/adobe/xdm/pull/1675/files). Dazu gehören Name, ID und Beschreibung. |
| Datentyp | [!UICONTROL Commerce] | Die [Der Commerce-Datentyp wurde aktualisiert](https://github.com/adobe/xdm/pull/1675/files) einschließen `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, und `requisitionList`. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Attributbasierte Zugriffssteuerung für die beschleunigte Speicherung | Verwenden Sie die attributbasierte Zugriffssteuerung mit Data Distiller, um die Zugriffssteuerung für alle Datensätze des beschleunigten Speichers zu definieren. Dadurch wird der Zugriff auf die benutzerdefinierten Datenmodelle gesteuert, die von Benutzenden erstellt und in einem beschleunigten Speicher abgelegt werden, um benutzerdefinierte Dashboards zu betreiben. |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition basiert auf Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketingexpertinnen und -experten mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Fehlerbehebung | Um eine genauere Darstellung der Profile in Ihrem System zu gewährleisten, enthält das System für die Real-time Customer Data Platform B2B Edition keine internen Profile mehr in der Gesamtprofilanzahl oder der adressierbaren Zielgruppenmetrik. Ab heute kann es zu einem einmaligen Rückgang der Metrik für die Gesamtzahl der Profile bzw. adressierbaren Zielgruppen kommen. Keine Ihrer Daten wurden gelöscht. Dies ist lediglich eine Änderung der Zählung. Wenden Sie sich bei Fragen an Ihren Kundenkontakt bei Adobe. |

{style="table-layout:auto"}

Weitere Informationen zur Real-Time CDP B2B Edition finden Sie in der [Übersicht zur Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Profilmetriken | Um eine genauere Darstellung der Profilmetriken zu erhalten, werden Mitgliedschaftsaufschlüsselungen und Abwanderungsmetriken kombiniert und jetzt über einen Zeitraum von 24 Stunden berechnet. Weitere Informationen finden Sie im [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verfügbarkeit der Betaversion von [!DNL Chatlio] | Die [!DNL Chatlio]-Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Chatlio]-Quelle, um Ihre [!DNL Chatlio]-Ereignisdaten zu Experience Platform zu streamen. Weitere Informationen finden Sie in der [[!DNL Chatlio] Übersicht](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Customer.io] | Die [!DNL Customer.io]-Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Customer.io]-Quelle, um Ihre Kundenereignisdaten zu Experience Platform zu streamen. Weitere Informationen finden Sie in der [[!DNL Customer.io] Übersicht](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Pendo] | Die [!DNL Pendo]-Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Pendo]-Quelle, um Ihre Produktanalysedaten zu Experience Platform zu streamen. Weitere Informationen finden Sie in der [[!DNL Pendo] Übersicht](../../sources/connectors/analytics/pendo-webhook.md). |
| Unterstützung für Entwürfe von Datenflüssen | Sie können jetzt die Flow Service-API verwenden, um Ihre Datenflüsse in einen Entwurfsstatus zu versetzen. Entworfene Datenflüsse können später aktualisiert und mit neuen Informationen veröffentlicht werden. Weitere Informationen finden Sie im Handbuch zum [Festlegen der Datenflüsse für Quellen als Entwürfe](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
