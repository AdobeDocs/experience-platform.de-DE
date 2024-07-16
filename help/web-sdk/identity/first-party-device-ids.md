---
title: Erstanbieter-Geräte-IDs im Web SDK
description: Erfahren Sie, wie Sie Erstanbieter-Geräte-IDs (FPIDs) für das Adobe Experience Platform Web SDK konfigurieren.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 9f10d48357b7fb28dc54375a4d077d0a1961a746
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---


# Erstanbieter-Geräte-IDs im Web SDK

Das Adobe Experience Platform Web SDK weist Website-Besuchern mithilfe von Cookies [Adobe Experience Cloud IDs (ECIDs)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=de) zu, um das Benutzerverhalten zu verfolgen. Um Browserbeschränkungen für Cookie-Lebenszyklen zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Diese werden als Erstanbieter-Geräte-IDs (FPIDs) bezeichnet.

>[!NOTE]
>
>Die Unterstützung der Erstanbieter-Geräte-ID ist nur verfügbar, wenn Daten über das Platform Web SDK an das Platform-Edge Network gesendet werden.

>[!IMPORTANT]
>
>Geräte-IDs von Erstanbietern sind nicht mit der Funktion [Drittanbieter-Cookies](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) im Web SDK kompatibel.
>Sie können entweder Geräte-IDs von Erstanbietern verwenden oder Sie können Drittanbieter-Cookies verwenden, aber Sie können nicht beide Funktionen gleichzeitig verwenden.

In diesem Dokument wird beschrieben, wie Sie Erstanbieter-Geräte-IDs für Ihre Platform Web SDK-Implementierung konfigurieren.

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie mit der Funktionsweise von Identitätsdaten für das Platform Web SDK vertraut sind, einschließlich der Rolle von ECIDs und `identityMap`. Weitere Informationen finden Sie in der Übersicht zu [Identitätsdaten im Web SDK](./overview.md) .

## Verwenden von FPIDs

