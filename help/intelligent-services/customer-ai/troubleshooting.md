---
keywords: Experience Platform; Erste Schritte; Kundenunterstützung; beliebte Themen; Eingabe der Kundenunterstützung; Ausgabe der Kundenai; Fehlerbehebung bei Kundenai; Fehler bei Kundenai
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Fehlerbehebung bei Customer AI
topic-legacy: Getting started
description: Hier finden Sie Antworten auf häufige Fehler in Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Fehlerbehebung bei Customer AI

Customer AI zeigt Fehler an, wenn Modellschulung, -bewertung und -konfiguration fehlschlagen. Im **[!UICONTROL Dienstinstanzen]** -Abschnitt, eine Spalte für **[!UICONTROL STATUS DER LETZTEN AUSFÜHRUNG]** zeigt eine der folgenden Meldungen an: **[!UICONTROL Erfolg]**, **[!UICONTROL Schulungsfehler]** und **[!UICONTROL Fehlgeschlagen]**.

![Letzter Ausführungsstatus](./images/errors/last-run-status.png)

In dem Ereignis **[!UICONTROL Fehlgeschlagen]** oder **[!UICONTROL Schulungsfehler]** angezeigt wird, können Sie den Ausführungsstatus auswählen, um einen Seitenbereich zu öffnen. Der Seitenbereich enthält Ihre **[!UICONTROL Letzter Ausführungsstatus]** und **[!UICONTROL Letzte Ausführungsdetails]**. **[!UICONTROL Letzte Ausführungsdetails]** enthält Informationen darüber, warum die Ausführung fehlgeschlagen ist. Falls Customer AI keine Details zu Ihrem Fehler bereitstellen kann, wenden Sie sich an den Support mit dem bereitgestellten Fehlercode.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Zugriff auf Customer AI in Chrome-Anmeldung nicht möglich

Das Laden von Fehlern im Inkognito-Modus von Google Chrome ist auf Aktualisierungen in den Sicherheitseinstellungen des Google Chrome-Inkognito-Modus zurückzuführen. Das Problem wird aktiv mit Chrome bearbeitet, um experience.adobe.com zu einer vertrauenswürdigen Domäne zu machen.

<img src="./images/errors/error.PNG" width="500" /><br />

### Empfohlene Fehlerbehebung

Um dieses Problem zu umgehen, müssen Sie experience.adobe.com als Site hinzufügen, die immer Cookies verwenden kann. Beginnen Sie, indem Sie zu **chrome://settings/cookies**. Scrollen Sie dann nach unten zum **Benutzerdefinierte Verhaltensweisen** und anschließend die **Hinzufügen** neben &quot;Sites, die immer Cookies verwenden können&quot;. Kopieren Sie in das angezeigte Popover-Element und fügen Sie `[*.]experience.adobe.com` und wählen Sie dann **Einschließen von Drittanbieter-Cookies** auf dieser Site aktivieren. Wählen Sie nach Abschluss **Hinzufügen** und laden Customer AI in Inkognito neu.

![empfohlene Korrektur](./images/errors/cookies2.gif)

## Modellqualität ist schlecht

Wenn Sie den Fehler &quot;[!UICONTROL Modellqualität ist schlecht. Es wird empfohlen, eine neue App mit der geänderten Konfiguration zu erstellen]&quot;. Befolgen Sie die unten empfohlenen Schritte, um die Fehlerbehebung zu unterstützen.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Empfohlene Fehlerbehebung

&quot;Modellqualität ist schlecht&quot;bedeutet, dass die Modellgenauigkeit nicht innerhalb eines akzeptablen Bereichs liegt. Customer AI konnte nach dem Training kein zuverlässiges Modell und keine zuverlässige AUC (Bereich unter der ROC-Kurve) &lt; 0,65 erstellen. Um den Fehler zu beheben, wird empfohlen, einen der Konfigurationsparameter zu ändern und das Training erneut durchzuführen.

Überprüfen Sie zunächst die Genauigkeit Ihrer Daten. Es ist wichtig, dass Ihre Daten die erforderlichen Felder enthalten, die für Ihr vorhersagbares Ergebnis erforderlich sind.

- Überprüfen Sie, ob Ihr Datensatz die neuesten Daten enthält. Customer AI geht immer davon aus, dass die Daten beim Auslösen des Modells aktuell sind.
- Prüfen Sie im definierten Prognosefenster und im Berechtigungsfenster, ob Daten fehlen. Ihre Daten müssen ohne Lücken gefüllt werden. Stellen Sie außerdem sicher, dass Ihr Datensatz die [Anforderungen an historische Daten von Customer AI](./input-output.md#data-requirements).
- Suchen Sie in den Eigenschaften Ihres Schemafelds nach fehlenden Daten in Commerce, Anwendung, Web und Suche.

Wenn Ihre Daten nicht das Problem zu sein scheinen, versuchen Sie, die Eignungsbedingung der Population zu ändern, um das Modell auf bestimmte Profile zu beschränken (z. B. `_experience.analytics.customDimensions.eVars.eVar142` ist in den letzten 56 Tagen verfügbar). Dadurch werden die Population und die Größe der im Trainings-Fenster verwendeten Daten eingeschränkt.

Wenn die Einschränkung der Berechtigungspopulation nicht funktioniert hat oder nicht möglich ist, ändern Sie das Prognosefenster.

- Versuchen Sie, Ihr Prognosefenster auf 7 Tage zu ändern und zu überprüfen, ob der Fehler weiterhin auftritt. Wenn der Fehler nicht mehr auftritt, deutet dies darauf hin, dass Sie möglicherweise nicht über genügend Daten für Ihr definiertes Prognosefenster verfügen.
