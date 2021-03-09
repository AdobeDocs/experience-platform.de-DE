---
title: Abrufen von Experience Cloud-IDs mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Adobe Experience Cloud-IDs (ECIDs) abrufen.
seo-description: Erfahren Sie, wie Sie die Adobe Experience Cloud-ID abrufen.
keywords: Identität;Erstanbieter-Identität;Identitätsdienst;Drittanbieter-Identität;ID-Migration;Besucher-ID;Drittanbieter-Identität;Drittanbieter-CookiesEnabled;idMigrationEnabled;getIdentity;Syncing-Identitäten;syncIdentity;sendEvent;identityMap;primary;ecid;Identity-Namensraum;Namensraum-ID;authenticationState;HashEnabled;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# Abrufen von Adobe Experience Cloud-IDs

Adobe Experience Platform Web SDK verwendet [Adobe Identity Service](../../identity-service/ecid.md). Dadurch wird sichergestellt, dass jedes Gerät über eine eindeutige ID verfügt, die auf dem Gerät beibehalten wird, damit die Aktivität zwischen den Seiten miteinander verknüpft werden kann.

## Identität des Erstanbieters

[!DNL Identity Service] speichert die Identität in einem Cookie in einer Erstanbieterdomäne. Das [!DNL Identity Service] versucht, das Cookie mithilfe eines HTTP-Headers in der Domäne festzulegen. Wenn dies fehlschlägt, kehrt [!DNL Identity Service] zurück, um Cookies über Javascript zu setzen. Adobe empfiehlt, dass Sie einen CNAME einrichten, um sicherzustellen, dass Ihre Cookies nicht durch clientseitige ITP-Beschränkungen begrenzt werden.

## Drittanbieter-Identität

Das [!DNL Identity Service] kann eine ID mit einer Drittanbieterdomäne (demdex.net) synchronisieren, um die Verfolgung über mehrere Sites hinweg zu ermöglichen. Wenn dies aktiviert ist, wird die erste Anforderung für einen Besucher (z. B. eine Person ohne ECID) an demdex.net gesendet. Dies geschieht nur in Browsern, die dies zulassen, wie Chrome) und wird durch den Parameter `thirdPartyCookiesEnabled` in der Konfiguration gesteuert. Wenn Sie diese Funktion zusammen deaktivieren möchten, setzen Sie `thirdPartyCookiesEnabled` auf false.

## ID-Migration

Bei der Migration von der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie den Parameter `idMigrationEnabled` in der Konfiguration fest. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um diesen Fall zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Darüber hinaus schreibt das SDK AMCV-Cookies, sodass nachfolgende Seiten, die mit der Besucher-API instrumentiert wurden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem SDK instrumentierten Seite abgerufen wird.
* Wenn Adobe Experience Platform Web SDK auf einer Seite eingerichtet ist, die auch über Besucher-API verfügt. Wenn der AMCV-Cookie nicht gesetzt ist, sucht das SDK zur Unterstützung dieses Falls nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das Adobe Experience Platform Web SDK verwendet und keine Besucher-API hat, ist es sinnvoll, die ECIDs zu migrieren, damit die Informationen zum zurückgegebenen Besucher erhalten bleiben. Nachdem das SDK für einen bestimmten Zeitraum mit `idMigrationEnabled` bereitgestellt wurde, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

## Eigenschaften für die Migration aktualisieren

Wenn XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Vorgang wird durch Verwendung des [BAAAM-Tools](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) erleichtert, das von Audience Manager erstellt wurde.

## Serverseitige Weiterleitung

Wenn Sie derzeit die serverseitige Weiterleitung aktiviert haben und `appmeasurement.js` verwenden. und `visitor.js` können Sie die Funktion für die serverseitige Weiterleitung aktivieren lassen, was keine Probleme verursacht. Im Backend ruft Adobe alle AAM Segmente ab und fügt sie dem Aufruf an Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics keinen Audience Manager auf, um Daten zu übermitteln, sodass keine Datenerfassung durch Dubletten erfolgt. Bei Verwendung des Web SDK ist auch kein Standort-Hint erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.

## Abrufen der Besucher-ID und Regions-ID

Wenn Sie die eindeutige Besucher-ID verwenden möchten, verwenden Sie den Befehl `getIdentity`. `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID. `getIdentity` gibt auch die Regions-ID für den Besucher zurück. Weitere Informationen finden Sie im [Adobe Audience Manager Benutzerhandbuch](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html).

>[!NOTE]
>
>Diese Methode wird in der Regel bei benutzerdefinierten Lösungen verwendet, bei denen die [!DNL Experience Cloud]-ID gelesen werden muss oder die Adobe Audience Manager-Ortskennung erforderlich ist. Sie wird nicht von einer Standardimplementierung verwendet.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Identitäten synchronisieren

>[!NOTE]
>
>Die `syncIdentity`-Methode wurde in Version 2.1.0 zusätzlich zur Hashing-Funktion entfernt. Wenn Sie Version 2.1.0+ verwenden und Identitäten synchronisieren möchten, können Sie diese direkt in der Option `xdm` des Befehls `sendEvent` unter dem Feld `identityMap` senden.

Darüber hinaus können Sie mit dem Befehl [!DNL Identity Service] Ihre eigenen IDs mit der ECID synchronisieren.`syncIdentity`

>[!NOTE]
>
>Es wird dringend empfohlen, alle verfügbaren Identitäten bei jedem Befehl `sendEvent` weiterzugeben. Dadurch wird eine Reihe von Anwendungsfällen, einschließlich der Personalisierung, freigegeben. Nachdem Sie diese Identitäten nun im Befehl `sendEvent` übergeben können, können sie direkt in DataLayer platziert werden.

Durch die Synchronisierung von Identitäten können Sie ein Gerät/einen Benutzer mit mehreren Identitäten identifizieren, den Authentifizierungsstatus festlegen und entscheiden, welcher Identifikator als der primäre Identifikator gilt. Wenn kein Bezeichner als `primary` festgelegt wurde, ist der primäre Standardwert `ECID`.

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
});
```

Jede Eigenschaft innerhalb von `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identitäts-Namensraum](../../identity-service/namespaces.md) gehören. Der Eigenschaftsname sollte das Identitäts-Namensraum-Symbol sein, das Sie in der Adobe Experience Platform-Benutzeroberfläche unter &quot;[!UICONTROL Identitäten]&quot;finden. Der Eigenschaftswert sollte ein Array von Identitäten sein, die zu diesem Identitäts-Namensraum gehören.

Jedes Identitätsobjekt im Identitätsarray ist wie folgt strukturiert:

### `id`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Dies ist die ID, die Sie für den angegebenen Namensraum synchronisieren möchten.

### `authenticationState`

| **Typ** | **Erforderlich** | **Standardwert** | **Mögliche Werte** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Zeichenfolge | Ja | mehrdeutig | mehrdeutig, authentifiziert und angemeldetOut |

Der Authentifizierungsstatus der ID.

### `primary`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | optional | false |

Bestimmt, ob diese Identität als primäres Fragment im einheitlichen Profil verwendet werden soll. Standardmäßig wird die ECID als primäre ID für den Benutzer festgelegt.
