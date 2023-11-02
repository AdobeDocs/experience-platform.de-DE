---
title: Adobe Experience Platform – Versionshinweise Januar 2023
description: Versionshinweise Januar 2023 für Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 98%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 25. Januar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Datenerfassung](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Services für künstliche Intelligenz/maschinelles Lernen {#ai-ml}

Mit den Services für künstliche Intelligenz und maschinelles Lernen können Marketing-Analysten und Fachleute die Leistung von KI/ML in Anwendungsfällen für Kundenerlebnisse nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene Prognosen erstellen, die auf die Anforderungen eines Unternehmens zugeschnitten sind, ohne dass datenwissenschaftliche Kenntnisse erforderlich sind.

### Attributions-KI

Attributions-KI wird verwendet, um Credits zu Touchpoints zuzuordnen, die zu Konversions-Ereignissen führen. Dies kann von Marketing-Fachleuten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| HIPAA-Bereitschaft | Wer Healthcare Shield nutzt, kann jetzt geschützte Gesundheitsinformationen in Attributions-KI und bestimmten anderen Experience Platform-basierten Anwendungen empfangen, verwenden, verwalten oder übermitteln. Healthcare Shield richtet sich an Kundinnen und Kunden im Gesundheitswesen, die gemäß HIPAA entweder ein Rechtsträger im Gesundheitswesen (Covered Entity) oder ein Geschäftspartner (Business Associate) sind. Weitere Informationen finden Sie in der Dokumentation zu [HIPAA und Adobe-Produkten und -Services](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Bearbeiten zusätzlicher Bewertungs-Datensatzspalten | Sie können jetzt beim Bearbeiten vorhandener Modelle zusätzliche Bewertungs-Datensatzspalten (Berichtsspalten) hinzufügen oder entfernen. Dies erweitert die Flexibilität der Attributionsbewertungen, um Ihnen Insights in zusätzliche Dimensionen zu bieten, nachdem ein Modell bereits erstellt wurde. Weitere Informationen finden Sie im [Handbuch zur Attributions-Benutzeroberfläche](../../intelligent-services/attribution-ai/user-guide.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Überblick zu [KI-/ML-Services](../../intelligent-services/attribution-ai/overview.md).

### Kunden-KI

Die Kunden-KI für Real-time Customer Data Platform dient dazu, im gewünschten Umfang benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| HIPAA-Bereitschaft | Wer Healthcare Shield nutzt, kann jetzt geschützte Gesundheitsinformationen in Attributions-KI für Real-time Customer Data Platform und bestimmten anderen Experience Platform-basierten Anwendungen empfangen, verwenden, verwalten oder übermitteln. Healthcare Shield richtet sich an Kundinnen und Kunden im Gesundheitswesen, die gemäß HIPAA entweder ein Rechtsträger im Gesundheitswesen (Covered Entity) oder ein Geschäftspartner (Business Associate) sind. Weitere Informationen finden Sie in der Dokumentation zu [HIPAA und Adobe-Produkten und -Services](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Überblick zu [KI-/ML-Services](../../intelligent-services/customer-ai/overview.md).

## Assurance {#assurance}

Mit Adobe Assurance können Sie die Datenerfassung und die Bereitstellung von Erlebnissen in Ihrer App untersuchen, testen, simulieren und überprüfen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Validierungs-Editor | Es wurden neue Verbesserungen zum Validierungs-Editor hinzugefügt. Zu diesen Verbesserungen gehören Validierungsspalten, neue Tools zur Code-Erstellung und optimierte Ansichten. |

{style="table-layout:auto"}

Weitere Informationen zu Assurance finden Sie in der [Assurance-Dokumentation](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neuer Startbildschirm | Die Startseite der Benutzeroberfläche für die Datenerfassung wurde aktualisiert und enthält jetzt hilfreiche Onboarding-Informationen und Links zur Optimierung der Produktivität. Dazu gehören:<ol><li>Dokumentation und empfohlene Workflows für die ersten Schritte</li><li>Aktuelle Eigenschaften, Regeln und Datenelemente</li><li>Beliebte Erweiterungen</li><li>Neue Erweiterungsaktualisierungen mit Schnellinstallationsfunktion</li></ol> |
| Senden von Daten an [!DNL Google Ads] mittels Ereignisweiterleitung | Sie können jetzt die [[!DNL Google Ads Enhanced Conversions] API-Erweiterung](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) für die Ereignisweiterleitung in Kombination mit [Google Oauth 2-Geheimnissen](../../tags/ui/event-forwarding/secrets.md#google-oauth2) verwenden, um Server-seitige Daten sicher und in Echtzeit an [!DNL Google Ads] zu senden. |

{style="table-layout:auto"}

## Ziele (am 2. Februar aktualisiert) {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud-Audiences-Verbindung](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Verwenden Sie die [!UICONTROL (Beta) Adobe Experience Cloud-Audiences]-Verbindung zum Freigeben von Segmenten aus Experience Platform für verschiedene Experience Platform-Lösungen wie Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target oder Marketo. |
| [Pega-Profil-Verbindung](../../destinations/catalog/personalization/pega-profile.md) | Verwenden Sie den [!DNL Pega Profile Connector] in Adobe Experience Platform, um eine ausgehende Live-Verbindung zu Ihrem [!DNL Amazon]-S3-Speicher herzustellen und so Profildaten regelmäßig in CSV-Dateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren. In [!DNL Pega Customer Decision Hub] können Sie Datenaufträge planen, um diese Profildaten aus dem S3-Speicher zur Aktualisierung des [!DNL Pega Customer Decision Hub]-Profils importieren. |
| [(Beta) The Trade Desk CRM-EU-Verbindung](../../destinations/catalog/advertising/tradedesk-emails.md) | Mit Veröffentlichung der EUID (European Unified ID) sehen Sie jetzt zwei [!DNL The Trade Desk - CRM]-Ziele im [Zielkatalog](/help/destinations/catalog/overview.md). <ul><li> Wenn Sie Daten in der EU beziehen, verwenden Sie bitte das **[!DNL The Trade Desk - CRM (EU)]**-Ziel.</li><li> Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie das **[!DNL The Trade Desk - CRM (NAMER & APAC)]**-Ziel. </li></ul> |

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Verbesserung der Paid-Media-Einverständnisrichtlinie für Integrationen mit Streaming-Zielen | Eine [verbesserte Durchsetzung von Einverständnisrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) an [Streaming-Zielen](/help/destinations/destination-types.md#streaming-destinations) für Anwendungsfälle zur Paid-Media-Aktivierung. Wenn Profile nicht mehr für eine Einverständnisrichtlinie qualifiziert sind, wird deren Richtlinienausstieg nun proaktiv von Experience Platform an Streaming-Ziele kommuniziert. <br> <b>Hinweis</b>: Diese Funktion steht nur Kundinnen und Kunden von **[!UICONTROL Privacy und Security Shield]** sowie **[!UICONTROL Healthcare Shield]** zur Verfügung. |
| Neue Trennzeichenoptionen für Beta-Cloud-Speicherziel-Connectoren | Drei neue Trennzeichenoptionen (Doppelpunkt `:`, Pipe, Semikolon `;`) sind jetzt für die neuen Beta-Cloud-Speicher-Ziele verfügbar – [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Lesen Sie diese Informationen zu den unterstützten [Dateiformatierungsoptionen](/help/destinations/ui/batch-destinations-file-formatting-options.md) für dateibasierte Ziele. |
| Neuer optionaler Parameter in [Kundendatenfeld](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md)-Konfigurationen in [Destination SDK](/help/destinations/destination-sdk/overview.md) verfügbar | `unique`: Verwenden Sie diesen Parameter, wenn Sie ein Kundendatenfeld erstellen müssen, dessen Wert über alle vom Unternehmen der Benutzenden eingerichteten Zieldatenflüsse hinweg eindeutig sein muss. <br> Beispiel: Das Feld **[!UICONTROL Integrationsalias]** im Ziel [[!UICONTROL Benutzerdefinierte Personalisierung]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) muss eindeutig sein, d. h., zwei separate Datenflüsse zu diesem Ziel dürfen für dieses Feld nicht denselben Wert aufweisen. |

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Korrektur oder Verbesserung</b></td>
        <td><b>Beschreibung</b></td>
    </tr>
    <tr>
        <td>Aktualisiertes Exportverhalten für dateibasierte Ziele (PLAT-123316)</td>
        <td>Es wurde ein Problem im Verhalten von <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">obligatorischen Attributen</a> beim Exportieren von Datendateien in Batch-Ziele behoben. <br> Zuvor wurde jeder Datensatz in den Ausgabedateien dahingehend überprüft, ob beides enthalten ist: <ol><li>ein Wert ungleich null der <code>mandatoryField</code>-Spalte und</li><li>ein Wert ungleich null für mindestens eines der anderen nicht obligatorischen Felder.</li></ol> Die zweite Bedingung wurde entfernt. Daher werden möglicherweise mehr Ausgabezeilen in Ihren exportierten Datendateien angezeigt, wie im folgenden Beispiel zu sehen ist:<br> <b> Beispielverhalten vor der Version Januar 2023 </b> <br> Obligatorisches Feld: <code>emailAddress</code> <br> <b>Eingabedaten zur Aktivierung</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Aktivierungsausgabe</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Beispielverhalten nach der Version vom Januar 2023 </b> <br> <b>Aktivierungsausgabe</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>UI- und API-Validierung für erforderliche und doppelte Zuordnungen (PLAT-123316)</td>
        <td>Die Validierung wird jetzt in der Benutzeroberfläche und API beim <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">Zuordnen von Feldern</a> im Workflow zum Aktivieren von Zielen wie folgt durchgesetzt:<ul><li><b>Erforderliche Zuordnungen</b>: Wenn das Ziel vom Zielentwickler-Team mit den erforderlichen Zuordnungen eingerichtet wurde (z. B. das Ziel <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a>), müssen diese erforderlichen Zuordnungen benutzerseitig hinzugefügt werden, wenn Daten für das Ziel aktiviert werden. </li><li><b>Doppelte Zuordnungen</b>: Im Zuordnungsschritt des Aktivierungs-Workflows können Sie doppelte Werte in den Quellfeldern, aber nicht in den Zielfeldern hinzufügen. In der folgenden Tabelle finden Sie ein Beispiel für zulässige und unzulässige Zuordnungskombinationen. <br><table><thead><tr><th>Zulässig/unzulässig</th><th>Quellfeld</th><th>Zielfeld</th></tr></thead><tbody><tr><td>Zugelassen</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email alias2</li></ul></td></tr><tr><td>Verboten</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserte Anzeigenamen in der Schemastruktur | Zuvor wurden Feldnamen in der Benutzeroberfläche angezeigt, aber nun sind die Anzeigenamen für Schemafelder auf der Schema-Arbeitsfläche einfacher zu lesen. |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL Konversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Eine Klasse zum Verfolgen von Konversionsdaten wie Währungsumrechnungen. |
| Feldergruppe | [[!UICONTROL Wechselkursdetails]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Eine Feldergruppe für die [!UICONTROL Konversionsklasse], die zusätzliche Details im Zusammenhang mit der Währungsumrechnung erfasst. |
| Feldergruppe | [[!UICONTROL Zuordnung der Auswertungsergebnisse für Einverständnisrichtlinien mit Metadaten]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | Es werden Details für das Auswertungsergebnis mehrerer Einverständnisrichtlinien erfasst, einschließlich Metadateninformationen zu Ein- und Austritten bei Einverständnisrichtlinien. |

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Das Feld `ID` wurde in `name` umbenannt, und das vorherige Feld `name` heißt jetzt `friendlyName`. |
| Datentyp | [[!UICONTROL Details zu Entscheidungsvorschlägen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Das Feld `selectionStrategy` wurde hinzugefügt, mit dem Details einer Auswahlstrategie erfasst werden. |
| Feldergruppe | [[!UICONTROL Erlebnisereignis – Interaktionen bei Vorschlägen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Die Feldergruppe ist jetzt mit der Klasse [!UICONTROL Journey-Schrittereignis] kompatibel. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Das Feld `ID` wurde in `name` umbenannt. |
| Datentyp | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Eine Musteränderung der Videosegmenteigenschaft wurde zurückgesetzt. |
| Datentyp | [[!UICONTROL Informationen zu QoE-Daten]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Das Feld `droppedFrameCount` wurde entfernt. |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Das Feld `isAuthorized` wurde in `authorized` umbenannt und sein `type` wurde in eine Zeichenfolge umgewandelt, wobei es sich zuvor um einen Booleschen Wert handelte. |
| Datentyp | [[!UICONTROL Lieferung]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Es wurden mehrere neue Felder hinzugefügt: `shipDate`, `trackingNumber` und `trackingURL`. |
| Feldergruppe | [[!UICONTROL AJO-Entitätsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Es wurden mehrere neue Felder hinzugefügt: `journeyNodeID`, `journeyNodeName` und `journeyModeType`. |
| Feldergruppe | [[!UICONTROL Kundenerlebnisereignis]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Die Feldergruppe ist jetzt auch mit der Klasse [!UICONTROL Zusammenfassungsmetriken] kompatibel. |
| Feldergruppe | [[!UICONTROL Produkt-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Das Feld `productTriggers` befindet sich jetzt unter einem `weather`-Objekt. |
| Feldergruppe | [[!UICONTROL Relative Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Das Feld `relativeTriggers` befindet sich jetzt unter einem `weather`-Objekt. |
| Feldergruppe | [[!UICONTROL Starke Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Das Feld `severeTriggers` befindet sich jetzt unter einem `weather`-Objekt. |
| Feldergruppe | [[!UICONTROL Wetter-Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Die Feld `weatherTriggers` ist jetzt unter einem `weather`-Objekt verschachtelt. |
| Feldergruppe | [[!UICONTROL XDM-bezogene Geschäftskonten]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Die Feldgruppe ist jetzt stabil. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Bevorstehende Einstellung** {#deprecation}

Um Redundanz im Lebenszyklus der Segmentzugehörigkeit zu entfernen, läuft der `Existing`-Status Ende März 2023 für die [Karte für die Segmentzugehörigkeit](../../xdm/field-groups/profile/segmentation.md) aus. Eine Folgemitteilung wird das genaue Datum der Einstellung enthalten.

Nach der Einstellung werden in einem Segment qualifizierte Profile als `Realized` und disqualifizierte Profile weiterhin als `Exited` dargestellt. Dies führt zu Gleichheit bei dateibasierten Zielen mit `Active`- und `Expired`-Segmentstatus.

Diese Änderung könnte sich auf Sie auswirken, wenn Sie [Unternehmensziele](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) verwenden und automatisierte nachgelagerte Prozesse basierend auf dem `Existing`-Status anwenden. Überprüfen Sie Ihre nachgelagerten Integrationen, falls dies auf Sie zutrifft. Wenn Sie über einen bestimmten Zeitraum hinaus an der Identifizierung neu qualifizierter Profile interessiert sind, sollten Sie eine Kombination des `Realized`-Status und der `lastQualificationTime` bei Ihrer Segmentzugehörigkeitszuordnung erwägen. Weitere Informationen erhalten Sie von Ihren Adobe-Support-Mitarbeitenden.

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit Profildaten, finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Massenwertimport in Segment Builder | Segment Builder unterstützt jetzt den Import mehrerer Werte, entweder durch Hochladen einer CSV- oder TSV-Datei oder durch manuelles Einfügen durch Kommas getrennter Werte. Weitere Informationen finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Ablauf der Zugehörigkeit zu einer externen Zielgruppe | Standardmäßig werden externe Zielgruppenzugehörigkeiten 30 Tage lang aufbewahrt. Um sie länger aufzubewahren, verwenden Sie das `validUntil`-Feld während der Aufnahme von Zielgruppendaten. |
| Beenden der Segmentzugehörigkeit durch die Plattform | Jede Segmentzugehörigkeit, die sich basierend auf dem `lastQualificationTime`-Feld für mehr als 30 Tage im `Exited`-Status befindet, wird gelöscht. |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Zulassen des Benutzerzugriffs auf Unterordner der Cloud-Speicherquellen | Sie können jetzt den Zugriff auf einen bestimmten Unterordner Ihrer Cloud-Speicherquelle definieren, wenn Sie ein neues Konto erstellen. Nach der Erstellung können Benutzende nur auf Daten aus dem zulässigen Unterordner zugreifen. Diese Funktion steht den folgenden Cloud-Speicherquellen zur Verfügung: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) und [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Verfügbarkeit der Betaversion von [!DNL SugarCRM] | [!DNL SugarCRM]-Quellen sind jetzt in der Betaversion verfügbar. Verwenden Sie die Quellen [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM]-Konto an Experience Platform. Weitere Informationen finden Sie im [[!DNL SugarCRM] Überblick](../../sources/connectors/crm/sugarcrm.md). |
