---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Kundenprofil
type: Documentation
description: Adobe Experience Platform Privacy Service verarbeitet Kundenanfragen zum Zugriff auf, zur Abmeldung vom Verkauf oder zur Löschung personenbezogener Daten gemäß den zahlreichen Datenschutzbestimmungen. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Echtzeit-Kundenprofil behandelt.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: d8665a349c6f453d83b64317982f3544bbcde0f7
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 28%

---

# Verarbeitung von Datenschutzanfragen in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden zum Zugriff auf, zur Abmeldung vom Verkauf oder zur Löschung ihrer personenbezogenen Daten gemäß Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und [!DNL California Consumer Privacy Act] (CCPA).

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Real-time Customer Profile] innerhalb von Adobe Experience Platform.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Profildatenspeicher in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Platform Data Lake planen, lesen Sie das Handbuch unter [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md) zusätzlich zu diesem Tutorial.
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

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

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Real-time Customer Profile] mithilfe der [!DNL Privacy Service] API oder Benutzeroberfläche. Bevor Sie diese Abschnitte lesen, wird dringend empfohlen, die [Privacy Service-API](../privacy-service/api/getting-started.md) oder [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) Dokumentation für die vollständigen Schritte zum Senden eines Datenschutzauftrags, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

>[!IMPORTANT]
>
>Privacy Service kann nur verarbeitet werden [!DNL Profile] Daten mit einer Zusammenführungsrichtlinie verwenden, die keine Identitätszuordnung durchführt. Wenn Sie die Benutzeroberfläche verwenden, um zu überprüfen, ob Ihre Datenschutzanfragen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit &quot;[!DNL None]&quot; [!UICONTROL ID-Zuordnung] Typ. Mit anderen Worten, Sie können keine Zusammenführungsrichtlinie verwenden, bei der [!UICONTROL ID-Zuordnung] auf &quot;[!UICONTROL Privates Diagramm]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Beachten Sie außerdem, dass die Dauer, die eine Datenschutzanfrage dauern kann, nicht garantiert werden kann. Wenn Änderungen in Ihrer [!DNL Profile] -Daten, während eine Anforderung noch verarbeitet wird, unabhängig davon, ob diese Datensätze auch verarbeitet werden, nicht garantiert werden können.

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API werden alle in `userIDs` muss eine bestimmte `namespace` und `type`. Eine gültige [Identitäts-Namespace](#namespaces) von [!DNL Identity Service] für die `namespace` -Wert, während die `type` muss entweder `standard` oder `unregistered` (für Standard- bzw. benutzerdefinierte Namespaces).

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Verteilung Ihrer Profilfragmente in Platform-Datensätzen müssen Sie möglicherweise mehr als eine ID für jeden Kunden angeben. Siehe nächsten Abschnitt [Profilfragmente](#fragments) für weitere Informationen.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Wenn Sie Anforderungen an [!DNL Data Lake], muss das Array den Wert &quot;ProfileService&quot;enthalten.

Mit der folgenden Anfrage wird ein neuer Datenschutzauftrag für die Daten eines einzelnen Kunden in der [!DNL Profile] speichern. Zwei Identitätswerte werden für den Kunden im `userIDs` Array; Standard `Email` Identitäts-Namespace und der andere mit einem benutzerdefinierten `Customer_ID` Namespace. Er enthält auch den Produktwert für [!DNL Profile] (`ProfileService`) im `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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

>[!IMPORTANT]
>
>Platform verarbeitet Datenschutzanfragen für alle [Sandboxes](../sandboxes/home.md) , die zu Ihrer Organisation gehören. Daher kann jede `x-sandbox-name` -Kopfzeile, die in der Anfrage enthalten ist, wird vom System ignoriert.

### Verwenden der UI

Wählen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** unter **[!UICONTROL Produkte]** aus, um Aufträge für Daten, die in [!DNL Data Lake] bzw. [!DNL Real-time Customer Profile] gespeichert sind, zu verarbeiten.

<img src="images/privacy/product-value.png" width="450"><br>

## Profilfragmente in Datenschutzanfragen {#fragments}

Im [!DNL Profile] Datenspeicher, bestehen die personenbezogenen Daten eines einzelnen Kunden oft aus mehreren Profilfragmenten, die über das Identitätsdiagramm mit der Person verknüpft sind. Wenn Sie Datenschutzanfragen an die [!DNL Profile] speichern, ist es wichtig zu beachten, dass Anforderungen nur auf Profil-Fragment-Ebene und nicht auf dem gesamten Profil verarbeitet werden.

Angenommen, Sie speichern Kundenattributdaten in drei separaten Datensätzen, die verschiedene Kennungen verwenden, um diese Daten einzelnen Kunden zuzuordnen:

| Datensatzname | Primäres Identitätsfeld | Gespeicherte Attribute |
| --- | --- | --- |
| Datensatz 1 | `customer_id` | `address` |
| Datensatz 2 | `email_id` | `firstName`, `lastName` |
| Datensatz 3 | `email_id` | `mlScore` |

Einer der Datensätze verwendet `customer_id` als primäre Kennung, während die beiden anderen verwenden `email_id`. Wenn Sie eine Datenschutzanfrage (Zugriff oder Löschung) nur mit `email_id` als Benutzer-ID-Wert, wird nur die `firstName`, `lastName`und `mlScore` -Attribute verarbeitet werden, während `address` nicht betroffen sein.

Um sicherzustellen, dass Ihre Datenschutzanfragen alle relevanten Kundenattribute verarbeiten, müssen Sie die primären Identitätswerte für alle relevanten Datensätze angeben, in denen diese Attribute gespeichert werden können (maximal neun IDs pro Kunde). Siehe Abschnitt zu Identitätsfeldern in der [Grundlagen der Schemakomposition](../xdm/schema/composition.md#identity) für weitere Informationen zu Feldern, die häufig als Identitäten markiert sind.

## Verarbeitung von Löschanfragen

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann aus dem [!DNL Data Lake] oder [!DNL Profile] speichern, sobald der Datenschutzauftrag abgeschlossen ist. Während der Löschauftrag noch verarbeitet wird, werden die Daten weich gelöscht und stehen daher keinem der Benutzer zur Verfügung [!DNL Platform] Dienst. Siehe Abschnitt [[!DNL Privacy Service] Dokumentation](../privacy-service/home.md#monitor) für weitere Informationen zum Verfolgen des Auftragsstatus.

>[!IMPORTANT]
>
>Bei einer erfolgreichen Löschanfrage werden die erfassten Attributdaten für einen Kunden (oder eine Gruppe von Kunden) entfernt. Die im Identitätsdiagramm eingerichteten Verknüpfungen werden jedoch durch die Anfrage nicht entfernt.
>
>Beispielsweise eine Löschanfrage, bei der die `email_id` und `customer_id` entfernt alle unter diesen IDs gespeicherten Attributdaten. Alle Daten, die anschließend unter dem gleichen `customer_id` weiterhin mit dem entsprechenden `email_id`, da die Verbindung noch existiert.

In zukünftigen Versionen wird [!DNL Platform] eine Bestätigung an [!DNL Privacy Service] senden, nachdem Daten physisch gelöscht wurden.

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit den wichtigen Konzepten zur Verarbeitung von Datenschutzanfragen in [!DNL Experience Platform]. Wir empfehlen Ihnen, die Dokumentation in diesem Handbuch weiterzulesen, um Ihr Verständnis hinsichtlich der Verwaltung von Identitätsdaten und Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanfragen für [!DNL Platform] nicht verwendete Ressourcen [!DNL Profile], siehe das Dokument unter [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).
