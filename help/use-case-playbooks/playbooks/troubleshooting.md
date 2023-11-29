---
solution: Experience Platform
title: Beheben von Playbook-Problemen
description: Erfahren Sie mehr über häufige Probleme mit Playbooks und deren Behebung
badgeBeta: label="Beta" type="Informative"
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 5226a3f9a6da22c2c199f8efffd71360af034dcc
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 100%

---


# (Beta) Fehlerbehebung und bekannte Einschränkungen

>[!AVAILABILITY]
>
>Diese Funktion befinden sich derzeit in der Betaphase und steht nicht allen Benutzenden zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Für die Betaversion der Funktion [!UICONTROL Playbooks für Anwendungsfälle] beachten Sie die Tipps zur Fehlerbehebung und die bekannten Einschränkungen.

## Bekannte Einschränkungen {#known-limitations}

Wenn Sie eine neue Instanz eines Playbooks erstellen, werden neue Assets generiert. Bei generierten Schemata gilt jedoch: Wenn ein Schema in einer Instanz eines Playbooks generiert wird und Sie es bearbeiten, wird bei Aktivierung einer anderen Instanz des Playbooks *kein* anderes Schema generiert. Stattdessen verwenden Sie weiterhin das Schema, das Sie in der neuen Instanz bearbeitet haben.
