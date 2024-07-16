---
keywords: Experience Platform; Query Service; Query Service; Query
title: Anwendungsbeispiel für Adobe Experience Platform Query Service
description: Ein durchgehendes Beispiel, das die Vielseitigkeit und Vorteile von Adobe Experience Platform Query Service demonstriert.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 38689125a43ad0b1a12a00efe6800bb310d7557c
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Anwendungsbeispiel für Adobe Experience Platform [!DNL Query Service]

Dieses Dokument und die zugehörige Videopräsentation bieten einen durchgängigen End-to-End-Workflow, der zeigt, wie Adobe Experience Platform [!DNL Query Service] die strategischen Geschäftseinblicke Ihres Unternehmens nutzt. In diesem Handbuch werden die folgenden Schlüsselkonzepte anhand eines Anwendungsbeispiels zum Abbruch von der Suche veranschaulicht:

* Die zentrale Bedeutung der Datenverarbeitung für die Maximierung des Potenzials von Adobe Experience Platform.
* Methoden zum Erstellen der Abfrage basierend auf Ihrer vorhandenen Datenarchitektur.
* Stellen Sie die Datenqualität sicher, die Ihren Anforderungen entspricht, und sorgen Sie für Methoden zur Reduzierung von Fehlern.
* Der Prozess zum Planen einer Abfrage für die nachfolgende Verwendung in der Segmentierung und in Personalisierungszielen.
* Die einfache Möglichkeit für Marketingexperten, abgeleitete Datensätze durch den Einsatz von [!DNL Query Service] in ihre Zielgruppen einzubeziehen.

## Ziele {#objectives}

Diese Workflow-Demonstration beruht auf mehreren Adobe Experience Platform-Diensten. Wenn Sie fortfahren möchten, sollten Sie die folgenden Funktionen und Dienste gut verstehen:

* Die [Grundlagen der Experience-Datenmodell (XDM)-Schemakomposition](../../xdm/schema/composition.md)
* Erstellen von Datensätzen und Erfassen von Daten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)[
* Erfassen von Daten mithilfe des Adobe Analytics-Quell-Connectors ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=de)[
* [Segmentierung](../../segmentation/home.md)
* [Ziele](../../destinations/home.md)

Im Beispiel zum Abbruch der Suche wird die Verwendung von Adobe [!DNL Analytics] -Daten verwendet, um eine bestimmte umsetzbare Zielgruppe zu erstellen. Die Zielgruppe wurde so optimiert, dass sie alle Kunden einbezieht, die die Website in den letzten vier Tagen besucht, aber keinen Kauf getätigt haben. Jedes Profil in der Zielgruppe wird dann mit der SKU mit dem höchsten Preis ausgewählt, die aus dem Verhaltensmuster des Kunden resultierte.

Die Abfrage selbst ist sehr verschreibungspflichtig und enthält nur Daten, die die Anwendungsfallkriterien für die Segmentdefinition erfüllen. Dies verbessert die Leistung, indem die Menge der verarbeiteten [!DNL Analytics] Daten minimiert wird. Außerdem werden die Daten nach Preis von der höchsten bis zur niedrigsten sortiert und die SKU mit dem höchsten Preis ausgewählt, die der Benutzer durchsuchte.

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

## Beispiel für abgebrochenen Durchsuchen mit Adobe Analytics[!DNL Query Service] {#video-example}

Die folgende Videopräsentation bietet einen ganzheitlichen, realen Anwendungsfall für Ihre Experience Platform-Daten mit dem Schwerpunkt auf [!DNL Query Service]- und Adobe-Analyseintegrationen.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Vorteile von [!DNL Query Service] {#benefits}

Die von [!DNL Query Service] bereitgestellten Funktionen dienen vielen Zwecken. Sie können sie verwenden, um komplexe Logik für die Segmentierung, die Berechnung verschiedener personalisierter Attribute zur nachgelagerten Verwendung oder die Erstellung Ihrer Zielgruppen erheblich zu vereinfachen.

Mit [!DNL Query Service] können Sie Einschränkungen in Ihre Abfragen einbeziehen, um den Prozess der Erstellung von Zielgruppen zu vereinfachen. Dies verbessert die Datenqualität, indem sichergestellt wird, dass die richtigen Daten für Ihre Zielgruppen geeignet sind. Die Aufrechterhaltung der Qualität Ihrer Abfrageergebnisse in einer präzisen Zielgruppe und hilft bei der Datenzuverlässigkeit. Sie können Ihre Audience auch speichern, indem Sie Schemas und benutzerdefinierte Tabellen basierend auf Attributen erstellen, die aus Ihrer Abfrage abgeleitet wurden. Eine benutzerdefinierte Tabelle kann für Profil aktiviert werden und Sie können diese Datenpunkte für die Segmentierung und Personalisierung verwenden. Diese Funktion unterstützt Marketingexperten, die eine klare Zielgruppe erstellen möchten.

Durch das Einschließen von Logik in Ihre Abfrage, die wiederkehrende oder statische Bedingungen erfüllt, extrahiert [!DNL Query Service] auch die Last einer aufwändigen Segmentierung.

Adobe Experience Platform bietet ein Daten-Repository und die erforderlichen Tools, um Ihre Daten effizient und zuverlässig zu aktivieren. Durch die Speicherung von Daten in Platform können Sie Attribute bei der Ausführung anderer Prozesse ableiten und die Notwendigkeit, Daten zur Bearbeitung und Verarbeitung in Drittanbieter-Tools zu exportieren, entfällt. Diese Verarbeitungskosten können sich stark auf die Zeitleiste eines Projekts auswirken, wenn es um Hunderte von Attributen oder Kampagnen geht. Dadurch erhalten Marketingexperten einen zentralen Standort, an dem sie auf ihre Daten zugreifen und Kampagnen erstellen können. Außerdem erhalten sie eine sehr dynamische Möglichkeit, Nachrichten zu segmentieren und zu personalisieren.

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie sich [!DNL Query Service] nicht nur auf die Qualität Ihrer Daten und die einfache Segmentierung auswirkt, sondern auch auf seine Bedeutung innerhalb Ihrer Datenarchitektur für den gesamten durchgehenden Workflow. Weitere SQL-Beispiele, die Adobe Analytics mit [!DNL Query Service] verwenden, finden Sie im Anwendungsfall [Adobe Analytics Merchandising-Variablen](./merchandising-variables.md).

Andere Dokumente, die die Vorteile von [!DNL Query Service] für die strategischen geschäftlichen Einblicke Ihres Unternehmens demonstrieren, sind das Beispiel für den [Bot-Filtervorgang](./bot-filtering.md) .

Alternativ können diese Dokumente für Ihr Verständnis der Funktionen von [!DNL Query Service] von Vorteil sein:

* [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md)
* [Anleitung für die Organisation von Daten-Assets](../best-practices/organize-data-assets.md).


