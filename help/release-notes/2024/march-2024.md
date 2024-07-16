---
title: Adobe Experience Platform – Versionshinweise März 2024
description: Versionshinweise März 2024 für Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 33%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 19. März 2024**

>[!TIP]
>
>Verwenden Sie das [Adobe Experience Platform-Glossar](/help/landing/glossary.md), um sich mit der in Real-time Customer Data Platform und Adobe Experience Platform verwendeten Terminologie vertraut zu machen. Wenn Sie einen bestimmten Begriff, den Sie suchen, nicht finden können, verwenden Sie die Feedback-Optionen auf der Seite, um die Hinzufügung neuer Begriffe zum Glossar anzufordern.

Aktualisierungen vorhandener Funktionen im Experience Platform:

- [Katalog-Service](#catalog-service)
- [Datenerfassung](#data-collection)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Katalog-Service {#catalog-service}

Catalog Service ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Während alle Daten, die in Experience Platform aufgenommen werden, als Dateien und Ordner im Data Lake gespeichert sind, enthält der Katalog die Metadaten und Beschreibungen dieser Dateien und Ordner zu Such- und Überwachungszwecken.

| Funktion | Beschreibung |
| --- | --- |
| Mehr Aktionen | Um Vorgänge flexibler zu gestalten und Sie bei der Verwaltung Ihrer Daten zu unterstützen, können Sie jetzt die Funktion &quot;Mehr Aktionen&quot;in der Detailansicht verwenden, um zusätzliche Aufgaben für einen Datensatz durchzuführen. Sie können den Datensatz entweder löschen oder für die Verwendung mit dem Echtzeit-Kundenprofil aktivieren, indem Sie ihn auf der Detailseite eines ausgewählten Datensatzes auswählen.<br>**Hinweis:** Wenn Sie einen Datensatz für die Profilaufnahme aktivieren, muss das Schema des Datensatzes mit dem Echtzeit-Kundenprofil kompatibel sein.<br>![Der Arbeitsbereich &quot;Datensätze&quot;mit dem Arbeitsbereich [!UICONTROL ... Mehr] Dropdown-Menü hervorgehoben.](../2024/assets/march/more-actions.png "Der Arbeitsbereich &quot;Datensätze&quot;mit dem Dropdown-Menü &quot;Mehr&quot;."){width="100" zoomable="yes"}.<br>Lesen Sie die Dokumentation zum [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md) , um weitere Informationen zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen zum Katalog-Service finden Sie in der [Übersicht über den Katalog-Service](../../catalog/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Zuordnungsfunktionen für Adobe Analytics | Sie können jetzt die folgenden Funktionen verwenden, um Ereignisdaten aus Adobe Analytics zu extrahieren: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Weitere Informationen zu diesen Funktionen finden Sie im Leitfaden für die [Datenvorbereitung-Funktionen](../../data-prep/functions.md#analytics-functions) . |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Datenvorbereitung - Übersicht](../../data-prep/home.md) .

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterungen | [!DNL Merkury] Tag-Erweiterung | Die [[!DNL Merkury] Tag-Erweiterung](https://exchange.adobe.com/apps/ec/600027/merkury-tag) bietet branchenführende Übereinstimmungsraten für anonyme Website-Besucher mit einer [!DNL Merkury] -ID. Marken können die Funktionen des Tags [!DNL Merkury] und des Adobe nutzen, um in Echtzeit personalisierte Website-Erlebnisse bereitzustellen. Darüber hinaus ermöglicht das Tag [!DNL Merkury] das Wachstum digitaler Erstanbieterdaten zusammen mit verbundenen Online- und Offline-Kundenprofilen. |

{style="table-layout:auto"}

Weiterführende Informationen zur Datenerfassung finden Sie in der [Übersicht zur Datenerfassung](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue und aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Typ | Beschreibung |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom Data Enhancement-Verbindung](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Neu | Verwenden Sie diesen Connector, um Erstanbieterprofile von Real-Time CDP nach Acxiom zu aktivieren, um Daten anzureichern und über Marketingkanäle hinweg zu verwenden. Sie können dann die Acxiom-Quelle verwenden, um die Profile mit erweiterten Daten zu importieren und in Real-Time CDP mit ihnen zu arbeiten. |
| [(Beta) Acxiom Prospect Unterdrückungsverbindung](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Neu | Exportieren Sie Ihre Erstanbieterzielgruppen in das Acxiom-Ziel, damit Acxiom bekannte oder konvertierte Kunden unterdrücken kann. Verwenden Sie dann den Quell-Connector [Acxiom Prospektion data import](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) , um Interessenten-Listen von Acxiom zu erfassen und zu aktivieren, wobei Ihre bekannten oder konvertierten Kunden entfernt werden. |
| [Amazon Ads-Verbindung](../../destinations/catalog/advertising/amazon-ads.md) | Update | Beim Export von Daten an das Amazon Ads-Ziel können Sie die Daten jetzt an die Amazon-DSP oder das Amazon-Marketing Cloud weiterleiten (neu). |
| [Onboarding-Verbindung für LiveRamp](../../destinations/catalog/advertising/liveramp-onboarding.md) | Update | Das LiveRamp Onboarding-Ziel unterstützt jetzt Sendungen an die Instanzen in Europa und Australien [!DNL LiveRamp] [!DNL SFTP]. Die maximal exportierte Dateigröße wurde ebenfalls auf 10 Millionen Zeilen erhöht (von 5 Millionen zuvor). |

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
| Experience Platform UI Map-Datentypunterstützung | Passen Sie die Datenstruktur Ihres Experience-Datenmodells (XDM) weiter an, indem Sie Zuordnungsfelder in der Platform-Benutzeroberfläche definieren. Sie können jetzt Zuordnungsfelder im Schema Editor erstellen, um flexible Datenstrukturen zu modellieren oder Schlüssel-Wert-Paare effizient zu speichern. Wählen Sie &quot;Zuordnung&quot;aus der Dropdown-Liste Typ aus, wenn Sie ein neues Feld definieren, um die Unterfelder zu konfigurieren und sie Feldergruppen zuzuweisen. Unterstützte Zuordnungs-Werttypen sind Zeichenfolge und Ganzzahl.<br>![Der Schemaeditor mit hervorgehobenen Feldern vom Typ Typ und Typ Zuordnungs-Wert.](../2024/assets/march/maps.png "Der Schemaeditor mit hervorgehobenen Feldern vom Typ Typ und Typ Zuordnungs-Wert."){width="100" zoomable="yes"}<br> Informationen zum Definieren von Zuordnungsfeldern in der Benutzeroberfläche ](../../xdm/ui/fields/map.md) finden Sie im UI-Handbuch.[ |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Massenaktionen | Das Zielgruppeninventar unterstützt jetzt Massenaktionen. Mithilfe von Massenaktionen können Sie schnell mehrere Zielgruppen auswählen, um sie in einen Ordner zu verschieben, Tags anzuwenden, Zugriffsbeschriftungen anzuwenden oder zu löschen. <br> ![Massenaktionen im Arbeitsbereich der Benutzeroberfläche &quot;Zielgruppen&quot;.](../2024/assets/march/bulk-actions.png "Massenaktionen im Arbeitsbereich der Benutzeroberfläche &quot;Zielgruppen&quot;."){width="100" zoomable="yes"} <br>Weitere Informationen zu dieser Funktion finden Sie in der [Übersicht über Audience Portal](../../segmentation/ui/audience-portal.md#bulk-actions) . |

{style="table-layout:auto"}

Weitere Informationen zum Segmentation Service finden Sie in der [Segmentation Service - Übersicht](../../segmentation/home.md) .

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue und aktualisierte Quellen**

| Funktion | Typ | Beschreibung |
| --- | --- | --- |
| [!BADGE Beta]{type=informative} [!DNL Acxiom Data Ingestion] | Neu | Verwenden Sie die [[!DNL Acxiom Data Ingestion] Quelle](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) , um [!DNL Acxiom] -Daten in Real-time Customer Data Platform aufzunehmen und Erstanbieterprofile anzureichern. Anschließend können Sie Ihre mit [!DNL Acxiom] angereicherten Erstanbieterprofile verwenden, um Zielgruppen zu verbessern und über Marketingkanäle hinweg zu aktivieren. <br> ![Die Acxiom-Datenerfassungsquelle.](../2024/assets/march/acxiom-data-ingestion.png "Neue Acxiom-Datenerfassungsquelle."){width="100" zoomable="yes"} <br> Lesen Sie die [[!DNL Acxiom Data Ingestion] Übersicht](../../sources/connectors/data-partners/acxiom-data-ingestion.md) , um Informationen zu den ersten Schritten zu erhalten. |
| [!BADGE Beta]{type=informative} [!DNL Stripe] | Neu | Verwenden Sie die [[!DNL Stripe] Quelle](../../sources/connectors/payments/stripe.md) , um Daten zu erfassen, die während des Kaufvorgangs von Ihren Kunden in die Experience Platform erfasst wurden. Nach der Erfassung können Sie diese Daten verwenden, um personalisierte Angebote zu erstellen und umfassendere geschäftliche Einblicke zu gewinnen. <br> ![Die Stripe-Quelle.](../2024/assets/march/stripe.png "Neue Stripe-Quelle."){width="100" zoomable="yes"} <br> Lesen Sie die [[!DNL Stripe] Übersicht](../../sources/connectors/payments/stripe.md) , um Informationen zu den ersten Schritten zu erhalten. |
| Benutzeroberflächenunterstützung für [!DNL Snowflake Streaming] | Neu | Sie können jetzt die [[!DNL Snowflake Streaming] Quelle](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) in der Experience Platform-Benutzeroberfläche verwenden, um Daten aus Ihrer [!DNL Snowflake] -Datenbank zu streamen. <br> ![Die Snowflake-Streaming-Quelle.](../2024/assets/march/snowflake-streaming.png "Neue Snowflake-Streaming-Quelle."){width="100" zoomable="yes"} <br> Lesen Sie die [[!DNL Snowflake Streaming] Übersicht](../../sources/connectors/databases/snowflake-streaming.md) , um Informationen zu den ersten Schritten zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).
