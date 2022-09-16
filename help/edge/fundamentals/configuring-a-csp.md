---
title: Konfigurieren einer CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie eine CSP für das Experience Platform Web SDK konfigurieren.
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: Konfigurieren; Konfiguration; SDK; Edge; Web SDK; konfigurieren; Kontext; Web; Gerät; Umgebung; Web SDK-Einstellungen; Content Security-Richtlinie
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Konfigurieren einer CSP

A [Inhaltssicherheitsrichtlinie](https://developer.mozilla.org/de-DE/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wird verwendet, um die Ressourcen zu beschränken, die ein Browser verwenden darf. Die CSP kann auch die Funktionalität von Skript- und Stilressourcen einschränken. Das Adobe Experience Platform Web SDK benötigt keine CSP. Durch Hinzufügen einer kann die Angriffsfläche jedoch reduziert werden, um schädliche Angriffe zu verhindern.

Das CSP muss reflektieren, wie [!DNL Platform Web SDK] bereitgestellt und konfiguriert wurde. Die folgende CSP zeigt, welche Änderungen erforderlich sein können, damit das SDK ordnungsgemäß funktioniert. Abhängig von Ihrer spezifischen Umgebung sind wahrscheinlich zusätzliche CSP-Einstellungen erforderlich.

## Beispiel für eine Content-Sicherheitsrichtlinie

Die folgenden Beispiele zeigen, wie Sie eine CSP konfigurieren.

### Zugriff auf die Edge-Domäne zulassen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Im obigen Beispiel `EDGE-DOMAIN` durch die Erstanbieterdomäne ersetzt werden. Die Erstanbieterdomäne ist für die [edgeDomain](configuring-the-sdk.md#edge-domain) -Einstellung. Wenn keine Erstanbieterdomäne konfiguriert wurde, wird `EDGE-DOMAIN` sollte ersetzt werden durch `*.adobedc.net`. Wenn die Besuchermigration mit [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), die `connect-src` auch `*.demdex.net`.

### Verwenden Sie NONCE, um Inline-Skript- und Stilelemente zuzulassen

[!DNL Platform Web SDK] kann den Seiteninhalt ändern und muss genehmigt werden, um Inline-Skript- und Stil-Tags zu erstellen. Um dies zu erreichen, empfiehlt Adobe die Verwendung einer Nonce für die [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP-Richtlinie. Eine Nonce ist ein Server-generiertes kryptografisch starkes zufälliges Token, das einmal pro eindeutigem Seitenaufruf generiert wird.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Darüber hinaus muss die CSP-Nonce als Attribut zum [!DNL Platform Web SDK] [Basis-Code](installing-the-sdk.md#adding-the-code) Skript-Tag. [!DNL Platform Web SDK] verwendet diese Nonce dann, wenn Inline-Skript- oder Stil-Tags zur Seite hinzugefügt werden:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Wenn keine Nonce verwendet wird, besteht die andere Option darin, `unsafe-inline` der `script-src` und `style-src` CSP-Anweisungen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe tut **not** empfehlen `unsafe-inline` weil es ermöglicht, dass jedes Skript auf der Seite ausgeführt wird, wodurch die Vorteile des CSP eingeschränkt werden.
