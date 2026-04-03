---
title: Fehlerbehebung bei Identitäten in der Datenerfassung
description: Diagnostizieren Sie häufige Identitätsprobleme in Web SDK-Implementierungen, einschließlich Besucherzuwachs, ECID-Inkonsistenzen, Cookie-Konflikte und FPID-Problemen.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Fehlerbehebung bei Identitäten in der Datenerfassung

Identitätsprobleme treten häufig eher als Symptome in nachgelagerten Berichten (überhöhte Besucherzahlen, fragmentierte Profile oder fehlerhafte Personalisierung) denn als Fehler in der Implementierung selbst auf. Auf dieser Seite können Sie die häufigsten Identitätsprobleme in Web SDK-Implementierungen diagnostizieren und beheben. Hintergrundinformationen zur Funktionsweise von Identitäten in der Datenerfassung finden Sie unter [Identitätsübersicht](./overview.md).

## Prüfen von Identitätswerten {#inspect-identity}

Bevor Sie ein bestimmtes Problem beheben, rufen Sie die aktuellen Identitätswerte ab, die von der Web-SDK verwendet werden. Verwenden Sie den [`getIdentity`](/help/collection/js/commands/getidentity.md)-Befehl, um die ECID und andere Identitätssignale anzuzeigen:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

Sie können auch Identitätswerte in den Entwickler-Tools Ihres Browsers überprüfen:

1. Öffnen Sie die Registerkarte **Anwendung** (Chrome/Edge) oder **Speicher** (Firefox/Safari).
2. Suchen Sie nach Cookies mit dem Präfix `kndctr_` in Ihrer Domain. Das `kndctr_<ORG_ID>_AdobeOrg_identity`-Cookie enthält die ECID.
3. Öffnen Sie die Registerkarte **Netzwerk** und suchen Sie eine `interact`- oder `collect`-Anfrage an Edge Network. Überprüfen Sie die Anfrage-Payload auf `identityMap` und die Antwort-Payload auf Identitäts-Handles.

## Häufige Probleme {#common-issues}

+++**Inflation der Besucherzahlen**

**Symptom**: Analytics-Berichte zeigen mehr Unique Visitors als erwartet an oder dieselbe Person wird sitzungsübergreifend als mehrere Besucher angezeigt.

**Mögliche**:

