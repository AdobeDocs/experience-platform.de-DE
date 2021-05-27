---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Kundenprofil
type: Documentation
description: Adobe Experience Platform Privacy Service verarbeitet Kundenanfragen zum Zugriff auf, zur Abmeldung vom Verkauf oder zur Löschung personenbezogener Daten gemäß den zahlreichen Datenschutzbestimmungen. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Echtzeit-Kundenprofil behandelt.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e94482532e0c5698cfe5e51ba260f89c67fa64f0
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 26%

---

# Verarbeitung von Datenschutzanfragen in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten gemäß Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und [!DNL California Consumer Privacy Act] (CCPA).

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Real-time Customer Profile] in Adobe Experience Platform beschrieben.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Profildatenspeicher in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Platform Data Lake planen, lesen Sie zusätzlich zu diesem Tutorial das Handbuch zur Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).[
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Anwendungen finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

## Erste Schritte

Sie sollten über Grundkenntnisse zu folgenden [!DNL Experience Platform]-Services verfügen, bevor Sie dieses Handbuch lesen:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen zusammengeführt werden.
* [[!DNL Real-time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service]**verwendet Identitäts-Namespaces, um einen Kontext zu Identitätswerten bereitzustellen, indem sie mit dem System ihrer Herkunft verknüpft werden.** Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Identity Service verwaltet einen Speicher mit global definierten (standardmäßigen) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten erfahren Sie, wie Sie mithilfe der [!DNL Privacy Service]-API oder -Benutzeroberfläche Datenschutzanfragen für [!DNL Real-time Customer Profile] stellen. Bevor Sie diese Abschnitte lesen, wird dringend empfohlen, die Dokumentation zur [Privacy Service-API](../privacy-service/api/getting-started.md) oder [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) zu lesen, um mehr über die Übermittlung eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

>[!IMPORTANT]
>
>Privacy Service kann [!DNL Profile]-Daten nur mithilfe einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszuordnung vornimmt. Wenn Sie über die Benutzeroberfläche überprüfen möchten, ob Ihre Datenschutzanfragen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit dem Typ [!DNL None] als [!UICONTROL ID-Stitching] verwenden. Mit anderen Worten: Sie können keine Zusammenführungsrichtlinie verwenden, bei der [!UICONTROL ID-Stitching] auf &quot;[!UICONTROL Privates Diagramm]&quot;festgelegt ist.
>
>![](./images/privacy/no-id-stitch.png)
>
>Beachten Sie außerdem, dass die Dauer, die eine Datenschutzanfrage dauern kann, nicht garantiert werden kann. Wenn Änderungen in Ihren [!DNL Profile]-Daten auftreten, während eine Anforderung noch verarbeitet wird, kann auch nicht garantiert werden, ob diese Datensätze verarbeitet werden oder nicht.

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API müssen alle in `userIDs` bereitgestellten IDs einen bestimmten `namespace` und `type` verwenden. Ein gültiger [Identitäts-Namespace](#namespaces), der von [!DNL Identity Service] erkannt wird, muss für den Wert `namespace` angegeben werden, während `type` entweder `standard` oder `unregistered` sein muss (für Standard- bzw. benutzerdefinierte Namespaces).

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Verteilung Ihrer Profilfragmente in Platform-Datensätzen müssen Sie möglicherweise mehr als eine ID für jeden Kunden angeben. Weitere Informationen finden Sie im nächsten Abschnitt [Profilfragmente](#fragments) .

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Bei Anfragen an [!DNL Data Lake] muss das Array den Wert &quot;ProfileService&quot;enthalten.

Die folgende Anfrage erstellt einen neuen Datenschutzauftrag für die Daten eines einzelnen Kunden im [!DNL Profile]-Store. Im Array `userIDs` werden zwei Identitätswerte für den Kunden bereitgestellt. einen, der den standardmäßigen `Email`-Identitäts-Namespace verwendet, und den anderen, der einen benutzerdefinierten `Customer_ID`-Namespace verwendet. Sie enthält auch den Produktwert für [!DNL Profile] (`ProfileService`) im `include`-Array:

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
    "regulation": "ccpa"
}'
```

### Verwenden der UI

Wählen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** unter **[!UICONTROL Produkte]** aus, um Aufträge für Daten, die in [!DNL Data Lake] bzw. [!DNL Real-time Customer Profile] gespeichert sind, zu verarbeiten.

<img src="images/privacy/product-value.png" width="450"><br>

## Profilfragmente in Datenschutzanfragen {#fragments}

Im [!DNL Profile]-Datenspeicher bestehen die personenbezogenen Daten eines einzelnen Kunden häufig aus mehreren Profilfragmenten, die über das Identitätsdiagramm mit der Person verknüpft sind. Bei Datenschutzanfragen an den [!DNL Profile]-Store ist es wichtig zu beachten, dass Anfragen nur auf Profil-Fragment-Ebene und nicht auf dem gesamten Profil verarbeitet werden.

Angenommen, Sie speichern Kundenattributdaten in drei separaten Datensätzen, die verschiedene Kennungen verwenden, um diese Daten einzelnen Kunden zuzuordnen:

| Datensatzname | Primäres Identitätsfeld | Gespeicherte Attribute |
| --- | --- | --- |
| Datensatz 1 | `customer_id` | `address` |
| Datensatz 2 | `email_id` | `firstName`, `lastName` |
| Datensatz 3 | `email_id` | `mlScore` |

Einer der Datensätze verwendet `customer_id` als primäre Kennung, während die anderen beiden `email_id` verwenden. Wenn Sie eine Datenschutzanfrage (Zugriff oder Löschung) mit nur `email_id` als Benutzer-ID-Wert senden möchten, werden nur die Attribute `firstName`, `lastName` und `mlScore` verarbeitet, während `address` nicht betroffen ist.

Um sicherzustellen, dass Ihre Datenschutzanfragen alle relevanten Kundenattribute verarbeiten, müssen Sie die primären Identitätswerte für alle relevanten Datensätze angeben, in denen diese Attribute gespeichert werden können (maximal neun IDs pro Kunde). Weitere Informationen zu Feldern, die häufig als Identitäten markiert sind, finden Sie im Abschnitt zu Identitätsfeldern in den [Grundlagen der Schemakomposition](../xdm/schema/composition.md#identity) .

>[!NOTE]
>
>Wenn Sie zum Speichern Ihrer [!DNL Profile]-Daten unterschiedliche [Sandboxes](../sandboxes/home.md) verwenden, müssen Sie für jede Sandbox eine separate Datenschutzanfrage stellen, die den entsprechenden Sandbox-Namen in der Kopfzeile `x-sandbox-name` angibt.

## Verarbeitung von Löschanfragen

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann aus dem [!DNL Data Lake]- oder [!DNL Profile]-Speicher entfernt, sobald der Datenschutzauftrag abgeschlossen ist. Während der Löschauftrag noch verarbeitet wird, werden die Daten weich gelöscht und stehen daher keinem [!DNL Platform]-Dienst zur Verfügung. Weitere Informationen zum Tracking der Auftragsstatus finden Sie in der [[!DNL Privacy Service] Dokumentation](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>Bei einer erfolgreichen Löschanfrage werden die erfassten Attributdaten für einen Kunden (oder eine Gruppe von Kunden) entfernt. Die im Identitätsdiagramm eingerichteten Verknüpfungen werden jedoch durch die Anfrage nicht entfernt.
>
>Beispielsweise werden bei einer Löschanfrage, bei der `email_id` und `customer_id` eines Kunden verwendet werden, alle unter diesen IDs gespeicherten Attributdaten entfernt. Alle Daten, die anschließend unter dem gleichen `customer_id` erfasst werden, werden jedoch weiterhin mit dem entsprechenden `email_id` verknüpft, da die Verknüpfung noch vorhanden ist.

In zukünftigen Versionen wird [!DNL Platform] eine Bestätigung an [!DNL Privacy Service] senden, nachdem Daten physisch gelöscht wurden.

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit den wichtigen Konzepten zur Verarbeitung von Datenschutzanfragen in [!DNL Experience Platform] vertraut gemacht. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanfragen für [!DNL Platform]-Ressourcen, die nicht von [!DNL Profile] verwendet werden, finden Sie im Dokument zur Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).[
