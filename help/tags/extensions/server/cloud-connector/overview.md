---
title: Cloud Connector-Erweiterung – Übersicht
description: Erfahren Sie mehr über die Cloud Connector-Ereignisweiterleitungserweiterung in Adobe Experience Platform.
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 100%

---

# Cloud Connector-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Mit der Cloud Connector-Ereignisweiterleitungserweiterung können Sie benutzerdefinierte HTTP-Anfragen erstellen, um Daten an ein Ziel zu senden oder Daten von einem Ziel abzurufen. Die Cloud Connector-Erweiterung ist wie Postman für das Adobe Experience Platform Edge Network und kann verwendet werden, um Daten an einen Endpunkt zu senden, der noch keine dedizierte Erweiterung hat.

Verwenden Sie diese Referenz, um Informationen zu den verfügbaren Optionen beim Erstellen einer Regel mithilfe dieser Erweiterung zu erhalten.

## Aktionstyp der Cloud Connector-Erweiterung

In diesem Abschnitt wird der Aktionstyp „Daten senden“ beschrieben, der in der Adobe Experience Platform Cloud Connector-Erweiterung verfügbar ist.

### Anfragetyp

Zur Auswahl des für den Endpunkt erforderlichen Anfragetyps wählen Sie den entsprechenden Typ in der Dropdown-Liste [!UICONTROL Anfragetyp] aus.

| Methode | Beschreibung |
|---|---|
| [GET](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Methods/GET) | Fordert eine Darstellung der angegebenen Ressource an. GET-Anforderungen sollten Daten nur abrufen. |
| [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) | Sendet eine Entität an die angegebene Ressource, was häufig zu Zustandsänderungen oder Nebeneffekten auf dem Server führt. |
| [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) | Ersetzt alle aktuellen Darstellungen der Zielressource durch die Anforderungsnutzdaten. |
| [PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) | Nimmt partielle Änderungen an einer Ressource vor. |
| [DELETE](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Methods/DELETE) | Löscht die angegebene Ressource. |

### Endpunkt-URL

Geben Sie in das Textfeld neben dem Dropdown-Menü „Anfragetyp“ die URL für den Endpunkt ein, an den Sie Daten senden möchten.

### Konfiguration der Abfrageparameter, Header und Nachrichtenkörper

Verwenden Sie die einzelnen Registerkarten (Abfrageparameter, Header und Nachrichtenkörper-Datenelemente), um zu steuern, welche Daten an einen bestimmten Endpunkt gesendet werden.

#### Abfrageparameter

Definieren Sie einen Schlüssel und einen Wert für jedes Schlüssel-Wert-Paar, das Sie als Abfragezeichenfolge-Parameter senden möchten. Um ein Datenelement manuell einzugeben, verwenden Sie die Datenelement-Tokenisierung für die Ereignisweiterleitung mit geschweiften Klammern. Um auf den Wert eines Datenelements mit dem Namen „siteSection“ als Schlüssel oder Wert zu verweisen, geben Sie `{{siteSection}}` ein. Sie können auch das zuvor erstellte Datenelement wählen, indem Sie es im Dropdown-Menü auswählen.

Um weitere Abfrageparameter hinzuzufügen, wählen Sie **[!UICONTROL Weitere hinzufügen]** aus.

#### Header

Definieren Sie einen Schlüssel und einen Wert für jedes Schlüssel-Wert-Paar, das Sie als Header senden möchten. Um ein Datenelement manuell einzugeben, verwenden Sie die Datenelement-Tokenisierung für die Ereignisweiterleitung mit geschweiften Klammern. Um auf den Wert eines Datenelements mit dem Namen „pageName“ als Schlüssel oder Wert zu verweisen, geben Sie `{{pageName}}` ein. Sie können auch das zuvor erstellte Datenelement wählen, indem Sie es im Dropdown-Menü auswählen.

Um weitere Header hinzuzufügen, wählen Sie **[!UICONTROL Weitere hinzufügen]** aus.

In der folgenden Tabelle sind die vordefinierten Header aufgeführt. Sie sind nicht auf diese Header beschränkt und können bei Bedarf eigene benutzerdefinierte Header hinzufügen. Diese stehen jedoch als Unterstützung zur Verfügung.

