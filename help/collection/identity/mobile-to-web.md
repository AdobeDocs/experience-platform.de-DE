---
title: Freigabe von Identitäten aus Mobile Apps für mobile Web-/Web-Ansichten
description: Identität von einer Mobile App in mobilen Webinhalt oder eine WebView zu übergeben, damit Reporting und Personalisierung im Webkontext fortgesetzt werden können.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Freigabe von Identitäten aus Mobile Apps für mobile Web-/Web-Ansichten

Wenn ein Besucher von einer mobilen App in eine WebView- oder mobile Web-Seite wechselt, behalten die App und die Web-Kontexte jeweils ihre eigene Identität bei. Ohne eine explizite Übergabe wird der Besucher im Web-Erlebnis als neue, unbekannte Person behandelt, wodurch das Reporting fragmentiert und die Personalisierung neu gestartet wird.

Die Freigabe von Mobile-zu-Web-Identitäten löst dies, indem die [Experience Cloud ID (ECID) des Besuchers ](./overview.md) einem `adobe_mc` Abfragezeichenfolgenparameter von der Mobile App an das Web-Ziel übergeben wird. Der Parameter enthält die ECID, Ihre Experience Cloud-Organisations-ID und einen Zeitstempel. Wenn das Web-Ziel mit einem gültigen `adobe_mc` geladen wird, liest die Web-SDK dies automatisch und wendet die weitergegebene Identität auf ihre erste Edge Network-Anfrage an, sodass beide Kontexte denselben Besucher haben.

Verwenden Sie dieses Muster, wenn Ihre Mobile App eine WebView- oder mobile Web-Seite öffnet, die Ihr Unternehmen steuert, und Sie möchten, dass die App-Aktivität und die Web-Aktivität weiterhin mit demselben Besucher verknüpft sind. Wenn Ihr Ziel die Identitätskontinuität zwischen Websites auf verschiedenen Domains ist, verwenden [ stattdessen die ](cross-domain-sharing.md) „Domain-übergreifende Freigabe“.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Ihre Implementierung die folgenden Anforderungen erfüllt:

* **Mobile App**: Die Adobe Experience Platform Mobile SDK mit der [Identity for Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/)-Erweiterungsversion **1.1.0 oder höher** (iOS und Android).
* **Web-**: Die [Web SDK](/help/collection/js/js-overview.md)-Version **2.11.0 oder höher** oder die Tag-Erweiterung „Web SDK&quot;.
* **URL-Steuerelement** Ihr Code steuert die URL, die die App an den WebView oder Browser übergibt, damit Sie Abfragezeichenfolgenparameter an ihn anhängen können.
* **Abgleichkonfiguration**: Dieselbe Experience Cloud-Organisations-ID wird sowohl in der mobilen als auch in der Web-Implementierung konfiguriert.

## Abrufen von Identitäten aus der Mobile App {#retrieve-identity}

Verwenden Sie die [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables)-API aus der Identity for Edge Network-Erweiterung, um die Identität des Besuchers als Abfragezeichenfolge abzurufen. Sie können diese Zeichenfolge dann an die URL anhängen, bevor Sie die WebView oder den Browser öffnen.

Die zurückgegebene Zeichenfolge enthält die folgenden URL-codierten Parameter:

| Parameter | Beschreibung |
| --- | --- |
| `MCID` | Die Experience Cloud-ID (ECID). |
| `MCORGID` | Ihre Experience Cloud-Organisations-ID. Dieser Parameter muss mit der in der Web-SDK auf der Zielseite konfigurierten Organisation übereinstimmen. |
| `TS` | Ein Zeitstempel. Das Ziel muss diesen Wert innerhalb von **fünf Minuten** erhalten oder die Übergabe wird abgelehnt. |

Die folgenden Code-Beispiele zeigen, wie eine Übergabe in Ihrer Mobile App aussehen könnte:

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Identität auf der Web-Seite erhalten {#receive-identity}

Für das Web-Ziel ist kein zusätzlicher Code erforderlich. Wenn die Web-SDK auf der Seite vorhanden ist und die URL einen gültigen `adobe_mc` enthält, extrahiert die SDK die ECID automatisch und wendet sie bei der ersten Edge Network-Anfrage auf die Identitätszuordnung des Besuchers an.

Wenn Ihr Web-Ziel die Tag-Erweiterung „Web SDK&quot; verwendet und Sie den Besucher unter Beibehaltung der Identität zu einer anderen Seite umleiten müssen, verwenden Sie die Aktion [Mit Identität umleiten](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md), um den `adobe_mc` Parameter zur nächsten Seite weiterzuleiten.

>[!NOTE]
>
>Der `adobe_mc` läuft nach **fünf Minuten** ab. Stellen Sie sicher, dass das Web-Ziel geladen wird und die erste Edge Network-Anfrage sofort nach dem Öffnen der URL sendet.
