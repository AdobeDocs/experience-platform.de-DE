---
title: Vom Kunden verwaltete Schlüssel in Adobe Experience Platform
description: Erfahren Sie, wie Sie eigene Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 29%

---

# Vom Kunden verwaltete Schlüssel in Adobe Experience Platform

In Adobe Experience Platform gespeicherte Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Platform aufbaut, können Sie stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

>[!NOTE]
>
>Kundenprofildaten, die in der [!DNL Azure Data Lake] von Platform und im [!DNL Azure Cosmos DB] gespeichert sind, werden nach der Aktivierung ausschließlich mit CMK verschlüsselt. Der Widerruf von Schlüsseln in Ihren primären Datenspeichern kann **einige Minuten bis 24 Stunden** und bei vorübergehenden oder sekundären Datenspeichern **bis zu 7** dauern. Weitere Informationen finden Sie im Abschnitt [Auswirkungen der Sperrung des Schlüsselzugriffs](#revoke-access).

Dieses Dokument bietet einen allgemeinen Überblick über den Prozess zur Aktivierung der Funktion für kundenverwaltete Schlüssel (CMK) in Platform und die erforderlichen Informationen, um diese Schritte durchzuführen.

>[!NOTE]
>
>Customer Journey Analytics-Kunden erhalten die Anweisungen in der [Customer Journey Analytics-Dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=de).

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer, der über die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] verfügt, kann für seine Organisation CMK aktivieren.

Weitere Informationen zur Zuweisung von Rollen und Berechtigungen in Experience Platform finden Sie in der [Dokumentation zu Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de).

Um CMK zu aktivieren, muss Ihr [!DNL Azure]-Schlüsseltresor mit den folgenden Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe  [!DNL Azure]  rollenbasierten Zugriffssteuerung](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Bitte lesen Sie die verlinkte Dokumentation, um den Prozess besser zu verstehen.

## Prozesszusammenfassung {#process-summary}

CMK ist Teil des Healthcare Shield- und des Privacy and Security Shield-Angebots von Adobe. Nachdem Ihr Unternehmen eine Lizenz für eines dieser Angebote erworben hat, können Sie einen einmaligen Prozess zur Einrichtung der Funktion starten.

>[!WARNING]
>
>Nach dem Einrichten von CMK können Sie nicht zu systemverwalteten Schlüsseln zurückkehren. Sie sind dafür verantwortlich, Ihre Schlüssel sicher zu verwalten und den Zugriff auf Ihre Schlüsseltresor-, Schlüssel- und CMK-App innerhalb von [!DNL Azure] bereitzustellen, um zu verhindern, dass der Zugriff auf Ihre Daten verloren geht.

Der Prozess sieht folgendermaßen aus:

1. [Konfigurieren Sie einen  [!DNL Azure] Schlüsseltresor](./azure-key-vault-config.md) auf der Grundlage der Richtlinien Ihrer Organisation und generieren Sie dann [einen Verschlüsselungsschlüssel](./azure-key-vault-config.md#generate-a-key), der letztendlich an Adobe weitergegeben wird.
1. Richten Sie die CMK-App mit Ihrem [!DNL Azure]-Mandanten entweder über [API-Aufrufe](./api-set-up.md#register-app) oder über die [UI](./ui-set-up.md#register-app) ein.
1. Senden Sie Ihre Verschlüsselungsschlüssel-ID an Adobe und starten Sie den Aktivierungsprozess für die Funktion entweder [in der ](./ui-set-up.md#send-to-adobe) oder mit einem [API-Aufruf](./api-set-up.md#send-to-adobe).
1. Überprüfen Sie den Status der Konfiguration, um zu überprüfen, ob CMK entweder [ der Benutzeroberfläche oder ](./ui-set-up.md#check-status) einem [API-Aufruf](./api-set-up.md#check-status) aktiviert wurde.

Sobald der Einrichtungsprozess abgeschlossen ist, werden alle Daten aus allen Sandboxes, die in Platform integriert sind, mit Ihrer [!DNL Azure]-Schlüsseleinrichtung verschlüsselt. Zur Verwendung von CMK nutzen Sie die [!DNL Microsoft Azure]-Funktionen, die Teil des [öffentlichen Vorschauprogramms](https://azure.microsoft.com/de-de/support/legal/preview-supplemental-terms/) sein können.

## Auswirkungen der Sperrung des Schlüsselzugriffs {#revoke-access}

Das Widerrufen oder Deaktivieren des Zugriffs auf die Schlüsseltresor-, Schlüssel- oder CMK-App kann zu erheblichen Unterbrechungen führen, darunter auch zu grundlegenden Änderungen an den Vorgängen Ihrer Plattform. Sobald diese Schlüssel deaktiviert sind, können Daten in Platform nicht mehr zugänglich sein, und nachgelagerte Vorgänge, die auf diese Daten angewiesen sind, funktionieren nicht mehr. Es ist wichtig, die nachgelagerten Auswirkungen vollständig zu verstehen, bevor Sie Änderungen an Ihren wichtigsten Konfigurationen vornehmen.

Wenn Sie sich entscheiden, den Platform-Zugriff auf Ihre Daten zu sperren, können Sie dies tun, indem Sie die mit der Anwendung verknüpfte Benutzerrolle aus dem Schlüsseltresor in [!DNL Azure] entfernen.

### Zeitleisten für die Übertragung {#propagation-timelines}

Nachdem der Schlüsselzugriff aus Ihrem [!DNL Azure] Schlüsseltresor widerrufen wurde, werden die Änderungen wie folgt weitergegeben:

| **Store-Typ** | **Beschreibung** | **Planung** |
|---|---|---|
| Primäre Datenspeicher | Zu diesen Stores gehören Azure Data Lake- und Azure Cosmos DB-Profilspeicher. Sobald der Schlüsselzugriff widerrufen wurde, ist der Zugriff auf die Daten nicht mehr möglich. | Ein **Minuten bis 24 Stunden**. |
| Zwischengespeicherte/vorübergehende Datenspeicher | Umfasst für Leistung verwendete Datenspeicher und zentrale Anwendungsfunktionen. Die Auswirkungen des Widerrufs eines Schlüssels sind verzögert. | **Bis zu 7**. |

Beispielsweise zeigt das Profil-Dashboard bis zu sieben Tage lang Daten aus seinem Cache an, bevor die Daten ablaufen und aktualisiert werden. Ebenso dauert es genauso lange, den Zugriff auf die Anwendung wieder zu aktivieren, bis die Datenverfügbarkeit in diesen Stores wiederhergestellt ist.

>[!NOTE]
>
>Es gibt zwei Anwendungsfall-spezifische Ausnahmen von der siebentägigen Datensatzgültigkeit für nicht primäre (zwischengespeicherte/vorübergehende) Daten. Weitere Informationen zu diesen Funktionen finden Sie in der entsprechenden Dokumentation.<ul><li>[Adobe Journey Optimizer URL-Verkürzung](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms)</li><li>[Edge-Prognosen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Nächste Schritte

Beginnen Sie zunächst mit der [Konfiguration eines  [!DNL Azure] -](./azure-key-vault-config.md) und [Generieren eines ](./azure-key-vault-config.md#generate-a-key)), um ihn für Adobe freizugeben.
