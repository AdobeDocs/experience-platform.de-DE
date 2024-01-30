---
title: Oracle NetSuite-Quellübersicht
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Oracle NetSuite und Adobe Experience Platform herstellen.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 21%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>Die [!DNL Oracle NetSuite]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Erfassung von Daten von Drittanbieter-Marketingautomatisierungssystemen. Der Support für Anbieter von Marketing-Automatisierung umfasst [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) ist eine Cloud-basierte Business-Management-Suite, die ERP/Finanz-, CRM- und E-Commerce-Lösungen umfasst.

Sie können zwei verschiedene Quellen verwenden, um Daten aus [!DNL Oracle NetSuite] auf Experience Platform:

* Verwenden Sie die [!DNL Oracle NetSuite Activities] -Quelle, um Ereignisdaten zu erfassen.
* Verwenden Sie die [!DNL Oracle NetSuite Entities] Quelle, um Kunden- und Kontaktdaten zu erfassen.

Weitere Informationen zu den beiden [!DNL Oracle NetSuite] Quellen.

| Quelle | Typ | Beschreibung |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Ereignis | Rufen Sie geplante Aktivitäten ab, die Ihrem Kalender hinzugefügt wurden. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kundin bzw. Kunde | Rufen Sie bestimmte Kundendaten ab, einschließlich Details wie Kundennamen, Adressen und Schlüsselkennungen. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kontakt | Rufen Sie Kontaktnamen, E-Mails, Telefonnummern und alle benutzerdefinierten Kontaktfelder ab, die mit Kunden verknüpft sind. |

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL Oracle NetSuite] -Daten an Experience Platform übermitteln, müssen Sie zunächst sicherstellen, dass Sie über Folgendes verfügen:

* **Ein [!DNL Oracle NetSuite] account**.
   * Kontakt [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) wenn Sie noch kein gültiges Konto haben.
* Ein **Aktives Abonnement** auf [!DNL Oracle NetSuite] Produkt.
* Ein **Konto-ID**.
   * Die [!DNL Oracle NetSuite] -Quelle verwendet OAuth 2.0 zur Kommunikation mit der [!DNL Oracle NetSuite] APIs. Wenn Sie nicht über Ihre Konto-ID verfügen, besuchen Sie die [!DNL Oracle] Dokumentation zu [Abrufen Ihrer Konto-ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **Client-ID** und **Client-Geheimnis** kombinieren.
   * Die Client-ID und das Client-Geheimnis sind für den Zugriff erforderlich. [!DNL Oracle NetSuite] APIs. Während dieses Schritts müssen Sie außerdem sicherstellen, dass Ihr Administrator über Folgendes verfügt:
      * Aktivierung der OAuth 2.0-Funktion und Einrichtung der entsprechenden OAuth 2.0-Rollen.
      * Benutzer den OAuth 2.0-Rollen zugewiesen und die erforderlichen Integrationsdatensätze erstellt.
* Ein **Zugriffstoken** und **Aktualisierungstoken**.
   * Siehe Abschnitt [!DNL Oracle] Handbuch zu [OAuth 2.0 Authorization Code Grant Flow](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) für Informationen zum Generieren Ihrer Zugriffs- und Aktualisierungstoken.

### Sammeln erforderlicher Anmeldeinformationen {#gather-credentials}

Um eine Verbindung zwischen [!DNL Oracle NetSuite] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Der Client-ID-Wert, der beim Erstellen des Integrationsdatensatzes in [!DNL Oracle NetSuite]. Lesen Sie die [!DNL Oracle] Anleitung zum [Integrationsdatensätze erstellen](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) für weitere Informationen. | `7fce.....b42f`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| Client-Geheimnis | Der Client-Geheimwert, der beim Erstellen des Integrationsdatensatzes generiert wird. Lesen Sie die [!DNL Oracle] Anleitung zum [Integrationsdatensätze erstellen](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) für weitere Informationen. | `5c98.....1b46`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| Autorisierungstest-URL | (Optional) Ihre [!DNL NetSuite] Autorisierungstest-URL. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Zugriffstoken | Das Zugriffstoken weist das JSON-Web-Token-Format (JWT) auf und ist nur 60 Minuten gültig. Weitere Informationen zum Abrufen Ihres Zugriffstokens finden Sie unter [!DNL Oracle] Handbuch zu [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, die als JSON-Web-Token (JWT) formatiert ist. |
| Aktualisierungstoken | Verwenden Sie die Aktualisierung , um ein neues Zugriffstoken zu generieren, nachdem Ihr Zugriffstoken abgelaufen ist. Das Aktualisierungs-Token ist sieben Tage lang gültig. Weitere Informationen zum Abrufen Ihres Zugriffstokens finden Sie unter [!DNL Oracle] Handbuch zu [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, die als JSON-Web-Token (JWT) formatiert ist. |
| Zugriffstoken-URL | Der Token-Endpunkt, an den die POST Anfragen sendet. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Nachdem ein Aktualisierungstoken abläuft, müssen Sie ein neues Konto in Experience Platform mit Ihren aktualisierten Token erstellen.

## Verbinden von [!DNL Oracle NetSuite Activities] mit Platform {#oracle-netsuite-activities}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Oracle NetSuite Activities] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL Oracle NetSuite Activities] Daten an Platform mithilfe von APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Verbinden Sie [!DNL Oracle NetSuite Activities] Konto für Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Erstellen eines Datenflusses für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).

## Verbinden von [!DNL Oracle NetSuite Entities] mit Platform {#oracle-netsuite-entities}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Oracle NetSuite Entities] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL Oracle NetSuite Entities] Daten an Platform mithilfe von APIs](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Verbinden Sie [!DNL Oracle NetSuite Entities] Konto für Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Erstellen eines Datenflusses für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
