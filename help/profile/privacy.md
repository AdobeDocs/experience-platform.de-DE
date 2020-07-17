---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Profil des Kunden
topic: overview
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 31%

---


# Verarbeitung von Datenschutzanfragen in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] processes customer requests to access, opt out of sale, or delete their personal data as delineated by privacy regulations such as the General Data Protection Regulation (GDPR) and [!DNL California Consumer Privacy Act] (CCPA).

In diesem Dokument werden wesentliche Konzepte für die Verarbeitung von Datenschutzanforderungen für [!DNL Real-time Customer Profile]Daten behandelt.

## Erste Schritte

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [!DNL Privacy Service](home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [!DNL Identity Service](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [!DNL Real-time Customer Profile](../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] überbrückt Identitätsdaten von Kunden über Systeme und Geräte hinweg. [!DNL Identity Service] verwendet **Identitäts-Namensraum** , um einen Kontext für Identitätswerte bereitzustellen, indem sie sie mit ihrem System der Herkunft verknüpfen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Der Identitätsdienst verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen [!DNL Experience Platform]finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

## Übermitteln von Anfragen {#submit}

>[!NOTE]
>
>This section covers how to create privacy requests for the [!DNL Profile] data store. Es wird dringend empfohlen, die Dokumentation zur [Privacy Service-API](../privacy-service/api/getting-started.md) oder zur [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) zu lesen, um mehr über alle Schritte beim Übermitteln eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

The following section outlines how to make privacy requests for [!DNL Real-time Customer Profile] and the [!DNL Data Lake] using the [!DNL Privacy Service] API or UI.

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API müssen alle angegebenen `userIDs` einen bestimmten `namespace` und `type` nutzen, je nach dem Datenspeicher, für den sie gelten. IDs für den [!DNL Profile] Store müssen entweder &quot;Standard&quot;oder &quot;benutzerdefiniert&quot;für ihren `type` Wert und einen gültigen [Identitäts-Namensraum](#namespaces) verwenden, der [!DNL Identity Service] für seinen `namespace` Wert erkannt wird.


Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. When making requests to the [!DNL Data Lake], the array must include the value &quot;ProfileService&quot;.

Mit der folgenden Anforderung wird ein neuer Datenschutzauftrag für beide Seiten [!DNL Real-time Customer Profile]unter Verwendung des standardmäßigen &quot;E-Mail&quot;-Identitäts-Namensraums erstellt. It also includes the product value for [!DNL Profile] in the `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Verwenden der UI

When creating job requests in the UI, be sure to select **[!UICONTROL AEP Data Lake]** and/or **[!UICONTROL Profile]** under _[!UICONTROL Products]_in order to process jobs for data stored in the[!DNL Data Lake]or[!DNL Real-time Customer Profile], respectively.

<img src="images/privacy/product-value.png" width="450"><br>

## Verarbeitung von Löschanfragen

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. The records are then removed from the [!DNL Data Lake] or [!DNL Profile] store within seven days. During that seven-day window, the data is soft-deleted and is therefore not accessible by any [!DNL Platform] service.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Nächste Schritte

By reading this document, you have been introduced to the important concepts involved with processing privacy requests in [!DNL Experience Platform]. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanforderungen für nicht von [!DNL Platform] Ihnen verwendete [!DNL Profile]Ressourcen finden Sie im Dokument zur Verarbeitung von [Datenschutzanfragen im Data Lake](../catalog/privacy.md).