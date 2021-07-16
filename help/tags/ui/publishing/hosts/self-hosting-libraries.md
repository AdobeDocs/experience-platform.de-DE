---
title: Self-Hosting von Bibliotheken
description: Erfahren Sie, wie Sie Self-Hosting für Ihre Tag-Bibliothek-Builds in Adobe Experience Platform implementieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 74%

---

# Self-Hosting von Bibliotheken

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Tags in Adobe Experience Platform ermöglichen die Erstellung eines Dateiensatzes namens [build](../builds.md). Dieser Dateisatz steuert das Verhalten Ihrer Anwendung zur Laufzeit.

Builds müssen an einer anderen Stelle gehostet werden, damit sie zur Laufzeit bei Bedarf von Clientgeräten abgerufen werden können.

Platform kann entweder das Hosting dieser Dateien für Sie verwalten, oder Sie tun dies selbst.

## Verwaltet von Adobe {#managed-by-adobe}

Adobe ist nicht im Bereich Web-Hosting tätig. Wenn Sie sich dafür entscheiden, Adobe das Hosting zu überlassen, werden Ihre Builds an ein Drittanbieter-Netzwerk zur Inhaltsbereitstellung (Content Delivery Network, CDN) übergeben, mit dem wir einen Vertrag abgeschlossen haben.

Derzeit ist der primäre CDN-Anbieter Akamai. Die auf Akamai gehosteten Dateien haben die Domäne `assets.adobedtm.com`.

### Gründe für die Verwendung des verwalteten Hostings

Der primäre Grund für die Verwendung von verwaltetem Hosting ist der Komfort. Es ist einfacher, den erforderlichen Host zu erstellen, und Sie müssen sich nicht um die Wartung kümmern.

## Selbstständiges Hosting

Wenn Adobe Ihre gehosteten Dateien nicht verwalten soll, müssen Sie sie selbst hosten. Zum Hosten Ihrer Dateien müssen Sie die fertigen Builds von Platform abrufen und dafür verantwortlich sein, die Dateien über den Versionszyklus Ihres Unternehmens auf vom Unternehmen verwaltete Server abzurufen.

### Gründe für die Verwendung des selbstständigen Hostings

Es gibt mehrere Gründe dafür, Ihre eigenen Build-Dateien zu hosten.

* Einige Browser blockieren die Domäne „assets.adobedtm.com“ aufgrund der Datenschutzeinstellungen, die der Endbenutzer konfiguriert hat.
* Das selbstständige Hosting reduziert die erforderliche Anzahl an DNS-Suchvorgängen.
* Sie benötigen die Verwendung von HTTP/2
* Sie verfügen über bestimmte Header für die Sicherheit.
* Ihre Anforderungen an die Cache-Steuerung unterscheiden sich von den Standardeinstellungen der Adobe
* Sie möchten mehr Kontrolle über den Speicherort der Edge-Knoten haben.
* Ihre Organisation verfügt über Sicherheits- und rechtliche Anforderungen, die die Verwendung der Option zur Verwaltung durch Adobe verhindern.

### Selbstständiges Hosten

Es gibt zwei Methoden, mit denen Sie fertige Builds für das selbstständige Hosten akquirieren können.

* Download
* Direkte Bereitstellung

#### Download

Die Builds können als komprimierte ZIP-Datei bereitgestellt werden (Verschlüsselung optional). Anschließend können Sie das Paket entpacken und den Inhalt in Ihren Versionszyklus einfügen, um ihn auf Ihren eigenen Servern zu platzieren.

Verwenden Sie einen Host vom Typ [Von Adobe verwaltet](self-hosting-libraries.md) und wählen Sie die Option [Archivieren](../environments.md) für Ihre Umgebung aus. Die Umgebung bietet einen Download-Link. Bei jeder Build-Erstellung können Sie ihn aus dem Download-Link der Umgebung abrufen.

#### Direkte Bereitstellung

Die Builds können auch direkt an einen von Ihnen erstellten SFTP-Server gesendet werden. Sie übernehmen die Verantwortung dafür, diese Dateien in Ihren Versionszyklus zu übernehmen und live zu schalten.

Für die Ausführung einer direkten Bereitstellung sollten Sie einen [SFTP-Host](sftp-host.md) erstellen und diesen Host Ihrer Umgebung zuweisen. Bei jeder Erstellung einer Bibliothek in dieser Umgebung werden die Dateien an Ihren SFTP-Server gesendet.
