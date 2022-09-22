---
title: Umgebungen
description: Hier erfahren Sie mehr über das Konzept von Tag-Umgebungen und wie sie in Adobe Experience Platform funktionieren.
exl-id: 0bf641c9-412e-4737-9b76-232d980385b2
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Umgebungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Tag-Umgebungen definieren mehrere Hauptaspekte der Bibliotheks-Builds, die Sie auf Ihrer Website oder in Ihrer App bereitstellen:

* Den Dateinamen des Builds
* Die Domain und den Pfad des Builds, je nach zugewiesenem Host der Umgebung
* Das Dateiformat des Builds, je nach ausgewählter Archivierungsoption

Wenn Sie einen Bibliotheks-Build erstellen, müssen Sie ihn einer Umgebung zuweisen. Die Erweiterungen, Regeln und Datenelemente des Builds werden dann kompiliert und in die zugewiesene Umgebung eingefügt. Jede Umgebung bietet einen eindeutigen Einbettungs-Code, mit dem Sie den zugewiesenen Build in Ihre Website integrieren können.

In den einzelnen Umgebungen können verschiedene Artefakte vorhanden sein. Dadurch können Sie verschiedene Bibliotheken in verschiedenen Umgebungen testen, während Sie Ihren Workflow durchlaufen.

In diesem Dokument wird beschrieben, wie Sie verschiedene Umgebungen in der Datenerfassungs-Benutzeroberfläche installieren, konfigurieren und erstellen.

## Umgebungstypen

Tags unterstützen drei verschiedene Umgebungstypen, die jeweils einem anderen Status im [Veröffentlichungs-Workflow](./publishing-flow.md) entsprechen:

| Umgebungstyp | Beschreibung |
| --- | --- |
| Entwicklung | Diese Umgebung entspricht der Spalte **Entwicklung** im Publishing-Workflow. |
| Staging | Diese Umgebung entspricht den Spalten **Gesendet** und **Genehmigt** im Publishing-Workflow. |
| Produktion | Diese Umgebung entspricht der Spalte **Veröffentlicht** im Publishing-Workflow. |

In den einzelnen Umgebungen können verschiedene Artefakte vorhanden sein. Dadurch können Sie verschiedene Bibliotheken in verschiedenen Umgebungen testen, während Sie den Publishing-Workflow durchlaufen.

>[!NOTE]
>
>Jeder Umgebung kann jeweils nur ein Bibliotheks-Build zugewiesen werden. Es ist jedoch zu erwarten, dass eine Umgebung im Laufe der Zeit viele verschiedene Builds enthält, während Sie sie durch den Publishing-Workflow bewegen und Builds Umgebungen bei Bedarf neu zuordnen.

## Installation {#installation}

Jede Umgebung verfügt über eine Reihe von Anweisungen, mit deren Hilfe sie mit Ihrer Anwendung verbunden werden kann. Bei Web-Eigenschaften werden mithilfe dieser Anweisungen Einbettungs-Codes bereitgestellt. Bei mobilen Eigenschaften stellen diese Anweisungen den Code bereit, der zum Instanziieren der von Ihnen verwendeten Bibliotheken und zum Abrufen der Konfiguration zur Laufzeit benötigt wird.

>[!IMPORTANT]
>
>Jeder Umgebungstyp hat seine eigenen Installationsanweisungen. Abhängig von der verwendeten Umgebung müssen Sie sicherstellen, dass Sie die richtigen Einbettungs-Codes und/oder Abhängigkeiten verwenden.
>
>Beispielsweise unterstützt der Produktions-Einbettungs-Code für eine Web-Eigenschaft die Zwischenspeicherung im Browser, während dies die Entwicklungs- und Staging-Einbettungs-Codes nicht unterstützen. Daher sollten Sie keine Entwicklungs- oder Staging-Einbettungs-Codes in Kontexten mit hohem Traffic oder Produktionsumgebungen verwenden.

Um auf die Installationsanweisungen für eine Umgebung zuzugreifen, navigieren Sie zur Registerkarte **[!UICONTROL Umgebungen]** für Ihre Eigenschaft und wählen dann das Symbol **[!UICONTROL Installieren]** für diese Umgebung aus.

![](./images/environments/install-buttons.png)

Wenn Sie eine Web-Eigenschaft verwenden, erhalten Sie einen Einbettungs-Code, der im `<head>`-Tag Ihres Dokuments verwendet werden soll. Sie haben außerdem die Möglichkeit, Bibliotheksdateien zur Laufzeit synchron oder asynchron bereitzustellen. Je nach der gewählten Einstellung werden andere Installationsanweisungen angezeigt. Einbettungs-Codes werden weiter unten in diesem Dokument erläutert.

