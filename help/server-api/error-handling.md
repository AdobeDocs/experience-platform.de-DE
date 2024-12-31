---
title: Umgang mit Fehlern
description: Erfahren Sie mehr über die möglichen Fehler, auf die Sie beim Ausführen von API-Anfragen an die Adobe Experience Platform Edge Network Server-API stoßen können.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 9%

---

# Umgang mit Fehlern

## Übersicht {#overview}

API-Fehler in der Adobe Experience Platform Edge Network Server-API können verschiedene Ursachen haben: intern (Edge Network selbst) oder extern (Eingabe, Konfiguration oder Upstream-bezogene).

## Fehlertypen {#error-types}

| Fehler | Typ | Beschreibung | Status-Code |
| --- | --- | --- | --- |
| `RequestProcessingError` | Intern | Allgemeiner Fehler, der vom Adobe Experience Platform-Edge Network unter unerwarteten Umständen ausgegeben wurde. | `500` |
| `InputError` | Extern | Umfasst Fehler, die durch fehlerhafte Eingabe verursacht werden, sowie Fehler bei der Entitätsvalidierung. | `4xx` |
| `ConfigurationError` | Extern | Server-seitige Konfigurationsfehler. | `422` |
| `UpstreamError` | Extern | Kommunikationsfehler mit Upstream-Services. | `207 Multi-Status` |

## Schweregrad

Server-API-Fehler können auch nach Schweregrad unterteilt werden:

* **Schwerwiegende Fehler** stoppt die Dispatch-Pipeline.
* **Nicht schwerwiegende Fehler** können eine teilweise Verarbeitung signalisieren, während die Anforderungsverarbeitung fortgesetzt werden kann.
   * Wenn vorhanden, wird der Gesamtstatus-Code der Anfrage in `207 Multi-Status` geändert.

| Fehler | Typ | Bemerkungen          |
| --- | --- | --- |
| `RequestProcessingError` | FATAL | Kann während der Anfrageverarbeitung jederzeit passieren. |
| `InputError` | FATAL | Dies geschieht, wenn die Anfrage akzeptiert wird, bevor sie an den Upstream gesendet wird. |
| `ConfigurationError` | FATAL | Dies geschieht, wenn die Anfrage akzeptiert wird, bevor sie an den Upstream gesendet wird. |
| `UpstreamError` | Nicht tödlich | Kommunikationsfehler mit Upstream-Services. |

### Schwerwiegende Fehler {#fatal-errors}

