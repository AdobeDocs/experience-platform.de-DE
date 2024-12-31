---
title: Datenschutz, Sicherheit und Governance im KI-Assistenten
description: Erfahren Sie mehr über die Datenschutz-, Sicherheits- und Governance-Praktiken für KI-Assistenten.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Datenschutz, Sicherheit und Governance im KI-Assistenten

Der KI-Assistent in Adobe Experience Platform ist so konzipiert, dass Datenschutz, Sicherheit und Governance im Vordergrund stehen.

Lesen Sie dieses Dokument, um mehr über die auf das Kundenvertrauen fokussierten Funktionen zu erfahren, die Sie vom KI-Assistenten erwarten können:

* KI Assistant verwendet heute keine personenbezogenen Daten, auch nicht für Trainingszwecke.
* Der KI-Assistent kennt keine Verbraucherdaten.
* Alle vorhandenen [Zugriffssteuerungsrichtlinien](../access-control/home.md) werden vom KI-Assistenten berücksichtigt.
   * Alle neuen attributbasierten Zugriffssteuerungsrichtlinien werden nach maximal 24 Stunden im KI-Assistenten angezeigt*
* Die Interaktion mit dem KI-Assistenten muss ausdrücklich erlaubt sein.
   * Sie können die Berechtigungen für Experience Platform und Journey Optimizer mithilfe der [Benutzeroberfläche „Berechtigungen“ unterschiedlich ](../access-control/abac/ui/permissions.md) und mithilfe der [Admin Console ](../access-control/ui/browse.md) Berechtigungen für Customer Journey Analytics zuweisen.
   * Die Berechtigungen sind granular und Ihr Sandbox-Administrator kann konfigurieren, welche Ihrer Benutzer bzw. Benutzerinnen verschiedene Fragenkategorien stellen können (Produktkenntnisfragen mit dem KI-Assistenten oder Fragen zu operativen Einblicken).
* Der KI-Assistent ist eine HIPAA-fähige Funktion, wenn sie in Kombination mit Adobe Experience Platform Healthcare Shield verwendet wird.
* Sie können ein Protokoll Ihrer vorherigen Interaktionen mit dem KI-Assistenten mit einer 30-Tage-Aufbewahrungsrichtlinie anzeigen.
* Der KI-Assistent basiert auf Sandbox-spezifischen Daten und der öffentlichen Adobe-Dokumentation, wenn auf Benutzeraufforderungen reagiert wird. Daten werden nicht über Sandboxes hinweg freigegeben.
* Eingabeaufforderungen, die Sie an den KI-Assistenten senden, werden nicht an andere Kunden weitergegeben.

**Dies bedeutet, dass es bis zu 24 Stunden dauert, bis neue Kennzeichnungen zu Feldern und Objekten hinzugefügt oder neue Richtlinien erstellt werden, die vom KI-Assistenten berücksichtigt werden. Während dieser 24 Stunden können Benutzer mit neu eingeschränktem Zugriff weiterhin auf diese Felder und Objekte zugreifen.*
