---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 25%

---


# Privacy request processing in the [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden zum Zugriff, Opt-out oder Löschen ihrer personenbezogenen Daten gemäß den gesetzlichen und organisatorischen Datenschutzbestimmungen.

This document covers essential concepts related to processing privacy requests for customer data stored in the [!DNL Data Lake].

## Erste Schritte

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [!DNL Privacy Service](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [!DNL Catalog Service](home.md): Das Datensatzsystem für die Datenposition und -linie innerhalb [!DNL Experience Platform]. Stellt eine API bereit, mit der Metadaten von Datensätzen aktualisiert werden können.
* [!DNL Experience Data Model (XDM) System](../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
* [!DNL Identity Service](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] überbrückt Identitätsdaten von Kunden über Systeme und Geräte hinweg. [!DNL Identity Service] verwendet **[!UICONTROL Identitäts-Namensraum]** , um einen Kontext für Identitätswerte bereitzustellen, indem sie sie mit ihrem System der Herkunft verknüpfen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

[!DNL Identity Service] verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen [!DNL Experience Platform]finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

## Hinzufügen von Identitätsdaten zu Datensätzen

Bei der Erstellung von Datenschutzanforderungen für die [!DNL Data Lake]müssen gültige Identitätswerte (und die zugehörigen Namensraum) für jeden einzelnen Kunden angegeben werden, damit die Daten gefunden und entsprechend verarbeitet werden können. Daher müssen alle Datensätze, die Datenschutzanforderungen unterliegen, einen **[!UICONTROL Identitätsdeskriptor]** in ihrem zugehörigen XDM-Schema enthalten.

>[!NOTE]
>
>Datensätze, die auf Schemas basieren, die keine Identitätsdeskriptordaten unterstützen (z. B. Ad-hoc-Datensätze), können derzeit nicht in Datenschutzanforderungen verarbeitet werden.

In diesem Abschnitt werden die Schritte zum Hinzufügen eines Identitätsdeskriptors zum XDM-Schema eines vorhandenen Datensatzes beschrieben. Wenn Sie bereits über einen Datensatz mit einem Identitätsdeskriptor verfügen, können Sie mit dem [nächsten Abschnitt](#nested-maps)fortfahren.

>[!IMPORTANT]
>
>Berücksichtigen Sie bei der Entscheidung, welche Schema-Felder als Identitäten festgelegt werden sollen, die [Einschränkungen bei der Verwendung verschachtelter Kartenfelder](#nested-maps).

Es gibt zwei Methoden zum Hinzufügen eines Identitätsdeskriptors zu einem DataSet-Schema:

* [Verwenden der UI](#identity-ui)
* [Verwenden der API](#identity-api)

### Verwenden der UI {#identity-ui}

In der [!DNL Experience Platform ]Benutzeroberfläche können Sie mit dem Arbeitsbereich &quot; _[!UICONTROL Schemas]_&quot;Ihre vorhandenen XDM-Schema bearbeiten. Um einem Schema einen Identitätsdeskriptor hinzuzufügen, wählen Sie das Schema in der Liste aus und führen Sie die Schritte zum[Festlegen eines Schema-Felds als Identitätsfeld](../xdm/tutorials/create-schema-ui.md#identity-field)im[!DNL Schema Editor]Lernprogramm aus.

Nachdem Sie die entsprechenden Felder im Schema als Identitätsfelder festgelegt haben, können Sie mit dem nächsten Abschnitt zum [Senden von Datenschutzanforderungen](#submit)fortfahren.

### Verwenden der API {#identity-api}

>[!NOTE]
>
>In diesem Abschnitt wird davon ausgegangen, dass Sie den eindeutigen URI-ID-Wert des XDM-Schemas Ihres Datensatzes kennen. Wenn Sie diesen Wert nicht kennen, können Sie ihn mithilfe der [!DNL Catalog Service] API abrufen. Nachdem Sie den [Abschnitt &quot;Erste Schritte](./api/getting-started.md) &quot;im Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die unter zur [Auflistung](./api/list-objects.md) oder [Suche nach](./api/look-up-object.md) [!DNL Catalog] Objekten beschrieben werden, um Ihren Datensatz zu finden. Die Schema-ID finden Sie unter `schemaRef.id`
>
> Dieser Abschnitt enthält Aufrufe der Schema Registry API. Wichtige Informationen zur Verwendung der API, einschließlich der Kenntnisse über Ihre `{TENANT_ID}` und das Konzept der Container, finden Sie im Abschnitt [Erste Schritte](../xdm/api/getting-started.md) im Entwicklerhandbuch.

Sie können dem XDM-Schema eines Datasets einen Identitätsdeskriptor hinzufügen, indem Sie eine POST-Anforderung an den `/descriptors` Endpunkt in der [!DNL Schema Registry] API senden.

**API-Format**

```http
POST /descriptors
```

**Anfrage**

Die folgende Anfrage definiert einen Identitätsdeskriptor für ein Feld „E-Mail-Adresse“ in einem Beispielschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu erstellenden Deskriptors. Bei Identitätsdeskriptoren muss der Wert &quot;xdm:descriptorIdentity&quot;lauten. |
| `xdm:sourceSchema` | Die eindeutige URI-ID des XDM-Schemas Ihres Datensatzes. |
| `xdm:sourceVersion` | Die Version des XDM-Schemas, die in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Der Pfad zum Schema, auf das der Deskriptor angewendet wird. |
| `xdm:namespace` | Einer der [standardmäßigen Identitäts-Namensraum](../privacy-service/api/appendix.md#standard-namespaces) , der von [!DNL Privacy Service]Ihrem Unternehmen erkannt wird, oder ein benutzerdefinierter Namensraum. |
| `xdm:property` | Entweder &quot;xdm:id&quot;oder &quot;xdm:code&quot;, je nach Namensraum, der unter `xdm:namespace`verwendet wird. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn &quot;true&quot;, bedeutet dies, dass das Feld eine primäre Identität ist. Schemas dürfen nur eine primäre Identität enthalten. Die Standardeinstellung lautet &quot;false&quot;(falsch), wenn sie nicht enthalten ist. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Übermitteln von Anfragen {#submit}

>[!NOTE]
>
>This section covers how to format privacy requests for the [!DNL Data Lake]. It is strongly recommended that you review the [!DNL Privacy Service UI](../privacy-service/ui/overview.md) or [!DNL Privacy Service API](../privacy-service/api/getting-started.md) documentation for complete steps on how to submit a privacy job, including how to properly format submitted user identity data in request payloads.

Im folgenden Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für die [!DNL Data Lake] Verwendung der [!DNL Privacy Service] Benutzeroberfläche oder API erstellen.

### Verwenden der UI

When creating job requests in the UI, be sure to select **[!UICONTROL AEP Data Lake]** and/or **[!UICONTROL Profile]** under _[!UICONTROL Products]_in order to process jobs for data stored in the[!DNL Data Lake]or[!DNL Real-time Customer Profile], respectively.

<img src="images/privacy/product-value.png" width="450"><br>

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API müssen alle angegebenen `userIDs` einen bestimmten `namespace` und `type` nutzen, je nach dem Datenspeicher, für den sie gelten. IDs for the [!DNL Data Lake] must use &quot;unregistered&quot; for their `type` value, and a `namespace` value that matches one the [privacy labels](#privacy-labels) that have been added to applicable datasets.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. When making requests to the [!DNL Data Lake], the array must include the value `aepDataLake`.

The following request creates a new privacy job for the [!DNL Data Lake], using the unregistered &quot;email_label&quot; namespace. It also includes the product value for the [!DNL Data Lake] in the `include` array:

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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Verarbeitung von Löschanfragen

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. The records are then removed from the [!DNL Data Lake] within seven days. During that seven-day window, the data is soft-deleted and is therefore not accessible by any [!DNL Platform] service.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Nächste Schritte

By reading this document, you have been introduced to the important concepts involved with processing privacy requests for the [!DNL Data Lake]. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

See the document on [privacy request processing for Real-time Customer Profile](../profile/privacy.md) for steps on processing privacy requests for the [!DNL Profile] store.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Verarbeitung von Datenschutzanforderungen im [!DNL Data Lake].

### Kennzeichnen verschachtelter Felder vom Typ Zuordnung {#nested-maps}

Beachten Sie, dass es zwei Arten von verschachtelten Feldern des Typs Zuordnung gibt, die keine Datenschutzkennzeichnung unterstützen:

* Feld vom Typ Zuordnung in einem Feld vom Typ Array
* Feld vom Typ Zuordnung in einem anderen Feld vom Typ Zuordnung

Die Verarbeitung von Datenschutzaufträgen für beide obigen Beispiele schlägt letztendlich fehl. Aus diesem Grund wird empfohlen, verschachtelte Felder vom Typ Zuordnung nicht zum Speichern vertraulicher Kundendaten zu verwenden. Relevante Kundenkennungen sollten bei datensatzbasierten Datensätzen als Nicht-Zuordnungs-Datentyp im `identityMap`-Feld (selbst ein Feld vom Typ Zuordnung) bzw. bei zeitreihenbasierten Datensätzen im `endUserID`-Feld gespeichert werden.