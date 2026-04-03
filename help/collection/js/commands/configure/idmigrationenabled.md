---
title: idMigrationEnabled
description: Ermöglicht dem Web-SDK, AMCV-Cookies zu lesen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

Die `idMigrationEnabled`-Eigenschaft ermöglicht es dem Web-SDK, AMCV-Cookies zu lesen, die von vorherigen Adobe Experience Cloud-Implementierungen festgelegt wurden. Wenn Ihr Unternehmen Ihre Implementierung auf Web SDK aktualisiert, ermöglicht diese Einstellung einen reibungsloseren Übergang zum aktuellen Adobe Experience Cloud ID-Service. Diese Einstellung ist nützlich, damit beim Upgrade auf Web SDK keine starke Zunahme von Unique Visitors auftritt.

Wenn Ihr Unternehmen eine neue Web SDK-Implementierung ausführt, hat die Aktivierung dieser Einstellung keine Auswirkungen auf die Datenerfassung oder Besucheridentifizierung. Es hat keine Nachteile, wenn es für alle Implementierungen aktiviert bleibt.

## Funktionsweise der Identitätsmigration {#how-it-works}

Die Besucher-API speichert die Experience Cloud-ID (ECID) in einem Cookie namens `AMCV_<ORG_ID>`. Wenn `idMigrationEnabled` (Standard) `true` ist, liest Web SDK automatisch die ECID aus dem AMCV-Cookie und verwendet sie bei der ersten Edge Network-Anfrage als Besucheridentität.

1. Ein Besucher gelangt auf eine Seite, die jetzt Web SDK anstelle der Besucher-API verwendet.
1. Web SDK sucht nach einem vorhandenen `kndctr_`-Identitäts-Cookie (seinem eigenen Cookie-Format). Wenn kein Cookie gefunden wird, wird nach einem `AMCV_` Cookie gesucht.
1. Wenn ein `AMCV_` Cookie gefunden wird, extrahiert Web SDK die ECID und verwendet sie, um die Besucheridentität zu initialisieren.
1. Web SDK setzt ein neues `kndctr_`-Identitäts-Cookie mit derselben ECID.
1. Bei nachfolgenden Besuchen verwendet Web SDK das `kndctr_`-Cookie direkt. Das `AMCV_`-Cookie wird nicht mehr benötigt.

Damit die Migration funktioniert, muss die Web-SDK mit demselben [`orgId`](/help/collection/js/commands/configure/orgid.md) konfiguriert werden, den die Besucher-API verwendet hat, und muss in derselben Domain (oder einer Subdomain derselben übergeordneten Domain) bereitgestellt werden, in der das AMCV-Cookie gesetzt wurde.

## Unterstützte Migrationsszenarien

Die ID-Migration unterstützt die folgenden Übergangsmuster:

* **Einige Seiten verwenden weiterhin die Besucher-API, während andere Seiten Web SDK verwenden**: Die SDK liest vorhandene AMCV-Cookies und schreibt ein neues Cookie mit der bestehenden ECID. AMCV-Cookies werden auch so geschrieben, dass Seiten, die noch die Besucher-API verwenden, weiterhin denselben Besucher erkennen.
* **Web-SDK und Besucher-API sind beide auf derselben Seite vorhanden**: Wenn das AMCV-Cookie nicht gesetzt ist, sucht die SDK auf der Seite nach der Besucher-API und verwendet diese, um die ECID abzurufen.
* **Die Website wurde vollständig in Web SDK verschoben**: Sie können die Migration für einen bestimmten Zeitraum aktiviert lassen, sodass bestehende AMCV-basierte Besucherinnen und Besucher die Kontinuität behalten, während ihre Cookies übergeben werden.

>[!IMPORTANT]
>
>Laden Sie die Besucher-API und die Web-SDK nicht gleichzeitig auf dieselbe Seite, es sei denn, Sie haben bestätigt, dass das AMCV-Cookie bereits gesetzt ist. Die Ausführung beider Bibliotheken auf einer einzelnen Seite kann Racebedingungen verursachen, bei denen jede Bibliothek versucht, Identität unabhängig zu verwalten, was möglicherweise doppelte oder widersprüchliche ECIDs erzeugt.

