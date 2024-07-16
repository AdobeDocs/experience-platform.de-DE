---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Kundenprofil
type: Documentation
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, die entsprechend diversen Datenschutzbestimmungen auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Echtzeit-Kundenprofil behandelt.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 25%

---

# Verarbeiten von Datenschutzanfragen in [!DNL Real-Time Customer Profile]

Der Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden, die entsprechend den Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und dem [!DNL California Consumer Privacy Act] (CCPA) auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Real-Time Customer Profile] innerhalb von Adobe Experience Platform dargelegt.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Profildatenspeicher in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Platform Data Lake planen, lesen Sie zusätzlich zu diesem Tutorial das Handbuch zur Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).[
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>Die Datenschutzanfrage in diesem Handbuch betrifft nicht personenbezogene B2B-Entitäten. **Nicht**

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden [!DNL Platform] -Komponenten voraus:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [[!DNL Real-Time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service] verwendet **Identitäts-Namespaces**, um durch die Verknüpfung der Identitätswerte mit ihrem Ursprungssystem einen Kontext zu den Werten bereitzustellen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) sein oder die Identität einer bestimmten Anwendung zuordnen, wie z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Identity Service verwaltet einen Speicher global definierter (standardmäßiger) und benutzerdefinierter Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/features/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Real-Time Customer Profile] mithilfe der [!DNL Privacy Service]-API oder -Benutzeroberfläche stellen. Bevor Sie diese Abschnitte lesen, sollten Sie die Dokumentation zur [Privacy Service-API](../privacy-service/api/getting-started.md) oder zur [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) lesen oder sich dessen bewusst sein. Diese Dokumente enthalten vollständige Schritte zum Senden eines Datenschutzauftrags, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

