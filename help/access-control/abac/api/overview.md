---
keywords: Experience Platform;Startseite;beliebte Themen;api;attributbasierte Zugriffssteuerung;attributbasierte Zugriffssteuerung
solution: Experience Platform
title: Handbuch für die attributbasierte Zugriffssteuerung in der API
description: Mit der attributbasierten Zugriffssteuerungs-API können Sie Rollen und Zugriffsrichtlinien in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 34%

---

# Handbuch zur attributbasierten Zugriffssteuerung für die API

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Die attributbasierte Zugriffssteuerungs-API wird verwendet, um auf Rollen, Produkte, Berechtigungskategorien und Berechtigungssätze in Adobe Experience Platform zuzugreifen und eine Benutzeroberfläche sowie eine RESTful-API bereitzustellen, über die alle verfügbaren Bibliotheksressourcen verfügbar sind.

>[!IMPORTANT]
>
>Die attributbasierte Zugriffssteuerung ist nicht zu verwechseln mit den Data Governance-Funktionen von Experience Platform, mit denen Sie mithilfe von Kennzeichnungen und Richtlinien steuern können, wie Daten in Experience Platform verwendet werden, und nicht damit, welche Benutzenden in Ihrem Unternehmen Zugriff darauf haben. Anweisungen zur programmgesteuerten Nutzung dieser Funktionen finden [ im ](../../../data-governance/api/overview.md) zur Policy Service-API .

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Rollen

Rollen definieren den Zugriff, den Admins, Fachleute oder Endbenutzende auf Ressourcen in Ihrer Organisation haben. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, und Mitglieder Ihrer Organisation können je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden. Weitere Informationen [ Arbeiten mit Rollen in der API finden ](./roles.md) im Handbuch zum roles-Endpunkt .

## Richtlinien

Richtlinien sind Anweisungen, die Attribute zusammenbringen, um zulässige und unzulässige Aktionen festzustellen. Richtlinien können entweder lokal oder global sein und andere Richtlinien überschreiben. Mit dem `/policies`-Endpunkt können Sie Richtlinien in Ihrer Organisation programmgesteuert verwalten. Weitere Informationen zum Arbeiten mit [ in der API finden ](./policies.md) im Handbuch zum policies-Endpunkt .

## Produkte

Mit dem `/products`-Endpunkt in der attributbasierten Zugriffssteuerungs-API können Sie Produkte sowie mit Produkten in Ihrer Organisation verknüpfte Berechtigungskategorien und Berechtigungssätze programmgesteuert verwalten. Weitere Informationen [ Arbeiten mit Produkten und den entsprechenden Berechtigungskategorien und ](./products.md) in der API finden Sie im Handbuch zum products-Endpunkt .

## Nächste Schritte

Um mit Aufrufen mit der attributbasierten Zugriffssteuerungs-API zu beginnen, lesen Sie das [Erste Schritte](./getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