![](./images/environments/web-instructions.png)

Wenn Sie eine Mobile-Eigenschaft verwenden, erhalten Sie separate Anweisungen zum Installieren von Abhängigkeiten für Android (über [Gradle](https://gradle.org/)) und iOS (über [CocoaPods](https://cocoapods.org/)).

![](./images/environments/mobile-instructions.png)

## Konfiguration für Mobilgeräte

Bezüglich der Eigenschaften von Mobilgeräten können Sie die Konfigurationsoptionen für eine Umgebung durch deren Auswahl in der Liste ansehen. Von hier aus können Sie den Namen der Umgebung ändern. Umgebungen mit Mobilgeräten können derzeit nur von Adobe verwaltete Hosts verwenden.

![](./images/environments/mobile-config.png)

Weitere Informationen finden Sie in der Übersicht zu [Hosts](./hosts/hosts-overview.md).

## Web-Konfiguration

Die Einstellungen aus der zugewiesenen Umgebung bestimmen Folgendes für Web-Eigenschaften:

* **Host**: Der Server-Speicherort, auf dem der Build bereitgestellt werden soll.
* **Archiveinstellung**: Gibt an, ob das System bereitstellbare Dateien ausgeben oder in einem Archivformat komprimieren soll.
* **Einbettungs-Code**: Der `<script>` Code, der in den HTML-Code Ihrer Web-Seiten eingebettet werden soll, mit dem der Bibliotheks-Build zur Laufzeit bereitgestellt wird.

Wählen Sie auf der Registerkarte [!UICONTROL Umgebungen] eine aufgelistete Umgebung aus, um deren Konfigurationssteuerelemente anzuzeigen.

![](./images/environments/environment-config.png)

### Host {#host}

Klicken Sie auf **[!UICONTROL Host]**, um einen vorkonfigurierten Host für die Umgebung aus dem Dropdown-Menü auszuwählen.

![](./images/environments/select-host.png)

Wenn ein Build erstellt wird, wird dieser Build an dem Speicherort bereitgestellt, den Sie für den zugewiesenen Host angegeben haben. Informationen zum Erstellen und Konfigurieren von Hosts in der Datenerfassungs-Benutzeroberfläche finden Sie in der [Übersicht über Hosts](./hosts/hosts-overview.md).

### Archivierungseinstellungen {#archive}

Die meisten Builds bestehen aus mehreren Dateien. Aus mehreren Dateien bestehende Builds enthalten eine Hauptbibliotheksdatei (verknüpft im Einbettungs-Code), die interne Verweise auf die anderen Dateien aufweist, die nach Bedarf aufgerufen werden.

Mit der Schaltfläche **[!UICONTROL Archiv erstellen]** können Sie die Archivierungseinstellung der Umgebung umschalten. Standardmäßig ist die Archivierungsoption deaktiviert und der Build wird in einem Format bereitgestellt, das wie vorgesehen ausgeführt wird (JavaScript für Web-Eigenschaften und JSON für Mobile-Eigenschaften).

Wenn Sie die Archivierungseinstellung aktivieren, werden in der Benutzeroberfläche zusätzliche Konfigurationseinstellungen angezeigt, mit denen Sie optional die Archivdatei verschlüsseln und einen Pfad zur Bibliothek definieren können, wenn Sie Self-Hosting verwenden.

![](./images/environments/archive-settings.png)

Der Pfad kann entweder eine vollständige URL oder ein relativer Pfad sein, der Domain-übergreifend verwendet werden kann. Dies ist wichtig, da die meisten Builds mehrere Dateien mit internen Verweisen aufeinander enthalten.

Wenn Sie die Archivierungsoption verwenden, werden alle Build-Dateien stattdessen als ZIP-Dateien übermittelt. Dies kann in folgenden Situationen hilfreich sein:

1. Sie hosten die Bibliothek selbst, möchten jedoch keinen SFTP-Host für die Bereitstellung einrichten.
1. Sie müssen die Code-Analyse zum Build vor der Implementierung ausführen.
1. Sie möchten nur den Build-Inhalt anzeigen, um zu sehen, was darin enthalten ist.

### Einbettungs-Code {#embed-code}

Ein Einbettungs-Code ist ein `<script>`-Tag, das die `<head>`-Abschnitte Ihrer Web-Seiten eingefügt werden muss, um den von Ihnen erstellten Code in zu laden und auszuführen. Jede Umgebungskonfiguration erzeugt automatisch einen eigenen Einbettungs-Code, sodass Sie ihn nur kopieren und auf den Seiten einfügen müssen, auf denen Tags ausgeführt werden sollen.

Bei der Ansicht der Installationsanweisungen können Sie festlegen, ob das Skript die Bibliotheksdateien synchron oder asynchron laden soll. Diese Einstellung ist nicht beständig und spiegelt nicht wider, wie Sie Tags auf Ihrer Site tatsächlich implementiert haben. Vielmehr soll nur gezeigt werden, wie die Umgebung richtig installiert werden kann.

>[!WARNING]
>
>Je nach Inhalt der Tag-Bibliothek kann sich das Verhalten der Regeln und anderer Elemente zwischen der synchronen und der asynchronen Implementierung ändern. Es ist daher wichtig, alle Änderungen, die Sie vornehmen, gründlich zu testen.

#### Asynchrone Implementierung

Durch die asynchrone Implementierung kann der Browser den Rest der Seite weiterhin laden, während die Bibliothek abgerufen wird. Bei Verwendung dieser Einstellung gibt es nur einen Einbettungs-Code, der im Dokument-`<head>` platziert werden muss.

Weitere Informationen zu dieser Einstellung finden Sie im Handbuch zur [asynchronen Implementierung](../client-side/asynchronous-deployment.md).

#### Synchrone Implementierung

Wenn der Browser einen Einbettungs-Code mithilfe der synchronen Implementierung liest, ruft er die Tag-Bibliothek ab und führt sie aus, bevor er die Seite weiter lädt.

Synchrone Einbettungs-Codes bestehen aus zwei `<script>`-Tags, die in den HTML-Code Ihrer Website eingefügt werden müssen. Ein `<script>`-Tag muss im Dokument-`<head>` platziert werden, das andere muss direkt vor dem schließenden `</body>`-Tag platziert werden.

#### Aktualisierungen des Einbettungs-Codes

Da Einbettungs-Codes basierend auf Ihren Umgebungskonfigurationen generiert werden, wird der Einbettungs-Code für die betreffende Umgebung durch manche Konfigurationsänderungen automatisch aktualisiert. Zu diesen Änderungen gehören:

* Wechsel von einem Adobe-verwalteten Host zu einem SFTP-Host (oder umgekehrt).
* Ändern der Archivierungseinstellung.
* Aktualisieren des Pfadfelds, wenn die Archivierungseinstellung aktiviert ist.

>[!WARNING]
>
>Wenn sich der Einbettungs-Code einer Tag-Umgebung ändert, müssen Sie die Einbettungs-Codes im HTML-Code manuell aktualisieren. Um kostenaufwändige Wartungsarbeiten zu vermeiden, sollten Sie Ihre Einbettungs-Codes nur dann aktualisieren, wenn dies unbedingt erforderlich ist.

## Erstellen einer Umgebung

Bei der ersten Erstellung einer Eigenschaft werden dieser Eigenschaft automatisch drei Umgebungen zugewiesen: Entwicklung, Staging und Produktion. Dies reicht aus, um den Publishing-Workflow auszuführen. Sie können jedoch bei Bedarf zusätzliche Entwicklungs-Umgebungen hinzufügen, da dies für größere Teams nützlich sein kann, bei denen mehrere Entwickler gleichzeitig an verschiedenen Projekten arbeiten.

Wählen Sie auf der Registerkarte [!UICONTROL Umgebungen] für Ihre Eigenschaft **[!UICONTROL Umgebung hinzufügen]** aus.

![](./images/environments/create-new.png)

Wählen Sie im nächsten Bildschirm die Option **[!UICONTROL Entwicklung]** aus.

![](./images/environments/create-development.png)

Im nächsten Bildschirm können Sie die neue Umgebung benennen, einen Host auswählen und eine Archivierungseinstellung auswählen. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]**, um die Umgebung zu erstellen.

![](./images/environments/create-config.png)

Die Registerkarte [!UICONTROL Umgebungen] wird erneut mit den Installationsanweisungen für die neue Umgebung angezeigt.

![](./images/environments/create-install.png)

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie nun über Kenntnisse zum Konfigurieren von Umgebungen in der Benutzeroberfläche und zum Installieren in Ihrer Website oder App verfügen. Jetzt sind Sie bereit, Ihre Bibliotheks-Builds zu veröffentlichen.

Wenn Sie Iterationen Ihrer Bibliothek veröffentlichen, ist es möglicherweise erforderlich, dass Sie frühere Builds zur Fehlerbehebung und zum Rollback verfolgen und archivieren. Weitere Informationen finden Sie im Handbuch zum [erneuten Veröffentlichen älterer Bibliotheken](./republish.md).
