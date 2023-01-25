---
title: Adobe Experience Platform - Versionshinweise Januar 2023
description: Die Versionshinweise für Adobe Experience Platform vom Januar 2023.
source-git-commit: 68e5baac9012a33d179f8ebff23deda7a8efd26b
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 25. Januar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Assurance](#assurance)
- [Datenerfassung](#data-collection)
- [Experience-Datenmodell (XDM)](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentation Service](#segmentation)
- [Quellen](#sources)

## Assurance {#assurance}

Mit Adobe Assurance können Sie die Datenerfassung und die Bereitstellung von Erlebnissen in Ihrer App überprüfen, testen, simulieren und überprüfen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Validierungs-Editor | Es wurden neue Verbesserungen am Validierungs-Editor hinzugefügt. Zu diesen Verbesserungen gehören Überprüfungsspalten, neue Tools zur Codeerstellung und verbesserte Ansichten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Zuverlässigkeitserklärung finden Sie im [Dokumentation zur Sicherheit](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neuer Startbildschirm | Die Startseite der Datenerfassungs-Benutzeroberfläche wurde aktualisiert und enthält jetzt hilfreiche Onboarding-Informationen und Links zur Optimierung der Produktivität. Dazu gehören:<ol><li>Dokumentation und empfohlene Workflows für die ersten Schritte</li><li>Letzte Eigenschaften, Regeln und Datenelemente</li><li>Beliebte Erweiterungen</li><li>Neue Erweiterungs-Updates mit einer Schnellinstallationsfunktion</li></ol> |
| Senden von Daten an [!DNL Google Ads] mit der Ereignisweiterleitung | Sie können jetzt die [[!DNL Google Ads Enhanced Conversions] API-Erweiterung](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) für die Ereignisweiterleitung, kombiniert mit [Google Oauth 2 Geheimnisse](../../tags/ui/event-forwarding/secrets.md#google-oauth2), um Server-seitige Daten sicher an zu senden [!DNL Google Ads] in Echtzeit. |

{style=&quot;table-layout:auto&quot;}

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Deaktivierung empfohlener Werte für Zeichenfolgenfelder | Sie können jetzt [Deaktivieren einzelner empfohlener Werte für Zeichenfolgenfelder](../../xdm/ui/fields/enum.md) im [!UICONTROL Schemas] Arbeitsbereich, einschließlich derjenigen aus Standardkomponenten. Diese Funktion ist nur für Felder mit empfohlenen Werten verfügbar und wird nicht für Enum-Begrenzungen unterstützt. |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL Konversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Eine Klasse zum Verfolgen von Konversionsdaten wie Währungsumrechnungen. |
| Feldergruppe | [[!UICONTROL Währungskonversionsratendetails]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Eine Feldergruppe für [!UICONTROL Konversion] -Klasse, die zusätzliche Details im Zusammenhang mit der Währungsumrechnung erfasst. |
| Feldergruppe | [[!UICONTROL Zuordnung der Bewertungsergebnisse für Einwilligungsrichtlinien mit Metadaten]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Erfasst Details für das Bewertungsergebnis mehrerer Zustimmungsrichtlinien, einschließlich Metadateninformationen zu Eintritten von Zustimmungsrichtlinien und vorhanden. |

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Die `ID` wurde in `name`und der vorherigen `name` Feld ist jetzt `friendlyName`. |
| Datentyp | [[!UICONTROL Details zu Entscheidungsvorschlägen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Eine `selectionStrategy` -Feld, das die Details einer Auswahlstrategie erfasst. |
| Feldergruppe | [[!UICONTROL Erlebnisereignis - Interaktionen bei Vorschlägen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Die Feldergruppe ist jetzt mit der [!UICONTROL Journey-Schrittereignis] -Klasse. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Die `ID` wurde in `name`. |
| Datentyp | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Eine Änderung des Musters an der Videosegmenteigenschaft wurde zurückgesetzt. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Entfernt die `droppedFrameCount` -Feld. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Die `isAuthorized` -Feld zu `authorized`und die `type` in eine Zeichenfolge, wenn es sich zuvor um einen booleschen Wert handelte. |
| Datentyp | [[!UICONTROL Lieferung]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Es wurden mehrere neue Felder hinzugefügt: `shipDate`, `trackingNumber`und `trackingURL`. |
| Feldergruppe | [[!UICONTROL AJO-Entitätsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Es wurden mehrere neue Felder hinzugefügt: `journeyNodeID`, `journeyNodeName`und `journeyModeType`. |
| Feldergruppe | [[!UICONTROL Ereignis für Kundenerlebnisse]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Die Feldergruppe ist jetzt auch mit der [!UICONTROL Zusammenfassungsmetriken] -Klasse. |
| Feldergruppe | [[!UICONTROL Produkt-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Die `productTriggers` -Feld ist jetzt unter einer `weather` -Objekt. |
| Feldergruppe | [[!UICONTROL Relative Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Die `relativeTriggers` -Feld ist jetzt unter einer `weather` -Objekt. |
| Feldergruppe | [[!UICONTROL Starke Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Die `severeTriggers` -Feld ist jetzt unter einer `weather` -Objekt. |
| Feldergruppe | [[!UICONTROL Wetter-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Die `weatherTriggers` -Feld ist jetzt unter einer `weather` -Objekt. |
| Feldergruppe | [[!UICONTROL XDM-bezogene Geschäftskonten]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Die Feldergruppe ist jetzt stabil. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit dem Echtzeit-Kundenprofil können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, die Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Bevorstehende Einstellung** {#deprecation}

Um Redundanz im Lebenszyklus der Segmentmitgliedschaft zu entfernen, muss die `Existing` Der Status wird vom [Segmentzugehörigkeitszuordnung](../../xdm/field-groups/profile/segmentation.md) Ende März 2023. Eine Folgenachricht enthält das genaue Datum der Einstellung.

Nach der Einstellung werden in einem Segment qualifizierte Profile als `Realized` und Profile, die disqualifiziert sind, weiterhin als `Exited`. Dies führt zu Parität mit dateibasierten Zielen mit `Active` und `Expired` Segmentstatus.

Diese Änderung könnte sich auf Sie auswirken, wenn Sie [Enterprise-Ziele](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) und haben automatisierte nachgelagerte Prozesse basierend auf der `Existing` Status. Überprüfen Sie Ihre nachgelagerten Integrationen, falls dies für Sie der Fall ist. Wenn Sie über einen bestimmten Zeitraum hinaus an der Identifizierung neu qualifizierter Profile interessiert sind, sollten Sie eine Kombination aus `Realized` und `lastQualificationTime` in Ihrer Segmentzugehörigkeitszuordnung. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer bei der Adobe.

Um mehr über das Echtzeit-Kundenprofil zu erfahren, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, lesen Sie zunächst das [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Von der Plattform generierte Segmentmitgliedschaftsgültigkeit | Jede Segmentzugehörigkeit, die sich im `Exited` für mehr als 30 Tage, basierend auf dem `lastQualificationTime` -Feld kann gelöscht werden. |
| Ablauf der Mitgliedschaft in einer externen Zielgruppe | Standardmäßig werden externe Zielgruppenmitgliedschaften 30 Tage lang aufbewahrt. Um sie länger aufzubewahren, verwenden Sie die `validUntil` -Feld während der Erfassung von Zielgruppendaten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und ermöglicht es Ihnen, diese Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Zulassen des Benutzerzugriffs auf Unterordner der Cloud-Speicherquellen | Sie können jetzt den Zugriff auf einen bestimmten Unterordner Ihrer Cloud-Speicherquelle definieren, wenn Sie ein neues Konto erstellen. Nach der Erstellung können Benutzer nur auf Daten aus dem zulässigen Unterordner zugreifen. Diese Funktion steht den folgenden Cloud-Speicher-Quellen zur Verfügung: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)und [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Verfügbarkeit von Beta [!DNL SugarCRM] | [!DNL SugarCRM] -Quellen sind jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] Quellen zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM] -Konto auf Experience Platform. Weitere Informationen finden Sie im Abschnitt [[!DNL SugarCRM] Übersicht](../../sources/connectors/crm/sugarcrm.md). |
