---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identitätsdaten für Datenschutzanfragen
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 43%

---


# Identitätsdaten für Datenschutzanfragen

In order for Adobe Experience Platform [!DNL Privacy Service] to process customer requests for their private data (including access, delete, or opt-out-of-sale requests), it must be provided with unique identifiers that link a specific customer to their stored private data in your Adobe Experience Cloud enabled applications. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle unter der Kundenidentität in gespeicherten Daten zu erfassen und gemäß der Kundenanfrage zu verarbeiten.[!DNL Experience Cloud]

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanal interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander in Einklang zu bringen. This in turn can make it difficult to determine which data belongs to a particular person in your [!DNL Experience Cloud] applications.

For example, when handling customer data requests in [!DNL Privacy Service], an identity may represent a cookie value set under an Adobe-controlled domain, a cookie value under a third-party domain and shared with Adobe, or a custom identifier that you explicitly define within your IMS Organization.

It is therefore required that each identity sent to [!DNL Privacy Service] is accompanied with a **namespace** that provides context by relating the identity value to its system of origin. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/namespaces.md). For a list of standard namespaces and namespace qualifiers that are commonly used in [!DNL Privacy Service], see the [appendix section](api/appendix.md) in the developer guide.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] serves as a common identification framework for [!DNL Experience Cloud], and assigns a unique, persistent ID to each site visitor. The [!DNL Experience Cloud] ID (ECID) tracks a customer&#39;s activity through the use of a first-party cookie, can uniquely identify a device across multiple applications, and allows you to identify the same site visitor and their data in different [!DNL Experience Cloud] applications. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://docs.adobe.com/content/help/de-DE/id-service/using/intro/overview.html).

Opt-in Service, an extension of [!DNL Experience Cloud Identity Service], allows you set up protocols on your application to let visitors determine whether you can set a cookie on the visitor&#39;s device or browser. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://docs.adobe.com/content/help/de-DE/id-service/using/implementation/opt-in-service/optin-overview.html).

Once your site visitors have been assigned ECIDs, you can utilize the Adobe [!DNL Privacy JavaScript Library] to retrieve those IDs for use in privacy requests, as described in the next section.

## [!DNL Privacy JS Library]

The [!DNL Adobe Privacy JavaScript Library] provides several functions that allow you to retrieve and remove customer identities that are stored in the browser. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Through the use of callbacks or promises, you can programmatically handle successfully retrieved IDs and send them to the [!DNL Privacy Service] API.

For more information about [!DNL Privacy JS Library], including code samples for several common use cases, please refer to the [Privacy JS Library overview](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. For steps on how to send retrieved IDs to [!DNL Privacy Service] for creating access, delete, or opt-out-of-sale requests, see the [Privacy Service developer guide](api/getting-started.md).