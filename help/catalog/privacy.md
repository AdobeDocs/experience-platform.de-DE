---
keywords: Experience Platform;Startseite;beliebte Themen;Datenschutz;Identity-Namespaces;Privatsphäre;Data Lake
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Data Lake
topic-legacy: overview
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, auf ihre personenbezogenen Daten zuzugreifen, sich gegen deren Verkauf zu wenden oder sie zu löschen, wie in den gesetzlichen und organisatorischen Datenschutzbestimmungen festgelegt. In diesem Dokument werden wesentliche Konzepte bei der Verarbeitung von Datenschutzanfragen für im Data Lake gespeicherte Kundendaten behandelt.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 100%

---

# Verarbeiten von Datenschutzanfragen im [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] bearbeitet Anfragen von Kunden, auf ihre personenbezogenen Daten zuzugreifen, sich gegen deren Verkauf zu wenden oder sie zu löschen, wie in den gesetzlichen und organisatorischen Datenschutzbestimmungen festgelegt.

In diesem Dokument werden wesentliche Konzepte bei der Verarbeitung von Datenschutzanfragen für im [!DNL Data Lake] gespeicherte Kundendaten behandelt.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Data Lake in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Echtzeit-Kundenprofil-Datenspeicher vornehmen möchten, lesen Sie zusätzlich zu diesem Tutorial das Handbuch [Verarbeitung von Datenschutzanfragen für Profil](../profile/privacy.md).
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

## Erste Schritte

Sie sollten über Grundkenntnisse zu folgenden [!DNL Experience Platform]-Services verfügen, bevor Sie dieses Handbuch lesen:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Catalog Service]](home.md): Das Aufzeichnungssystem für Speicherort und Herkunft von Daten in [!DNL Experience Platform]. Stellt eine API bereit, mit der Metadaten von Datensätzen aktualisiert werden können.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
* [[!DNL Identity Service]](../identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service] verwendet Identitäts-Namespaces, um einen Kontext zu Identitätswerten bereitzustellen, indem sie mit dem System ihrer Herkunft verknüpft werden. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) sein oder die Identität einer bestimmten Anwendung zuordnen, wie z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

[!DNL Identity Service] verwaltet einen Speicher global definierter (standardmäßiger) und benutzerdefinierter Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/namespaces.md).

## Hinzufügen von Identitätsdaten zu Datensätzen

Beim Erstellen von Datenschutzanfragen für den [!DNL Data Lake] müssen für jeden Kunden gültige Identitätswerte (und die zugehörigen Namespaces) angegeben werden, um die Daten finden und sie entsprechend verarbeiten zu können. Daher müssen alle Datensätze, die Datenschutzanfragen unterliegen, einen Identitätsdeskriptor in ihrem zugehörigen XDM-Schema enthalten.

>[!NOTE]
>
>Datensätze, die auf Schemata basieren, die keine Identitätsdeskriptor-Metadaten unterstützen (z. B. Ad-hoc-Datensätze), können derzeit nicht in Datenschutzanfragen verarbeitet werden.

