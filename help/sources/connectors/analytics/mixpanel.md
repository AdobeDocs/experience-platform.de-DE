---
title: Übersicht über den Mixpanel Source Connector
description: Erfahren Sie, wie Sie Mixpanel über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 30%

---

# [!DNL Mixpanel]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einer Analytics-Anwendung eines Drittanbieters. Unterstützung für Analytics-Anbieter ist [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Tool zur Produktanalyse, mit dem Sie Daten darüber erfassen können, wie Benutzer mit einem digitalen Produkt interagieren. Mithilfe von Mixpanel können Sie diese Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit nur wenigen Klicks abfragen und visualisieren können.

Quellen nutzen die [Mixpanel Event Export API > Download](https://developer.mixpanel.com/reference/raw-event-export) , um Ihre Ereignisdaten herunterzuladen, sobald sie in [!DNL Mixpanel] empfangen und gespeichert werden, sowie alle Ereigniseigenschaften (einschließlich `distinct_id`) und den genauen Zeitstempel, mit dem das Ereignis an Experience Platform gesendet wurde. Mixpanel verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit der Mixpanel Event Export API.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Ihr [!DNL Mixpanel]-Konto authentifizieren

In diesem Abschnitt werden die erforderlichen Schritte zum Ausführen der Authentifizierung für Ihr Konto und zum Übertragen Ihrer [!DNL Mixpanel] -Daten an Platform beschrieben.

Um eine [!DNL Mixpanel]-Quellverbindung und einen Datenfluss zu erstellen, müssen Sie zunächst über ein gültiges [!DNL Mixpanel]-Konto verfügen. Wenn Sie kein gültiges [!DNL Mixpanel]-Konto haben, lesen Sie die Seite [Mixpanel register](https://mixpanel.com/register/) , um Ihr Konto zu erstellen.

Nachdem Sie erfolgreich ein [!DNL Mixpanel] -Konto erstellt haben, navigieren Sie zur Registerkarte [!DNL Project Details] auf der Seite [!DNL Project Seettings] der Benutzeroberfläche von [!DNL Mixpanel] , um Ihre Projekt-ID abzurufen und Ihre Zeitzone zu konfigurieren.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigieren Sie anschließend zur Registerkarte [!DNL Service Accounts] auf der Seite [!DNL Project Settings] in der Benutzeroberfläche von [!DNL Mixpanel] , um Ihre Anmeldedaten für Dienstkonten abzurufen.

>[!TIP]
>
>Es hat sich bewährt, ein Dienstkonto auszuwählen, das [nicht abläuft](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel-Dienstkonto](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Erstellen Sie abschließend ein Platform [schema](../../../xdm/schema/composition.md) , das für die [!DNL Mixpanel Event Export API] erforderlich ist. Weitere Informationen zu den für Ihr Schema erforderlichen Zuordnungen finden Sie im Handbuch zum Erstellen einer  [!DNL Mixpanel] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).[

![Schema erstellen](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinden von [!DNL Mixpanel] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Mixpanel] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen einer Quellverbindung und eines Datenflusses für  [!DNL Mixpanel]  mithilfe der Flow Service-API](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinden von [!DNL Mixpanel] mit Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL Mixpanel] -Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md)
* [Erstellen eines Datenflusses für eine Kundenerfolgsquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/analytics.md)
