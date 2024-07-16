---
title: Erweiterte Aktivierung für Audience Manager
description: Erfahren Sie, wie Sie Audience Manager-Zielgruppen über Audience Manager Extended Activation für Social- und Werbeziele aktivieren.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Erweiterte Aktivierung für Audience Manager

Auf der Grundlage von Adobe Experience Platform hilft Audience Manager Extended Activation vorhandenen [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) -Benutzern dabei, ihre Zielgruppen für [Social](../destinations/catalog/social/overview.md) und [Werbung](../destinations/catalog/advertising/overview.md) aus Real-Time CDP zu aktivieren, z. B. für [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) und mehr.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] ist nur für bestehende [!DNL Audience Manager] -Benutzer verfügbar.

## Terminologie {#terminology}

Audience Manager Extended Activation verwendet Konzepte und Komponenten aus Adobe Experience Platform. Um den Workflow &quot;Erweiterte Aktivierung&quot;und die von Ihnen verwendeten Komponenten besser zu verstehen, sollten Sie über grundlegende Kenntnisse der folgenden Konzepte verfügen:

* [Zielgruppen](../segmentation/ui/overview.md): Zielgruppen sind Gruppen von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen oder der Zielgruppenzusammensetzung (plattformgenerierte Zielgruppe) oder aus externen Quellen wie benutzerdefinierten Uploads (extern generierte Zielgruppe) erstellt werden. Unter Erweiterte Aktivierung werden Ihre Audience Manager-Segmente (Zielgruppen) als [benutzerdefinierte Uploads](../segmentation/ui/audience-portal.md#import-audience) importiert.
* [Source-Connectoren](../sources/home.md): Source-Connectoren (auch als Quellen bezeichnet) helfen Experience Platform-Benutzern, Daten aus verschiedenen Quellen einfach zu erfassen, sodass Daten strukturiert, beschriftet und mithilfe von Experience Platform-Diensten erweitert werden können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.
* [Ziel-Connectoren](../destinations/home.md): Ziele beschreiben jeden Endpunkt, z. B. eine Adobe-Anwendung, Werbeplattform, einen Cloud-Speicher-Dienst oder einen Marketing-Dienst, an dem eine Zielgruppe aktiviert und bereitgestellt wird. [!DNL Expanded Activation] unterstützt die Aktivierung von Zielgruppen für [Werbung](../destinations/catalog/advertising/overview.md) - und [Social](../destinations/catalog/social/overview.md) -Ziel-Connectoren.

## Voraussetzungen {#prerequisites}

Bevor Sie Zielgruppen über die erweiterte Aktivierung aktivieren können, stellen Sie sicher, dass Sie die unten beschriebenen Voraussetzungen erfüllen.

### Benutzer- und Rollenanforderungen {#permission-requirements}

Bevor Sie [!DNL Expanded Activation] verwenden können, müssen Sie ein Benutzerkonto aus der Admin Console erstellen und es der [!DNL Expanded Activation] -Rolle zuweisen. Detaillierte Anweisungen dazu finden Sie auf der Seite [Administration](administration.md) .

### Zielgruppenanforderungen {#audience-requirements}

Um Zielgruppen über [!DNL Expanded Activation] zu aktivieren, stellen Sie sicher, dass Ihre Audience Manager-Zielgruppen auf **Hash-E-Mail-Adressen** basieren. Je nach Verwendung Ihrer Audience Manager gibt es zwei Möglichkeiten, dies sicherzustellen:

* Wenn Sie die Funktion &quot;[Audience Manager People-based Destinations](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview)&quot;verwenden, nehmen Sie in Audience Manager bereits Hash-E-Mail-Adressen auf. Es gibt keinen weiteren Schritt, den Sie in diesem Fall unternehmen müssen. Sie können die Aktivierung von Zielgruppen über die erweiterte Aktivierung](activate-audiences.md) überspringen.[
* Wenn Sie _nicht_ mit der Funktion [People-based Destinations auf Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) verwenden, müssen Sie eine neue Datenquelle in Audience Manager erstellen und diese zum Speichern von Hash-E-Mail-Adressen verwenden. Weitere Informationen dazu finden Sie in der Dokumentation zu [Konfigurieren einer Datenquelle für Hash-E-Mail-Workflows](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) . Nachdem Sie Hash-E-Mail-Adressen in Ihrer Audience Manager-Datenquelle erfasst haben, lesen Sie die Dokumentation unter [Aktivieren von Zielgruppen durch erweiterte Aktivierung](activate-audiences.md).

## Nächste Schritte {#next-steps}

Nachdem Sie nun ein besseres Verständnis der Anwendungsfälle und Vorteile der Verwendung von [!DNL Expanded Activation] haben, starten Sie die [Konfiguration Ihres Kontos](administration.md) und dann [Aktivieren Ihrer Zielgruppen](activate-audiences.md).
