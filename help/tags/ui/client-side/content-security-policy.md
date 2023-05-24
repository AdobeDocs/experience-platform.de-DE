---
title: Unterstützung einer Content Security Policy (CSP)
description: Erfahren Sie, wie Sie mit den Einschränkungen der Content Security Policy (CSP) umgehen, wenn Sie Ihre Website mit Tags in Adobe Experience Platform integrieren.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 100%

---

# Unterstützung einer Content Security Policy (CSP)

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Eine Content Security Policy (CSP) ist eine Sicherheitsfunktion, die Cross-Site-Scripting-Angriffe (XSS) verhindert. Bei Cross-Site Scripting wird der Browser dazu gebracht, schädliche Inhalte auszuführen, die scheinbar aus vertrauenswürdigen Quellen stammen, die aber in Wahrheit von woanders her stammen. Mit CSPs kann der Browser (im Namen des Benutzers) überprüfen, ob das Skript tatsächlich von einer vertrauenswürdigen Quelle stammt.

CSPs werden implementiert, indem Sie Ihren Server-Antworten einen `Content-Security-Policy`-HTTP-Header hinzufügen oder indem Sie ein konfiguriertes `<meta>`-Element im `<head>`-Abschnitt Ihrer HTML-Dateien hinzufügen.

>[!NOTE]
>
> Weitere Informationen zu CSP finden Sie in den [MDN-Webdocs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

Tags in Adobe Experience Platform sind ein Tag-Management-System, das dazu dient, Skripte auf Ihrer Website dynamisch zu laden. Eine Standard-CSP blockiert diese dynamisch geladenen Skripte aufgrund potenzieller Sicherheitsprobleme. Dieses Dokument enthält Anleitungen zum Konfigurieren Ihres CSP, um dynamisch geladene Skripte aus Tags zu ermöglichen.

Wenn Sie möchten, dass Tags mit Ihrem CSP zusammenarbeiten, müssen Sie sicherstellen, dass zwei Bedingungen erfüllt sind:

* **Die Quelle für Ihre Tag-Bibliothek muss als vertrauenswürdig eingestuft werden.** Wenn diese Bedingung nicht erfüllt ist, werden die Tag-Bibliothek und andere erforderliche JavaScript-Dateien vom Browser blockiert und nicht auf der Seite geladen.
* **Inline-Skripte müssen erlaubt sein.** Wenn diese Bedingung nicht erfüllt ist, werden auf Regeln von benutzerspezifischem Code basierende Aktionen auf der Seite blockiert und nicht ordnungsgemäß ausgeführt.

Erhöhte Sicherheit erfordert einen erhöhten Arbeitsaufwand auf Seiten des Erstellers von Inhalten. Wenn Sie Tags verwenden möchten und ein CSP vorhanden ist, müssen Sie beide Voraussetzungen schaffen, ohne andere Skripte fälschlicherweise als sicher zu kennzeichnen. Der Rest dieses Dokuments enthält Anleitungen, wie Sie dies erreichen können.

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

Wenn Sie einen von [Adobe verwalteten Host](../publishing/hosts/managed-by-adobe-host.md) verwenden, wird Ihr Build auf `assets.adobedtm.com` aufbewahrt. Sie sollten `self` als sichere Domain angeben, damit Sie keine Skripte beschädigen, die bereits geladen werden. Zusätzlich muss `assets.adobedtm.com` als sicher angegeben werden, da ansonsten Ihre Tag-Bibliothek nicht auf der Seite geladen wird. In diesem Fall sollten Sie die folgende Konfiguration verwenden:

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>`-Tag**


Es gibt eine sehr wichtige Voraussetzung: Sie müssen die Tag-Bibliothek [asynchron](./asynchronous-deployment.md) laden. Dies funktioniert nicht mit einem synchronen Laden der Tag-Bibliothek (was zu Konsolenfehlern und nicht ordnungsgemäßer Ausführung von Regeln führt).

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
>Die CSP-Spezifikation enthält Details zu einer dritten Option mit Hashes, aber dieser Ansatz ist nicht möglich, wenn Tag-Management-Systeme wie Tags verwendet werden. Weitere Informationen zu den Einschränkungen bei der Verwendung von Hashes in mit Tags in Platform finden Sie im [Handbuch zu Subresource Integrity (SRI)](./sri.md).

### Mit Nonce zulassen {#nonce}

Bei dieser Methode wird eine kryptografische Nonce erzeugt und zu Ihrem CSP und jedem Inline-Skript auf Ihrer Website hinzugefügt. Wenn der Browser die Anweisung erhält, ein Inline-Skript mit einer darin enthaltenen Nonce zu laden, vergleicht der Browser den Nonce-Wert mit dem im CSP-Header enthaltenen Wert. Wenn diese übereinstimmen, wird das Skript geladen. Die Nonce sollte bei jedem Laden einer neuen Seite verändert werden.

>[!IMPORTANT]
>
>Um diese Methode verwenden zu können, müssen Sie den Build asynchron laden. Dies funktioniert nicht, wenn der Build synchron geladen wird, was zu Konsolenfehlern und nicht ordnungsgemäß ausgeführten Regeln führt. Weitere Informationen finden Sie im Handbuch zur [asynchronen Bereitstellung](./asynchronous-deployment.md).

Die folgenden Beispiele zeigen, wie Sie Ihre Nonce zur CSP-Konfiguration für einen von Adobe verwalteten Host hinzufügen können. Wenn Sie Self-Hosting verwenden, können Sie `assets.adobedtm.com` ausschließen.

**HTTP-Header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>`-Tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Sobald Sie Ihren Header oder Ihr HTML-Tag konfiguriert haben, müssen Sie dem Tag mitteilen, wo es die Nonce beim Laden eines Inline-Skripts findet. Damit ein Tag beim Laden des Skripts die Nonce verwenden kann, ist Folgendes erforderlich:

1. Erstellen Sie ein Datenelement, das auf die Position der Nonce in Ihrer Datenschicht verweist.
1. Konfigurieren Sie die Haupterweiterung und spezifizieren Sie, welches Datenelement Sie verwendet haben.
1. Veröffentlichen Sie das Datenelement und die Änderungen in der Haupterweiterung.

>[!NOTE]
>
>Der obige Prozess behandelt nur das Laden Ihres benutzerspezifischen Codes, nicht aber was dieser benutzerspezifische Code tut. Wenn ein Inline-Skript benutzerdefinierten Code enthält, der nicht mit Ihrem CSP konform ist, hat das CSP Vorrang. Wenn Sie beispielsweise benutzerdefinierten Code zum Laden von Inline-Skripten verwenden, indem Sie ihn an das DOM anhängen, kann das Tag die Nonce nicht korrekt hinzufügen, sodass diese bestimmte benutzerdefinierte Code-Aaktion nicht wie erwartet funktioniert.

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

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie Ihren CSP-Header so konfigurieren können, dass er die Tag-Bibliotheksdatei und Inline-Skripte akzeptiert.

Als zusätzliche Sicherheitsmaßnahme können Sie auch Subresource Integrity (SRI) verwenden, um abgerufene Bibliotheks-Builds zu validieren. Diese Funktion hat jedoch einige große Einschränkungen, wenn sie mit Tag-Management-Systemen wie Tags verwendet wird. Weitere Informationen finden Sie im Handbuch zur [SRI-Kompatibilität in Platform](./sri.md).
