---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 63%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 27. Oktober 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Quellen](#sources)

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Amazon S3]-Quellverbesserungen | Sie können jetzt die `s3SessionToken` Parameter zum Verbinden Ihrer [!DNL Amazon S3] -Konto für Platform mit temporären Sicherheitsberechtigungen erstellen. Mit diesem Token können Sie kurzfristigen, temporären Zugriff auf Ihre [!DNL Amazon S3] Ressourcen für Benutzer in nicht vertrauenswürdigen Umgebungen. Siehe [[!DNL Amazon S3] Dokumentation](../../sources/connectors/cloud-storage/s3.md#prerequisites) für weitere Informationen. |
| [!DNL Generic REST API] (Betaversion) | Sie können jetzt eine [!DNL Generic REST API] Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) oder [Benutzeroberfläche](../../sources/tutorials/ui/create/protocols/generic-rest.md) , um Daten von einer generischen REST-Anwendung an Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Generic REST API] Übersicht über](../../sources/connectors/protocols/generic-rest.md). |
| [!DNL Zoho CRM] (Betaversion) | Sie können jetzt eine [!DNL Zoho CRM] Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) oder [Benutzeroberfläche](../../sources/tutorials/ui/create/crm/zoho.md) Daten von [!DNL Zoho CRM] -Konto auf Platform. Weitere Informationen finden Sie in der [[!DNL Zoho CRM] Übersicht über](../../sources/connectors/crm/zoho.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
