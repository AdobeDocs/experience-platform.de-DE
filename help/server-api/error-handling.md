---
title: Umgang mit Fehlern
description: Erfahren Sie mehr über die möglichen Fehler, die bei der Ausführung von API-Anfragen an die Adobe Experience Platform Edge Network Server-API auftreten können.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 4%

---

# Umgang mit Fehlern

## Übersicht {#overview}

API-Fehler in der Adobe Experience Platform Edge Network Server-API können verschiedene Ursachen haben: interne (Edge Network selbst) oder externe (Eingabe, Konfiguration oder vorgelagerte) Ursachen.

## Fehlertypen {#error-types}

| Fehler | Typ | Beschreibung | Status-Code |
| --- | --- | --- | --- |
| `RequestProcessingError` | Intern | Allgemeiner Zweckfehler, der vom Adobe Experience Platform Edge Network unter unerwarteten Umständen ausgegeben wurde. | `500` |
| `InputError` | Extern | Enthält Fehler, die durch fehlerhafte Eingabe verursacht wurden, sowie Entitätsvalidierungsfehler. | `4xx` |
| `ConfigurationError` | Extern | Serverseitige Konfigurationsfehler. | `422` |
| `UpstreamError` | Extern | Kommunikationsfehler bei Upstream-Diensten. | `207 Multi-Status` |

## Schweregrad

Server-API-Fehler können auch nach Schweregrad aufgeteilt werden:

* **Schwerwiegende Fehler** stoppt die Dispatch-Pipeline.
* **Nicht tödliche Fehler** kann eine partielle Verarbeitung signalisieren und gleichzeitig die Weiterverarbeitung der Anforderung ermöglichen.
   * Wenn vorhanden, wird der allgemeine Status-Code der Anfrage in `207 Multi-Status`.

| Fehler | Typ | Bemerkungen |
| --- | --- | --- |
| `RequestProcessingError` | Tödlich | Kann jederzeit während der Anforderungsverarbeitung erfolgen. |
| `InputError` | Tödlich | Tritt auf, wenn die Anfrage akzeptiert wird, bevor sie in einem vorgelagerten Schritt gesendet wird. |
| `ConfigurationError` | Tödlich | Tritt auf, wenn die Anfrage akzeptiert wird, bevor sie in einem vorgelagerten Schritt gesendet wird. |
| `UpstreamError` | Nicht tödlich | Kommunikationsfehler bei Upstream-Diensten. |

### Schwerwiegende Fehler {#fatal-errors}

