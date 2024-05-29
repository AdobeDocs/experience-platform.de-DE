---
title: Identitätsdaten in Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Cloud IDs (ECIDs) mit dem Adobe Experience Platform Web SDK abrufen und verwalten.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 6b58d72628b58b75a950892e7c16d397e3c107e2
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 2%

---

# Identitätsdaten in Web SDK

Das Adobe Experience Platform Web SDK verwendet [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/features/ecid.md) , um das Besucherverhalten zu verfolgen. Mithilfe von ECIDs können Sie sicherstellen, dass jedes Gerät über eine eindeutige ID verfügt, die über mehrere Sitzungen hinweg persistent sein kann, und alle Treffer, die während und über mehrere Websitzungen hinweg auftreten, an ein bestimmtes Gerät binden.

Dieses Dokument bietet einen Überblick darüber, wie ECIDs mit dem Platform Web SDK verwaltet werden.

## Tracking von ECIDs mit dem SDK

Das Platform Web SDK weist ECIDs mithilfe von Cookies zu und verfolgt sie. Es stehen verschiedene Methoden zur Konfiguration der Erstellung dieser Cookies zur Verfügung.

Wenn ein neuer Benutzer auf Ihre Website gelangt, versucht Adobe Experience Cloud Identity Service, ein Cookie zur Identifizierung des Geräts für diesen Benutzer zu setzen. Bei Erstbesuchern wird eine ECID generiert und in der ersten Antwort vom Adobe Experience Platform-Edge Network zurückgegeben. Bei wiederkehrenden Besuchern wird die ECID aus dem `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie und vom Edge Network zur Payload hinzugefügt.

Sobald das Cookie, das die ECID enthält, gesetzt wurde, enthält jede nachfolgende vom Web SDK generierte Anfrage eine codierte ECID in der `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie.

Bei der Verwendung von Cookies zur Geräteidentifizierung haben Sie zwei Möglichkeiten, mit dem Edge Network zu interagieren:

