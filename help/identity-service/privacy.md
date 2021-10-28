---
keywords: Experience Platform;Home;beliebte Themen
title: Verarbeitung von Datenschutzanfragen in Identity Service
description: Adobe Experience Platform Privacy Service verarbeitet Kundenanfragen zum Zugriff auf, zur Abmeldung vom Verkauf oder zur Löschung personenbezogener Daten gemäß den zahlreichen Datenschutzbestimmungen. In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für Identity Service behandelt.
source-git-commit: 49f5de6c4711120306bfc3e6759ed4e83e8a19c2
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 38%

---


# Verarbeitung von Datenschutzanfragen in [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] verarbeitet Anfragen von Kunden zum Zugriff auf, zur Abmeldung vom Verkauf oder zur Löschung ihrer personenbezogenen Daten gemäß Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und [!DNL California Consumer Privacy Act] (CCPA).

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanfragen für [!DNL Identity Service] innerhalb von Adobe Experience Platform.

>[!NOTE]
>
>In diesem Handbuch wird nur beschrieben, wie Sie Datenschutzanfragen für den Identitätsdatenspeicher in Experience Platform stellen. Wenn Sie außerdem Datenschutzanfragen für den Platform Data Lake oder [!DNL Real-time Customer Profile], siehe Handbuch zu [Verarbeitung von Datenschutzanfragen im Data Lake](../catalog/privacy.md) und zum Handbuch [Verarbeitung von Datenschutzanfragen für Profil](../profile/privacy.md) zusätzlich zu diesem Tutorial.
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

In den folgenden Abschnitten wird beschrieben, wie Sie Datenschutzanfragen für [!DNL Identity Service] mithilfe der [!DNL Privacy Service] API oder Benutzeroberfläche. Bevor Sie diese Abschnitte lesen, wird dringend empfohlen, die [Privacy Service-API](../privacy-service/api/getting-started.md) oder [Privacy Service-Benutzeroberfläche](../privacy-service/ui/overview.md) Dokumentation für die vollständigen Schritte zum Senden eines Datenschutzauftrags, einschließlich der richtigen Formatierung von Benutzerdaten in Anfrage-Payloads.

### Verwenden der API

Beim Erstellen von Auftragsanfragen in der API werden alle in `userIDs` muss eine bestimmte `namespace` und `type`. Eine gültige [Identitäts-Namespace](#namespaces) von [!DNL Identity Service] für die `namespace` -Wert, während die `type` muss entweder `standard` oder `unregistered` (für Standard- bzw. benutzerdefinierte Namespaces).

Darüber hinaus muss das `include`-Array der Anfrage-Payload die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anfrage gesendet wird. Bei Anforderungen an [!DNL Identity], muss das Array den Wert enthalten. `Identity`.

Die folgende Anfrage erstellt einen neuen Datenschutzauftrag gemäß der DSGVO für die Daten eines einzelnen Kunden in der [!DNL Identity] speichern. Zwei Identitätswerte werden für den Kunden im `userIDs` Array; Standard `Email` Identitäts-Namespace und der andere mit einem `ECID` namespace, es enthält auch den Produktwert für [!DNL Identity] (`Identity`) im `include` array:

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

### Verwenden der UI

Stellen Sie beim Erstellen von Auftragsanfragen in der Benutzeroberfläche sicher, dass Sie **[!UICONTROL Identität]** under **[!UICONTROL Produkte]** zum Verarbeiten von Aufträgen für in gespeicherte Daten [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Verarbeitung von Löschanfragen

Wenn [!DNL Experience Platform] von [!DNL Privacy Service] eine DELETE-Anfrage erhält, sendet [!DNL Platform] eine Bestätigung an [!DNL Privacy Service], dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Das Löschen der einzelnen Identität basiert auf dem angegebenen Namespace- und/oder ID-Wert. Darüber hinaus erfolgt der Löschvorgang für alle Sandboxes, die einer bestimmten IMS-Organisation zugeordnet sind.

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit den wichtigen Konzepten zur Verarbeitung von Datenschutzanfragen in [!DNL Identity Service]. Informationen zur Verarbeitung von Datenschutzanfragen für andere [!DNL Experience Cloud] Anwendungen, siehe das Dokument unter [[!DNL Privacy Service] and [!DNL Experience Cloud] Anwendungen](../privacy-service/experience-cloud-apps.md).