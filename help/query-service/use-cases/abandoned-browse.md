---
keywords: Experience Platform;Abfrage-Service;Abfrage-Service;Abfrage
title: Anwendungsbeispiel für Adobe Experience Platform Query Service
description: Ein Beispiel, das die Vielseitigkeit und die Vorteile des Abfrage-Service von Adobe Experience Platform veranschaulicht.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 38689125a43ad0b1a12a00efe6800bb310d7557c
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Anwendungsbeispiel für Adobe Experience Platform [!DNL Query Service]

Dieses Dokument und die zugehörige Videopräsentation bieten einen allgemeinen End-to-End-Workflow, der zeigt, wie Adobe Experience Platform [!DNL Query Service] die strategischen geschäftlichen Erkenntnisse Ihres Unternehmens nutzt. Anhand eines Anwendungsfalls zum Durchsuchen von Abbrüchen als Beispiel zeigt dieses Handbuch die folgenden Schlüsselkonzepte:

* Die zentrale Bedeutung der Datenverarbeitung für die Maximierung des Potenzials von Adobe Experience Platform.
* Möglichkeiten zum Erstellen der Abfrage basierend auf Ihrer vorhandenen Datenarchitektur.
* Stellen Sie sicher, dass die Datenqualität Ihren Anforderungen entspricht und Methoden zur Behebung von Mängeln vorhanden sind.
* Der Prozess zur Planung einer Abfrage, die mit einer bestimmten Häufigkeit ausgeführt wird, um sie nachgelagert in der Segmentierung und bei Zielen für die Personalisierung zu verwenden.
* Die [!DNL Query Service] von ermöglicht es Marketing-Experten, abgeleitete Datensätze in ihre Zielgruppen aufzunehmen.

## Ziele {#objectives}

Diese Workflow-Demonstration beruht auf mehreren Adobe Experience Platform-Services. Wenn Sie dem Beispiel folgen möchten, sollten Sie über ein gutes Verständnis der folgenden Funktionen und Services verfügen:

* Die [Grundlagen der Schemakomposition des Experience-Datenmodells (XDM)](../../xdm/schema/composition.md)
* So erstellen [ Datensätze und nehmen Daten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* So [ Sie Daten mithilfe des Adobe Analytics-Quell-Connectors aufnehmen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=de)
* [Segmentierung](../../segmentation/home.md)
* [Ziele](../../destinations/home.md)

Das Beispiel für den Abbruch von Durchsuchen-Vorgängen konzentriert sich auf die Verwendung von Adobe-[!DNL Analytics]-Daten zum Erstellen einer bestimmten nachvollziehbaren Zielgruppe. Die Zielgruppe wird so angepasst, dass sie alle Kunden umfasst, die in den letzten vier Tagen die Website besucht, aber keinen Kauf getätigt haben. Jedes Profil in der Zielgruppe wird dann mit der SKU mit dem höchsten Preis angesprochen, der aus dem Verhaltensmuster des Kunden resultierte.

Die Abfrage selbst ist sehr präskriptiv und enthält nur Daten, die die Anwendungsfallkriterien für die Segmentdefinition erfüllen. Dies verbessert die Leistung, indem die Menge der verarbeiteten [!DNL Analytics] minimiert wird. Außerdem werden die Daten nach Preis vom höchsten zum niedrigsten Preis sortiert und die preisgünstigste SKU ausgewählt, die der Benutzer durchsucht hat.

Die in der Präsentation verwendete Abfrage wird unten angezeigt:

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

## Beispiel für einen [!DNL Query Service]-Abbruch mit Adobe Analytics {#video-example}

Die folgende Videopräsentation bietet einen ganzheitlichen Anwendungsfall für Ihre Experience Platform-Daten in der realen Welt, der sich auf [!DNL Query Service]- und Adobe-Analytics-Integrationen konzentriert.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Vorteile von [!DNL Query Service] {#benefits}

Die von [!DNL Query Service] bereitgestellten Funktionen dienen vielen Zwecken. Sie können ihn verwenden, um komplexe Logik für die Segmentierung einzubeziehen, verschiedene personalisierte Attribute zur nachgelagerten Verwendung zu berechnen oder die Erstellung Ihrer Zielgruppen erheblich zu vereinfachen.

[!DNL Query Service] können Sie Einschränkungen in Ihre Abfragen einbeziehen, um den Prozess der Zielgruppenerstellung zu vereinfachen. Dadurch wird die Datenqualität verbessert, indem sichergestellt wird, dass für Ihre Zielgruppen die richtigen Daten qualifiziert sind. Die Aufrechterhaltung der Qualität Ihrer Abfrage führt zu einer genauen Zielgruppe und hilft bei der Datenzuverlässigkeit. Sie können Ihre Zielgruppe auch speichern, indem Sie Schemata und benutzerdefinierte Tabellen erstellen, die auf aus Ihrer Abfrage abgeleiteten Attributen basieren. Für Profile kann eine benutzerdefinierte Tabelle aktiviert werden, und Sie können diese Datenpunkte zur Segmentierung und Personalisierung verwenden. Diese Funktion unterstützt Marketing-Fachleute, die eine klare Zielgruppe erstellen möchten.

Indem Sie außerdem Logik in Ihre Abfrage aufnehmen, die alle wiederkehrenden oder statischen Bedingungen erfüllt, extrahiert [!DNL Query Service] den Aufwand für eine aufwändige Segmentierung.

Adobe Experience Platform bietet ein Daten-Repository und die erforderlichen Tools, um Ihre Daten effizient und zuverlässig zu aktivieren. Da Daten in Platform gespeichert bleiben, können Sie Attribute ableiten, während Sie andere Prozesse ausführen, und Sie müssen keine Daten mehr zur Bearbeitung und Verarbeitung in Tools von Drittanbietern exportieren. Ein solcher Verarbeitungsaufwand kann sich erheblich auf die Zeitleiste eines Projekts auswirken, wenn Hunderte von Attributen oder Kampagnen verarbeitet werden. Dadurch erhalten Marketing-Fachleute einen zentralen Ort, an dem sie auf ihre Daten zugreifen und Kampagnen erstellen können, sowie eine sehr dynamische Möglichkeit, ihre Nachrichten zu segmentieren und zu personalisieren.

## Nächste Schritte

Durch das Lesen dieses Dokuments sollten Sie jetzt verstehen, wie sich [!DNL Query Service] nicht nur auf die Qualität Ihrer Daten und die Einfachheit der Segmentierung auswirkt, sondern auch auf ihre Bedeutung in Ihrer Datenarchitektur für den gesamten End-to-End-Workflow. Anwendbare SQL-Beispiele, die Adobe Analytics mit [!DNL Query Service] verwenden, finden Sie im Anwendungsfall [Adobe Analytics-Merchandising-Variablen](./merchandising-variables.md).

Andere Dokumente, die die Vorteile der [!DNL Query Service] für die strategischen geschäftlichen Einblicke Ihres Unternehmens zeigen, sind [ Beispiel die ](./bot-filtering.md) „Bot-Filterung“.

Alternativ können diese Dokumente Ihr Verständnis [!DNL Query Service] Funktionen verbessern:

* [Leitlinien für die Ausführung von Abfragen](../best-practices/writing-queries.md)
* [Anleitung für die Organisation von Daten-Assets](../best-practices/organize-data-assets.md).


