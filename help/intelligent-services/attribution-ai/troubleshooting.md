---
keywords: Experience Platform;Erste Schritte;Attributions-KI;beliebte Themen;Input-Attributions-KI;Output-Attributions-KI;Fehlerbehebungs-Attributions-KI;Fehler-Attributions-KI
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Fehlerbehebung bei der Attributions-KI
description: Hier finden Sie Antworten auf häufige Fehler in der Attributions-KI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 100%

---

# Fehlerbehebung bei der Attributions-KI

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Attributions-KI.

## Inkognito-Zugriff auf Attributions-KI in Chrome nicht möglich

Ladefehler im Inkognito-Modus von Google Chrome sind auf Aktualisierungen in den Sicherheitseinstellungen des Inkognito-Modus von Google Chrome zurückzuführen. An dem Problem wird aktiv mit Chrome gearbeitet, um experience.adobe.com als vertrauenswürdige Domain einzustufen.

<img src="./images/faq/error.PNG" width="500" /><br />

### Empfohlene Fehlerbehebung

Um dieses Problem zu umgehen, müssen Sie experience.adobe.com als Website hinzufügen, die immer Cookies verwenden darf. Navigieren Sie zunächst zu **chrome://settings/cookies**. Scrollen Sie dann nach unten zum Abschnitt **Benutzerdefinierte Einstellungen** und wählen Sie die Schaltfläche **Hinzufügen** neben „Websites, die immer Cookies verwenden dürfen“ aus. Kopieren Sie `[*.]experience.adobe.com` und fügen Sie dies in das angezeigte Popup ein. Aktivieren Sie dann das Kontrollkästchen **Einschließlich Cookies von Drittanbietern auf dieser Website**. Wählen Sie anschließend die Option **Hinzufügen** aus und laden Sie die Attributions-KI im Inkognito-Modus neu.

![empfohlene Fehlerbehebung](./images/faq/cookies2.gif)