Schwerwiegende Fehler unterbrechen die Anfrageverarbeitung und führen dazu, dass ein Nicht-2xx-Antwortstatus zurückgegeben wird. Sehen Sie sich den [Fehlertypen](#error-types) an, um den erwarteten Status-Code für jeden Fehlertyp anzuzeigen.

Zu Fehlern wird ein Antworttext mit einem Fehlerobjekt hinzugefügt. In diesem Fall enthält der Antworttext ein Problemdetail, wie in [RFC 7807 Problemdetails für HTTP-APIs](https://tools.ietf.org/html/rfc7807) definiert.

Der zurückgegebene Inhaltstyp ist der `application/problem+json` Medientyp. Wenn vorhanden, enthält diese Antwort maschinenlesbare Details zum Fehler. Zu den Problemdetails gehört ein URI-Typ.

Alle Fehlerobjekte verfügen über die Eigenschaften &quot;`type`&quot;, &quot;`status`&quot;, &quot;`title`&quot;, &quot;`detail`&quot; und &quot;`report`&quot;, sodass der API-Client feststellen kann, wo das Problem liegt.

| Eigenschaft | Typ | Beschreibung |
| -------- | ------ | ----------- |
| `type` | Zeichenfolge | Eine URI-Referenz (RFC3986), die den Problemtyp identifiziert und dem Format `https://ns.adobe.com/aep/errors/<ERROR-CODE>` folgt. |
| `status` | Zahl | Der vom Server für dieses Auftreten des Problems generierte HTTP-Status-Code. |
| `title` | String | Eine kurze, für Menschen lesbare Zusammenfassung des Problemtyps. |
| `detail` | String | Eine kurze, für Menschen lesbare Beschreibung des Problemtyps. |
| `report` | Objekt | Eine Zuordnung zusätzlicher Eigenschaften, die beim Debugging helfen, z. B. die Anfrage-ID oder die Organisations-ID. In einigen Fällen kann sie Daten enthalten, die für den jeweiligen Fehler spezifisch sind, z. B. eine Liste mit Validierungsfehlern. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Nicht schwerwiegende Fehler {#non-fatal-errors}

Nicht schwerwiegende Fehler können weiter unterteilt werden in:

* Fehler: Probleme, die bei der Verarbeitung der Anfrage aufgetreten sind, aber nicht dazu geführt haben, dass die gesamte Anfrage abgelehnt wurde (z. B. ein nicht kritischer Fehler im Vorfeld).
* Warnungen: Nachrichten von Upstream-Services, die darauf hinweisen können, dass eine teilweise Verarbeitung der Anfrage stattgefunden hat.

Wenn nicht schwerwiegende Fehler (außer Warnungen) auftreten, ändert der [!DNL Server API] den Antwortstatus in `207 Multi-Status`.

Warnhinweise sind dagegen meist informativ, da sie in der Regel eine potenziell vorübergehende Bedingung darstellen, die sich nicht in vollem Umfang auf die Anfrage ausgewirkt hat. Ein Beispiel hierfür ist ein in der Segmentierungs-Engine gelesenes Teilprofil. In diesem Fall wird die Genauigkeit etwas beeinträchtigt, die Funktionalität wird jedoch weiterhin bereitgestellt.

Nicht schwerwiegende Fehler werden im Format _Problemdetails_ dargestellt, sind jedoch direkt in die Standardantwort des Edge-Gateways vom Typ `application/json` eingebettet.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Umgang mit `4xx`- und `5xx`

| Fehler-Code | Beschreibung |
|---|---|
| `4xx Bad Request` | Die meisten `4xx` Fehler, z. B. 400, 403, 404, sollten nicht im Namen des Clients erneut versucht werden, mit Ausnahme von `429`. Hierbei handelt es sich um Clientfehler, die nicht erfolgreich sind. Der Client muss den Fehler beheben, bevor er die Anfrage erneut versuchen kann. |
| `429 Too Many Requests` | `429` HTTP-Antwort-Code gibt an, dass das Adobe Experience Platform-Edge Network oder ein vorgelagerter Service die Rate einschränkt, mit der die Anfragen verarbeitet werden. In diesem Fall muss der Aufrufer in einem solchen Fall die `Retry-After`-Antwortkopfzeile beachten. Jede Antwort, die zurückgegeben wird, muss den HTTP-Antwort-Code mit einem Domain-spezifischen Fehler-Code enthalten. |
| `500 Internal Server Error` | `500`-Fehler sind generische, allgemeingültige Fehler. `500` Fehler dürfen nicht erneut versucht werden, mit Ausnahme von `502` und `503`. Die Vermittler müssen mit einem `500` Fehler antworten und können mit einem allgemeinen Fehlercode/einer allgemeinen Fehlermeldung oder einem eher Domain-spezifischen Fehlercode/einer Fehlermeldung antworten. |
| `502 Bad Gateway` | Gibt an, dass das Adobe Experience Platform-Edge Network eine ungültige Antwort von den Upstreamservern erhalten hat. Hierzu kann es aufgrund von Netzwerkproblemen zwischen Servern kommen. Das temporäre Netzwerkproblem kann möglicherweise behoben werden, sodass das Problem möglicherweise durch einen erneuten Versuch behoben wird. Empfangende `502` Fehler können die Anfrage daher nach einiger Zeit erneut ausführen. |
| `503 Service Unavailable` | Dieser Fehler-Code gibt an, dass der Service vorübergehend nicht verfügbar ist. Hierzu kann es während Wartungszeiträumen kommen. Empfänger `503` Fehler können die Anfrage wiederholen, müssen jedoch die `Retry-After`-Kopfzeile beachten. |
| `504 Gateway Timeout` | Gibt an, dass die Adobe Experience Platform-Edge Network-Anfrage an die Upstream-Server abgelaufen ist. Dies kann aufgrund von Netzwerkproblemen zwischen Servern, DNS-Problemen oder anderen Netzwerkproblemen passieren. Die temporären Netzwerkprobleme können nach einiger Zeit behoben werden, und ein erneuter Versuch kann das Problem beheben. |
