---
keywords: Experience Platform; Erste Schritte; Kundenunterstützung; beliebte Themen; Eingabe der Kundenunterstützung; Ausgabe der Kundenai; Fehlerbehebung bei Kundenai; Fehler bei Kundenai
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Fehlerbehebung bei Customer AI
topic-legacy: Getting started
description: Hier finden Sie Antworten auf häufige Fehler in Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Fehlerbehebung bei Customer AI

Customer AI zeigt Fehler an, wenn Modellschulung, -bewertung und -konfiguration fehlschlagen. Im Abschnitt **[!UICONTROL Dienstinstanzen]** zeigt eine Spalte für **[!UICONTROL LAST RUN STATUS]** eine der folgenden Meldungen an: **[!UICONTROL Erfolg]**, **[!UICONTROL Schulungsproblem]** und **[!UICONTROL Fehlgeschlagen]**.

![Letzter Ausführungsstatus](./images/errors/last-run-status.png)

Falls **[!UICONTROL Failed]** oder **[!UICONTROL Training issue]** angezeigt wird, können Sie den Ausführungsstatus auswählen, um ein seitliches Bedienfeld zu öffnen. Das Seitenbedienfeld enthält Ihre **[!UICONTROL Status der letzten Ausführung]** und **[!UICONTROL Details der letzten Ausführung]**. **[!UICONTROL Details zur letzten Ausführung]** enthalten Informationen dazu, warum die Ausführung fehlgeschlagen ist. Falls Customer AI keine Details zu Ihrem Fehler bereitstellen kann, wenden Sie sich an den Support mit dem bereitgestellten Fehlercode.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Modellqualität ist schlecht

Wenn Sie den Fehler &quot;[!UICONTROL Modellqualität ist schlecht erhalten. Es wird empfohlen, eine neue App mit der geänderten Konfiguration] zu erstellen.&quot; Befolgen Sie die unten empfohlenen Schritte, um die Fehlerbehebung zu unterstützen.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Empfohlene Fehlerbehebung

&quot;Modellqualität ist schlecht&quot;bedeutet, dass die Modellgenauigkeit nicht innerhalb eines akzeptablen Bereichs liegt. Customer AI konnte nach dem Training kein zuverlässiges Modell und keine zuverlässige AUC (Bereich unter der ROC-Kurve) &lt; 0,65 erstellen. Um den Fehler zu beheben, wird empfohlen, einen der Konfigurationsparameter zu ändern und das Training erneut durchzuführen.

Überprüfen Sie zunächst die Genauigkeit Ihrer Daten. Es ist wichtig, dass Ihre Daten die erforderlichen Felder enthalten, die für Ihr vorhersagbares Ergebnis erforderlich sind.

- Überprüfen Sie, ob Ihr Datensatz die neuesten Daten enthält. Customer AI geht immer davon aus, dass die Daten beim Auslösen des Modells aktuell sind.
- Prüfen Sie im definierten Prognosefenster und im Berechtigungsfenster, ob Daten fehlen. Ihre Daten müssen ohne Lücken gefüllt werden. Stellen Sie außerdem sicher, dass Ihr Datensatz die [Customer AI-Anforderungen hinsichtlich historischer Daten](./input-output.md#data-requirements) erfüllt.
- Suchen Sie in den Eigenschaften Ihres Schemafelds nach fehlenden Daten in Commerce, Anwendung, Web und Suche.

Wenn Ihre Daten nicht das Problem zu sein scheinen, versuchen Sie, die Eignungsbedingung der Population zu ändern, um das Modell auf bestimmte Profile zu beschränken (z. B. `_experience.analytics.customDimensions.eVars.eVar142` existiert in den letzten 56 Tagen). Dadurch werden die Population und die Größe der im Trainings-Fenster verwendeten Daten eingeschränkt.

Wenn die Einschränkung der Berechtigungspopulation nicht funktioniert hat oder nicht möglich ist, ändern Sie das Prognosefenster.

- Versuchen Sie, Ihr Prognosefenster auf 7 Tage zu ändern und zu überprüfen, ob der Fehler weiterhin auftritt. Wenn der Fehler nicht mehr auftritt, deutet dies darauf hin, dass Sie möglicherweise nicht über genügend Daten für Ihr definiertes Prognosefenster verfügen.
