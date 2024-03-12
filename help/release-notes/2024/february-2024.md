---
title: Adobe Experience Platform – Versionshinweise Februar 2024
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2024.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: aa33f7006b1a3abf7d19ffe3e0d5e5ee39fe9a5d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 29%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Donnerstag, 21. Februar 2024**

Aktualisierungen vorhandener Funktionen im Experience Platform:

- [Warnhinweise](#alerts)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Tab Verlauf der Warnhinweise | Als Experience Platform-Administrator können Sie die Funktion zum Verwalten von Abonnenten von Warnhinweisen verwenden, um einer Adobe-Benutzer-ID, einer externen E-Mail-Adresse oder einer E-Mail-Gruppenliste einen Warnhinweis zuzuweisen. Weitere Informationen finden Sie unter [Dokumentation zur Warn-Benutzeroberfläche](../../observability/alerts/ui.md) für weitere Informationen zum Tab Verlauf. |

{style="table-layout:auto"}

Weitere Informationen zu Warnungen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Web-In-App-Messaging-Unterstützung im Web SDK](../../web-sdk/personalization/web-in-app-messaging.md) | Das Adobe Experience Platform Web SDK unterstützt jetzt die Konfiguration von Web-In-App-Nachrichten für Adobe Journey Optimizer-Kampagnen. |

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
| [Gainsight PX-Verbindung](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX ist eine Produkterlebnisplattform, mit der Produktteams verstehen können, wie Benutzer ihre Produkte verwenden, Feedback erfassen und In-App-Interaktionen wie Produktumgehungen erstellen können, um das Onboarding und die Produktakzeptanz zu steigern. |
| [Verbindung zwischen Mailchimp-Tags](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp ist eine beliebte Marketing-Automatisierungsplattform und E-Mail-Marketing-Service. Sie können den Connector Mailchimp-Tags verwenden, um Ihre Kontakte zu strukturieren, zu beschriften oder zu kategorisieren. |
| [SAP Commerce-Verbindung](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce ist eine Cloud-basierte E-Commerce-Plattform-Lösung für B2B- und B2C-Unternehmen und ist als Teil des SAP Customer Experience-Portfolios verfügbar. Mit diesem Ziel können Sie Ihre Kundendetails in SAP Commerce von einer bestehenden Experience Platform-Audience aktualisieren. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Allgemeine verfügbare Kontozielgruppen aktivieren | Die Funktion zum Aktivieren von Kontozielgruppen für bestimmte Ziele ist jetzt allgemein für Unternehmen verfügbar, die die [B2B](/help/rtcdp/overview.md#rtcdp-b2b) und [B2B](/help/rtcdp/overview.md#rtcdp-b2p) Editionen von Real-time Customer Data Platform. Tutorial lesen unter [Aktivieren von Kontozielgruppen](/help/destinations/ui/activate-account-audiences.md) um vollständige Informationen zu erhalten, einschließlich unterstützter Ziele. |
| Digital Markets Act - Instrumente zur Durchsetzung der Zustimmung für Google-Ziele | Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Kundenabgleich](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)und die [Display &amp; Video 360-API](https://developers.google.com/display-video/api/guides/getting-started/overview) um die Erfüllung und die Zustimmungsanforderungen zu unterstützen, die im Rahmen der [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union ([EU-Richtlinie zur Benutzereinwilligung](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Zustimmungsanforderungen wird voraussichtlich ab dem 6. März 2024 in Kraft treten. <br/><br/> Um die EU-Politik zur Einwilligung von Nutzern einzuhalten und im Europäischen Wirtschaftsraum (EWR) weiterhin Zielgruppenlisten für Benutzer zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Einwilligung der Endnutzer weitergeben. Als Google-Partner bietet Ihnen Adobe die nötigen Tools, um diese Zustimmungsanforderungen gemäß DMA in der Europäischen Union zu erfüllen.<br/><br/>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Einverständnisrichtlinie](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) zum Herausfiltern von Profilen ohne Zustimmung müssen keine Maßnahmen ergriffen werden.<br/><br/>Kunden, die keine Adobe Privacy &amp; Security Shield erworben haben, müssen die [Segmentdefinition](../../segmentation/home.md#segment-definitions) Funktionen in [Segment Builder](../../segmentation/ui/segment-builder.md) , um Profile ohne Zustimmung herauszufiltern, damit die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiterhin verwendet werden. |
| [!BADGE Beta]{type=Informative} Neuanordnen von Zuordnungsfeldern für Batch-Ziele | Sie können jetzt die Reihenfolge der Spalten in Ihren CSV-Exporten ändern, indem Sie die Zuordnungsfelder per Drag-and-Drop in die [Mapping](../../destinations/ui/activate-batch-profile-destinations.md#mapping) Schritt. Die Reihenfolge der zugeordneten Felder in der Benutzeroberfläche entspricht der Reihenfolge der Spalten in der exportierten CSV-Datei von oben nach unten, wobei die oberste Zeile die ganz links in der CSV-Datei ist. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern. |
| [!BADGE Beta]{type=Informative} Vorgewählte standardmäßige Exportpläne für Batch-Ziele | Experience Platform legt nun automatisch einen Standardzeitplan für jeden Dateiexport fest. Siehe die Dokumentation unter [Zielgruppenexporte planen](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) , um zu erfahren, wie Sie den Standardzeitplan ändern. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern. |
| [!BADGE Beta]{type=Informative} Zeitpläne zur Massenbearbeitung von Zielgruppenaktivierungen für Batch-Ziele | Sie können jetzt den Aktivierungsplan für mehrere Zielgruppen in großen Mengen über die [Aktivierungsdaten](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) Seite. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern. |
| [!BADGE Beta]{type=Informative} Massenexport von Dateien bei Bedarf an Batch-Zielen | Sie können jetzt Zielgruppen stapelweise zu Batch-Zielen exportieren, indem Sie die [Exportieren von Dateien On-Demand](../../destinations/ui/export-file-now.md) Funktionalität. <br/><br/> Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Werkzeuge | Verwenden Sie jetzt nicht nur Objekttypen für Zustimmungs- und Governance-Regeln, sondern auch Sandbox-Tools, um Schemas ohne aktivierte einheitliche Profile zu importieren, beim Import eines Segments nach fehlenden Attributen in der Ziel-Sandbox zu suchen und standardmäßig die vorhandene Zusammenführungsrichtlinie zu verwenden. Weitere Informationen zu diesen Funktionen finden Sie im Abschnitt [Handbuch zur Sandbox-Tools-Benutzeroberfläche](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie im Abschnitt [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Kontozielgruppen | Kundenzielgruppen sind jetzt allgemein verfügbar! Sie können jetzt die Kontosegmentierung verwenden, um die vollständige Leichtigkeit und Komplexität der Marketing-Segmentierungserfahrung von benutzerbezogenen Zielgruppen zu kontobasierten Zielgruppen in den B2B- und B2P-Editionen der Echtzeit-Kundenplattform zu bringen. In dieser Version können Sie benutzerspezifische Zielgruppen als Prädikat für kontobasierte Zielgruppen verwenden, Suchfunktionen hinzufügen, die Verwendung benutzerdefinierter Entitäten unterstützen und mit Data Governance konform sein. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Übersicht über Kontozielgruppen](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] source | Verwenden Sie die [[!DNL Acxiom Prospecting Data Import] source](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) zum Abrufen und Zuordnen von Daten aus [!DNL Acxiom] Prospektivdienst zu Experience Platform. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
