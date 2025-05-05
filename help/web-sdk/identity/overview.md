---
title: Identitätsdaten in Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Cloud IDs (ECIDs) mit der Adobe Experience Platform Web SDK abrufen und verwalten.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 3724c43090e37d21384e9dfe45e60ee2eec68a81
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 1%

---


# Identitätsdaten in Web SDK

Adobe Experience Platform Web SDK verwendet [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/features/ecid.md) um das Besucherverhalten zu verfolgen. Mit [!DNL ECIDs] können Sie sicherstellen, dass jedes Gerät über eine eindeutige Kennung verfügt, die sitzungsübergreifend beibehalten werden kann. So können Sie alle Treffer, die während und über Web-Sitzungen hinweg auftreten, mit einem bestimmten Gerät verknüpfen.

Dieses Dokument bietet einen Überblick darüber, wie Sie [!DNL ECIDs] und [!DNL CORE IDs] mit der Web SDK verwalten.

## Tracking von ECIDs mit Web SDK {#tracking-ecids-web-sdk}

Web SDK weist [!DNL ECIDs] mithilfe von Cookies zu und verfolgt diese. Dabei stehen mehrere Methoden zur Konfiguration der Erstellung dieser Cookies zur Verfügung.

Wenn ein neuer Benutzer auf Ihre Website gelangt, versucht der [Adobe Experience Cloud Identity Service](../../identity-service/home.md), ein Gerätekennungs-Cookie für diesen Benutzer zu setzen.

* Bei Erstbesuchern wird eine [!DNL ECID] generiert und in der ersten Antwort vom Experience Platform-Edge Network zurückgegeben.
* Bei zurückkehrenden Besuchern wird die [!DNL ECID] aus dem `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`-Cookie abgerufen und vom -Edge Network zur Anfrage-Payload hinzugefügt.

Nachdem das Cookie, das die [!DNL ECID] enthält, gesetzt wurde, enthält jede nachfolgende, von der Web-SDK generierte Anfrage eine codierte [!DNL ECID] im `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`-Cookie.

Bei der Verwendung von Cookies zur Geräte-Identifizierung haben Sie zwei Möglichkeiten, mit dem Edge Network zu interagieren:

