---
title: Adobe Experience Platform - Versionshinweise Januar 2023
description: Die Versionshinweise für Adobe Experience Platform vom Januar 2023.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 41%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 25. Januar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Quellen](#sources)

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und ermöglicht es Ihnen, diese Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Zulassen des Benutzerzugriffs auf Unterordner der Cloud-Speicherquellen | Sie können jetzt den Zugriff auf einen bestimmten Unterordner Ihrer Cloud-Speicherquelle definieren, wenn Sie ein neues Konto erstellen. Nach der Erstellung können Benutzer nur auf Daten aus dem zulässigen Unterordner zugreifen. Diese Funktion steht den folgenden Cloud-Speicher-Quellen zur Verfügung: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)und [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Verfügbarkeit von Beta [!DNL SugarCRM] | [!DNL SugarCRM] -Quellen sind jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] Quellen zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM] -Konto auf Experience Platform. Weitere Informationen finden Sie im Abschnitt [[!DNL SugarCRM] Übersicht](../../sources/connectors/crm/sugarcrm.md). |