---
title: Client-Zustandsverwaltung
description: Erfahren Sie, wie das Adobe Experience Platform Edge Network den Clientstatus verwaltet.
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: Client;Status;Management;Edge;Netzwerk;Gateway;API
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 3%

---

# Client-Zustandsverwaltung

Das Edge-Netzwerk selbst ist zustandslos (es verwaltet keine eigene Sitzung). Es gibt jedoch einige Anwendungsfälle, die eine clientseitige Statuspersistenz erfordern, z. B.:

* Konsistente Geräterkennung (siehe [Besucheridentifizierung](visitor-identification.md))
* Erfassen und Erzwingen der Benutzerzustimmung
* Kennung der Personalisierungssitzung beibehalten

Das Edge-Netzwerk verwendet ein Zustandsverwaltungsprotokoll, das den Speicheraspekt an seinen Client/SDK delegiert und Statuseinträge in seine Antworten einbezieht. Bei Browsern werden die Einträge als Cookies gespeichert.

Die Verantwortung des Kunden besteht darin, sie in allen nachfolgenden Anfragen zu speichern und einzubeziehen. Der Client muss auch für den ordnungsgemäßen Ablauf der Einträge sorgen, wie vom Gateway angewiesen. Wenn die Einträge als Cookies gespeichert wurden, führt der Browser all dies automatisch durch.

Obwohl die Statuseinträge immer eine Ebene aufweisen `String` -Wert (für Aufrufer/SDK sichtbar), sollten Sie die Werte in keiner Weise konsumieren oder manipulieren. Die Wertstruktur/-format oder sogar der Name selbst kann sich jederzeit ändern, was zu unerwartetem Verhalten für Clients führen kann, die den Status intern verwenden. Der Status soll immer vom Gateway selbst oder anderen Edge-Diensten genutzt werden.

## Beständiger Clientstatus als Metadaten

Der Status, der von der [!DNL Edge Network] im Antworttext ist eine `Handle` Objekt mit dem Typ `state:store`.

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
| `value` | Zeichenfolge | *Optional*. Der Eingabewert. |
| `maxAge` | Ganzzahl | *Optional* Die &quot;Einschaltzeit (TTL)&quot; (Einstiegszeit bis zum Live-Betrieb) in Sekunden. Wenn sie fehlt, sollten Einträge nur für die aktuelle Sitzung gespeichert werden. |
| `attrs` | `Map<String, String>` | *Optional*. Eine optionale Liste der Eintragsattribute. Bei allen sicheren Verbindungen mit einem sicheren Referrer-HTTP-Header muss die `SameSite` -Attribut auf `None`. |


Zur Unterstützung von Multi-Tagging (d. h. mehreren SDK-Instanzen in derselben Eigenschaft, die möglicherweise auf verschiedene Organisationen verweisen), werden alle Statuseinträge automatisch mit dem Präfix `kndctr_` und die URL-sichere Organisations-ID.

Wenn das Client-SDK eine `state:store` in der Antwort verarbeitet werden, muss es Folgendes tun:

* Speichern Sie Einträge Client-seitig, wobei die vom Gateway angegebene Ablaufzeit berücksichtigt wird.
* Laden Sie sie aus dem Client-Store und fügen Sie alle nicht abgelaufenen Einträge in die nachfolgenden Anforderungen ein.

Im Folgenden finden Sie ein Beispiel für eine Anfrage, die im clientseitigen gespeicherten Status übergeben wird:

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

## Beständiger Clientstatus in Browser-Cookies

Beim Arbeiten mit Browser-Clients kann das Edge Network die Einträge automatisch als Browser-Cookies beibehalten. Dies ermöglicht eine transparente Zustandsspeicherung, da Browser standardmäßig das Zustandsverwaltungsprotokoll einhalten.

