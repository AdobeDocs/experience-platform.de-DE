---
title: Datenvorbereitung für die Datenerfassung
description: Erfahren Sie, wie Sie beim Konfigurieren eines Datenstroms für die Adobe Experience Platform Web- und Mobile-SDKs Ihre Daten einem XDM-Ereignisschema (Experience-Datenmodell) zuordnen können.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 53%

---

# Datenvorbereitung für die Datenerfassung

Datenvorbereitung ist ein Adobe Experience Platform-Service, mit dem Sie Daten zuordnen, umwandeln und validieren können, die an das [Experience-Datenmodell (XDM)](../xdm/home.md) gesendet oder von ihm empfangen werden. Beim Konfigurieren eines Experience Platform-aktivierten [Datenstroms](./overview.md) können Sie Datenvorbereitungsfunktionen verwenden, um Ihre Quelldaten dem XDM zuzuordnen, wenn Sie sie an die Experience Platform Edge Network senden.

Alle von einer Web-Seite gesendeten Daten müssen als XDM in Experience Platform landen. Es gibt 3 Möglichkeiten, Daten von einer On-Page-Datenschicht in das von Experience Platform akzeptierte XDM zu übersetzen:

1. Formatieren Sie die Datenschicht auf der Webseite selbst in XDM neu.
2. Verwenden Sie die Funktion Native Datenelemente von Tags , um das vorhandene Datenschichtformat einer Web-Seite in XDM umzuformatieren.
3. Formatieren Sie das vorhandene Datenschichtformat einer Web-Seite über die Edge Network in XDM um, indem Sie die Datenvorbereitung für die Datenerfassung verwenden.

Dieses Handbuch konzentriert sich auf die dritte Option.

## Verwendung der Datenvorbereitung für die Datenerfassung {#when-to-use-data-prep}

Es gibt zwei Anwendungsfälle, in denen die Datenvorbereitung für die Datenerfassung nützlich ist:

1. Die Website verfügt über eine gut geformte, verwaltete und gepflegte Datenschicht und es wird empfohlen, sie direkt an die Edge Network zu senden, anstatt die JavaScript-Manipulation zu verwenden, um sie auf der Seite in XDM zu konvertieren (entweder über Tags-Datenelemente oder über die manuelle JavaScript-Manipulation).
2. Ein anderes Tagging-System als Tags wird auf der Site bereitgestellt.

## Senden einer vorhandenen Datenschicht an die Edge Network über WebSDK {#send-datalayer-via-websdk}

Die vorhandene Datenschicht muss mithilfe des [`data`](/help/web-sdk/commands/sendevent/data.md)-Objekts innerhalb des `sendEvent`-Befehls gesendet werden.

Wenn Sie Tags verwenden, müssen Sie das Feld **[!UICONTROL Daten]** des Aktionstyps **[!UICONTROL Ereignis senden]** verwenden, wie in der Dokumentation [Web SDK-Tag-Erweiterung](/help/tags/extensions/client/web-sdk/action-types.md) beschrieben.

Der Rest dieses Handbuchs konzentriert sich auf die Zuordnung der Datenschicht zu XDM-Standards, nachdem sie vom WebSDK gesendet wurde.

>[!NOTE]
>
>Eine umfassende Anleitung zu allen Datenvorbereitungs-Funktionen, einschließlich der Umwandlungsfunktionen für berechnete Felder, finden Sie in der folgenden Dokumentation:
>
>* [Datenvorbereitung – Übersicht](../data-prep/home.md)
>* [Funktionen zur Datenvorbereitung](../data-prep/functions.md)
>* [Verarbeiten von Datenformaten mit der Datenvorbereitung](../data-prep/data-handling.md)

