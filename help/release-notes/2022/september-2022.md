---
title: Adobe Experience Platform - Versionshinweise - September 2022
description: Die Versionshinweise für Adobe Experience Platform vom September 2022.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 38%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 28. September 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Identity Service](#identity-service)
- [Quellen](#sources)

## Identity Service {#identity-service}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, wodurch jeder Kunde über mehrere &quot;Identitäten&quot;verfügt.

Mit Adobe Experience Platform Identity Service erhalten Sie einen besseren Überblick über Ihren Kunden und sein Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit für effektive, persönliche digitale Erlebnisse sorgen können.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Löschen von Datensätzen | Identity Service unterstützt jetzt das Löschen von Datensätzen, wenn über die [Catalog Service-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), Benutzeroberfläche oder Datenhygiene. Lesen Sie das Handbuch unter [Löschen von Datensätzen in der Benutzeroberfläche](../../catalog/datasets/user-guide.md#delete-a-dataset) für weitere Informationen. |

Weitere Informationen zum Identity Service finden Sie im Abschnitt [Identity Service - Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auswirkungen der Population des Audience Manager-Segments auf das Echtzeit-Kundenprofil | Die Erfassung umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mit der Audience Manager-Quelle an Platform senden. Das bedeutet, dass die Auswahl aller Segmente potenziell zu einer Profilanzahl führen kann, die über Ihrer Lizenznutzungsberechtigung liegt. Weitere Informationen finden Sie im Abschnitt [Übersicht über die Audience Manager-Quelle](../../sources/connectors/adobe-applications/audience-manager.md). Informationen zur Verwendung Ihrer Lizenz finden Sie in der Dokumentation unter [Verwenden des Dashboards zur Lizenznutzung](../../dashboards/guides/license-usage.md). |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).