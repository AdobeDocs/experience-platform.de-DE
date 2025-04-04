---
title: Braze-Ströme Source - Übersicht
description: Erfahren Sie, wie Sie Daten von Braze Current an Experience Platform streamen.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 12%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Die Unterstützung für Streaming-Anbieter umfasst [!DNL Braze Currents].

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen von der Braze-Plattform, der der robusteste und zugleich granularste Export aus der [!DNL Braze]-Plattform ist.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie Folgendes:

* Eine Anmeldung bei [Adobe Experience Platform ](https://platform.adobe.com) die Berechtigung zum Erstellen einer neuen Streaming-Quellverbindung.
* Eine Anmeldung bei Ihrem [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in), eine nicht verwendete [Aktuelle Connector-](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)) und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie unter [Voraussetzungen für die Einrichtung [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Sammeln erforderlicher Anmeldedaten

Um Ihre [!DNL Braze Currents] Daten erfolgreich an Experience Platform zu senden, müssen Sie die folgenden Experience Platform-Anmeldeinformationen in das Dashboard der [!DNL Braze]-Benutzeroberfläche eingeben.

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Client-ID. |
| Client-Geheimnis | Das mit Ihrer Experience Platform-Quelle verknüpfte Client-Geheimnis. |
| Mandanten-ID | Die Mandanten-ID, die mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Datenfluss-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der mit Ihrer Experience Platform-Quelle verknüpfte Streaming-Endpunkt. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

Informationen zum Abrufen dieser Werte finden Sie im Handbuch unter [Erste Schritte mit Experience Platform-APIs](../../../landing/api-authentication.md). Informationen zur Verwendung des [!DNL Braze]-Dashboards finden Sie im [!DNL Braze] Handbuch [Navigieren zu Strömen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL Braze Currents]-Konto an Experience Platform zu streamen. Sie können jetzt mit dem Handbuch unter [Verbinden [!DNL Braze Currents]  mit Experience Platform über die Benutzeroberfläche ](../../tutorials/ui/create/marketing-automation/braze.md).
