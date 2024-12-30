---
keywords: Experience Platform;Startseite;Intelligent Services;beliebte Themen;Intelligent Service;Intelligent Service
solution: Experience Platform
title: Vorbereiten von Daten für die Verwendung in Intelligent Services
description: Damit Intelligent Services Einblicke aus Ihren Marketing-Ereignisdaten gewinnen kann, müssen die Daten semantisch angereichert und in einer Standardstruktur verwaltet werden. Intelligent Services verwenden Experience-Datenmodell(XDM)-Schemata, um dies zu erreichen.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 87a8ad253abb219662034652b5f8c4fabfa40484
workflow-type: tm+mt
source-wordcount: '2823'
ht-degree: 2%

---

# Vorbereiten von Daten für die Verwendung in [!DNL Intelligent Services]

Damit [!DNL Intelligent Services] Einblicke aus Ihren Marketing-Ereignisdaten gewinnen können, müssen die Daten semantisch angereichert und in einer Standardstruktur verwaltet werden. [!DNL Intelligent Services] nutzen [!DNL Experience Data Model] (XDM)-Schemata, um dies zu erreichen. Insbesondere müssen alle Datensätze, die in [!DNL Intelligent Services] verwendet werden, dem Consumer ExperienceEvent (CEE)-XDM-Schema entsprechen oder den Adobe Analytics-Connector verwenden. Darüber hinaus unterstützt Kunden-KI den Adobe Audience Manager-Connector.

