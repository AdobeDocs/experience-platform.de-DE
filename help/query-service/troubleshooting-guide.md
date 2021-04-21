---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Fehlerbehebungshandbuch;FAQ;Fehlerbehebung;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung beim Abfrage Service
topic-legacy: troubleshooting
description: Dieses Dokument enthält Informationen zu häufig auftretenden Fehlercodes und möglichen Ursachen.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 82%

---

# [!DNL Query Service] Handbuch zur Fehlerbehebung

## REST-API-Fehler

| HTTP-Status-Code | Beschreibung | Mögliche Ursachen |
| ---------------- | ----------- | --------------- |
| 400 | Ungültige Anfrage | Falsch formulierte oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungs-Token |
| 500 | Interner Server-Fehler | Interner Systemfehler |

## PostgreSQL-API-Fehler

| Fehlercode und Verbindungsstatus | Beschreibung | Mögliche Ursache |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start-up – Authentifizierung | Ungültiges Kennwort | Ungültiges Authentifizierungs-Token |
| **28000** Start-up – Authentifizierung | Ungültiger Autorisierungstyp | Ungültiger Autorisierungstyp. Muss `AuthenticationCleartextPassword`sein. |
| **42P12** Start-up – Authentifizierung | Keine Tabellen gefunden | Keine Tabellen zur Verwendung gefunden |
| **42601** Abfrage | Syntaxfehler | Ungültiger Befehl- oder Syntaxfehler |
| **58000** Abfrage | Systemfehler | Interner Systemfehler |
| **42P01** Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P07** Abfrage | Tabelle vorhanden | Tabelle ist bereits mit demselben Namen vorhanden (CREATE TABLE) |
| **53400** Abfrage | LIMIT überschreitet den Maximalwert | Benutzer hat eine LIMIT-Klausel über 100.000 angegeben |
| **53400** Abfrage | Anweisungs-Timeout | Die abgesendete Live-Anweisung dauerte mehr als 10 Minuten |
| **08P01** K. A. | Nicht unterstützter Nachrichtentyp | Nicht unterstützter Nachrichtentyp |
