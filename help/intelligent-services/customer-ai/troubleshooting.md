---
keywords: Experience Platform;Erste Schritte;Kunden-KI;beliebte Themen;Kunden-KI-Eingabe;Kunden-KI-Ausgabe;Fehlerbehebung bei der Kunden-KI;Fehler bei der Kunden-KI
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Fehlerbehebung bei der Kunden-KI
description: Hier finden Sie Antworten auf häufige Fehler in der Kunden-KI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: ht
source-wordcount: '529'
ht-degree: 100%

---

# Fehlerbehebung bei der Kunden-KI

Die Kunden-KI zeigt Fehler an, wenn Modell-Training, -bewertung und -konfiguration fehlschlagen. Im Abschnitt **[!UICONTROL Service-Instanzen]** wird in einer Spalte für **[!UICONTROL STATUS DES LETZTEN DURCHGANGS]** eine der folgenden Meldungen angezeigt: **[!UICONTROL Erfolg]**, **[!UICONTROL Problem mit Training]** und **[!UICONTROL Fehlgeschlagen]**.

![Status des letzten Durchgangs](./images/errors/last-run-status.png)

Falls **[!UICONTROL Fehlgeschlagen]** oder **[!UICONTROL Problem mit Training]** angezeigt wird, können Sie den Status des Durchgangs auswählen, um einen Seitenbereich zu öffnen. Im Seitenbereich sind der **[!UICONTROL Status des letzten Durchgangs]** und **[!UICONTROL Details des letzten Durchgangs]** einsehbar. Der Abschnitt **[!UICONTROL Details des letzten Durchgangs]** enthält Informationen darüber, warum der Durchgang fehlgeschlagen ist. Falls die Kunden-KI keine Details zu Ihrem Fehler bereitstellen kann, wenden Sie sich an den Support unter Angabe des angegebenen Fehler-Codes.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Inkognito-Zugriff auf Kunden-KI in Chrome nicht möglich

Ladefehler im Inkognito-Modus von Google Chrome sind auf Aktualisierungen in den Sicherheitseinstellungen des Inkognito-Modus von Google Chrome zurückzuführen. An dem Problem wird aktiv mit Chrome gearbeitet, um experience.adobe.com als vertrauenswürdige Domain einzustufen.

<img src="./images/errors/error.PNG" width="500" /><br />

### Empfohlene Fehlerbehebung

Um dieses Problem zu umgehen, müssen Sie experience.adobe.com als Website hinzufügen, die immer Cookies verwenden darf. Navigieren Sie zunächst zu **chrome://settings/cookies**. Scrollen Sie dann nach unten zum Abschnitt **Benutzerdefinierte Einstellungen** und wählen Sie die Schaltfläche **Hinzufügen** neben „Websites, die immer Cookies verwenden dürfen“ aus. Kopieren Sie `[*.]experience.adobe.com` und fügen Sie dies in das angezeigte Popup ein. Aktivieren Sie dann das Kontrollkästchen **Einschließlich Cookies von Drittanbietern auf dieser Website**. Wählen Sie anschließend die Option **Hinzufügen** aus und laden Sie die Kunden-KI im Inkognito-Modus neu.

![Empfohlene Fehlerbehebung](./images/errors/cookies2.gif)

## Modellqualität ist schlecht

Wenn der Fehler „[!UICONTROL Modellqualität ist schlecht. Es wird empfohlen, eine neue App mit der geänderten Konfiguration zu erstellen]“ angezeigt wird, befolgen Sie die unten empfohlenen Schritte zur Fehlerbehebung.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Empfohlene Fehlerbehebung

„Modellqualität ist schlecht“ bedeutet, dass die Modellgenauigkeit nicht innerhalb eines akzeptablen Bereichs liegt. Die Kunden-KI konnte nach dem Training kein zuverlässiges Modell und keine zuverlässige AUC (Area under the ROC Curve) von &lt; 0,65 erstellen. Um den Fehler zu beheben, wird empfohlen, einen der Konfigurationsparameter zu ändern und das Training erneut durchzuführen.

Überprüfen Sie zunächst die Genauigkeit Ihrer Daten. Es ist wichtig, dass Ihre Daten die erforderlichen Felder enthalten, die für Ihr prognostiziertes Ergebnis erforderlich sind.

- Überprüfen Sie, ob Ihr Datensatz die neuesten Daten enthält. Die Kunden-KI geht immer davon aus, dass die Daten beim Auslösen des Modells aktuell sind.
- Überprüfen Sie im definierten Prognose- und Eignungsfenster, ob Daten fehlen. Ihre Daten müssen vollständig und lückenlos sein. Stellen Sie außerdem sicher, dass Ihr Datensatz die [Kunden-KI-Anforderungen an historische Daten](./input-output.md#data-requirements) erfüllt.
- Suchen Sie in den Eigenschaften Ihres Schemafelds nach fehlenden Daten in Commerce, Anwendung, Web und Suche.

Wenn das Problem offenbar nicht auf Ihre Daten zurückzuführen ist, versuchen Sie, die Eignungsbedingung der Population zu ändern, um das Modell auf bestimmte Profile zu beschränken (z. B. `_experience.analytics.customDimensions.eVars.eVar142` in den letzten 56 Tagen vorhanden). Dadurch werden die Population und die Größe der im Trainings-Fenster verwendeten Daten eingeschränkt.

Wenn die Einschränkung der Eignungspopulation nicht funktioniert hat oder nicht möglich ist, ändern Sie das Prognosefenster.

- Versuchen Sie, Ihr Prognosefenster auf 7 Tage zu ändern, und überprüfen Sie, ob der Fehler weiterhin auftritt. Wenn der Fehler nicht mehr auftritt, deutet dies darauf hin, dass Sie möglicherweise nicht über genügend Daten für Ihr definiertes Prognosefenster verfügen.
