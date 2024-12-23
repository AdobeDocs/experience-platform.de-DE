---
title: Konfigurieren einer CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie eine CSP für das Experience Platform Web SDK konfigurieren
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: Konfigurieren; Konfiguration; SDK; Edge; Web SDK; konfigurieren; Kontext; Web; Gerät; Umgebung; Web SDK-Einstellungen; Content Security-Richtlinie
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Konfigurieren einer CSP

Eine [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wird verwendet, um die Ressourcen zu beschränken, die ein Browser verwenden darf. Die CSP kann auch die Funktionalität von Skript- und Stilressourcen einschränken. Das Adobe Experience Platform Web SDK benötigt keine CSP. Durch Hinzufügen einer kann die Angriffsfläche jedoch reduziert werden, um schädliche Angriffe zu verhindern.

Das CSP muss die Bereitstellung und Konfiguration von [!DNL Platform Web SDK] widerspiegeln. Die folgende CSP zeigt, welche Änderungen erforderlich sein können, damit das SDK ordnungsgemäß funktioniert. Abhängig von Ihrer spezifischen Umgebung sind wahrscheinlich zusätzliche CSP-Einstellungen erforderlich.

## Beispiel für eine Content-Sicherheitsrichtlinie

Die folgenden Beispiele zeigen, wie Sie eine CSP konfigurieren.

### Zugriff auf die Edge-Domäne zulassen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Im obigen Beispiel sollte `EDGE-DOMAIN` durch die Erstanbieterdomäne ersetzt werden. Die Erstanbieterdomäne ist für die Einstellung [edgeDomain](../commands/configure/edgedomain.md) konfiguriert. Wenn keine Erstanbieterdomäne konfiguriert wurde, sollte `EDGE-DOMAIN` durch `*.adobedc.net` ersetzt werden. Wenn die Besuchermigration mit [idMigrationEnabled](../commands/configure/idmigrationenabled.md) aktiviert ist, muss die `connect-src` -Direktive auch `*.demdex.net` enthalten.

### Verwenden Sie NONCE, um Inline-Skript- und Stilelemente zuzulassen

[!DNL Platform Web SDK] kann den Seiteninhalt ändern und muss genehmigt werden, um Inline-Skript- und Stil-Tags zu erstellen. Um dies zu erreichen, empfiehlt Adobe die Verwendung einer Nonce für die CSP-Direktive [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) . Eine Nonce ist ein Server-generiertes kryptografisch starkes zufälliges Token, das einmal pro eindeutigem Seitenaufruf generiert wird.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Darüber hinaus muss die CSP-Nonce als Attribut zum Skript-Tag [!DNL Platform Web SDK] [Basis-Code](../install/library.md) hinzugefügt werden. [!DNL Platform Web SDK] verwendet diese Nonce dann beim Hinzufügen von Inline-Skript- oder Stil-Tags zur Seite:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Wenn keine Nonce verwendet wird, besteht die andere Option darin, der CSP-Direktive `script-src` und `style-src` den Wert `unsafe-inline` hinzuzufügen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe empfiehlt **nicht**, `unsafe-inline` anzugeben, da es die Ausführung eines Skripts auf der Seite ermöglicht, wodurch die Vorteile des CSP eingeschränkt werden.

## CSP für In-App-Nachrichten konfigurieren {#in-app-messaging}

Wenn Sie [Web In-App Messaging](../personalization/web-in-app-messaging.md) konfigurieren, müssen Sie die folgende Anweisung in Ihre CSP aufnehmen:

```
default-src  blob:;
```