Fast alle Einträge werden als Erstanbieter-Cookies bereitgestellt, wenn sie aktiviert und unterstützt werden (siehe Hinweis unten). Das Gateway kann jedoch auch einige Drittanbieter-Cookies speichern, wenn der Drittanbieter `adobedc.demdex.net` Domäne verwendet wird.

Da Einträge von ihrer Definition immer an einen bestimmten Bereich (Gerät/Anwendung) gebunden sind, wird nur die Teilmenge, die mit dem aktuellen Anforderungskontext kompatibel ist, vom Edge Network geschrieben. Nicht geschriebene Einträge werden innerhalb eines `state:store` Handle.

In der Regel werden Einträge mit Anwendungsbereichen immer als Erstanbieter-Cookies geschrieben, während Einträge mit Gerätebereich als Drittanbieter-Cookies geschrieben werden. Die Entscheidung ist für den Aufrufer vollständig transparent, das Gateway entscheidet, welche Einträge je nach Aufrufkontext geschrieben werden können.

Der Aufrufer muss explizit die Unterstützung zum Speichern des Clientstatus als Cookies über die `meta.state.cookiesEnabled` Markierung:

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
| `cookiesEnabled` | Boolesch | Wenn festgelegt, ermöglicht die Unterstützung von Cookies. Der Standardwert ist `false`. |
| `domain` | Zeichenfolge | Erforderlich when `cookiesEnabled: true`. Die Domäne auf oberster Ebene, in die die Cookies geschrieben werden sollen. Das Edge-Netzwerk verwendet diesen Wert, um zu entscheiden, ob der Status als Cookies beibehalten werden kann. |

Auch wenn die Cookie-Unterstützung über die `cookiesEnabled` -Markierung verwenden, schreibt das Adobe Experience Platform Edge Network die Statuseinträge nur, wenn die Top-Level-Domäne der Anforderung mit der `domain` vom Aufrufer angegeben. Wenn es zu einer Nichtübereinstimmung kommt, werden Einträge in einer `state:store` Handle.

Die Erstanbieter-Cookies können in folgenden Fällen nicht geschrieben werden (auch wenn die Unterstützung aktiviert ist):

* Die Anfrage geht an den Drittanbieter `adobedc.demdex.net` Domäne.
* Die Anfrage wird von einem Erstanbieter gestellt `CNAME` Domäne, die sich von der vom Aufrufer in angegebenen unterscheidet `meta.state.domain`.

## Cookie-Sicherheit

Alle Cookies haben die [Sichere Markierung](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) wann immer möglich aktiviert wurde.

Alle sicheren Cookies verfügen über die [SameSite-Attribut](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) auf `None`, was bedeutet, dass Cookies in allen Kontexten gesendet werden, sowohl in Erstanbieter- als auch in Cross-Origin-Instanzen.

* Für Erstanbieter-Cookies (`kndcrt_*`), die `Secure` -Markierung wird nur gesetzt, wenn der Anforderungskontext sicher (HTTPS) ist und wenn der Referrer ([Referrer HTTP Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) ist auch HTTPS. Wenn der Referrer nicht sicher (HTTP) ist, wird die `Secure` -Markierung fehlt, damit das Web SDK sie lesen kann. Ein sicheres Cookie kann nicht aus einem unsicheren Kontext gelesen werden.
* Für das Drittanbieter-Cookie (demdex) wird die Variable `Secure` -Flag immer gesetzt ist, da alle Anfragen HTTPS sind, sodass der Anforderungskontext sicher ist und dieses Cookie nie aus JavaScript gelesen wird.

Die `Secure` -Markierung ist nicht in der [Metadatendarstellung von Cookies](#state-as-metadata). Nur die `SameSite` -Attribut enthalten ist. In diesem Fall ist es Sache des Kunden, die `Secure` Markierung immer dann, wenn `SameSite` -Attribut vorhanden ist. Cookies mit `SameSite=None` muss auch `Secure` -Attribut, da sie einen sicheren Kontext (HTTPS) benötigen.
