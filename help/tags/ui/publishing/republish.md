---
title: Bibliothek erneut veröffentlichen
description: Erfahren Sie, wie Sie eine vorherige Tag-Bibliothek in Adobe Experience Platform erneut veröffentlichen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 60%

---

# Bibliothek erneut veröffentlichen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Die fünf zuletzt in Ihrer Produktionsumgebung auf einer Web-Eigenschaft veröffentlichten Bibliotheken können zu einem späteren Zeitpunkt abgerufen werden. Diese Funktion ist hilfreich, wenn Sie einen Fehler in Ihrer Produktionsbibliothek finden und unmittelbar einen funktionierenden Zustand wiederherstellen müssen.

Der Abrufvorgang hängt von den Umgebungseinstellungen zum Zeitpunkt der ursprünglichen Veröffentlichung der Bibliothek ab. Dies ist wichtig, da das Abrufen einer archivierten Bibliothek nichts an Ihrer Live-Site ändert, während das Abrufen einer normalen Bibliothek etwas ändern würde.

Die folgenden Optionen sind verfügbar:

* **Host: Verwaltet nach Adobe, Archivieren: Aus:** Wenn Sie den Host &quot;Managed by Adobe&quot;verwenden und Ihre Bibliothek nicht archivieren, können Sie diese älteren Bibliotheken erneut veröffentlichen.

* **Host: Verwaltet nach Adobe, Archivieren: On:** Wenn Sie den Host &quot;Managed by Adobe&quot;verwenden und Ihre Bibliothek archivieren, können Sie diese älteren Bibliotheken herunterladen.

* **Host: SFTP, Archiv: an oder aus:** Wenn Sie den SFTP-Host verwenden, wird angenommen, dass Sie über eigene Archivierungsstrategien verfügen, weshalb keine Abrufoptionen verfügbar sind.

Abrufoptionen für mobile Eigenschaften sind noch nicht verfügbar.

## Erneutes Veröffentlichen

Jede Tag-Umgebung stellt einen Link zu einer Bibliotheksdatei bereit. Jede Bibliothek, die Sie in dieser Umgebung erstellen, kann mit diesem Link referenziert werden.

Wenn Sie eine Entwicklungs- oder Staging-Umgebung erstellen, wird der alte Build bereinigt und der neue Build bereitgestellt. In der Produktionsumgebung wird dieser Link aktualisiert, damit er auf den neuesten Build verweist. Doch auch die fünf letzten Builds werden beibehalten, bevor sie bereinigt werden.

Deshalb können diese fünf letzten Builds in Ihrer Produktionsumgebung abgerufen werden.

Wenn Sie eine ältere Bibliothek erneut veröffentlichen, aktualisiert Platform den Umgebungs-Link, um auf einen dieser älteren Builds zu verweisen, die noch nicht bereinigt wurden.  Platform sendet außerdem eine Bereinigungsanfrage an den CDN-Edge-Knoten-Cache, um anzugeben, dass die Bibliothek aktualisiert wurde und eine neue Kopie von der Quelle abgerufen werden sollte.

Beim erneuten Veröffentlichen einer älteren Bibliothek passiert Folgendes:

* An den Ressourcen (oder historischen Revisionen) in Ihrer Tag-Eigenschaft werden keine Änderungen vorgenommen

* Die Art und Weise, wie in Entwicklungs- und Staging-Umgebungen vorgelagerte Vorgänge berechnet werden, ändert sich nicht.

Wenn Sie einen Rollback durchführen, weil es ein Problem mit einer Regel gibt, achten Sie auf die jeweiligen Gegebenheiten. Die Regelrevision, die mittlerweile in der Produktionsumgebung vorhanden ist, könnte z. B. drei Revisionen alt sein. Wenn Sie diese Regel in der Datenerfassungs-Benutzeroberfläche anzeigen, um sie zu beheben, spiegelt sie weiterhin die neuesten gespeicherten Änderungen wider und nicht das, was derzeit in Produktion ist.

Aus diesem Grund werden Sie von Platform darüber informiert, dass eine Eigenschaft erneut veröffentlicht wurde, um Sie daran zu erinnern, dass das, was Sie auf der Benutzeroberfläche für die Datenerfassung sehen, etwas weiter aus der Produktion entfernt ist als üblich. Diese Benachrichtigung ist nicht zulässig und wird einmal pro Browser-Sitzung angezeigt, wenn Sie die Eigenschaft zum ersten Mal anzeigen.

### So veröffentlichen Sie eine ältere Bibliothek erneut

![Bibliothek erneut veröffentlichen](images/retrieve_republish.png)

Im Bildschirm „Veröffentlichen“:

1. Suchen Sie in der Spalte „Veröffentlicht“ die Bibliothek, die Sie erneut veröffentlichen möchten.
1. Wählen Sie die Auslassungspunkte (`...`) in der oberen rechten Ecke der Bibliothekskarte aus.
1. Wählen Sie **[!UICONTROL Neu veröffentlichen]** aus.

## Herunterladen

Das Herunterladen einer archivierten Bibliothek ist einfacher. Auf diese ZIP-Dateien wird nirgendwo direkt verwiesen, daher können Sie die ältere Bibliothek einfach auf Ihren Computer herunterladen und den üblichen Prozess ausführen.

### Herunterladen einer älteren Bibliothek

![Herunterladen einer Bibliothek](images/retrieve_download.png)

Im Bildschirm „Veröffentlichen“:

1. Suchen Sie in der Spalte „Veröffentlicht“ die Bibliothek, die Sie herunterladen möchten.
1. Wählen Sie die Auslassungspunkte (`...`) in der oberen rechten Ecke der Bibliothekskarte aus.
1. Wählen Sie **[!UICONTROL Herunterladen]** aus.
