---
title: Übersicht über die Braze Currency Source
description: Erfahren Sie, wie Sie Daten von Braze Currents an Experience Platform streamen.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 19%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Die Unterstützung für Streaming-Anbieter umfasst [!DNL Braze Currents].

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen aus der Braze-Plattform, der den robusten, aber granularsten Export aus der [!DNL Braze]-Plattform darstellt.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie:

* Anmeldung bei [Adobe Experience Platform](https://platform.adobe.com) und Berechtigung zum Erstellen einer neuen Streaming-Quellverbindung.
* Anmeldung bei Ihrem [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in), eine nicht verwendete [Lizenz für den aktuellen Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie in den [Anforderungen zum Einrichten von  [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements) .

### Sammeln erforderlicher Anmeldeinformationen

Um Ihre [!DNL Braze Currents] -Daten erfolgreich an Experience Platform zu senden, müssen Sie die folgenden Experience Platform-Anmeldedaten im Dashboard der [!DNL Braze]-Benutzeroberfläche eingeben.

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die Client-ID, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Client-Geheimnis | Das Client-Geheimnis, das mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Mandanten-ID | Die Mandantenkennung, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Datenfluss-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der Streaming-Endpunkt, der Ihrer Experience Platform-Quelle zugeordnet ist. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

Informationen zum Abrufen dieser Werte finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-authentication.md). Informationen zur Verwendung des Dashboards [!DNL Braze] finden Sie in der [!DNL Braze]-Anleitung zum Navigieren zu aktuellen Elementen [3}.](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents)

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL Braze Currents]-Konto an Experience Platform zu streamen. Sie können jetzt mit dem Handbuch zum Verbinden von [1}mit dem Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/braze.md) fortfahren. [!DNL Braze Currents] 
