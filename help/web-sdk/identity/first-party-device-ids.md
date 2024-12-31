---
title: IDs von Erstanbieter-Geräten in Web SDK
description: Erfahren Sie, wie Sie First-Party-Geräte-IDs (FPIDs) in der Adobe Experience Platform Web SDK konfigurieren.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 04ef39cbfc614369cb15f4d947474b491c34ef33
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 0%

---


# IDs von Erstanbieter-Geräten in Web SDK

Adobe Experience Platform Web SDK weist Website-Besuchern mithilfe von Cookies [Adobe Experience Cloud-IDs (ECIDs](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=de) zu, um das Benutzerverhalten zu verfolgen. Um Browser-Einschränkungen hinsichtlich der Cookie-Lebensdauer zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Diese werden als First-Party-Geräte-IDs (`FPIDs`) bezeichnet.

>[!NOTE]
>
>Die Unterstützung von Erstanbieter-Geräte-IDs ist nur verfügbar, wenn Daten über die Web-SDK an das Experience Platform-Edge Network gesendet werden.

>[!IMPORTANT]
>
>IDs von Erstanbieter-Geräten sind nicht mit der Funktion [Drittanbieter-Cookies](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK kompatibel.
>Sie können entweder Erstanbieter-Geräte-IDs verwenden oder Drittanbieter-Cookies verwenden. Sie können jedoch nicht beide Funktionen gleichzeitig verwenden.

In diesem Dokument wird erläutert, wie Erstanbieter-Geräte-IDs für Ihre Web SDK-Implementierung konfiguriert werden.

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie mit der Funktionsweise von Identitätsdaten für Platform Web SDK vertraut sind, einschließlich der Rolle von ECIDs und `identityMap`. Weitere Informationen finden Sie in der Übersicht [Identitätsdaten in der Web](./overview.md)SDK) .

## Verwenden von First-Party-Geräte-IDs (FPIDs) {#using-fpid}

Erstanbieter-Geräte-IDs ([!DNL FPIDs]) verfolgen Besucher mithilfe von Erstanbieter-Cookies. Erstanbieter-Cookies sind am effektivsten, wenn sie mit einem Server gesetzt werden, der einen DNS-[A-Eintrag](https://datatracker.ietf.org/doc/html/rfc1035) (für IPv4) oder [AAAA-Eintrag](https://datatracker.ietf.org/doc/html/rfc3596) (für IPv6) im Gegensatz zu einem DNS-[!DNL CNAME] oder [!DNL JavaScript]-Code verwendet.

>[!IMPORTANT]
>
>[!DNL A]- oder [!DNL AAAA] werden nur für das Setzen und Tracking von Cookies unterstützt. Die primäre Methode zur Datenerfassung erfolgt über eine [!DNL DNS] [!DNL CNAME]. Mit anderen Worten: [!DNL FPIDs] werden mit einem [!DNL A] oder [!DNL AAAA] Datensatz festgelegt und dann mit einem [!DNL CNAME] an Adobe gesendet.
>
>Das [Adobe-Managed Certificate Program](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) wird weiterhin für die Erstanbieter-Datenerfassung unterstützt.

Sobald ein [!DNL FPID] Cookie gesetzt wurde, kann sein Wert abgerufen und bei der Erfassung von Ereignisdaten an Adobe gesendet werden. Die erfassten [!DNL FPIDs] werden als Testadressen verwendet, um [!DNL ECIDs] zu generieren, die weiterhin die primären IDs in Adobe Experience Cloud-Programmen sind.

Um eine [!DNL FPID] für einen Website-Besucher an das Edge Network zu senden, müssen Sie die [!DNL FPID] in die `identityMap` für diesen Besucher einschließen. Weitere Informationen finden Sie im Abschnitt weiter unten in diesem Dokument [Verwenden von FPIDs in `identityMap`](#identityMap).

### Formatierungsanforderungen für First-Party-Geräte-IDs {#formatting-requirements}

Das Edge Network akzeptiert nur [!DNL IDs], die dem Format [UUIDv4“ ](https://datatracker.ietf.org/doc/html/rfc4122). Geräte-IDs, die nicht im [!DNL UUIDv4] Format vorliegen, werden abgelehnt.

Die Erstellung einer [!DNL UUID] führt fast immer zu einer eindeutigen, zufälligen ID, wobei die Wahrscheinlichkeit, dass eine Kollision auftritt, vernachlässigbar ist. [!DNL UUIDv4] können nicht mit IP-Adressen oder anderen personenbezogenen Daten ([!DNL PII]) gesendet werden. [!DNL UUIDs] sind allgegenwärtig und Bibliotheken können für praktisch jede Programmiersprache gefunden werden, um sie zu erzeugen.

## Festlegen eines Erstanbieter-ID-Cookies in der Datenstrom-Benutzeroberfläche {#setting-cookie-datastreams}

Sie können einen Cookie-Namen in der Datenstrom-Benutzeroberfläche angeben, in dem sich der [!DNL FPID] befinden kann, anstatt den Cookie-Wert lesen und den [!DNL FPID] in die Identitätszuordnung einschließen zu müssen.

>[!IMPORTANT]
>
>Für diese Funktion muss [ Erstanbieter-Datenerfassung aktiviert ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en).

Siehe [Dokumentation zu Datenströmen](../../datastreams/configure.md) für detaillierte Informationen zur Konfiguration eines Datenstroms.

Aktivieren Sie beim Konfigurieren Ihres Datenstroms die Option **[!UICONTROL Erstanbieter-ID-Cookie]** . Diese Einstellung weist das Edge Network an, bei der Suche nach einer First-Party-Geräte-ID ein bestimmtes Cookie zu verwenden, anstatt nach diesem Wert in der [Identitätszuordnung](#identityMap).

Weitere Informationen zur Funktionsweise [ Erstanbieter-Cookies finden ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) in der Dokumentation zu Adobe Experience Cloud .

![Platform-UI-Bild mit der Datenstromkonfiguration, in der die First-Party-ID-Cookie-Einstellung hervorgehoben ist](../assets/first-party-id-datastreams.png)

Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die ID gespeichert ist.

Wenn Sie Erstanbieter-IDs verwenden, können Sie keine ID-Synchronisierungen von Drittanbietern durchführen. ID-Synchronisierungen von Drittanbietern basieren auf dem [!DNL Visitor ID]-Service und den von diesem Service generierten `UUID`. Bei Verwendung der ID-Funktion von Erstanbietern wird die [!DNL ECID] ohne Verwendung des [!DNL Visitor ID]-Service generiert, was die Synchronisierung von Drittanbieter-IDs unmöglich macht.

Wenn Sie Erstanbieter-IDs verwenden, werden [Audience Manager ](https://experienceleague.adobe.com/en/docs/audience-manager)-Funktionen, die auf die Aktivierung in Partnerplattformen abzielen, nicht unterstützt, da die Synchronisierung der Audience Manager-Partner-IDs größtenteils auf `UUIDs` oder `DIDs` basiert. Die von einer Erstanbieter-ID abgeleitete [!DNL ECID] ist nicht mit einer `UUID` verknüpft, sodass sie nicht adressierbar ist.

## Setzen eines Cookies mit Ihrem eigenen Server {#set-cookie-server}

Beim Setzen eines Cookies mit einem Server, dessen Eigentümer Sie sind, können Sie verschiedene Methoden verwenden, um zu verhindern, dass das Cookie aufgrund von Browser-Richtlinien eingeschränkt wird:

* Generieren von Cookies mithilfe von Server-seitigen Skriptsprachen
* Setzen von Cookies als Reaktion auf eine API-Anfrage an eine Subdomain oder einen anderen Endpunkt auf der Website
* Generieren von Cookies mithilfe eines [!DNL CMS]
* Generieren von Cookies mithilfe eines [!DNL CDN]

>[!IMPORTANT]
>
>Cookies, die mit der `document.cookie`-Methode von JavaScript gesetzt werden, sind fast nie vor Browser-Richtlinien geschützt, die die Cookie-Dauer beschränken.

### Wann das Cookie gesetzt werden soll {#when-to-set-cookie}

Das [!DNL FPID]-Cookie sollte idealerweise gesetzt werden, bevor Anfragen an das Edge Network gesendet werden. In Fällen, in denen dies nicht möglich ist, wird jedoch weiterhin ein [!DNL ECID] mit vorhandenen Methoden generiert und fungiert als primäre Kennung, solange das Cookie vorhanden ist.

Angenommen, die [!DNL ECID] ist letztendlich von einer Browser-Löschrichtlinie betroffen, die [!DNL FPID] jedoch nicht, wird die [!DNL FPID] beim nächsten Besuch zur primären Kennung und wird zum Seed der [!DNL ECID] bei jedem nachfolgenden Besuch verwendet.

### Einstellen des Ablaufs für das Cookie {#set-expiration}

Das Setzen des Ablaufs eines Cookies sollte bei der Implementierung der [!DNL FPID] sorgfältig berücksichtigt werden. Bei der Entscheidung sollten Sie die Länder oder Regionen berücksichtigen, in denen Ihre Organisation tätig ist, sowie die Gesetze und Richtlinien in jeder dieser Regionen.

Im Rahmen dieser Entscheidung sollten Sie möglicherweise eine unternehmensweite Cookie-Setzungsrichtlinie oder eine Richtlinie einführen, die für die Benutzer in jedem Gebietsschema, in dem Sie tätig sind, variiert.

Unabhängig von der Einstellung, die Sie für den anfänglichen Ablauf eines Cookies auswählen, müssen Sie sicherstellen, dass Sie eine Logik einschließen, die den Ablauf des Cookies jedes Mal verlängert, wenn eine neue Website besucht wird.

## Auswirkungen von Cookie-Flags {#cookie-flag-impact}

Es gibt verschiedene Cookie-Flags, die sich darauf auswirken, wie Cookies in verschiedenen Browsern behandelt werden:

* [`HTTPOnly`](#http-only)
* [`Sicher`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Auf Cookies, die mit dem `HTTPOnly`-Flag gesetzt werden, kann nicht über Client-seitige Skripte zugegriffen werden. Wenn Sie also beim Festlegen der [!DNL FPID] ein `HTTPOnly`-Flag festlegen, müssen Sie eine Server-seitige Skriptsprache verwenden, um den Cookie-Wert zur Aufnahme in die `identityMap` zu lesen.

Wenn Sie möchten, dass das Edge Network den Wert des [!DNL FPID] Cookies liest, wird durch das Setzen des `HTTPOnly`-Flags sichergestellt, dass Client-seitige Skripte nicht auf den Wert zugreifen können, jedoch keine negativen Auswirkungen auf die Fähigkeit des Edge Networks haben, das Cookie zu lesen.

>[!NOTE]
>
>Die Verwendung des `HTTPOnly`-Flags hat keine Auswirkungen auf die Cookie-Richtlinien, die die Cookie-Lebensdauer einschränken können. Sie sollten dies jedoch berücksichtigen, wenn Sie den Wert der [!DNL FPID] festlegen und lesen.

### `Secure` {#secure}

Cookies, die mit dem `Secure`-Attribut gesetzt werden, werden nur mit einer verschlüsselten Anfrage über das [!DNL HTTPS]-Protokoll an den Server gesendet. Die Verwendung dieser Markierung kann sicherstellen, dass für Man-in-the-Middle-Angreifer kein einfacher Zugriff auf den Wert des Cookies möglich ist. Wenn möglich, ist es immer eine gute Idee, die `Secure` Flag zu setzen.

### `SameSite` {#same-site}

Mit dem Attribut `SameSite` können Server bestimmen, ob Cookies mit Site-übergreifenden Anfragen gesendet werden. Das -Attribut bietet einen gewissen Schutz vor Cross-Site-Forgery-Angriffen. Es gibt drei mögliche Werte: `Strict`, `Lax` und `None`. Besprechen Sie mit Ihrem internen Team, welche Einstellung für Ihr Unternehmen am besten geeignet ist.

Wenn kein `SameSite`-Attribut angegeben ist, ist die Standardeinstellung für einige Browser jetzt `SameSite=Lax`.

## Verwenden von FPIDs in `identityMap` {#identityMap}

Im Folgenden finden Sie ein Beispiel dafür, wie Sie ein [!DNL FPID] im `identityMap` festlegen:

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

Wie bei anderen Identitätstypen können Sie die [!DNL FPID] mit anderen Identitäten in `identityMap` einbeziehen. Im Folgenden finden Sie ein Beispiel für die [!DNL FPID], die in einem authentifizierten [!DNL CRM ID] enthalten sind:

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Wenn die [!DNL FPID] in einem Cookie enthalten ist, das vom Edge Network gelesen wird, wenn die Erstanbieter-Datenerfassung aktiviert ist, sollten Sie nur die authentifizierten [!DNL CRM ID] erfassen:

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

Das folgende `identityMap` würde zu einer Fehlerantwort des Edge Networks führen, da es nicht den `primary` für die [!DNL FPID] enthält. Mindestens eine der in `identityMap` vorhandenen IDs muss als `primary` markiert sein.

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

Die vom Edge Network zurückgegebene Fehlerantwort würde in diesem Fall der folgenden ähneln:

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

## Festlegen einer FPID in Ihrer eigenen Domain {#setting-fpid-domain}

Sie können nicht nur den [!DNL FPID] in der Identitätszuordnung festlegen, sondern auch das [!DNL FPID]-Cookie in Ihrer eigenen Domain, wenn Sie eine Erstanbieter-Datenerfassung konfiguriert [!DNL CNAME].

Wenn die Erstanbieter-Datenerfassung mithilfe eines [!DNL CNAME] aktiviert ist, werden alle Cookies für Ihre Domain bei Anfragen an den Datenerfassungsendpunkt gesendet.

Alle Cookies, die für die Datenerfassung der Adobe nicht relevant sind, werden gelöscht. Sie können [!DNL FPID] den Namen des [!DNL FPID]-Cookies in der Datenstromkonfiguration angeben. In diesem Fall liest das Edge Network den Inhalt des [!DNL FPID]-Cookies, anstatt nach dem [!DNL FPID] in der Identitätszuordnung zu suchen.

Um diese Funktion verwenden zu können, müssen Sie die [!DNL FPID] auf der obersten Ebene Ihrer Domain anstatt einer bestimmten Subdomain festlegen. Wenn Sie ihn für eine Subdomain festlegen, wird der Cookie-Wert nicht an das Edge Network gesendet und die [!DNL FPID] Lösung funktioniert nicht wie beabsichtigt.

## ID-Hierarchie {#id-hierarchy}

Wenn sowohl ein [!DNL ECID] als auch ein [!DNL FPID] vorhanden sind, wird der [!DNL ECID] bei der Identifizierung des Benutzers priorisiert. Dadurch wird sichergestellt, dass eine vorhandene [!DNL ECID] im Browser-Cookie-Speicher vorhanden ist, die primäre Kennung bleibt und die Anzahl vorhandener Besucher nicht beeinträchtigt wird. Für bestehende Benutzer wird die [!DNL FPID] erst dann zur primären Identität, wenn die [!DNL ECID] abläuft oder als Ergebnis einer Browser-Richtlinie oder eines manuellen Prozesses gelöscht wird.

Identitäten werden in der folgenden Reihenfolge priorisiert:

1. In der `identityMap` enthaltene [!DNL ECID]
1. In einem Cookie gespeicherte [!DNL ECID]
1. In der `identityMap` enthaltene [!DNL FPID]
1. In einem Cookie gespeicherte [!DNL FPID]

## Migrieren zu First-Party-Geräte-IDs {#migrating-to-fpid}

Wenn Sie von einer früheren Implementierung zu Erstanbieter-Geräte-IDs migrieren, kann es schwierig sein, sich ein Bild davon zu machen, wie die Transition auf niedriger Ebene aussehen könnte.

Zur Veranschaulichung dieses Prozesses sollten Sie sich ein Szenario ansehen, in dem ein Kunde involviert ist, der bereits Ihre Site besucht hat, und welche Auswirkungen eine [!DNL FPID] auf die Art und Weise hätte, wie dieser Kunde in Adobe-Lösungen identifiziert wird.

![Diagramm, das zeigt, wie die ID-Werte eines Kunden zwischen Besuchen nach der Migration zu FPIDs aktualisiert werden](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Das `ECID`-Cookie hat immer Vorrang vor dem `FPID`.

| Besuch | Beschreibung |
| --- | --- |
| Erster Besuch | Angenommen, Sie haben noch nicht mit dem Setzen des [!DNL FPID]-Cookies begonnen. Die im [AMCV-Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) enthaltene [!DNL ECID] ist die Kennung, die zur Identifizierung des Besuchers verwendet wird. |
| Zweiter Besuch | Der Rollout der [!DNL FPID] Lösung hat begonnen. Die vorhandene [!DNL ECID] ist noch vorhanden und bleibt die primäre Kennung zur Besucheridentifizierung. |
| Dritter Besuch | Zwischen dem zweiten und dem dritten Besuch ist ausreichend Zeit verstrichen, um die [!DNL ECID] aufgrund der Browser-Richtlinie zu löschen. Da die [!DNL FPID] jedoch mit einem [!DNL DNS] [!DNL A]-Eintrag festgelegt wurde, bleibt die [!DNL FPID] bestehen. Die [!DNL FPID] wird jetzt als primäre ID betrachtet und zum Testen der [!DNL ECID] verwendet, die auf das Endbenutzergerät geschrieben wird. Der Benutzer wird jetzt als neuer Besucher in den Lösungen Adobe Experience Platform und Experience Cloud betrachtet. |
| Vierter Besuch | Zwischen dem dritten und vierten Besuch ist ausreichend Zeit verstrichen, um die [!DNL ECID] aufgrund der Browser-Richtlinie zu löschen. Wie beim vorherigen Besuch bleibt die [!DNL FPID] aufgrund der Art und Weise, wie sie festgelegt wurde, bestehen. Diesmal wird derselbe [!DNL ECID] wie beim vorherigen Besuch generiert. Der Benutzer wird in allen Experience Platform- und Experience Cloud-Lösungen als derselbe Benutzer wie beim vorherigen Besuch angezeigt. |
| Fünfter Besuch | Zwischen dem vierten und fünften Besuch hat der Endbenutzer alle Cookies in seinem Browser gelöscht. Ein neues [!DNL FPID] wird generiert und verwendet, um die Erstellung eines neuen [!DNL ECID] zu beschleunigen. Der Benutzer wird jetzt als neuer Besucher in den Lösungen Adobe Experience Platform und Experience Cloud betrachtet. |

{style="table-layout:auto"}

## Häufig gestellte Fragen {#faq}

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Erstanbieter-Geräte-IDs.

### Inwiefern unterscheidet sich das Seeding einer ID vom einfachen Generieren einer ID?

Das Seeding-Konzept ist insofern einzigartig, als die an Adobe Experience Cloud übergebene [!DNL FPID] mithilfe eines deterministischen Algorithmus in eine [!DNL ECID] konvertiert wird. Jedes Mal, wenn derselbe [!DNL FPID] an das Edge Network gesendet wird, wird derselbe [!DNL ECID] vom [!DNL FPID] gesendet.

### Wann soll die First-Party-Geräte-ID generiert werden?

Um die mögliche Besucherinflation zu reduzieren, sollte die [!DNL FPID] vor der ersten Anfrage mit dem Web SDK generiert werden. Wenn Sie dies nicht tun können, wird dennoch eine [!DNL ECID] für diesen Benutzer generiert und als primäre Kennung verwendet. Die generierte [!DNL FPID] wird erst dann zur primären Kennung, wenn die [!DNL ECID] nicht mehr vorhanden ist.

### Welche Datenerfassungsmethoden unterstützen First-Party-Geräte-IDs?

Derzeit unterstützt nur Web SDK IDs von Erstanbieter-Geräten.

### Werden First-Party-Geräte-IDs auf beliebigen Platform- oder Experience Cloud-Lösungen gespeichert?

Nachdem der [!DNL FPID] zum Seed eines [!DNL ECID] verwendet wurde, wird er aus dem `identityMap` gelöscht und durch den generierten [!DNL ECID] ersetzt. Das [!DNL FPID] wird in keiner Adobe Experience Platform- oder Experience Cloud-Lösung gespeichert.
