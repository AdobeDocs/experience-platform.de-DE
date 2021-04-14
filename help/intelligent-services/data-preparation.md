---
keywords: Experience Platform;Home;Intelligente Dienste;beliebte Themen;Intelligenter Dienst;Intelligente Dienste
solution: Experience Platform, Intelligent Services
title: Vorbereiten von Daten für die Verwendung in Intelligent Services
topic: Intelligent Services
description: Damit Intelligent Services Einblicke aus den Daten Ihrer Marketing-Ereignis erhalten kann, müssen die Daten semantisch erweitert und in einer Standardstruktur gepflegt werden. Intelligente Dienste nutzen Experience Data Model-(XDM-)Schema, um dies zu erreichen. Insbesondere müssen alle in Intelligent Services verwendeten Datensätze dem XDM-Schema von Consumer ExperienceEvent (CEE) entsprechen.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
translation-type: tm+mt
source-git-commit: b311a5970a121a3277bdb72f5a1285216444b339
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 2%

---

# Daten für die Verwendung in [!DNL Intelligent Services] vorbereiten

Damit [!DNL Intelligent Services] Einblicke aus Ihren Marketing-Ereignissen entdecken kann, müssen die Daten semantisch erweitert und in einer Standardstruktur gepflegt werden. [!DNL Intelligent Services] XDM-Schema  [!DNL Experience Data Model] (XDM) nutzen, um dies zu erreichen. Insbesondere müssen alle in [!DNL Intelligent Services] verwendeten Datensätze dem Consumer ExperienceEvent (CEE) XDM-Schema entsprechen.

In diesem Dokument erhalten Sie allgemeine Anleitungen zur Zuordnung Ihrer Marketing-Ereignis-Daten aus mehreren Kanälen zu diesem Schema. In diesen Anleitungen werden Informationen zu wichtigen Feldern im Schema zusammengefasst, die Ihnen bei der Bestimmung helfen, wie Sie Ihre Daten effektiv der Struktur zuordnen können.

## Workflow-Übersicht

Der Vorbereitungsprozess hängt davon ab, ob Ihre Daten in Adobe Experience Platform oder extern gespeichert werden. In diesem Abschnitt werden die notwendigen Schritte zusammengefasst, die Sie in beiden Szenarien unternehmen müssen.

### Vorbereitung externer Daten

Wenn Ihre Daten außerhalb von [!DNL Experience Platform] gespeichert werden, führen Sie die folgenden Schritte aus:

