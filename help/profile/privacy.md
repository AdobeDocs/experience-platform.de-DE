---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Profil des Kunden
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 11%

---


# Verarbeitung von Datenschutzanfragen in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] processes customer requests to access, opt out of sale, or delete their personal data as delineated by privacy regulations such as the General Data Protection Regulation (GDPR) and [!DNL California Consumer Privacy Act] (CCPA).

In diesem Dokument werden wesentliche Konzepte für die Verarbeitung von Datenschutzanforderungen für [!DNL Real-time Customer Profile]Daten behandelt.

## Erste Schritte

It is recommended that you have a working understanding of the following [!DNL Experience Platform] services before reading this guide:

* [[!DNL Privacy Service]](home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] überbrückt Identitätsdaten von Kunden über Systeme und Geräte hinweg. [!DNL Identity Service] verwendet **Identitäts-Namensraum** , um einen Kontext für Identitätswerte bereitzustellen, indem sie sie mit ihrem System der Herkunft verknüpfen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Der Identitätsdienst verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen [!DNL Experience Platform]finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanforderungen für die [!DNL Real-time Customer Profile] Verwendung der [!DNL Privacy Service] API oder Benutzeroberfläche stellen. Before reading these sections, it is strongly recommended that you review the [Privacy Service API](../privacy-service/api/getting-started.md) or [Privacy Service UI](../privacy-service/ui/overview.md) documentation for complete steps on how to submit a privacy job, including how to properly format submitted user identity data in request payloads.

>[!IMPORTANT]
>
>Privacy Service kann [!DNL Profile] Daten nur mit einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszuordnung vornimmt. Wenn Sie die Benutzeroberfläche verwenden, um zu bestätigen, ob Ihre Datenschutzanforderungen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit &quot;[!DNL None]&quot;als [!UICONTROL ID-Hefttyp] verwenden. Mit anderen Worten: Sie können keine Zusammenführungsrichtlinie verwenden, bei der die [!UICONTROL ID-Suche] auf &quot;[!UICONTROL Privates Diagramm]&quot;eingestellt ist.
>
>![](./images/privacy/no-id-stitch.png)
>
>Es ist auch wichtig zu beachten, dass die Dauer, die eine Datenschutzanforderung dauern kann, nicht garantiert werden kann. Wenn während der Verarbeitung einer Anforderung Änderungen an Ihren [!DNL Profile] Daten auftreten, kann auch nicht garantiert werden, dass diese Datensätze verarbeitet werden.

### Verwenden der API

