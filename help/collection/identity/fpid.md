---
title: Verwenden von First-Party-Geräte-IDs in der Datenerfassung
description: Konfigurieren Sie First-Party-Geräte-IDs (FPIDs) für eine dauerhafte Identität in Web-Implementierungen, die Daten an die Edge Network senden.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Verwenden von First-Party-Geräte-IDs in der Datenerfassung

Experience Platform Edge Network verwendet Experience Cloud-IDs (ECIDs) zur Identifizierung von Website-Besuchern. Um die Dauerhaftigkeit der Identität in eigenen Eigenschaften zu verbessern, können Sie Ihre eigenen Geräte-IDs festlegen und verwalten, die als First-Party-Geräte-IDs (FPIDs) bezeichnet werden. Der Edge Network verwendet den FPID zum Seed der ECID, die Adobe-Lösungen verwenden.

Auf dieser Seite wird davon ausgegangen, dass Sie mit ECIDs und `identityMap` vertraut sind. Weitere Informationen [&#x200B; Sie unter „Identität &#x200B;](./overview.md) Datenerfassung“.

## Verwendung von FPIDs {#when-to-use}

Browser-Einschränkungen können die Lebensdauer von Cookies verkürzen, die Adobe verwendet, um wiederkehrende Besucher zu erkennen. Wenn Sie eine dauerhaftere Identität auf Sites benötigen, die Ihrem Unternehmen gehören und von ihm kontrolliert werden, können Sie mit FPIDs Ihre eigene Geräte-ID verwalten und diese zum Seed der ECID verwenden.

FPIDs werden für Web-Implementierungen unterstützt, die die Web-SDK verwenden, einschließlich der Tag-Erweiterung „Web SDK&quot;. Sie eignen sich optimal, wenn Ihr Hauptziel eine stärkere Identitätspersistenz in Domains ist, die Ihrem Unternehmen gehören, oder wenn Sie eine bessere Kontinuität für das Reporting und die Personalisierung in eigenen Web-Eigenschaften wünschen. Sie ermöglichen es Ihnen auch, ein Erstanbieter-Cookie in der von Ihnen kontrollierten Infrastruktur festzulegen und zu verwalten.

FPIDs sind nicht das richtige Tool, wenn Ihr Hauptziel die Übergabe von einer App an das Web oder die Identitätskontinuität über mehrere Domains hinweg ist. Für diese Szenarien siehe [Freigabe von Identitäten zwischen Mobilgeräten &#x200B;](./mobile-to-web.md) Web und [Domain-übergreifende Freigabe](./cross-domain-sharing.md).

Vorteile der Verwendung von FPIDs:

* Stärkere Persistenz auf eigenen Eigenschaften.
* Mehr Kontrolle darüber, wie die Gerätekennung generiert und verwaltet wird.
* Eine dauerhafte Grundlage für Analysen und Personalisierung.

Zu den Nachteilen der Verwendung von FPIDs gehören:

* Mehr Implementierungsverantwortung als sich auf das standardmäßige Identitätsverhalten zu verlassen.
* Koordination Ihrer Server-seitigen Cookie-Logik und Datenerfassungskonfiguration.
* Zusätzliche Validierung zur Bestätigung, dass die Kennung erwartungsgemäß verwendet wird.

### Pfad für allgemeine Einrichtung

1. Generieren und Verwalten einer First-Party-Geräte-ID in der von Ihnen verwalteten Infrastruktur.
1. Konfigurieren Sie Ihre Implementierung so, dass diese ID entweder aus einem [Erstanbieter-Cookie](#setting-cookie-datastreams) oder aus der [Identitäts-Payload](#identityMap) gelesen wird.
1. Überprüfen Sie, ob wiederkehrende Besucher über einen längeren Zeitraum eine konsistente Identität in Ihren eigenen Eigenschaften behalten.

## Funktionsweise von FPIDs {#how-fpids-work}

Die an Adobe Experience Cloud übergebene FPID wird mithilfe eines deterministischen Algorithmus in eine ECID konvertiert. Jedes Mal, wenn derselbe FPID an den Edge Network gesendet wird, wird dieselbe ECID vom FPID vorgegeben. Nachdem der FPID zum Seed einer ECID verwendet wurde, wird er aus der `identityMap` gelöscht und durch die generierte ECID ersetzt. Die FPID wird nicht in Adobe Experience Platform- oder Experience Cloud-Lösungen gespeichert.

Wenn sowohl eine ECID als auch eine FPID vorhanden ist, wird die ECID immer zuerst zur Identifizierung des Benutzers verwendet. Durch diese Priorisierung wird sichergestellt, dass eine vorhandene ECID im Browser-Cookie-Store als primäre Kennung beibehalten wird und die Anzahl vorhandener Besucher kein Inflationsrisiko darstellt. Für bestehende Benutzer wird die FPID erst dann zur primären Identität, wenn die ECID abläuft oder infolge einer Browser-Richtlinie oder manuellen Aktion gelöscht wird.

Identitäten werden in der folgenden Reihenfolge priorisiert:

1. In der `identityMap` enthaltene ECID
1. In einem Cookie gespeicherte ECID
1. In der `identityMap` enthaltene FPID
1. In einem Cookie gespeicherte FPID

## Generieren und Festlegen des FPID-Cookies {#set-fpid-cookie}

Die Edge Network akzeptiert nur IDs, die dem [UUIDv4-Format](https://datatracker.ietf.org/doc/html/rfc4122) entsprechen. Geräte-IDs, die nicht im UUIDv4-Format vorliegen, werden abgelehnt.

* UUIDs sind eindeutig und zufällig, mit einer vernachlässigbaren Wahrscheinlichkeit einer Kollision.
* UUIDv4 kann nicht mit IP-Adressen oder anderen persönlich identifizierbaren Informationen (PII) vorab gesendet werden.
* Bibliotheken zum Generieren von UUIDs stehen für jede Programmiersprache zur Verfügung.

### Server-seitige Cookie-Einstellung {#set-cookie-server}

Wenn Sie ein Cookie über Ihren eigenen Server setzen, können Sie verschiedene Methoden verwenden, um zu verhindern, dass das Cookie durch Browser-Richtlinien eingeschränkt wird:

* Generieren von Cookies mithilfe von Server-seitigen Skriptsprachen
* Setzen von Cookies als Reaktion auf eine API-Anfrage an eine Subdomain oder einen anderen Endpunkt auf der Website
* Generieren von Cookies mithilfe eines Content-Management-Systems (CMS)
* Generieren von Cookies mithilfe eines Content Delivery Network (CDN)

Erstanbieter-Cookies sind am effektivsten, wenn sie mit einem Server gesetzt werden, der einen DNS-[A-Eintrag](https://datatracker.ietf.org/doc/html/rfc1035) (für IPv4) oder [AAAA-Eintrag](https://datatracker.ietf.org/doc/html/rfc3596) (für IPv6) im Gegensatz zu einem DNS-`CNAME` oder JavaScript-Code verwendet.

>[!IMPORTANT]
>
>Cookies, die mit der `document.cookie`-Methode von JavaScript festgelegt werden (einschließlich der Verwendung der Tag-Methode [`cookie.set()`](../tags/cookie.md)), sind fast nie vor Browser-Richtlinien geschützt, die die Cookie-Dauer beschränken.

Beachten Sie, dass `A` oder `AAAA` Datensätze nur für das Setzen und Tracking von Cookies unterstützt werden. Die primäre Methode zur Datenerfassung erfolgt über eine DNS-`CNAME`. FPIDs werden mithilfe eines `A`- oder `AAAA`-Datensatzes festgelegt und mithilfe eines `CNAME` an Adobe gesendet. Mit dem Adobe-Managed Certificate Program [&#x200B; Sie eine &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de#adobe-managed-certificate-program) für die Datenerfassung konfigurieren.`CNAME`

### Wann das Cookie gesetzt werden soll {#when-to-set-cookie}

Das FPID-Cookie wird idealerweise gesetzt, bevor Daten an die Edge Network gesendet werden. Wenn Ihre Implementierung vor der Datenerfassung ein Einverständnis erfordert, finden Sie unter [Einverständnis mit First-Party-Geräte-IDs](./consent.md#consent-with-fpids) Anleitungen zur Koordinierung des FPID-Cookies mit Ihrem Einverständnisfluss. Die Besucherinflation wird reduziert, wenn Sie sicherstellen, dass der FPID verfügbar ist, um die ECID aus der ersten Anfrage zu testen. In Szenarien, in denen dies nicht möglich ist, wird weiterhin eine ECID mit vorhandenen Methoden generiert und fungiert als primäre Kennung, solange das Cookie vorhanden ist. Die generierte FPID wird erst dann zur primären Kennung, wenn die ECID nicht mehr vorhanden ist. Wenn die ECID letztendlich von einer Browser-Löschrichtlinie betroffen ist, der FPID jedoch nicht, wird die FPID beim nächsten Besuch zur primären Kennung und wird verwendet, um die ECID bei jedem nachfolgenden Besuch zu testen.

### Festlegen des Ablaufs {#set-expiration}

Adobe empfiehlt, die Lebensdauer Ihres FPID-Cookies sorgfältig zu prüfen. Achten Sie darauf, dass Sie die Datenschutzrichtlinien Ihrer Organisation zusammen mit den Gesetzen und Richtlinien der Länder oder Regionen, in denen Ihre Organisation tätig ist, berücksichtigen. Je nach Einrichtung Ihres Unternehmens können Sie eine unternehmensweite Cookie-Richtlinie oder eine Richtlinie einführen, die für Benutzende in jedem Gebietsschema, in dem Sie tätig sind, variiert. Stellen Sie unabhängig vom anfänglichen Cookie-Ablauf sicher, dass Sie eine Logik verwenden, die den Ablauf jedes Mal verlängert, wenn ein neuer Site-Besuch stattfindet.

### Cookie-Flags {#cookie-flags}

Es gibt mehrere Cookie-Flags, die sich darauf auswirken, wie Cookies in verschiedenen Browsern behandelt werden:

* **`HTTPOnly`**: Auf Cookies, die mit dem `HTTPOnly`-Flag gesetzt werden, kann nicht über Client-seitige Skripte zugegriffen werden. Wenn Sie also beim Festlegen des FPID ein `HTTPOnly`-Flag festlegen, müssen Sie eine Server-seitige Skriptsprache verwenden, um den Cookie-Wert zur Aufnahme in das `identityMap` zu lesen. Wenn Sie möchten, dass der Edge Network den Wert des FPID-Cookies liest, wird durch das Festlegen des `HTTPOnly`-Flags sichergestellt, dass der Zugriff auf den Wert durch Client-seitige Skripte nicht möglich ist, aber die Fähigkeit des Edge Network, das Cookie zu lesen, nicht beeinträchtigt. Die Verwendung des `HTTPOnly`-Flags hat keine Auswirkungen auf Cookie-Richtlinien, die die Cookie-Lebensdauer einschränken können. Es ist jedoch immer noch zu beachten, wenn Sie den Wert der FPID festlegen und lesen.
* **`Secure`**: Cookies, die mit dem `Secure`-Attribut gesetzt werden, werden nur mit einer verschlüsselten Anforderung über das HTTPS-Protokoll an den Server gesendet. Mit dieser Markierung können Sie sicherstellen, dass für Man-in-the-Middle-Angreifer kein einfacher Zugriff auf den Cookie-Wert möglich ist. Wenn möglich, ist es immer eine gute Idee, die `Secure` Flag zu setzen.
* **`SameSite`**: Mit dem Attribut `SameSite` können Server bestimmen, ob Cookies mit Site-übergreifenden Anfragen gesendet werden. Das -Attribut bietet einen gewissen Schutz vor Cross-Site-Forgery-Angriffen. Es gibt drei mögliche Werte: `Strict`, `Lax` und `None`. Besprechen Sie mit Ihrem internen Team, welche Einstellung für Ihr Unternehmen am besten geeignet ist. Wenn kein `SameSite`-Attribut angegeben ist, ist die Standardeinstellung für einige Browser `SameSite=Lax`.

## FPID an Edge Network senden {#send-fpid}

Sie können FPIDs auf zwei Arten an Edge Network senden:

* **[Methode 1](#setting-cookie-datastreams)**: Konfigurieren Sie eine `CNAME` für Ihre Web-SDK-Aufrufe und nehmen Sie den Namen Ihres FPID-Cookies in Ihre Datenstromkonfiguration auf.
* **[Methode 2](#identityMap)**: FPID in die Identitätszuordnung einschließen.

### Methode 1: Konfigurieren eines `CNAME` und Festlegen eines Erstanbieter-ID-Cookies in Ihrem Datenstrom {#setting-cookie-datastreams}

Um ein FPID-Cookie in Ihrer eigenen Domain einzurichten, müssen Sie Ihre eigenen `CNAME` für Ihre Web-SDK-Aufrufe konfigurieren und dann die First-Party-ID-Cookie-Funktion in Ihrer Datenstromkonfiguration aktivieren. Mit einem `CNAME`-Eintrag in Ihrem DNS können Sie einen Alias von einem Domain-Namen zu einem anderen erstellen. Dieser Alias kann dazu beitragen, dass Drittanbieterdienste so aussehen, als wären sie Teil Ihrer eigenen Domain, sodass ihre Cookies wie Erstanbieter-Cookies aussehen. Wenn die Erstanbieter-Datenerfassung mithilfe eines `CNAME` aktiviert ist, werden alle Cookies für Ihre Domain bei Anfragen an den Datenerfassungsendpunkt gesendet.

1. Arbeiten Sie mit Adobe zusammen, um einen `CNAME` Datensatz für die Datenerfassung in Ihrem Unternehmen zu erstellen. Den vollständigen Prozess finden Sie unter &lbrace;0[&#x200B; Adobe-verwaltetes Zertifikatprogramm .](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/adobe-managed-cert)
1. Aktivieren Sie die Option **[!UICONTROL First Party ID Cookie]** in Ihrem Datenstrom. Diese Einstellung weist Edge Network an, beim Suchen nach einer First-Party-Geräte-ID das angegebene Cookie zu verwenden, anstatt nach dem Wert in der Identitätszuordnung zu suchen. Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die FPID gespeichert ist. Weitere [&#x200B; finden Sie unter „Erstellen und Konfigurieren &#x200B;](/help/datastreams/configure.md#advanced-options) Datenströmen“.

   ![Platform-UI-Bild mit der Datenstromkonfiguration, in der die First-Party-ID-Cookie-Einstellung hervorgehoben ist](/help/collection/js/assets/first-party-id-datastreams.png)

### Methode 2: Verwenden von FPIDs in `identityMap` {#identityMap}

Als Alternative zum Speichern der FPID in Ihrem eigenen Cookie können Sie die FPID über die Identitätszuordnung an die Edge Network senden.

Im Folgenden finden Sie ein Beispiel dafür, wie Sie eine FPID in der `identityMap` festlegen:

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

Wie bei anderen Identitätstypen können Sie die FPID mit anderen Identitäten in `identityMap` einbeziehen. Das folgende Beispiel enthält die FPID mit einer authentifizierten CRM-ID:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Wenn der FPID in einem Cookie enthalten ist, das von der Edge Network gelesen wird, wenn die Erstanbieter-Datenerfassung aktiviert ist, erfassen Sie nur die authentifizierte CRM-ID:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Die folgende `identityMap` führt zu einer Fehlerantwort von Edge Network, da ihr der `primary` für den FPID fehlt. Mindestens eine der in `identityMap` vorhandenen IDs muss als `primary` gekennzeichnet sein.

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migration zu FPIDs {#migrating-to-fpid}

Wenn Sie von einer früheren Implementierung zu Erstanbieter-Geräte-IDs migrieren, kann es schwierig sein, sich ein Bild davon zu machen, wie die Transition auf niedriger Ebene aussehen könnte. Zur Veranschaulichung dieses Prozesses sollten Sie sich ein Szenario ansehen, in dem ein Kunde involviert ist, der bereits Ihre Site besucht hat, und welche Auswirkungen eine FPID-Migration auf die Art und Weise hätte, wie dieser Kunde in Adobe-Lösungen identifiziert wird.

![Diagramm, das zeigt, wie die ID-Werte eines Kunden zwischen Besuchen nach der Migration zu FPIDs aktualisiert werden](/help/collection/js/assets/identity/tracking/visits.png)

| Besuch | Beschreibung |
| --- | --- |
| Erster Besuch | Angenommen, Sie haben noch nicht mit dem Setzen des FPID-Cookies begonnen. Die im -AMCV[Cookie enthaltene ECID &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=de#section-c55af54828dc4cce89f6118655d694c8) die Kennung, die zur Identifizierung des Besuchers verwendet wird. |
| Zweiter Besuch | Der Rollout der FPID-Lösung hat begonnen. Die vorhandene ECID ist weiterhin vorhanden und bleibt die primäre Kennung zur Besucheridentifizierung. |
| Dritter Besuch | Zwischen dem zweiten und dem dritten Besuch ist ausreichend Zeit verstrichen, um die ECID aufgrund der Browser-Richtlinie zu löschen. Da die FPID jedoch mithilfe eines DNS-`A`-Eintrags festgelegt wurde, bleibt die FPID bestehen. Die FPID wird jetzt als primäre ID betrachtet und zum Seed der ECID verwendet, die auf das Endbenutzergerät geschrieben wird. Der Benutzer wird jetzt als neuer Besucher in Adobe Experience Platform- und Experience Cloud-Lösungen betrachtet. |
| Vierter Besuch | Zwischen dem dritten und vierten Besuch ist ausreichend Zeit verstrichen, um die ECID aufgrund der Browser-Richtlinie zu löschen. Wie beim vorherigen Besuch bleibt die FPID aufgrund der Art und Weise, wie sie festgelegt wurde, bestehen. Diesmal wird dieselbe ECID wie beim vorherigen Besuch generiert. Der Benutzer wird in allen Adobe Experience Platform- und Experience Cloud-Lösungen als derselbe Benutzer angezeigt wie der vorherige Besuch. |
| Fünfter Besuch | Zwischen dem vierten und fünften Besuch hat der Endbenutzer alle Cookies im Browser gelöscht. Eine neue FPID wird generiert und verwendet, um die Erstellung einer neuen ECID zu starten. Der Benutzer wird jetzt als neuer Besucher in Adobe Experience Platform- und Experience Cloud-Lösungen betrachtet. |
