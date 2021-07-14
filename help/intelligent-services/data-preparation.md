---
keywords: Experience Platform; Startseite; Intelligent Services; beliebte Themen; intelligenter Dienst; Intelligent Service
solution: Experience Platform, Intelligent Services
title: Vorbereiten von Daten für die Verwendung in Intelligent Services
topic-legacy: Intelligent Services
description: Damit Intelligent Services Einblicke aus Ihren Marketing-Ereignisdaten gewinnen kann, müssen die Daten semantisch angereichert und in einer Standardstruktur verwaltet werden. Intelligent Services verwenden dazu Experience-Datenmodell (XDM)-Schemas.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: aa73f8f4175793e82d6324b7c59bdd44bf8d20f9
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 1%

---

# Vorbereiten von Daten für die Verwendung in [!DNL Intelligent Services]

Damit [!DNL Intelligent Services] Einblicke aus Ihren Marketing-Ereignisdaten erhalten kann, müssen die Daten semantisch angereichert und in einer Standardstruktur verwaltet werden. [!DNL Intelligent Services] nutzen Sie  [!DNL Experience Data Model] (XDM)-Schemas, um dies zu erreichen. Insbesondere müssen alle Datensätze, die in [!DNL Intelligent Services] verwendet werden, dem XDM-Schema Consumer ExperienceEvent (CEE) entsprechen oder den Adobe Analytics-Connector verwenden. Darüber hinaus unterstützt Customer AI den Adobe Audience Manager-Connector.

