---
title: Identitätsdaten im Platform Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Cloud IDs (ECIDs) mit dem Adobe Experience Platform Web SDK abrufen und verwalten.
keywords: Identität; Erstanbieter-Identität; Identity-Dienst; Drittanbieter-Identität; ID-Migration; Besucher-ID; Drittanbieter-Identität; thirdPartyCookiesEnabled; idMigrationEnabled; getIdentity; Syncing Identities; syncIdentity; sendEvent; identityMap; primary; ecid; Identity-Namespace; Namespace-ID; authenticationState; hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 6fb6d1579f888720b6af9617400d512a68d06264
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 1%

---

# Identitätsdaten im Platform Web SDK

Das Adobe Experience Platform Web SDK nutzt [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/ecid.md) , um das Besucherverhalten zu verfolgen. Mithilfe von ECIDs können Sie sicherstellen, dass jedes Gerät über eine eindeutige ID verfügt, die über mehrere Sitzungen hinweg persistent sein kann, und alle Treffer, die während und über mehrere Websitzungen hinweg auftreten, an ein bestimmtes Gerät binden.

Dieses Dokument bietet einen Überblick darüber, wie ECIDs mit dem Platform Web SDK verwaltet werden.

## Tracking von ECIDs mit dem SDK

Das Platform Web SDK weist ECIDs mithilfe von Cookies zu und verfolgt sie mit verschiedenen Methoden, um zu konfigurieren, wie diese Cookies generiert werden.

