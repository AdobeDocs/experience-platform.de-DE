---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Übersicht über den Microsoft Dynamics Source Connector
description: Erfahren Sie, wie Sie Microsoft Dynamics über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 50%

---

# Microsoft Dynamics-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] unterstützt die Aufnahme von Daten aus einem Drittanbieter-CRM-System. Unterstützung für CRM-Anbieter umfasst [!DNL Microsoft Dynamics].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Feldzuordnung von [!DNL Microsoft Dynamics] zu XDM

Um eine Quellverbindung zwischen [!DNL Microsoft Dynamics] und Platform herzustellen, müssen die [!DNL Microsoft Dynamics]-Quelldatenfelder den entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Im Folgenden finden Sie detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Microsoft Dynamics] Datensätzen und Platform:

- [Kontakte](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Konten](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunities](../adobe-applications/mapping/dynamics.md#opportunities)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Kampagnen](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing-Experte](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Marketing-Listenmitglieder](../adobe-applications/mapping/dynamics.md#marketing-list-members)

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche [!DNL Microsoft Dynamics] mit [!DNL Platform] verbinden:

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Basisverbindung mit Microsoft Dynamics mithilfe der Flow Service-API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer Quellverbindung mit Microsoft Dynamics in der Benutzeroberfläche](../../tutorials/ui/create/crm/dynamics.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
