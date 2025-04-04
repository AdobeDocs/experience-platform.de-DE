---
title: Adobe Experience Platform – Versionshinweise März 2024
description: Versionshinweise März 2024 für Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 33%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 19. März 2024**

>[!TIP]
>
>Verwenden Sie das [Adobe Experience Platform-Glossar](/help/landing/glossary.md) um sich mit der in Real-Time Customer Data Platform und Adobe Experience Platform verwendeten Terminologie vertraut zu machen. Wenn Sie einen bestimmten Begriff, den Sie suchen, nicht finden können, verwenden Sie die Feedback-Optionen auf der Seite, um anzufordern, dass neue Begriffe dem Glossar hinzugefügt werden.

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Katalog-Service](#catalog-service)
- [Datenerfassung](#data-collection)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Alle in Experience Platform aufgenommenen Daten werden als Dateien und Ordner im Data Lake gespeichert. Catalog speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such- und Überwachungszwecke.

| Funktion | Beschreibung |
| --- | --- |
| Mehr Aktionen | Um Vorgänge flexibler zu gestalten und die Verwaltung Ihrer Daten zu erleichtern, können Sie jetzt die Funktion „Weitere Aktionen“ in der Detailansicht verwenden, um zusätzliche Aufgaben für einen Datensatz auszuführen. Sie können den Datensatz entweder löschen oder für die Verwendung mit dem Echtzeit-Kundenprofil auf der Detailseite eines ausgewählten Datensatzes aktivieren.<br>**Hinweis** Wenn Sie einen Datensatz für die Profilaufnahme aktivieren, muss das Schema des Datensatzes mit dem Echtzeit-Kundenprofil kompatibel sein.<br>![Der Arbeitsbereich Datensätze mit den [!UICONTROL … Mehr] Dropdown-Menü hervorgehoben.](../2024/assets/march/more-actions.png "Der Arbeitsbereich Datensätze mit hervorgehobenem Dropdown-Menü „Mehr“."){width="100" zoomable="yes"}.<br>Weitere Informationen finden [ in der Dokumentation ](../../catalog/datasets/user-guide.md)Benutzerhandbuch zu Datensätzen“. |

{style="table-layout:auto"}

Weitere Informationen zum Katalog-Service finden Sie in der [Übersicht über den Katalog-Service](../../catalog/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Zuordnungsfunktionen für Adobe Analytics | Sie können jetzt die folgenden Funktionen verwenden, um Ereignisdaten aus Adobe Analytics zu extrahieren: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Weitere Informationen zu diesen Funktionen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterungen | [!DNL Merkury] Tag-Erweiterung | Die [[!DNL Merkury] Tag-Erweiterung](https://exchange.adobe.com/apps/ec/600027/merkury-tag) bietet branchenführende Übereinstimmungsraten für anonyme Website-Besuchende mit einer [!DNL Merkury] ID. Marken können die Leistungsfähigkeit von [!DNL Merkury] Tag und Adobe nutzen, um personalisierte Website-Erlebnisse in Echtzeit bereitzustellen. Darüber hinaus ermöglicht das [!DNL Merkury]-Tag das Wachstum von digitalen First-Party-Daten zusammen mit verbundenen Online- und Offline-Kundenprofilen. |

{style="table-layout:auto"}

Weitere Informationen zur Datenerfassung finden Sie unter [Datenerfassung - Übersicht](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue und aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Typ | Beschreibung |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom Data Enhancement-Verbindung](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Neu | Verwenden Sie diesen Connector, um Erstanbieterprofile von Real-Time CDP für die Datenanreicherung und die Verwendung über Marketing-Kanäle hinweg zu aktivieren. Anschließend können Sie die Acxiom-Quelle verwenden, um die Profile mit erweiterten Daten zu importieren und mit ihnen in Real-Time CDP zu arbeiten. |
| Unterdrückungsverbindung für [(Beta) Acxiom Prospect](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Neu | Exportieren Sie Ihre Erstanbieter-Zielgruppen in das Acxiom-Ziel, damit Acxiom bekannte oder konvertierte Kundinnen und Kunden unterdrücken kann. Verwenden Sie dann den Quell-Connector [Akquise-Datenimport von Acxiom](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md), um Interessentenlisten von Acxiom aufzunehmen und zu aktivieren, wobei Ihre bekannten oder konvertierten Kunden entfernt werden. |
| [Amazon Ads-Verbindung](../../destinations/catalog/advertising/amazon-ads.md) | Update | Beim Exportieren von Daten an das Amazon Ads-Ziel können Sie die Daten jetzt an Amazon DSP oder Amazon Marketing Cloud (neu) weiterleiten. |
| [LiveRamp-Onboarding-Verbindung](../../destinations/catalog/advertising/liveramp-onboarding.md) | Update | Das LiveRamp-Onboarding-Ziel bietet jetzt Unterstützung für Sendungen nach Europa und Australien [!DNL LiveRamp] [!DNL SFTP]. Die maximale Größe der exportierten Datei wurde ebenfalls auf 10 Millionen Zeilen erhöht (von zuvor 5 Millionen). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Experience Platform UI Map-Datentypen | Passen Sie Ihre Experience-Datenmodell (XDM)-Datenstruktur weiter an, indem Sie Zuordnungsfelder in der Experience Platform-Benutzeroberfläche definieren. Sie können jetzt im Schema-Editor Zuordnungsfelder erstellen, um flexible Datenstrukturen zu modellieren oder Schlüssel-Wert-Paare effizient zu speichern. Wählen Sie beim Definieren eines neuen Felds „Zuordnung“ aus der Dropdown-Liste Typ aus, um Unterfelder zu konfigurieren und sie Feldergruppen zuzuweisen. Unterstützte Zuordnungswerttypen sind „String“ und „Integer“.<br>![Der Schemaeditor mit den hervorgehobenen Feldern Typ und Zuordnungswerttyp.](../2024/assets/march/maps.png "Der Schemaeditor mit den hervorgehobenen Feldern Typ und Zuordnungswerttyp."){width="100" zoomable="yes"}<br> Informationen zum [ (Definieren von Zuordnungsfeldern in der Benutzeroberfläche](../../xdm/ui/fields/map.md) finden Sie im Handbuch zur Benutzeroberfläche . |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Experience Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Massenaktionen | Das Zielgruppen-Inventar unterstützt jetzt Massenaktionen. Mithilfe von Massenaktionen können Sie schnell mehrere Zielgruppen auswählen, um sie in einen Ordner zu verschieben, Tags anzuwenden, Zugriffsbeschriftungen anzuwenden oder zu löschen. <br> ![Massenaktionen im Arbeitsbereich der Zielgruppen-Benutzeroberfläche.](../2024/assets/march/bulk-actions.png "Massenaktionen im Arbeitsbereich der Zielgruppen-Benutzeroberfläche."){width="100" zoomable="yes"} <br>Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Zielgruppenportal - Übersicht](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Weitere Informationen zum Segmentierungs-Service finden Sie unter [Segmentierungs-Service - Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue und aktualisierte Quellen**

| Funktion | Typ | Beschreibung |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | Neu | Verwenden Sie die [[!DNL Acxiom Data Ingestion] Quelle](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) um [!DNL Acxiom] Daten in Real-Time Customer Data Platform aufzunehmen und First-Party-Profile anzureichern. Anschließend können Sie Ihre mit [!DNL Acxiom] angereicherten First-Party-Profile verwenden, um Zielgruppen zu verbessern und über Marketing-Kanäle hinweg zu aktivieren. <br> ![Die Acxiom-Datenaufnahmequelle.](../2024/assets/march/acxiom-data-ingestion.png "Neue Acxiom-Datenquelle zur Datenaufnahme."){width="100" zoomable="yes"} <br> Lesen Sie [[!DNL Acxiom Data Ingestion] Übersicht](../../sources/connectors/data-partners/acxiom-data-ingestion.md) um Informationen zu den ersten Schritten zu erhalten. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | Neu | Verwenden Sie die [[!DNL Stripe] Quelle](../../sources/connectors/payments/stripe.md) um Daten, die während des Kaufablaufs von Ihren Kunden erfasst wurden, in Experience Platform aufzunehmen. Nach der Aufnahme können Sie diese Daten verwenden, um personalisierte Angebote zu erstellen und umfassendere geschäftliche Einblicke zu erschließen. <br> ![Die Stripe-Quelle.](../2024/assets/march/stripe.png "Neue Stripe-Quelle."){width="100" zoomable="yes"} <br> Lesen Sie [[!DNL Stripe] Übersicht](../../sources/connectors/payments/stripe.md) um Informationen zu den ersten Schritten zu erhalten. |
| UI-Unterstützung für [!DNL Snowflake Streaming] | Neu | Sie können jetzt die [[!DNL Snowflake Streaming] Quelle](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) in der Experience Platform-Benutzeroberfläche verwenden, um Daten aus Ihrer [!DNL Snowflake] zu streamen. <br> ![Die Snowflake-Streaming-Quelle.](../2024/assets/march/snowflake-streaming.png "Neue Snowflake-Streaming-Quelle."){width="100" zoomable="yes"} <br> Lesen Sie [[!DNL Snowflake Streaming] Übersicht](../../sources/connectors/databases/snowflake-streaming.md) um Informationen zu den ersten Schritten zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
