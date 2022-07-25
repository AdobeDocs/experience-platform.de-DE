---
title: Client-Zustandsverwaltung
description: Erfahren Sie, wie das Adobe Experience Platform Edge Network den Client-Status verwaltet.
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: Client;Status;Management;Edge;Network;Gateway;API
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 100%

---

# Client-Zustandsverwaltung

Das Edge Network selbst besitzt keinen Status (es verwaltet keine eigene Sitzung). Es gibt jedoch einige Anwendungsfälle, die eine Client-seitige Persistenz eines Status erfordern, z. B.:

* Konsistente Geräterkennung (siehe [Besucheridentifizierung](visitor-identification.md))
* Erfassen und Erzwingen der Benutzerzustimmung
* Beibehalten der Kennung der Personalisierungssitzung

Das Edge Network verwendet ein Protokoll zur Statusverwaltung, das den Speicheraspekt an seinen Client/SDK delegiert und Statuseinträge in seine Antworten einbezieht. Bei Browsern werden die Einträge als Cookies gespeichert.

Es liegt in der Verantwortung des Clients, diese Einträge in allen nachfolgenden Anfragen zu speichern und einzubeziehen. Der Client muss auch für den ordnungsgemäßen Ablauf der Einträge sorgen, wie vom Gateway angewiesen. Wenn die Einträge als Cookies gespeichert wurden, führt der Browser all dies automatisch durch.

Obwohl die Statuseinträge immer einen einfachen `String`-Wert aufweisen (für Aufrufer/SDK sichtbar), sollten Sie die Werte in keiner Weise konsumieren oder manipulieren. Die Struktur/das Format des Wertes oder sogar der Name kann sich jederzeit ändern, was zu unerwartetem Verhalten für Clients führen kann, die den Status intern verwenden. Der Status soll nur vom Gateway selbst oder anderen Edge-Services genutzt werden.

## Beständiger Client-Status als Metadaten

