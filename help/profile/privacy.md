---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Kundenprofil
type: Documentation
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, die entsprechend diversen Datenschutzbestimmungen auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten. In diesem Dokument werden wesentliche Konzepte bei der Verarbeitung von Datenschutzanfragen für das Echtzeit-Kundenprofil behandelt.
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
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Profildatenspeicher in Experience Platform stellen. Wenn Sie auch Datenschutzanfragen für den Data Lake von Platform beabsichtigen, lesen Sie zusätzlich zu diesem Tutorial [ Handbuch ](../catalog/privacy.md) Verarbeitung von Datenschutzanfragen im Data Lake .
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>Die Datenschutzanfrage in diesem Handbuch **nicht** B2B-Nicht-Personen-Entitäten.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden [!DNL Platform] voraus:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [[!DNL Real-Time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service] verwendet **Identitäts-Namespaces**, um durch die Verknüpfung der Identitätswerte mit ihrem Ursprungssystem einen Kontext zu den Werten bereitzustellen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) sein oder die Identität einer bestimmten Anwendung zuordnen, wie z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Identity Service verwaltet einen Speicher global definierter (standardmäßiger) und benutzerdefinierter Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/features/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Real-Time Customer Profile] mithilfe der [!DNL Privacy Service]-API oder -Benutzeroberfläche stellen. Bevor Sie diese Abschnitte lesen, sollten Sie die Dokumentation zur [Privacy Service-API](../privacy-service/api/getting-started.md) oder zur [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) lesen. Diese Dokumente enthalten vollständige Schritte zum Senden eines Datenschutzauftrags, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anfrage-Payloads.

