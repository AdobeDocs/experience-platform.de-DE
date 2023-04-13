---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Kundenprofil
type: Documentation
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, die entsprechend diversen Datenschutzbestimmungen auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Echtzeit-Kundenprofil behandelt.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 42e59ba1c7b1980d6633ced264673afcf8d80810
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 26%

---

# Verarbeiten von Datenschutzanfragen in [!DNL Real-Time Customer Profile]

Der Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden, die entsprechend den Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und dem [!DNL California Consumer Privacy Act] (CCPA) auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Real-Time Customer Profile] innerhalb von Adobe Experience Platform dargelegt.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Profildatenspeicher in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Platform Data Lake planen, lesen Sie das Handbuch unter [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md) zusätzlich zu diesem Tutorial.
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Punkte voraus [!DNL Platform] Komponenten:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [[!DNL Real-Time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service] verwendet **Identitäts-Namespaces**, um durch die Verknüpfung der Identitätswerte mit ihrem Ursprungssystem einen Kontext zu den Werten bereitzustellen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) sein oder die Identität einer bestimmten Anwendung zuordnen, wie z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Identity Service verwaltet einen Speicher global definierter (standardmäßiger) und benutzerdefinierter Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Real-Time Customer Profile] mithilfe der [!DNL Privacy Service]-API oder -Benutzeroberfläche stellen. Bevor Sie diese Abschnitte lesen, wird dringend empfohlen, die [Privacy Service-API](../privacy-service/api/getting-started.md) oder [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) Dokumentation für die vollständigen Schritte zum Senden eines Datenschutzauftrags, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