1. Wenden Sie sich an Adobe Consulting Services, um Zugangsdaten für einen dedizierten Azurblase Datenspeicherung Container anzufordern.
1. Laden Sie Ihre Daten mit Ihren Zugriffsberechtigungen in den Blob-Container hoch.
1. Arbeiten Sie mit Adobe Consulting Services, um Ihre Daten dem [Consumer ExperienceEvent-Schema](#cee-schema) zuzuordnen und in [!DNL Intelligent Services] einzufügen.

### [!DNL Experience Platform] Datenaufbereitung

Wenn Ihre Daten bereits in [!DNL Platform] gespeichert sind, führen Sie die folgenden Schritte aus:

1. Überprüfen Sie die Struktur des [Consumer ExperienceEvent-Schemas](#cee-schema) und stellen Sie fest, ob Ihre Daten Feldern zugeordnet werden können.
1. Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in [!DNL Intelligent Services] zu erfassen, oder befolgen Sie die Schritte in diesem Handbuch](#mapping), wenn Sie die Daten selbst zuordnen möchten.[

## Das CEE-Schema {#cee-schema}

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Individuums in Bezug auf digitale Marketing-Ereignis (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist aufgrund seiner semantisch definierten Felder (Spalten) erforderlich, wobei unbekannte Namen vermieden werden, die sonst die Daten weniger eindeutig machen würden.[!DNL Intelligent Services]

Das CEE-Schema erfasst wie alle XDM ExperienceEvent-Schema den zeitreihenbasierten Systemzustand, in dem ein Ereignis (oder eine Reihe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des jeweiligen Objekts. Erfahrungs-Ereignisse sind Faktenberichte über das, was geschehen ist, und somit sind sie unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist.

[!DNL Intelligent Services] Verwenden Sie mehrere Schlüsselfelder in diesem Schema, um Einblicke aus Ihren Marketing-Ereignissen-Daten zu generieren, die sich alle auf der Stammebene befinden und erweitert werden, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schema ist auch das CEE-Mixin erweiterbar. Mit anderen Worten, dem CEE-Mixin können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehreren Schemas enthalten sein.

Ein vollständiges Beispiel des Mixins finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Darüber hinaus können Sie die folgende [JSON-Datei](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) als Beispiel für die Strukturierung von Daten zur Erfüllung des CEE-Schemas Ansicht und Kopieren verwenden. In beiden Beispielen erfahren Sie mehr über die im folgenden Abschnitt beschriebenen Schlüsselfelder, um zu ermitteln, wie Sie dem Schema Ihre eigenen Daten zuordnen können.

## Schlüsselfelder

Es gibt mehrere Schlüsselfelder im CEE-Mixin, die verwendet werden sollten, damit [!DNL Intelligent Services] nützliche Einblicke generiert. In diesem Abschnitt werden der Verwendungsfall und die erwarteten Daten für diese Felder beschrieben und Links zur Referenzdokumentation für weitere Beispiele bereitgestellt.

### Obligatorische Felder

Die Verwendung aller Schlüsselfelder wird dringend empfohlen, es gibt jedoch zwei Felder, die **erforderlich** sind, damit [!DNL Intelligent Services] funktioniert:

* [Ein primäres Identitätsfeld](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:Kanal](#channel) (nur für Attribution AIS obligatorisch)

#### Primär identity {#identity}

Eines der Felder in Ihrem Schema muss als primäres Identitätsfeld festgelegt werden, das es [!DNL Intelligent Services] ermöglicht, jede Instanz von Zeitreihendaten mit einer Person zu verknüpfen.

Sie müssen das beste Feld als primäre Identität basierend auf der Quelle und der Art Ihrer Daten festlegen. Ein Identitätsfeld muss einen **Identitäts-Namensraum** enthalten, der den Typ der Identitätsdaten angibt, den das Feld als Wert erwartet. Zu den gültigen Namensräumen gehören:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(für Adobe Audience Manager-IDs)
* &quot;aaid&quot;(für Adobe Analytics-IDs)

Wenn Sie sich nicht sicher sind, welches Feld Sie als primäre Identität verwenden sollten, wenden Sie sich an Adobe Consulting Services, um die beste Lösung zu finden. Wenn keine primäre Identität festgelegt ist, verwendet die Anwendung &quot;Intelligent Service&quot;das folgende Standardverhalten:

| Standard | Attribution AI | Customer AI |
| --- | --- | --- |
| Identitätsspalte | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Um eine primäre Identität festzulegen, navigieren Sie auf der Registerkarte **[!UICONTROL Schema]** zu Ihrem Schema und wählen Sie den Hyperlink für den Schema-Namen aus, um das **[!DNL Schema Editor]** zu öffnen.

![Zu Schema navigieren](./images/data-preparation/navigate_schema.png)

Navigieren Sie anschließend zu dem Feld, das Sie als primäre Identität definieren möchten, und wählen Sie es aus. Das Menü **[!UICONTROL Feldeigenschaften]** wird für dieses Feld geöffnet.

![Feld auswählen](./images/data-preparation/find_field.png)

Blättern Sie im Menü **[!UICONTROL Feldeigenschaften]** nach unten, bis Sie das Kontrollkästchen **[!UICONTROL Identität]** gefunden haben. Nach dem Aktivieren des Kontrollkästchens wird die Option zum Festlegen der ausgewählten Identität als **[!UICONTROL Primär identity]** angezeigt. Wählen Sie auch dieses Kontrollkästchen aus.

![Kontrollkästchen auswählen](./images/data-preparation/set_primary_identity.png)

Als Nächstes müssen Sie einen **[!UICONTROL Identity-Namensraum]** aus der Liste vordefinierter Namensraum im Dropdown-Menü angeben. In diesem Beispiel wird der ECID-Namespace ausgewählt, da eine Adobe Audience Manager-ID `mcid.id` verwendet wird. Wählen Sie **[!UICONTROL Übernehmen]**, um die Aktualisierungen zu bestätigen, und wählen Sie dann **[!UICONTROL Speichern]** in der oberen rechten Ecke aus, um die Änderungen in Ihrem Schema zu speichern.

![Speichern Sie die Änderungen](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Dieses Feld gibt den Zeitpunkt an, zu dem das Ereignis aufgetreten ist. Dieser Wert muss als Zeichenfolge gemäß ISO 8601 angegeben werden.

#### xdm:channel {#channel}

>[!NOTE]
>
>Dieses Feld ist nur bei Verwendung von Attribution AI obligatorisch.

Dieses Feld stellt den Marketing-Kanal im Zusammenhang mit dem ExperienceEvent dar. Das Feld enthält Informationen zum Typ des Kanals, Medientyp und Standort.

![](./images/data-preparation/channel.png)

**Beispiel-Schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:channel` finden Sie im Schema [Experience Kanal](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) spec. Einige Beispielzuordnungen finden Sie in der Tabelle [unter](#example-channels).

#### Beispiel für Kanal-Zuordnungen {#example-channels}

Die folgende Tabelle enthält einige Beispiele für Marketing-Kanal, die dem Schema `xdm:channel` zugeordnet sind:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/Kanal-types/search | bezahlt | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/Kanal-types/social | verdient | Klicks |
| Anzeigen | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | Klicks |
| E-Mail  | https:/<span>/ns.adobe.com/xdm/Kanal-types/email | bezahlt | Klicks |
| Interner Werber | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | Klicks |
| Display ViewThrough | https:/<span>/ns.adobe.com/xdm/Kanal-types/display | bezahlt | impressions |
| QR-Codeumleitung | https:/<span>/ns.adobe.com/xdm/Kanal-types/direct | besetzt | Klicks |
| Mobile | https:/<span>/ns.adobe.com/xdm/Kanal-types/mobile | besetzt | Klicks |

### Empfohlene Felder

Die übrigen Schlüsselfelder werden in diesem Abschnitt beschrieben. Diese Felder sind zwar nicht unbedingt erforderlich, damit [!DNL Intelligent Services] funktioniert, es wird jedoch dringend empfohlen, möglichst viele davon zu verwenden, um tiefer gehende Einblicke zu erhalten.

#### xdm:productListItems

Dieses Feld enthält eine Reihe von Artikeln, die die von einem Kunden ausgewählten Produkte darstellen, einschließlich der Produkt-SKU, des Namens, des Preises und der Menge.

![](./images/data-preparation/productListItems.png)

**Beispiel-Schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie im [Commerce details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) spec.

#### xdm:commerce

Dieses Feld enthält handelsspezifische Informationen zum ExperienceEvent, einschließlich Bestellnummer und Zahlungsinformationen.

![](./images/data-preparation/commerce.png)

**Beispiel-Schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:commerce` finden Sie im [Commerce details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) spec.

#### xdm:web

Dieses Feld enthält Webdetails zum ExperienceEvent, wie Interaktion, Seitendetails und Werber.

![](./images/data-preparation/web.png)

**Beispiel-Schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie im [ExperienceEvent-Webdetails-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) spec.

#### xdm:marketing

Dieses Feld enthält Informationen zu Marketing-Aktivitäten, die mit dem Touchpoint aktiv sind.

![](./images/data-preparation/marketing.png)

**Beispiel-Schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie in der Spezifikation [marketing sechma](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Zuordnen und Erfassen von Daten {#mapping}

Sobald Sie festgestellt haben, ob Ihre Marketing-Ereignis-Daten dem CEE-Schema zugeordnet werden können, müssen Sie als Nächstes ermitteln, welche Daten Sie in [!DNL Intelligent Services] einführen möchten. Alle in [!DNL Intelligent Services] verwendeten Verlaufsdaten müssen innerhalb des minimalen Zeitfensters von vier Monaten an Daten liegen, zuzüglich der Anzahl der Tage, die als Lookback-Zeitraum vorgesehen sind.

Wenden Sie sich nach der Entscheidung über den zu sendenden Datenbereich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in den Dienst zu integrieren.

Wenn Sie ein [!DNL Adobe Experience Platform]-Abonnement haben und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden von Adobe Experience Platform

>[!NOTE]
>
>Die folgenden Schritte erfordern ein Abonnement zur Experience Platform. Wenn Sie keinen Zugriff auf die Plattform haben, fahren Sie mit dem Abschnitt [Nächste Schritte](#next-steps) fort.

In diesem Abschnitt wird der Arbeitsablauf für die Zuordnung und Eingabe von Daten in die Experience Platform zur Verwendung in [!DNL Intelligent Services] beschrieben, einschließlich Links zu Tutorials für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und eines Datasets

Wenn Sie bereit sind, Ihre Daten für die Erfassung vorzubereiten, müssen Sie zunächst ein neues XDM-Schema erstellen, das das CEE-Mixin verwendet. Die folgenden Lernprogramme erläutern die Erstellung eines neuen Schemas in der Benutzeroberfläche oder API:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Die oben stehenden Lernprogramme folgen einem allgemeinen Arbeitsablauf zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie das CEE-Mixin dem Schema hinzufügen.

Nachdem Sie das CEE-Mixin zum Schema hinzugefügt haben, können Sie je nach Bedarf weitere Mixins in Ihre Daten einfügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie auf der Grundlage dieses Schemas einen neuen Datensatz erstellen. Die folgenden Lernprogramme erläutern den Vorgang zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API:

* [Erstellen eines Datensatzes in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create)  (Workflow zur Verwendung eines vorhandenen Schemas)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

Nachdem der Datensatz erstellt wurde, können Sie ihn in der Plattform-Benutzeroberfläche im Arbeitsbereich **[!UICONTROL Datensätze]** finden.

![](images/data-preparation/dataset-location.png)

#### hinzufügen Identitätsfelder in den Datensatz

Wenn Sie Daten von [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] oder einer anderen externen Quelle eingeben, haben Sie die Möglichkeit, ein Schema als Identitätsfeld festzulegen. Um ein Schema als Identitätsfeld festzulegen, Ansicht Sie den Abschnitt zum Festlegen von Identitätsfeldern im [UI-Tutorial](../xdm/tutorials/create-schema-ui.md#identity-field) oder [API-Tutorial](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) zum Erstellen eines Schemas.

Wenn Sie Daten aus einer lokalen CSV-Datei aufnehmen, können Sie den nächsten Abschnitt [Zuordnung und Eingabe von Daten](#ingest) überspringen.

#### Daten zuordnen und erfassen {#ingest}

Nachdem Sie ein CEE-Schema und einen Dataset erstellt haben, können Sie Ihre Datentabellen dem Schema zuordnen und diese Daten in Platform erfassen. Anweisungen dazu, wie Sie dies in der Benutzeroberfläche durchführen, finden Sie im Lernprogramm [Zuordnen einer CSV-Datei zu einem XDM-Schema](../ingestion/tutorials/map-a-csv-file.md). Sie können die folgende JSON-Beispieldatei [verwenden, um den Erfassungsvorgang zu testen, bevor Sie Ihre eigenen Daten verwenden.](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)

Nachdem ein Datensatz gefüllt wurde, kann derselbe Datensatz zum Erfassen zusätzlicher Datendateien verwendet werden.

Wenn Ihre Daten in einer unterstützten Drittanbieteranwendung gespeichert werden, können Sie auch einen [Quellanschluss](../sources/home.md) erstellen, um Ihre Marketing-Ereignis-Daten in Echtzeit in [!DNL Platform] zu erfassen.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in [!DNL Intelligent Services]. Wenn Sie je nach Anwendungsfall weitere Beratung benötigen, wenden Sie sich bitte an den Adobe Consulting Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten gefüllt haben, können Sie [!DNL Intelligent Services] verwenden, um Erkenntnisse zu generieren. Die ersten Schritte finden Sie in den folgenden Dokumenten:

* [Attribution AI – Übersicht](./attribution-ai/overview.md)
* [Kunden-KI – Übersicht](./customer-ai/overview.md)
