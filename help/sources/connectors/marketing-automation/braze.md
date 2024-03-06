---
title: Überblick über die aktuelle Quelle
description: Erfahren Sie, wie Sie Daten von Braze Currents an Experience Platform streamen.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 18%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>Die [!DNL Braze Currents]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Braze Currents].

[!DNL Braze] ermöglicht kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit. [!DNL Braze Currents] ist ein Echtzeit-Datenstrom von Interaktionsereignissen von der Braze-Plattform, die den robusten, aber granularsten Export aus der [!DNL Braze] Plattform.

## Voraussetzungen

Um die Schritte in diesem Handbuch abzuschließen, benötigen Sie:

* Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und Berechtigung zum Erstellen einer neuen Streaming-Quell-Verbindung.
* Melden Sie sich bei Ihrer [[!DNL Braze] Dashboard](https://dashboard.braze.com/sign_in)nicht verwendete [Aktuelle Connector-Lizenz](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)und Berechtigungen zum Erstellen eines Connectors. Weitere Informationen finden Sie im Abschnitt [Anforderungen für die Einrichtung [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Sammeln erforderlicher Anmeldeinformationen

Zur erfolgreichen Übermittlung [!DNL Braze Currents] Daten an Experience Platform senden, müssen Sie die folgenden Experience Platform-Anmeldedaten in die [!DNL Braze] UI-Dashboard.

| Feld | Beschreibung |
| --- | --- |
| Client-ID | Die Client-ID, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Client-Geheimnis | Das Client-Geheimnis, das mit Ihrer Experience Platform-Quelle verknüpft ist. |
| Mandanten-ID | Die Mandantenkennung, die Ihrer Experience Platform-Quelle zugeordnet ist. |
| Sandbox-Name | Die mit Ihrer Experience Platform-Quelle verknüpfte Sandbox. |
| Dataflow-ID | Die mit Ihrer Experience Platform-Quelle verknüpfte Datenfluss-ID. |
| Streaming-Endpunkt | Der Streaming-Endpunkt, der Ihrer Experience Platform-Quelle zugeordnet ist. **Hinweis**: [!DNL Braze] konvertiert dies automatisch in den Batch-Streaming-Endpunkt. |

Informationen zum Abrufen dieser Werte finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-authentication.md). Informationen zur Verwendung der [!DNL Braze] Dashboard, lesen Sie die [!DNL Braze] Anleitung zum [Navigieren zu Aktuellen](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung zum Streamen von Daten von Ihrer [!DNL Braze Currents] -Konto auf Experience Platform. Sie können jetzt mit dem Handbuch zu [Verbindung [!DNL Braze Currents] zum Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/braze.md).