Dieses Dokument enthält allgemeine Anleitungen zum Zuordnen Ihrer Marketing-Ereignisdaten aus mehreren Kanälen zum CEE-Schema und enthält Informationen zu wichtigen Feldern innerhalb des Schemas, damit Sie ermitteln können, wie Sie Ihre Daten effektiv ihrer Struktur zuordnen können. Wenn Sie Adobe Analytics-Daten verwenden möchten, lesen Sie bitte den Abschnitt zur [Vorbereitung von Adobe Analytics-Daten](#analytics-data). Wenn Sie Adobe Audience Manager-Daten verwenden möchten (nur Kunden-KI), lesen Sie bitte den Abschnitt [Adobe Audience Manger-Datenvorbereitung](#AAM-data).

## Datenanforderungen

[!DNL Intelligent Services] benötigen je nach erstelltem Ziel unterschiedliche Mengen historischer Daten. Unabhängig davon müssen die Daten, die Sie für **alle**-[!DNL Intelligent Services] vorbereiten, sowohl positive als auch negative Journey/Ereignisse enthalten. Sowohl negative als auch positive Ereignisse verbessern die Modellgenauigkeit und -genauigkeit.

Wenn Sie beispielsweise Kunden-KI verwenden, um die Kauftendenz eines Produkts vorherzusagen, benötigt das Modell für Kunden-KI sowohl Beispiele für erfolgreiche Kaufpfade als auch Beispiele für nicht erfolgreiche Pfade. Dies liegt daran, dass Kunden-KI bei der Modellschulung untersucht, welche Ereignisse und Journey zu einem Kauf führen. Dies umfasst auch die Aktionen, die von Kunden durchgeführt wurden, die nicht gekauft haben, z. B. eine Person, die ihren Journey gestoppt hat, als sie einen Artikel zum Warenkorb hinzufügte. Diese Kunden weisen möglicherweise ähnliche Verhaltensweisen auf. Kunden-KI kann jedoch Einblicke bieten und die wichtigsten Unterschiede und Faktoren aufschlüsseln, die zu einem höheren Neigungs-Score führen. In ähnlicher Weise erfordert Attribution AI sowohl Ereignistypen als auch Journey, um Metriken wie Touchpoint-Effektivität, Top-Konversionspfade und Aufschlüsselungen nach Touchpoint-Position anzuzeigen.

Weitere Beispiele und Informationen zu historischen Datenanforderungen finden Sie im Abschnitt [Kunden-KI](./customer-ai/data-requirements.md#data-requirements) oder [Attribution AI ](./attribution-ai/input-output.md#data-requirements) Historische Datenanforderungen in der Eingabe-/Ausgabedokumentation.

### Richtlinien für das Zusammenfügen von Daten

Es wird empfohlen, die Ereignisse einer Benutzerin oder eines Benutzers nach Möglichkeit über eine gemeinsame ID hinweg zuzuordnen. Beispielsweise können Benutzerdaten mit „id1“ über 10 Ereignisse verteilt sein. Später hat derselbe Benutzer die Cookie-ID gelöscht und wird für die nächsten 20 Ereignisse als „id2“ aufgezeichnet. Wenn Sie wissen, dass ID1 und ID2 demselben Benutzer bzw. derselben Benutzerin entsprechen, empfiehlt es sich, alle 30 Ereignisse mit einer gemeinsamen ID zusammenzufügen.

Wenn dies nicht möglich ist, sollten Sie beim Erstellen Ihrer Modelleingabedaten jeden Satz von Ereignissen als einen anderen Benutzer behandeln. Dadurch werden die besten Ergebnisse beim Modell-Training und Scoring sichergestellt.

## Workflow-Zusammenfassung

Der Vorbereitungsprozess hängt davon ab, ob Ihre Daten in Adobe Experience Platform oder extern gespeichert werden. In diesem Abschnitt werden die erforderlichen Schritte zusammengefasst, die Sie bei beiden Szenarien ausführen müssen.

### Vorbereitung externer Daten

Wenn Ihre Daten außerhalb von Experience Platform gespeichert werden, müssen Sie Ihre Daten den erforderlichen und relevanten Feldern in einem „Consumer ExperienceEvent[Schema ](#cee-schema). Dieses Schema kann mit benutzerdefinierten Feldergruppen erweitert werden, um Ihre Kundendaten besser zu erfassen. Nach der Zuordnung können Sie einen Datensatz mit Ihrem Consumer ExperienceEvent-Schema erstellen und [Ihre Daten in Platform aufnehmen](../ingestion/home.md). Der CEE-Datensatz kann dann beim Konfigurieren eines [!DNL Intelligent Service] ausgewählt werden.

Je nach gewünschter [!DNL Intelligent Service] können verschiedene Felder erforderlich sein. Beachten Sie, dass es sich als Best Practice empfiehlt, einem Feld Daten hinzuzufügen, wenn die Daten verfügbar sind. Weitere Informationen zu den erforderlichen Feldern finden Sie im Handbuch zu den Datenanforderungen für {](./attribution-ai/input-output.md)}Attribution AI [ oder ](./customer-ai/data-requirements.md)Kunden-KI).[

### Datenvorbereitung in Adobe Analytics {#analytics-data}

Kunden-KI und Attribution AI unterstützen nativ Adobe Analytics-Daten. Um Adobe Analytics-Daten zu verwenden, führen Sie die in der Dokumentation beschriebenen Schritte aus, um einen [Analytics-Quell-Connector) ](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Sobald der Quell-Connector Ihre Daten in Experience Platform streamt, können Sie Adobe Analytics als Datenquelle und anschließend während der Konfiguration Ihrer Instanz einen Datensatz auswählen. Alle erforderlichen Schemafeldgruppen und einzelnen Felder werden bei der Einrichtung der Verbindung automatisch erstellt. Sie müssen die Datensätze nicht im CEE-Format abfragen (Extract, Transform, Load).

Wenn Sie die Daten, die über den Adobe Analytics-Quell-Connector nach Adobe Experience Platform übertragen werden, mit den Adobe Analytics-Daten vergleichen, können Sie einige Diskrepanzen feststellen. Der Analytics Source-Connector kann beim Konvertieren in ein Experience-Datenmodell (XDM)-Schema Zeilen ignorieren. Es kann mehrere Gründe dafür geben, dass die gesamte Zeile nicht für die Umwandlung geeignet ist, darunter fehlende Zeitstempel, fehlende Personen-IDs, ungültige oder große Personen-IDs, ungültige Analysewerte und mehr.

Weitere Informationen und Beispiele finden Sie in der Dokumentation zu [Vergleichen von Adobe Analytics- und Customer Journey Analytics-Daten](https://www.adobe.com/go/compare-aa-data-to-cja-data). Dieser Artikel soll Ihnen dabei helfen, diese Unterschiede zu diagnostizieren und zu beheben, damit Sie und Ihr Team Adobe Experience Platform-Daten für Intelligent Services ohne Beeinträchtigung der Datenintegrität verwenden können.

Führen Sie in Adobe Experience Platform Query Services die folgende Abfrage zur Gesamtzahl der Datensätze zwischen Start- und Endzeitstempel nach channel.typeAtSource aus, um die Anzahl nach Marketing-Kanälen zu finden.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Die Aufstockung von Daten durch den Adobe Analytics-Connector dauert bis zu vier Wochen. Wenn Sie kürzlich eine Verbindung eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Kunden oder Attribution AI erforderliche Mindestlänge von Daten aufweist. Lesen Sie die Abschnitte zu historischen Daten in [Kunden-KI](./customer-ai/data-requirements.md#data-requirements) oder [Attribution AI ](./attribution-ai/input-output.md#data-requirements) und stellen Sie sicher, dass Sie über genügend Daten für Ihr Prognoseziel verfügen.

### Datenvorbereitung in Adobe Audience Manager (nur Kunden-KI) {#AAM-data}

Kunden-KI unterstützt nativ Adobe Audience Manager-Daten. Um Audience Manager-Daten zu verwenden, führen Sie die in der Dokumentation beschriebenen Schritte aus, um einen [Audience Manager-Quell-Connector einzurichten](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Nachdem der Quell-Connector Ihre Daten in Experience Platform gestreamt hat, können Sie Adobe Audience Manager als Datenquelle und anschließend während Ihrer Kunden-KI-Konfiguration einen Datensatz auswählen. Alle Schemafeldgruppen und einzelnen Felder werden bei der Einrichtung der Verbindung automatisch erstellt. Sie müssen die Datensätze nicht im CEE-Format abfragen (Extract, Transform, Load).

>[!IMPORTANT]
>
>Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die erforderliche Mindestlänge von Daten aufweist. Lesen Sie den Abschnitt zu historischen Daten in der [Eingabe-/Ausgabedokumentation](./customer-ai/data-requirements.md) für Kunden-KI und stellen Sie sicher, dass Sie über genügend Daten für Ihr Prognoseziel verfügen.

### [!DNL Experience Platform]

Wenn Ihre Daten bereits in [!DNL Platform] gespeichert sind und nicht über Adobe Analytics oder Adobe Audience Manager (nur Kunden-KI) gestreamt werden, führen Sie die folgenden Schritte aus. Es wird dennoch empfohlen, das CEE-Schema zu verstehen.

1. Überprüfen Sie die Struktur des Schemas [Consumer ExperienceEvent](#cee-schema) und stellen Sie fest, ob Ihre Daten dessen Feldern zugeordnet werden können.
2. Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und in [!DNL Intelligent Services] aufzunehmen, oder [führen Sie die Schritte in diesem Handbuch aus](#mapping) wenn Sie die Daten selbst zuordnen möchten.

## Grundlegendes zum CEE-Schema {#cee-schema}

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Kontakts im Zusammenhang mit digitalen Marketing-Ereignissen (Web oder Mobile) sowie mit Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist für [!DNL Intelligent Services] aufgrund seiner semantisch klar definierten Felder (Spalten) erforderlich, wobei unbekannte Namen vermieden werden, die die Daten ansonsten weniger klar machen würden.

Wie alle XDM ExperienceEvent-Schemata erfasst auch das CEE-Schema den zeitreihenbasierten Status des Systems, wenn ein Ereignis (oder eine Reihe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Erlebnisereignisse sind Tatsachenaufzeichnungen über das Geschehene und daher unveränderlich und stellen dar, was ohne Aggregation oder Interpretation passiert ist.

[!DNL Intelligent Services] verwenden mehrere Schlüsselfelder in diesem Schema, um Einblicke aus Ihren Marketing-Ereignisdaten zu generieren, die alle auf der Stammebene gefunden und erweitert werden können, um die erforderlichen Unterfelder anzuzeigen.

![](./images/data-preparation/schema-expansion.gif)

Wie alle XDM-Schemata ist die Schemafeldgruppe CEE erweiterbar. Mit anderen Worten können der CEE-Feldergruppe zusätzliche Felder hinzugefügt werden und verschiedene Varianten können bei Bedarf in mehrere Schemata aufgenommen werden.

Ein vollständiges Beispiel für die Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Darüber hinaus können Sie die folgende (JSON[Datei) anzeigen und kopieren](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) um ein Beispiel dafür zu erhalten, wie Daten entsprechend dem CEE-Schema strukturiert werden können. Siehe beide Beispiele, während Sie mehr über die im folgenden Abschnitt beschriebenen Schlüsselfelder erfahren, um zu bestimmen, wie Sie Ihre eigenen Daten dem Schema zuordnen können.

## Schlüsselfelder

Es gibt mehrere Schlüsselfelder innerhalb der CEE-Feldergruppe, die verwendet werden sollten, damit [!DNL Intelligent Services] nützliche Einblicke gewinnen können. In diesem Abschnitt werden der Anwendungsfall und die erwarteten Daten für diese Felder beschrieben. Außerdem finden Sie Links zur Referenzdokumentation für weitere Beispiele.

### Pflichtfelder

Die Verwendung aller Schlüsselfelder wird zwar dringend empfohlen, es gibt jedoch zwei Felder, die **erforderlich** sind, damit [!DNL Intelligent Services] funktioniert:

* [Ein primäres Identitätsfeld](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (nur für Attribution AI erforderlich)

#### Primäre Identität {#identity}

Eines der Felder in Ihrem Schema muss als primäres Identitätsfeld festgelegt werden, mit dem [!DNL Intelligent Services] jede Instanz von Zeitreihendaten mit einer einzelnen Person verknüpfen können.

Sie müssen basierend auf der Quelle und der Art Ihrer Daten das Feld ermitteln, das am besten als primäre Identität verwendet werden kann. Ein Identitätsfeld muss einen **Identity-Namespace** enthalten, der den Typ der Identitätsdaten angibt, den das Feld als Wert erwartet. Zu den gültigen Namespace-Werten gehören:

>[!NOTE]
>
>Die Experience Cloud-ID (ECID) wird auch als MCID bezeichnet und weiterhin in Namespaces verwendet.

* „E-Mail“
* „Telefon“
* „mcid“ (für Adobe Audience Manager IDs)
* „aaid“ (für Adobe Analytics IDs)

Wenn Sie sich nicht sicher sind, welches Feld Sie als primäre Identität verwenden sollten, wenden Sie sich an Adobe Consulting Services, um die beste Lösung zu ermitteln. Wenn keine primäre Identität festgelegt ist, verwendet die Intelligent Service-Anwendung das folgende Standardverhalten:

| Standard | Attributions-KI | Kunden-KI |
| --- | --- | --- |
| Identitätsspalte | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Um eine primäre Identität festzulegen, navigieren Sie von der Registerkarte **[!UICONTROL Schemata]** zu Ihrem Schema und wählen Sie den Hyperlink für den Schemanamen aus, um das **[!DNL Schema Editor]** zu öffnen.

![Zu Schema navigieren](./images/data-preparation/navigate_schema.png)

Navigieren Sie dann zu dem Feld, das Sie als primäre Identität verwenden möchten, und wählen Sie es aus. Das **[!UICONTROL Feldeigenschaften]** Menü wird für dieses Feld geöffnet.

![Feld auswählen](./images/data-preparation/find_field.png)

Scrollen Sie im Menü **[!UICONTROL Feldeigenschaften]** nach unten, bis Sie das Kontrollkästchen **[!UICONTROL Identität]** finden. Nach dem Aktivieren des Kontrollkästchens wird die Option zum Festlegen der ausgewählten Identität als **[!UICONTROL Primäre Identität]** angezeigt. Aktivieren Sie dieses Kontrollkästchen ebenfalls.

![Kontrollkästchen aktivieren](./images/data-preparation/set_primary_identity.png)

Als Nächstes müssen Sie einen **[!UICONTROL Identity-Namespace]** aus der Liste der vordefinierten Namespaces im Dropdown-Menü angeben. In diesem Beispiel wird der ECID-Namespace ausgewählt, da ein Adobe Audience Manager-ID-`mcid.id` verwendet wird. Wählen Sie **[!UICONTROL Anwenden]** aus, um die Aktualisierungen zu bestätigen, und wählen Sie dann **[!UICONTROL Speichern]** in der oberen rechten Ecke, um die Änderungen an Ihrem Schema zu speichern.

![Speichern Sie die Änderungen](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Dieses Feld stellt den Zeitpunkt dar, zu dem das Ereignis aufgetreten ist. Dieser Wert muss gemäß ISO 8601 als Zeichenfolge angegeben werden.

#### xdm:channel {#channel}

>[!NOTE]
>
>Dieses Feld ist nur bei Verwendung von Attribution AI erforderlich.

Dieses Feld stellt den Marketing-Kanal für das ExperienceEvent dar. Das Feld enthält Informationen zum Kanaltyp, Medientyp und Standorttyp.

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:channel` finden Sie in der Spezifikation [Experience-Kanal](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) . Einige Beispielzuordnungen finden Sie in der [Tabelle unten](#example-channels).

#### Beispiel für Kanalzuordnungen {#example-channels}

Die folgende Tabelle enthält einige Beispiele für Marketing-Kanäle, die dem `xdm:channel`-Schema zugeordnet sind:

| Kanal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Paid Search | https:/<span>/ns.adobe.com/xdm/channel-types/search | bezahlt | Klicks |
| Sozial - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | verdient | Klicks |
| Anzeige | https:/<span>/ns.adobe.com/xdm/channel-types/display | bezahlt | Klicks |
| E-Mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | bezahlt | Klicks |
| Interne Referenz | https:/<span>/ns.adobe.com/xdm/channel-types/direct | in Besitz | Klicks |
| Ansicht anzeigen durch | https:/<span>/ns.adobe.com/xdm/channel-types/display | bezahlt | Impressionen |
| QR-Code-Umleitung | https:/<span>/ns.adobe.com/xdm/channel-types/direct | in Besitz | Klicks |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | in Besitz | Klicks |

### Empfohlene Felder

Die übrigen Schlüsselfelder sind in diesem Abschnitt beschrieben. Diese Felder sind zwar nicht unbedingt erforderlich, damit [!DNL Intelligent Services] funktionieren, es wird jedoch dringend empfohlen, so viele wie möglich davon zu verwenden, um umfassendere Einblicke zu erhalten.

#### xdm:productListItems

Dieses Feld ist ein Array von Elementen, die von einem Kunden ausgewählte Produkte darstellen, einschließlich der Produkt-SKU, des Namens, des Preises und der Menge.

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für die `xdm:productListItems` finden Sie in der Spezifikation [Commerce-Details](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) .

#### xdm:commerce

Dieses Feld enthält Commerce-spezifische Informationen zum ExperienceEvent, einschließlich der Bestellnummer und Zahlungsinformationen.

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für die `xdm:commerce` finden Sie in der Spezifikation [Commerce-Details](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) .

#### xdm:web

Dieses Feld stellt Web-Details dar, die sich auf das ExperienceEvent beziehen, z. B. die Interaktion, Seitendetails und den Referrer.

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

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für die `xdm:productListItems` finden Sie in der Spezifikation [ExperienceEvent-Web-Details](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) .

#### xdm:marketing

Dieses Feld enthält Informationen zu Marketing-Aktivitäten, die mit dem Touchpoint aktiv sind.

![](./images/data-preparation/marketing.png)

**Beispielschema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Vollständige Informationen zu den einzelnen erforderlichen Unterfeldern für `xdm:productListItems` finden Sie in der Spezifikation [Marketing-](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md)).

## Zuordnen und Aufnehmen von Daten {#mapping}

Nachdem Sie ermittelt haben, ob Ihre Marketing-Ereignisdaten dem CEE-Schema zugeordnet werden können, besteht der nächste Schritt darin, zu bestimmen, welche Daten Sie in [!DNL Intelligent Services] importieren müssen. Alle in [!DNL Intelligent Services] verwendeten historischen Daten müssen innerhalb des Mindestzeitfensters von vier Monaten liegen, plus der Anzahl der Tage, die als Lookback-Zeitraum vorgesehen sind.

Nachdem Sie den Datenbereich bestimmt haben, den Sie senden möchten, wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und in den Service aufzunehmen.

Wenn Sie über ein [!DNL Adobe Experience Platform]-Abonnement verfügen und die Daten selbst zuordnen und aufnehmen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden von Adobe Experience Platform

>[!NOTE]
>
>Für die folgenden Schritte ist ein Abonnement von Experience Platform erforderlich. Wenn Sie keinen Zugriff auf Platform haben, fahren Sie mit dem Abschnitt [nächsten Schritte](#next-steps) fort.

In diesem Abschnitt wird der Workflow für die Zuordnung und Aufnahme von Daten in Experience Platform zur Verwendung in [!DNL Intelligent Services] beschrieben, einschließlich Links zu Tutorials mit detaillierten Schritten.

#### Erstellen eines CEE-Schemas und -Datensatzes

Wenn Sie bereit sind, Ihre Daten für die Aufnahme vorzubereiten, besteht der erste Schritt darin, ein neues XDM-Schema zu erstellen, das die CEE-Feldergruppe verwendet. In den folgenden Tutorials wird erläutert, wie Sie ein neues Schema in der Benutzeroberfläche oder API erstellen:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Die obigen Tutorials folgen einem allgemeinen Workflow zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie die CEE-Feldergruppe zum Schema hinzufügen.

Nachdem Sie die CEE-Feldergruppe zum Schema hinzugefügt haben, können Sie bei Bedarf weitere Feldergruppen für zusätzliche Felder in Ihren Daten hinzufügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie einen neuen Datensatz basierend auf diesem Schema erstellen. In den folgenden Tutorials wird erläutert, wie Sie einen neuen Datensatz in der Benutzeroberfläche oder API erstellen:

* [Erstellen eines Datensatzes in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create) (befolgen Sie den Workflow zur Verwendung eines vorhandenen Schemas)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

Nachdem der Datensatz erstellt wurde, können Sie ihn in der Platform-Benutzeroberfläche im Arbeitsbereich **[!UICONTROL Datensätze]** finden.

![](images/data-preparation/dataset-location.png)

#### Hinzufügen von Identitätsfeldern zum Datensatz

Wenn Sie Daten aus [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] oder einer anderen externen Quelle importieren, haben Sie die Möglichkeit, ein Schemafeld als Identitätsfeld festzulegen. Um ein Schemafeld als Identitätsfeld festzulegen, lesen Sie den Abschnitt zum Festlegen von Identitätsfeldern im [UI-Tutorial](../xdm/tutorials/create-schema-ui.md#identity-field) oder [API-Tutorial](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) zum Erstellen eines Schemas.

Wenn Sie Daten aus einer lokalen CSV-Datei erfassen, können Sie mit dem nächsten Abschnitt zum Thema [Zuordnen und Aufnehmen von Daten“ ](#ingest).

#### Zuordnen und Aufnehmen von Daten {#ingest}

Nachdem Sie ein CEE-Schema und einen Datensatz erstellt haben, können Sie mit der Zuordnung Ihrer Datentabellen zum Schema beginnen und diese Daten in Platform aufnehmen. Anweisungen dazu, wie Sie [ der Benutzeroberfläche durchführen, finden Sie im Tutorial ](../ingestion/tutorials/map-csv/overview.md) Zuordnen einer CSV-Datei zu einem XDM-Schema . Sie können die folgende [JSON-Beispieldatei) verwenden](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) um den Aufnahmeprozess zu testen, bevor Sie Ihre eigenen Daten verwenden.

Sobald ein Datensatz ausgefüllt wurde, kann derselbe Datensatz zum Aufnehmen zusätzlicher Datendateien verwendet werden.

Wenn Ihre Daten in einem unterstützten Drittanbieterprogramm gespeichert sind, können Sie auch einen [Quell-Connector](../sources/home.md) erstellen, um Ihre Marketing-Ereignisdaten in Echtzeit in [!DNL Platform] aufzunehmen.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in [!DNL Intelligent Services]. Wenn Sie zusätzliche Beratung basierend auf Ihrem Anwendungsfall benötigen, wenden Sie sich bitte an den Adobe Consulting-Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten erfolgreich ausgefüllt haben, können Sie [!DNL Intelligent Services] verwenden, um Einblicke zu generieren. Informationen zu den ersten Schritten finden Sie in den folgenden Dokumenten:

* [Attribution AI – Übersicht](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
