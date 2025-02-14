---
keywords: Experience Platform;Startseite;beliebte Themen
title: Verarbeitung von Datenschutzanfragen in Identity Service
description: Adobe Experience Platform Privacy Service bearbeitet Anfragen von Kunden, die entsprechend diversen Datenschutzbestimmungen auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Identity Service behandelt.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: a75a5603eacc1b4625a19adfddbb2f4bb81f66d3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 60%

---

# Verarbeiten von Datenschutzanfragen in [!DNL Identity Service]

Der Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden, die entsprechend den Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und dem [!DNL California Consumer Privacy Act] (CCPA) auf ihre personenbezogenen Daten zugreifen, deren Verkauf widersprechen oder sie löschen möchten.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Identity Service] innerhalb von Adobe Experience Platform dargelegt.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen an den Identitätsdatenspeicher in Experience Platform stellen. Wenn Sie außerdem Datenschutzanfragen an Platform Data Lake oder [!DNL Real-Time Customer Profile] beabsichtigen, finden Sie zusätzlich zu diesem Tutorial weitere Informationen im Handbuch [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md) und im Handbuch [Verarbeitung von Datenschutzanfragen für ](../profile/privacy.md)).
>
>Anweisungen zum Ausführen von Datenschutzanfragen für andere Adobe Experience Cloud-Programme finden Sie in der [Privacy Service-Dokumentation](../privacy-service/experience-cloud-apps.md).

## Erste Schritte

Sie sollten über Grundkenntnisse zu folgenden [!DNL Experience Platform]-Services verfügen, bevor Sie dieses Handbuch lesen:

* [[!DNL Privacy Service]](../privacy-service/home.md): Verwaltet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [[!DNL Identity Service]](../identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [[!DNL Real-Time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Identitäts-Namespaces verstehen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] führt Identitätsdaten von Kunden über Systeme und Geräte hinweg zusammen. [!DNL Identity Service] verwendet **Identitäts-Namespaces**, um durch die Verknüpfung der Identitätswerte mit ihrem Ursprungssystem einen Kontext zu den Werten bereitzustellen. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) sein oder die Identität einer bestimmten Anwendung zuordnen, wie z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Identity Service verwaltet einen Speicher global definierter (standardmäßiger) und benutzerdefinierter Identitäts-Namespaces. Standardmäßige Namespaces (z. B. „E-Mail“ und „ECID“) stehen für alle Unternehmen zur Verfügung, während Ihr Unternehmen außerdem benutzerdefinierte Namespaces erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namespaces in [!DNL Experience Platform] finden Sie unter [Identitäts-Namespaces – Übersicht](../identity-service/features/namespaces.md).

## Übermitteln von Anfragen {#submit}

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Identity Service] mithilfe der [!DNL Privacy Service]-API oder -Benutzeroberfläche stellen. Es wird dringend empfohlen, vor der Lektüre dieser Abschnitte die Dokumentation zur [Privacy Service-API](../privacy-service/api/getting-started.md) oder [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) erneut zu lesen, um mehr über alle Schritte zur Übermittlung eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung von Nutzerdaten in Anfrage-Payloads.

### Verwenden der API