In diesem Abschnitt werden die Schritte zum Hinzufügen eines Identitätsdeskriptors zum XDM-Schema eines vorhandenen Datensatzes beschrieben. Wenn Sie bereits über einen Datensatz mit einem Identitätsdeskriptor verfügen, können Sie zum [nächsten Abschnitt](#nested-maps) springen.

>[!IMPORTANT]
>
>Beachten Sie bei der Entscheidung, welche Schema-Felder als Identitäten festgelegt werden sollen, die [Einschränkungen bei der Verwendung von verschachtelten Feldern vom Mapping-Typ](#nested-maps).

Es gibt zwei Methoden zum Hinzufügen eines Identitätsdeskriptors zu einem Datensatzschema:

* [Verwenden der Benutzeroberfläche](#identity-ui)
* [Verwenden der API](#identity-api)

### Verwenden der Benutzeroberfläche {#identity-ui}

In der [!DNL Experience Platform ]-Benutzeroberfläche können Sie mit dem Arbeitsbereich **[!UICONTROL Schemata]** Ihre vorhandenen XDM-Schemata bearbeiten. Um einem Schema einen Identitätsdeskriptor hinzuzufügen, wählen Sie das Schema in der Liste aus und befolgen Sie die Schritte zum [Einrichten eines Schema-Felds als Identitätsfeld](../xdm/tutorials/create-schema-ui.md#identity-field) im Tutorial [!DNL Schema Editor].

Nachdem Sie die entsprechenden Felder im Schema als Identitätsfelder festgelegt haben, können Sie mit dem nächsten Abschnitt zum [Senden von Datenschutzanfragen](#submit) fortfahren.

### Verwenden der API {#identity-api}

>[!NOTE]
>
>In diesem Abschnitt wird davon ausgegangen, dass Sie den eindeutigen URI-ID-Wert des XDM-Schemas Ihres Datensatzes kennen. Wenn Sie diesen Wert nicht kennen, können Sie ihn mit der [!DNL Catalog Service]-API abrufen. Nachdem Sie den Abschnitt [Erste Schritte](./api/getting-started.md) des Entwicklerhandbuchs gelesen haben, führen Sie die Schritte aus, die unter [Auflistung](./api/list-objects.md) oder [Suchen](./api/look-up-object.md) von [!DNL Catalog]-Objekten beschrieben sind, um Ihren Datensatz zu finden. Die Schema-ID befindet sich unter `schemaRef.id`
>
>In diesem Abschnitt wird außerdem davon ausgegangen, dass Sie wissen, wie Sie Aufrufe an die Schema-Registry-API durchführen. Wichtige Informationen zur Verwendung der API, einschließlich Details über `{TENANT_ID}` und das Konzept der Container, finden Sie im Abschnitt [Erste Schritte](../xdm/api/getting-started.md) des API-Handbuchs.

Sie können dem XDM-Schema eines Datensatzes einen Identitätsdeskriptor hinzufügen, indem Sie eine POST-Anfrage an den `/descriptors`-Endpunkt in der [!DNL Schema Registry]-API stellen.

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `@type` | Der Typ des zu erstellenden Deskriptors. Bei Identitätsdeskriptoren muss der Wert „xdm:descriptorIdentity“ lauten. |
| `xdm:sourceSchema` | Die eindeutige URI-ID des XDM-Schemas Ihres Datensatzes. |
| `xdm:sourceVersion` | Die in `xdm:sourceSchema` angegebene Version des XDM-Schemas. |
| `xdm:sourceProperty` | Der Pfad zum Schemafeld, auf das der Deskriptor angewendet wird. |
| `xdm:namespace` | Einer der [standardmäßigen Identity-Namespaces](../privacy-service/api/appendix.md#standard-namespaces), die von [!DNL Privacy Service] erkannt werden, oder ein benutzerdefinierter Namespace, der von Ihrem Unternehmen definiert wurde. |
| `xdm:property` | Entweder „xdm:id“ oder „xdm:code“, je nach Namespace, der unter `xdm:namespace` verwendet wird. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn „true“, bedeutet dies, dass das Feld eine primäre Identität ist. Schemas dürfen nur eine primäre Identität enthalten. Die Standardeinstellung lautet „false“, wenn sie nicht enthalten ist. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) sowie die Details des neu erstellten Deskriptors zurück.

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
>In diesem Abschnitt wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Data Lake] formatieren. Es wird dringend empfohlen, die Dokumentation zur [[!DNL Privacy Service] Benutzeroberfläche](../privacy-service/ui/overview.md) oder zur [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) zu lesen, um mehr über alle Schritte beim Übermitteln eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Payloads von Anfragen.

Im folgenden Abschnitt wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Data Lake] mithilfe der [!DNL Privacy Service]-Benutzeroberfläche oder -API durchführen.

>[!IMPORTANT]
>
>Die Dauer, die eine Datenschutzanfrage in Anspruch nehmen kann, kann nicht garantiert werden. Wenn Änderungen in Data Lake während der Verarbeitung einer Anfrage auftreten, kann auch nicht garantiert werden, ob diese Datensätze verarbeitet werden oder nicht.

### Verwenden der Benutzeroberfläche

Wählen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** unter **[!UICONTROL Produkte]** aus, um Aufträge für Daten, die in [!DNL Data Lake] bzw. [!DNL Real-time Customer Profile] gespeichert sind, zu verarbeiten.

<img src="images/privacy/product-value.png" width="450"><br>

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API müssen alle angegebenen `userIDs` einen bestimmten `namespace` und `type` nutzen, je nach dem Datenspeicher, für den sie gelten. Kennungen für [!DNL Data Lake] müssen bei `type` den Wert `unregistered` aufweisen sowie über einen `namespace`-Wert verfügen, der mit einer der [Datenschutzkennzeichnungen](#privacy-labels) übereinstimmt, die den entsprechenden Datensätzen hinzugefügt wurden.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Bei Anfragen an [!DNL Data Lake] muss das Array den Wert `aepDataLake` enthalten.

In der folgenden Anfrage wird ein neuer Datenschutzvorgang für den [!DNL Data Lake] mit dem nicht registrierten Namespace `email_label` erstellt. Sie enthält außerdem den Produktwert für [!DNL Data Lake] im `include`-Array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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

>[!IMPORTANT]
>
>Platform verarbeitet Datenschutzanfragen für alle [Sandboxes](../sandboxes/home.md), die zu Ihrer Organisation gehören. Daher wird jede `x-sandbox-name`-Kopfzeile, die in der Anfrage enthalten ist, vom System ignoriert.

## Verarbeitung von Löschanfragen

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann innerhalb von sieben Tagen aus [!DNL Data Lake] entfernt. Während dieses 7-Tage-Fensters werden die Daten vorläufig gelöscht und stehen somit keinem [!DNL Platform]-Service mehr zur Verfügung.

In zukünftigen Versionen wird [!DNL Platform] eine Bestätigung an [!DNL Privacy Service] senden, nachdem Daten physisch gelöscht wurden.

## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu den wichtigsten Konzepten bei der Verarbeitung von Datenschutzanfragen für [!DNL Data Lake] erhalten. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Anweisungen zur Verarbeitung von Datenschutzanfragen für den [!DNL Profile]-Speicher finden Sie im Dokument zur [Verarbeitung von Datenschutzanfragen für Echtzeit-Kundenprofile](../profile/privacy.md).

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Verarbeitung von Datenschutzanfragen in [!DNL Data Lake].

### Kennzeichnen verschachtelter Felder vom Typ Zuordnung {#nested-maps}

Beachten Sie, dass es zwei Arten von verschachtelten Feldern des Typs Zuordnung gibt, die keine Datenschutzkennzeichnung unterstützen:

* Feld vom Typ Zuordnung in einem Feld vom Typ Array
* Feld vom Typ Zuordnung in einem anderen Feld vom Typ Zuordnung

Die Verarbeitung von Datenschutzaufträgen für beide obigen Beispiele schlägt letztendlich fehl. Aus diesem Grund wird empfohlen, verschachtelte Felder vom Typ Zuordnung nicht zum Speichern vertraulicher Kundendaten zu verwenden. Relevante Kundenkennungen sollten bei datensatzbasierten Datensätzen als Nicht-Zuordnungs-Datentyp im `identityMap`-Feld (selbst ein Feld vom Typ Zuordnung) bzw. bei zeitreihenbasierten Datensätzen im `endUserID`-Feld gespeichert werden.
