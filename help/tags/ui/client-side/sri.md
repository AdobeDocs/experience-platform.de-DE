---
title: Unterstützung von Subresource Integrity (SRI)
description: Erfahren Sie, wie die Subresource-Integrität (SRI) in Adobe Experience Platform unterstützt wird.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 100%

---

# Unterstützung von Subresource Integrity (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Dieses Dokument beschreibt, wie die Subresource-Integrität (SRI) in Adobe Experience Platform unterstützt wird.

Moderne Websites werden durch Verweise auf Bilder, Inhalte und Skripten aus verschiedenen Bereichen des Internets erstellt. Mit SRI kann ein Browser überprüfen, ob der Inhalt einer angeforderten Datei nicht unerwartet geändert wurde.

Während sich ihre Anwendungsfälle gegenseitig ergänzen, unterscheidet sich SRI von einer Content Security Policy (CSP), die sicherstellt, dass nur Dateien aus vertrauenswürdigen Quellen auf Ihrer Website verwendet werden. SRI geht noch einen Schritt weiter, indem sichergestellt wird, dass der Inhalt dieser Dateien Ihren Erwartungen entspricht.

>[!NOTE]
>
>Weitere Informationen zu SRI finden Sie in den [MDN-Webdocs](https://developer.mozilla.org/de-DE/docs/Web/Security/Subresource_Integrity).

Der SRI-Validierungsprozess lässt sich wie folgt zusammenfassen:

1. Sie generieren einen kryptografischen Hash des Assets, das Sie überprüfen möchten.
1. Auf Ihrer Website wird der Hash im `integrity`-Attribut des HTML-Elements platziert, das die Datei lädt.
1. Wenn der Browser das `integrity`-Attribut sieht, fordert der Browser die Ressource an und erstellt unabhängig seine eigene Version des kryptografischen Hashs.
1. Der Browser vergleicht den `integrity`-Hash mit dem selbst generierten. Wenn sie übereinstimmen, ist das Asset zulässig. Wenn sie nicht übereinstimmen, wird das Asset blockiert.

## Einschränkungen in Tag-Management-Systemen

Als Tag-Management-System (TMS) bieten Tags in Adobe Experience Platform eine kompilierte JavaScript-Bibliothek, die Sie mit einem einzigen `<script>`-Element (Einbettungs-Code) auf Ihre Seiten laden können. Die dynamische Funktionalität, die das TMS bietet, wird erreicht, indem der Inhalt dieses Skripts dynamisch ausgetauscht wird, ohne dass Sie andere Änderungen vornehmen müssen.

Wenn sich der Skriptinhalt ändert, ändert sich aber auch der kryptografische Hash dieser Inhalte. Die einzige Möglichkeit, dass SRI mit einem TMS funktioniert, besteht daher darin, Ihren Einbettungs-Code gleichzeitig mit der Veröffentlichung eines neuen Builds zu aktualisieren. Für viele wird dadurch der primäre Zweck, ein TMS zu verwenden, von vornherein zunichte gemacht.

Die nächstbeste Sicherheitsoption für Tags ist die Implementierung einer Content Security Policy. Weitere Informationen finden Sie im Handbuch zu [CSPs und Tags](./content-security-policy.md).

## Integration von SRI in die Build-Bereitstellung

Wenn Sie weiterhin SRI für Ihre Bibliotheks-Builds verwenden möchten, müssen Sie Self-Hosting nutzen. Wenn Sie Adobe-verwaltetes Hosting nutzen, ist es nicht möglich, SRI zu verwenden, da ansonsten der Inhalt des neuen Builds über einen gewissen Zeitraum nicht mit dem `integrity`-Attribut des Einbettungscodes übereinstimmt.

Die Automatisierung des Aktualisierungsprozesses Ihres Einbettungs-Codes hängt von der Struktur Ihrer Website ab. Die allgemeinen Schritte können jedoch wie folgt zusammengefasst werden:

1. Rufen Sie den Produktionsbibliotheks-Build entweder über die SFTP-Bereitstellung ab oder laden Sie das Archiv über die Benutzeroberfläche herunter.
1. Generieren Sie den kryptografischen Hash des Haupt-Builds.
1. Stellen Sie sicher, dass das `integrity`-Attribut des Einbettungs-Codes auf den neuen Hash aktualisiert wird und dass der referenzierte Build im Rahmen derselben Bereitstellung aktualisiert wird.

>[!IMPORTANT]
>
>Dieser Ansatz betrifft nur den Haupt-Build. Er beinhaltet keine der kleineren Dateien, die möglicherweise vorhanden sind.

## Nächste Schritte

Dieses Dokument behandelt die Einschränkungen bei der Verwendung von SRI mit Tags und die Schritte, die erforderlich sind, um es trotz dieser Einschränkungen in Ihre Bibliotheks-Build-Bereitstellungen zu integrieren. Wenn Sie dies noch nicht getan haben, wird dringend empfohlen, das Handbuch zu [CSPs und Tags](./content-security-policy.md) für eine alternative Sicherheitsoption zu lesen.