## Deaktivieren der Migration {#turn-off-migration}

Nachdem Ihre gesamte Site auf der Web-SDK ausgeführt wird und keine Besuchenden nur ein `AMCV_` Cookie ohne das entsprechende `kndctr_`-Cookie mit sich führen, können Sie die Identitätsmigration sicher deaktivieren, indem Sie `idMigrationEnabled` auf `false` setzen. Dies ist eine geringfügige Leistungsoptimierung und reduziert die Oberfläche Ihrer Identitätslogik.

Warten Sie als Richtlinie, bis die maximale Lebensdauer des AMCV-Cookies nach der Migration der letzten Seite abgelaufen ist. Wenn Ihre AMCV-Cookies zwei Jahre ablaufen, warten Sie zwei Jahre, nachdem die letzte Seite an die Web-SDK übergeben wurde. In der Praxis deaktivieren die meisten Unternehmen die Migration früher (nach einigen Monaten) und akzeptieren eine zu vernachlässigende Inflation durch die geringe Anzahl von Besuchern, die nach langer Abwesenheit zum ersten Mal zurückkehren.

## Audience Manager-Eigenschaftsaktualisierungen

Wenn während der Migration XDM-formatierte Daten an Audience Manager gesendet werden, müssen diese Daten in Signale konvertiert werden. Ihre Eigenschaften müssen aktualisiert werden, um die neuen, von XDM bereitgestellten Schlüssel widerzuspiegeln. Dieser Prozess wird durch die Verwendung des [BAAAM-Tools](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) vereinfacht.

## Migration der Drittanbieter-ID {#third-party-id}

Wenn Ihre Besucher-API-Implementierung Drittanbieter-IDs (das `demdex.net`-Cookie) verwendet, kann die Web-SDK diese ebenfalls migrieren. Konfigurieren Sie [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) für `true` in Ihrer Web SDK-Konfiguration. Web SDK liest das vorhandene Demdex-Cookie und fügt die Drittanbieteridentität in seine Edge Network-Anfragen ein, wobei demselben Migrationsmuster wie das AMCV-Cookie gefolgt wird.

## Validierung {#validation}

So überprüfen Sie, ob die Identitätsmigration ordnungsgemäß funktioniert:

1. Öffnen Sie eine Seite, die zuvor die Besucher-API verwendet hat (jetzt unter Verwendung der Web-SDK), in einem Browser, der über ein `AMCV_`-Cookie verfügt.
2. Stellen Sie in den Entwickler-Tools sicher, dass ein `kndctr_` Identitäts-Cookie gesetzt wurde und dass die ECID mit der im `AMCV_`-Cookie übereinstimmt.
3. Vergleichen Sie nach der Bereitstellung die Zahlen der Unique Visitors vor und nach der Migration für denselben Zeitraum. Ein deutlicher Anstieg der Unique Visitors kann darauf hinweisen, dass die Migration keine Identitäten weiterträgt.

>[!TIP]
>
>Verwenden Sie `getIdentity` , um die ECID zum Vergleich programmgesteuert abzurufen:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Konfigurieren `idMigrationEnabled` {#configure}

Legen Sie beim Ausführen des `idMigrationEnabled`-Befehls den booleschen Wert `configure` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diese Eigenschaft fest, wenn Sie die Möglichkeit deaktivieren möchten, AMCV-Cookies zu lesen, die von der Besucher-API festgelegt werden. Die meisten Organisationen müssen diese Eigenschaft nicht festlegen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Aktivieren der Migration von Besucher-IDs mithilfe der Tag-Erweiterung von Web SDK

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Identitätskonfigurationseinstellungen](/help/tags/extensions/client/web-sdk/configure/identity.md) konfiguriert werden.
