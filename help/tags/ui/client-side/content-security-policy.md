---
title: Unterstützung einer Content Security Policy (CSP)
description: Erfahren Sie, wie Sie bei der Integration Ihrer Website mit Tags in Adobe Experience Platform mit Einschränkungen der Content Security Policy (CSP) umgehen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 59%

---

# Unterstützung einer Content Security Policy (CSP)

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Eine Content Security Policy (CSP) ist eine Sicherheitsfunktion, die Cross-Site-Scripting-Angriffe (XSS) verhindert. Dies geschieht, wenn der Browser dazu gebracht wird, schädliche Inhalte auszuführen, die scheinbar von einer vertrauenswürdigen Quelle stammen, aber tatsächlich von einer anderen Quelle stammen. Mit CSPs kann der Browser (im Namen des Benutzers) überprüfen, ob das Skript tatsächlich von einer vertrauenswürdigen Quelle stammt.

CSPs werden implementiert, indem Sie Ihren Server-Antworten einen `Content-Security-Policy`-HTTP-Header hinzufügen oder indem Sie ein konfiguriertes `<meta>`-Element im `<head>`-Abschnitt Ihrer HTML-Dateien hinzufügen.

>[!NOTE]
>
> Weitere Informationen zu CSP finden Sie in den [MDN-Webdocs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

Tags in Adobe Experience Platform sind ein Tag-Management-System, mit dem Skripte dynamisch auf Ihre Website geladen werden können. Eine Standard-CSP blockiert diese dynamisch geladenen Skripte aufgrund potenzieller Sicherheitsprobleme. Dieses Dokument enthält Anleitungen zum Konfigurieren Ihrer CSP, um dynamisch geladene Skripte von Tags zu ermöglichen.

Wenn Sie möchten, dass Tags mit Ihrem CSP zusammenarbeiten, müssen Sie sicherstellen, dass zwei Voraussetzungen erfüllt sind:

* **Die Quelle für Ihre Tag-Bibliothek muss als vertrauenswürdig eingestuft werden.** Wenn diese Bedingung nicht erfüllt ist, werden die Tag-Bibliothek und andere erforderliche JavaScript-Dateien vom Browser blockiert und nicht auf der Seite geladen.
* **Inline-Skripte müssen erlaubt sein.** Wenn diese Bedingung nicht erfüllt ist, werden auf Regeln von benutzerspezifischem Code basierende Aktionen auf der Seite blockiert und nicht ordnungsgemäß ausgeführt.

Erhöhte Sicherheit erfordert ein höheres Arbeitsvolumen im Auftrag des Erstellers von Inhalten. Wenn Sie Tags verwenden möchten und ein CSP vorhanden ist, müssen Sie beide Probleme beheben, ohne andere Skripte fälschlicherweise als sicher zu kennzeichnen. Der Rest dieses Dokuments enthält Anleitungen, wie Sie dies erreichen können.

## Hinzufügen von Tags als vertrauenswürdige Quelle

Bei Verwendung eines CSP müssen Sie alle vertrauenswürdigen Domains in den Wert der `Content-Security-Policy`-Kopfzeile einschließen. Der Wert, den Sie für Tags angeben müssen, hängt vom verwendeten Hosting-Typ ab.

### Selbstständiges Hosting

Wenn Sie Ihre Bibliothek [selbst hosten](../publishing/hosts/self-hosting-libraries.md), ist die Quelle für Ihre Bibliothek wahrscheinlich Ihre eigene Domain. Mit der folgenden Konfiguration können Sie festlegen, dass die Host-Domain eine sichere Quelle ist:

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>`-Tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Adobe-verwaltetes Hosting

Wenn Sie einen von [Adobe verwalteten Host](../publishing/hosts/managed-by-adobe-host.md) verwenden, wird Ihr Build auf `assets.adobedtm.com` aufbewahrt. Sie sollten `self` als sichere Domäne angeben, damit Sie keine Skripte beschädigen, die bereits geladen werden. Sie müssen aber auch `assets.adobedtm.com` als sicher angeben, da ansonsten Ihre Tag-Bibliothek nicht auf der Seite geladen wird. In diesem Fall sollten Sie die folgende Konfiguration verwenden:

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>`-Tag**


Es gibt eine sehr wichtige Voraussetzung: Sie müssen die Tag-Bibliothek [asynchron](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/asynchronous-deployment.html?lang=de) laden. Dies funktioniert nicht bei synchronem Laden der Tag-Bibliothek (was zu Konsolenfehlern und nicht ordnungsgemäß ausgeführten Regeln führt).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Sie sollten `self` als sichere Domain spezifizieren, damit Sie keine Skripte beschädigen, sie bereits geladen werden. Zusätzlich muss `assets.adobedtm.com` als sicher angegeben werden, da ansonsten Ihr Bibliotheks-Build nicht auf der Seite geladen wird.

## Inline-Skripte

CSP deaktiviert Inline-Skripte standardmäßig und muss daher manuell konfiguriert werden, um sie zuzulassen. Sie haben zwei Optionen, um Inline-Skripte zuzulassen:

* [Mit Nonce zulassen](#nonce) (gute Sicherheit)
* [Alle Inline-Skripte zulassen](#unsafe-inline) (am wenigsten sicher)

>[!NOTE]
>
>Die CSP-Spezifikation enthält Details zu einer dritten Option mit Hashes, aber dieser Ansatz ist nicht möglich, wenn Tag-Management-Systeme wie Tags verwendet werden. Weitere Informationen zu den Einschränkungen bei der Verwendung von Hashes mit Tags in Platform finden Sie im Handbuch [Subresource Integrity (SRI)](./sri.md).

### Mit Nonce zulassen {#nonce}

Bei dieser Methode wird eine kryptografische Nonce erzeugt und zu Ihrem CSP und jedem Inline-Skript auf Ihrer Website hinzugefügt. Wenn der Browser die Anweisung erhält, ein Inline-Skript mit einer darin enthaltenen Nonce zu laden, vergleicht der Browser den Nonce-Wert mit dem im CSP-Header enthaltenen Wert. Wenn diese übereinstimmen, wird das Skript geladen. Die Nonce sollte bei jedem Laden einer neuen Seite verändert werden.

>[!IMPORTANT]
>
>Um diese Methode verwenden zu können, müssen Sie den Build asynchron laden. Dies funktioniert nicht, wenn der Build synchron geladen wird, was zu Konsolenfehlern und nicht ordnungsgemäß ausgeführten Regeln führt. Weitere Informationen finden Sie im Handbuch zur [asynchronen Implementierung](./asynchronous-deployment.md).

Die folgenden Beispiele zeigen, wie Sie Ihre Nonce zur CSP-Konfiguration für einen von Adobe verwalteten Host hinzufügen können. Wenn Sie Self-Hosting verwenden, können Sie `assets.adobedtm.com` ausschließen.

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>`-Tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Nachdem Sie den Header oder das HTML-Tag konfiguriert haben, müssen Sie dem Tag mitteilen, wo die Nonce beim Laden eines Inline-Skripts zu finden ist. Damit ein Tag die Nonce beim Laden des Skripts verwendet, müssen Sie:

1. Erstellen Sie ein Datenelement, das auf die Position der Nonce in Ihrer Datenschicht verweist.
1. Konfigurieren Sie die Haupterweiterung und spezifizieren Sie, welches Datenelement Sie verwendet haben.
1. Veröffentlichen Sie das Datenelement und die Änderungen in der Haupterweiterung.

>[!NOTE]
>
>Der obige Prozess behandelt nur das Laden Ihres benutzerspezifischen Codes, nicht aber was dieser benutzerspezifische Code tut. Wenn ein Inline-Skript benutzerdefinierten Code enthält, der nicht mit Ihrem CSP konform ist, hat das CSP Vorrang. Wenn Sie beispielsweise benutzerdefinierten Code verwenden, um ein Inline-Skript zu laden, indem Sie es an das DOM anhängen, kann das Tag die Nonce nicht korrekt hinzufügen. Daher funktioniert diese spezifische Aktion für benutzerspezifischen Code nicht erwartungsgemäß.

### Alle Inline-Skripte zulassen {#unsafe-inline}

Wenn die Verwendung einer Nonce bei Ihnen nicht anwendbar ist, können Sie Ihre CSP so konfigurieren, dass alle Inline-Skripte zugelassen werden. Dies ist zwar die am wenigsten sichere Option, sie ist aber am einfachsten zu implementieren und zu warten.

Die folgenden Beispiele zeigen, wie Sie alle Inline-Skripte im CSP-Header zulassen können.

#### Selbstständiges Hosting

Verwenden Sie die folgenden Konfigurationen, wenn Sie Self-Hosting verwenden:

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>`-Tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Adobe-verwaltetes Hosting

Verwenden Sie die folgenden Konfigurationen, wenn Sie Adobe-verwaltetes Hosting verwenden:

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>`-Tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie Ihren CSP-Header so konfigurieren können, dass die Tag-Bibliotheksdatei und Inline-Skripte akzeptiert werden.

Als zusätzliche Sicherheitsmaßnahme können Sie auch Subresource Integrity (SRI) verwenden, um abgerufene Bibliotheks-Builds zu validieren. Diese Funktion weist jedoch einige wesentliche Einschränkungen auf, wenn sie mit Tag-Management-Systemen wie Tags verwendet wird. Weitere Informationen finden Sie im Handbuch zur [SRI-Kompatibilität in Platform](./sri.md).
