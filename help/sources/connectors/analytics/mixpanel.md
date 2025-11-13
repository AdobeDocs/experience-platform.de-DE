---
title: Übersicht über den Mixpanel Source Connector
description: Erfahren Sie, wie Sie Mixpanel mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 13%

---

# [!DNL Mixpanel]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einem Analyseprogramm eines Drittanbieters. Der Support für Analytics-Anbieter umfasst [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Tool zur Produktanalyse, mit dem Sie Daten darüber erfassen können, wie Benutzende mit einem digitalen Produkt interagieren. Mit Mixpanel können Sie diese Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit nur wenigen Klicks abfragen und visualisieren können.

Sources nutzt die [Mixpanel-Ereignisexport-API > Download](https://developer.mixpanel.com/reference/raw-event-export), um Ihre Ereignisdaten so herunterzuladen, wie sie in [!DNL Mixpanel] empfangen und gespeichert werden, sowie alle Ereigniseigenschaften (einschließlich `distinct_id`) und den genauen Zeitstempel, an den das Ereignis an Experience Platform gesendet wurde. Mixpanel verwendet Bearer-Token als Authentifizierungsmechanismus für die Kommunikation mit der Mixpanel-Ereignisexport-API.

## Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

## [!DNL Mixpanel] authentifizieren

In diesem Abschnitt werden die Schritte beschrieben, die erforderlich sind, um Ihr -Konto zu authentifizieren und Ihre [!DNL Mixpanel] an Experience Platform zu übertragen.

Um eine [!DNL Mixpanel] Quellverbindung und einen Datenfluss zu erstellen, müssen Sie zunächst über ein gültiges [!DNL Mixpanel]-Konto verfügen. Wenn Sie kein gültiges [!DNL Mixpanel]-Konto haben, lesen Sie die Seite [Mixpanel-Register](https://mixpanel.com/register/), um Ihr Konto zu erstellen.

Nachdem Sie ein [!DNL Mixpanel]-Konto erfolgreich erstellt haben, navigieren Sie zur Registerkarte [!DNL Project Details] auf der Seite [!DNL Project Seettings] der [!DNL Mixpanel]-Benutzeroberfläche, um Ihre Projekt-ID abzurufen und Ihre Zeitzone zu konfigurieren.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigieren Sie dann auf der [!DNL Service Accounts] in der [!DNL Project Settings]-Benutzeroberfläche zur Registerkarte [!DNL Mixpanel] , um Ihre Anmeldedaten für das Service-Konto abzurufen.

>[!TIP]
>
>Wählen Sie als Best Practice ein Dienstkonto aus, das [nicht abläuft](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel-Dienstkonto](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Erstellen Sie abschließend ein Experience Platform [Schema](../../../xdm/schema/composition.md), das für die [!DNL Mixpanel Event Export API] erforderlich ist. Weitere Informationen zu den für Ihr Schema erforderlichen Zuordnungen finden Sie im Handbuch unter [Erstellen einer - [!DNL Mixpanel]  in der Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Schema erstellen](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinden von [!DNL Mixpanel] mit Experience Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Mixpanel] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen einer Quellverbindung und eines Datenflusses für  [!DNL Mixpanel]  mithilfe der Flow Service-API](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinden von [!DNL Mixpanel] mit Experience Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL Mixpanel] -Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md)
* [Erstellen eines Datenflusses für eine Customer-Success-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/analytics.md)
