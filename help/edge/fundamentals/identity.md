---
title: Abrufen der Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK Abrufen der Experience Cloud ID
description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
seo-description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
translation-type: tm+mt
source-git-commit: a9dd5fd93397e57d0876bec334d54c517fa86939
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 10%

---


# Abrufen der Experience Cloud ID

Das Adobe Experience Platform Web SDK nutzt den [Adobe-Identitätsdienst](../../identity-service/ecid.md). Dadurch wird sichergestellt, dass jedes Gerät über eine eindeutige ID verfügt, die auf dem Gerät beibehalten wird, damit die Aktivität zwischen den Seiten miteinander verknüpft werden kann.

## Identität des Ersten

Der ID-Dienst speichert die Identität in einem Cookie in einer Erstanbieterdomäne. Der ID-Dienst versucht, das Cookie mithilfe eines HTTP-Headers in der Domäne einzustellen, wenn dies fehlschlägt, wird der ID-Dienst auf das Setzen von Cookies über JavaScript zurückgreifen. Adobe empfiehlt, dass Sie einen CNAME einrichten, um sicherzustellen, dass Ihre Cookies nicht durch clientseitige ITP-Beschränkungen begrenzt werden.

## Drittanbieter-Identität

Die ID-Dienste haben die Möglichkeit, eine ID mit einer Drittanbieterdomäne (demdex.net) zu synchronisieren, um die Site-übergreifende Verfolgung zu aktivieren. Wenn dies aktiviert ist, wird die erste Anforderung für einen Besucher (z.B. eine Person ohne ECID) an demdex.net gesendet. Dies geschieht nur in Browsern, die es zulassen (z.B. Chrome) und wird durch den `thirdPartyCookiesEnabled` Parameter in der Konfiguration gesteuert. Wenn Sie diese Funktion deaktivieren möchten, setzen Sie sie alle zusammen `thirdPartyCookiesEnabled` auf &quot;false&quot;.

## Abrufen der Besucher-ID

Wenn Sie diese eindeutige ID verwenden möchten, verwenden Sie den `getIdentity` Befehl. `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID.

>[!NOTE]
>
>Diese Methode wird in der Regel bei benutzerdefinierten Lösungen verwendet, bei denen die Experience Cloud ID gelesen werden muss. Sie wird nicht von einer Standardimplementierung verwendet.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Identitäten synchronisieren

Darüber hinaus ermöglicht Ihnen der Identitätsdienst die Synchronisierung Ihrer eigenen IDs mit der ECID mithilfe des `syncIdentity` Befehls.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Optionen für die Synchronisierung von Identitäten

#### Identitäts-Namensraum

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Der Schlüssel für das Objekt ist das Symbol für den [Identitäts-Namensraum](../../identity-service/namespaces.md) . Sie finden dies in der Benutzeroberfläche von Adobe Experience Platform unter Identitäten.

#### `id`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Dies ist die ID, die Sie für den angegebenen Namensraum synchronisieren möchten.

#### `authenticationState`

| **Typ** | **Erforderlich** | **Standardwert** | **Mögliche Werte** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Zeichenfolge | Ja | mehrdeutig | mehrdeutig, authentifiziert und angemeldetOut |

Der Authentifizierungsstatus der ID.

#### `primary`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | optional | false |

Sollte diese Identität als primäres Fragment im einheitlichen Profil verwendet werden. Standardmäßig wird die ECID als primäre ID für den Benutzer festgelegt.

#### `hashEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | optional | false |

Bei Aktivierung wird die Identität mit SHA256-Hashing gehackt.
