---
keywords: Experience Platform; Startseite; beliebte Themen; API; attributbasierte Zugriffssteuerung; attributbasierte Zugriffssteuerung
solution: Experience Platform
title: API-Anleitung zur Attributbasierten Zugriffssteuerung
description: Mit der Attributbasierten Zugriffssteuerungs-API können Sie Rollen und Richtlinien in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
hide: true
hidefromtoc: true
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 11%

---

# API-Handbuch zur Attributbasierten Zugriffskontrolle

>[!IMPORTANT]
>
>Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung.

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administratoren den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Ein Administrator definiert Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Die attributbasierte Zugriffssteuerungs-API wird verwendet, um auf Rollen, Produkte, Berechtigungskategorien und Berechtigungssätze in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche und RESTful-API bereitzustellen, über die alle verfügbaren Bibliotheksressourcen zugänglich sind.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Rollen

Rollen definieren den Zugriff, den ein Administrator, ein Spezialist oder ein Endbenutzer auf Ressourcen in Ihrem Unternehmen hat. In einer rollenbasierten Zugriffskontrollumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen und Mitglieder Ihrer Organisation können je nach dem Umfang der Ansicht oder des Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden. Siehe [Benutzerendpunkt-Handbuch](./roles.md) Weitere Informationen zum Arbeiten mit Rollen in der API.

## Richtlinien

Richtlinien sind Aussagen, die Attribute zusammenbringen, um zulässige und unzulässige Handlungen festzustellen. Richtlinien können lokal oder global sein und andere Richtlinien überschreiben. Die `/policies` -Endpunkt ermöglicht Ihnen die programmgesteuerte Verwaltung von Richtlinien in Ihrem Unternehmen. Siehe [Richtlinien-Endpunktleitfaden](./policies.md) Weitere Informationen zum Arbeiten mit Richtlinien in der API.

## Produkte

Die `/products` -Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Produkte sowie Berechtigungskategorien und Berechtigungssätze, die mit Produkten in Ihrer Organisation verknüpft sind, programmgesteuert verwalten. Siehe [Endpunktleitfaden für Produkte](./products.md) für weitere Informationen zum Arbeiten mit Produkten und den zugehörigen Berechtigungskategorien und Berechtigungssätzen in der API.

## Nächste Schritte

Um Aufrufe mit der attributbasierten Zugriffssteuerungs-API zu starten, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