>[!IMPORTANT]
>
>Privacy Service kann nur verarbeitet werden [!DNL Profile] Daten mit einer Zusammenführungsrichtlinie verwenden, die keine Identitätszuordnung durchführt. Siehe Abschnitt zu [Einschränkungen bei Zusammenführungsrichtlinien](#merge-policy-limitations) für weitere Informationen.
>
>Bitte beachten Sie, dass die Dauer des Abschlusses einer Datenschutzanfrage dauern kann **cannot** garantiert werden. Wenn Änderungen in Ihrer [!DNL Profile] -Daten, während eine Anforderung noch verarbeitet wird, unabhängig davon, ob diese Datensätze auch verarbeitet werden, nicht garantiert werden können.

### Verwenden der API

Beim Erstellen von Vorgangsanfragen in der API müssen alle IDs innerhalb von `userIDs` über einen spezifischen `namespace` und `type` verfügen. Für den `namespace`-Wert muss ein gültiger, von [!DNL Identity Service] erkannter [Identitäts-Namespace](#namespaces) bereitgestellt werden, während der `type` entweder `standard` (für Standard-Namespaces) oder `unregistered` (für benutzerdefinierte Namespaces) sein muss.

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Verteilung Ihrer Profilfragmente in Platform-Datensätzen müssen Sie möglicherweise mehr als eine ID für jeden Kunden angeben. Siehe nächsten Abschnitt [Profilfragmente](#fragments) für weitere Informationen.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Um die mit einer Identität verknüpften Profildaten zu löschen, muss das Array den Wert enthalten `ProfileService`. Um die Identitätsdiagrammzuordnungen des Kunden zu löschen, muss das Array den Wert enthalten `identity`.

>[!NOTE]
>
>Siehe Abschnitt zu [Profilanfragen und Identitätsanfragen](#profile-v-identity) Weitere Informationen zu den Auswirkungen der Verwendung von `ProfileService` und `identity` innerhalb der `include` Array.

Mit der folgenden Anfrage wird ein neuer Datenschutzauftrag für die Daten eines einzelnen Kunden in der [!DNL Profile] speichern. Zwei Identitätswerte werden für den Kunden im `userIDs` Array; Standard `Email` Identitäts-Namespace und der andere mit einem benutzerdefinierten `Customer_ID` Namespace. Er enthält auch den Produktwert für [!DNL Profile] (`ProfileService`) im `include` array:

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

Stellen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche sicher, dass Sie **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profil]** under **[!UICONTROL Produkte]** zur Verarbeitung von Aufträgen für Daten, die im Data Lake gespeichert sind, oder [!DNL Real-Time Customer Profile]zurück.

![Eine Zugriffsanfrage, die in der Benutzeroberfläche erstellt wird, wobei die Option Profil unter Produkte ausgewählt ist](./images/privacy/product-value.png)

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

## Verarbeitung von Löschanfragen {#delete}

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann entfernt, sobald der Datenschutzauftrag abgeschlossen ist.

>[!IMPORTANT]
>
>Datenschutzlöschanfragen sind nicht unmittelbar und können je nach betroffenen Diensten und anderen Faktoren, die sich auf den geografischen Standort auswirken, variieren. Der Zeitrahmen für die Fertigstellung von Datenschutzaufträgen kann zwischen 15 und 45 Tagen betragen, ist jedoch nicht garantiert.

Je nachdem, ob Sie auch Identity Service eingeschlossen haben (`identity`) und dem Datensee (`aepDataLake`) als Produkte in Ihrer Datenschutzanfrage für Profil (`ProfileService`), werden verschiedene Datensätze, die sich auf das Profil beziehen, zu unterschiedlichen Zeitpunkten aus dem System entfernt:

| Produkte inbegriffen | Effekte |
| --- | --- |
| `ProfileService` only | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten erfasst werden. Die mit dem Profil verknüpften Daten verbleiben ebenfalls im Data Lake. |
| `ProfileService` und `identity` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Die mit dem Profil verknüpften Daten verbleiben im Data Lake. |
| `ProfileService` und `aepDataLake` | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten erfasst werden.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten weich gelöscht und stehen daher keinem [!DNL Platform] Dienst. Nach Abschluss des Auftrags werden die Daten vollständig aus dem Data Lake entfernt. |
| `ProfileService`, `identity`, und `aepDataLake` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten weich gelöscht und stehen daher keinem [!DNL Platform] Dienst. Nach Abschluss des Auftrags werden die Daten vollständig aus dem Data Lake entfernt. |

Siehe Abschnitt [[!DNL Privacy Service] Dokumentation](../privacy-service/home.md#monitor) für weitere Informationen zum Verfolgen des Auftragsstatus.

### Profilanfragen versus Identitätsanfragen {#profile-v-identity}

Wenn eine Löschanfrage für das Profil erfolgt (`ProfileService`), aber nicht Identity Service (`identity`), entfernt der resultierende Auftrag die erfassten Attributdaten für einen Kunden (oder eine Gruppe von Kunden), entfernt jedoch nicht die im Identitätsdiagramm eingerichteten Verknüpfungen.

Beispielsweise eine Löschanfrage, bei der die `email_id` und `customer_id` entfernt alle unter diesen IDs gespeicherten Attributdaten. Alle Daten, die anschließend unter dem gleichen `customer_id` weiterhin mit dem entsprechenden `email_id`, da die Verbindung noch existiert.

Um das Profil und alle Identitätszuordnungen für einen bestimmten Kunden zu entfernen, stellen Sie sicher, dass Sie sowohl Profil als auch Identity Service als Zielprodukte in Ihre Löschanfragen aufnehmen.

### Einschränkungen von Zusammenführungsrichtlinien {#merge-policy-limitations}

Privacy Service kann nur verarbeitet werden [!DNL Profile] Daten mit einer Zusammenführungsrichtlinie verwenden, die keine Identitätszuordnung durchführt. Wenn Sie über die Benutzeroberfläche überprüfen, ob Ihre Datenschutzanfragen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit **[!DNL None]** als [!UICONTROL ID-Zuordnung] Typ. Mit anderen Worten, Sie können keine Zusammenführungsrichtlinie verwenden, bei der [!UICONTROL ID-Zuordnung] auf [!UICONTROL Privates Diagramm].
>![Die ID-Zuordnung der Zusammenführungsrichtlinie ist auf &quot;Ohne&quot;festgelegt](./images/privacy/no-id-stitch.png)
>
## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu den wichtigsten Konzepten bei der Verarbeitung von Datenschutzanfragen in [!DNL Experience Platform] erhalten. Um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen, lesen Sie bitte weiterhin die Dokumentation in diesem Handbuch.

Informationen zur Verarbeitung von Datenschutzanfragen für [!DNL Platform] nicht verwendete Ressourcen [!DNL Profile], siehe das Dokument unter [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).
