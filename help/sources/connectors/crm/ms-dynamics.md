---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Übersicht über den Microsoft Dynamics Source Connector
description: Erfahren Sie, wie Sie Microsoft Dynamics mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 50%

---

# Microsoft Dynamics-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] unterstützt die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Microsoft Dynamics].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Feldzuordnung von [!DNL Microsoft Dynamics] zu XDM

Um eine Quellverbindung zwischen [!DNL Microsoft Dynamics] und Experience Platform herzustellen, müssen die [!DNL Microsoft Dynamics] Quelldatenfelder den entsprechenden XDM-Zielfeldern zugeordnet werden, bevor sie in Experience Platform aufgenommen werden können.

Ausführliche Informationen zu den Regeln für die Feldzuordnung zwischen [!DNL Microsoft Dynamics] Datensätzen und Experience Platform finden Sie unten:

- [Kontakte](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Konten](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunities](../adobe-applications/mapping/dynamics.md#opportunities)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Kampagnen](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing-Liste](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Marketing-Listenmitglieder](../adobe-applications/mapping/dynamics.md#marketing-list-members)

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Experience Platform] mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Experience Platform] mithilfe von APIs

- [Erstellen einer Microsoft Dynamics-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Microsoft Dynamics] mit [!DNL Experience Platform] über die Benutzeroberfläche

- [Erstellen einer Microsoft Dynamics-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/crm/dynamics.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
