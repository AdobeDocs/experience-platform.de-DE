---
title: Registerkarte „Netzwerk“
description: Erfahren Sie, wie Sie die Registerkarte „Netzwerk“ in Adobe Experience Platform Debugger verwenden.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Netzwerk;Informationen
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 59%

---

# Registerkarte „Netzwerk“

Die Registerkarte **Netzwerk** fasst alle Aufrufe der Adobe Experience Cloud-Lösung auf der Seite zusammen und zeigt sie in der Reihenfolge von links nach rechts an. Standardparameter werden automatisch mit benutzerfreundlichen Namen versehen und so angeordnet, dass gemeinsame Parameter derselben Rolle zusammenstehen.

![](images/network.jpg)

Auf diesem Bildschirm können Schlüsselwertpaare von Treffern verglichen werden. Hier können Sie außerdem überprüfen, ob die für Integrationen verwendeten Parameter, wie z. B. die Experience Cloud-Besucher-ID oder die Ergänzende-Daten-ID, für alle Integrationen einheitlich sind.

>[!NOTE]
>
>Aktuell werden nicht alle innerhalb der Lösungsaufrufe übergebenen Parameter auf dem Netzwerkbildschirm angezeigt (z. B. Analytics-Kontextvariablen, benutzerdefinierte Target-Parameter oder die Kunden-IDs des Experience Cloud ID-Dienstes).

Um die entsprechenden Informationen einer Lösung anzuzeigen, wählen Sie die gewünschte Lösung aus der Liste im linken Navigationsbereich aus. Im folgenden Beispiel wird der Filter so gewählt, dass nur Analytics angezeigt wird:

![](images/network-analytics.jpg)

Um zur Anzeige aller Lösungen zurückzukehren, wählen Sie **[!UICONTROL Netzwerk]**

Wählen Sie ein Element in der Netzwerkansicht aus, um eine erweiterte Ansicht anzuzeigen. In der erweiterten Ansicht können Sie die angezeigten Informationen in die Zwischenablage kopieren.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Um die Liste zu löschen, wählen Sie **[!UICONTROL Ereignisse entfernen]** aus.

Um eine Excel-Datei mit den Informationen auf diesem Bildschirm herunterzuladen, wählen Sie **[!UICONTROL Herunterladen]**.