Schwerwiegende Fehler stoppen die Anforderungsverarbeitung und führen zur Rückgabe des Nicht-2xx-Antwortstatus. Sehen Sie sich die [Fehlertypen](#error-types) -Abschnitt, um den erwarteten Status-Code zu sehen, der jedem Fehlertyp entspricht.

Fehler werden von einem Antworttext begleitet, der ein Fehlerobjekt enthält. In diesem Fall enthält der Antworttext ein Problemdetail, wie definiert durch [RFC 7807 - Problemdetails für HTTP-APIs](https://tools.ietf.org/html/rfc7807).

Der zurückgegebene Inhaltstyp ist der `application/problem+json` Medientyp. Sofern vorhanden, enthält diese Antwort maschinenlesbare Details zum Fehler. Zu den Problemdetails zählen URI-Typen.

Alle Fehlerobjekte haben eine `type`, `status`, `title`, `detail` und `report` Meldungseigenschaften, damit der API-Client das Problem erkennen kann.

| Eigenschaft | Typ | Beschreibung |
| -------- | ------ | ----------- |
| `type` | Zeichenfolge | Eine URI-Referenz (RFC3986), die den Problemtyp angibt, im folgenden Format: `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Zahl | Der vom Server für dieses Auftreten des Problems generierte HTTP-Status-Code. |
| `title` | Zeichenfolge | Eine kurze, für Menschen lesbare Zusammenfassung des Problemtyps. |
| `detail` | Zeichenfolge | Eine kurze, für Menschen lesbare Beschreibung des Problemtyps. |
| `report` | Objekt | Eine Zuordnung von zusätzlichen Eigenschaften, die das Debugging unterstützen, z. B. die Anfrage-ID oder die Organisations-ID. In einigen Fällen kann er Daten enthalten, die für den jeweiligen Fehler spezifisch sind, z. B. eine Liste mit Validierungsfehlern. |

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

### Nicht tödliche Fehler {#non-fatal-errors}

Nicht-tödliche Fehler können weiter aufgeschlüsselt werden in:

* Fehler: Probleme, die bei der Verarbeitung der Anfrage aufgetreten sind, aber nicht dazu geführt haben, dass die gesamte Anfrage abgelehnt wurde (z. B. nicht kritische Upstream-Fehler).
* Warnungen: Nachrichten von vorgelagerten Diensten, die darauf hinweisen könnten, dass die Anfrage teilweise verarbeitet wurde.

Bei nichtletalen Fehlern (ohne Warnungen) wird die [!DNL Server API] ändert den Antwortstatus in `207 Multi-Status`.

Warnungen hingegen sind meist informativ, da sie im Allgemeinen eine potenziell vorübergehende Bedingung darstellen, die sich nicht vollständig auf die Anfrage auswirkte. Ein Beispiel hierfür ist ein Teilprofil, das in der Segmentierungsmaschine gelesen wird. In diesem Fall hat die Genauigkeit bis zu einem gewissen Grad Auswirkungen, die Funktionalität wird jedoch weiterhin bereitgestellt.

Nicht tödliche Fehler werden im _Problemdetails_ Format, jedoch direkt in die Standardantwort des Edge-Gateways eingebettet, die vom Typ `application/json`.

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

## Handhabung `4xx` und `5xx` Antworten


| Fehler-Code | Beschreibung |
|---|---|
| `4xx Bad Request` | Am meisten `4xx` Fehler wie 400, 403, 404 sollten nicht im Namen des Kunden wiederholt werden, außer für `429`. Dies sind Client-Fehler und werden nicht erfolgreich sein. Der Client muss den Fehler beheben, bevor die Anfrage erneut versucht werden kann. |
| `429 Too Many Requests` | `429` HTTP-Antwort-Code gibt an, dass das Adobe Experience Platform Edge Network oder ein Upstream-Dienst die Rate begrenzt. In diesem Fall muss der Anrufer in einem solchen Fall die `Retry-After` Antwortheader. Jede Antwort, die zurückfließt, muss den HTTP-Antwort-Code mit einem domänenspezifischen Fehlercode enthalten. |
| `500 Internal Server Error` | `500` Fehler sind allgemeine, allgemeingültige Fehler. `500` -Fehler dürfen nicht wiederholt werden, mit Ausnahme von `502` und `503`. Vermittelnde Stellen müssen mit einer `500` und kann mit einem generischen Fehlercode/einer generischen Fehlermeldung oder einem domänenspezifischeren Fehlercode/einer domänenspezifischen Fehlermeldung reagieren. |
| `502 Bad Gateway` | Gibt an, dass das Adobe Experience Platform Edge Network eine ungültige Antwort von Upstream-Servern erhalten hat. Dies kann aufgrund von Netzwerkproblemen zwischen Servern geschehen. Das temporäre Netzwerkproblem kann gelöst werden, sodass ein erneuter Versuch das Problem lösen kann, sodass Empfänger von `502` -Fehler können die Anfrage nach einiger Zeit erneut versuchen. |
| `503 Service Unavailable` | Dieser Fehlercode zeigt an, dass der Dienst vorübergehend nicht verfügbar ist. Dies kann während der Wartungszeiträume geschehen. Empfänger `503` Fehler können die Anfrage möglicherweise erneut versuchen, müssen jedoch die `Retry-After` -Kopfzeile. |
| `504 Gateway Timeout` | Gibt an, dass bei der Adobe Experience Platform Edge Network-Anforderung an die Upstream-Server eine Zeitüberschreitung aufgetreten ist. Dies kann aufgrund von Netzwerkproblemen zwischen Servern, DNS-Problemen oder anderen Netzwerkproblemen auftreten. Die temporären Netzwerkprobleme können nach einiger Zeit behoben werden und ein erneuter Versuch kann das Problem lösen. |
