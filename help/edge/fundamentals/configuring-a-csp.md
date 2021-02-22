---
title: Konfigurieren eines CSP
seo-title: Konfigurieren eines CSP für Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie einen CSP für das Web SDK der Experience Platform konfigurieren.
seo-description: Erfahren Sie, wie Sie einen CSP für das Web SDK der Experience Platform konfigurieren.
keywords: configuring;configuration;SDK;edge;Web SDK;configure;context;web;device;Umgebung;Web-SDK-Einstellungen;Content-Sicherheitsrichtlinie
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# Konfigurieren eines CSP

Eine [Content Security Policy](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wird verwendet, um die Ressourcen einzuschränken, die ein Browser verwenden darf. Der CSP kann auch die Funktionalität von Skript- und Stilressourcen einschränken. Adobe Experience Platform Web SDK benötigt keinen CSP, aber das Hinzufügen eines CSP kann die Angriffsfläche verringern, um böswillige Angriffe zu verhindern.

Das CSP muss die Bereitstellung und Konfiguration von [!DNL Platform Web SDK] widerspiegeln. Die folgende CSP zeigt, welche Änderungen erforderlich sein können, damit das SDK ordnungsgemäß funktioniert. Je nach Umgebung sind wahrscheinlich zusätzliche CSP-Einstellungen erforderlich.

## Beispiel für eine Content-Sicherheitsrichtlinie

Die folgenden Beispiele zeigen, wie ein CSP konfiguriert wird.

### Zugriff auf die Edge-Domäne zulassen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Im obigen Beispiel sollte `EDGE-DOMAIN` durch die Erstanbieterdomäne ersetzt werden. Die Erstanbieterdomäne ist für die Einstellung [edgeDomain](configuring-the-sdk.md#edge-domain) konfiguriert. Wenn keine Erstanbieterdomäne konfiguriert wurde, sollte `EDGE-DOMAIN` durch `*.adobedc.net` ersetzt werden. Wenn die Migration von Besuchern mit [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled) aktiviert ist, muss die `connect-src`-Direktive auch `*.demdex.net` enthalten.

### Verwenden Sie NONCE, um Inline-Skript- und Stilelemente zuzulassen

[!DNL Platform Web SDK] können den Seiteninhalt ändern und müssen genehmigt werden, um Inline-Skript- und Stil-Tags zu erstellen. Um dies zu erreichen, empfiehlt Adobe die Verwendung einer nonce für die CSP-Direktive [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Eine Nonce ist ein servergeneriertes, kryptografisch starkes, zufälliges Token, das einmal pro Ansicht der einzelnen Seiten generiert wird.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Darüber hinaus muss die CSP nonce als Attribut zum Skript-Tag [!DNL Platform Web SDK] [base code](installing-the-sdk.md#adding-the-code) hinzugefügt werden. [!DNL Platform Web SDK] verwendet dann diese nonce, wenn Inline-Skript- oder Stil-Tags zur Seite hinzugefügt werden:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Wenn keine Nonce verwendet wird, besteht die andere Option darin, `unsafe-inline` den CSP-Direktiven `script-src` und `style-src` hinzuzufügen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Die Adobe empfiehlt die Angabe von **nicht**, da sie die Ausführung eines Skripts auf der Seite zulässt, wodurch die Vorteile des CSP eingeschränkt werden.`unsafe-inline`
