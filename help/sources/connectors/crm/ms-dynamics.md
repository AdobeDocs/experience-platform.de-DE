---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Microsoft Dynamics über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 4fbf1b9a55c755d0bac9e15efbf6bdb25fa24deb
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 56%

---

# Microsoft Dynamics-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] bietet Unterstützung für die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Microsoft Dynamics].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Feldzuordnung aus [!DNL Microsoft Dynamics] in XDM

So richten Sie eine Quellverbindung zwischen [!DNL Microsoft Dynamics] und Platform, die [!DNL Microsoft Dynamics] Quelldatenfelder müssen ihren entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Microsoft Dynamics] Datensätze und Plattform:

- [Kontakte](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Konten](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunities](../adobe-applications/mapping/dynamics.md#opportunities)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Kampagnen](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing-Experte](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Mitglieder der Marketing-Liste](../adobe-applications/mapping/dynamics.md#marketing-list-members)

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Microsoft Dynamics] mit mithilfe von APIs oder der Benutzeroberfläche:[!DNL Platform]

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Basisverbindung mit Microsoft Dynamics mithilfe der Flow Service-API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Datentabellen mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer Quellverbindung mit Microsoft Dynamics in der Benutzeroberfläche](../../tutorials/ui/create/crm/dynamics.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
