---
title: Erweiterte Aktivierung für Audience Manager
description: Erfahren Sie, wie Sie Audience Manager-Zielgruppen über Audience Manager Expanded Activation für Social-Media- und Werbeziele aktivieren.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# Erweiterte Aktivierung für Audience Manager

Die auf Adobe Experience Platform aufbauende erweiterte Audience Manager-Aktivierung unterstützt bestehende [Audience Manager](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/aam-home)-Benutzende bei der Aktivierung ihrer Zielgruppen für [Social](../destinations/catalog/social/overview.md)- und [Advertising](../destinations/catalog/advertising/overview.md)-Zielplattformen von Real-Time CDP, z. B. [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) und mehr.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] ist nur für bestehende [!DNL Audience Manager] verfügbar.

## Terminologie {#terminology}

Audience Manager Expanded Activation verwendet Konzepte und Komponenten aus Adobe Experience Platform. Um den erweiterten Aktivierungs-Workflow und die verwendeten Komponenten besser zu verstehen, müssen Sie über grundlegende Kenntnisse der folgenden Konzepte verfügen:

* [Zielgruppen](../segmentation/ui/overview.md): Zielgruppen sind Gruppen von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen oder der Zielgruppenkomposition (Experience Platform-generierte Zielgruppe) oder aus externen Quellen wie benutzerdefinierten Uploads (extern generierte Zielgruppe) generiert werden. In der erweiterten Aktivierung werden Ihre Audience Manager-Segmente (Zielgruppen) als &quot;[ Uploads“ ](../segmentation/ui/audience-portal.md#import-audience).
* [Source-Connectoren](../sources/home.md): Source-Connectoren (auch als Quellen bezeichnet) helfen Experience Platform-Benutzern, Daten aus mehreren Quellen einfach aufzunehmen, wodurch die Strukturierung, Beschriftung und Verbesserung von Daten mithilfe von Experience Platform-Services ermöglicht wird. Daten können aus einer Vielzahl von Quellen aufgenommen werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.
* [Ziel-Connectoren](../destinations/home.md): Ziele beschreiben jeden Endpunkt, z. B. ein Adobe-Programm, eine Werbeplattform, einen Cloud-Speicher-Service oder einen Marketing-Service, bei dem eine Zielgruppe aktiviert und bereitgestellt wird. [!DNL Expanded Activation] unterstützt die Aktivierung von Zielgruppen für [Advertising](../destinations/catalog/advertising/overview.md) und [Social](../destinations/catalog/social/overview.md)-Ziel-Connectoren.

## Voraussetzungen {#prerequisites}

Bevor Sie Zielgruppen über erweiterte Aktivierung aktivieren können, stellen Sie sicher, dass Sie die unten beschriebenen Voraussetzungen erfüllen.

### Anforderungen an Benutzer und Rollen {#permission-requirements}

Bevor Sie [!DNL Expanded Activation] verwenden können, müssen Sie über die Admin Console ein Benutzerkonto erstellen und es der Rolle [!DNL Expanded Activation] zuweisen. Detaillierte Anweisungen dazu finden [ auf ](administration.md) Seite „Administration“.

### Zielgruppenanforderungen {#audience-requirements}

Um Zielgruppen über [!DNL Expanded Activation] zu aktivieren, stellen Sie sicher, dass Ihre Audience Manager-Zielgruppen auf (**E-Mail-Adressen)**. Abhängig von Ihrer Audience Manager-Nutzung gibt es zwei Möglichkeiten, dies sicherzustellen:

* Wenn Sie die Funktion [Personenbasierte Ziele in Audience Manager](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) verwenden, erfassen Sie bereits Hash-E-Mail-Adressen in Audience Manager. Es gibt in diesem Fall keinen zusätzlichen Schritt, den Sie ausführen müssen. Sie können zu [Aktivieren von Zielgruppen durch erweiterte Aktivierung“ ](activate-audiences.md).
* Wenn Sie _nicht_ die Funktion [Audience Manager People-Based Destinations](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) verwenden, müssen Sie eine neue Datenquelle in Audience Manager erstellen und sie zum Speichern von Hash-E-Mail-Adressen verwenden. Weitere Informationen dazu finden Sie in [ Dokumentation unter „Konfigurieren einer Datenquelle für ](https://experienceleague.adobe.com/de/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails)-Workflows“. Nachdem Sie Hash-E-Mail-Adressen in Ihre Audience Manager-Datenquelle aufgenommen haben, lesen Sie die Dokumentation unter [Aktivieren von Zielgruppen durch erweiterte Aktivierung](activate-audiences.md).

## Nächste Schritte {#next-steps}

Nachdem Sie nun die Anwendungsfälle und Vorteile der Verwendung von [!DNL Expanded Activation] besser verstehen, können Sie [Ihr Konto konfigurieren](administration.md) und dann [Zielgruppen aktivieren](activate-audiences.md).
