---
title: Bibliothek erneut veröffentlichen
description: Erfahren Sie, wie Sie eine frühere Tag-Bibliothek in Adobe Experience Platform erneut veröffentlichen.
exl-id: 026b01f2-a93d-4e8a-9ed2-47c4f011e70f
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 96%

---

# Bibliothek erneut veröffentlichen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Die fünf zuletzt in Ihrer Produktionsumgebung auf einer Web-Eigenschaft veröffentlichten Bibliotheken können zu einem späteren Zeitpunkt abgerufen werden. Diese Funktion ist hilfreich, wenn Sie einen Fehler in Ihrer Produktionsbibliothek finden und unmittelbar einen funktionierenden Zustand wiederherstellen müssen.

Der Abrufvorgang hängt von den Umgebungseinstellungen zum Zeitpunkt der ursprünglichen Veröffentlichung der Bibliothek ab. Dies ist wichtig, da das Abrufen einer archivierten Bibliothek nichts an Ihrer Live-Site ändert, während das Abrufen einer normalen Bibliothek etwas ändern würde.

Die folgenden Optionen sind verfügbar:

* **Host: Managed by Adobe, Archiv: Aus:** Wenn Sie den Managed by Adobe-Host verwenden und Ihre Bibliothek nicht archivieren, können Sie diese älteren Bibliotheken erneut veröffentlichen.

* **Host: Managed by Adobe, Archiv: Ein:** Wenn Sie den Managed by Adobe-Host verwenden und Ihre Bibliothek archivieren, können Sie diese älteren Bibliotheken herunterladen.

* **Host: SFTP, Archiv: an oder aus:** Wenn Sie den SFTP-Host verwenden, wird angenommen, dass Sie über eigene Archivierungsstrategien verfügen, weshalb keine Abrufoptionen verfügbar sind.

Abrufoptionen für Mobile-Eigenschaften sind noch nicht verfügbar.

## Erneutes Veröffentlichen

Jede Tag-Umgebung enthält einen Link zu einer Bibliotheksdatei. Jede in dieser Umgebung erstellte Bibliothek kann mit diesem Link referenziert werden.

Wenn Sie eine Entwicklungs- oder Staging-Umgebung erstellen, wird der alte Build bereinigt und der neue Build bereitgestellt. In der Produktionsumgebung wird dieser Link aktualisiert, damit er auf den neuesten Build verweist. Doch auch die fünf letzten Builds werden beibehalten, bevor sie bereinigt werden.

Deshalb können diese fünf letzten Builds in Ihrer Produktionsumgebung abgerufen werden.

Wenn Sie eine ältere Bibliothek erneut veröffentlichen, aktualisiert Platform den Umgebungs-Link, damit er auf einen dieser älteren Builds verweist, die noch nicht bereinigt wurden. Platform stellt außerdem eine Bereinigungsanfrage an den CDN-Edge-Knoten-Cache, um darauf hinzuweisen, dass die Bibliothek aktualisiert wurde und eine neue Kopie von der Quelle abgerufen werden sollte.

Beim erneuten Veröffentlichen einer älteren Bibliothek passiert Folgendes:

* An den Ressourcen (oder früheren Revisionen) Ihrer Tag-Eigenschaft werden keine Änderungen vorgenommen.

* Die Art und Weise, wie in Entwicklungs- und Staging-Umgebungen vorgelagerte Vorgänge berechnet werden, ändert sich nicht.

Wenn Sie einen Rollback durchführen, weil es ein Problem mit einer Regel gibt, achten Sie auf die jeweiligen Gegebenheiten. Die Regelrevision, die mittlerweile in der Produktionsumgebung vorhanden ist, könnte z. B. drei Revisionen alt sein. Wenn Sie diese Regel in der Benutzeroberfläche anzeigen, um sie zu beheben, spiegelt sie weiterhin die zuletzt gespeicherten Änderungen wider und nicht die derzeit in Produktion befindlichen Änderungen.

Deshalb informiert Platform Sie darüber, dass eine Eigenschaft erneut veröffentlicht wurde, um Sie daran zu erinnern, dass das, was Sie in der Datenerfassungs-Benutzeroberfläche sehen, eine frühere Version ist. Diese Benachrichtigung kann geschlossen werden und wird einmal pro Browser-Sitzung angezeigt, wenn Sie die Eigenschaft zum ersten Mal anzeigen.

### So veröffentlichen Sie eine ältere Bibliothek erneut

![Bibliothek erneut veröffentlichen](images/retrieve_republish.png)

Im Bildschirm „Veröffentlichen“:

1. Suchen Sie in der Spalte „Veröffentlicht“ die Bibliothek, die Sie erneut veröffentlichen möchten.
1. Wählen Sie die Auslassungspunkte (`...`) in der oberen rechten Ecke der Bibliothekskarte aus.
1. Wählen Sie **[!UICONTROL Neu veröffentlichen]** aus.

## Download

Das Herunterladen einer archivierten Bibliothek ist einfacher. Auf diese ZIP-Dateien wird nirgendwo direkt verwiesen, daher können Sie die ältere Bibliothek einfach auf Ihren Computer herunterladen und den üblichen Prozess ausführen.

### Herunterladen einer älteren Bibliothek

![Herunterladen einer Bibliothek](images/retrieve_download.png)

Im Bildschirm „Veröffentlichen“:

1. Suchen Sie in der Spalte „Veröffentlicht“ die Bibliothek, die Sie herunterladen möchten.
1. Wählen Sie die Auslassungspunkte (`...`) in der oberen rechten Ecke der Bibliothekskarte aus.
1. Wählen Sie **[!UICONTROL Herunterladen]** aus.
