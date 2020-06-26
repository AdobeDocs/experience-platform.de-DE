---
title: Abrufen der Experience Cloud-ID
seo-title: Adobe Experience Platform Web SDK Experience Cloud-ID abrufen
description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
seo-description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 10%

---


# Identität - Abrufen der Experience Cloud-ID

Das Adobe Experience Platform Web SDK nutzt den [Adobe-Identitätsdienst](../../identity-service/ecid.md). Dadurch wird sichergestellt, dass jedes Gerät über eine eindeutige ID verfügt, die auf dem Gerät beibehalten wird, damit die Aktivität zwischen den Seiten miteinander verknüpft werden kann.

## Identität des Ersten

Die [!DNL Identity Service] Identität wird in einem Cookie in einer Erstanbieterdomäne gespeichert. Der [!DNL Identity Service] Versuch, das Cookie mit einem HTTP-Header in der Domäne festzulegen. Wenn dies fehlschlägt, [!DNL Identity Service] kehrt das Programm zurück, um Cookies über JavaScript zu setzen. Adobe empfiehlt, dass Sie einen CNAME einrichten, um sicherzustellen, dass Ihre Cookies nicht durch clientseitige ITP-Beschränkungen begrenzt werden.

## Drittanbieter-Identität

Die [!DNL Identity Service] Gruppe kann eine ID mit einer Drittanbieterdomäne (demdex.net) synchronisieren, um die Verfolgung über mehrere Sites hinweg zu ermöglichen. Wenn dies aktiviert ist, wird die erste Anforderung für einen Besucher (z.B. eine Person ohne ECID) an demdex.net gesendet. Dies geschieht nur in Browsern, die es zulassen (z.B. Chrome) und wird durch den `thirdPartyCookiesEnabled` Parameter in der Konfiguration gesteuert. Wenn Sie diese Funktion vollständig deaktivieren möchten, setzen Sie sie `thirdPartyCookiesEnabled` auf &quot;false&quot;.

## Abrufen der Besucher-ID

Wenn Sie diese eindeutige ID verwenden möchten, verwenden Sie den `getIdentity` Befehl. `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID.

>[!NOTE]
>
>Diese Methode wird in der Regel bei benutzerdefinierten Lösungen verwendet, bei denen die Experience Cloud-ID gelesen werden muss. Sie wird nicht von einer Standardimplementierung verwendet.

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

Darüber hinaus [!DNL Identity Service] können Sie mit dem Befehl Ihre eigenen IDs mit der ECID synchronisieren `syncIdentity` .

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

Der Schlüssel für das Objekt ist das Symbol für den [Identitäts-Namensraum](../../identity-service/namespaces.md) . Sie finden diese in der Benutzeroberfläche der Adobe Experience Platform unter [!UICONTROL Identitäten].

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

Bestimmt, ob diese Identität als primäres Fragment im einheitlichen Profil verwendet werden soll. Standardmäßig wird die ECID als primäre ID für den Benutzer festgelegt.

#### `hashEnabled`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | optional | false |

Bei Aktivierung wird die Identität mit SHA256-Hashing gehackt.
