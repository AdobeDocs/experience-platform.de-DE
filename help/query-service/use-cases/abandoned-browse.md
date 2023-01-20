---
keywords: Experience Platform; Query Service; Query Service; Query
title: Anwendungsbeispiel für Adobe Experience Platform Query Service
description: Ein durchgängiges Beispiel, um die Vielseitigkeit und Vorteile von Adobe Experience Platform Query Service zu demonstrieren.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 3%

---

# Anwendungsbeispiel für Adobe Experience Platform [!DNL Query Service]

Dieses Dokument und die zugehörige Videopräsentation bieten einen umfassenden End-to-End-Workflow, der zeigt, wie Adobe Experience Platform funktioniert [!DNL Query Service] profitieren von den strategischen Geschäftseinblicken Ihres Unternehmens. In diesem Handbuch werden die folgenden Schlüsselkonzepte anhand eines Anwendungsbeispiels zum Abbruch von der Suche veranschaulicht:

* Die zentrale Bedeutung der Datenverarbeitung für die Maximierung des Potenzials von Adobe Experience Platform.
* Methoden zum Erstellen der Abfrage basierend auf Ihrer vorhandenen Datenarchitektur.
* Stellen Sie die Datenqualität sicher, die Ihren Anforderungen entspricht, und sorgen Sie für Methoden zur Reduzierung von Fehlern.
* Der Prozess zum Planen einer Abfrage für die nachfolgende Verwendung in der Segmentierung und in Personalisierungszielen.
* Die einfache Möglichkeit für Marketing-Experten, abgeleitete Attribute in ihre Segmente einzuschließen, indem die Vorteile von [!DNL Query Service].

## Ziele {#objectives}

Diese Workflow-Demonstration beruht auf mehreren Adobe Experience Platform-Diensten. Wenn Sie fortfahren möchten, sollten Sie die folgenden Funktionen und Dienste gut verstehen:

* Die [Grundlagen der Experience-Datenmodell (XDM)-Schemakomposition](../../xdm/schema/composition.md)
* Anleitung [Erstellen von Datensätzen und Erfassen von Daten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de)
* Anleitung [Daten mithilfe des Adobe Analytics-Quell-Connectors erfassen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=de)
* [Segmentierung](../../segmentation/home.md)
* [Ziele](../../destinations/home.md)

Im Beispiel zum Abbruch der Suche wird die Verwendung von Adobe verwendet [!DNL Analytics] Daten, um eine bestimmte umsetzbare Zielgruppe zu erstellen. Die Zielgruppe wurde so optimiert, dass sie alle Kunden einbezieht, die die Website in den letzten vier Tagen besucht, aber keinen Kauf getätigt haben. Jedes Profil in der Zielgruppe wird dann mit der SKU mit dem höchsten Preis ausgewählt, die aus dem Verhaltensmuster des Kunden resultierte.

Die Abfrage selbst ist sehr verschreibungspflichtig und enthält nur Daten, die die Anwendungsfallkriterien für die Segmentdefinition erfüllen. Dies verbessert die Leistung, indem die Anzahl der [!DNL Analytics] Daten, die verarbeitet werden. Außerdem werden die Daten nach Preis von der höchsten bis zur niedrigsten sortiert und die SKU mit dem höchsten Preis ausgewählt, die der Benutzer durchsuchte.

Die in der Präsentation verwendete Abfrage ist unten dargestellt:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] Beispiel für abgebrochene Suche mit Adobe Analytics {#video-example}

Die folgende Videopräsentation bietet einen ganzheitlichen, realen Anwendungsfall für Ihre Experience Platform-Daten, der auf Folgendes ausgerichtet ist: [!DNL Query Service] und Adobe Analytics-Integrationen.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Vorteile von [!DNL Query Service] {#benefits}

Die durch [!DNL Query Service] dient vielen Zwecken. Sie können sie verwenden, um komplexe Logik für die Segmentierung, die Berechnung verschiedener personalisierter Attribute zur nachgelagerten Verwendung oder die Erstellung Ihrer Segmente erheblich zu vereinfachen.

[!DNL Query Service] ermöglicht Ihnen, Einschränkungen in Ihre Abfragen einzubeziehen, um den Prozess der Segmenterstellung zu vereinfachen. Dies verbessert die Datenqualität, indem sichergestellt wird, dass die richtigen Daten für Ihre Segmente qualifiziert sind, und präzisere Zielgruppen erstellt werden. Die Aufrechterhaltung der Qualität Ihrer Abfrageergebnisse in einer präzisen Zielgruppe und hilft bei der Datenzuverlässigkeit. Sie können Ihre Audience auch speichern, indem Sie Schemas und benutzerdefinierte Tabellen basierend auf Attributen erstellen, die aus Ihrer Abfrage abgeleitet wurden. Eine benutzerdefinierte Tabelle kann für Profil aktiviert werden und Sie können diese Datenpunkte für die Segmentierung und Personalisierung verwenden. Diese Funktion unterstützt Marketingexperten, die eine klare Zielgruppe erstellen möchten.

Indem Sie auch eine Logik in Ihre Abfrage einfügen, die wiederkehrende oder statische Bedingungen erfüllt, [!DNL Query Service] extrahiert die Last einer detaillierten Segmentierung.

Adobe Experience Platform bietet ein Daten-Repository und die erforderlichen Tools, um Ihre Daten effizient und zuverlässig zu aktivieren. Durch die Speicherung von Daten in Platform können Sie Attribute bei der Ausführung anderer Prozesse ableiten und die Notwendigkeit, Daten zur Bearbeitung und Verarbeitung in Drittanbieter-Tools zu exportieren, entfällt. Diese Verarbeitungskosten können sich stark auf die Planung eines Projekts auswirken, wenn Hunderte von Attributen oder Kampagnen verarbeitet werden. Dadurch erhalten Marketing-Experten einen zentralen Ort, an dem sie auf ihre Daten zugreifen und Kampagnen erstellen können. Außerdem erhalten sie eine sehr dynamische Möglichkeit, Nachrichten zu segmentieren und zu personalisieren.

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie [!DNL Query Service] wirkt sich nicht nur auf die Qualität Ihrer Daten und die einfache Segmentierung aus, sondern auch auf deren Bedeutung innerhalb Ihrer Datenarchitektur für den gesamten End-to-End-Workflow. Für zutreffendere SQL-Beispiele, die Adobe Analytics mit [!DNL Query Service], siehe [Anwendungsfall für Adobe Analytics Merchandising-Variablen](./merchandising-variables.md).

Andere Dokumente, die die Vorteile von [!DNL Query Service] zu den strategischen geschäftlichen Einblicken Ihres Unternehmens sind die [Anwendungsfall für Bot-Filter](./bot-filtering.md) Beispiel.

Alternativ können diese Dokumente für Ihr Verständnis von [!DNL Query Service] Funktionen:

* [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md)
* [Informationen zur Ordnung von Daten-Medienelementen](../best-practices/organize-data-assets.md).


