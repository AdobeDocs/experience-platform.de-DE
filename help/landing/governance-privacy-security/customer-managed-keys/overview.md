---
title: Vom Kunden verwaltete Schlüssel in Adobe Experience Platform
description: Erfahren Sie, wie Sie eigene Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 5a5d35dad5f1b89c0161f4b29722b76c3caf3609
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 29%

---

# Vom Kunden verwaltete Schlüssel in Adobe Experience Platform

In Adobe Experience Platform gespeicherte Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Platform aufbaut, können Sie stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

>[!NOTE]
>
>Kundenprofildaten, die im [!DNL Azure Data Lake] der Plattform und im [!DNL Azure Cosmos DB] Profilspeicher gespeichert sind, werden nach Aktivierung ausschließlich mit CMK verschlüsselt. Die Sperrung der Schlüssel in Ihren primären Datenspeichern kann zwischen **ein paar Minuten und 24 Stunden** dauern und kann bei vorübergehenden oder sekundären Datenspeichern **bis zu 7 Tage** dauern. Weitere Informationen finden Sie im Abschnitt [Implikationen beim Sperren des Schlüsselzugriffs](#revoke-access).

Dieses Dokument bietet einen allgemeinen Überblick über den Prozess zur Aktivierung der Funktion für kundenverwaltete Schlüssel (CMK) in Platform und die erforderlichen Informationen zum Ausführen dieser Schritte.

>[!NOTE]
>
>Für Customer Journey Analytics-Kunden folgen Sie den Anweisungen in der [Customer Journey Analytics-Dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=de).

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen und aufzurufen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer mit der Berechtigung [!UICONTROL Kunden-verwalteten Schlüssel verwalten] kann CMK für seine Organisation aktivieren.

Weiterführende Informationen zum Zuweisen von Rollen und Berechtigungen in Experience Platform finden Sie in der Dokumentation [Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de) .

Um CMK zu aktivieren, muss Ihr [!DNL Azure] Key Vault mit den folgenden Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe der rollenbasierten Zugriffskontrolle [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Lesen Sie die verknüpfte Dokumentation, um den Prozess besser zu verstehen.

## Prozesszusammenfassung {#process-summary}

CMK ist Teil des Healthcare Shield- und des Privacy and Security Shield-Angebots von Adobe. Nachdem Ihr Unternehmen eine Lizenz für eines dieser Angebote erworben hat, können Sie einen einmaligen Prozess zur Einrichtung der Funktion starten.

>[!WARNING]
>
>Nach dem Einrichten von CMK können Sie nicht zu systemverwalteten Schlüsseln zurückkehren. Sie sind dafür verantwortlich, Ihre Schlüssel sicher zu verwalten und den Zugriff auf Ihre Schlüsseltresor-, Schlüssel- und CMK-App innerhalb von [!DNL Azure] bereitzustellen, um zu verhindern, dass der Zugriff auf Ihre Daten verloren geht.

Der Prozess sieht folgendermaßen aus:

1. [Konfigurieren Sie einen  [!DNL Azure] Schlüsseltresor](./azure-key-vault-config.md) auf der Grundlage der Richtlinien Ihrer Organisation und generieren Sie dann [einen Verschlüsselungsschlüssel](./azure-key-vault-config.md#generate-a-key), der letztendlich an Adobe weitergegeben wird.
1. Richten Sie die CMK-App mit Ihrem [!DNL Azure] -Mandanten entweder über [API-Aufrufe](./api-set-up.md#register-app) oder die [UI](./ui-set-up.md#register-app) ein.
1. Senden Sie Ihre Verschlüsselungsschlüssel-ID an Adobe und starten Sie den Aktivierungsprozess für die Funktion entweder [in der Benutzeroberfläche](./ui-set-up.md#send-to-adobe) oder mit einem [API-Aufruf](./api-set-up.md#send-to-adobe).
1. Überprüfen Sie den Status der Konfiguration, um zu überprüfen, ob CMK entweder [in der Benutzeroberfläche](./ui-set-up.md#check-status) oder mit einem [API-Aufruf](./api-set-up.md#check-status) aktiviert wurde.

Sobald der Einrichtungsprozess abgeschlossen ist, werden alle Daten aus allen Sandboxes, die in Platform integriert sind, mit Ihrer [!DNL Azure]-Schlüsseleinrichtung verschlüsselt. Zur Verwendung von CMK nutzen Sie die [!DNL Microsoft Azure]-Funktionen, die Teil des [öffentlichen Vorschauprogramms](https://azure.microsoft.com/de-de/support/legal/preview-supplemental-terms/) sein können.

## Auswirkungen der Sperrung des Schlüsselzugriffs {#revoke-access}

Das Sperren oder Deaktivieren des Zugriffs auf die Key Vault-, Schlüssel- oder CMK-App kann zu erheblichen Unterbrechungen führen, wozu auch das Umbrechen von Änderungen an den Vorgängen Ihrer Plattform gehört. Sobald diese Schlüssel deaktiviert sind, können Daten in Platform nicht mehr zugänglich sein, und alle nachgelagerten Vorgänge, die auf diese Daten angewiesen sind, funktionieren nicht mehr. Es ist von entscheidender Bedeutung, die nachgelagerten Auswirkungen vollständig zu verstehen, bevor Sie Änderungen an Ihren Schlüsselkonfigurationen vornehmen.

Wenn Sie sich entscheiden, den Platform-Zugriff auf Ihre Daten zu sperren, können Sie dies tun, indem Sie die mit der Anwendung verknüpfte Benutzerrolle aus dem Key Vault in [!DNL Azure] entfernen.

### Zeitpläne für die Propagierung {#propagation-timelines}

Nachdem der Schlüsselzugriff von Ihrem [!DNL Azure] Key Vault widerrufen wurde, werden die Änderungen wie folgt übertragen:

| **Speichertyp** | **Beschreibung** | **Planung** |
|---|---|---|
| Primäre Datenspeicher | Zu diesen Stores gehören Azure Data Lake und Azure Cosmos DB Profile Stores. Sobald der Zugriff auf Schlüssel widerrufen wurde, ist der Zugriff auf Daten nicht mehr möglich. | Ein **paar Minuten bis 24 Stunden**. |
| Zwischengespeicherte/Übergangs-Datenspeicher | Umfasst Datenspeicher, die für Leistung und Kernanwendungsfunktionen verwendet werden. Die Auswirkungen der wichtigsten Sperrung sind verzögert. | **Bis zu 7 Tage**. |

Beispielsweise zeigt das Profil-Dashboard bis zu sieben Tage lang, bevor die Daten ablaufen, weiterhin Daten aus dem Cache an und wird aktualisiert. Ebenso dauert es ebenso lange, den Zugriff auf die Anwendung erneut zu aktivieren, bis die Datenverfügbarkeit in diesen Stores wiederhergestellt ist.

>[!NOTE]
>
>Es gibt zwei anwendungsspezifische Ausnahmen für den Ablauf von Datensätzen mit sieben Tagen, die nicht primäre (zwischengespeicherte/transiente) Daten betreffen. Weitere Informationen zu diesen Funktionen finden Sie in der entsprechenden Dokumentation .<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms)</li><li>[Edge-Projektionen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Nächste Schritte

Beginnen Sie zum Starten des Prozesses mit der [Konfiguration eines  [!DNL Azure] Key Vault](./azure-key-vault-config.md) und [Generierung eines Verschlüsselungsschlüssels](./azure-key-vault-config.md#generate-a-key), der für Adobe freigegeben werden soll.