>[!IMPORTANT]
>
>Privacy Service kann nur [!DNL Profile] -Daten mithilfe einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszusammenfügung vornimmt. Weitere Informationen finden Sie im Abschnitt zu [Einschränkungen bei Zusammenführungsrichtlinien](#merge-policy-limitations) .
>
>Beachten Sie, dass Datenschutzanfragen asynchron innerhalb der regulatorischen Anforderungen verarbeitet werden. Die Zeit, die diese für die Durchführung benötigen, kann variieren. Wenn Änderungen an Ihren [!DNL Profile] -Daten auftreten, während eine Anfrage noch verarbeitet wird, ist nicht garantiert, dass diese eingehenden Datensätze auch in dieser Anfrage verarbeitet werden. Es wird garantiert, dass nur Profile gelöscht werden, die zum Zeitpunkt der Anforderung des Datenschutzauftrags im Data Lake oder Profilspeicher gespeichert sind. Wenn Sie während des Löschvorgangs Profildaten zum Betreff einer Löschanfrage erfassen, ist nicht garantiert, dass alle Profilfragmente gelöscht werden.
>Es liegt in Ihrer Verantwortung, zum Zeitpunkt einer Löschanfrage alle in Platform oder Profile Service eingehenden Daten zu kennen, da diese Daten in Ihre Datensatzspeicher eingefügt werden. Sie müssen bei der Erfassung von Daten, die gelöscht wurden oder werden, vorsichtig sein.

### Verwenden der API

Beim Erstellen von Vorgangsanfragen in der API müssen alle IDs innerhalb von `userIDs` über einen spezifischen `namespace` und `type` verfügen. Für den `namespace`-Wert muss ein gültiger, von [!DNL Identity Service] erkannter [Identitäts-Namespace](#namespaces) bereitgestellt werden, während der `type` entweder `standard` (für Standard-Namespaces) oder `unregistered` (für benutzerdefinierte Namespaces) sein muss.

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Verteilung Ihrer Profilfragmente in Platform-Datensätzen müssen Sie möglicherweise mehr als eine ID für jeden Kunden angeben. Weitere Informationen finden Sie im nächsten Abschnitt [Profilfragmente](#fragments) .

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Um die mit einer Identität verknüpften Profildaten zu löschen, muss das Array den Wert `ProfileService` enthalten. Um die Identitätsdiagrammzuordnungen des Kunden zu löschen, muss das Array den Wert `identity` enthalten.

>[!NOTE]
>
>Weitere Informationen zu den Auswirkungen der Verwendung von `ProfileService` und `identity` im Array `include` finden Sie im Abschnitt zu [Profilanfragen und Identitätsanfragen](#profile-v-identity) weiter unten in diesem Dokument.

Die folgende Anfrage erstellt einen neuen Datenschutzauftrag für die Daten eines einzelnen Kunden im [!DNL Profile] -Store. Im Array `userIDs` werden zwei Identitätswerte für den Kunden bereitgestellt: einer mit dem standardmäßigen Identitäts-Namespace `Email` und der andere mit einem benutzerdefinierten Namespace `Customer_ID`. Er enthält auch den Produktwert für [!DNL Profile] (`ProfileService`) im Array `include` :

**Anfrage**

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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform verarbeitet Datenschutzanfragen für alle [Sandboxes](../sandboxes/home.md), die zu Ihrer Organisation gehören. Daher wird jede `x-sandbox-name`-Kopfzeile, die in der Anfrage enthalten ist, vom System ignoriert.

**Produktantwort**

Beim Profil-Service wird nach Abschluss des Datenschutzauftrags eine Antwort im JSON-Format mit Informationen zu den angeforderten Benutzer-IDs zurückgegeben.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### Verwenden der Benutzeroberfläche

Stellen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche sicher, dass Sie unter **[!UICONTROL Produkte]** die Option **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** auswählen, um Aufträge für Daten zu verarbeiten, die im Data Lake bzw. in [!DNL Real-Time Customer Profile] gespeichert sind.

![Eine Zugriffsanfrage, die in der Benutzeroberfläche erstellt wird, wobei die Option Profil unter Produkte ausgewählt ist](./images/privacy/product-value.png)

## Profilfragmente in Datenschutzanfragen {#fragments}

Im [!DNL Profile] -Datenspeicher bestehen die personenbezogenen Daten eines einzelnen Kunden häufig aus mehreren Profilfragmenten, die über das Identitätsdiagramm mit der Person verknüpft sind. Bei Datenschutzanfragen an den [!DNL Profile] -Store ist es wichtig zu beachten, dass Anfragen nur auf der Ebene der Profilfragmente und nicht auf dem gesamten Profil verarbeitet werden.

Angenommen, Sie speichern Kundenattributdaten in drei separaten Datensätzen, die verschiedene Kennungen verwenden, um diese Daten einzelnen Kunden zuzuordnen:

| Datensatzname | Feld „Primärer Identitätswert“ | Gespeicherte Attribute |
| --- | --- | --- |
| Datensatz 1 | `customer_id` | `address` |
| Datensatz 2 | `email_id` | `firstName`, `lastName` |
| Datensatz 3 | `email_id` | `mlScore` |

Einer der Datensätze verwendet `customer_id` als primäre Kennung, während die anderen beiden `email_id` verwenden. Wenn Sie eine Datenschutzanfrage (Zugriff oder Löschung) nur mit `email_id` als Benutzer-ID-Wert senden sollten, werden nur die Attribute `firstName`, `lastName` und `mlScore` verarbeitet, während `address` nicht betroffen ist.

Um sicherzustellen, dass Ihre Datenschutzanfragen alle relevanten Kundenattribute verarbeiten, müssen Sie die primären Identitätswerte für alle relevanten Datensätze angeben, in denen diese Attribute gespeichert werden können (maximal neun IDs pro Kunde). Weitere Informationen zu Feldern, die üblicherweise als Identitäten markiert sind, finden Sie im Abschnitt zu Identitätsfeldern in den [Grundlagen der Schemakomposition](../xdm/schema/composition.md#identity) .

## Verarbeitung von Löschanfragen {#delete}

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann entfernt, sobald der Datenschutzauftrag abgeschlossen ist.

>[!IMPORTANT]
>
>Datenschutzlöschanfragen sind nicht unmittelbar und können je nach betroffenen Diensten und anderen Faktoren, die sich auf den geografischen Standort auswirken, variieren. Der Zeitrahmen für die Fertigstellung von Datenschutzaufträgen kann zwischen 15 und 45 Tagen betragen, ist jedoch nicht garantiert.

Je nachdem, ob Sie auch Identity Service (`identity`) und den Data Lake (`aepDataLake`) als Produkte in Ihrer Datenschutzanfrage nach Profil (`ProfileService`) aufgenommen haben, werden verschiedene mit dem Profil verknüpfte Datensätze zu unterschiedlichen Zeitpunkten aus dem System entfernt:

| Produkte inbegriffen | Effekte |
| --- | --- |
| Nur `ProfileService` | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten erfasst werden. Die mit dem Profil verknüpften Daten verbleiben ebenfalls im Data Lake. |
| `ProfileService` und `identity` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Die mit dem Profil verknüpften Daten verbleiben im Data Lake. |
| `ProfileService` und `aepDataLake` | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten erfasst werden.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten weich gelöscht und stehen daher keinem [!DNL Platform]-Dienst zur Verfügung. Nach Abschluss des Auftrags werden die Daten vollständig aus dem Data Lake entfernt. |
| `ProfileService`, `identity` und `aepDataLake` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten weich gelöscht und stehen daher keinem [!DNL Platform]-Dienst zur Verfügung. Nach Abschluss des Auftrags werden die Daten vollständig aus dem Data Lake entfernt. |

Weitere Informationen zum Tracking der Auftragsstatus finden Sie in der [[!DNL Privacy Service] Dokumentation](../privacy-service/home.md#monitor) .

### Profilanfragen versus Identitätsanfragen {#profile-v-identity}

Wenn eine Löschanfrage für Profil (`ProfileService`), aber nicht für Identity Service (`identity`) durchgeführt wird, entfernt der resultierende Auftrag die erfassten Attributdaten für einen Kunden (oder eine Gruppe von Kunden), entfernt jedoch nicht die im Identitätsdiagramm eingerichteten Verknüpfungen.

Beispielsweise entfernt eine Löschanfrage, die die `email_id` und `customer_id` eines Kunden verwendet, alle unter diesen IDs gespeicherten Attributdaten. Alle Daten, die anschließend unter dem gleichen `customer_id` erfasst werden, werden jedoch weiterhin mit dem entsprechenden `email_id` verknüpft, da die Zuordnung noch vorhanden ist.

Um das Profil und alle Identitätszuordnungen für einen bestimmten Kunden zu entfernen, stellen Sie sicher, dass Sie sowohl Profil als auch Identity Service als Zielprodukte in Ihre Löschanfragen aufnehmen.

### Einschränkungen von Zusammenführungsrichtlinien {#merge-policy-limitations}

Privacy Service kann nur [!DNL Profile] -Daten mithilfe einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszusammenfügung vornimmt. Wenn Sie über die Benutzeroberfläche überprüfen möchten, ob Ihre Datenschutzanfragen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit dem Typ [!UICONTROL ID-Zusammenfügung] mit **[!DNL None]** verwenden. Mit anderen Worten: Sie können keine Zusammenführungsrichtlinie verwenden, bei der [!UICONTROL ID-Stitching] auf [!UICONTROL Privates Diagramm] festgelegt ist.

>![Die ID-Zuordnung der Zusammenführungsrichtlinie ist auf &quot;None&quot;](./images/privacy/no-id-stitch.png) festgelegt

## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu den wichtigsten Konzepten bei der Verarbeitung von Datenschutzanfragen in [!DNL Experience Platform] erhalten. Um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen, lesen Sie weiterhin die Dokumentation in diesem Handbuch.

Informationen zur Verarbeitung von Datenschutzanfragen für [!DNL Platform] -Ressourcen, die nicht von [!DNL Profile] verwendet werden, finden Sie im Dokument zur Verarbeitung von Datenschutzanfragen im Data Lake [.](../catalog/privacy.md)
