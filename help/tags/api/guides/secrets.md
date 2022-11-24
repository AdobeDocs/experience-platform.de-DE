---
title: Geheime Daten in der Reactor-API
description: Hier erfahren Sie mehr über die Grundlagen zum Konfigurieren von geheimen Daten in der Reactor-API für die Verwendung in der Ereignisweiterleitung.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 87%

---

# Geheime Daten in der Reactor-API

In der Reactor-API sind geheime Daten eine Ressource, die einen Authentifizierungsnachweis darstellt. Geheime Daten werden bei der Ereignisweiterleitung verwendet, um sich für einen sicheren Datenaustausch bei einem anderen System zu authentifizieren. Daher können geheime Daten nur in Ereignisweiterleitungs-Eigenschaften erstellt werden (Eigenschaften, deren `platform`-Attribut auf `edge` festgelegt ist).

Es gibt derzeit drei unterstützte Typen von geheimen Daten, die in dem Attribut `type_of` aufgeführt werden:

| Typ von geheimen Daten | Beschreibung |
| --- | --- |
| `token` | Eine einzelne Zeichenfolge, die den Wert eines Authentifizierungs-Tokens darstellt, der von beiden Systemen verstanden wird. |
| `simple-http` | Enthält zwei Zeichenfolgen-Attribute für einen Benutzernamen und ein Kennwort. |
| `oauth2-client_credentials` | Enthält mehrere Attribute zur Unterstützung der [OAuth](https://datatracker.ietf.org/doc/html/rfc6749)-Authentifizierungsspezifikation. Die Ereignisweiterleitung fragt Sie nach den erforderlichen Informationen und behandelt dann die Verlängerung dieser Token für Sie in einem bestimmten Intervall. |

{style=&quot;table-layout:auto&quot;}

Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie geheime Daten für die Verwendung in der Ereignisweiterleitung konfiguriert werden. Ausführliche Anleitungen zum Verwalten von geheimen Daten in der Reactor-API, einschließlich Beispiel-JSON der Struktur geheimer Daten, finden Sie im [Handbuch zum Secrets-Endpunkt](../endpoints/secrets.md).

## Anmeldeinformationen

Geheime Daten enthalten ein Attribut `credentials`, das die entsprechenden Werte der Anmeldeinformationen enthält. Wann [Erstellen eines Geheimnisses in der API](../endpoints/secrets.md#create), weist jeder geheime Typ verschiedene erforderliche Attribute auf, wie in den folgenden Abschnitten dargestellt:

* [`token`](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

Geheime Daten mit einem `type_of`-Wert von `token` erfordern nur ein einziges Attribut unter `credentials`:

| Anmeldeinformations-Attribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `token` | Zeichenfolge | Ein geheimes Token, das vom Zielsystem verstanden wird. |

{style=&quot;table-layout:auto&quot;}

Das Token wird als statischer Wert gespeichert, weswegen die Eigenschaften `expires_at` und `refresh_at` auf `null` festgelegt werden, wenn die geheimen Daten erstellt werden.

### `simple-http` {#simple-http}

Geheime Daten mit einem `type_of`-Wert von `simple-http` erfordern die folgenden Attribute unter `credentials`:

| Anmeldeinformations-Attribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `username` | Zeichenfolge | Ein Benutzername. |
| `password` | Zeichenfolge | Ein Kennwort. Dieser Wert ist nicht in der API-Antwort enthalten. |

{style=&quot;table-layout:auto&quot;}

Wenn die geheimen Daten erstellt werden, werden die beiden Attribute mit einer BASE64-Codierung von `username:password` ausgetauscht. Nach dem Austausch sind die Eigenschaften `expires_at` und `refresh_at` auf `null` festgelegt.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Geheime Daten mit einem `type_of`-Wert von `oauth2-client_credentials` erfordern die folgenden Attribute unter `credentials`:

| Anmeldeinformations-Attribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `client_id` | Zeichenfolge | Die Kunden-ID für die OAuth-Integration. |
| `client_secret` | Zeichenfolge | Die Kunden-seitigen geheimen Daten für die OAuth-Integration. Dieser Wert ist nicht in der API-Antwort enthalten. |
| `token_url` | Zeichenfolge | Die Autorisierungs-URL für die OAuth-Integration. |
| `refresh_offset` | Ganzzahl | *(Optional)* Der Wert in Sekunden, um den der Aktualisierungsvorgang versetzt wird. Wenn dieses Attribut beim Erstellen der geheimen Daten weggelassen wird, wird der Wert standardmäßig auf `14400` (4 Stunden) gesetzt. |
| `options` | Objekt | *(Optional)* Gibt zusätzliche Optionen für die OAuth-Integration an:<ul><li>`scope`: Eine Zeichenfolge, die den [OAuth 2.0-Gültigkeitsbereich](https://oauth.net/2/scope/) für die Anmeldeinformationen darstellt.</li><li>`audience`: Eine Zeichenfolge, die ein [Auth0-Zugriffstoken](https://auth0.com/docs/protocols/protocol-oauth2) darstellt.</li></ul> |

Wenn geheime Daten vom Typ `oauth2-client_credentials` erstellt oder aktualisiert werden, werden `client_id` und `client_secret` (und gegebenenfalls `options`) in einer POST-Anfrage an die `token_url` entsprechend dem Client-Anmeldedaten-Fluss des OAuth-Protokolls ausgetauscht.

>[!NOTE]
>
>Es wird erwartet, dass die Antwort des Autorisierungs-Services mit dem OAuth-Protokoll kompatibel ist.

Wenn der Autorisierungs-Service mit `200 OK` und einem JSON-Antworttext antwortet, wird der Text geparst, das `access_token` in die Edge-Umgebung verschoben und `expires_in` verwendet, um die Attribute `expires_at` und `refresh_at` für die geheimen Daten zu berechnen. Wenn keine Umgebungsverknüpfung für die geheimen Daten vorhanden ist, wird das `access_token` verworfen.

Ein Austausch von Anmeldeinformationen wird unter folgenden Bedingungen als erfolgreich betrachtet:

* `expires_in` ist größer als `28800` (acht Stunden).
* `refresh_offset` ist kleiner als der Wert von `expires_in` minus `14400` (vier Stunden). Wenn beispielsweise `expires_in` `36000` (zehn Stunden) ist und `refresh_offset` `28800` (acht Stunden), wird der Austausch als fehlgeschlagen betrachtet, weil `28800` größer als `36000` - `14400` (`21600`) ist.

Wenn der Austausch erfolgreich ist, wird das Statusattribut der geheimen Daten auf `succeeded` festgelegt und es werden zudem Werte für `expires_at` und `refresh_at` definiert:

* `expires_at` ist die aktuelle UTC-Zeit plus der Wert von `expires_in`.
* `refresh_at` ist die aktuelle UTC-Zeit plus der Wert von `expires_in` abzüglich des Werts von `refresh_offset`. Wenn beispielsweise `expires_in` `43200` (zwölf Stunden) ist und `refresh_offset` `14400` (vier Stunden), würde die Eigenschaft `refresh_at` auf `28800` (acht Stunden) nach der aktuellen UTC-Zeit festgelegt.

Wenn der Austausch aus irgendeinem Grund fehlschlägt, wird das Attribut `status_details` im Objekt `meta` mit relevanten Informationen aktualisiert.

#### Aktualisieren von geheimen Daten des Typs `oauth2-client_credentials`

Wenn geheime Daten des Typs `oauth2-client_credentials` einer Umgebung zugewiesen wurden und ihr Status `succeeded` (die Anmeldeinformationen wurden erfolgreich ausgetauscht) lautet, wird zum Zeitpunkt `refresh_at` automatisch ein neuer Austausch durchgeführt.

Wenn der Austausch erfolgreich ist, wird das Attribut `refresh_status` im Objekt `meta` auf `succeeded` festgelegt und `expires_at`, `refresh_at` und `activated_at` werden entsprechend aktualisiert.

Wenn der Austausch fehlschlägt, erfolgen drei weitere Versuche, den Vorgang auszuführen, wobei der letzte Versuch spätestens zwei Stunden vor Ablauf des Zugriffs-Tokens stattfindet. Wenn alle Versuche fehlschlagen, wird das Attribut `refresh_status_details` aus dem Objekt `meta` mit relevanten Details aktualisiert.

### `oauth2-google` {#oauth2-google}

Geheimnisse mit `type_of` Wert von `oauth2-google` erfordert das folgende Attribut unter `credentials`:

| Anmeldeinformations-Attribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `scopes` | Array | Listet die Google-Produktbereiche für die Authentifizierung auf. Die folgenden Bereiche werden unterstützt:<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google-Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Nach der Erstellung `oauth2-google` geheim ist, enthält die Antwort eine `meta.authorization_url` -Eigenschaft. Sie müssen diese URL kopieren und in einen Browser einfügen, um den Google-Authentifizierungsfluss abzuschließen.

#### Erneutes Autorisieren eines `oauth2-google` secret

Die Autorisierungs-URL für eine `oauth2-google` geheim läuft eine Stunde nach der Erstellung des Geheimnisses ab (wie durch `meta.authorization_url_expires_at`). Danach muss das Geheimnis erneut autorisiert werden, um den Authentifizierungsprozess zu verlängern.

Siehe Abschnitt [Endpunktleitfaden für Geheimnisse](../endpoints/secrets.md#reauthorize) für Details zur Neuautorisierung eines `oauth2-google` geheim durch eine PATCH-Anfrage an die Reactor-API.

## Umgebungsbeziehung

Beim Erstellen geheimer Daten müssen Sie die [Umgebung](../endpoints/environments.md) angeben, in der sie existieren werden. Geheime Daten werden sofort in der Umgebung bereitgestellt, in der sie erstellt werden.

Geheime Daten können jeweils nur mit einer Umgebung verknüpft werden. Sobald die Beziehung zwischen geheimen Daten und einer Umgebung hergestellt ist, können die geheimen Daten nicht mehr aus der Umgebung gelöscht werden und sie können nicht mit einer anderen Umgebung verknüpft werden.

>[!NOTE]
>
>Es gibt nur eine Ausnahme von dieser Regel, und zwar wenn die betreffende Umgebung gelöscht wird. In diesem Fall wird die Beziehung gelöscht und die geheimen Daten können einer anderen Umgebung zugewiesen werden.

Nachdem die Anmeldeinformationen von geheimen Daten erfolgreich ausgetauscht wurden, wird das Austausch-Artefakt (die Token-Zeichenfolge für `token`, der Base64-codierte String für `simple-http` oder das Zugriffs-Token für `oauth2-client_credentials`) sicher in der Umgebung gespeichert, um die geheimen Daten mit der Umgebung zu verknüpfen.

Nachdem das Austausch-Artefakt erfolgreich in der Umgebung gespeichert wurde, wird das Attribut `activated_at` der geheimen Daten auf die aktuelle UTC-Zeit festgelegt, sodass jetzt mithilfe eines Datenelements darauf verwiesen werden kann. Siehe den [nächsten Abschnitt](#referencing-secrets) mit weiteren Informationen zum Verweisen auf geheime Daten.

## Verweisen auf geheime Daten {#referencing-secrets}

Um auf geheime Daten zu verweisen, müssen Sie ein Datenelement des Typs [!UICONTROL Geheime Daten] (bereitgestellt von der [[!UICONTROL Core]-Erweiterung](../../extensions/client/core/overview.md)) in einer Ereignisweiterleitungs-Eigenschaft erstellen. Beim Konfigurieren dieses Datenelements werden Sie aufgefordert, anzugeben, welche geheimen Daten für jede Umgebung verwendet werden sollen. Anschließend können Sie Regeln erstellen, die auf ein Geheime-Daten-Datenelement verweisen, z. B. im Header für einen HTTP-Aufruf.

![Geheime-Daten-Datenelement](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Um ein Geheime-Daten-Datenelement zu einer Bibliothek hinzuzufügen, müssen Sie über schon über geheime Daten des Typs `succeeded` verfügen, die mit der Umgebung verknüpft sind, in der die Bibliothek erstellt wird. Wenn beispielsweise eine Bibliothek über ein Geheime-Daten-Datenelement verfügt, das keine geheimen Daten vom Typ `succeeded` für den Abschnitt [!UICONTROL Geheime Daten – Staging] hat, führt der Versuch, diese Bibliothek in der Staging-Umgebung zu erstellen, zu einem Fehler.

Zur Laufzeit wird das Geheime-Daten-Datenelement durch das entsprechende Geheime-Daten-Austausch-Artefakt ersetzt, das in der Umgebung gespeichert ist.

## Nächste Schritte

In diesem Handbuch wurden die Grundlagen für die Arbeit mit geheimen Daten in der Reactor-API behandelt. Weitere Informationen zum Verwalten von geheimen Daten mithilfe von API-Aufrufen finden Sie im [Handbuch zum Secrets-Endpunkt](../endpoints/secrets.md).