Beim Erstellen von Auftragsanforderungen in der API `userIDs` müssen alle IDs, die in bereitgestellt werden, eine bestimmte `namespace` und eine bestimmte `type`verwenden. Ein gültiger [Identitätswert](#namespaces) , der von erkannt [!DNL Identity Service] wird, muss für den `namespace` Wert angegeben werden, während der Namensraum entweder `type` oder `standard` `unregistered` (für Standard- bzw. benutzerdefinierte Namensraum) angegeben werden muss.

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Verteilung der Fragmente in Plattformdatensätzen müssen Sie für jeden Profil möglicherweise mehr als eine ID angeben. Weitere Informationen finden Sie im nächsten Abschnitt [Profil-Fragmente](#fragments) .

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. When making requests to the [!DNL Data Lake], the array must include the value &quot;ProfileService&quot;.

Die folgende Anforderung erstellt einen neuen Datenschutzauftrag für die Daten eines einzelnen Kunden im [!DNL Profile] Store. Für den Kunden werden im `userIDs` Array zwei Identitätswerte bereitgestellt. eine mit dem Standard- `Email` Identitäts-Namensraum und die andere mit einem benutzerdefinierten `Customer_ID` Namensraum. It also includes the product value for [!DNL Profile] (`ProfileService`) in the `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Verwenden der UI

When creating job requests in the UI, be sure to select **[!UICONTROL AEP Data Lake]** and/or **[!UICONTROL Profile]** under **[!UICONTROL Products]** in order to process jobs for data stored in the [!DNL Data Lake] or [!DNL Real-time Customer Profile], respectively.

<img src="images/privacy/product-value.png" width="450"><br>

## Fragmente von Profilen in Datenschutzanforderungen {#fragments}

Im [!DNL Profile] Datenspeicher bestehen die personenbezogenen Daten eines einzelnen Kunden oft aus mehreren Profil-Fragmenten, die über das Identitätsdiagramm mit der Person verknüpft sind. Bei Datenschutzanforderungen an den [!DNL Profile] Store ist zu beachten, dass Anforderungen nur auf der Ebene des Profils und nicht des gesamten Profils verarbeitet werden.

Betrachten Sie zum Beispiel eine Situation, in der Sie Kundenattributdaten in drei separaten Datensätzen speichern, die unterschiedliche IDs verwenden, um diese Daten mit einzelnen Kunden zu verknüpfen:

| Datensatzname | Primär-Identitätsfeld | Gespeicherte Attribute |
| --- | --- | --- |
| Datensatz 1 | `customer_id` | `address` |
| Datensatz 2 | `email_id` | `firstName`, `lastName` |
| Datensatz 3 | `email_id` | `mlScore` |

Einer der Datensätze verwendet `customer_id` den primären Bezeichner, während die anderen beiden verwenden `email_id`. Wenn Sie eine Datenschutzanforderung (Zugriff oder Löschen) nur `email_id` als Benutzer-ID-Wert senden möchten, werden nur die Attribute `firstName`, `lastName`und `mlScore` Attribute verarbeitet, ohne dass dies davon betroffen `address` wäre.

Um sicherzustellen, dass Ihre Datenschutzanforderungen alle relevanten Kundenattribute verarbeiten, müssen Sie die primären Identitätswerte für alle anwendbaren Datensätze angeben, in denen diese Attribute gespeichert werden können (bis zu neun IDs pro Kunde). Weitere Informationen zu Schemas, die häufig als Identitäten gekennzeichnet werden, finden Sie im Abschnitt zu Identitätsfeldern in den [Grundlagen der -Komposition](../xdm/schema/composition.md#identity) .

>[!NOTE]
>
>Wenn Sie verschiedene [Sandboxen](../sandboxes/home.md) verwenden, um Ihre [!DNL Profile] Daten zu speichern, müssen Sie für jede Sandbox eine separate Datenschutzanfrage stellen, die den entsprechenden Sandbox-Namen in der `x-sandbox-name` Kopfzeile angibt.

## Verarbeitung von Löschanfragen

When [!DNL Experience Platform] receives a delete request from [!DNL Privacy Service], [!DNL Platform] sends confirmation to [!DNL Privacy Service] that the request has been received and affected data has been marked for deletion. Sobald der Datenschutzauftrag abgeschlossen ist, werden die Datensätze aus dem [!DNL Data Lake] oder [!DNL Profile] Store entfernt. Während der Löschauftrag noch verarbeitet wird, werden die Daten weich gelöscht und stehen daher keinem [!DNL Platform] Dienst zur Verfügung. Weitere Informationen zum Verfolgen von Auftragsstatus finden Sie in der [[!DNL Privacy Service] Dokumentation](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>Bei einer erfolgreichen Löschanforderung werden zwar die erfassten Attributdaten eines Kunden (oder einer Gruppe von Kunden) entfernt, die Anforderung entfernt jedoch nicht die im Identitätsdiagramm festgelegten Verknüpfungen.
>
>Eine Löschanforderung, die beispielsweise die eines Kunden verwendet `email_id` und alle unter diesen IDs gespeicherten Attributdaten `customer_id` entfernt. Alle Daten, die danach unter dem gleichen Element erfasst werden, `customer_id` werden jedoch weiterhin mit dem entsprechenden verknüpft, `email_id`da die Verbindung noch besteht.

In future releases, [!DNL Platform] will send confirmation to [!DNL Privacy Service] after data has been physically deleted.

## Nächste Schritte

By reading this document, you have been introduced to the important concepts involved with processing privacy requests in [!DNL Experience Platform]. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanforderungen für nicht von [!DNL Platform] Ihnen verwendete [!DNL Profile]Ressourcen finden Sie im Dokument zur Verarbeitung von [Datenschutzanfragen im Data Lake](../catalog/privacy.md).