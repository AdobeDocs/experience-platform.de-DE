---
keywords: Experience Platform;Startseite;beliebte Themen;
title: (Beta) Mixpanel Source Connector - Übersicht
description: Erfahren Sie, wie Sie Mixpanel über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 30%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>Die [!DNL Mixpanel]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einer Analytics-Anwendung von Drittanbietern. Unterstützung für Analytics-Anbieter: [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Produktanalysetool, mit dem Sie Daten darüber erfassen können, wie Benutzer mit einem digitalen Produkt interagieren. Mithilfe von Mixpanel können Sie diese Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit nur wenigen Klicks abfragen und visualisieren können.

Quellen nutzen die [Mixpanel-Ereignis-Export-API > Herunterladen](https://developer.mixpanel.com/reference/raw-event-export) zum Herunterladen Ihrer Ereignisdaten beim Empfang und bei der Speicherung in [!DNL Mixpanel]zusammen mit allen Ereigniseigenschaften (einschließlich `distinct_id`) und dem genauen Zeitstempel, mit dem das Ereignis an Experience Platform gesendet wurde. Mixpanel verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit der Mixpanel Event Export API.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Authentifizieren Sie Ihre [!DNL Mixpanel] account

In diesem Abschnitt werden die erforderlichen Schritte beschrieben, die zum Authentifizieren Ihres Kontos und zum Übermitteln Ihrer [!DNL Mixpanel] Daten an Platform.

Um eine [!DNL Mixpanel] Quellverbindung und Datenfluss müssen Sie zunächst über eine gültige [!DNL Mixpanel] -Konto. Wenn Sie keine gültige [!DNL Mixpanel] -Konto, siehe [Mixpanel-Register](https://mixpanel.com/register/) Seite, um Ihr Konto zu erstellen.

Nachdem Sie erfolgreich eine [!DNL Mixpanel] -Konto, navigieren Sie zum [!DNL Project Details] im [!DNL Project Seettings] der [!DNL Mixpanel] Benutzeroberfläche zum Abrufen Ihrer Projekt-ID und Konfigurieren der Zeitzone.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigieren Sie dann zum [!DNL Service Accounts] im [!DNL Project Settings] in der [!DNL Mixpanel] Benutzeroberfläche zum Abrufen der Anmeldedaten für Ihr Dienstkonto.

>[!TIP]
>
>Es hat sich bewährt, ein Dienstkonto auszuwählen, das [läuft nicht ab](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel-Dienstkonto](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Erstellen Sie abschließend eine Plattform . [schema](../../../xdm/schema/composition.md) für [!DNL Mixpanel Event Export API]. Weitere Informationen zu den für Ihr Schema erforderlichen Zuordnungen finden Sie im Handbuch unter [Erstellen einer [!DNL Mixpanel] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Schema erstellen](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinden von [!DNL Mixpanel] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Mixpanel] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss für [!DNL Mixpanel] Verwenden der Flow Service-API](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinden von [!DNL Mixpanel] mit Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL Mixpanel] -Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/analytics/mixpanel.md)
* [Erstellen eines Datenflusses für eine Kundenerfolgsquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/analytics.md)
