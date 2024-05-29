---
title: Vom Kunden verwaltete Schlüssel in Adobe Experience Platform
description: Erfahren Sie, wie Sie eigene Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 36%

---

# Vom Kunden verwaltete Schlüssel in Adobe Experience Platform

In Adobe Experience Platform gespeicherte Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Platform aufbaut, können Sie stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

>[!NOTE]
>
>Daten in Adobe Experience Platform Data Lake und Profilspeicher werden mit CMK verschlüsselt. Diese werden als Ihre primären Datenspeicher betrachtet.

Dieses Dokument bietet einen allgemeinen Überblick über den Prozess zur Aktivierung der Funktion für kundenverwaltete Schlüssel (CMK) in Platform und die erforderlichen Informationen zum Ausführen dieser Schritte.

>[!NOTE]
>
>Für Customer Journey Analytics-Kunden folgen Sie bitte den Anweisungen im Abschnitt [Customer Journey Analytics-Dokumentation](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=de).

## Voraussetzungen

So zeigen Sie die [!UICONTROL Verschlüsselung] in Adobe Experience Platform müssen Sie eine Rolle erstellt und der [!UICONTROL Verwalten des kundenverwalteten Schlüssels] Berechtigung für diese Rolle. Jeder Benutzer, der über [!UICONTROL Verwalten des kundenverwalteten Schlüssels] -Berechtigung kann CMK für ihre Organisation aktivieren.

Weiterführende Informationen zum Zuweisen von Rollen und Berechtigungen in Experience Platform finden Sie im Abschnitt [Berechtigungsdokumentation konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de).

Um CMK zu aktivieren, muss die [!DNL Azure] Key Vault muss mit den folgenden Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Löschen aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Zugriff konfigurieren mit [!DNL Azure] rollenbasierte Zugriffssteuerung](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Lesen Sie die verknüpfte Dokumentation, um den Prozess besser zu verstehen.

## Prozesszusammenfassung {#process-summary}

CMK ist Teil des Healthcare Shield- und des Privacy and Security Shield-Angebots von Adobe. Nachdem Ihr Unternehmen eine Lizenz für eines dieser Angebote erworben hat, können Sie einen einmaligen Prozess zur Einrichtung der Funktion starten.

>[!WARNING]
>
>Nach dem Einrichten von CMK können Sie nicht zu systemverwalteten Schlüsseln zurückkehren. Sie sind dafür verantwortlich, Ihre Schlüssel sicher zu verwalten und den Zugriff auf Ihre Schlüsseltresor-, Schlüssel- und CMK-App innerhalb von [!DNL Azure] bereitzustellen, um zu verhindern, dass der Zugriff auf Ihre Daten verloren geht.

Der Prozess sieht folgendermaßen aus:

1. [Konfigurieren Sie einen  [!DNL Azure] Schlüsseltresor](./azure-key-vault-config.md) auf der Grundlage der Richtlinien Ihrer Organisation und generieren Sie dann [einen Verschlüsselungsschlüssel](./azure-key-vault-config.md#generate-a-key), der letztendlich an Adobe weitergegeben wird.
1. Richten Sie die CMK-App mit Ihrer [!DNL Azure] Mandanten über [API-Aufrufe](./api-set-up.md#register-app) oder [Benutzeroberfläche](./ui-set-up.md#register-app).
1. Senden Sie Ihre Verschlüsselungsschlüssel-ID an Adobe und starten Sie den Aktivierungsprozess für die Funktion entweder [in der Benutzeroberfläche](./ui-set-up.md#send-to-adobe) oder mit [API-Aufruf](./api-set-up.md#send-to-adobe).
1. Überprüfen Sie den Status der Konfiguration, um zu überprüfen, ob CMK aktiviert wurde. [in der Benutzeroberfläche](./ui-set-up.md#check-status) oder mit [API-Aufruf](./api-set-up.md#check-status).

Sobald der Einrichtungsprozess abgeschlossen ist, werden alle Daten aus allen Sandboxes, die in Platform integriert sind, mit Ihrer [!DNL Azure]-Schlüsseleinrichtung verschlüsselt. Zur Verwendung von CMK nutzen Sie die [!DNL Microsoft Azure]-Funktionen, die Teil des [öffentlichen Vorschauprogramms](https://azure.microsoft.com/de-de/support/legal/preview-supplemental-terms/) sein können.

## Zugriff sperren {#revoke-access}

Wenn Sie den Platform-Zugriff auf Ihre Daten sperren möchten, können Sie die mit dem Programm verknüpfte Benutzerrolle aus dem Schlüsseltresor in [!DNL Azure] entfernen.

>[!WARNING]
>
>Das Deaktivieren der Schlüssel-Vault-, Schlüssel- oder CMK-App kann zu einer brechenden Änderung führen. Sobald die Schlüssel-Vault-, Schlüssel- oder CMK-App deaktiviert ist und die Daten in Platform nicht mehr verfügbar sind, sind alle nachgelagerten Vorgänge im Zusammenhang mit diesen Daten nicht mehr möglich. Stellen Sie sicher, dass Sie die nachgelagerten Auswirkungen der Sperrung des Platform-Zugriffs auf Ihren Schlüssel verstehen, bevor Sie Änderungen an Ihrer Konfiguration vornehmen.

Nachdem Sie den Schlüsselzugriff entfernt oder den Schlüssel deaktiviert/gelöscht haben [!DNL Azure] -Schlüsselwertgewölbe kann es zwischen einigen Minuten und 24 Stunden dauern, bis diese Konfiguration in die primären Datenspeicher übertragen wird. Platform-Workflows umfassen auch zwischengespeicherte und vorübergehende Datenspeicher, die für die Leistung und die Kernfunktionen der Anwendung erforderlich sind. Die Übertragung der CMK-Sperrung durch diese zwischengespeicherten und vorübergehenden Speicher kann bis zu sieben Tage dauern, wie von ihren Datenverarbeitungs-Workflows bestimmt. Dies bedeutet beispielsweise, dass das Profil-Dashboard Daten aus seinem Cache-Datenspeicher aufbewahrt und anzeigt und es sieben Tage dauert, bis die im Cache-Datenspeicher gespeicherten Daten im Rahmen des Aktualisierungszyklus ablaufen. Die gleiche Zeitverzögerung gilt für Daten, die erneut verfügbar werden, wenn der Zugriff auf das Programm erneut aktiviert wird.

>[!NOTE]
>
>Es gibt zwei anwendungsspezifische Ausnahmen für den Ablauf von Datensätzen mit sieben Tagen, die nicht primäre (zwischengespeicherte/transiente) Daten betreffen. Weitere Informationen zu diesen Funktionen finden Sie in der entsprechenden Dokumentation .<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms)</li><li>[Edge-Projektionen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Nächste Schritte

Beginnen Sie zum Starten des Prozesses mit [Konfiguration einer [!DNL Azure] Key Vault](./azure-key-vault-config.md) und [einen Verschlüsselungsschlüssel generieren](./azure-key-vault-config.md#generate-a-key) für Adobe freigeben.
