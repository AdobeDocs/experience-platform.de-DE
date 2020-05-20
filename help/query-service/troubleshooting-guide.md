---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Fehlerbehebung beim Adobe Experience Platform Abfrage Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---


# Fehler und Fehlerbehebung

## REST-API-Fehler

| HTTP-Statuscode | Beschreibung | Mögliche Ursachen |
| ---------------- | ----------- | --------------- |
| 400 | Ungültige Anforderung | Falsche oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungstoken |
| 500 | Interner Server-Fehler | Systemfehler |

## PostgreSQL-API-Fehler

| Fehlercode und Verbindungsstatus | Beschreibung | Mögliche Ursache |
| ------------------------------- | ----------- | -------------- |
| **28P01** Beginn-up - Authentifizierung | Ungültiges Kennwort | Ungültiges Authentifizierungstoken |
| **28000** Beginn-up - Authentifizierung | Ungültiger Autorisierungstyp | Ungültiger Autorisierungstyp. Muss `AuthenticationCleartextPassword`sein. |
| **42P12** Beginn-up - Authentifizierung | Keine Tabellen gefunden | Keine Tabellen zur Verwendung gefunden |
| **42601** Abfrage | Syntaxfehler | Ungültiger Befehl- oder Syntaxfehler |
| **58000** Abfrage | Systemfehler | Systemfehler |
| **42P01** Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P07** Abfrage | Tabelle vorhanden | Tabelle ist bereits mit demselben Namen vorhanden (CREATE TABLE) |
| **53400** Abfrage | LIMIT überschreitet den Maximalwert | Benutzer hat eine LIMIT-Klausel über 100.000 angegeben |
| **53400** Abfrage | Statement timeout | Die abgesendete Live-Anweisung dauerte mehr als 10 Minuten |
| **08P01** N/A | Nicht unterstützter Nachrichtentyp | Nicht unterstützter Nachrichtentyp |
