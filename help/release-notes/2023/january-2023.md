---
title: Adobe Experience Platform - Versionshinweise Januar 2023
description: Die Versionshinweise für Adobe Experience Platform vom Januar 2023.
source-git-commit: c60c58e563a324c4f8f90eac04686f2190e8448d
workflow-type: tm+mt
source-wordcount: '2444'
ht-degree: 27%

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
- [Segmentation Service](#segmentation)
- [Quellen](#sources)

## Künstliche Intelligenz/Dienstleistungen des maschinellen Lernens {#ai-ml}

Mit den Services für künstliche Intelligenz und maschinelles Lernen können Marketing-Analysten und Praktiker die Leistung von KI/ML in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene Prognosen erstellen, die auf die Anforderungen eines Unternehmens zugeschnitten sind, ohne dass datenwissenschaftliche Kenntnisse erforderlich sind.

### Attributions-KI

Attribution AI wird verwendet, um Touchpoints, die zu Konversionsereignissen führen, Gutschriften zuzuordnen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| HIPAA-Bereitschaft | Gesundheitsschutzschild-Kunden können jetzt geschützte Gesundheitsinformationen in Attribution AIS und bestimmten anderen Experience Platformen empfangen, verwenden, verwalten oder übermitteln. Der Gesundheitsschild ist für Kunden im Gesundheitswesen bestimmt, die entweder eine gedeckte Einheit oder ein Unternehmensverbund im Rahmen des HIPAA sind. Weitere Informationen finden Sie in der Dokumentation unter [HIPAA und Adobe - Produkte und Dienstleistungen](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Zusätzliche Datensatzspalten mit Bewertungen bearbeiten | Sie können jetzt beim Bearbeiten vorhandener Modelle zusätzliche Score-Datensatzspalten (Berichtsspalten) hinzufügen oder entfernen. Dies erweitert die Flexibilität der Attributionsbewertungen, um Ihnen Einblicke in zusätzliche Dimensionen zu bieten, nachdem ein Modell bereits erstellt wurde. Siehe [Handbuch zur Attribution UI](../../intelligent-services/attribution-ai/user-guide.md) , um mehr zu erfahren. |

{style=&quot;table-layout:auto&quot;}

Siehe [KI-/ML-Dienste](../../intelligent-services/attribution-ai/overview.md) Übersicht für weitere Informationen.

### Kunden-KI

Customer AI für Real-time Customer Data Platform wird verwendet, um benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile in großem Maßstab zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| HIPAA-Bereitschaft | Gesundheitsschutzschild-Kunden können jetzt geschützte Gesundheitsinformationen in Customer AI für Real-time Customer Data Platform und bestimmte andere Experience Platform-basierte Anwendungen empfangen, verwenden, verwalten oder übermitteln. Der Gesundheitsschild ist für Kunden im Gesundheitswesen bestimmt, die entweder eine gedeckte Einheit oder ein Unternehmensverbund im Rahmen des HIPAA sind. Weitere Informationen finden Sie in der Dokumentation unter [HIPAA und Adobe - Produkte und Dienstleistungen](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style=&quot;table-layout:auto&quot;}

Siehe [KI-/ML-Dienste](../../intelligent-services/customer-ai/overview.md) Übersicht für weitere Informationen.

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

## Ziele (am 2. Februar aktualisiert) {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [(Beta) Verbindung zu Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Verwenden Sie die [!UICONTROL (Beta) Adobe Experience Cloud-Zielgruppen] Verbindung zum Freigeben von Segmenten aus Experience Platform für verschiedene Experience Platform-Lösungen wie Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target oder Marketo. |
| [Pega-Profil-Verbindung](../../destinations/catalog/personalization/pega-profile.md) | Verwenden Sie die [!DNL Pega Profile Connector] in Adobe Experience Platform , um eine ausgehende Live-Verbindung zu Ihrer [!DNL Amazon] S3-Datenspeicherung , um Profildaten regelmäßig in CSV-Dateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren. In [!DNL Pega Customer Decision Hub]können Sie Datenaufträge planen, um diese Profildaten aus dem S3-Speicher zu importieren, um die [!DNL Pega Customer Decision Hub] Profil. |
| [(Beta) Verbindung des Trade Desk CRM EU](../../destinations/catalog/advertising/tradedesk-emails.md) | Mit der Veröffentlichung der EUID (European Unified ID) sehen Sie jetzt zwei [!DNL The Trade Desk - CRM] Ziele im [Zielkatalog](/help/destinations/catalog/overview.md). <ul><li> Wenn Sie Daten in der EU beziehen, verwenden Sie bitte die **[!DNL The Trade Desk - CRM (EU)]** Ziel.</li><li> Wenn Sie Daten in der APAC- oder NAMER-Region beziehen, verwenden Sie bitte die **[!DNL The Trade Desk - CRM (NAMER & APAC)]** Ziel. </li></ul> |

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Verbesserung der Richtlinie zur Zustimmung für Paid Media für Integrationen mit Streaming-Zielen | Ein [Verbesserung der Durchsetzung von Zustimmungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) on [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations) für Anwendungsfälle zur Aktivierung gebührenpflichtiger Medien. Wenn Profile nicht mehr für eine Zustimmungsrichtlinie qualifiziert sind, kommuniziert Experience Platform jetzt proaktiv ihren Richtlinienausstieg an Streaming-Ziele. <br> <b>Hinweis</b>: Diese Funktion steht nur Kunden von **[!UICONTROL Datenschutz und Sicherheitsschild]** und der **[!UICONTROL Gesundheitsschild]**. |
| Neue Trennzeichenoptionen für Beta-Cloud-Speicher-Ziel-Connectoren | Drei neue Trennzeichenoptionen (Doppelpunkt `:`, Pipe, Semikolon `;`) sind jetzt für die neuen Beta-Cloud-Speicher-Ziele verfügbar - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Informationen zu den unterstützten [Dateiformatierungsoptionen](/help/destinations/ui/batch-destinations-file-formatting-options.md) für dateibasierte Ziele. |
| Neuer optionaler Parameter verfügbar in [Kundendatenfelder](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) Konfigurationen in [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Verwenden Sie diesen Parameter, wenn Sie ein Kundendatenfeld erstellen müssen, dessen Wert über alle von der Organisation eines Benutzers eingerichteten Ziel-Datenflüsse hinweg eindeutig sein muss. <br> Beispiel: die **[!UICONTROL Integrationsalias]** im Feld [[!UICONTROL Benutzerdefinierte Personalisierung]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) Das Ziel muss eindeutig sein, d. h. zwei separate Datenflüsse zu diesem Ziel dürfen für dieses Feld nicht denselben Wert haben. |

**Fehlerbehebungen und Verbesserungen** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Fehlerbehebung oder Verbesserung</b></td>
        <td><b>Beschreibung</b></td>
    </tr>
    <tr>
        <td>Aktualisiertes Exportverhalten für dateibasierte Ziele (PLAT-123316)</td>
        <td>Es wurde ein Problem im Verhalten von <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">obligatorische Attribute</a> beim Exportieren von Datendateien in Batch-Ziele. <br> Zuvor wurde überprüft, ob jeder Datensatz in den Ausgabedateien beide enthält: <ol><li>Ein Wert ungleich null des <code>mandatoryField</code> Spalte und</li><li>Ein Wert ungleich null für mindestens eines der anderen nicht obligatorischen Felder.</li></ol> Die zweite Bedingung wurde entfernt. Daher werden möglicherweise mehr Ausgabezeilen in Ihren exportierten Datendateien angezeigt, wie im folgenden Beispiel gezeigt:<br> <b> Beispielverhalten vor der Version vom Januar 2023 </b> <br> Obligatorisches Feld: <code>emailAddress</code> <br> <b>Eingabedaten zur Aktivierung</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Aktivierungsausgabe</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Beispielverhalten nach der Version vom Januar 2023 </b> <br> <b>Aktivierungsausgabe</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>UI- und API-Validierung für erforderliche Zuordnungen und doppelte Zuordnungen (PLAT-123316)</td>
        <td>Die Validierung wird jetzt in der Benutzeroberfläche und in der API wie folgt erzwungen, wenn <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">Zuordnungsfelder</a> im Workflow Ziele aktivieren :<ul><li><b>Erforderliche Zuordnungen</b>: Wenn das Ziel vom Zielentwickler mit den erforderlichen Zuordnungen eingerichtet wurde (z. B. die <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> Ziel), müssen diese erforderlichen Zuordnungen vom Benutzer hinzugefügt werden, wenn er Daten für das Ziel aktiviert. </li><li><b>Duplizieren von Zuordnungen</b>: Im Zuordnungsschritt des Aktivierungs-Workflows können Sie doppelte Werte in den Quellfeldern, aber nicht in den Zielfeldern hinzufügen. In der folgenden Tabelle finden Sie ein Beispiel für zulässige und verbotene Zuordnungskombinationen. <br><table><thead><tr><th>Zulässig/verboten</th><th>Quellfeld</th><th>Zielfeld</th></tr></thead><tbody><tr><td>Zugelassen</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email alias2</li></ul></td></tr><tr><td>Verboten</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

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
| Massenwertimport in Segment Builder | Segment Builder unterstützt jetzt den Import mehrerer Werte, entweder durch Hochladen einer CSV- oder TSV-Datei oder durch manuelles Einfügen von durch Kommas getrennten Werten. Weitere Informationen finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Ablauf der Mitgliedschaft in einer externen Zielgruppe | Standardmäßig werden externe Zielgruppenmitgliedschaften 30 Tage lang aufbewahrt. Um sie länger aufzubewahren, verwenden Sie die `validUntil` -Feld während der Erfassung von Zielgruppendaten. |
| Von der Plattform generierte Segmentmitgliedschaftsgültigkeit | Jede Segmentzugehörigkeit, die sich im `Exited` für mehr als 30 Tage, basierend auf dem `lastQualificationTime` -Feld kann gelöscht werden. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und ermöglicht es Ihnen, diese Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Zulassen des Benutzerzugriffs auf Unterordner der Cloud-Speicherquellen | Sie können jetzt den Zugriff auf einen bestimmten Unterordner Ihrer Cloud-Speicherquelle definieren, wenn Sie ein neues Konto erstellen. Nach der Erstellung können Benutzer nur auf Daten aus dem zulässigen Unterordner zugreifen. Diese Funktion steht den folgenden Cloud-Speicher-Quellen zur Verfügung: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)und [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Verfügbarkeit von Beta [!DNL SugarCRM] | [!DNL SugarCRM] -Quellen sind jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] Quellen zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM] -Konto auf Experience Platform. Weitere Informationen finden Sie im Abschnitt [[!DNL SugarCRM] Übersicht](../../sources/connectors/crm/sugarcrm.md). |