Der Status, der von [!DNL Edge Network] im Antworttext zurückgegeben wird, ist ein `Handle`-Objekt mit dem Typ `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Attribut | Typ | Beschreibung |
| --- | --- | --- |
| `key` | Zeichenfolge | **Erforderlich**. Der Name des Eintrags. |
| `value` | Zeichenfolge | *Optional*. Der Wert des Eintrags. |
| `maxAge` | Ganzzahl | *Optional*: Die Lebensdauer („time-to-live“, TTL) des Eintrags in Sekunden. Wenn sie fehlt, sollten Einträge nur für die aktuelle Sitzung gespeichert werden. |
| `attrs` | `Map<String, String>` | *Optional*. Eine optionale Liste der Eintragsattribute. Für alle sicheren Verbindungen mit einer sicheren Referrer-HTTP-Kopfzeile wird das Attribut `SameSite` auf `None` gesetzt. |


Zur Unterstützung von Multi-Tagging (d. h. mehreren SDK-Instanzen in derselben Eigenschaft, die möglicherweise auf verschiedene Organisationen verweisen) werden alle Statuseinträge automatisch mit dem Präfix `kndctr_` und der URL-sicheren Organisations-ID versehen.

Wenn das Client-SDK ein `state:store`-Handle in der Antwort erhält, muss es Folgendes tun:

* Einträge Client-seitig speichern und dabei die vom Gateway angegebene Ablaufzeit beachten.
* Sie aus dem Client-Speicher laden und alle nicht abgelaufenen Einträge in die nachfolgenden Anfragen aufnehmen.

Im Folgenden finden Sie ein Beispiel für eine Anfrage, die im Client-seitigen gespeicherten Status übergeben wird:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Beständiger Client-Status in Browser-Cookies

Beim Arbeiten mit Browser-Clients kann das Edge Network die Einträge automatisch als Browser-Cookies aufbewahren. Dies ermöglicht eine transparente Zustandsspeicherung, da Browser standardmäßig das Protokoll zur Statusverwaltung einhalten.

Fast alle Einträge werden als Erstanbieter-Cookies bereitgestellt, wenn sie aktiviert und unterstützt werden (siehe Hinweis unten). Das Gateway kann jedoch auch einige Drittanbieter-Cookies speichern, wenn die Drittanbieter-Domain `adobedc.demdex.net` verwendet wird.

Da Einträge von ihrer Definition immer an einen bestimmten Bereich (Gerät/Programm) gebunden sind, wird nur die Teilmenge, die mit dem aktuellen Anfragekontext kompatibel ist, vom Edge Network geschrieben. Nicht geschriebene Einträge werden innerhalb eines `state:store`-Handles zurückgegeben.

In der Regel werden programmbezogene Einträge immer als Erstanbieter-Cookies geschrieben, während gerätebezogene Einträge als Drittanbieter-Cookies geschrieben werden. Die Entscheidung ist für die Aufrufenden vollständig transparent, und das Gateway entscheidet, welche Einträge je nach Aufrufkontext geschrieben werden können.

Die Aufrufenden müssen die Unterstützung für die Speicherung von Client-Status als Cookies explizit über das Flag `meta.state.cookiesEnabled` aktivieren:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Attribut | Typ | Beschreibung |
| --- | --- | --- |
| `cookiesEnabled` | Boolesch | Wenn festgelegt, ermöglicht es die Unterstützung von Cookies. Der Standardwert ist `false`. |
| `domain` | Zeichenfolge | Erforderlich wenn `cookiesEnabled: true`. Die Domain auf oberster Ebene, in die die Cookies geschrieben werden sollen. Das Edge Network verwendet diesen Wert, um zu entscheiden, ob der Status als Cookies beibehalten werden kann. |

Selbst wenn die Cookie-Unterstützung über das Flag `cookiesEnabled` aktiviert ist, schreibt das Adobe Experience Platform Edge Network die Statuseinträge nur, wenn die Top-Level-Domain der Anforderung mit der von den Aufrufenden angegebenen `domain` übereinstimmt. Bei Nichtübereinstimmung werden die Einträge in einem `state:store`-Handle zurückgegeben.

Die Erstanbieter-Cookies können in folgenden Fällen nicht geschrieben werden (selbst wenn die Unterstützung aktiviert ist):

* Die Anforderung kommt über die `adobedc.demdex.net`-Domain eines Drittanbieters.
* Die Anfrage kommt von einer `CNAME`-Domain eines Erstanbieters, die sich von derjenigen unterscheidet, die die Aufrufenden in `meta.state.domain` angegeben haben.

## Cookie-Sicherheit

Für alle Cookies ist das [Sicherheits-Flag](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Cookies#restrict_access_to_cookies) nach Möglichkeit aktiviert.

Bei allen sicheren Cookies ist das [SameSite-Attribut](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Set-Cookie/SameSite) auf `None` gesetzt, was bedeutet, dass Cookies in allen Kontexten gesendet werden, egal ob Erstanbieter oder Queranbieter.

* Für die Erstanbieter-Cookies (`kndcrt_*`) wird das Flag `Secure` nur gesetzt, wenn der Anfragekontext sicher ist (HTTPS) und wenn der Referrer ([Referrer-HTTP-Kopfzeile](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Referer)) ebenfalls HTTPS ist. Wenn der Referrer nicht sicher ist (HTTP), wird das Flag `Secure` weggelassen, damit das Web SDK die Cookies lesen kann. Ein sicheres Cookie kann nicht aus einem unsicheren Kontext gelesen werden.
* Für das Drittanbieter-Cookie (demdex) wird das Flag `Secure` immer gesetzt ist, da alle Anfragen HTTPS sind, sodass der Anfragekontext sicher ist und dieses Cookie nie aus JavaScript gelesen wird.

Das Flag `Secure` ist in der [Metadatendarstellung von Cookies](#state-as-metadata) nicht vorhanden. Nur das Attribut `SameSite` ist enthalten. In diesem Fall liegt es in der Verantwortung des Clients, das Flag `Secure` korrekt zu setzen, wenn das Attribut `SameSite` vorhanden ist. Cookies mit `SameSite=None` müssen auch das Attribut `Secure` angeben, da sie einen sicheren Kontext (HTTPS) erfordern.
