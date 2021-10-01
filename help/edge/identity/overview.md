---
title: Abrufen von Experience Cloud-IDs mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Cloud IDs (ECIDs) mit dem Adobe Experience Platform Web SDK abrufen.
seo-description: Learn how to get Adobe Experience Cloud Id.
keywords: Identität; Erstanbieter-Identität; Identity-Dienst; Drittanbieter-Identität; ID-Migration; Besucher-ID; Drittanbieter-Identität; thirdPartyCookiesEnabled; idMigrationEnabled; getIdentity; Syncing Identities; syncIdentity; sendEvent; identityMap; primary; ecid; Identity-Namespace; Namespace-ID; authenticationState; hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: d753cfca6f518dfe2cafa1cb30ad26bd0b591c54
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 6%

---

# Adobe Experience Cloud IDs

Das Adobe Experience Platform Web SDK nutzt [Adobe Identity Service](../../identity-service/ecid.md). Dadurch wird sichergestellt, dass jedes Gerät über eine eindeutige Kennung verfügt, die auf dem Gerät beibehalten wird, sodass Aktivitäten zwischen Seiten verknüpft werden können.

## Erstanbieteridentität

[!DNL Identity Service] speichert die Identität in einem Cookie in einer Erstanbieterdomäne. [!DNL Identity Service] versucht, das Cookie mithilfe eines HTTP-Headers in der Domäne festzulegen. Wenn dies fehlschlägt, setzt [!DNL Identity Service] auf das Setzen von Cookies mit JavaScript zurück. Es wird empfohlen, einen CNAME für Ihre [Edge Domain-Konfiguration](../fundamentals/configuring-the-sdk.md#edgeConfigId) einzurichten.

Jedem vom Platform Web SDK stammenden Treffer wird vom Identity Service im Edge Network eine ECID hinzugefügt. Bei erstmaligen Besuchern wird die ECID generiert und der Payload hinzugefügt. Bei sich wiederholenden Besuchern wird die ECID aus dem `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie abgerufen und der Payload hinzugefügt.

Die ECID wird unter dem Feld `identityMap` in Ihrem `xdm` hinzugefügt. Mithilfe des Entwicklungstools des Browsers können Sie die ECID in der Antwort unter der Payload mit dem Typ anzeigen: `identity:result`, aber die ECID kann nicht in der Anfrage angezeigt werden.

Mit der CNAME-Implementierungen können Sie die von Adobe verwendete Sammel-Domain so anpassen, dass sie mit Ihrer eigenen Domain übereinstimmt. Dadurch kann Adobe First-Party-Cookies mithilfe von JavaScript Server-seitig anstatt Client-seitig setzen. In der Vergangenheit waren diese Server-seitigen Erstanbieter-Cookies keinen Beschränkungen unterworfen, die gemäß der ITP-Richtlinie (Intelligent Tracking Prevention) von Apple für Safari-Browser gelten. Im November 2020 aktualisierte Apple jedoch seine Richtlinien, sodass diese Einschränkungen auch auf Cookies angewendet wurden, die über CNAME gesetzt wurden. Derzeit sind beide Cookies, die serverseitig durch CNAME gesetzt werden, und die von JavaScript auf Client-Seite gesetzten Cookies unter ITP auf einen Ablauf von sieben Tagen oder 24 Stunden beschränkt. Weitere Informationen zur ITP-Richtlinie finden Sie in diesem Apple-Dokument zu [Tracking Prevention](https://webkit.org/tracking-prevention/#intelligent-tracking-prevention-itp).

Auch wenn eine CNAME-Implementierung keine Vorteile in Bezug auf die Cookie-Lebensdauer bietet, kann es einige weitere Vorteile wie Anzeigenblocker und weniger häufig verwendete Browser geben, die verhindern, dass Daten an Domänen gesendet werden, die sie als Tracker klassifizieren. In diesen Fällen kann die Verwendung eines CNAME verhindern, dass die Datenerfassung für Benutzer, die diese Tools verwenden, unterbrochen wird.

## Identität von Drittanbietern

[!DNL Identity Service] kann eine ID mit einer Drittanbieterdomäne (demdex.net) synchronisieren, um die Site-übergreifende Verfolgung zu ermöglichen. Wenn dies aktiviert ist, wird die erste Anforderung für einen Besucher (z. B. eine Person ohne ECID) an demdex.net gesendet. Dies erfolgt nur bei Browsern, die dies zulassen (z. B. Chrome) und wird durch den Parameter `thirdPartyCookiesEnabled` in der Konfiguration gesteuert. Wenn Sie diese Funktion alle zusammen deaktivieren möchten, setzen Sie `thirdPartyCookiesEnabled` auf &quot;false&quot;.

## ID-Migration

Bei der Migration von der Verwendung der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie den Parameter `idMigrationEnabled` in der Konfiguration fest. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um dies zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Darüber hinaus schreibt das SDK AMCV-Cookies so, dass nachfolgende Seiten, die mit der Besucher-API instrumentiert werden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem SDK instrumentierten Seite abgerufen wird.
* Wenn das Adobe Experience Platform Web SDK auf einer Seite eingerichtet ist, die auch über eine Besucher-API verfügt. Wenn das AMCV-Cookie nicht gesetzt ist, sucht das SDK in diesem Fall nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das Adobe Experience Platform Web SDK verwendet und keine Besucher-API hat, ist es nützlich, die ECIDs zu migrieren, damit die zurückgegebenen Besucherinformationen beibehalten werden. Nachdem das SDK für einen bestimmten Zeitraum mit `idMigrationEnabled` bereitgestellt wurde, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

## Eigenschaften für die Migration aktualisieren

Wenn XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Vorgang wird durch die Verwendung des [BAAAM-Tools](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) vereinfacht, das der Audience Manager erstellt hat.

## Serverseitige Weiterleitung

Wenn Sie derzeit die serverseitige Weiterleitung aktiviert haben und `appmeasurement.js` verwenden. und `visitor.js` können Sie die serverseitige Weiterleitungsfunktion aktivieren lassen, was keine Probleme verursacht. Im Backend ruft Adobe alle AAM Segmente ab und fügt sie zum Aufruf von Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics Audience Manager nicht auf, Daten weiterzuleiten, sodass keine doppelte Datenerfassung erfolgt. Bei Verwendung des Web SDK ist außerdem kein Standorthinweis erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.

## Abrufen der Besucher-ID und Regions-ID

Wenn Sie die Unique Visitor-ID verwenden möchten, verwenden Sie den Befehl `getIdentity` . `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID. `getIdentity` gibt auch die Regions-ID für den Besucher zurück. Weitere Informationen finden Sie im [Adobe Audience Manager-Benutzerhandbuch](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=de).

>[!NOTE]
>
>Diese Methode wird normalerweise bei benutzerdefinierten Lösungen verwendet, bei denen die [!DNL Experience Cloud]-ID gelesen werden muss oder die den Adobe Audience Manager-Standorthinweis benötigen. Sie wird nicht von einer Standardimplementierung verwendet.

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

## Synchronisieren von Identitäten

>[!NOTE]
>
>Die `syncIdentity`-Methode wurde in Version 2.1.0 zusätzlich zur Hashing-Funktion entfernt. Wenn Sie Version 2.1.0+ verwenden und Identitäten synchronisieren möchten, können Sie diese direkt in der `xdm`-Option des Befehls `sendEvent` unter dem Feld `identityMap` senden.

Außerdem können Sie mit [!DNL Identity Service] Ihre eigenen IDs mit der ECID synchronisieren, indem Sie den Befehl `syncIdentity` verwenden.

>[!NOTE]
>
>Es wird dringend empfohlen, alle verfügbaren Identitäten bei jedem `sendEvent`-Befehl weiterzugeben. Dadurch wird eine Reihe von Anwendungsfällen, einschließlich der Personalisierung, freigeschaltet. Nachdem Sie diese Identitäten nun im Befehl `sendEvent` übergeben können, können sie direkt in Ihre DataLayer eingefügt werden.

Durch die Synchronisierung von Identitäten können Sie ein Gerät/Benutzer anhand mehrerer Identitäten identifizieren, seinen Authentifizierungsstatus festlegen und entscheiden, welche Kennung als die primäre ID gilt. Wenn keine Kennung als `primary` festgelegt wurde, ist die primäre Standardeinstellung `ECID`.

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

Jede Eigenschaft innerhalb von `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identitäts-Namespace](../../identity-service/namespaces.md) gehören. Der Eigenschaftsname sollte das Identitäts-Namespace-Symbol sein, das Sie in der Adobe Experience Platform-Benutzeroberfläche unter &quot;[!UICONTROL Identitäten]&quot;finden. Der Eigenschaftswert sollte ein Array von Identitäten sein, die sich auf diesen Identitäts-Namespace beziehen.

Jedes Identitätsobjekt im Identitäts-Array ist wie folgt strukturiert:

### `id`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Zeichenfolge | Ja | Keine |

Dies ist die ID, die Sie für den angegebenen Namespace synchronisieren möchten.

### `authenticationState`

| **Typ** | **Erforderlich** | **Standardwert** | **Mögliche Werte** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Zeichenfolge | Ja | mehrdeutig | mehrdeutig, authentifiziert und angemeldetOut |

Der Authentifizierungsstatus der ID.

### `primary`

| **Typ** | **Erforderlich** | **Standardwert** |
| -------- | ------------ | ----------------- |
| Boolesch | optional | false |

Bestimmt, ob diese Identität als primäres Fragment im einheitlichen Profil verwendet werden soll. Standardmäßig wird die ECID als primäre Kennung für den Benutzer festgelegt.
