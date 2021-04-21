---
keywords: Experience Platform;Home;beliebte Themen;Datenschutz;Identitäts-Namensräume;Privatsphäre;Datensee
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Data Lake
topic-legacy: overview
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, um auf ihre personenbezogenen Daten zuzugreifen, sie Opt-out zu verkaufen oder sie zu löschen, wie in den gesetzlichen und organisatorischen Datenschutzbestimmungen festgelegt. In diesem Dokument werden wesentliche Konzepte bei der Verarbeitung von Datenschutzanfragen für im Data Lake gespeicherte Kundendaten behandelt.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 25%

---

# Verarbeitung von Datenschutzanforderungen in [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden zum Zugriff, Opt-out oder Löschen ihrer personenbezogenen Daten gemäß den gesetzlichen und organisatorischen Datenschutzbestimmungen.

Dieses Dokument behandelt wesentliche Konzepte im Zusammenhang mit der Verarbeitung von Datenschutzanforderungen für Kundendaten, die im Ordner [!DNL Data Lake] gespeichert sind.

## Erste Schritte

Es wird empfohlen, die folgenden [!DNL Experience Platform]-Dienste zu verstehen, bevor Sie dieses Handbuch lesen:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Catalog Service]](home.md): Das Datensatzsystem für die Datenposition und -linie innerhalb  [!DNL Experience Platform]. Stellt eine API bereit, mit der Metadaten von Datensätzen aktualisiert werden können.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
* [[!DNL Identity Service]](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] überbrückt Identitätsdaten von Kunden über Systeme und Geräte hinweg. [!DNL Identity Service] verwendet Identitäts-Namensraum, um einen Kontext zu Identitätswerten bereitzustellen, indem sie sie mit ihrem System der Herkunft verknüpfen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

[!DNL Identity Service] verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen in [!DNL Experience Platform] finden Sie unter [Übersicht über Identitäts-Namensraum](../identity-service/namespaces.md).

## Hinzufügen von Identitätsdaten zu Datensätzen

Beim Erstellen von Datenschutzanforderungen für das [!DNL Data Lake] müssen für jeden Kunden gültige Identitätswerte (und die zugehörigen Namensraum) angegeben werden, um die Daten zu finden und sie entsprechend zu verarbeiten. Daher müssen alle Datensätze, die Datenschutzanforderungen unterliegen, einen Identitätsdeskriptor in ihrem zugehörigen XDM-Schema enthalten.

>[!NOTE]
>
>Datensätze, die auf Schemas basieren, die keine Identitätsdeskriptordaten unterstützen (z. B. Ad-hoc-Datensätze), können derzeit nicht in Datenschutzanforderungen verarbeitet werden.

