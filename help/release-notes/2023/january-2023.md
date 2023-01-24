---
title: Adobe Experience Platform - Versionshinweise Januar 2023
description: Die Versionshinweise für Adobe Experience Platform vom Januar 2023.
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 43%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 25. Januar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

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

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und ermöglicht es Ihnen, diese Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Zulassen des Benutzerzugriffs auf Unterordner der Cloud-Speicherquellen | Sie können jetzt den Zugriff auf einen bestimmten Unterordner Ihrer Cloud-Speicherquelle definieren, wenn Sie ein neues Konto erstellen. Nach der Erstellung können Benutzer nur auf Daten aus dem zulässigen Unterordner zugreifen. Diese Funktion steht den folgenden Cloud-Speicher-Quellen zur Verfügung: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)und [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Verfügbarkeit von Beta [!DNL SugarCRM] | [!DNL SugarCRM] -Quellen sind jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] Quellen zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM] -Konto auf Experience Platform. Weitere Informationen finden Sie im Abschnitt [[!DNL SugarCRM] Übersicht](../../sources/connectors/crm/sugarcrm.md). |
