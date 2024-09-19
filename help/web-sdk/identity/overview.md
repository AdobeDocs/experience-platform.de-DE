---
title: Identitätsdaten in Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Cloud IDs (ECIDs) mit dem Adobe Experience Platform Web SDK abrufen und verwalten.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c99831cf2bb1b862d65851701b38c6d3dfe99000
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 1%

---


# Identitätsdaten in Web SDK

Das Adobe Experience Platform Web SDK verwendet [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/features/ecid.md), um das Besucherverhalten zu verfolgen. Mit [!DNL ECIDs] können Sie sicherstellen, dass jedes Gerät über eine eindeutige Kennung verfügt, die über mehrere Sitzungen hinweg bestehen bleiben kann, wobei alle Treffer, die während und über mehrere Websitzungen hinweg auftreten, an ein bestimmtes Gerät gebunden werden.

Dieses Dokument bietet einen Überblick darüber, wie Sie [!DNL ECIDs] und [!DNL CORE IDs] mit dem Web SDK verwalten.

## Tracking von ECIDs mit dem Web SDK {#tracking-ecids-web-sdk}

Das Web SDK weist [!DNL ECIDs] mithilfe von Cookies zu und verfolgt sie nach, wobei mehrere verfügbare Methoden zum Konfigurieren der Erstellung dieser Cookies verfügbar sind.

Wenn ein neuer Benutzer auf Ihre Website gelangt, versucht der [Adobe Experience Cloud Identity Service](../../identity-service/home.md), ein Identifizierungs-Cookie für den betreffenden Benutzer zu setzen.

* Bei Erstbesuchern wird ein [!DNL ECID] generiert und in der ersten Antwort vom Experience Platform-Edge Network zurückgegeben.
* Bei wiederkehrenden Besuchern wird der [!DNL ECID] aus dem `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie abgerufen und vom Edge Network zur Anfrage-Payload hinzugefügt.

Nachdem das Cookie mit dem [!DNL ECID] gesetzt wurde, enthält jede nachfolgende vom Web SDK generierte Anforderung einen kodierten [!DNL ECID] im `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie.

Bei der Verwendung von Cookies zur Geräterkennung haben Sie zwei Möglichkeiten, mit dem Edge Network zu interagieren:

1. Erstellen Sie einen CNAME für Ihre eigene Domäne, der auf `adobedc.net` verweist. Diese Methode wird als [Erstanbieter-Datenerfassung](#first-party) bezeichnet.
1. Senden Sie Daten direkt an die Edge Network-Domäne `adobedc.net`. Diese Methode wird als [Datenerfassung durch Dritte](#third-party) bezeichnet.

Wie in den folgenden Abschnitten erläutert, wirkt sich die von Ihnen gewählte Datenerfassungsmethode direkt auf die Cookie-Lebensdauer in allen Browsern aus.

## Tracking von CORE-IDs mit dem Web SDK {#tracking-coreid-web-sdk}

Wenn Sie Google Chrome mit aktivierten Drittanbieter-Cookies verwenden und kein `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie gesetzt ist, durchläuft die erste Edge Network-Anfrage eine `demdex.net` -Domäne, die einen demdex-Cookie setzt. Dieses Cookie enthält einen [!DNL CORE ID]. Dies ist eine eindeutige Benutzer-ID, die sich von der [!DNL ECID] unterscheidet.

Abhängig von Ihrer Implementierung können Sie [auf den  [!DNL CORE ID]](#retrieve-coreid) zugreifen.

### Erstanbieter-Datenerfassung {#first-party}

Die Datenerfassung von Erstanbietern umfasst das Setzen von Cookies über eine `CNAME` in Ihrer eigenen Domäne, die auf `adobedc.net` verweist.

Während Browser Cookies, die von `CNAME` -Endpunkten gesetzt werden, seit langem ähnlich wie von Site-eigenen Endpunkten behandeln, haben jüngste, von Browsern implementierte Änderungen eine Unterscheidung in der Handhabung von `CNAME` -Cookies geschaffen. Es gibt zwar keine Browser, die standardmäßig Erstanbieter-Cookies vom Typ `CNAME` blockieren, aber einige Browser beschränken die Lebensdauer von Cookies, die mit dem Wert `CNAME` gesetzt werden, auf nur sieben Tage.

### Datenerfassung von Drittanbietern {#third-party}

Die Datenerfassung von Drittanbietern beinhaltet das direkte Senden von Daten an die Edge Network-Domäne `adobedc.net`.

In den letzten Jahren haben die Webbrowser bei der Behandlung von Cookies, die von Dritten gesetzt werden, immer restriktiver werden. Einige Browser blockieren standardmäßig Drittanbieter-Cookies. Wenn Sie zur Identifizierung von Site-Besuchern Drittanbieter-Cookies verwenden, ist die Lebensdauer dieser Cookies fast immer kürzer, als dies sonst durch Erstanbieter-Cookies möglich wäre. Manchmal läuft ein Drittanbieter-Cookie in nur sieben Tagen ab.

Bei der Verwendung der Datenerfassung von Drittanbietern beschränken einige Anzeigensperren den Traffic außerdem vollständig auf Adobe-Datenerfassungs-Endpunkte.

### Auswirkungen von Cookie-Lebenszyklen auf Adobe Experience Cloud-Anwendungen {#lifespans}

Unabhängig davon, ob Sie die Datenerfassung von Erstanbietern oder Drittanbietern auswählen, hat die Dauer, die ein Cookie beibehalten werden kann, direkte Auswirkungen auf die Besucherzahlen in [Adobe Analytics](https://experienceleague.adobe.com/de/docs/analytics) und [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/customer-journey-analytics). Außerdem kann es bei Endbenutzern zu inkonsistenten Personalisierungserlebnissen kommen, wenn [Adobe Target](https://experienceleague.adobe.com/en/docs/target) oder [Offer decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision) auf der Site verwendet werden.

Angenommen, Sie haben ein Personalisierungs-Erlebnis erstellt, das jedes Element auf die Startseite weiterleitet, wenn ein Benutzer es in den letzten sieben Tagen dreimal angesehen hat.

Wenn ein Endbenutzer die Site dreimal in einer Woche besucht und dann sieben Tage lang nicht erneut aufruft, kann dieser Benutzer bei seiner Rückkehr zur Site als neuer Benutzer gelten, da seine Cookies möglicherweise von einer Browserrichtlinie gelöscht wurden (je nach dem Browser, den er bei seinem Besuch auf der Site verwendet hat). In diesem Fall behandelt Ihr Analytics-Tool den Besucher als neuen Benutzer, auch wenn er die Site vor etwas mehr als sieben Tagen besucht hat. Außerdem beginnt jeder Versuch, das Erlebnis für den Benutzer zu personalisieren, erneut.

### Erstanbieter-Geräte-IDs (FPIDs) {#fpid}

Um die oben beschriebenen Auswirkungen von Cookie-Lebenszyklen zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Weitere Informationen finden Sie im Leitfaden zu [IDs von Erstanbieter-Geräten](./first-party-device-ids.md).

## Abrufen der ECID und der Region für den aktuellen Benutzer {#retrieve-ecid}

Je nach Anwendungsfall gibt es zwei Möglichkeiten, auf den [!DNL ECID] zuzugreifen:

* [Rufen Sie den  [!DNL ECID] über die Datenvorbereitung für die Datenerfassung ab](#retrieve-ecid-data-prep): Dies ist die empfohlene Methode.
* [Rufen Sie den  [!DNL ECID]  durch den Befehl `getIdentity()` ab](#retrieve-ecid-getidentity): Verwenden Sie diese Methode nur, wenn Sie die [!DNL ECID] -Informationen clientseitig benötigen.

### Abrufen des [!DNL ECID] über die Datenvorbereitung für die Datenerfassung {#retrieve-ecid-data-prep}

Verwenden Sie [Datenvorbereitung für die Datenerfassung](../../datastreams/data-prep.md) , um die [!DNL ECID] einem [!DNL XDM] -Feld zuzuordnen. Dies ist die empfohlene Methode für den Zugriff auf den [!DNL ECID].

Setzen Sie dazu das Quellfeld auf den folgenden Pfad:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Zielfeld auf einen XDM-Pfad fest, bei dem das Feld vom Typ `string` ist.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Rufen Sie den [!DNL ECID] über den Befehl `getIdentity()` ab {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Sie sollten die ECID nur über den Befehl `getIdentity()` abrufen, wenn Sie die [!DNL ECID] auf der Clientseite benötigen. Wenn Sie die ECID nur einem XDM-Feld zuordnen möchten, verwenden Sie stattdessen [Datenvorbereitung für die Datenerfassung](#retrieve-ecid-data-prep) .

Verwenden Sie den Befehl `getIdentity` , um die eindeutige ECID für den aktuellen Besucher abzurufen. Für erstmalige Besucher, die noch nicht über &quot;[!DNL ECID]&quot; verfügen, generiert dieser Befehl eine neue &quot;[!DNL ECID]&quot;. `getIdentity` gibt auch die Regions-ID für den Besucher zurück.

>[!NOTE]
>
>Diese Methode wird normalerweise bei benutzerdefinierten Lösungen verwendet, bei denen die [!DNL Experience Cloud]-ID gelesen werden muss oder ein Standorthinweis für Adobe Audience Manager erforderlich ist. Sie wird nicht von einer Standardimplementierung verwendet.

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

## Abrufen der CORE-ID für den aktuellen Benutzer {#retrieve-coreid}

Um die CORE-ID für einen Benutzer abzurufen, können Sie den Befehl [`getIdentity()`](../commands/getidentity.md) verwenden, wie unten dargestellt.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## Verwenden `identityMap` {#using-identitymap}

Mithilfe eines XDM [`identityMap`-Felds ](../../xdm/schema/composition.md#identityMap) können Sie ein Gerät/einen Benutzer anhand mehrerer Identitäten identifizieren, seinen Authentifizierungsstatus festlegen und entscheiden, welche Kennung als die primäre ID gilt. Wenn keine Kennung als `primary` festgelegt wurde, ist die primäre Standardeinstellung die `ECID`.

`identityMap` -Felder werden mit dem Befehl `sentEvent` aktualisiert.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe empfiehlt das Senden von Namespaces, die eine Person repräsentieren, z. B. `CRMID`, als primäre Identität.


Jede Eigenschaft innerhalb von `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identitäts-Namespace](../../identity-service/features/namespaces.md) gehören. Der Eigenschaftsname sollte das Identitäts-Namespace-Symbol sein, das Sie in der Adobe Experience Platform-Benutzeroberfläche unter &quot;[!UICONTROL Identitäten]&quot;finden. Der Eigenschaftswert sollte ein Array von Identitäten sein, die sich auf diesen Identitäts-Namespace beziehen.

>[!IMPORTANT]
>
>Bei der Namespace-ID, die an `identityMap` übergeben wird, wird zwischen Groß- und Kleinschreibung unterschieden. Stellen Sie sicher, dass Sie die richtige Namespace-ID verwenden, um eine unvollständige Datenerfassung zu vermeiden.

Jedes Identitätsobjekt im Identitäten-Array enthält die folgenden Eigenschaften:

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | **(Erforderlich)** Die ID, die Sie für den angegebenen Namespace festlegen möchten. |
| `authenticatedState` | String | **(Erforderlich)** Der Authentifizierungsstatus der ID. Zu den möglichen Werten gehören `ambiguous`, `authenticated` und `loggedOut`. |
| `primary` | Boolesch | Bestimmt, ob diese Identität als primäres Fragment im Profil verwendet werden soll. Standardmäßig wird die ECID als primäre Kennung für den Benutzer festgelegt. Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |

Die Verwendung des Felds `identityMap` zur Identifizierung von Geräten oder Benutzern führt zum selben Ergebnis wie die Verwendung der Methode [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) aus dem [!DNL ID Service API]. Weitere Informationen finden Sie in der Dokumentation zur [ID-Dienst-API](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) .

## Migration von der Besucher-API zur ECID {#migrating-visitor-api-ecid}

Bei der Migration von der Verwendung der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie den Parameter `idMigrationEnabled` in der Konfiguration fest. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um dies zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Außerdem schreibt das SDK AMCV-Cookies so, dass nachfolgende Seiten, die mit der Besucher-API instrumentiert werden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem SDK instrumentierten Seite abgerufen wird.
* Wenn das Adobe Experience Platform Web SDK auf einer Seite eingerichtet ist, die auch über eine Besucher-API verfügt. Wenn das AMCV-Cookie nicht gesetzt ist, sucht das SDK in diesem Fall nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das Adobe Experience Platform Web SDK verwendet und keine Besucher-API hat, ist es nützlich, die ECIDs zu migrieren, damit die zurückgegebenen Besucherinformationen beibehalten werden. Nachdem das SDK eine Zeit lang mit `idMigrationEnabled` bereitgestellt wurde, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

### Eigenschaften für die Migration aktualisieren

Wenn XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Vorgang wird durch die Verwendung des von Audience Manager erstellten [BAAAM-Tools](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) vereinfacht.

## Verwendung in der Ereignisweiterleitung

Wenn Sie derzeit die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) aktiviert haben und `appmeasurement.js` und `visitor.js` verwenden, können Sie die Ereignisweiterleitungsfunktion aktiviert lassen, was keine Probleme verursacht. Am Backend ruft Adobe alle AAM Segmente ab und fügt sie zum Aufruf von Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics Audience Manager nicht auf, Daten weiterzuleiten, sodass keine doppelte Datenerfassung erfolgt. Bei Verwendung des Web SDK ist außerdem kein Standorthinweis erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.