In diesem Abschnitt werden die Schritte zum Hinzufügen eines Identitätsdeskriptors zum XDM-Schema eines vorhandenen Datensatzes beschrieben. Wenn Sie bereits über einen Datensatz mit einem Identitätsdeskriptor verfügen, können Sie mit dem [nächsten Abschnitt](#nested-maps) fortfahren.

>[!IMPORTANT]
>
>Beachten Sie bei der Entscheidung, welche Schema-Felder als Identitäten festgelegt werden sollen, die [Einschränkungen bei der Verwendung von verschachtelten Kartenfeldern](#nested-maps).

Es gibt zwei Methoden zum Hinzufügen eines Identitätsdeskriptors zu einem DataSet-Schema:

* [Verwenden der UI](#identity-ui)
* [Verwenden der API](#identity-api)

### Verwenden der UI {#identity-ui}

In der [!DNL Experience Platform ]Benutzeroberfläche können Sie mit dem Arbeitsbereich **[!UICONTROL Schema]** Ihre vorhandenen XDM-Schema bearbeiten. Um einem Schema einen Identitätsdeskriptor hinzuzufügen, wählen Sie das Schema in der Liste aus und befolgen Sie die Schritte für [Einrichten eines Schema-Felds als Identitätsfeld](../xdm/tutorials/create-schema-ui.md#identity-field) im Lehrgang [!DNL Schema Editor].

Nachdem Sie die entsprechenden Felder im Schema als Identitätsfelder festgelegt haben, können Sie mit dem nächsten Abschnitt [Datenschutzanforderungen senden](#submit) fortfahren.

### Verwenden der API {#identity-api}

>[!NOTE]
>
>In diesem Abschnitt wird davon ausgegangen, dass Sie den eindeutigen URI-ID-Wert des XDM-Schemas Ihres Datensatzes kennen. Wenn Sie diesen Wert nicht kennen, können Sie ihn mit der API [!DNL Catalog Service] abrufen. Nachdem Sie den Abschnitt [Erste Schritte](./api/getting-started.md) des Entwicklerhandbuchs gelesen haben, führen Sie die Schritte aus, die unter [Auflistung](./api/list-objects.md) oder [Suchen](./api/look-up-object.md) [!DNL Catalog]-Objekte beschrieben sind, um Ihren Datensatz zu finden. Die Schema-ID befindet sich unter `schemaRef.id`
>
> Dieser Abschnitt enthält Aufrufe der Schema Registry API. Wichtige Informationen zur Verwendung der API, einschließlich des Wissens über `{TENANT_ID}` und das Konzept der Container, finden Sie im Abschnitt [Erste Schritte](../xdm/api/getting-started.md) des Entwicklerhandbuchs.

Sie können dem XDM-Schema eines Datasets einen Identitätsdeskriptor hinzufügen, indem Sie eine POST an den `/descriptors`-Endpunkt in der [!DNL Schema Registry]-API anfordern.

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
| `xdm:sourceVersion` | Die in `xdm:sourceSchema` angegebene Version des XDM-Schemas. |
| `xdm:sourceProperty` | Der Pfad zum Schema, auf das der Deskriptor angewendet wird. |
| `xdm:namespace` | Einer der [Standardidentitäts-Namensraum](../privacy-service/api/appendix.md#standard-namespaces), der von [!DNL Privacy Service] erkannt wird, oder ein benutzerdefinierter Namensraum, der von Ihrem Unternehmen definiert wird. |
| `xdm:property` | Entweder &quot;xdm:id&quot;oder &quot;xdm:code&quot;, je nach Namensraum, der unter `xdm:namespace` verwendet wird. |
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
>In diesem Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für [!DNL Data Lake] formatieren. Es wird dringend empfohlen, die Dokumentation [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) oder [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) zu lesen, um die vollständigen Schritte zum Senden eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anforderungs-Nutzdaten.

Im folgenden Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für [!DNL Data Lake] mithilfe der [!DNL Privacy Service]-Benutzeroberfläche oder -API durchführen.

>[!IMPORTANT]
>
>Die Dauer, die eine Datenschutzanforderung dauern kann, kann nicht garantiert werden. Wenn Änderungen im Data Lake während der Verarbeitung einer Anforderung auftreten, kann auch nicht garantiert werden, ob diese Datensätze verarbeitet werden oder nicht.

### Verwenden der UI

Wählen Sie beim Erstellen von Auftragsanforderungen in der Benutzeroberfläche unter **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** unter **[!UICONTROL Produkte]** aus, um Aufträge für die in [!DNL Data Lake] oder [!DNL Real-time Customer Profile] gespeicherten Daten zu verarbeiten.

<img src="images/privacy/product-value.png" width="450"><br>

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API müssen alle angegebenen `userIDs` einen bestimmten `namespace` und `type` nutzen, je nach dem Datenspeicher, für den sie gelten. IDs für [!DNL Data Lake] müssen &quot;nicht registriert&quot;für ihren `type`-Wert und einen `namespace`-Wert verwenden, der mit einer [Datenschutzbeschriftung](#privacy-labels) übereinstimmt, die den entsprechenden Datensätzen hinzugefügt wurde.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Bei Anforderungen an [!DNL Data Lake] muss das Array den Wert `aepDataLake` enthalten.

Mit der folgenden Anforderung wird ein neuer Datenschutzauftrag für [!DNL Data Lake] unter Verwendung des nicht registrierten Namensraums &quot;email_label&quot;erstellt. Er enthält außerdem den Produktwert für [!DNL Data Lake] im `include`-Array:

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

Wenn [!DNL Experience Platform] eine Löschanforderung von [!DNL Privacy Service] erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anforderung empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann innerhalb von sieben Tagen aus dem [!DNL Data Lake] entfernt. Während dieses siebentägigen Fensters werden die Daten weich gelöscht und stehen daher keinem [!DNL Platform]-Dienst zur Verfügung.

In zukünftigen Versionen sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], nachdem die Daten physisch gelöscht wurden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie zu den wichtigen Konzepten der Verarbeitung von Datenschutzanforderungen für das [!DNL Data Lake] hinzugefügt. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Im Dokument [Verarbeitung von Datenschutzanforderungen für Echtzeit-Kundendaten](../profile/privacy.md) finden Sie Anweisungen zur Verarbeitung von Datenschutzanforderungen für den [!DNL Profile]-Speicher.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Verarbeitung von Datenschutzanforderungen in der [!DNL Data Lake].

### Kennzeichnen verschachtelter Felder vom Typ Zuordnung {#nested-maps}

Beachten Sie, dass es zwei Arten von verschachtelten Feldern des Typs Zuordnung gibt, die keine Datenschutzkennzeichnung unterstützen:

* Feld vom Typ Zuordnung in einem Feld vom Typ Array
* Feld vom Typ Zuordnung in einem anderen Feld vom Typ Zuordnung

Die Verarbeitung von Datenschutzaufträgen für beide obigen Beispiele schlägt letztendlich fehl. Aus diesem Grund wird empfohlen, verschachtelte Felder vom Typ Zuordnung nicht zum Speichern vertraulicher Kundendaten zu verwenden. Relevante Kundenkennungen sollten bei datensatzbasierten Datensätzen als Nicht-Zuordnungs-Datentyp im `identityMap`-Feld (selbst ein Feld vom Typ Zuordnung) bzw. bei zeitreihenbasierten Datensätzen im `endUserID`-Feld gespeichert werden.