Beim Erstellen von Vorgangsanfragen in der API müssen alle IDs innerhalb von `userIDs` über einen spezifischen `namespace` und `type` verfügen. Für den `namespace`-Wert muss ein gültiger, von [!DNL Identity Service] erkannter [Identitäts-Namespace](#namespaces) bereitgestellt werden, während der `type` entweder `standard` (für Standard-Namespaces) oder `unregistered` (für benutzerdefinierte Namespaces) sein muss.

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Bei Anfragen an [!DNL Identity] muss das Array den Wert `Identity` enthalten.

Die folgende Anfrage erstellt einen neuen Datenschutzvorgang gemäß der DSGVO für die Daten eines einzelnen Kunden im [!DNL Identity]-Speicher. Im Array `userIDs` werden zwei Identitätswerte für den Kunden bereitgestellt; einer davon verwendet den standardmäßigen Identity-Namespace `Email` und der andere einen `ECID`-Namespace. Es enthält auch den Produktwert für [!DNL Identity] (`Identity`) im Array :`include`

>[!TIP]
>
>Sie müssen beim Löschen von Identitäten mithilfe der DSGVO das Identitätssymbol als Namespace anstelle des Anzeigenamens angeben.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Verwenden der Benutzeroberfläche

>[!TIP]
>
>Sie müssen beim Löschen von Identitäten mithilfe der DSGVO das Identitätssymbol als Namespace anstelle des Anzeigenamens angeben.

Wählen Sie beim Erstellen von Vorgangsanfragen in der Benutzeroberfläche **[!UICONTROL Identität]** unter **[!UICONTROL Produkte]**, um Vorgänge für Daten zu verarbeiten, die in [!DNL Identity Service] gespeichert sind.

![identity-gdpr](./images/identity-gdpr.png)

## Verarbeitung von Löschanfragen

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Das Löschen einer einzelnen Identität basiert auf dem angegebenen Namespace- und/oder ID-Wert. Darüber hinaus erfolgt der Löschvorgang für alle mit einer bestimmten Organisation verknüpften Sandboxes.

Je nachdem, ob Sie in Ihrer Datenschutzanfrage für Identity Service (`identity`) auch das Echtzeit-Kundenprofil (`ProfileService`) und den Data Lake (`aepDataLake`) als Produkte einbezogen haben, werden verschiedene Datensätze, die sich auf die Identität beziehen, zu möglicherweise unterschiedlichen Zeiten aus dem System entfernt:

| Enthaltene Produkte | Effekte |
| --- | --- |
| Nur `identity` | Die angegebene Identität wird gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das aus diesem Identitätsdiagramm erstellte Profil bleibt weiterhin bestehen, wird jedoch nicht aktualisiert, da neue Daten aufgenommen werden, da die Identitätszuordnungen jetzt entfernt wurden. Die mit dem Profil verknüpften Daten verbleiben ebenfalls im Data Lake. |
| `identity` und `ProfileService` | Die angegebene Identität wird gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Die mit dem Profil verknüpften Daten verbleiben im Data Lake. |
| `identity` und `aepDataLake` | Die angegebene Identität wird gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde. Das aus diesem Identitätsdiagramm erstellte Profil bleibt weiterhin bestehen, wird jedoch nicht aktualisiert, da neue Daten aufgenommen werden, da die Identitätszuordnungen jetzt entfernt wurden.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten vorläufig gelöscht und stehen somit keinem [!DNL Platform]-Service mehr zur Verfügung. Sobald der Auftrag abgeschlossen ist, werden die Daten vollständig aus dem Data Lake entfernt. |
| `identity`, `ProfileService` und `aepDataLake` | Die angegebene Identität wird gelöscht, sobald Platform die Bestätigung sendet, dass die Löschanfrage empfangen wurde.<br><br>Wenn das Data Lake-Produkt antwortet, dass die Anfrage empfangen wurde und derzeit verarbeitet wird, werden die mit dem Profil verknüpften Daten vorläufig gelöscht und stehen somit keinem [!DNL Platform]-Service mehr zur Verfügung. Sobald der Auftrag abgeschlossen ist, werden die Daten vollständig aus dem Data Lake entfernt. |

Weitere Informationen zum Verfolgen [[!DNL Privacy Service]  Auftragsstatus finden ](../privacy-service/home.md#monitor) in der Dokumentation .

## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu den wichtigsten Konzepten bei der Verarbeitung von Datenschutzanfragen in [!DNL Identity Service] erhalten. Informationen zur Verarbeitung von Datenschutzanfragen für andere [!DNL Experience Cloud] finden Sie im Dokument zu [[!DNL Privacy Service] und [!DNL Experience Cloud] Anwendungen](../privacy-service/experience-cloud-apps.md).
