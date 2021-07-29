---
title: Builds
description: Erfahren Sie mehr über das Konzept von Builds und ihre Funktionsweise in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 53%

---

# Builds

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Bei einem Build handelt es sich um eine Gruppe von Dateien, die sämtlichen Code enthalten, der auf dem Clientgerät ausgeführt wird.

Es handelt sich um eine Zusammenstellung der Änderungen, die Sie in Ihrer Bibliothek angegeben haben, sowie aller zuvor gesendeten, genehmigten oder veröffentlichten Elemente.

Der Build besteht aus clientseitigen Codedateien, die sich gegenseitig referenzieren. Diese Dateien werden mithilfe der Umgebung und des Hosts, den Sie für Ihre Bibliothek ausgewählt haben, an Ihren Hosting-Standort übertragen. Der Code, den Sie auf Ihrer Site bereitstellen, verweist auf denselben Speicherort, damit die Dateien geladen werden können, wenn ein Benutzer auf Ihre Site oder Anwendung zugreift.

## Dateiinhalt

Eine Bibliothek definiert einen speziellen Satz von Tag-Ressourcen (Erweiterungen, Regeln und Datenelemente), die darin enthalten sein sollen.

Ein Build enthält den gesamten Modulcode (bereitgestellt von den Entwicklern der Erweiterung) und die Konfiguration (von Ihnen eingegeben), die erforderlich sind, um die in der Bibliothek enthaltenen Ressourcen zu nutzen. Wenn beispielsweise eine Erweiterung Aktionen bereitstellt, die nicht in Ihren Regeln verwendet werden, ist der Code für die Durchführung dieser Aktionen nicht im Build enthalten.

Builds sind in die Hauptbibliotheksdatei und möglicherweise in viele kleinere Dateien unterteilt. Auf die Hauptbibliotheksdatei wird in Ihrem Einbettungscode verwiesen, und sie wird zur Laufzeit auf der Seite geladen. Sie enthält Folgendes:

* Regel-Engine
* Gesamte Erweiterungskonfiguration
* Gesamten Code und gesamte Konfiguration von Datenelementen
* Gesamten Code und gesamte Konfiguration von Regelereignissen
* Gesamten Code und gesamte Konfiguration von Bedingungen
* Ereigniscode und -konfiguration für sämtliche Regeln, die „Bibliothek geladen“ oder „Seitenende“ als Ereignis verwenden (da wir wissen, dass wir diese sofort benötigen).

Die kleineren Dateien enthalten den Code und die Konfiguration für einzelne Aktionen, die nach Bedarf auf der Seite geladen werden. Wenn eine Regel ausgelöst wird und ihre Bedingungen so ausgewertet werden, dass die Aktionen ausgeführt werden müssen, werden der erforderliche Code und die Konfiguration für diese bestimmte Aktion aus einer der kleineren Dateien abgerufen. Das bedeutet, dass immer nur der Code auf der Seite geladen wird, der erforderlich ist, um die jeweiligen Aktionen durchzuführen. So wird die Hauptbibliothek möglichst klein gehalten.

## Dateiformat

Das Standarddateiformat für Builds ist ein Paket von Dateien, die den gesamten Code enthalten, damit Ihre Erweiterungen, Datenelemente und Regeln auf die gewünschte Weise ausgeführt werden können.

In bestimmten Fällen empfiehlt sich jedoch ein ZIP-Archiv der Dateien anstelle der ausführbaren clientseitigen Codedatei. Beispiel: Ein Archiv ist sinnvoll, wenn Sie Ihren Build selbst hosten und den Build in einer anderen Implementierung verwenden möchten. Wenn Sie im selbstständig gehosteten Pfad zum Bibliotheksfeld etwas angeben, können Sie Ihre Umgebung speichern. Neben Ihrem neuen Code wird ein Link zum archivierten Download verfügbar. Nachdem die Bibliothek erstellt wurde, haben Sie die Möglichkeit, eine ZIP-Datei auf Akamai bereitzustellen und sie von `assets.adobedtm.com/...` herunterzuladen.

>[!NOTE]
>
>An diesem Ort ist nichts vorhanden, bis Sie einen Build erstellen.

Unabhängig vom Dateiformat wird der Build immer an dem vom Host angegebenen Speicherort bereitgestellt.

Um einen Build abzuschließen, wählen Sie eine Bibliothek und die Build-Option aus, die auf dieser Ebene des Veröffentlichungsvorgangs verfügbar ist (Build für die Entwicklung, Build für das Staging...).

## Minimierung

Durch Minimierung werden Bandbreitenkosten reduziert und die Geschwindigkeit erhöht, indem Daten, die nicht für die Ausführung erforderlich sind, aus der jeweiligen Datei entfernt werden.

Um die Leistung zu steigern, minimiert Platform alle Elemente, einschließlich:

* Die Haupt-Tag-Bibliothek
* Modul-Code, der von den Entwicklern als Teil einer Erweiterung bereitgestellt wird
* Benutzerdefinierter Code, der von Platform-Benutzern bereitgestellt wird

>[!NOTE]
>
>Wenn Ihr Modul- und Ihr benutzerspezifischer Code bereits minimiert wurden, minimiert Platform sie erneut. Diese zweite Minimierung bietet keine zusätzlichen Vorteile, verursacht jedoch keinen Schaden und macht Platform weniger komplex und leichter zu verwalten.

Jeder clientseitige Code, der bereitgestellt wird, verweist auf die minimierte Version des Codes. Dies wird in den Dateinamen angezeigt, die der standardmäßigen Namenskonvention für minimierte Dateien entsprechen:

`launch-%environment_id%.min.js`

Wenn der nicht minimierte Code angezeigt werden soll, entfernen Sie &quot;.min&quot;aus dem Dateinamen:

`launch-%environment_id%.js`

Wenn ein Erweiterungsentwickler minimierten Code mit seiner Erweiterung bereitstellt, stellt Platform im nicht minimierten Build keinen nicht minimierten Code bereit. Wenn ein Platform-Benutzer minimierten Code in ein Feld für benutzerdefinierten Code eingibt, wird dieser Code in nicht minimierten Builds dennoch minimiert. Die Minimierung von Elementen in Platform wird nicht rückgängig gemacht.

Weitere Informationen zur Minimierung finden Sie in [diesem Stackpath-Artikel](https://blog.stackpath.com/glossary/minification/).

Beim Erstellen eines Builds wird zuerst die nicht minimierte Bibliothek erstellt und dann die gesamte Bibliothek gleichzeitig minimiert.