>[!NOTE]
>
>Weitere Informationen zu diesen Headern finden Sie unter [https://developer.mozilla.org/de/docs/Web/HTTP/Headers](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers).

| Header | Beschreibung |
|---|---|
| [A-IM](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Accept) |  |
| [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Accept-Charset](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Charset) |  |
| [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) |  |
| [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) |  |
| [Accept-Datetime](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) | Wird von einem Benutzeragenten zur Angabe übertragen, dass er auf einen früheren Zustand einer Originalressource zugreifen möchte. Zu diesem Zweck wird der `Accept-Datetime`-Header in einer HTTP-Anfrage an ein TimeGate für eine ursprüngliche Ressource übermittelt. Der Wert gibt den Zeitpunkt des gewünschten früheren Zustands der Originalressource an. |
| Access-Control-Request-Headers | Wird von Browsern bei einer [Preflight-Anfrage](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request) verwendet, um dem Server mitzuteilen, welche [HTTP-Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) der Client bei der eigentlichen Anfrage senden könnte. |
| Access-Control-Request-Method | Wird von Browsern bei einer [Preflight-Anfrage](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request) verwendet, um dem Server mitzuteilen, welche [HTTP-Methode](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Methods) bei der eigentlichen Anfrage verwendet wird. Dieser Header ist erforderlich, da die Preflight-Anfrage immer eine [OPTION](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) ist und nicht dieselbe Methode wie die eigentliche Anfrage verwendet. |
| Authorization | Enthält die Anmeldeinformationen zum Authentifizieren eines Benutzeragenten bei einem Server. |
| [Cache-Control](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Cache-Control) | Anweisungen für Caching-Mechanismen sowohl in Anfragen als auch in Antworten. |
| [Verbindung](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Connection) | Steuert, ob die Netzwerkverbindung nach Abschluss der aktuellen Transaktion geöffnet bleibt. |
| [Content-Length](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Length) | Die Größe der Ressource in Bytes als Dezimalzahl. |
| [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) | Gibt den Medientyp der Ressource an. |
| Cookie | Enthält gespeicherte [HTTP-Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies), die zuvor vom Server mit dem [`Set-Cookie`](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Set-Cookie)-Header gesendet wurden. |
| Datum | Der allgemeine HTTP-Header enthält das Datum und die Uhrzeit, wann die Nachricht ursprünglich gesendet wurde. |
| [DNT](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/DNT) | Gibt die Tracking-Präferenz des Benutzers an. |
| Expect | Gibt Erwartungen an, die vom Server erfüllt werden müssen, um die Anfrage ordnungsgemäß zu verarbeiten. |
| Forwarded | Enthält Informationen von den [Reverse-Proxy-Servern](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling), die verändert werden oder verloren gehen, wenn ein Proxy am Pfad der Anfrage beteiligt ist. |
| Aus | Enthält eine Internet-E-Mail-Adresse für einen menschlichen Benutzer, der den anfragenden Benutzeragenten steuert. |
| Host | Gibt den Host und die Port-Nummer des Servers an, an den die Anfrage gesendet wird. |
| If-Match |  |
| If-Modified-Since |  |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) |  |
| [If-Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) |  |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) |  |
| [Pragma](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma) | Implementierungsspezifischer Header, der an jeder Stelle der Anfrage-Antwort-Kette verschiedene Effekte haben kann. Wird für Abwärtskompatibilität mit HTTP/1.0-Caches verwendet, bei denen der Cache-Control-Header noch nicht vorhanden ist. |  |
| [Proxy-Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Bereich](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | Gibt den Teil eines Dokuments an, der vom Server zurückgegeben werden soll. |  |
| [Referrer](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Referer) | Die Adresse der vorherigen Web-Seite, von der einem Link zur aktuell angeforderten Seite gefolgt wurde. |  |
| TE | Gibt die Übertragungskodierungen an, die der Benutzeragent akzeptiert. (Sie könnten es informell `Accept-Transfer-Encoding` nennen, was intuitiver wäre). |
| Upgrade | Das relevante RFC-Dokument für das [`Upgrade`-Header-Feld ist RFC 7230, Abschnitt 6.7](https://tools.ietf.org/html/rfc7230#section-6.7). Der Standard legt Regeln für die Aktualisierung oder den Wechsel zu einem anderen Protokoll in der aktuellen Client-, Server- und Transportprotokollverbindung fest. Dieser Header-Standard ermöglicht es beispielsweise einem Client, von HTTP 1.1 zu HTTP 2.0 zu wechseln, vorausgesetzt, der Server entscheidet, das `Upgrade`-Header-Feld zu bestätigen und zu implementieren. Keine der Parteien muss die im `Upgrade`-Header-Feld angegebenen Bedingungen akzeptieren. Es kann sowohl in Client- als auch in Server-Headern verwendet werden. Wenn das `Upgrade`-Header-Feld angegeben ist, MUSS der Absender auch das `Connection`-Header-Feld mit der `upgrade`-Option senden. |  |
| [User-Agent](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/User-Agent) | Enthält eine charakteristische Zeichenfolge, die es den Netzwerkprotokoll-Peers ermöglicht, den Programmtyp, das Betriebssystem, den Software-Hersteller oder die Software-Version des anfragenden Software-Benutzeragenten zu identifizieren. |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | Wird von Proxies hinzugefügt, sowohl von Forward- als auch von Reverse-Proxies, und kann in den Anfrage-Headern und in den Antwort-Headern vorhanden sein. |
| [Warnung](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | Allgemeine Warnhinweise zu möglichen Problemen. |
| X-CSRF-Token |  |
| X-Requested-With |  |

#### Nachrichtenkörper als JSON

Definieren Sie einen Schlüssel und einen Wert für jedes Schlüssel-Wert-Paar, das Sie im Nachrichtenkörper der Anfrage senden möchten. Um ein Datenelement manuell einzugeben, verwenden Sie die Datenelement-Tokenisierung für die Ereignisweiterleitung mit geschweiften Klammern. Um auf den Wert eines Datenelements mit dem Namen „appSection“ als Schlüssel oder Wert zu verweisen, geben Sie `{{appSection}}` ein. Sie können auch das zuvor erstellte Datenelement wählen, indem Sie es im Dropdown-Menü auswählen.

Um weitere Schlüssel-Wert-Paare hinzuzufügen, wählen Sie **[!UICONTROL Weitere hinzufügen]** aus.

#### Nachrichtenkörper als Rohtext

Definieren Sie einen Schlüssel und einen Wert für jedes Schlüssel-Wert-Paar, das Sie im Nachrichtenkörper der Anfrage senden möchten. Um ein Datenelement manuell einzugeben, verwenden Sie die Datenelement-Tokenisierung für die Ereignisweiterleitung mit geschweiften Klammern. Um auf den Wert eines Datenelements mit dem Namen „appSection“ als Schlüssel oder Wert zu verweisen, geben Sie `{{appSection}}` ein. Sie können auch das zuvor erstellte Datenelement wählen, indem Sie es im Dropdown-Menü auswählen. Sie können ein oder mehrere Datenelemente hinzufügen.

### Erweitert

Aktionen innerhalb von Regeln in der Ereignisweiterleitung werden sequenziell ausgeführt. In bestimmten Szenarien möchten Sie aber womöglich Daten von einer externen Quelle abrufen, die nicht im vom Client eingehenden Ereignis vorhanden ist, um im Rahmen einer einzelnen Regel die in dieser Antwort enthaltenen Daten entweder umzuwandeln oder an ein in einer nachfolgenden Aktion enthaltenes endgültiges Ziel zu senden. Die Option „Save the request response“ (Anfrageantwort speichern) im Bereich „Advanced“ (Erweitert) ermöglicht dies.

Um den von einem Endpunkt erhaltenen Antworttext zu speichern, aktivieren Sie das Kontrollkästchen **[!UICONTROL Anfrageantwort speichern]** und legen Sie im Textfeld einen Antwortschlüssel fest.

Wenn Sie den Antwortschlüssel als `productDetails` festgelegt haben, verweisen Sie in einem Datenelement auf diese Daten sowie in einer nachfolgenden Aktion innerhalb derselben Regel auf dieses Datenelement. Um ein Datenelement zu erstellen, das auf `productDetail` verweist, erstellen Sie ein Datenelement vom Typ `path` und geben Sie den folgenden Pfad ein:

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