>[!IMPORTANT]
>
>Privacy Service kann [!DNL Profile] Daten nur mithilfe einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszuordnung durchführt. Weitere Informationen finden Sie im Abschnitt [Einschränkungen ](#merge-policy-limitations) Zusammenführungsrichtlinien“.
>
>Beachten Sie, dass Datenschutzanfragen innerhalb der regulatorischen Anforderungen asynchron verarbeitet werden und die Dauer bis zum Abschluss variieren kann. Wenn Änderungen an Ihren [!DNL Profile] Daten auftreten, während eine Anfrage noch verarbeitet wird, ist nicht garantiert, dass diese eingehenden Datensätze auch in dieser Anfrage verarbeitet werden. Es werden nur Profile gelöscht, die zum Zeitpunkt der Anforderung des Datenschutzauftrags im Data Lake oder Profilspeicher gespeichert sind. Wenn Sie Profildaten im Zusammenhang mit dem Betreff einer Löschanfrage während des Löschvorgangs aufnehmen, ist nicht garantiert, dass alle Profilfragmente gelöscht werden.
>Es liegt in Ihrer Verantwortung, zum Zeitpunkt einer Löschanfrage über eingehende Daten in Platform oder im Profil-Service Bescheid zu wissen, da diese Daten in Ihre Datensatzspeicher eingefügt werden. Sie müssen bei der Aufnahme von Daten, die gelöscht wurden oder werden, vorsichtig sein.

### Verwenden der API

Beim Erstellen von Vorgangsanfragen in der API müssen alle IDs innerhalb von `userIDs` über einen spezifischen `namespace` und `type` verfügen. Für den `namespace`-Wert muss ein gültiger, von [!DNL Identity Service] erkannter [Identitäts-Namespace](#namespaces) bereitgestellt werden, während der `type` entweder `standard` (für Standard-Namespaces) oder `unregistered` (für benutzerdefinierte Namespaces) sein muss.

>[!NOTE]
>
>Je nach Identitätsdiagramm und der Art und Weise, wie Ihre Profilfragmente in Platform-Datensätzen verteilt werden, müssen Sie möglicherweise mehr als eine ID für jeden Kunden angeben. Weitere Informationen finden Sie [ nächsten Abschnitt ](#fragments)Profilfragmente“.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Um die mit einer Identität verknüpften Profildaten zu löschen, muss das Array den Wert `ProfileService` enthalten. Um die Identitätsdiagramm-Zuordnungen des Kunden zu löschen, muss das Array den Wert `identity` enthalten.

>[!NOTE]
>
>Weitere Informationen zu den Auswirkungen [ Verwendung von `ProfileService` und `identity` innerhalb des `include`-Arrays finden Sie ](#profile-v-identity) Abschnitt zu Profilanfragen und Identitätsanfragen weiter unten in diesem Dokument.

Die folgende Anfrage erstellt einen neuen Datenschutzauftrag für die Daten eines einzelnen Kunden im [!DNL Profile]. Im `userIDs`-Array werden zwei Identitätswerte für den Kunden bereitgestellt; einer davon verwendet den standardmäßigen Identity-Namespace von `Email` und der andere einen benutzerdefinierten Namespace von `Customer_ID`. Sie enthält auch den Produktwert für [!DNL Profile] (`ProfileService`) im `include`-Array:

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

Für den Profil-Service wird nach Abschluss des Datenschutzauftrags eine Antwort im JSON-Format mit Informationen zu den angeforderten Benutzer-IDs zurückgegeben.

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

Wählen Sie beim Erstellen von Vorgangsanfragen in der Benutzeroberfläche **[!UICONTROL AEP Data Lake]** und/oder **[!UICONTROL Profile]** unter **[!UICONTROL Produkte]** aus, um Vorgänge für Daten zu verarbeiten, die im Data Lake bzw. [!DNL Real-Time Customer Profile] gespeichert sind.

![Eine Zugriffsanfrage wird in der Benutzeroberfläche erstellt, wobei die Profiloption unter „Produkte“ ausgewählt ist](./images/privacy/product-value.png)

## Profilfragmente in Datenschutzanfragen {#fragments}

Im [!DNL Profile] Datenspeicher bestehen die personenbezogenen Daten für einen einzelnen Kunden häufig aus mehreren Profilfragmenten, die über das Identitätsdiagramm mit der Person verknüpft sind. Beachten Sie bei Datenschutzanfragen an den [!DNL Profile], dass Anfragen nur auf der Ebene der Profilfragmente und nicht im gesamten Profil verarbeitet werden.

Betrachten Sie beispielsweise eine Situation, in der Sie Kundenattributdaten in drei separaten Datensätzen speichern, die verschiedene Kennungen verwenden, um diese Daten mit einzelnen Kunden zu verknüpfen:

| Datensatzname | Feld „Primärer Identitätswert“ | Gespeicherte Attribute |
| --- | --- | --- |
| Datensatz 1 | `customer_id` | `address` |
| Datensatz 2 | `email_id` | `firstName`, `lastName` |
| Datensatz 3 | `email_id` | `mlScore` |

Einer der Datensätze verwendet `customer_id` als primäre Kennung, während die beiden anderen `email_id` verwenden. Wenn Sie eine Datenschutzanfrage (Zugriff oder Löschen) nur mit `email_id` als Benutzer-ID-Wert senden, werden nur die Attribute `firstName`, `lastName` und `mlScore` verarbeitet, während `address` nicht betroffen sind.

Um sicherzustellen, dass Ihre Datenschutzanfragen alle relevanten Kundenattribute verarbeiten, müssen Sie die primären Identitätswerte für alle entsprechenden Datensätze angeben, in denen diese Attribute gespeichert werden können (bis zu neun IDs pro Kunde). Siehe Abschnitt zu Identitätsfeldern in den [Grundlagen der Schemakomposition](../xdm/schema/composition.md#identity) für weitere Informationen zu Feldern, die häufig als Identitäten markiert sind.

## Verarbeitung von Löschanfragen {#delete}

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann entfernt, sobald der Datenschutzauftrag abgeschlossen ist.

>[!IMPORTANT]
>
>Anfragen zum Löschen von Datenschutzanfragen werden nicht sofort gestellt und können je nach den betroffenen Services und anderen relevanten Faktoren wie dem geografischen Standort variieren. Der Zeitrahmen für den Abschluss von Datenschutzaufträgen kann zwischen 15 und 45 Tagen betragen, ist jedoch nicht garantiert.

Je nachdem, ob Sie in Ihrer Datenschutzanfrage für Profil (`ProfileService`) auch Identity Service (`identity`) und den Data Lake (`aepDataLake`) als Produkte einbezogen haben, werden verschiedene Datensätze, die sich auf das Profil beziehen, zu möglicherweise unterschiedlichen Zeiten aus dem System entfernt:

| Enthaltene Produkte | Effekte |
| --- | --- |
| Nur `ProfileService` | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten aufgenommen werden. Die mit dem Profil verknüpften Daten verbleiben ebenfalls im Data Lake. |
| `ProfileService` und `identity` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Die mit dem Profil verknüpften Daten verbleiben im Data Lake. |
| `ProfileService` und `aepDataLake` | Das Profil wird sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das Identitätsdiagramm des Profils bleibt jedoch erhalten und das Profil kann möglicherweise rekonstruiert werden, wenn neue Daten mit denselben Identitäten aufgenommen werden.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten vorläufig gelöscht und stehen somit keinem [!DNL Platform]-Service mehr zur Verfügung. Sobald der Auftrag abgeschlossen ist, werden die Daten vollständig aus dem Data Lake entfernt. |
| `ProfileService`, `identity` und `aepDataLake` | Das Profil und das zugehörige Identitätsdiagramm werden sofort gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten vorläufig gelöscht und stehen somit keinem [!DNL Platform]-Service mehr zur Verfügung. Sobald der Auftrag abgeschlossen ist, werden die Daten vollständig aus dem Data Lake entfernt. |

Weitere Informationen zum Verfolgen [[!DNL Privacy Service]  Auftragsstatus finden ](../privacy-service/home.md#monitor) in der Dokumentation .

### Profilanfragen versus Identitätsanfragen {#profile-v-identity}

Wenn eine Löschanfrage für Profil (`ProfileService`), aber nicht für Identity Service (`identity`) gestellt wird, entfernt der resultierende Auftrag die erfassten Attributdaten für einen Kunden (oder eine Reihe von Kunden), aber nicht die im Identitätsdiagramm eingerichteten Verknüpfungen.

Beispiel: Eine Löschanfrage, die die `email_id` eines Kunden verwendet und `customer_id` alle Attributdaten entfernt, die unter diesen IDs gespeichert sind. Alle Daten, die anschließend unter demselben `customer_id` aufgenommen werden, werden jedoch weiterhin mit dem entsprechenden `email_id` verknüpft, da die Verknüpfung noch besteht.

Um das Profil und alle Identitätszuordnungen für einen bestimmten Kunden zu entfernen, stellen Sie sicher, dass Sie sowohl Profil als auch Identity Service als Zielprodukte in Ihre Löschanfragen einbeziehen.

### Einschränkungen bei Zusammenführungsrichtlinien {#merge-policy-limitations}

Privacy Service kann [!DNL Profile] Daten nur mithilfe einer Zusammenführungsrichtlinie verarbeiten, die keine Identitätszuordnung durchführt. Wenn Sie die Benutzeroberfläche verwenden, um zu bestätigen, ob Ihre Datenschutzanfragen verarbeitet werden, stellen Sie sicher, dass Sie eine Richtlinie mit **[!DNL None]** als Typ „ID[!UICONTROL Zuordnung] verwenden. Mit anderen Worten: Sie können keine Zusammenführungsrichtlinie verwenden, bei der [!UICONTROL ID-Zuordnung] auf &quot;[!UICONTROL  Diagramm“ ] ist.

>![Die ID-Zuordnung der Zusammenführungsrichtlinie ist auf „Keine“ festgelegt](./images/privacy/no-id-stitch.png)

## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu den wichtigsten Konzepten bei der Verarbeitung von Datenschutzanfragen in [!DNL Experience Platform] erhalten. Lesen Sie die in diesem Handbuch bereitgestellte Dokumentation, um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanfragen für [!DNL Platform] Ressourcen, die nicht von [!DNL Profile] verwendet werden, finden [ im Dokument zur Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md).