1. Daten direkt an die Edge Network-Domäne senden `adobedc.net`. Diese Methode wird als [Datenerfassung von Drittanbietern](#third-party).
1. Erstellen Sie einen CNAME für Ihre eigene Domäne, der auf `adobedc.net`. Diese Methode wird als [Erstanbieter-Datenerfassung](#first-party).

Wie in den folgenden Abschnitten erläutert, wirkt sich die von Ihnen gewählte Datenerfassungsmethode direkt auf die Cookie-Lebensdauer in allen Browsern aus.

### Datenerfassung von Drittanbietern {#third-party}

Die Datenerfassung von Drittanbietern beinhaltet das direkte Senden von Daten an die Edge Network-Domäne `adobedc.net`.

In den letzten Jahren haben die Webbrowser bei der Behandlung von Cookies von Drittanbietern immer restriktiver werden. Einige Browser blockieren standardmäßig Drittanbieter-Cookies. Wenn Sie zur Identifizierung von Site-Besuchern Drittanbieter-Cookies verwenden, ist die Lebensdauer dieser Cookies fast immer kürzer, als dies sonst durch Erstanbieter-Cookies möglich wäre. Manchmal läuft ein Drittanbieter-Cookie in nur sieben Tagen ab.

Wenn die Datenerfassung von Drittanbietern verwendet wird, beschränken einige Anzeigensperren den Traffic außerdem vollständig auf Adobe-Datenerfassungs-Endpunkte.

### Erstanbieter-Datenerfassung {#first-party}

Die Datenerfassung von Erstanbietern umfasst das Setzen von Cookies über einen CNAME in Ihrer eigenen Domäne, der auf Folgendes verweist: `adobedc.net`.

Während Browser Cookies, die von CNAME-Endpunkten gesetzt werden, seit langem ähnlich wie von Site-eigenen Endpunkten behandeln, haben kürzlich von Browsern implementierte Änderungen eine Unterscheidung in der Handhabung von CNAME-Cookies geschaffen. Es gibt zwar keine Browser, die standardmäßig Erstanbieter-CNAME-Cookies blockieren, aber einige Browser beschränken die Lebensdauer von Cookies, die mit einem CNAME gesetzt werden, auf sieben Tage.

### Auswirkungen von Cookie-Lebenszyklen auf Adobe Experience Cloud-Anwendungen {#lifespans}

Unabhängig davon, ob Sie die Datenerfassung von Erstanbietern oder Drittanbietern auswählen, hat die Dauer, die ein Cookie beibehalten werden kann, direkte Auswirkungen auf die Besucherzahlen in Adobe Analytics und Customer Journey Analytics. Außerdem kann es bei Endbenutzern zu inkonsistenten Personalisierungserlebnissen kommen, wenn Adobe Target oder Offer decisioning auf der Site verwendet werden.

Angenommen, Sie haben ein Personalisierungs-Erlebnis erstellt, das jedes Element auf die Startseite weiterleitet, wenn ein Benutzer es in den letzten sieben Tagen dreimal angesehen hat.

Wenn ein Endbenutzer die Site dreimal in einer Woche besucht und dann sieben Tage lang nicht erneut aufruft, kann dieser Benutzer bei seiner Rückkehr zur Site als neuer Benutzer gelten, da seine Cookies möglicherweise von einer Browserrichtlinie gelöscht wurden (je nach dem Browser, den er bei seinem Besuch auf der Site verwendet hat). In diesem Fall behandelt Ihr Analytics-Tool den Besucher als neuen Benutzer, auch wenn er die Site vor etwas mehr als sieben Tagen besucht hat. Außerdem beginnt jeder Versuch, das Erlebnis für den Benutzer zu personalisieren, erneut.

### IDs von Erstanbieter-Geräten

Um die oben beschriebenen Auswirkungen von Cookie-Lebenszyklen zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Weitere Informationen finden Sie im Leitfaden zu [IDs von Erstanbieter-Geräten](./first-party-device-ids.md).

## Abrufen der ECID und der Region für den aktuellen Benutzer {#retrieve-ecid}

Je nach Anwendungsfall gibt es zwei Möglichkeiten, auf die [!DNL ECID]:

* [Rufen Sie die [!DNL ECID] durch Datenvorbereitung für die Datenerfassung](#retrieve-ecid-data-prep): Dies ist die empfohlene Methode.
* [Rufen Sie die [!DNL ECID] durch die `getIdentity()` command](#retrieve-ecid-getidentity): Verwenden Sie diese Methode nur, wenn Sie die [!DNL ECID] Informationen Client-seitig.

### Rufen Sie die [!DNL ECID] durch Datenvorbereitung für die Datenerfassung {#retrieve-ecid-data-prep}

Verwendung [Datenvorbereitung für die Datenerfassung](../../datastreams/data-prep.md) zum Zuordnen des [!DNL ECID] zu [!DNL XDM] -Feld. Dies ist die empfohlene Methode für den Zugriff auf [!DNL ECID].

Setzen Sie dazu das Quellfeld auf den folgenden Pfad:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Zielfeld auf einen XDM-Pfad fest, bei dem das Feld vom Typ ist `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Rufen Sie die [!DNL ECID] durch die `getIdentity()` command {#retrieve-ecid-getidentity}


>[!IMPORTANT]
>
>Sie sollten die ECID nur über die `getIdentity()` , wenn Sie [!DNL ECID] Client-seitig. Wenn Sie die ECID nur einem XDM-Feld zuordnen möchten, verwenden Sie [Datenvorbereitung für die Datenerfassung](#retrieve-ecid-data-prep) anstatt.

Verwenden Sie zum Abrufen der eindeutigen ECID für den aktuellen Besucher die `getIdentity` Befehl. Für erstmalige Besucher ohne [!DNL ECID] Dieser Befehl generiert jedoch eine neue [!DNL ECID]. `getIdentity` gibt auch die Regions-ID für den Besucher zurück.

>[!NOTE]
>
>Diese Methode wird normalerweise bei benutzerdefinierten Lösungen verwendet, bei denen das Lesen der [!DNL Experience Cloud] ID oder Sie benötigen einen Standorthinweis für Adobe Audience Manager. Sie wird nicht von einer Standardimplementierung verwendet.

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

## Verwenden `identityMap`

Verwenden eines XDM [`identityMap` field](../../xdm/schema/composition.md#identityMap)können Sie ein Gerät/einen Benutzer anhand mehrerer Identitäten identifizieren, seinen Authentifizierungsstatus festlegen und entscheiden, welche Kennung als die primäre ID gilt. Wenn keine Kennung als `primary`, ist standardmäßig die `ECID`.

`identityMap` -Felder werden mit der Variablen `sentEvent` Befehl.

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


Jede Eigenschaft in `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identitäts-Namespace](../../identity-service/features/namespaces.md). Der Eigenschaftsname sollte das Identitäts-Namespace-Symbol sein, das Sie in der Adobe Experience Platform-Benutzeroberfläche unter[!UICONTROL Identitäten]&quot;. Der Eigenschaftswert sollte ein Array von Identitäten sein, die sich auf diesen Identitäts-Namespace beziehen.

>[!IMPORTANT]
>
>Die Namespace-ID, die im `identityMap` zwischen Groß- und Kleinschreibung unterschieden wird. Stellen Sie sicher, dass Sie die richtige Namespace-ID verwenden, um eine unvollständige Datenerfassung zu vermeiden.

Jedes Identitätsobjekt im Identitäten-Array enthält die folgenden Eigenschaften:

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | **(Erforderlich)** Die ID, die Sie für den angegebenen Namespace festlegen möchten. |
| `authenticationState` | Zeichenfolge | **(Erforderlich)** Der Authentifizierungsstatus der ID. Zu den möglichen Werten gehören `ambiguous`, `authenticated` und `loggedOut`. |
| `primary` | Boolesch | Bestimmt, ob diese Identität als primäres Fragment im Profil verwendet werden soll. Standardmäßig wird die ECID als primäre Kennung für den Benutzer festgelegt. Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |

Verwenden der `identityMap` -Feld zur Identifizierung von Geräten oder Benutzern führt zum gleichen Ergebnis wie bei Verwendung der [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) -Methode aus [!DNL ID Service API]. Siehe [Dokumentation zur ID-Dienst-API](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) für weitere Details.

## Migration von der Besucher-API zur ECID

Bei der Migration von der Verwendung der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie die `idMigrationEnabled` -Parameter in der Konfiguration. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um dies zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Außerdem schreibt das SDK AMCV-Cookies so, dass nachfolgende Seiten, die mit der Besucher-API instrumentiert werden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem SDK instrumentierten Seite abgerufen wird.
* Wenn das Adobe Experience Platform Web SDK auf einer Seite eingerichtet ist, die auch über eine Besucher-API verfügt. Wenn das AMCV-Cookie nicht gesetzt ist, sucht das SDK in diesem Fall nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das Adobe Experience Platform Web SDK verwendet und keine Besucher-API hat, ist es nützlich, die ECIDs zu migrieren, damit die zurückgegebenen Besucherinformationen beibehalten werden. Nach der Bereitstellung des SDK mit `idMigrationEnabled` eine Zeit lang, damit die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

### Eigenschaften für die Migration aktualisieren

Wenn XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Prozess wird durch die Verwendung der [BAAAM-Tool](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) Dieser Audience Manager hat erstellt.

## Verwendung in der Ereignisweiterleitung

Wenn Sie derzeit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) aktiviert sind und verwenden `appmeasurement.js` und `visitor.js`können Sie die Ereignisweiterleitungsfunktion aktivieren lassen, was keine Probleme verursacht. Am Backend ruft Adobe alle AAM Segmente ab und fügt sie zum Aufruf von Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics Audience Manager nicht auf, Daten weiterzuleiten, sodass keine doppelte Datenerfassung erfolgt. Bei Verwendung des Web SDK ist außerdem kein Standorthinweis erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.
