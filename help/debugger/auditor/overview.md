---
title: Registerkarte „Auditor“
description: Erfahren Sie, wie Sie die Registerkarte „Auditor“ in Adobe Experience Platform Debugger verwenden, um Ihre Adobe Experience Cloud-Implementierungen zu testen.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Auditor;DTM;Target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 32%

---

# Registerkarte „Auditor“

In Adobe Experience Platform Debugger können Sie die Registerkarte **[!UICONTROL Auditor]** verwenden, um eine Reihe von Audittests auf Ihrer Seite durchzuführen.

So verwenden Sie diese Funktion:

1. Wählen Sie **[!UICONTROL Auditor]** in der linken Navigationsleiste aus.
1. Wählen Sie **[!UICONTROL Run Auditor Tests]** aus. Sobald die Tests abgeschlossen sind, werden ihre Ergebnisse unten angezeigt.

![Screenshot der Testergebnisse auf der Registerkarte „Auditor“](../images/auditor-results.png)

In der Ergebnisliste werden der Test und das Ergebnis sowie Vorschläge zur Lösung von Problemen angezeigt.

## Interpretieren der Testergebnisse

Jeder Test wird gewichtet, und die Testpunktzahl entspricht der zugewiesenen Gewichtung. Wenn Sie einen Test mit einem Gewicht von 5 bestehen, erhalten Sie fünf Punkte.

| Ergebnis | Beschreibung |
| --- | --- |
| 0 | Warnt Sie vor Problemen, die Sie kennen sollten, die sich jedoch nicht auf Ihr Ergebnis auswirken. |
| 1 | empfiehlt eine Optimierung. Keine Auswirkung auf die Datengenauigkeit. |
| 2 | Wenn dieser Test nicht erfolgreich ist, haben Sie keinen Zugriff auf die neuesten Funktionen und Fehlerbehebungen in Adobe Experience Cloud. |
| 3 | Tests auf Effizienz und ob die Implementierung den Best Practices entspricht. |
| 4 | Ein Fehler bedeutet, dass Sie möglicherweise unzuverlässige Daten erfassen. |
| 5 | Ein Fehler kann zu Datenverlust führen. |

Alle Tests bestehen oder schlagen fehl. Während der Tests wird geprüft, ob die Testbedingungen erfüllt wurden oder nicht, sodass keine Abstufungsergebnisse für eine teilweise Erfüllung entstehen können. Wird bei einem Test beispielsweise die neueste Version einer Adobe-Lösung geprüft, erhalten Sie immer dasselbe Ergebnis – unabhängig davon, ob Sie nur eine oder fünf Version in Verzug sind. Die neuesten Versionen enthalten Leistungsverbesserungen und Fehlerbehebungen. Daher wird empfohlen, die neueste Version zu verwenden.

Es wird **dringend empfohlen**, Ergebnisse der Stufe 4 oder 5 zu korrigieren.

Es wird **empfohlen**, Ergebnisse der Stufen 1 bis 3 zu korrigieren.

## Unterstützte Adobe-Technologien

Die Auditor-Funktion kann die folgenden Adobe-Technologien bewerten:

* Adobe Advertising DSP
* Adobe Advertising Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* Tags (ehemals Adobe Experience Platform Launch)

## Testrubriken

Weitere Informationen zu den von dieser Funktion bereitgestellten Testrubriken finden Sie in den folgenden Dokumenten:

* [Tag-Konsistenz](./tag-consistency.md)
* [Tag-Präsenz](./tag-presence.md)
* [Konfiguration](./configuration.md)
* [Warnhinweise](./alerts.md)