| Ursache | Anleitung zur Identifizierung | Lösung |
| --- | --- | --- |
| Kurze Cookie-Lebensdauer | Überprüfen Sie den Ablauf `kndctr_` Cookies im Browser. Wenn sie in 7 Tagen oder weniger ablaufen, schränken Browser-Richtlinien wahrscheinlich die Cookie-Dauer ein. | Implementieren Sie [Erstanbieter-Geräte-IDs (FPIDs](./fpid.md), die von einem Server mithilfe eines DNS-A/AAAA-Eintrags festgelegt werden, um eine längere Cookie-Persistenz zu gewährleisten. |
| Fehlende FPID bei erster Anfrage | Überprüfen Sie die erste Edge Network-Anfrage beim Laden der Seite. Wenn kein FPID-Cookie vorhanden ist, generiert Edge Network eine neue ECID. Wenn die FPID nach der ersten Anfrage festgelegt wird, wird die für diese erste Anfrage generierte ECID verwaist. | Setzen Sie das FPID-Cookie, bevor Web SDK seine erste Anforderung sendet. Siehe [Wann wird das Cookie gesetzt](./fpid.md#when-to-set-cookie). |
| `orgId` nicht übereinstimmender Domains | Vergleichen Sie den `orgId` Konfigurationswert über Ihre Domains hinweg. Nicht übereinstimmende Werte führen zu separaten Identitätsbereichen. | Verwenden Sie denselben [`orgId`](/help/collection/js/commands/configure/orgid.md) auf allen Domains innerhalb Ihrer Organisation. |
| Einverständnisbanner Löschen von Cookies | Wenn Ihre Einwilligungsimplementierung alle Cookies löscht, bevor das Einverständnis erteilt wird, und dann die Web-SDK initialisiert wird, wird eine neue ECID generiert. | Konfigurieren Sie Ihr Einverständnisbanner, um `kndctr_` Cookies beizubehalten oder die Web SDK-Initialisierung zu verzögern, bis das Einverständnis eingeholt wurde. Siehe auch [Zustimmung und Identität](./consent.md). |
| Von JavaScript festgelegte FPID-Cookies | Cookies, die mit `document.cookie` gesetzt werden, unterliegen Browser-Einschränkungen (ITP, ETP), die ihre Lebensdauer begrenzen, manchmal auf bis zu 24 Stunden. | Setzen Sie FPID-Cookies vom Server mithilfe eines DNS-A/AAAA-Eintrags, nicht von JavaScript. |

+++

+++**ECID ändert sich zwischen Seiten unerwartet**

**Problem**: Die ECID unterscheidet sich auf verschiedenen Seiten derselben Domain oder ändert sich beim Laden jeder Seite.

**Diagnoseschritte**:

1. Vergewissern Sie sich, dass das `kndctr_` Identitäts-Cookie auf beiden Seiten vorhanden ist. Wenn er auf einer Seite fehlt, überprüfen Sie, ob die Web-SDK auf dieser Seite konfiguriert ist.
2. Stellen Sie sicher, dass die Cookie-Domain breit genug eingestellt ist. Ein auf `shop.example.com` festgelegtes Cookie ist auf `www.example.com` nicht verfügbar. Stellen Sie sicher, dass die Erstanbieter-Infrastruktur für die Erfassung und das Setzen von Cookies denselben Domain-Bereich verwenden.
3. Suchen Sie nach JavaScript, das Cookies bei der Navigation löscht (z. B. aggressive Cookie-Einverständnisskripte oder Datenschutz-Tools).
4. Wenn Sie ein Einzelseitenprogramm verwenden, stellen Sie sicher, dass der Web-SDK einmal bei der App-Initialisierung konfiguriert und nicht bei jeder Routenänderung neu initialisiert ist. Bei der erneuten Initialisierung kann eine neue ECID generiert werden.

+++

+++**FPID sendet die ECID nicht**

**Symptom**: Sie haben ein FPID-Cookie gesetzt, aber `getIdentity` gibt eine ECID zurück, die über alle Besuche hinweg nicht konsistent ist, oder die FPID wird nicht in den Payloads von Edge Network-Anfragen angezeigt.

**Diagnoseschritte**:

1. **Überprüfen des FPID-Cookie** Formats: Die FPID muss eine gültige [UUIDv4“ &#x200B;](https://datatracker.ietf.org/doc/html/rfc4122). Öffnen Sie die Entwickler-Tools Ihres Browsers, suchen Sie das FPID-Cookie und überprüfen Sie, ob der Wert mit dem Muster `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx` übereinstimmt.
2. **Überprüfen Sie den Cookie-Namen im Datenstrom**: Wenn Sie die [Datenstrom-Cookie-Methode](./fpid.md#setting-cookie-datastreams) verwenden, muss der im Datenstrom konfigurierte Cookie-Name genau mit dem Namen des Cookies übereinstimmen, das Ihr Server setzt.
3. **Vergewissern Sie sich, dass das Cookie bei der Anfrage gesendet wird**: Überprüfen Sie auf der Registerkarte „Netzwerk“ die `Cookie` der Edge Network-Anfrage. Das FPID-Cookie muss enthalten sein.
4. **Identitätspriorität überprüfen**: Wenn eine vorhandene ECID bereits in einem `kndctr_` Cookie gespeichert ist, hat sie Vorrang vor der FPID. Der FPID übergibt nur dann eine neue ECID, wenn keine vorhandene ECID vorhanden ist. Siehe [Funktionsweise von FPIDs](./fpid.md#how-fpids-work) für die vollständige Prioritätsreihenfolge.
5. **Validieren des CNAME**: Wenn Sie die Datenstrom-Cookie-Methode verwenden, stellen Sie sicher, dass der Erstanbieter-Sammlungs-CNAME korrekt konfiguriert ist und dass Anfragen über ihn weitergeleitet werden.

+++

+++**Domain-übergreifende Identität funktioniert nicht**

**Symptom**: Ein Besucher, der von einer Ihrer Domains auf eine andere klickt, wird als neuer Besucher auf der Ziel-Domain behandelt.

**Diagnoseschritte**:

1. **URL überprüfen** Überprüfen Sie die Ziel-URL, wenn der Besucher auf den Link klickt. Sie muss einen `adobe_mc` Abfragezeichenfolgenparameter enthalten. Wenn der Parameter fehlt, hängt die Quell-Domain ihn nicht an. Siehe [Implementieren der domänenübergreifenden Freigabe](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Überprüfen Sie die Zeitplanung**: Der `adobe_mc` läuft nach fünf Minuten ab. Wenn das Laden der Zielseite zu lange dauert (z. B. aufgrund von Umleitungen oder einem langsamen Netzwerk), kann der -Parameter ablaufen, bevor die Web-SDK ihn lesen kann.
3. **`orgId` Übereinstimmung überprüfen**: Beide Domains müssen denselben [`orgId`](/help/collection/js/commands/configure/orgid.md) verwenden. Nicht übereinstimmende Organisations-IDs führen dazu, dass die Ziel-Domain die weitergegebene Identität ablehnt.
4. **Bestätigen, dass sich Web SDK am Ziel befindet**: Auf der Zielseite muss Web SDK installiert und konfiguriert sein. Ohne dies wird der `adobe_mc` ignoriert.
5. **URL-Stripping**: Einige Umleitungs-Services, CDNs oder Server-seitige Logik entfernen unbekannte Abfragezeichenfolgen-Parameter. Stellen Sie sicher, dass `adobe_mc` alle Umleitungen zwischen Quell- und Zielseite überlebt.

+++

+++**Handoff von Mobile-zu-Web-Identität schlägt fehl**

**Symptom**: Ein Besucher, der in der Mobile App beginnt und einen WebView- oder mobilen Browser öffnet, wird auf der Web-Seite als neuer Besucher behandelt.

**Diagnoseschritte**:

1. **URL überprüfen**: Die an die WebView übergebene URL protokollieren. Sie muss einen von `adobe_mc`[`getUrlVariables` generierten &#x200B;](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) enthalten.
2. **SDK-Versionen überprüfen**: Die Mobile Identity for Edge Network-Erweiterung muss Version 1.1.0 oder höher und die Web-SDK muss Version 2.11.0 oder höher sein.
3. **Überprüfen Sie das Timing**: Wie bei der Domain-übergreifenden Freigabe läuft der `adobe_mc` nach fünf Minuten ab. Stellen Sie sicher, dass der WebView sofort nach dem Erstellen der URL geladen wird.
4. **`orgId` Übereinstimmung bestätigen**: Die Experience Cloud-Organisations-ID muss sowohl in der mobilen SDK- als auch in der Web-SDK-Konfiguration identisch sein.

+++
