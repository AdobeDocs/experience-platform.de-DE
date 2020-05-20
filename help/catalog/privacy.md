---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: d3584202554baf46aad174d671084751e6557bbc
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# Verarbeitung von Datenschutzanfragen im Data Lake

Der Adobe Experience Platform-Datenschutzdienst verarbeitet Anfragen von Kunden, um auf ihre personenbezogenen Daten zuzugreifen, sie Opt-out zu verkaufen oder sie zu löschen, wie in den gesetzlichen und organisatorischen Datenschutzbestimmungen festgelegt.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanforderungen für im Data Lake gespeicherte Kundendaten behandelt.

## Erste Schritte

Es wird empfohlen, die folgenden Experience Platform-Dienste zu verstehen, bevor Sie dieses Handbuch lesen:

* [Datenschutzdienst](../privacy-service/home.md): Verwaltet Kundenanforderungen für den Zugriff auf, die Einstellung des Verkaufs oder das Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [Katalogdienst](home.md): Das Datensatzsystem für die Position und die Lineage von Daten in Experience Platform. Stellt eine API bereit, mit der die Metadaten des Datensatzes aktualisiert werden können.
* [Erlebnis-Datenmodell (XDM)-System](../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Identitätsdienst](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.

## Identitäts-Namensräume {#namespaces}

Der Identitätsdienst für Adobe Experience Platform verbindet Daten zur Kundenidentität über Systeme und Geräte hinweg. Der Identitätsdienst nutzt **Identitätskennungen** , um einen Kontext für Identitätswerte bereitzustellen, indem er sie mit ihrem System der Herkunft verknüpft. Ein Namensraum kann ein allgemeines Konzept wie eine E-Mail-Adresse (&quot;E-Mail&quot;) oder die Identität einer bestimmten Anwendung zuordnen, z. B. einer Adobe Advertising Cloud ID (&quot;AdCloud&quot;) oder einer Adobe-Zielgruppe-ID (&quot;TNTID&quot;).

Der Identitätsdienst verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen in Experience Platform finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

## Hinzufügen von Identitätsdaten zu Datensätzen

Beim Erstellen von Datenschutzanforderungen für den Data Lake müssen für jeden einzelnen Kunden gültige Identitätswerte (und die zugehörigen Namensraum) angegeben werden, um die Daten zu finden und entsprechend zu verarbeiten. Daher müssen alle Datensätze, die Datenschutzanforderungen unterliegen, einen **Identitätsdeskriptor** in ihrem zugehörigen XDM-Schema enthalten.

>[!NOTE] Datensätze, die auf Schemas basieren, die keine Identitätsdeskriptordaten unterstützen (z. B. Ad-hoc-Datensätze), können derzeit nicht in Datenschutzanforderungen verarbeitet werden.

In diesem Abschnitt werden die Schritte zum Hinzufügen eines Identitätsdeskriptors zum XDM-Schema eines vorhandenen Datensatzes beschrieben. Wenn Sie bereits über einen Datensatz mit einem Identitätsdeskriptor verfügen, können Sie mit dem [nächsten Abschnitt](#nested-maps)fortfahren.

>[!IMPORTANT] Berücksichtigen Sie bei der Entscheidung, welche Schema-Felder als Identitäten festgelegt werden sollen, die [Einschränkungen bei der Verwendung verschachtelter Kartenfelder](#nested-maps).

Es gibt zwei Methoden zum Hinzufügen eines Identitätsdeskriptors zu einem DataSet-Schema:

* [Verwenden der Benutzeroberfläche](#identity-ui)
* [Verwenden der API](#identity-api)

### Verwenden der Benutzeroberfläche {#identity-ui}

In der Benutzeroberfläche von Experience Platform können Sie Ihre vorhandenen XDM-Schema mit dem Arbeitsbereich _[!UICONTROL Schemas]_bearbeiten. Um einem Schema einen Identitätsdeskriptor hinzuzufügen, wählen Sie das Schema in der Liste aus und befolgen Sie die Schritte zum[Festlegen eines Schema-Felds als Identitätsfeld](../xdm/tutorials/create-schema-ui.md#identity-field)im Schema-Editor-Lernprogramm.

Nachdem Sie die entsprechenden Felder im Schema als Identitätsfelder festgelegt haben, können Sie mit dem nächsten Abschnitt zum [Senden von Datenschutzanforderungen](#submit)fortfahren.

### Verwenden der API {#identity-api}

>[!NOTE] In diesem Abschnitt wird davon ausgegangen, dass Sie den eindeutigen URI-ID-Wert des XDM-Schemas Ihres Datensatzes kennen. Wenn Sie diesen Wert nicht kennen, können Sie ihn mithilfe der Katalogdienst-API abrufen. Nachdem Sie den [Abschnitt &quot;Erste Schritte](./api/getting-started.md) &quot;im Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die unter zur [Auflistung](./api/list-objects.md) oder [Suche](./api/look-up-object.md) von Katalogobjekten nach dem Datensatz beschrieben werden. Die Schema-ID finden Sie unter `schemaRef.id`
>
> Dieser Abschnitt enthält Aufrufe der Schema Registry API. Wichtige Informationen zur Verwendung der API, einschließlich der Kenntnisse über Ihre `{TENANT_ID}` und das Konzept der Container, finden Sie im Abschnitt [Erste Schritte](../xdm/api/getting-started.md) im Entwicklerhandbuch.

Sie können dem XDM-Schema eines Datasets einen Identitätsdeskriptor hinzufügen, indem Sie eine POST-Anforderung an den `/descriptors` Endpunkt in der Schema Registry-API senden.

**API-Format**

```http
POST /descriptors
```

**Anfrage**

Die folgende Anforderung definiert einen Identitätsdeskriptor für ein &quot;E-Mail-Adresse&quot;-Feld in einem Beispiel-Schema.

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
| `xdm:namespace` | Einer der vom Datenschutzdienst erkannten [Identitätskennungen](../privacy-service/api/appendix.md#standard-namespaces) oder ein benutzerdefinierter Namensraum, der von Ihrem Unternehmen definiert wird. |
| `xdm:property` | Entweder &quot;xdm:id&quot;oder &quot;xdm:code&quot;, je nach Namensraum, der unter `xdm:namespace`verwendet wird. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn &quot;true&quot;, bedeutet dies, dass das Feld eine primäre Identität ist. Schema dürfen nur eine primäre Identität enthalten. Die Standardeinstellung lautet &quot;false&quot;(falsch), wenn sie nicht enthalten ist. |

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

## Einreichen von Anträgen {#submit}

>[!NOTE] In diesem Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für den Data Lake formatieren. Es wird dringend empfohlen, die Dokumentation der Benutzeroberfläche [des](../privacy-service/ui/overview.md) Datenschutzdienstes oder der [Datenschutzdienst-API](../privacy-service/api/getting-started.md) zu lesen, um die vollständigen Schritte zum Senden eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anforderungs-Nutzdaten.

Im folgenden Abschnitt wird beschrieben, wie Sie mithilfe der Benutzeroberfläche oder API des Datenschutzdienstes Datenschutzanforderungen für den Data Lake durchführen.

### Verwenden der Benutzeroberfläche

Wählen Sie beim Erstellen von Auftragsanforderungen in der Benutzeroberfläche **AEP Data Lake** und/oder **Profil** unter _Products_ aus, um Aufträge für Daten zu verarbeiten, die im Data Lake bzw. im Real-Time Customer Profil gespeichert werden.

<img src="images/privacy/product-value.png" width="450"><br>

### Verwenden der API

Beim Erstellen von Auftragsanforderungen in der API müssen alle `userIDs` bereitgestellten Aufträge einen bestimmten `namespace` und `type` je nach Datenspeicher verwenden, für den sie gelten. IDs für den Data Lake müssen für ihren `type` Wert &quot;nicht registriert&quot;und einen `namespace` Wert verwenden, der mit einer der [Datenschutzbeschriftungen](#privacy-labels) übereinstimmt, die den entsprechenden Datensätzen hinzugefügt wurden.

Darüber hinaus muss das `include` Array der Anforderungs-Nutzlast die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anforderung gesendet wird. Bei Anforderungen an den Data Lake muss das Array den Wert &quot;aepDataLake&quot;enthalten.

Die folgende Anforderung erstellt einen neuen Datenschutzauftrag für den Data Lake mit dem nicht registrierten Namensraum &quot;email_label&quot;. Er enthält außerdem den Produktwert für den Data Lake im `include` Array:

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

## Anforderungsverarbeitung löschen

Wenn Experience Platform eine Löschanforderung vom Datenschutzdienst erhält, sendet Platform eine Bestätigung an den Datenschutzdienst, dass die Anforderung empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann innerhalb von sieben Tagen aus dem Data Lake entfernt. Während dieses siebentägigen Fensters werden die Daten weich gelöscht und stehen daher keinem Plattformdienst zur Verfügung.

In zukünftigen Versionen sendet Platform eine Bestätigung an den Datenschutzdienst, nachdem die Daten physisch gelöscht wurden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie zu den wichtigen Konzepten der Verarbeitung von Datenschutzanforderungen für den Data Lake vorgestellt. Es wird empfohlen, die Dokumentation in diesem Handbuch weiter zu lesen, um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen.

Anweisungen zur Verarbeitung von Datenschutzanforderungen für den Profil Store finden Sie im Dokument zur Verarbeitung von [Datenschutzanforderungen für Echtzeit-Kundendaten](../profile/privacy.md) .

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Verarbeitung von Datenschutzanforderungen im Data Lake.

### Bezeichnen verschachtelter Kartenfelder {#nested-maps}

Beachten Sie, dass es zwei Arten von verschachtelten Kartenfeldern gibt, die keine Datenschutzkennzeichnung unterstützen:

* Ein Feld vom Typ &quot;map&quot;in einem Feld vom Typ &quot;array&quot;
* Ein Feld vom Typ &quot;Map&quot;in einem anderen Feld vom Typ &quot;map&quot;

Die Verarbeitung von Datenschutzaufträgen für eines der beiden obigen Beispiele schlägt schließlich fehl. Aus diesem Grund wird empfohlen, verschachtelte Felder vom Typ &quot;Map&quot;nicht zum Speichern von Daten privater Kunden zu verwenden. Relevante Kunden-IDs sollten als Nicht-Map-Datentyp innerhalb des `identityMap` Felds (selbst ein Zuordnungsfeld) für Datensatzdatasets oder als `endUserID` Feld für zeitreihenbasierte Datensätze gespeichert werden.