Dieses Dokument bietet allgemeine Anleitungen zum Zuordnen Ihrer Marketing-Ereignisdaten aus mehreren Kanälen zum CEE-Schema sowie Informationen zu wichtigen Feldern innerhalb des Schemas, anhand derer Sie bestimmen können, wie Ihre Daten effektiv der Struktur zugeordnet werden können. Wenn Sie planen, Adobe Analytics-Daten zu verwenden, lesen Sie bitte den Abschnitt [Adobe Analytics-Datenvorbereitung](#analytics-data). Wenn Sie planen, Adobe Audience Manager-Daten zu verwenden (nur Customer AI), lesen Sie bitte den Abschnitt für [Adobe Audience Manager-Datenvorbereitung](#AAM-data).

## Datenanforderungen

[!DNL Intelligent Services] erfordert je nach dem erstellten Ziel unterschiedliche Mengen historischer Daten. Unabhängig davon müssen die Daten, die Sie für **all** [!DNL Intelligent Services] vorbereiten, sowohl positive als auch negative Journey/Ereignisse enthalten. Negative und positive Ereignisse verbessern die Modellgenauigkeit und -genauigkeit.

Wenn Sie beispielsweise Customer AI verwenden, um die Tendenz zum Kauf eines Produkts vorherzusagen, benötigt das Modell für Customer AI sowohl Beispiele für erfolgreiche Kaufpfade als auch Beispiele für nicht erfolgreiche Pfade. Dies liegt daran, dass Customer AI während der Modellschulung versucht zu verstehen, welche Ereignisse und Journey zu einem Kauf führen. Dazu gehören auch die Aktionen von Kunden, die nichts gekauft haben, z. B. von Personen, die ihre Journey beim Hinzufügen eines Artikels zum Warenkorb angehalten haben. Diese Kunden können jedoch ähnliche Verhaltensweisen aufweisen. Customer AI kann jedoch Einblicke bieten und die wichtigsten Unterschiede und Faktoren, die zu einem höheren Tendenzwert führen, detailliert aufzeigen. In ähnlicher Weise erfordert Attribution AI sowohl Ereignistypen als auch Journey, um Metriken wie Touchpoint-Effektivität, Top-Konversionspfade und Aufschlüsselungen nach Touchpoint-Position anzuzeigen.

Weitere Beispiele und Informationen zu den Anforderungen an historische Daten finden Sie im Abschnitt [Customer AI](./customer-ai/input-output.md#data-requirements) oder [Attribution AI](./attribution-ai/input-output.md#data-requirements) Verlaufsdatenanforderungen in der Eingabe-/Ausgabedokumentation.

### Richtlinien für die Datenzuordnung

Es wird empfohlen, die Ereignisse eines Benutzers nach Möglichkeit einer gemeinsamen ID zuzuordnen. Beispielsweise können Sie Benutzerdaten mit &quot;id1&quot;über 10 Ereignisse hinweg haben. Später hat derselbe Benutzer die Cookie-ID gelöscht und wird bei den nächsten 20 Ereignissen als &quot;id2&quot;aufgezeichnet. Wenn Sie wissen, dass id1 und id2 demselben Benutzer entsprechen, empfiehlt es sich, alle 30 Ereignisse mit einer gemeinsamen ID zu verknüpfen.

Ist dies nicht möglich, sollten Sie jeden Satz von Ereignissen beim Erstellen Ihrer Modelleingabedaten als einen anderen Benutzer behandeln. Dadurch werden die besten Ergebnisse bei Modellschulung und -bewertung sichergestellt.

## Workflow-Zusammenfassung

Der Vorbereitungsprozess hängt davon ab, ob Ihre Daten in Adobe Experience Platform oder extern gespeichert werden. In diesem Abschnitt werden die erforderlichen Schritte für die beiden Szenarien zusammengefasst.

### Vorbereitung externer Daten

Wenn Ihre Daten außerhalb von Experience Platform gespeichert werden, müssen Sie Ihre Daten den erforderlichen und relevanten Feldern in einem [Consumer ExperienceEvent-Schema](#cee-schema) zuordnen. Dieses Schema kann mit benutzerdefinierten Feldergruppen erweitert werden, um Ihre Kundendaten besser zu erfassen. Nach der Zuordnung können Sie einen Datensatz mit Ihrem Customer ExperienceEvent-Schema erstellen und [Ihre Daten in Platform](../ingestion/home.md) aufnehmen. Der CEE-Datensatz kann dann beim Konfigurieren eines [!DNL Intelligent Service] ausgewählt werden.

Je nach dem [!DNL Intelligent Service], den Sie verwenden möchten, können verschiedene Felder erforderlich sein. Es empfiehlt sich, einem Feld Daten hinzuzufügen, wenn die Daten verfügbar sind. Weitere Informationen zu den erforderlichen Feldern finden Sie im Handbuch [Attribution AI](./attribution-ai/input-output.md) oder [Customer AI](./customer-ai/input-output.md) Eingabe-/Ausgabe-Handbuch.

### Adobe Analytics-Datenvorbereitung {#analytics-data}

Customer AI und Attribution AI unterstützen nativ Adobe Analytics-Daten. Um Adobe Analytics-Daten zu verwenden, führen Sie die in der Dokumentation beschriebenen Schritte aus, um einen [Analytics-Quell-Connector](../sources/tutorials/ui/create/adobe-applications/analytics.md) einzurichten.

Sobald der Quell-Connector Ihre Daten in Experience Platform streamt, können Sie Adobe Analytics während der Instanzkonfiguration als Datenquelle und danach als Datensatz auswählen. Alle erforderlichen Schemafeldgruppen und individuellen Felder werden während der Verbindungseinrichtung automatisch erstellt. Sie müssen die Datensätze nicht im CEE-Format ETL (Extract, Transform, Load) verschieben.

>[!IMPORTANT]
>
>Der Adobe Analytics-Connector benötigt bis zu vier Wochen, um Daten aufzustocken. Wenn Sie kürzlich eine Verbindung eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für den Kunden oder Attribution AI erforderliche Mindestlänge von Daten aufweist. Überprüfen Sie die Abschnitte mit den historischen Daten in [Customer AI](./customer-ai/input-output.md#data-requirements) oder [Attribution AI](./attribution-ai/input-output.md#data-requirements) und überprüfen Sie, ob Sie über genügend Daten für Ihr Prognoseziel verfügen.

### Adobe Audience Manager-Datenvorbereitung (nur Customer AI) {#AAM-data}

Customer AI unterstützt nativ Adobe Audience Manager-Daten. Um Audience Manager-Daten zu verwenden, führen Sie die in der Dokumentation beschriebenen Schritte aus, um einen [Quell-Connector für Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) einzurichten.

Sobald der Quell-Connector Ihre Daten an Experience Platform streamt, können Sie Adobe Audience Manager während Ihrer Customer AI-Konfiguration als Datenquelle und danach als Datensatz auswählen. Alle Schemafeldgruppen und einzelnen Felder werden während der Verbindungseinrichtung automatisch erstellt. Sie müssen die Datensätze nicht im CEE-Format ETL (Extract, Transform, Load) verschieben.

>[!IMPORTANT]
>
>Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die erforderliche Mindestlänge von Daten aufweist. Lesen Sie den Abschnitt zu historischen Daten in der [Eingabe-/Ausgabedokumentation](./customer-ai/input-output.md) für Customer AI und überprüfen Sie, ob Sie über genügend Daten für Ihr Prognoseziel verfügen.

### [!DNL Experience Platform] Datenvorbereitung

Wenn Ihre Daten bereits in [!DNL Platform] gespeichert sind und nicht über die Quell-Connectoren für Adobe Analytics oder Adobe Audience Manager (nur Customer AI) streamen, führen Sie die folgenden Schritte aus. Es wird dennoch empfohlen, das CEE-Schema zu verstehen.

1. Überprüfen Sie die Struktur des [Consumer ExperienceEvent-Schemas](#cee-schema) und stellen Sie fest, ob Ihre Daten Feldern zugeordnet werden können.
2. Wenden Sie sich an Adobe Consulting Services , um Ihre Daten dem Schema zuzuordnen und es in [!DNL Intelligent Services] aufzunehmen. Befolgen Sie die Schritte in diesem Handbuch](#mapping), wenn Sie die Daten selbst zuordnen möchten.[

## Grundlegendes zum CEE-Schema {#cee-schema}

Das Schema Consumer ExperienceEvent beschreibt das Verhalten einer Person in Bezug auf digitale Marketing-Ereignisse (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist für [!DNL Intelligent Services] erforderlich, da es semantisch genau definierte Felder (Spalten) enthält, sodass unbekannte Namen vermieden werden, die sonst dazu führen würden, dass die Daten weniger klar sind.

Das CEE-Schema erfasst wie alle XDM ExperienceEvent-Schemas den zeitreihenbasierten Status des Systems, in dem ein Ereignis (oder eine Reihe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des beteiligten Subjekts. Erlebnisereignisse sind Faktenaufzeichnungen dessen, was geschehen ist, und sind somit unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist.

[!DNL Intelligent Services] Verwenden Sie mehrere Schlüsselfelder in diesem Schema, um Einblicke aus Ihren Marketing-Ereignisdaten zu generieren, die sich alle auf der Stammebene befinden und erweitert werden können, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schemas ist auch die CEE-Schemafeldgruppe erweiterbar. Mit anderen Worten, der CEE-Feldergruppe können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehrere Schemas aufgenommen werden.

Ein vollständiges Beispiel für die Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Außerdem können Sie die folgende [JSON-Datei](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) anzeigen und kopieren, um ein Beispiel dafür zu erhalten, wie Daten entsprechend dem CEE-Schema strukturiert sein können. Sehen Sie sich diese beiden Beispiele an, wenn Sie mehr über die im folgenden Abschnitt beschriebenen Schlüsselfelder erfahren, um zu bestimmen, wie Sie Ihre eigenen Daten dem Schema zuordnen können.

## Schlüsselfelder

Es gibt mehrere Schlüsselfelder in der CEE-Feldergruppe, die verwendet werden sollten, damit [!DNL Intelligent Services] nützliche Einblicke generiert. In diesem Abschnitt werden der Anwendungsfall und die erwarteten Daten für diese Felder beschrieben und Links zur Referenzdokumentation für weitere Beispiele bereitgestellt.

### Obligatorische Felder

Es wird zwar dringend empfohlen, alle Schlüsselfelder zu verwenden, es gibt jedoch zwei Felder, die **erforderlich** sind, damit [!DNL Intelligent Services] funktioniert:

* [Ein primäres Identitätsfeld](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel)  (nur für Attribution AI erforderlich)

#### Primäre Identität {#identity}

Eines der Felder in Ihrem Schema muss als primäres Identitätsfeld festgelegt werden, das es [!DNL Intelligent Services] ermöglicht, jede Instanz von Zeitreihendaten mit einer einzelnen Person zu verknüpfen.

Sie müssen basierend auf der Quelle und der Art Ihrer Daten festlegen, welches Feld als primäre Identität verwendet werden soll. Ein Identitätsfeld muss einen **Identitäts-Namespace** enthalten, der den Typ der Identitätsdaten angibt, die das Feld als Wert erwartet. Zu den gültigen Namespace-Werten gehören:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(für Adobe Audience Manager IDs)
* &quot;aaid&quot;(für Adobe Analytics IDs)

Wenn Sie sich nicht sicher sind, welches Feld Sie als primäre Identität verwenden sollten, wenden Sie sich an Adobe Consulting Services , um die beste Lösung zu ermitteln. Wenn keine primäre Identität festgelegt ist, verwendet die Anwendung &quot;Intelligent Service&quot;das folgende Standardverhalten:

| Standard | Attribution AI | Customer AI |
| --- | --- | --- |
| Identitätsspalte | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Um eine primäre Identität festzulegen, navigieren Sie auf der Registerkarte **[!UICONTROL Schemas]** zu Ihrem Schema und wählen Sie den Hyperlink für den Schemanamen aus, um **[!DNL Schema Editor]** zu öffnen.

![Navigieren zum Schema](./images/data-preparation/navigate_schema.png)

Navigieren Sie anschließend zu dem Feld, das Sie als primäre Identität festlegen möchten, und wählen Sie es aus. Das Menü **[!UICONTROL Feldeigenschaften]** wird für dieses Feld geöffnet.

![Feld auswählen](./images/data-preparation/find_field.png)

Scrollen Sie im Menü **[!UICONTROL Feldeigenschaften]** nach unten, bis Sie das Kontrollkästchen **[!UICONTROL Identität]** finden. Nachdem Sie das Kontrollkästchen aktiviert haben, wird die Option zum Festlegen der ausgewählten Identität als **[!UICONTROL Primäre Identität]** angezeigt. Wählen Sie auch dieses Feld aus.

![Kontrollkästchen aktivieren](./images/data-preparation/set_primary_identity.png)

Als Nächstes müssen Sie einen **[!UICONTROL Identitäts-Namespace]** aus der Liste der vordefinierten Namespaces im Dropdown-Menü angeben. In diesem Beispiel wird der ECID-Namespace ausgewählt, da eine Adobe Audience Manager ID `mcid.id` verwendet wird. Wählen Sie **[!UICONTROL Anwenden]** aus, um die Aktualisierungen zu bestätigen, und klicken Sie dann oben rechts auf **[!UICONTROL Speichern]** , um die Änderungen am Schema zu speichern.

![Speichern Sie die Änderungen](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Dieses Feld gibt den Zeitpunkt an, zu dem das Ereignis aufgetreten ist. Dieser Wert muss als Zeichenfolge gemäß ISO 8601 angegeben werden.

#### xdm:channel {#channel}

>[!NOTE]
>
>Dieses Feld ist nur bei Verwendung von Attribution AI erforderlich.

Dieses Feld stellt den mit dem ExperienceEvent verknüpften Marketingkanal dar. Das Feld enthält Informationen zum Kanaltyp, Medientyp und Standorttyp.

![](./images/data-preparation/channel.png)

**Beispielschema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:channel` finden Sie in der Spezifikation für [Erlebniskanalschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Einige Beispielzuordnungen finden Sie in der [Tabelle unter](#example-channels).

#### Beispiel für Kanalzuordnungen {#example-channels}

Die folgende Tabelle enthält einige Beispiele für Marketingkanäle, die dem Schema `xdm:channel` zugeordnet sind:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/channel-types/search | bezahlt | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | Earned | Klicks |
| Anzeigen | https:/<span>/ns.adobe.com/xdm/channel-types/display | bezahlt | Klicks |
| E-Mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | bezahlt | Klicks |
| Interner Referrer | https:/<span>/ns.adobe.com/xdm/channel-types/direct | Eigentümer | Klicks |
| Display ViewThrough | https:/<span>/ns.adobe.com/xdm/channel-types/display | bezahlt | impressions |
| QR-Code-Umleitung | https:/<span>/ns.adobe.com/xdm/channel-types/direct | Eigentümer | Klicks |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | Eigentümer | Klicks |

### Empfohlene Felder

Die übrigen Schlüsselfelder werden in diesem Abschnitt beschrieben. Diese Felder sind zwar nicht unbedingt erforderlich, damit [!DNL Intelligent Services] funktioniert, es wird jedoch dringend empfohlen, möglichst viele davon zu verwenden, um umfassendere Einblicke zu erhalten.

#### xdm:productListItems

Dieses Feld ist ein Array von Artikeln, die von einem Kunden ausgewählte Produkte darstellen, einschließlich Produkt-SKU, Name, Preis und Menge.

![](./images/data-preparation/productListItems.png)

**Beispielschema**

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie in der Spezifikation für [Commerce-Detailschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Dieses Feld enthält Commerce-spezifische Informationen zum ExperienceEvent, einschließlich Bestellnummer und Zahlungsinformationen.

![](./images/data-preparation/commerce.png)

**Beispielschema**

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:commerce` finden Sie in der Spezifikation für [Commerce-Detailschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Dieses Feld stellt Webdetails zum ExperienceEvent dar, z. B. die Interaktion, die Seitendetails und den Referrer.

![](./images/data-preparation/web.png)

**Beispielschema**

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

Ausführliche Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie in der Spezifikation [ExperienceEvent-Webdetailschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Dieses Feld enthält Informationen zu Marketingaktivitäten, die mit dem Touchpoint aktiv sind.

![](./images/data-preparation/marketing.png)

**Beispielschema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie in der Spezifikation [Marketing sechma](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Daten zuordnen und erfassen {#mapping}

Nachdem Sie ermittelt haben, ob Ihre Marketing-Ereignisdaten dem CEE-Schema zugeordnet werden können, müssen Sie im nächsten Schritt ermitteln, welche Daten in [!DNL Intelligent Services] integriert werden sollen. Alle historischen Daten, die in [!DNL Intelligent Services] verwendet werden, müssen innerhalb des Zeitfensters von mindestens vier Monaten mit Daten liegen, zuzüglich der Anzahl der Tage, die als Lookback-Zeitraum vorgesehen sind.

Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und in den Dienst zu integrieren, nachdem Sie den Datenbereich ausgewählt haben, den Sie senden möchten.

Wenn Sie über ein [!DNL Adobe Experience Platform]-Abonnement verfügen und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden von Adobe Experience Platform

>[!NOTE]
>
>Die folgenden Schritte erfordern ein Abonnement für Experience Platform. Wenn Sie keinen Zugriff auf Platform haben, fahren Sie mit dem Abschnitt [Nächste Schritte](#next-steps) fort.

In diesem Abschnitt wird der Workflow für die Zuordnung und Aufnahme von Daten in Experience Platform zur Verwendung in [!DNL Intelligent Services] beschrieben, einschließlich Links zu Tutorials für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und -Datensatzes

Wenn Sie bereit sind, Ihre Daten für die Aufnahme vorzubereiten, besteht der erste Schritt darin, ein neues XDM-Schema zu erstellen, das die CEE-Feldergruppe verwendet. In den folgenden Tutorials wird das Erstellen eines neuen Schemas in der Benutzeroberfläche oder API erläutert:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Die obigen Tutorials folgen einem allgemeinen Workflow zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie die CEE-Feldergruppe zum Schema hinzufügen.

Nachdem Sie die CEE-Feldergruppe zum Schema hinzugefügt haben, können Sie weitere Feldergruppen hinzufügen, die für zusätzliche Felder in Ihren Daten erforderlich sind.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie einen neuen Datensatz erstellen, der auf diesem Schema basiert. In den folgenden Tutorials wird der Prozess zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API erläutert:

* [Erstellen Sie einen Datensatz in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create)  (folgen Sie dem Workflow zur Verwendung eines vorhandenen Schemas).
* [Datensatz in der API erstellen](../catalog/datasets/create.md)

Nachdem der Datensatz erstellt wurde, können Sie ihn in der Platform-Benutzeroberfläche im Arbeitsbereich **[!UICONTROL Datensätze]** finden.

![](images/data-preparation/dataset-location.png)

#### Identitätsfelder zum Datensatz hinzufügen

Wenn Sie Daten von [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] oder einer anderen externen Quelle abrufen, haben Sie die Möglichkeit, ein Schemafeld als Identitätsfeld festzulegen. Um ein Schemafeld als Identitätsfeld festzulegen, sehen Sie sich den Abschnitt zum Festlegen von Identitätsfeldern im [UI-Tutorial](../xdm/tutorials/create-schema-ui.md#identity-field) oder [API-Tutorial](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) zum Erstellen eines Schemas an.

Wenn Sie Daten aus einer lokalen CSV-Datei erfassen, können Sie mit dem nächsten Abschnitt [Mapping und Erfassen von Daten](#ingest) fortfahren.

#### Daten zuordnen und erfassen {#ingest}

Nachdem Sie ein CEE-Schema und einen Datensatz erstellt haben, können Sie mit der Zuordnung Ihrer Datentabellen zum Schema beginnen und diese Daten in Platform erfassen. Anweisungen dazu, wie Sie dies in der Benutzeroberfläche durchführen, finden Sie im Tutorial zum [Zuordnen einer CSV-Datei zu einem XDM-Schema](../ingestion/tutorials/map-a-csv-file.md) . Sie können die folgende [JSON-Beispieldatei](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) verwenden, um den Aufnahmevorgang zu testen, bevor Sie Ihre eigenen Daten verwenden.

Nachdem ein Datensatz gefüllt wurde, kann derselbe Datensatz zur Aufnahme zusätzlicher Datendateien verwendet werden.

Wenn Ihre Daten in einer unterstützten Drittanbieteranwendung gespeichert sind, können Sie auch einen [Quell-Connector](../sources/home.md) erstellen, um Ihre Marketing-Ereignisdaten in Echtzeit in [!DNL Platform] aufzunehmen.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in [!DNL Intelligent Services]. Wenn Sie je nach Anwendungsfall zusätzliche Beratung benötigen, wenden Sie sich an den Support von Adobe Consulting.

Nachdem Sie einen Datensatz erfolgreich mit Ihren Kundenerlebnisdaten ausgefüllt haben, können Sie [!DNL Intelligent Services] verwenden, um Einblicke zu generieren. Erste Schritte finden Sie in den folgenden Dokumenten:

* [Attribution AI – Übersicht](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