Wenn ein neuer Benutzer auf Ihre Website gelangt, versucht Adobe Experience Cloud Identity Service, ein Cookie zur Identifizierung des Geräts für diesen Benutzer zu setzen. Bei erstmaligen Besuchern wird eine ECID generiert und in der ersten Antwort vom Adobe Experience Platform Edge Network zurückgegeben. Bei wiederkehrenden Besuchern wird die ECID aus dem `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -Cookie und zur Payload hinzugefügt.

Nachdem das Cookie mit der ECID gesetzt wurde, enthält jede nachfolgende vom Platform Web SDK generierte Anforderung die ECID.

Bei der Verwendung von Cookies zur Geräteerkennung haben Sie zwei Möglichkeiten, mit dem Edge Network zu interagieren:

1. Daten direkt an die Edge Network-Domäne senden `adobedc.net`. Diese Methode wird als [Datenerfassung von Drittanbietern](#third-party).
1. Erstellen Sie einen CNAME für Ihre eigene Domäne, der auf `adobedc.net`. Diese Methode wird als [Erstanbieter-Datenerfassung](#first-party).

Wie in den folgenden Abschnitten erläutert, wirkt sich die von Ihnen gewählte Datenerfassungsmethode direkt auf die Cookie-Lebensdauer in allen Browsern aus.

### Datenerfassung von Drittanbietern {#third-party}

Die Datenerfassung von Drittanbietern beinhaltet das direkte Senden von Daten an die Edge Network-Domäne `adobedc.net`.

In den letzten Jahren haben die Webbrowser bei der Behandlung von Cookies von Drittanbietern immer restriktiver werden. Einige Browser blockieren standardmäßig Drittanbieter-Cookies. Wenn Sie zur Identifizierung von Site-Besuchern Drittanbieter-Cookies verwenden, ist die Lebensdauer dieser Cookies fast immer kürzer, als dies sonst durch Erstanbieter-Cookies möglich wäre. In einigen Fällen läuft ein Drittanbieter-Cookie innerhalb von sieben Tagen ab.

Wenn die Datenerfassung von Drittanbietern verwendet wird, beschränken einige Anzeigensperren den Traffic außerdem vollständig auf die Datenerfassungs-Endpunkte der Adobe.

### Erstanbieter-Datenerfassung {#first-party}

Die Datenerfassung von Erstanbietern umfasst das Setzen von Cookies über einen CNAME in Ihrer eigenen Domäne, der auf Folgendes verweist: `adobedc.net`.

Während Browser Cookies, die von CNAME-Endpunkten gesetzt werden, seit langem ähnlich wie von Site-eigenen Endpunkten behandeln, haben kürzlich von Browsern implementierte Änderungen eine Unterscheidung in der Handhabung von CNAME-Cookies geschaffen. Es gibt zwar keine Browser, die standardmäßig Erstanbieter-CNAME-Cookies blockieren, aber einige Browser beschränken die Lebensdauer von Cookies, die mit einem CNAME gesetzt werden, auf nur sieben Tage.

### Auswirkungen von Cookie-Lebenszyklen auf Adobe Experience Cloud-Anwendungen {#lifespans}

Unabhängig davon, ob Sie die Datenerfassung von Erstanbietern oder Drittanbietern auswählen, hat die Dauer, die ein Cookie beibehalten werden kann, direkte Auswirkungen auf die Besucherzahlen in Adobe Analytics und Customer Journey Analytics. Darüber hinaus kann es bei Endbenutzern zu inkonsistenten Personalisierungserlebnissen kommen, wenn Adobe Target oder Offer decisioning auf der Site verwendet wird.

Angenommen, Sie haben ein Personalisierungs-Erlebnis erstellt, das jedes Element auf die Startseite weiterleitet, wenn ein Benutzer es in den letzten sieben Tagen dreimal angesehen hat.

Wenn ein Endbenutzer die Site dreimal in einer Woche besucht und dann sieben Tage lang nicht erneut aufruft, kann dieser Benutzer bei seiner Rückkehr zur Site als neuer Benutzer gelten, da seine Cookies möglicherweise von einer Browserrichtlinie gelöscht wurden (je nach dem Browser, den er bei seinem Besuch auf der Site verwendet hat). In diesem Fall behandelt Ihr Analytics-Tool den Besucher als neuen Benutzer, auch wenn er die Site vor etwas mehr als sieben Tagen besucht hat. Darüber hinaus beginnen alle Bemühungen, das Erlebnis für den Benutzer zu personalisieren, erneut.

### Erstanbieter-Geräte-IDs

Um die oben beschriebenen Auswirkungen von Cookie-Lebenszyklen zu berücksichtigen, können Sie stattdessen Ihre eigenen Geräte-IDs festlegen und verwalten. Siehe Handbuch unter [Erstanbieter-Geräte-IDs](./first-party-device-ids.md) für weitere Informationen.

## Abrufen der ECID und der Region für den aktuellen Benutzer

Um die eindeutige ECID für den aktuellen Besucher abzurufen, verwenden Sie die `getIdentity` Befehl. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID. `getIdentity` gibt auch die Regions-ID für den Besucher zurück.

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

`identityMap` -Felder werden mithilfe der `sentEvent` Befehl.

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

Jede Eigenschaft in `identityMap` stellt Identitäten dar, die zu einem bestimmten [Identitäts-Namespace](../../identity-service/namespaces.md). Der Eigenschaftsname sollte das Identitäts-Namespace-Symbol sein, das Sie in der Adobe Experience Platform-Benutzeroberfläche unter[!UICONTROL Identitäten]&quot;. Der Eigenschaftswert sollte ein Array von Identitäten sein, die sich auf diesen Identitäts-Namespace beziehen.

Jedes Identitätsobjekt im Identitäten-Array enthält die folgenden Eigenschaften:

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `id` | Zeichenfolge | **(Erforderlich)** Die ID, die Sie für den angegebenen Namespace festlegen möchten. |
| `authenticationState` | Zeichenfolge | **(Erforderlich)** Der Authentifizierungsstatus der ID. Zu den möglichen Werten gehören `ambiguous`, `authenticated` und `loggedOut`. |
| `primary` | Boolesch | Bestimmt, ob diese Identität als primäres Fragment im Profil verwendet werden soll. Standardmäßig wird die ECID als primäre Kennung für den Benutzer festgelegt. Wenn dieses Wert weggelassen wird, wird standardmäßig `false` verwendet. |

## Migration von der Besucher-API zur ECID

Bei der Migration von der Verwendung der Besucher-API können Sie auch vorhandene AMCV-Cookies migrieren. Um die ECID-Migration zu aktivieren, legen Sie die `idMigrationEnabled` -Parameter in der Konfiguration. Die ID-Migration ermöglicht die folgenden Anwendungsfälle:

* Wenn einige Seiten einer Domäne die Besucher-API verwenden und andere Seiten dieses SDK verwenden. Um dies zu unterstützen, liest das SDK vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der vorhandenen ECID. Darüber hinaus schreibt das SDK AMCV-Cookies so, dass nachfolgende Seiten, die mit der Besucher-API instrumentiert werden, dieselbe ECID haben, wenn die ECID zuerst auf einer mit dem SDK instrumentierten Seite abgerufen wird.
* Wenn das Adobe Experience Platform Web SDK auf einer Seite eingerichtet ist, die auch über eine Besucher-API verfügt. Wenn das AMCV-Cookie nicht gesetzt ist, sucht das SDK in diesem Fall nach der Besucher-API auf der Seite und ruft sie auf, um die ECID abzurufen.
* Wenn die gesamte Site das Adobe Experience Platform Web SDK verwendet und keine Besucher-API hat, ist es nützlich, die ECIDs zu migrieren, damit die zurückgegebenen Besucherinformationen beibehalten werden. Nach der Bereitstellung des SDK mit `idMigrationEnabled` für einen bestimmten Zeitraum, sodass die meisten Besucher-Cookies migriert werden, kann die Einstellung deaktiviert werden.

### Eigenschaften für die Migration aktualisieren

Wenn XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten bei der Migration in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen Schlüssel widerzuspiegeln, die XDM bereitstellt. Dieser Prozess wird durch die Verwendung der [BAAAM-Tool](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) Dieser Audience Manager hat erstellt.

## Verwendung in der Ereignisweiterleitung

Wenn Sie derzeit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) aktiviert sind und verwenden `appmeasurement.js` und `visitor.js`können Sie die Ereignisweiterleitungsfunktion aktivieren lassen, was keine Probleme verursacht. Am Backend ruft Adobe alle AAM Segmente ab und fügt sie zum Aufruf von Analytics hinzu. Wenn der Aufruf an Analytics diese Segmente enthält, ruft Analytics Audience Manager nicht auf, Daten weiterzuleiten, sodass keine doppelte Datenerfassung erfolgt. Bei Verwendung des Web SDK ist außerdem kein Standorthinweis erforderlich, da dieselben Segmentierungsendpunkte im Backend aufgerufen werden.
