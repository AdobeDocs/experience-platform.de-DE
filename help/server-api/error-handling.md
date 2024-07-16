---
title: Umgang mit Fehlern
description: Erfahren Sie mehr über die möglichen Fehler, die bei der Ausführung von API-Anfragen an die Adobe Experience Platform Edge Network Server-API auftreten können.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 9%

---

# Umgang mit Fehlern

## Übersicht {#overview}

API-Fehler in der Adobe Experience Platform Edge Network Server-API können verschiedene Ursachen haben: interne (Edge Network selbst) oder externe (Eingabe, Konfiguration oder vorgelagerte Beziehung).

## Fehlertypen {#error-types}

| Fehler | Typ | Beschreibung | Status-Code |
| --- | --- | --- | --- |
| `RequestProcessingError` | intern | Allgemeiner Zweckfehler, der vom Adobe Experience Platform-Edge Network bei unerwarteten Umständen ausgegeben wurde. | `500` |
| `InputError` | Externe | Enthält Fehler, die durch fehlerhafte Eingabe verursacht wurden, sowie Entitätsvalidierungsfehler. | `4xx` |
| `ConfigurationError` | Externe | Serverseitige Konfigurationsfehler. | `422` |
| `UpstreamError` | Externe | Kommunikationsfehler bei Upstream-Diensten. | `207 Multi-Status` |

## Schweregrad

Server-API-Fehler können auch nach Schweregrad aufgeteilt werden:

* **Schwerwiegende Fehler** stoppt die Dispatch-Pipeline.
* **Nicht tödliche Fehler** konnten eine partielle Verarbeitung signalisieren, während die Anforderungsverarbeitung fortgesetzt werden konnte.
   * Wenn vorhanden, wird der Gesamtstatuscode der Anfrage in `207 Multi-Status` geändert.

| Fehler | Typ | Bemerkungen          |
| --- | --- | --- |
| `RequestProcessingError` | Tödlich | Kann jederzeit während der Anforderungsverarbeitung erfolgen. |
| `InputError` | Tödlich | Tritt auf, wenn die Anfrage akzeptiert wird, bevor sie in einem vorgelagerten Schritt gesendet wird. |
| `ConfigurationError` | Tödlich | Tritt auf, wenn die Anfrage akzeptiert wird, bevor sie in einem vorgelagerten Schritt gesendet wird. |
| `UpstreamError` | Nicht tödlich | Kommunikationsfehler bei Upstream-Diensten. |

### Schwerwiegende Fehler {#fatal-errors}

Schwerwiegende Fehler stoppen die Anforderungsverarbeitung und führen zur Rückgabe des Nicht-2xx-Antwortstatus. Sehen Sie sich den Abschnitt [Fehlertypen](#error-types) an, um den erwarteten Statuscode für jeden Fehlertyp anzuzeigen.

Fehler werden von einem Antworttext begleitet, der ein Fehlerobjekt enthält. In diesem Fall enthält der Antworttext ein Problemdetail gemäß der Definition in [RFC 7807-Problemdetails für HTTP-APIs](https://tools.ietf.org/html/rfc7807).

Der zurückgegebene Inhaltstyp ist der Medientyp `application/problem+json` . Sofern vorhanden, enthält diese Antwort maschinenlesbare Details zum Fehler. Zu den Problemdetails zählen URI-Typen.

Alle Fehlerobjekte verfügen über die Nachrichteneigenschaften `type`, `status`, `title`, `detail` und `report`, sodass der API-Client erkennen kann, welches Problem vorliegt.

| Eigenschaft | Typ | Beschreibung |
| -------- | ------ | ----------- |
| `type` | Zeichenfolge | Eine URI-Referenz (RFC3986), die den Problemtyp identifiziert, gefolgt vom Format `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
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

* Fehler: Probleme, die während der Verarbeitung der Anfrage aufgetreten sind, aber nicht dazu geführt haben, dass die gesamte Anfrage abgelehnt wurde (z. B. nicht kritische Upstream-Fehler).
* Warnungen: Nachrichten von Upstream-Diensten, die darauf hinweisen könnten, dass die Anfrage teilweise verarbeitet wurde.

Bei nicht tödlichen Fehlern (ohne Warnungen) ändert der [!DNL Server API] den Antwortstatus auf `207 Multi-Status`.

Warnungen hingegen sind meist informativ, da sie im Allgemeinen eine potenziell vorübergehende Bedingung darstellen, die sich nicht vollständig auf die Anfrage auswirkte. Ein Beispiel hierfür ist ein Teilprofil, das in der Segmentierungsmaschine gelesen wird. In diesem Fall hat die Genauigkeit bis zu einem gewissen Grad Auswirkungen, die Funktionalität wird jedoch weiterhin bereitgestellt.

Fehler, die nicht tödlich sind, werden im Format _Problemdetails_ dargestellt, sind jedoch direkt in die Standardantwort des Edge-Gateways eingebettet, die vom Typ `application/json` ist.

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

## Umgang mit `4xx` und `5xx` Antworten

| Fehler-Code | Beschreibung |
|---|---|
| `4xx Bad Request` | Die meisten `4xx`-Fehler wie 400, 403, 404 sollten nicht im Namen des Clients wiederholt werden, mit Ausnahme von `429`. Dies sind Client-Fehler und werden nicht erfolgreich sein. Der Client muss den Fehler beheben, bevor die Anfrage erneut versucht werden kann. |
| `429 Too Many Requests` | `429` HTTP-Antwortcode zeigt an, dass das Adobe Experience Platform-Edge Network oder ein Upstream-Dienst die Rate begrenzt. In diesem Fall muss der Aufrufer in einem solchen Szenario die Antwort-Kopfzeile `Retry-After` berücksichtigen. Jede Antwort, die zurückgegeben wird, muss den HTTP-Antwort-Code mit einem Domain-spezifischen Fehler-Code enthalten. |
| `500 Internal Server Error` | `500`-Fehler sind generische, allgemeingültige Fehler. Fehler vom Typ `500` dürfen nicht wiederholt werden, mit Ausnahme von `502` und `503`. Intermediäre müssen mit einem `500` -Fehler antworten und können mit einem allgemeinen Fehlercode/einer allgemeinen Fehlermeldung oder einem domänenspezifischeren Fehlercode/einer domänenspezifischen Fehlermeldung reagieren. |
| `502 Bad Gateway` | Gibt an, dass das Adobe Experience Platform-Edge Network eine ungültige Antwort von Upstream-Servern erhalten hat. Hierzu kann es aufgrund von Netzwerkproblemen zwischen Servern kommen. Das temporäre Netzwerkproblem kann möglicherweise gelöst werden, sodass ein erneuter Versuch das Problem beheben kann, sodass Empfänger von `502` -Fehlern die Anfrage nach einiger Zeit erneut versuchen können. |
| `503 Service Unavailable` | Dieser Fehler-Code gibt an, dass der Service vorübergehend nicht verfügbar ist. Hierzu kann es während Wartungszeiträumen kommen. Empfänger von `503` -Fehlern können die Anfrage möglicherweise erneut versuchen, müssen jedoch die `Retry-After` -Kopfzeile berücksichtigen. |
| `504 Gateway Timeout` | Gibt an, dass bei Adobe Experience Platform-Edge Network-Anfragen an die Upstream-Server eine Zeitüberschreitung aufgetreten ist. Dies kann aufgrund von Netzwerkproblemen zwischen Servern, DNS-Problemen oder anderen Netzwerkproblemen auftreten. Die temporären Netzwerkprobleme können nach einiger Zeit behoben werden und ein erneuter Versuch kann das Problem lösen. |
