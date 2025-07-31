---
title: Konfigurieren eines CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie eine CSP für die Experience Platform Web SDK konfigurieren
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: Konfigurieren;Konfiguration;SDK;Edge;Web SDK;Konfigurieren;Kontext;Web;Gerät;Umgebung;Web SDK-Einstellungen;Inhaltssicherheitsrichtlinie;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Konfigurieren eines CSP

Eine [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wird verwendet, um die Ressourcen einzuschränken, die ein Browser verwenden darf. Der CSP kann auch die Funktionalität von Skript- und Stilressourcen einschränken. Adobe Experience Platform Web SDK erfordert keine CSP, aber das Hinzufügen einer CSP kann die Angriffsfläche reduzieren, um vor böswilligen Angriffen zu schützen.

Das CSP muss widerspiegeln, wie [!DNL Experience Platform Web SDK] bereitgestellt und konfiguriert wird. Das folgende CSP zeigt, welche Änderungen erforderlich sein können, damit SDK ordnungsgemäß funktioniert. Abhängig von Ihrer spezifischen Umgebung sind wahrscheinlich zusätzliche CSP-Einstellungen erforderlich.

## Beispiel für eine Content Security-Richtlinie

Die folgenden Beispiele zeigen, wie Sie einen CSP konfigurieren.

### Zugriff auf die Edge-Domain zulassen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Im obigen Beispiel sollte `EDGE-DOMAIN` durch die Erstanbieter-Domain ersetzt werden. Die Erstanbieterdomäne ist für die Einstellung [edgeDomain](../commands/configure/edgedomain.md) konfiguriert. Wenn keine Erstanbieterdomäne konfiguriert wurde, sollte `EDGE-DOMAIN` durch `*.adobedc.net` ersetzt werden. Wenn die Besuchermigration mit [idMigrationEnabled](../commands/configure/idmigrationenabled.md) aktiviert ist, muss die `connect-src`-Anweisung auch `*.demdex.net` enthalten.

### Verwenden Sie NONCE, um Inline-Skript- und Stilelemente zuzulassen.

[!DNL Experience Platform Web SDK] können Seiteninhalte ändern und müssen genehmigt werden, um Inline-Skript- und Stil-Tags zu erstellen. Zu diesem Zweck empfiehlt Adobe die Verwendung einer Nonce für die CSP[Direktive ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src)default-src. Eine Nonce ist ein vom Server generiertes kryptografisch starkes Zufallstoken, das einmal pro eindeutiger Seitenansicht generiert wird.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Darüber hinaus muss die CSP-Nonce dem Skript-Tag [!DNL Experience Platform Web SDK]Basis[ als ](../install/library.md) hinzugefügt werden. [!DNL Experience Platform Web SDK] verwenden diese Nonce dann, wenn Inline-Skript- oder Stil-Tags zur Seite hinzugefügt werden:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Wenn keine Nonce verwendet wird, besteht die andere Option darin, `unsafe-inline` zu den `script-src`- und `style-src` CSP-Anweisungen hinzuzufügen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe empfiehlt **nicht** die Angabe von `unsafe-inline`, da dies die Ausführung jedes Skripts auf der Seite ermöglicht, was die Vorteile des CSP einschränkt.

## Konfigurieren eines CSP für In-App-Messaging {#in-app-messaging}

Beim Konfigurieren von [Web-In-App](../personalization/web-in-app-messaging.md)Messaging) müssen Sie die folgende Anweisung in Ihr CSP aufnehmen:

```
default-src  blob:;
```
