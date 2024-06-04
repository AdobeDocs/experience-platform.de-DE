---
title: Datenschutz, Sicherheit und Governance im KI-Assistenten
description: Erfahren Sie mehr über die Datenschutz-, Sicherheits- und Governance-Verfahren für AI Assistant.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: 1762fcbcc730ccb08340a71383c90404c3fea614
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Datenschutz, Sicherheit und Governance im KI-Assistenten

Die KI-Assistenzkraft in Adobe Experience Platform basiert auf Datenschutz, Sicherheit und Governance.

Lesen Sie dieses Dokument, um mehr über die vertrauensorientierten Funktionen von AI Assistant zu erfahren:

* Derzeit werden keine personenbezogenen Daten von AI Assistant verwendet, auch nicht zu Trainingszwecken.
* Der KI-Assistent kennt keine Verbraucherdaten.
* Alle vorhandenen [Zugriffskontrolle](../access-control/home.md) Richtlinien werden von der KI-Assistenzkraft berücksichtigt.
   * Alle neuen attributbasierten Zugriffssteuerungsrichtlinien werden nach maximal 24 Stunden im AI-Assistenten angezeigt.*
* Sie müssen über eine explizite Berechtigung zur Interaktion mit dem AI-Assistenten verfügen.
   * Sie können Berechtigungen für Experience Platform und Journey Optimizer mithilfe der Variablen [Berechtigungs-Benutzeroberfläche](../access-control/abac/ui/permissions.md) und Sie können die [Admin Console](../access-control/ui/browse.md) , um Berechtigungen für Customer Journey Analytics zuzuweisen.
   * Die Berechtigungen sind detailliert und Ihr Sandbox-Administrator kann konfigurieren, welche Ihrer Benutzer verschiedene Fragekategorien stellen kann (produktbezogene Fragen mit dem KI-Assistenten oder Fragen zu betrieblichen Einblicken).
* Die KI-Assistenzkraft ist eine HIPAA-fähige Funktion und erfüllt die HIPAA-Anforderungen in Bezug auf die Verarbeitung und Verwendung geschützter Gesundheitsinformationen (PHI).
* Sie können ein Protokoll Ihrer vorherigen Interaktionen mit AI Assistant mit einer 30-tägigen Aufbewahrungsrichtlinie anzeigen.
* Der AI-Assistent basiert auf Sandbox-spezifischen Daten und der öffentlichen Adobe-Dokumentation, wenn auf Benutzeraufforderungen geantwortet wird. Daten werden nicht über Sandboxes hinweg freigegeben.
* Die von Ihnen für den AI-Assistenten bereitgestellten Eingabeaufforderungen werden nicht an andere Kunden weitergegeben.


**Dies bedeutet, dass es bis zu 24 Stunden dauern wird, bis neue Beschriftungen zu Feldern und Objekten hinzugefügt oder neue Richtlinien erstellt werden. In diesen 24 Stunden können Benutzer mit neu eingeschränktem Zugriff weiterhin auf diese Felder und Objekte zugreifen.*
