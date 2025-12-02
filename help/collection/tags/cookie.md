---
title: Cookie
description: Manuelles Schreiben, Bearbeiten oder Löschen von Cookies für die Tag-Eigenschaft.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

Das `_satellite.cookie`-Objekt enthält Methoden, mit denen Sie Cookies schreiben, bearbeiten oder löschen können, auf die Ihre Tag-Regeln verweisen können. Es handelt sich dabei um eine Teilkopie von [`js-cookie`](https://github.com/js-cookie/js-cookie), die viele Kernfunktionen dieser Bibliothek enthält.

## `cookie.set()`

Die `set()`-Methode schreibt ein Cookie, auf das Ihre Tag-Eigenschaft verweisen kann.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Die folgenden Methodenparameter sind verfügbar:

| Name | Typ | Erforderlich | Beschreibung |
|---|---|---|---|
| **`name`** | `string` | Ja | Der Name des Cookies. |
| **`value`** | `string` | Ja | Der Wert des Cookies |
| **`attributes`** | `object` | Nein | Zusätzliche Attribute, die das Cookie enthalten soll. |

Das `attributes`-Objekt unterstützt die folgenden Eigenschaften:

| Attributname | Typ | Erforderlich | Standard | Beschreibung |
|---|---|---|---|---|
| **`expires`** | `number` oder [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | Nein | Cookie läuft am Ende der Browser-Sitzung ab | Die Anzahl der Tage, die das Cookie ablaufen soll. |
| **`path`** | `string` | Nein | Website-weit sichtbares Cookie | Wo in Ihrer Domain das Cookie sichtbar ist. |
| **`domain`** | `string` | Nein | Cookie sichtbar für Domain, unter der es erstellt wurde | Eine gültige Domain (mit oder ohne Subdomain), in der das Cookie sichtbar ist. Wenn eine Domain ohne Subdomain enthalten ist, ist das Cookie für alle Subdomains unter dieser Domain sichtbar. |
| **`secure`** | `boolean` | Nein | Kein Attribut festgelegt | Bestimmt, ob das Cookie ein sicheres Protokoll erfordert (`https://`). Wenn dies weggelassen wird, gibt es keine sichere Protokollanforderung. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | Nein | Kein Attribut festgelegt | Hier können Sie das [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value)-Attribut eines Cookies festlegen. Wenn Sie `sameSite` auf `None` setzen, müssen Sie auch `secure` auf `true` setzen. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Der Aufruf dieser Methode schreibt das gewünschte Cookie und gibt die serialisierte Cookie-Zeichenfolge zurück, die geschrieben wurde. Diese Zeichenfolge wird hauptsächlich zum Debuggen oder zur Protokollierung verwendet.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Frühere Versionen des Tag-Objekts `_satellite.setCookie()` verwendet. Die `setCookie()` Methode ist zugunsten von `_satellite.cookie.set()` veraltet.

## `cookie.get()`

Die `get()` Methode gibt einen Cookie-Wert zurück.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Name | Typ | Erforderlich | Beschreibung |
|---|---|---|---|
| **`name`** | `string` | Ja | Der Cookie-Name, von dem Sie den Wert abrufen möchten (unter Berücksichtigung der Groß-/Kleinschreibung). |

Gibt den Cookie-Wert zurück, wenn der Cookie-Name vorhanden ist. Wenn der Cookie-Name nicht vorhanden ist, gibt `undefined` zurück.

>[!TIP]
>
>Frühere Versionen des Tag-Objekts `_satellite.getCookie()` verwendet. Die `getCookie()` Methode ist zugunsten von `_satellite.cookie.get()` veraltet.

## `cookie.remove()`

Die `remove()` Methode löscht ein Cookie, das Sie gesetzt haben.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Name | Typ | Erforderlich | Beschreibung |
|---|---|---|---|
| **`name`** | `string` | Ja | Der Cookie-Name, den Sie entfernen möchten. |
| **`attributes`** | `object` | Nein | Die mit dem Cookie verknüpften Attribute, die Sie entfernen möchten. Wenn Sie ein Cookie mithilfe der Attribute `path` oder `domain` setzen, schließen Sie beim Entfernen des Cookies dieselben Attribute mit ein. Wenn diese Attribute nicht eingeschlossen werden, wird das Cookie nicht entfernt. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Frühere Versionen des Tag-Objekts `_satellite.removeCookie()` verwendet. Die `removeCookie()` Methode ist zugunsten von `_satellite.cookie.remove()` veraltet.