In diesem Handbuch wird beschrieben, wie Sie Ihre Daten innerhalb der Benutzeroberfläche zuordnen können. Führen Sie zunächst den Prozess zur Erstellung eines Datenstroms bis (einschließlich) der [allgemeinen Konfiguration](./overview.md#create) aus.

Eine kurze Erklärung des Prozesses „Datenvorbereitung für die Datenerfassung“ finden Sie im folgenden Video:

>[!VIDEO](https://video.tv.adobe.com/v/3410301?quality=12&enable10seconds=on&speedcontrol=on&captions=ger)

## [!UICONTROL Auswählen von Daten] {#select-data}

Wählen Sie nach der allgemeinen Konfiguration eines Datenstroms die Option **[!UICONTROL Speichern und Zuordnung hinzufügen]** aus. Daraufhin wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt. Von hier aus müssen Sie ein JSON-Beispielobjekt bereitstellen, das die Struktur der Daten darstellt, die Sie an Experience Platform senden möchten.

Um Eigenschaften direkt aus Ihrer Datenschicht zu erfassen, muss das JSON-Objekt über eine einzige Stammeigenschaft verfügen: `data`. Die Untereigenschaften des `data`-Objekts sollten dann so konstruiert werden, dass es den Datenschicht-Eigenschaften zugeordnet werden kann, die Sie erfassen möchten. Wählen Sie den folgenden Abschnitt aus, um ein Beispiel für ein ordnungsgemäß formatiertes JSON-Objekt mit einem `data`-Stamm zu sehen.

+++JSON-Beispieldatei mit `data`-Stamm

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Bei der Erfassung von Eigenschaften aus einem XDM-Objekt-Datenelement gelten dieselben Regeln für das JSON-Objekt, doch die Stammeigenschaft muss stattdessen als `xdm` eingegeben werden. Wählen Sie den folgenden Abschnitt aus, um ein Beispiel für ein ordnungsgemäß formatiertes JSON-Objekt mit einem `xdm`-Stamm zu sehen.

+++JSON-Beispieldatei mit `xdm`-Stamm

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

Sie können die Option zum Hochladen des Objekts als Datei auswählen oder stattdessen das Raw-Objekt in das bereitgestellte Textfeld einfügen. Wenn die JSON gültig ist, wird im rechten Bereich ein Vorschauschema angezeigt. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![JSON-Beispiel für erwartete eingehende Daten.](assets/data-prep/select-data.png)

>[!NOTE]
>
> Verwenden Sie ein JSON-Beispielobjekt, das jedes Datenschichtelement darstellt, das auf einer beliebigen Seite verwendet werden kann. Beispielsweise verwenden nicht alle Seiten Datenschichtelemente des Warenkorbs. Die Datenschichtelemente des Warenkorbs sollten jedoch in diesem JSON-Beispielobjekt enthalten sein.

## [!UICONTROL Zuordnung]

Der **[!UICONTROL Zuordnungsschritt]** wird angezeigt, sodass Sie die Felder in Ihren Quelldaten dem Zielereignisschema in Experience Platform zuordnen können. Sie haben die Möglichkeit, die Zuordnung auf zwei Arten zu konfigurieren:

* [Erstellen Sie ](#create-mapping) für diesen Datenstrom durch einen manuellen Prozess.
* [Importieren Sie Zuordnungsregeln](#import-mapping) aus einem vorhandenen Datenstrom.

>[!IMPORTANT]
>
>Die Datenvorbereitung überschreibt `identityMap` XDM-Payloads, was sich weiter auf den Profilabgleich mit Real-Time CDP-Zielgruppen auswirken kann.

### Erstellen von Zuordnungsregeln {#create-mapping}

Um eine Zuordnungsregel zu erstellen, wählen Sie **[!UICONTROL Neue Zuordnung hinzufügen]** aus.

![Neue Zuordnung hinzufügen.](assets/data-prep/add-new-mapping.png)

Wählen Sie das Quellensymbol (![Quellensymbol](/help/images/icons/source.png)) und danach im sich öffnenden Dialogfeld das Quellfeld aus, das Sie auf der bereitgestellten Arbeitsfläche zuordnen möchten. Nachdem Sie ein Feld ausgewählt haben, verwenden Sie die Schaltfläche **[!UICONTROL Auswählen]**, um fortzufahren.

![Auswahl des Felds, das im Quellschema zugeordnet werden soll.](assets/data-prep/source-mapping.png)

Wählen Sie anschließend das Schemasymbol (![Schemasymbol](/help/images/icons/schema.png)) aus, um ein ähnliches Dialogfeld für das Zielereignisschema zu öffnen. Wählen Sie das Feld aus, dem Sie die Daten zuordnen möchten, und bestätigen Sie dann mit **[!UICONTROL Auswählen]**.

![Auswählen des Felds, das im Zielschema zugeordnet werden soll.](assets/data-prep/target-mapping.png)

Die Zuordnungsseite wird erneut mit der abgeschlossenen Feld-Zuordnung angezeigt. Der Abschnitt **[!UICONTROL Zuordnungsfortschritt]** wird aktualisiert und zeigt die Gesamtzahl der Felder an, die bereits erfolgreich zugeordnet wurden.

![Feld, das erfolgreich zugeordnet wurde und dessen Fortschritt widergespiegelt wird.](assets/data-prep/field-mapped.png)

>[!TIP]
>
>Wenn Sie ein Array von Objekten (im Quellfeld) einem Array von anderen Objekten (im Zielfeld) zuordnen möchten, fügen Sie wie unten dargestellt in den Pfaden der Quell- und Zielfelder nach dem Array-Namen `[*]` ein.
>
>![Array-Objektzuordnung.](assets/data-prep/array-object-mapping.png)

### Importieren vorhandener Zuordnungsregeln {#import-mapping}

Wenn Sie zuvor einen Datenstrom erstellt haben, können Sie seine konfigurierten Zuordnungsregeln für einen neuen Datenstrom wiederverwenden.

>[!WARNING]
>
>Durch das Importieren von Zuordnungsregeln aus einem anderen Datenstrom werden alle Feldzuordnungen überschrieben, die Sie möglicherweise vor dem Import hinzugefügt haben.

Wählen Sie zunächst **[!UICONTROL Zuordnung importieren]** aus.

![Auswahl der Schaltfläche Zuordnung importieren.](assets/data-prep/import-mapping-button.png)

Wählen Sie im sich öffnenden Dialogfeld den Datenstrom aus, dessen Zuordnungsregeln Sie importieren möchten. Wählen Sie danach **[!UICONTROL Vorschau]** aus.

![Auswählen eines vorhandenen Datenstroms.](assets/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Datenströme können nur innerhalb derselben [Sandbox](../sandboxes/home.md) importiert werden. Mit anderen Worten: Sie können den Datenstrom von einer Sandbox nicht in eine andere importieren.

Im nächsten Bildschirm wird eine Vorschau der gespeicherten Zuordnungsregeln für den ausgewählten Datenstrom gezeigt. Prüfen Sie, ob die angezeigten Zuordnungen korrekt sind und wählen Sie dann **[!UICONTROL Importieren]** aus, um die Zuordnungen zu bestätigen und zum neuen Datenstrom hinzuzufügen.

![Zuordnungsregeln zum Importieren.](assets/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Wenn Quellfelder in den importierten Zuordnungsregeln nicht in den von Ihnen [zuvor bereitgestellten](#select-data) JSON-Beispieldaten enthalten sind, werden diese Feldzuordnungen nicht in den Import einbezogen.

### Abschließen der Zuordnung

Führen Sie die oben genannten Schritte erneut aus, um den Rest der Felder dem Zielschema zuzuordnen. Sie müssen zwar nicht alle verfügbaren Quellfelder zuordnen, jedoch müssen alle Felder im Zielschema, die als erforderlich festgelegt sind, zugeordnet werden, um diesen Schritt abzuschließen. Der Zähler **[!UICONTROL Erforderliche Felder]** gibt an, wie viele erforderlichen Felder in der aktuellen Konfiguration noch nicht zugeordnet sind.

Nachdem die erforderliche Feldanzahl null erreicht hat und Sie Ihre Zuordnung überprüft haben, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen abzuschließen.

![Zuordnungen abgeschlossen](assets/data-prep/mapping-complete.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Ihre Daten XDM zuordnen, wenn Sie einen Datenstrom in der Benutzeroberfläche einrichten. Wenn Sie dem Tutorial zu allgemeinen Datenströmen gefolgt sind, können Sie jetzt zur Anleitung zum [Anzeigen von Datenspeicherdetails](./overview.md) zurückkehren
