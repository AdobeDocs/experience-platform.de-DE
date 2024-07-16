---
title: Oracle NetSuite Source - Überblick
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Oracle NetSuite und Adobe Experience Platform herstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 22%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>Die [!DNL Oracle NetSuite]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Erfassung von Daten von Drittanbieter-Marketingautomatisierungssystemen. Der Support für Anbieter von Marketing-Automatisierung umfasst [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) ist eine Cloud-basierte Business Management Suite, die ERP/Finanz-, CRM- und E-Commerce-Lösungen umfasst.

Sie können zwei verschiedene Quellen verwenden, um Daten von [!DNL Oracle NetSuite] zu Experience Platform zu erfassen:

* Verwenden Sie die Quelle [!DNL Oracle NetSuite Activities] , um Ereignisdaten zu erfassen.
* Verwenden Sie die Quelle [!DNL Oracle NetSuite Entities] , um Kunden- und Kontaktdaten aufzunehmen.

In der folgenden Tabelle finden Sie weitere Informationen zu den beiden [!DNL Oracle NetSuite] -Quellen.

| Quelle | Typ | Beschreibung |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Ereignis | Rufen Sie geplante Aktivitäten ab, die Ihrem Kalender hinzugefügt wurden. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kundin bzw. Kunde | Rufen Sie bestimmte Kundendaten ab, einschließlich Details wie Kundennamen, Adressen und Schlüsselkennungen. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kontakt | Rufen Sie Kontaktnamen, E-Mails, Telefonnummern und alle benutzerdefinierten Kontaktfelder ab, die mit Kunden verknüpft sind. |

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL Oracle NetSuite] -Daten auf Experience Platform bringen können, müssen Sie zunächst sicherstellen, dass Sie über Folgendes verfügen:

* **Ein [!DNL Oracle NetSuite] Konto**.
   * Kontaktieren Sie [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) , wenn Sie noch kein gültiges Konto haben.
* Ein **aktives Abonnement** für ein beliebiges [!DNL Oracle NetSuite] Produkt.
* Eine **Konto-ID**.
   * Die Quelle [!DNL Oracle NetSuite] verwendet OAuth 2.0 zur Kommunikation mit den [!DNL Oracle NetSuite] -APIs. Wenn Sie nicht über Ihre Konto-ID verfügen, lesen Sie die [!DNL Oracle] -Dokumentation unter [ , wie Sie Ihre Konto-ID abrufen](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Eine Kombination aus **Client-ID** und **Client-Geheimnis** .
   * Für den Zugriff auf [!DNL Oracle NetSuite] -APIs sind die Client-ID und das Client-Geheimnis erforderlich. Während dieses Schritts müssen Sie außerdem sicherstellen, dass Ihr Administrator über Folgendes verfügt:
      * Aktivierung der OAuth 2.0-Funktion und Einrichtung der entsprechenden OAuth 2.0-Rollen.
      * Benutzer den OAuth 2.0-Rollen zugewiesen und die erforderlichen Integrationsdatensätze erstellt.
* Ein **Zugriffstoken** und ein **Aktualisierungstoken**.
   * Informationen zum Generieren von Zugriffs- und Aktualisierungstoken finden Sie im Leitfaden [!DNL Oracle] unter [OAuth 2.0 Authorization Code Grant Flow](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) .

### Sammeln erforderlicher Anmeldeinformationen {#gather-credentials}

Um eine Verbindung zwischen [!DNL Oracle NetSuite] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Der Client-ID-Wert, der beim Erstellen des Integrationsdatensatzes in [!DNL Oracle NetSuite] generiert wird. Weitere Informationen finden Sie im Leitfaden [!DNL Oracle] , in dem beschrieben wird, wie Sie [Integrationsdatensätze erstellen](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) . | `7fce.....b42f`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| Client-Geheimnis | Der Client-Geheimwert, der beim Erstellen des Integrationsdatensatzes generiert wird. Weitere Informationen finden Sie im Leitfaden [!DNL Oracle] , in dem beschrieben wird, wie Sie [Integrationsdatensätze erstellen](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) . | `5c98.....1b46`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| Autorisierungstest-URL | (Optional) Ihre Test-URL für die [!DNL NetSuite]-Autorisierung. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Zugriffs-Token | Das Zugriffstoken weist das JSON-Web-Token-Format (JWT) auf und ist nur 60 Minuten gültig. Weitere Informationen zum Abrufen Ihres Zugriffs-Tokens finden Sie im [!DNL Oracle]-Handbuch zur [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, die als JSON-Web-Token (JWT) formatiert ist. |
| Token aktualisieren | Verwenden Sie die Aktualisierung , um ein neues Zugriffstoken zu generieren, nachdem Ihr Zugriffstoken abgelaufen ist. Das Aktualisierungs-Token ist sieben Tage lang gültig. Weitere Informationen zum Abrufen Ihres Zugriffs-Tokens finden Sie im [!DNL Oracle]-Handbuch zur [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, die als JSON-Web-Token (JWT) formatiert ist. |
| Zugriffstoken-URL | Der Token-Endpunkt, an den die POST Anfragen sendet. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Nachdem ein Aktualisierungstoken abläuft, müssen Sie ein neues Konto in Experience Platform mit Ihren aktualisierten Token erstellen.

## Verbinden von [!DNL Oracle NetSuite Activities] mit Platform {#oracle-netsuite-activities}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Oracle NetSuite Activities] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL Oracle NetSuite Activities] Daten mithilfe von APIs an Platform zu bringen](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Verbinden Sie Ihr [!DNL Oracle NetSuite Activities] Konto über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) mit dem Experience Platform.
* [Erstellen Sie einen Datenfluss für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).

## Verbinden von [!DNL Oracle NetSuite Entities] mit Platform {#oracle-netsuite-entities}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Oracle NetSuite Entities] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL Oracle NetSuite Entities] Daten mithilfe von APIs an Platform zu bringen](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Verbinden Sie Ihr [!DNL Oracle NetSuite Entities] Konto über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) mit dem Experience Platform.
* [Erstellen Sie einen Datenfluss für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
