---
title: Adobe Experience Platform – Versionshinweise Februar 2024
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2024.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 25%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Donnerstag, 21. Februar 2024**

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Warnhinweise](#alerts)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Registerkarte „Warnhinweisverlauf“ | Als Experience Platform-Administrator können Sie die Funktion Warnhinweis-Abonnenten verwalten verwenden, um einen Warnhinweis einer Adobe-Benutzer-ID, einer externen E-Mail-Adresse oder einer E-Mail-Gruppenliste zuzuweisen. Weitere Informationen zur Registerkarte „Verlauf[ finden Sie in der ](../../observability/alerts/ui.md) zur Warnhinweis-Benutzeroberfläche. |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Web-In-App-Messaging-Unterstützung in Web SDK](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK unterstützt jetzt die Konfiguration von Web-In-App-Nachrichten für Adobe Journey Optimizer-Kampagnen. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie im Abschnitt [Datenerfassung – Übersicht](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Gainsight PX-Verbindung](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX ist eine Produkterlebnisplattform, mit der Produkt-Teams verstehen können, wie Benutzer ihre Produkte verwenden, Feedback einholen und In-App-Interaktionen wie exemplarische Vorgehensweisen für Produkte erstellen können, um das Onboarding von Benutzern und die Produktakzeptanz zu fördern. |
| [Mailchimp-Tags-Verbindung](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp ist eine beliebte Marketing-Automatisierungsplattform und E-Mail-Marketing-Service. Sie können den Mailchimp Tags-Connector verwenden, um Ihre Kontakte zu strukturieren, zu kennzeichnen oder zu kategorisieren. |
| [SAP Commerce-Verbindung](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce ist eine Cloud-basierte E-Commerce-Plattformlösung für B2B- und B2C-Unternehmen und als Teil des SAP Customer Experience Portfolios verfügbar. Sie können dieses Ziel verwenden, um Ihre Kundendaten in SAP Commerce von einer bestehenden Experience Platform-Zielgruppe aus zu aktualisieren. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Kontozielgruppen aktivieren, die allgemein verfügbar sind | Die Funktion zum Aktivieren von Account-Zielgruppen für bestimmte Ziele ist jetzt allgemein für Unternehmen verfügbar, die die [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)- und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-Editionen von Real-Time Customer Data Platform erwerben. Lesen Sie das Tutorial [Aktivieren von Konto-Zielgruppen](/help/destinations/ui/activate-account-audiences.md), um vollständige Informationen zu erhalten, einschließlich unterstützter Ziele. |
| Tools zur Durchsetzung von Einverständniserklärungen für Google-Ziele | Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union definiert sind ([EU-Richtlinie zur ](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Zustimmungspflichten wird voraussichtlich ab dem 6. März 2024 in Kraft treten. <br/><br/> Um die EU-Richtlinie zur Benutzerzustimmung einzuhalten und weiterhin Zielgruppenlisten für Nutzer im Europäischen Wirtschaftsraum (EWR) zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Zustimmung der Endnutzer weitergeben. Als Google-Partner stellt Adobe Ihnen die erforderlichen Tools zur Verfügung, um diese Zustimmungsanforderungen gemäß dem DMA in der Europäischen Union zu erfüllen.<br/><br/>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Einverständnisrichtlinie“ ](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) haben, um nicht einverstandene Profile herauszufiltern, müssen keine Maßnahmen ergreifen.<br/><br/>Kunden, die Adobe Privacy &amp; Security Shield nicht erworben haben, müssen die Funktionen [Segmentdefinition](../../segmentation/home.md#segment-definitions) in [Segment Builder](../../segmentation/ui/segment-builder.md) verwenden, um nicht einverstandene Profile herauszufiltern, damit die vorhandenen Real-Time CDP Google-Ziele ohne Unterbrechung weiterhin verwendet werden können. |
| [!BADGE Beta]{type=Informative} Ordnen Sie Zuordnungsfelder für Batch-Ziele neu an | Sie können jetzt die Reihenfolge der Spalten in Ihren CSV-Exporten ändern, indem Sie die Zuordnungsfelder im Schritt [Zuordnung“ ](../../destinations/ui/activate-batch-profile-destinations.md#mapping) und ablegen. Die Reihenfolge der zugeordneten Felder in der Benutzeroberfläche wird in der Reihenfolge der Spalten in der exportierten CSV-Datei von oben nach unten widergespiegelt, wobei die oberste Zeile die Spalte in der CSV-Datei ganz links ist. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. |
| [!BADGE Beta]{type=Informative} Vorab ausgewählte standardmäßige Exportpläne für Batch-Ziele | Experience Platform legt jetzt automatisch einen Standardzeitplan für jeden Dateiexport fest. Weitere Informationen zum Ändern des Standardzeitplans finden [ in der Dokumentation unter Planen ](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) Zielgruppenexporten“. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. |
| [!BADGE Beta]{type=Informative} Massenbearbeitung von Zielgruppen-Aktivierungszeitplänen für Batch-Ziele | Sie können jetzt den Aktivierungsplan für mehrere Zielgruppen stapelweise über die Seite „Aktivierungsdaten[ bearbeiten](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. |
| [!BADGE Beta]{type=Informative} Massenexport von Dateien nach Bedarf an Batch-Ziele | Sie können Zielgruppen jetzt über die Funktion [Dateien bei Bedarf exportieren](../../destinations/ui/export-file-now.md) stapelweise in Batch-Ziele exportieren. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Werkzeuge | Zusätzlich zur Unterstützung von Objekttypen für Einverständnis- und Governance-Regeln verwenden Sie jetzt die Sandbox-Tools , um Schemas zu importieren, für die keine einheitlichen Profile aktiviert sind. Außerdem prüfen Sie beim Importieren eines Segments, ob in der Ziel-Sandbox fehlende Attribute vorhanden sind, und verwenden Sie standardmäßig die vorhandene Zusammenführungsrichtlinie. Weitere Informationen zu diesen Funktionen finden Sie im [Handbuch zur Sandbox-Tooling-Benutzeroberfläche](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Experience Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Konto-Zielgruppen | Account-Zielgruppen sind jetzt allgemein verfügbar! Sie können jetzt die Kontosegmentierung verwenden, um die volle Einfachheit und Komplexität des Marketing-Segmentierungserlebnisses von personenbasierten Zielgruppen zu Account-basierten Zielgruppen in den B2B- und B2P-Editionen von Real-time Customer Experience Platform zu bringen. In dieser Version können Sie personenbasierte Zielgruppen als Prädikat für kontobasierte Zielgruppen verwenden, Suchfunktionen hinzufügen, die Verwendung benutzerdefinierter Entitäten unterstützen und mit Data Governance konform sind. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Übersicht über Kontozielgruppen](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] | Verwenden Sie die [[!DNL Acxiom Prospecting Data Import] Quelle](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) um Daten von [!DNL Acxiom] Interessenten-Service abzurufen und sie Experience Platform zuzuordnen. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