1. Erstellen Sie einen CNAME in Ihrer eigenen Domain, der auf `adobedc.net` verweist. Diese Methode wird als [Erstanbieter-Datenerfassung“ ](#first-party).
1. Senden Sie Daten direkt an die Edge Network-Domain `adobedc.net`. Diese Methode wird als [Datenerfassung von Drittanbietern“ ](#third-party).

Wie in den folgenden Abschnitten erläutert, hat die von Ihnen gewählte Datenerfassungsmethode direkte Auswirkungen auf die Cookie-Lebensdauer in allen Browsern.

## Tracking von CORE-IDs mit Web SDK {#tracking-coreid-web-sdk}

Wenn Sie Google Chrome mit aktivierten Drittanbieter-Cookies verwenden und kein `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`-Cookie gesetzt ist, wird die erste Edge Network-Anfrage über eine `demdex.net`-Domain gesendet, die ein demdex-Cookie setzt. Dieses Cookie enthält eine [!DNL CORE ID]. Dies ist eine eindeutige Benutzer-ID, die sich von der [!DNL ECID] unterscheidet.

Abhängig von Ihrer -Implementierung möchten Sie möglicherweise auf [zugreifen [!DNL CORE ID]](#retrieve-coreid).

### Erstanbieter-Datenerfassung {#first-party}

Bei der Erstanbieter-Datenerfassung werden Cookies über eine `CNAME` in Ihrer eigenen Domain gesetzt, die auf `adobedc.net` verweist.

Während Browser Cookies, die von `CNAME`-Endpunkten gesetzt werden, seit langem ähnlich wie diejenigen behandeln, die von Website-eigenen Endpunkten gesetzt werden, haben jüngste von Browsern implementierte Änderungen zu einem Unterschied bei der Verarbeitung `CNAME` Cookies geführt. Es gibt zwar keine Browser, die derzeit standardmäßig Erstanbieter-`CNAME`-Cookies blockieren, aber einige Browser beschränken die Lebensdauer von Cookies, die mit einem `CNAME` gesetzt werden, auf nur sieben Tage.

### Datenerfassung durch Dritte {#third-party}

Die Datenerfassung von Drittanbietern umfasst das direkte Senden von Daten an die Edge Network-Domain `adobedc.net`.

In den letzten Jahren wurden Webbrowser immer restriktiver in ihrer Handhabung von Cookies, die von Dritten gesetzt werden. Einige Browser blockieren standardmäßig Cookies von Drittanbietern. Wenn Sie Drittanbieter-Cookies verwenden, um Besucher der Website zu identifizieren, ist die Lebensdauer dieser Cookies fast immer kürzer als die, die andernfalls mit Erstanbieter-Cookies verfügbar wären. Manchmal läuft ein Drittanbieter-Cookie in nur sieben Tagen ab.

Bei der Verwendung der Datenerfassung von Drittanbietern beschränken einige Anzeigenblocker den Traffic außerdem vollständig auf Adobe-Datenerfassungsendpunkte.

### Auswirkungen der Cookie-Lebensdauer auf Adobe Experience Cloud-Anwendungen {#lifespans}

Unabhängig davon, ob Sie die Datenerfassung von Erstanbietern oder Drittanbietern auswählen, wirkt sich die Dauer, während der ein Cookie bestehen kann, direkt auf die Besucherzahlen in [Adobe Analytics](https://experienceleague.adobe.com/de/docs/analytics) und [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/customer-journey-analytics) aus. Außerdem kann es bei Endbenutzern zu inkonsistenten Personalisierungserlebnissen kommen, wenn [Adobe TargetOffer decisioning ](https://experienceleague.adobe.com/de/docs/target) oder [&#128279;](https://experienceleague.adobe.com/de/docs/target/using/integrate/ajo/offer-decision) auf der Website verwendet werden.

Stellen Sie sich beispielsweise eine Situation vor, in der Sie ein Personalisierungserlebnis erstellt haben, das jedes Element auf die Startseite höher stuft, wenn ein Benutzer es in den letzten sieben Tagen dreimal angesehen hat.

Wenn ein Endbenutzer dreimal in der Woche die Website besucht und dann sieben Tage lang nicht zu ihr zurückkehrt, kann dieser Benutzer bei der Rückkehr zur Website als neuer Benutzer betrachtet werden, da seine Cookies möglicherweise durch eine Browser-Richtlinie gelöscht wurden (je nach Browser, den er beim Besuch der Website verwendet hat). In diesem Fall behandelt Ihr Analytics-Tool den Besucher als neuen Benutzer, obwohl er die Website erst vor etwas mehr als sieben Tagen besucht hat. Außerdem beginnt jeder Versuch, das Erlebnis für den Benutzer zu personalisieren, wieder.

### First-Party-Geräte-IDs (FPIDs) {#fpid}

Um die Auswirkungen der Cookie-Lebensdauern wie oben beschrieben zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Weitere Informationen finden Sie im Leitfaden zu [IDs von Erstanbieter-Geräten](./first-party-device-ids.md).

## Abrufen der ECID und Region für den aktuellen Benutzer {#retrieve-ecid}

Je nach Anwendungsfall gibt es zwei Möglichkeiten, auf die [!DNL ECID] zuzugreifen:

* [Abrufen der  [!DNL ECID]  durch die Datenvorbereitung für ](#retrieve-ecid-data-prep): Dies ist die empfohlene Methode.
* [Abrufen der  [!DNL ECID]  über den `getIdentity()`-Befehl](#retrieve-ecid-getidentity): Verwenden Sie diese Methode nur, wenn Sie die [!DNL ECID] Informationen Client-seitig benötigen.

### Abrufen der [!DNL ECID] durch die Datenvorbereitung für die Datenerfassung {#retrieve-ecid-data-prep}

Verwenden [Datenvorbereitung für die Datenerfassung](../../datastreams/data-prep.md) um die [!DNL ECID] einem [!DNL XDM] zuzuordnen. Dies ist die empfohlene Methode für den Zugriff auf die [!DNL ECID].

Legen Sie dazu das Quellfeld auf den folgenden Pfad fest:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Zielfeld auf einen XDM-Pfad fest, in dem das Feld vom Typ `string` ist.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Rufen Sie die [!DNL ECID] über den `getIdentity()`-Befehl ab {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Sie sollten die ECID nur über den `getIdentity()`-Befehl abrufen, wenn Sie die [!DNL ECID] auf Client-Seite benötigen. Wenn Sie die ECID nur einem XDM-Feld zuordnen möchten, verwenden Sie [Datenvorbereitung für die Datenerfassung](#retrieve-ecid-data-prep).

Um die eindeutige ECID für den aktuellen Besucher abzurufen, verwenden Sie den `getIdentity`. Für erstmalige Besucherinnen und Besucher, die noch keine [!DNL ECID] haben, generiert dieser Befehl eine neue [!DNL ECID]. `getIdentity` gibt auch die Regions-ID für den Besucher zurück.

>[!NOTE]
>
>Diese Methode wird normalerweise mit benutzerdefinierten Lösungen verwendet, für die das Lesen der [!DNL Experience Cloud]-ID oder ein Standorthinweis für Adobe Audience Manager erforderlich ist. Sie wird nicht von einer Standardimplementierung verwendet.

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

Um die CORE-ID für einen Benutzer abzurufen, können Sie den [`getIdentity()`](../commands/getidentity.md)-Befehl verwenden, wie unten dargestellt.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## Verwenden `identityMap` {#using-identitymap}

Mithilfe eines XDM-[`identityMap` können ](../../xdm/schema/composition.md#identityMap) ein Gerät/einen Benutzer mithilfe mehrerer Identitäten identifizieren, seinen Authentifizierungsstatus festlegen und entscheiden, welche Kennung als die primäre Kennung betrachtet wird. Wenn keine Kennung als `primary` festgelegt wurde, ist standardmäßig die `ECID` die primäre Kennung.

`identityMap` Felder werden mithilfe des Befehls `sentEvent` aktualisiert.

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
>Adobe empfiehlt, Namespaces zu senden, die eine Person darstellen, z. B. `CRMID`, als primäre Identität.


Jede Eigenschaft in `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identity-Namespace) ](../../identity-service/features/namespaces.md). Der Eigenschaftsname sollte das Identity-Namespace-Symbol sein, das in der Benutzeroberfläche von Adobe Experience Platform unter „Identitäten[!UICONTROL &#x200B; aufgeführt &#x200B;]. Der Eigenschaftswert sollte ein Array von Identitäten sein, die zu diesem Identity-Namespace gehören.

>[!IMPORTANT]
>
>Bei der in der `identityMap` übergebenen Namespace-ID wird zwischen Groß- und Kleinschreibung unterschieden. Stellen Sie sicher, dass Sie die richtige Namespace-ID verwenden, um eine unvollständige Datenerfassung zu vermeiden.

Jedes Identitätsobjekt im Identitäts-Array enthält die folgenden Eigenschaften:

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | **(Erforderlich)** Die ID, die Sie für den angegebenen Namespace festlegen möchten. |
| `authenticatedState` | String | **(Erforderlich)** Der Authentifizierungsstatus der ID. Zu den möglichen Werten gehören `ambiguous`, `authenticated` und `loggedOut`. |
| `primary` | Boolesch | Legt fest, ob diese Identität als primäres Fragment im Profil verwendet werden soll. Standardmäßig wird die ECID als primäre Kennung für den Benutzer festgelegt. Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |

Die Verwendung des Felds `identityMap` zur Identifizierung von Geräten oder Benutzern führt zum gleichen Ergebnis wie die Verwendung der [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=de) Methode aus der [!DNL ID Service API]. Weitere Informationen finden Sie in der [ID-Service](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html?lang=de)API-Dokumentation .

## Migration von der Besucher-API zu ECID {#migrating-visitor-api-ecid}

Bei der Migration von mit der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie den `idMigrationEnabled` in der Konfiguration fest. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn auf einigen Seiten einer Domain die Besucher-API und auf anderen Seiten diese SDK verwendet wird. Um diesen Fall zu unterstützen, liest der SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Außerdem schreibt der SDK AMCV-Cookies, sodass nachfolgende Seiten, die mit der Besucher-API instrumentiert werden, dieselbe ECID aufweisen, wenn die ECID zuerst auf einer mit der SDK instrumentierten Seite abgerufen wird.
* Wenn Adobe Experience Platform Web SDK auf einer Seite eingerichtet wird, die auch über eine Besucher-API verfügt. Ist das AMCV-Cookie nicht gesetzt, sucht der SDK daher auf der Seite nach der Besucher-API und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site Adobe Experience Platform Web SDK verwendet und nicht über eine Besucher-API verfügt, ist es nützlich, die ECIDs zu migrieren, damit die zurückgegebenen Besucherinformationen beibehalten werden. Nachdem SDK einige Zeit mit `idMigrationEnabled` bereitgestellt wurde, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

### Aktualisieren von Eigenschaften für die Migration

Wenn XDM-formatierte Daten an den Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale umgewandelt werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Prozess wird durch die Verwendung des [BAAAM-Tools](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=de#getting-started-with-bulk-management) das der Audience Manager erstellt hat, erleichtert.

## Verwendung bei der Ereignisweiterleitung

Wenn Sie derzeit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) aktiviert haben und `appmeasurement.js` und `visitor.js` verwenden, können Sie die Ereignisweiterleitungsfunktion aktiviert lassen, was keine Probleme verursacht. Am Back-End ruft Adobe alle AAM-Segmente ab und fügt sie dem Aufruf an Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics den Audience Manager nicht auf, um Daten weiterzuleiten, sodass keine doppelte Datenerfassung erfolgt. Bei Verwendung der Web-SDK ist auch kein Standorthinweis erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.