FPIDs verfolgen Besucher mithilfe von Erstanbieter-Cookies. Erstanbieter-Cookies sind am effektivsten, wenn sie mit einem Server gesetzt werden, der einen DNS-Eintrag [A record](https://datatracker.ietf.org/doc/html/rfc1035) (für IPv4) oder einen [AAAA-Eintrag](https://datatracker.ietf.org/doc/html/rfc3596) (für IPv6) verwendet, im Gegensatz zu einem DNS-CNAME oder JavaScript-Code.

>[!IMPORTANT]
>
>Datensätze vom Typ `A` oder `AAAA` werden nur zum Setzen und Verfolgen von Cookies unterstützt. Die primäre Methode für die Datenerfassung ist ein DNS-CNAME. Anders ausgedrückt: FPIDs werden mit einem A-Datensatz oder AAAA-Datensatz festgelegt und dann mit einem CNAME an Adobe gesendet.
>
>Das [Adobe-Managed Certificate Program](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) wird auch für die Erstanbieter-Datenerfassung unterstützt.

Sobald ein FPID-Cookie gesetzt ist, kann der zugehörige Wert abgerufen und an Adobe gesendet werden, während Ereignisdaten erfasst werden. Erfasste FPIDs werden als Samen zur Generierung von ECIDs verwendet, die in Adobe Experience Cloud-Anwendungen weiterhin die primäre IDs sind.

Um eine FPID für einen Website-Besucher an das Platform-Edge Network zu senden, müssen Sie die FPID in die `identityMap` für diesen Besucher einschließen. Weitere Informationen finden Sie im Abschnitt weiter unten in diesem Dokument zu [Verwendung von FPIDs in `identityMap`](#identityMap) .

### Anforderungen an die ID-Formatierung

Das Platform-Edge Network akzeptiert nur IDs, die dem [UUIDv4-Format](https://datatracker.ietf.org/doc/html/rfc4122) entsprechen. Geräte-IDs, die nicht im UUIDv4-Format vorliegen, werden abgelehnt.

Die Erstellung einer UUID führt fast immer zu einer eindeutigen, zufälligen ID, wobei die Wahrscheinlichkeit eines Zusammenstoßes vernachlässigbar ist. UUIDv4 kann nicht mit IP-Adressen oder anderen personenbezogenen Daten (PII) gesendet werden. UUIDs sind allgegenwärtig und es gibt Bibliotheken für praktisch jede Programmiersprache, um sie zu generieren.

## Festlegen eines Erstanbieter-ID-Cookies in der Benutzeroberfläche von Datastreams {#setting-cookie-datastreams}

Sie können einen Cookie-Namen in der Benutzeroberfläche von Datastreams angeben, in dem sich der [!DNL FPID] befinden kann, anstatt den Cookie-Wert lesen und die FPID in die Identitätszuordnung aufnehmen zu müssen.

>[!IMPORTANT]
>
>Für diese Funktion muss [Erstanbieter-Datenerfassung](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) aktiviert sein.

Detaillierte Informationen zum Konfigurieren eines Datenspeichers finden Sie in der Dokumentation zu [datastreams](../../datastreams/configure.md) .

Aktivieren Sie beim Konfigurieren Ihres Datastreams die Option **[!UICONTROL Erstanbieter-ID-Cookie]** . Diese Einstellung weist das Edge Network an, beim Suchen nach einer Erstanbieter-Geräte-ID auf ein bestimmtes Cookie zu verweisen, anstatt nach diesem Wert in der [Identitätszuordnung](#identityMap) zu suchen.

Weitere Informationen zur Arbeit mit Adobe Experience Cloud finden Sie in der Dokumentation zu [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) .

![Bild der Platform-Benutzeroberfläche, das die Konfiguration des Datastreams anzeigt und die Einstellung des Erstanbieter-ID-Cookies hervorhebt](../assets/first-party-id-datastreams.png)

Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die ID gespeichert werden soll.

Wenn Sie Erstanbieter-IDs verwenden, können Sie keine ID-Synchronisierungen von Drittanbietern durchführen. Die Synchronisierung der Drittanbieter-ID beruht auf dem [!DNL Visitor ID]-Dienst und dem von diesem Dienst generierten `UUID`. Bei Verwendung der Erstanbieter-ID-Funktion wird die ECID ohne Verwendung des [!DNL Visitor ID]-Dienstes generiert, wodurch ID-Synchronisierungen von Drittanbietern unmöglich werden.

Wenn Sie Erstanbieter-IDs verwenden, werden Audience Manager-Funktionen, die auf die Aktivierung in Partnerplattformen ausgerichtet sind, nicht unterstützt, da die Audience Manager-Partner-ID-Synchronisationen hauptsächlich auf `UUIDs` oder `DIDs` basieren. Die ECID, die von einer Erstanbieter-ID abgeleitet wird, ist nicht mit einem `UUID` verknüpft, sodass sie nicht mehr adressierbar ist.

## Festlegen eines Cookies mithilfe eines eigenen Servers

Beim Festlegen eines Cookies mithilfe eines Servers, dessen Eigentümer Sie sind, können verschiedene Methoden verwendet werden, um zu verhindern, dass das Cookie aufgrund von Browserrichtlinien eingeschränkt wird:

* Generieren von Cookies mithilfe von serverseitigen Skriptsprachen
* Setzen von Cookies als Reaktion auf eine API-Anfrage an eine Subdomain oder einen anderen Endpunkt auf der Site
* Generieren von Cookies mithilfe eines CMS
* Generieren von Cookies mithilfe eines CDN

>[!IMPORTANT]
>
>Cookies, die mit der JavaScript-Methode `document.cookie` gesetzt werden, werden fast nie vor Browserrichtlinien geschützt, die die Cookie-Dauer einschränken.

### Festlegen des Cookies

Das FPID-Cookie sollte idealerweise gesetzt werden, bevor Anfragen an das Edge Network gesendet werden. In Fällen, in denen dies nicht möglich ist, wird jedoch eine ECID nach wie vor mit vorhandenen Methoden generiert und dient als primäre Kennung, solange das Cookie vorhanden ist.

Wenn die ECID schließlich von einer Richtlinie zum Löschen von Browsern beeinflusst wird, die FPID jedoch nicht, wird die FPID beim nächsten Besuch zur primären Kennung und wird zum Testen der ECID bei jedem nachfolgenden Besuch verwendet.

### Festlegen des Ablaufs für das Cookie

Das Festlegen des Ablaufs eines Cookies sollte bei der Implementierung der FPID-Funktion sorgfältig berücksichtigt werden. Bei der Entscheidung sollten Sie die Länder oder Regionen berücksichtigen, in denen Ihre Organisation tätig ist, sowie die Gesetze und Richtlinien in jeder dieser Regionen.

Im Rahmen dieser Entscheidung möchten Sie möglicherweise eine unternehmensweite Cookie-Einstellung oder eine Richtlinie festlegen, die für Benutzer in jedem Gebietsschema, in dem Sie tätig sind, unterschiedlich ist.

Unabhängig von der Einstellung, die Sie für den anfänglichen Ablauf eines Cookies auswählen, müssen Sie sicherstellen, dass Sie eine Logik einschließen, die den Ablauf des Cookies bei jedem neuen Besuch der Site verlängert.

## Auswirkungen von Cookie-Flags

Es gibt verschiedene Cookie-Flags, die sich auf die Behandlung von Cookies in verschiedenen Browsern auswirken:

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Auf Cookies, die mit dem Flag `HTTPOnly` gesetzt wurden, kann nicht mithilfe clientseitiger Skripte zugegriffen werden. Wenn Sie beim Festlegen der FPID eine `HTTPOnly` -Markierung setzen, müssen Sie also eine serverseitige Skriptsprache verwenden, um den Cookie-Wert zur Aufnahme in `identityMap` zu lesen.

Wenn Sie sich dafür entscheiden, dass das Platform-Edge Network den Wert des FPID-Cookies liest, stellt das Setzen des Flags &quot;`HTTPOnly`&quot;sicher, dass der Wert nicht von clientseitigen Skripten aufgerufen werden kann, jedoch keine negativen Auswirkungen auf die Fähigkeit des Platform-Edge Networks, das Cookie zu lesen.

>[!NOTE]
>
>Die Verwendung des Flags `HTTPOnly` hat keine Auswirkungen auf die Cookie-Richtlinien, die die Lebensdauer von Cookies einschränken können. Sie sollten dies jedoch dennoch berücksichtigen, während Sie den Wert der FPID festlegen und lesen.

### `Secure` {#secure}

Mit dem Attribut `Secure` festgelegte Cookies werden nur mit einer verschlüsselten Anforderung über das HTTPS-Protokoll an den Server gesendet. Die Verwendung dieses Flag kann dazu beitragen, sicherzustellen, dass man-in-the-Middle-Angreifer nicht einfach auf den Wert des Cookies zugreifen können. Wenn möglich, ist es immer empfehlenswert, das `Secure` -Flag festzulegen.

### `SameSite` {#same-site}

Mit dem Attribut `SameSite` können Server bestimmen, ob Cookies mit Site-übergreifenden Anforderungen gesendet werden. Das -Attribut bietet einen gewissen Schutz vor Site-übergreifenden Fälschungsangriffen. Es gibt drei mögliche Werte: `Strict`, `Lax` und `None`. Wenden Sie sich an Ihr internes Team, um zu bestimmen, welche Einstellung für Ihr Unternehmen geeignet ist.

Wenn kein `SameSite` -Attribut angegeben ist, ist die Standardeinstellung für einige Browser jetzt `SameSite=Lax`.

## Verwenden von FPIDs in `identityMap` {#identityMap}

Im Folgenden finden Sie ein Beispiel dafür, wie Sie eine FPID im `identityMap` festlegen:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Wie bei anderen Identitätstypen können Sie die FPID mit anderen Identitäten in `identityMap` einbeziehen. Im Folgenden finden Sie ein Beispiel der FPID, die mit einer authentifizierten CRM-ID enthalten ist:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Wenn die FPID in einem Cookie enthalten ist, das vom Edge Network gelesen wird, wenn die Erstanbieter-Datenerfassung aktiviert ist, sollten Sie nur die authentifizierte CRM-ID erfassen:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Die folgende `identityMap` -Zeichenfolge führt zu einer Fehlerantwort des Edge Networks, da die `primary` -Anzeige für die FPID fehlt. Mindestens eine der in `identityMap` vorhandenen IDs muss als `primary` markiert sein.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

Die vom Edge Network zurückgegebene Fehlerantwort ähnelt in diesem Fall der folgenden:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID-Hierarchie

Wenn sowohl eine ECID als auch eine FPID vorhanden sind, wird die ECID bei der Identifizierung des Benutzers priorisiert. Dadurch wird sichergestellt, dass eine vorhandene ECID im Browser-Cookie-Store weiterhin die primäre Kennung bleibt und die vorhandenen Besucherzahlen keine Auswirkungen haben. Für bestehende Benutzer wird die FPID erst dann zur primären Identität, wenn die ECID abläuft oder infolge einer Browserrichtlinie oder eines manuellen Prozesses gelöscht wird.

Identitäten werden in der folgenden Reihenfolge priorisiert:

1. In der `identityMap` enthaltene ECID
1. In einem Cookie gespeicherte ECID
1. In der `identityMap` enthaltene FPID
1. In einem Cookie gespeicherte FPID

## Migration zu Erstanbieter-Geräte-IDs

Wenn Sie zur Verwendung von FPIDs aus einer früheren Implementierung migrieren, ist es möglicherweise schwierig, sich vorzustellen, wie die Transition auf einer niedrigen Ebene aussehen könnte.

Um diesen Vorgang zu veranschaulichen, sollten Sie sich ein Szenario ansehen, an dem ein Kunde beteiligt ist, der Ihre Site bereits besucht hat, und welche Auswirkungen eine FPID-Migration auf die Identifizierung dieses Kunden in Adobe-Lösungen haben würde.

![Diagramm, das zeigt, wie die ID-Werte eines Kunden zwischen Besuchen nach der Migration zu FPIDs aktualisiert werden ](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Das `ECID` -Cookie wird immer priorisiert gegenüber dem `FPID`.

| Besuch | Beschreibung |
| --- | --- |
| Erster Besuch | Angenommen, Sie haben noch nicht mit dem Setzen des FPID-Cookies begonnen. Die im [AMCV-Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) enthaltene ECID ist die Kennung, mit der der Besucher identifiziert wird. |
| Zweiter Besuch | Der Rollout der Erstanbieter-Geräte-ID-Lösung wurde gestartet. Die vorhandene ECID ist weiterhin vorhanden und bleibt die primäre Kennung für die Besucheridentifizierung. |
| Dritter Besuch | Zwischen dem zweiten und dritten Besuch ist genügend Zeit vergangen, um die ECID aufgrund der Browserrichtlinie zu löschen. Da die FPID jedoch mithilfe eines DNS-A-Eintrags festgelegt wurde, bleibt die FPID bestehen. Die FPID wird jetzt als primäre ID betrachtet und zum Testen der ECID verwendet, die auf das Endbenutzergerät geschrieben wird. Der Benutzer wird nun als neuer Besucher in den Adobe Experience Platform- und Experience Cloud-Lösungen betrachtet. |
| Vierter Besuch | Zwischen dem dritten und vierten Besuch hat genügend Zeit verstrichen, dass die ECID aufgrund der Browserrichtlinie gelöscht wurde. Wie beim vorherigen Besuch bleibt die FPID aufgrund der Art und Weise, wie sie festgelegt wurde. Diesmal wird dieselbe ECID wie beim vorherigen Besuch generiert. Der Benutzer wird in den Experience Platform- und Experience Cloud-Lösungen als derselbe Benutzer wie beim vorherigen Besuch gesehen. |
| Fünfter Besuch | Zwischen dem vierten und fünften Besuch hat der Endbenutzer alle Cookies in seinem Browser gelöscht. Eine neue FPID wird generiert und zum Testen der Erstellung einer neuen ECID verwendet. Der Benutzer wird nun als neuer Besucher in den Adobe Experience Platform- und Experience Cloud-Lösungen betrachtet. |

{style="table-layout:auto"}

## Häufig gestellte Fragen

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Erstanbieter-Geräte-IDs.

### Inwiefern unterscheidet sich das Senden einer ID vom bloßen Generieren einer ID?

Das Sitzungskonzept ist insofern eindeutig, als die an Adobe Experience Cloud übergebene FPID mithilfe eines deterministischen Algorithmus in eine ECID konvertiert wird. Jedes Mal, wenn dieselbe FPID im Adobe Experience Platform-Edge Network gesendet wird, wird dieselbe ECID von der FPID gesendet.

### Wann sollte die Erstanbieter-Geräte-ID generiert werden?

Um die potenzielle Besucherinflation zu reduzieren, sollte die FPID generiert werden, bevor Sie Ihre erste Anfrage mit dem Web SDK stellen. Wenn Sie dies jedoch nicht tun können, wird für diesen Benutzer weiterhin eine ECID generiert und als primäre Kennung verwendet. Die generierte FPID wird erst dann zur primären Kennung, wenn die ECID nicht mehr vorhanden ist.

### Welche Datenerfassungsmethoden unterstützen Erstanbieter-Geräte-IDs?

Derzeit unterstützt nur das Web SDK FPIDs.

### Werden FPIDs in Platform- oder Experience Cloud-Lösungen gespeichert?

Sobald die FPID zum Testen einer ECID verwendet wurde, wird sie aus dem `identityMap` entfernt und durch die generierte ECID ersetzt. Die FPID wird nicht in Adobe Experience Platform- oder Experience Cloud-Lösungen gespeichert.
