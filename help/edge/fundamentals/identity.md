---
title: Abrufen der Experience Cloud-ID
seo-title: Adobe Experience Platform Web SDK Experience Cloud-ID abrufen
description: Erfahren Sie, wie Sie die Adobe Experience Cloud-ID abrufen.
seo-description: Erfahren Sie, wie Sie die Adobe Experience Cloud-ID abrufen.
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 6%

---


# Identität - Abrufen der Experience Cloud-ID

Das Adobe Experience Platform [!DNL Web SDK] nutzt den Identitätsdienst für [Adoben](../../identity-service/ecid.md). Dadurch wird sichergestellt, dass jedes Gerät über eine eindeutige ID verfügt, die auf dem Gerät beibehalten wird, damit die Aktivität zwischen den Seiten miteinander verknüpft werden kann.

## Identität des Ersten

Die [!DNL Identity Service] Identität wird in einem Cookie in einer Erstanbieterdomäne gespeichert. Der [!DNL Identity Service] Versuch, das Cookie mit einem HTTP-Header in der Domäne festzulegen. Wenn dies fehlschlägt, [!DNL Identity Service] kehrt das Programm zurück, um Cookies über JavaScript zu setzen. Adobe empfiehlt, dass Sie einen CNAME einrichten, um sicherzustellen, dass Ihre Cookies nicht durch clientseitige ITP-Beschränkungen begrenzt werden.

## Drittanbieter-Identität

Die [!DNL Identity Service] Gruppe kann eine ID mit einer Drittanbieterdomäne (demdex.net) synchronisieren, um die Verfolgung über mehrere Sites hinweg zu ermöglichen. Wenn dies aktiviert ist, wird die erste Anforderung für einen Besucher (z.B. eine Person ohne ECID) an demdex.net gesendet. Dies geschieht nur in Browsern, die es zulassen (z.B. Chrome) und wird durch den `thirdPartyCookiesEnabled` Parameter in der Konfiguration gesteuert. Wenn Sie diese Funktion vollständig deaktivieren möchten, setzen Sie sie `thirdPartyCookiesEnabled` auf &quot;false&quot;.

## ID-Migration

Bei der Migration von der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie den `idMigrationEnabled` Parameter in der Konfiguration fest. Die ID-Migration wird eingerichtet, um einige Anwendungsfälle zu aktivieren:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um diesen Fall zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Darüber hinaus schreibt das SDK AMCV-Cookies, sodass nachfolgende Seiten, die mit der Besucher-API instrumentiert wurden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem AEP Web SDK instrumentierten Seite abgerufen wird.
* Wenn das AEP Web SDK auf einer Seite eingerichtet wird, die auch über Besucher-API verfügt. Um diesen Fall zu unterstützen, sucht das SDK, wenn das AMCV-Cookie nicht gesetzt ist, nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das AEP Web SDK verwendet und über keine Besucher-API verfügt, ist es sinnvoll, die ECIDs zu migrieren, damit die Informationen zum zurückgegebenen Besucher beibehalten werden. Nachdem das SDK `idMigrationEnabled` für einen bestimmten Zeitraum bereitgestellt wurde, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

## Abrufen der Besucher-ID

Wenn Sie diese eindeutige ID verwenden möchten, verwenden Sie den `getIdentity` Befehl. `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID.

>[!NOTE]
>
>Diese Methode wird in der Regel bei benutzerdefinierten Lösungen verwendet, bei denen die [!DNL Experience Cloud] ID gelesen werden muss. Sie wird nicht von einer Standardimplementierung verwendet.

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

>[!NOTE]
>
>Die `syncIdentity` Methode wurde in Version 2.1.0 zusätzlich zur Hashfunktion entfernt. Wenn Sie Version 2.1.0+ verwenden und Identitäten synchronisieren möchten, können Sie diese direkt in der `xdm` Option des `sendEvent` Befehls unter dem `identityMap` Feld senden.

Darüber hinaus [!DNL Identity Service] können Sie mit dem Befehl Ihre eigenen IDs mit der ECID synchronisieren `syncIdentity` .

>[!NOTE]
>
>Es wird dringend empfohlen, alle verfügbaren Identitäten an jedem `sendEvent` Befehl weiterzugeben. Dadurch wird eine Reihe von Anwendungsfällen, einschließlich der Personalisierung, freigegeben. Nachdem Sie diese Identitäten nun im `sendEvent` Befehl übergeben können, können sie direkt in DataLayer platziert werden.

Durch die Synchronisierung von Identitäten können Sie ein Gerät/einen Benutzer mit mehreren Identitäten identifizieren, den Authentifizierungsstatus festlegen und entscheiden, welcher Identifikator als der primäre Identifikator gilt. Wenn kein Bezeichner als `primary`festgelegt wurde, ist der primäre Standardwert der `ECID`.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
})
```


### Optionen für die Synchronisierung von Identitäten

#### Identitäts-Namensraum

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Der Schlüssel für das Objekt ist das Symbol für den [Identitäts-Namensraum](../../identity-service/namespaces.md) . Sie finden diese in der Adobe Experience Platform Benutzeroberfläche unter &quot;[!UICONTROL Identitäten]&quot;.

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
