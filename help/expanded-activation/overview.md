---
title: Erweiterte Aktivierung des Audience Managers
description: Erfahren Sie, wie Sie Audience Manager-Zielgruppen über Audience Manager Extended Activation für Social- und Werbeziele aktivieren.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Erweiterte Aktivierung des Audience Managers

Auf Adobe Experience Platform aufbauend hilft die erweiterte Aktivierung von Audience Managern vorhandenen [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) Benutzer aktivieren ihre Zielgruppen für [social](../destinations/catalog/social/overview.md) und [Werbung](../destinations/catalog/advertising/overview.md) Zielplattformen aus Real-Time CDP, wie z. B. [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md)und mehr.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] ist nur für bestehende verfügbar [!DNL Audience Manager] Benutzer.

## Terminologie {#terminology}

Audience Manager Extended Activation verwendet Konzepte und Komponenten aus Adobe Experience Platform. Um den Workflow &quot;Erweiterte Aktivierung&quot;und die von Ihnen verwendeten Komponenten besser zu verstehen, sollten Sie über grundlegende Kenntnisse der folgenden Konzepte verfügen:

* [Zielgruppen](../segmentation/ui/overview.md): Zielgruppen sind Gruppen von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen oder der Zielgruppenzusammensetzung (plattformgenerierte Zielgruppe) oder aus externen Quellen wie benutzerdefinierten Uploads (extern generierte Zielgruppe) erstellt werden. Unter Erweiterte Aktivierung werden Ihre Audience Manager-Segmente (Zielgruppen) als [benutzerspezifische Uploads](../segmentation/ui/overview.md#import-audience).
* [Quell-Connectoren](../sources/home.md): Mithilfe von Quell-Connectoren (auch als Quellen bezeichnet) können Experience Platform-Benutzer Daten aus mehreren Quellen einfach erfassen und so die Strukturierung, Kennzeichnung und Verbesserung von Daten mithilfe von Experience Platform-Services ermöglichen. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.
* [Ziel-Connectoren](../destinations/home.md): Ziele beschreiben jeden Endpunkt, z. B. eine Adobe-Anwendung, eine Werbeplattform, einen Cloud-Speicher-Dienst oder einen Marketing-Dienst, bei dem eine Zielgruppe aktiviert und bereitgestellt wird. [!DNL Expanded Activation] unterstützt die Aktivierung von Zielgruppen in [Werbung](../destinations/catalog/advertising/overview.md) und [social](../destinations/catalog/social/overview.md) Ziel-Connectoren.

## Voraussetzungen {#prerequisites}

Bevor Sie Zielgruppen über die erweiterte Aktivierung aktivieren können, stellen Sie sicher, dass Sie die unten beschriebenen Voraussetzungen erfüllen.

### Benutzer- und Rollenanforderungen {#permission-requirements}

Bevor Sie [!DNL Expanded Activation], müssen Sie ein Benutzerkonto aus der Admin Console erstellen und es der [!DNL Expanded Activation] Rolle. Siehe [Administration](administration.md) für detaillierte Anweisungen.

### Zielgruppenanforderungen {#audience-requirements}

So aktivieren Sie Zielgruppen durch [!DNL Expanded Activation], stellen Sie sicher, dass Ihre Audience Manager-Zielgruppen auf **Hash-E-Mail-Adressen**. Je nach Verwendung Ihrer Audience Manager gibt es zwei Möglichkeiten, dies sicherzustellen:

* Wenn Sie die [Benutzerbasierte Audience Manager-Ziele](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) verwenden, nehmen Sie in Audience Manager bereits Hash-E-Mail-Adressen auf. Es gibt keinen weiteren Schritt, den Sie in diesem Fall unternehmen müssen. Sie können zu [Aktivieren von Zielgruppen durch erweiterte Aktivierung](activate-audiences.md).
* Wenn Sie _not_ mithilfe der [Benutzerbasierte Audience Manager-Ziele](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) verwenden, müssen Sie eine neue Datenquelle in Audience Manager erstellen und diese zum Speichern von Hash-E-Mail-Adressen verwenden. Siehe die Dokumentation unter [Konfigurieren einer Datenquelle für Hash-E-Mail-Workflows](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) , um zu erfahren, wie man das macht. Nachdem Sie Hash-E-Mail-Adressen in Ihrer Audience Manager-Datenquelle erfasst haben, lesen Sie die Dokumentation unter [Aktivieren von Zielgruppen durch erweiterte Aktivierung](activate-audiences.md).

## Nächste Schritte {#next-steps}

Jetzt, da Sie ein besseres Verständnis der Anwendungsfälle und Vorteile der Verwendung von [!DNL Expanded Activation], start [Konto konfigurieren](administration.md) und dann [Zielgruppen aktivieren](activate-audiences.md).

