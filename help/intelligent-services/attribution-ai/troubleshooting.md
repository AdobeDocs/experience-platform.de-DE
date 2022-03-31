---
keywords: Experience Platform; Erste Schritte; Attribution-Hilfe; beliebte Themen; Attribution-AI-Eingabe; Attribution-AI-Ausgabe; Fehlerbehebung bei Attributionsai; Attributionsai-Fehler
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Fehlerbehebung bei Attribution AI
description: Hier finden Sie Antworten auf häufige Fehler in Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Fehlerbehebung bei Attribution AI

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Attribution AI.

## Zugriff auf Attribution AI in Chrome-Inkognito nicht möglich

Das Laden von Fehlern im Inkognito-Modus von Google Chrome ist auf Aktualisierungen in den Sicherheitseinstellungen des Google Chrome-Inkognito-Modus zurückzuführen. Das Problem wird aktiv mit Chrome bearbeitet, um experience.adobe.com zu einer vertrauenswürdigen Domäne zu machen.

<img src="./images/faq/error.PNG" width="500" /><br />

### Empfohlene Fehlerbehebung

Um dieses Problem zu umgehen, müssen Sie experience.adobe.com als Site hinzufügen, die immer Cookies verwenden kann. Beginnen Sie, indem Sie zu **chrome://settings/cookies**. Scrollen Sie dann nach unten zum **Benutzerdefinierte Verhaltensweisen** und anschließend die **Hinzufügen** neben &quot;Sites, die immer Cookies verwenden können&quot;. Kopieren Sie in das angezeigte Popover-Element und fügen Sie `[*.]experience.adobe.com` und wählen Sie dann **Einschließen von Drittanbieter-Cookies** auf dieser Site aktivieren. Wählen Sie nach Abschluss **Hinzufügen** und das Attribution AI in Inkognito neu laden.

![empfohlene Korrektur](./images/faq/cookies2.gif)
