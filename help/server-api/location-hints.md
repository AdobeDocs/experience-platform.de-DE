---
title: Standorthinweise
description: In diesem Artikel wird erläutert, wie Standorthinweise in der Edge Network-Server-API funktionieren, sodass Endbenutzeranfragen immer an denselben Server weitergeleitet werden können.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# Standorthinweise

## Übersicht {#overview}

Der [!DNL Adobe Experience Platform Edge Network] verwendet mehrere global verteilte Server, um schnelle Reaktionszeiten unabhängig vom Standort des Endbenutzers zu gewährleisten. Außerdem wird DNS-basiertes Routing verwendet, um sicherzustellen, dass Anfragen immer an den Edge Network-Speicherort weitergeleitet werden, der den Endbenutzern am nächsten ist.

Wenn Endbenutzer während einer Sitzung eine Verbindung zu einem VPN herstellen oder auf ihren Mobilgeräten Netzwerktypen wechseln, können Edge Network-Anfragen oft an einen anderen Speicherort weitergeleitet werden. Das Routing zwischen Servern während der Sitzung kann problematisch sein, da Adobe Experience Platform- und Adobe Experience Cloud-Lösungen Endbenutzerprofilinformationen im Edge Network speichern.

An dieser Stelle kommen Standorthinweise ins Spiel.

Um sicherzustellen, dass Endbenutzende immer mit dem regionalen Sitzungsserver interagieren, der ihre aktuellen Profildaten enthält, stellt die Funktion für Standorthinweise sicher, dass alle Anfragen an das Edge Network Edge Network an denselben Server gesendet werden, auf dem die erste Sitzungsanfrage erfolgte. Dies hilft Benutzern, ein konsistentes Erlebnis zu haben, unabhängig davon, welche Netzwerkänderungen sie im Laufe einer Sitzung erleben.

## Verwendung von Standorthinweisen

Speicherorthinweise sind in der Antwort der ersten Edge Network-Anfrage und in allen nachfolgenden Anfragen enthalten, wie im folgenden Beispiel gezeigt:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

Der `EdgeNetwork` enthält alle relevanten Informationen, die das Edge Network benötigt, um nachfolgende Anfragen entsprechend weiterzuleiten. In der Antwort auf die anfängliche und jede nachfolgende Anfrage an das Edge-Netzwerk gibt es einen Abschnitt im -Handle mit dem Typ `locationHint:result`.

Der mit dem `EdgeNetwork` Bereich verknüpfte Hinweis kann einen der folgenden Werte enthalten:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API-Format**

Um sicherzustellen, dass nachfolgende Anfragen korrekt weitergeleitet werden, fügen Sie den Standorthinweis in den URL-Pfad nachfolgender API-Aufrufe zwischen dem Basispfad, in der Regel `ee`, und `v2` API-Version ein.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Speichern von Standorthinweisen in Cookies {#storing-hints-in-cookies}

Um sicherzustellen, dass der vom Edge Network zurückgegebene Standorthinweis für die Dauer der Sitzung bestehen bleibt, können Sie den Wert des Standorthinweises zusammen mit der Cookie-Lebensdauer in einem Cookie speichern, das im Feld `ttlSeconds` enthalten ist (in der Regel 1800 Sekunden).

Wie bei den meisten Cookies sollten Sie die Lebensdauer dieses Cookies jedes Mal verlängern, wenn eine Antwort des Edge Networks eingeht. Um eine größtmögliche Kompatibilität mit der Web-SDK zu gewährleisten, verwenden Sie den Cookie-Namen `kndctr_{IMSORG}_AdobeOrg_cluster`. Organisations-IDs enden normalerweise mit `@AdobeOrg`. Der `@` muss in einen Unterstrich konvertiert werden, um sicherzustellen, dass das Cookie das richtige Format aufweist.
