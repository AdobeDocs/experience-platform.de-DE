---
title: Geheimnisse in der Reaktor-API
description: Erfahren Sie mehr über die Konfiguration von Geheimnissen in der Reaktor-API für die Verwendung in der Ereignis-Weiterleitung.
source-git-commit: 6822199c3ecf4414893a8b8dfc650e3da40a6470
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 3%

---

# Geheimnisse in der Reaktor-API

In der Reactor-API ist ein Geheimnis eine Ressource, die eine Authentifizierungsberechtigung darstellt. Geheimnisse werden bei der Weiterleitung von Ereignissen verwendet, um sich für den sicheren Datenaustausch an ein anderes System zu authentifizieren. Daher können Geheimnisse nur in Ereignis-Weiterleitungseigenschaften erstellt werden (Eigenschaften, deren Eigenschaften `platform` Attribut wurde festgelegt auf `edge`).

Es gibt derzeit drei unterstützte geheime Typen, die in der `type_of` Attribut:

| Geheimer Typ | Beschreibung |
| --- | --- |
| `token` | Eine einzelne Zeichenfolge aus Zeichen, die einen Authentifizierungstoken-Wert darstellt, der von beiden Systemen bekannt und verstanden wird. |
| `simple-http` | Enthält zwei Zeichenfolgenattribute für einen Benutzernamen und ein Kennwort. |
| `oauth2` | Enthält mehrere Attribute zur Unterstützung der [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) Authentifizierungsspezifikation. Ereignis Forwarding fragt Sie nach den erforderlichen Informationen und behandelt dann die Erneuerung dieser Token für Sie in einem bestimmten Intervall. |

{style=&quot;table-layout:auto&quot;}

Dieser Leitfaden bietet einen Überblick über die Konfiguration von Geheimnissen für die Verwendung in der Ereignis-Weiterleitung. Ausführliche Anleitungen zum Verwalten von Geheimnissen in der Reaktor-API, einschließlich Beispiel JSON der Struktur eines geheimen Geheims, finden Sie im [Secrets-Endpunkt-Leitfaden](../endpoints/secrets.md).

## Anmeldedaten

Jedes Geheimnis enthält `credentials` Attribut, das die entsprechenden Berechtigungswerte enthält. Jeder geheime Typ verfügt über verschiedene erforderliche Attribute, wie in den unten stehenden Abschnitten dargestellt.

### `token`

Geheimnisse mit `type_of` Wert von `token` nur ein einzelnes Attribut benötigen unter `credentials`:

| Berechtigungsattribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `token` | Zeichenfolge | Ein geheimes Token, das vom Zielsystem verstanden wird. |

{style=&quot;table-layout:auto&quot;}

Das Token wird als statischer Wert gespeichert, und daher ist der geheime Wert `expires_at` und `refresh_at` Eigenschaften sind festgelegt auf `null` wenn das Geheimnis erstellt wird.

### `simple-http`

Geheimnisse mit `type_of` Wert von `simple-http` die folgenden Attribute anfordern unter `credentials`:

| Berechtigungsattribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `username` | Zeichenfolge | Ein Benutzername. |
| `password` | Zeichenfolge | Ein Kennwort. Dieser Wert ist in der API-Antwort nicht enthalten. |

{style=&quot;table-layout:auto&quot;}

Wenn das Geheimnis erstellt wird, werden die beiden Attribute mit einer BASE64-Kodierung von `username:password`. Nach dem Austausch `expires_at` und `refresh_at` Eigenschaften sind festgelegt auf `null`.

### `oauth2`

>[!NOTE]
>
>Zurzeit gilt nur für [Art der Clientberechtigungen](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) wird für OAuth-Geheimnisse unterstützt.

Geheimnisse mit `type_of` Wert von `oauth2` die folgenden Attribute anfordern unter `credentials`:

| Berechtigungsattribut | Datentyp | Beschreibung |
| --- | --- | --- |
| `client_id` | Zeichenfolge | Die Client-ID für die OAuth-Integration. |
| `client_secret` | Zeichenfolge | Das Kundengeheimnis für die OAuth-Integration. Dieser Wert ist in der API-Antwort nicht enthalten. |
| `authorization_url` | Zeichenfolge | Die Autorisierungs-URL für die OAuth-Integration. |
| `refresh_offset` | Ganzzahl | *(Optional)* Der Wert (in Sekunden), um den der Aktualisierungsvorgang versetzt wird. Wenn dieses Attribut beim Erstellen des Geheimtitels ausgelassen wird, wird der Wert auf `14400` (standardmäßig vier Stunden). |
| `options` | Objekt | *(Optional)* Gibt zusätzliche Optionen für die OAuth-Integration an:<ul><li>`scope`: Eine Zeichenfolge, die die [OAuth 2.0-Anwendungsbereich](https://oauth.net/2/scope/) für die Anmeldedaten.</li><li>`audience`: Eine Zeichenfolge, die eine [Auth0-Zugriffstoken](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Wann ein `oauth2` geheim erstellt oder aktualisiert wird, `client_id` und `client_secret` (und gegebenenfalls `options`) in einer POST an die `authorization_url`, entsprechend dem Client Credits-Fluss des OAuth-Protokolls.

>[!NOTE]
>
>Es wird erwartet, dass die Stelle für die Antwort des Autorisierungsdienstes mit dem OAuth-Protokoll kompatibel ist.

Wenn der Autorisierungsdienst `200 OK` und einem JSON-Ansprechkörper, wird der Körper analysiert und `access_token` an die Umgebung der Kante geschoben wird und `expires_in` wird zur Berechnung der `expires_at` und `refresh_at` Attribute für das Geheimnis. Wenn es keine geheime Umgebung gibt, `access_token` wird verworfen.

Ein Austausch von Anmeldeinformationen gilt unter folgenden Bedingungen als erfolgreich:

* `expires_in` ist größer als `28800` (acht Stunden).
* `refresh_offset` kleiner als der Wert von `expires_in` minus `14400` (vier Stunden). Zum Beispiel, wenn `expires_in` ist `36000` (zehn Stunden) und `refresh_offset` ist `28800` (acht Stunden), wird der Austausch als fehlgeschlagen betrachtet, weil `28800` ist größer als `36000` - `14400` (`21600`).

Wenn der Austausch erfolgreich war, wird das Statusattribut des geheimen Geheims auf `succeeded` und Werte für `expires_at` und `refresh_at` eingestellt:

* `expires_at` ist die aktuelle UTC-Zeit plus der Wert von `expires_in`.
* `refresh_at` ist die aktuelle UTC-Zeit plus der Wert von `expires_in`, abzüglich des Werts von `refresh_offset`. Zum Beispiel, wenn `expires_in` ist `43200` (zwölf Stunden) und `refresh_offset` ist `14400` (vier Stunden), `refresh_at` Eigenschaft wurde auf `28800` (acht Stunden) nach der aktuellen UTC-Zeit.

Wenn die Börse aus irgendeinem Grund fehlschlägt, `status_details` im `meta` Objektaktualisierungen mit relevanten Informationen.

### Aktualisieren eines `oauth2` geheim

Wenn `oauth2` einer Umgebung geheim wurde und ihr Status `succeeded` (Die Anmeldedaten wurden erfolgreich ausgetauscht), wird ein neuer Austausch automatisch durchgeführt am `refresh_at`.

Wenn der Austausch erfolgreich ist, `refresh_status` im `meta` Objekt wurde eingestellt auf `succeeded` während `expires_at`, `refresh_at`und `activated_at` entsprechend aktualisiert werden.

Wenn der Austausch fehlschlägt, wird der Vorgang dreimal mit dem letzten Versuch versucht, nicht mehr als zwei Stunden vor Ablauf des Zugriffstokens. Wenn alle Versuche fehlschlagen, wird die `refresh_status_details` Attribut aus `meta` Objektaktualisierungen mit relevanten Details.

## Umgebung-Beziehung

Wenn Sie ein Geheimnis erstellen, müssen Sie Folgendes angeben: [Umgebung](../endpoints/environments.md) , in dem sie existieren wird. Geheimnisse werden sofort in der Umgebung bereitgestellt, in der sie erstellt werden.

Ein Geheimnis kann nur mit einer Umgebung verknüpft werden. Sobald die Beziehung zwischen einem Geheimnis und einer Umgebung hergestellt ist, kann das Geheimnis nicht mehr aus der Umgebung gelöscht werden und das Geheimnis kann nicht mit einer anderen Umgebung verknüpft werden.

>[!NOTE]
>
>Die einzige Ausnahme von dieser Regel besteht darin, dass die betreffende Umgebung gelöscht wird. In diesem Fall wird die Beziehung gelöscht und das Geheimnis kann einer anderen Umgebung zugewiesen werden.

Nachdem die Anmeldeinformationen eines geheimen geheimen Geheims erfolgreich ausgetauscht wurden, um ein Geheimnis mit einer Umgebung zu verknüpfen, das Exchange-Artefakt (die Token-Zeichenfolge für `token`, die Base64-kodierte Zeichenfolge für `simple-http`oder das Zugriffstoken für `oauth2`) ist sicher auf der Umgebung gespeichert.

Nachdem das Austauschartefakt erfolgreich auf der Umgebung gespeichert wurde, `activated_at` -Attribut auf die aktuelle UTC-Zeit eingestellt ist und kann nun mithilfe eines Datenelements referenziert werden. Siehe [nächster Abschnitt](#referencing-secrets) für weitere Informationen zum Bezug von Geheimnissen.

## Verweisende Geheimnisse {#referencing-secrets}

Um auf ein Geheimnis zu verweisen, müssen Sie ein Datenelement des Typs &quot;[!UICONTROL Geheimnis]&quot; (bereitgestellt von [[!UICONTROL Core] Erweiterung](../../extensions/web/core/overview.md)) auf einem Ereignis, das eine Eigenschaft weiterleitet. Bei der Konfiguration dieses Datenelements werden Sie aufgefordert, anzugeben, welches Geheimnis für jede Umgebung verwendet werden soll. Sie können dann Regeln erstellen, die auf ein geheimes Datenelement verweisen, z. B. im Header eines HTTP-Aufrufs.

![Geheimes Datenelement](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Um einer Bibliothek ein geheimes Datenelement hinzufügen zu können, müssen Sie mindestens ein Datenelement hinzufügen. `succeeded` geheim, das mit der Umgebung verknüpft ist, auf der die Bibliothek erstellt wird. Wenn eine Bibliothek beispielsweise ein geheimes Datenelement enthält, das nicht über ein `succeeded` geheim konfiguriert für [!UICONTROL Staging-Geheimnis] -Abschnitt, der versucht, diese Bibliothek in der Staging-Umgebung zu erstellen, führt zu einem Fehler.

Zur Laufzeit wird das Geheimdatenelement durch das entsprechende geheime Tauschobjekt ersetzt, das auf der Umgebung gespeichert ist.

## Nächste Schritte

Dieses Handbuch behandelt die Grundlagen der Arbeit mit Geheimnissen in der Reactor-API. Weitere Informationen zum Verwalten von Geheimnissen mithilfe von API-Aufrufen finden Sie im [Secrets-Endpunkt-Leitfaden](../endpoints/secrets.md).
