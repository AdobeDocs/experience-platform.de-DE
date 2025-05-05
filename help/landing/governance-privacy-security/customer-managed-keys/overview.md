---
title: Vom Kunden verwaltete Schlüssel in Adobe Experience Platform
description: Erfahren Sie, wie Sie eigene Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 6%

---

# Vom Kunden verwaltete Schlüssel in Adobe Experience Platform

In Adobe Experience Platform gespeicherte Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie ein Programm verwenden, das auf Experience Platform aufbaut, können Sie stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

>[!AVAILABILITY]
>
>Adobe Experience Platform unterstützt kundenseitig verwaltete Schlüssel (CMK) für Microsoft Azure und Amazon Web Services (AWS). Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Wenn Ihre Implementierung auf AWS ausgeführt wird, haben Sie die Möglichkeit, den Key Management Service (KMS) für die Experience Platform-Datenverschlüsselung zu verwenden. Weitere Informationen zur unterstützten Infrastruktur finden Sie in der [Übersicht über die Experience Platform-Multi-Cloud](https://experienceleague.adobe.com/de/docs/experience-platform/landing/multi-cloud).
>
>Informationen zur Erstellung und Verwaltung von Verschlüsselungsschlüsseln in AWS KMS finden Sie im [Handbuch zur AWS KMS-Datenverschlüsselung](./aws/configure-kms.md). Informationen zu Azure-Implementierungen finden Sie im [Konfigurationshandbuch für Azure Key Vault](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Bei [!DNL Azure] gehosteten Experience Platform-Instanzen werden Kundenprofildaten, die in der [!DNL Azure Data Lake] von Experience Platform und im [!DNL Azure Cosmos DB] gespeichert sind, nach der Aktivierung ausschließlich mit CMK verschlüsselt. Der Widerruf von Schlüsseln in primären Datenspeichern kann zwischen **einigen Minuten bis 24 Stunden** und **bis zu 7 Tage** bei vorübergehenden oder sekundären Datenspeichern dauern. Weitere Informationen finden Sie im Abschnitt [Auswirkungen der Sperrung des Schlüsselzugriffs](#revoke-access).

Dieses Dokument bietet einen allgemeinen Überblick über den Prozess zur Aktivierung der CMK-Funktion (Customer Managed Keys) in Experience Platform in [!DNL Azure] und AWS sowie über die erforderlichen Informationen zum Durchführen dieser Schritte.

>[!NOTE]
>
>Customer Journey Analytics-Kunden sollten die Anweisungen in der [Dokumentation zu Customer Journey Analytics befolgen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=de).

## Voraussetzungen

Um CMK zu aktivieren, muss die Hosting-Umgebung Ihrer Plattform ([!DNL Azure] oder AWS) bestimmte Konfigurationsanforderungen erfüllen:

### Allgemeine Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzeigen und darauf zugreifen zu können, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben.  Jeder Benutzer mit der Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] kann für seine Organisation CMK aktivieren.

Weitere Informationen zur Zuweisung von Rollen und Berechtigungen in Experience Platform finden Sie in der [Dokumentation zu Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de).

### Azure-spezifische Voraussetzungen

Konfigurieren Sie für von Azure gehostete Implementierungen Ihren [!DNL Azure]-Schlüsseltresor mit den folgenden Einstellungen:

- [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Konfigurieren des Zugriffs mithilfe  [!DNL Azure]  rollenbasierten Zugriffssteuerung](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### AWS-spezifische Voraussetzungen

Für von AWS gehostete Implementierungen konfigurieren Sie Ihre AWS-Umgebung wie folgt:

- Stellen Sie sicher, dass Sie über Berechtigungen zum Verwalten von Verschlüsselungsschlüsseln mit AWS Identity and Access Management (IAM) verfügen. Weitere Informationen finden Sie unter [IAM-Richtlinien für AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Einrichten von AWS KMS mit Unterstützung für CMK. Weitere Informationen finden Sie im [Handbuch zur AWS KMS-Datenverschlüsselung](./aws/configure-kms.md).

## Prozesszusammenfassung {#process-summary}

Vom Kunden verwaltete Schlüssel (CMK) sind über die Adobe-Angebote Healthcare Shield und Privacy and Security Shield verfügbar. Auf Azure wird CMK sowohl für Healthcare Shield als auch für Privacy and Security Shield unterstützt. Auf AWS wird CMK nur für Privacy und Security Shield unterstützt und ist nicht für Healthcare Shield verfügbar. Sobald Ihr Unternehmen eine Lizenz für eines dieser Angebote erworben hat, können Sie den einmaligen Einrichtungsprozess zur Aktivierung von CMK starten.

>[!WARNING]
>
>Nach dem Einrichten von CMK können Sie nicht zu systemverwalteten Schlüsseln zurückkehren. Sie sind dafür verantwortlich, Ihre Schlüssel sicher zu verwalten, um zu verhindern, dass der Zugriff auf Ihre Daten verloren geht.

Der Prozess sieht folgendermaßen aus:

### Für Azure {#azure-process-summary}

1. [Konfigurieren Sie  [!DNL Azure]  Schlüsseltresor](./azure/azure-key-vault-config.md) basierend auf den Richtlinien Ihrer Organisation und [generieren Sie dann einen ](./azure/azure-key-vault-config.md#generate-a-key), der für Adobe freigegeben wird.
1. Richten Sie die CMK-App mit Ihrem [!DNL Azure]-Mandanten entweder über [API-Aufrufe](./azure/api-set-up.md#register-app) oder über die [UI](./azure/ui-set-up.md#register-app) ein.
1. Senden Sie Ihre Verschlüsselungsschlüssel-ID an Adobe und starten Sie den Aktivierungsprozess für die Funktion, entweder [ der Benutzeroberfläche ](./azure/ui-set-up.md#send-to-adobe) mit einem [API-Aufruf](./azure/api-set-up.md#send-to-adobe).
1. Überprüfen Sie den Status der Konfiguration, um zu überprüfen, ob CMK aktiviert wurde, entweder [in der ](./azure/ui-set-up.md#check-status) oder mit einem [API-Aufruf](./azure/api-set-up.md#check-status).

Sobald der Einrichtungsprozess für die von Azure gehosteten Experience Platform-Instanzen abgeschlossen ist, werden alle Daten in allen Sandboxes, die in Experience Platform integriert sind, mit Ihrer [!DNL Azure] verschlüsselt. Zur Verwendung von CMK nutzen Sie die [!DNL Microsoft Azure]-Funktionen, die Teil des [öffentlichen Vorschauprogramms](https://azure.microsoft.com/de-de/support/legal/preview-supplemental-terms/) sein können.

### Für AWS {#aws-process-summary}

1. [Richten Sie AWS KMS ein](./aws/configure-kms.md) indem Sie einen Verschlüsselungsschlüssel konfigurieren, der für Adobe freigegeben werden soll.
2. Befolgen Sie die für AWS spezifischen Anweisungen im [UI-Einrichtungshandbuch](./aws/ui-set-up.md).
3. Überprüfen Sie die Einrichtung, um sicherzustellen, dass Experience Platform-Daten mit dem von AWS gehosteten Schlüssel verschlüsselt werden.

<!--  Pending: or [API setup guide]() -->

Sobald der Einrichtungsprozess für von AWS gehostete Experience Platform-Instanzen abgeschlossen ist, werden alle Daten aus allen Sandboxes, die in Experience Platform integriert sind, mit Ihrer AWS Key Management Service (KMS)-Konfiguration verschlüsselt. Um CMK in AWS zu verwenden, verwenden Sie den AWS-Schlüsselverwaltungsdienst, um Ihre Verschlüsselungsschlüssel entsprechend den Sicherheitsanforderungen Ihres Unternehmens zu erstellen und zu verwalten.

## Auswirkungen der Sperrung des Schlüsselzugriffs {#revoke-access}

Das Widerrufen oder Deaktivieren des Zugriffs auf den Schlüsseltresor, den Schlüssel oder die CMK-App in Azure oder den Verschlüsselungsschlüssel in AWS kann zu erheblichen Unterbrechungen führen, darunter auch zu grundlegenden Änderungen an den Vorgängen Ihrer Experience Platform. Sobald -Schlüssel deaktiviert sind, können Daten in Experience Platform nicht mehr aufgerufen werden und nachgelagerte Vorgänge, die auf diese Daten angewiesen sind, funktionieren nicht mehr. Es ist wichtig, die nachgelagerten Auswirkungen vollständig zu verstehen, bevor Sie Änderungen an Ihren wichtigsten Konfigurationen vornehmen.

Um Experience Platform den Zugriff auf Ihre Daten in [!DNL Azure] zu entziehen, entfernen Sie die mit der Anwendung verknüpfte Benutzerrolle aus dem Schlüsseltresor. Bei AWS können Sie den Schlüssel deaktivieren oder die Richtlinienanweisung aktualisieren. Detaillierte Anweisungen zum AWS-Prozess finden Sie im Abschnitt [Sperren von Schlüsseln](./aws/ui-set-up.md#key-revocation).


### Zeitleisten für die Übertragung {#propagation-timelines}

Nachdem der Schlüsselzugriff aus Ihrem [!DNL Azure] Schlüsseltresor widerrufen wurde, werden die Änderungen wie folgt weitergegeben:

| **Store-Typ** | **Beschreibung** | **Planung** |
|---|---|---|
| Primäre Datenspeicher | Umfasst Data Lakes (Azure Data Lake, AWS S3) und Azure Cosmos DB-Profilspeicher. Sobald der Schlüsselzugriff widerrufen wurde, ist der Zugriff auf die Daten nicht mehr möglich. | Ein **Minuten bis 24 Stunden**. |
| Zwischengespeicherte/vorübergehende Datenspeicher | Umfasst sekundäre Datenspeicher, die für Leistung und Kernanwendungsfunktionen verwendet werden. Die Auswirkungen des Widerrufs eines Schlüssels sind verzögert. | **Bis zu 7**. |

Beispielsweise zeigt das Profil-Dashboard bis zu sieben Tage lang Daten aus seinem Cache an, bevor die Daten ablaufen und aktualisiert werden. Ebenso dauert es genauso lange, den Zugriff auf die Anwendung wieder zu aktivieren, bis die Datenverfügbarkeit in diesen Stores wiederhergestellt ist.

>[!NOTE]
>
>Die Wiederherstellung des Zugriffs auf die Anwendung kann dieselbe Zeit in Anspruch nehmen wie die Sperrung, um die Datenverfügbarkeit in diesen Stores wiederherzustellen.

>[!TIP]
>
>Es gibt zwei Anwendungsfall-spezifische Ausnahmen von der siebentägigen Datensatzgültigkeit für nicht primäre (zwischengespeicherte/vorübergehende) Daten. Weitere Informationen zu diesen Funktionen finden Sie in der entsprechenden Dokumentation.<ul><li>[Adobe Journey Optimizer URL-Verkürzung](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=de#message-preset-sms)</li><li>[Edge-Prognosen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=de#edge-projections)</li></ul>

## Nächste Schritte

So starten Sie den Prozess:

- Für Azure: Beginnen Sie mit dem [Konfigurieren eines  [!DNL Azure] -Schlüsseltresors](./azure/azure-key-vault-config.md) und [Generieren eines ](./azure/azure-key-vault-config.md#generate-a-key), der für Adobe freigegeben werden soll.
- Für AWS: [Richten Sie AWS KMS ein](./aws/configure-kms.md) und stellen Sie sicher, dass die richtigen IAM- und KMS-Konfigurationen vorliegen, bevor Sie mit den Handbüchern zur Benutzeroberfläche oder zur API-Einrichtung fortfahren.
