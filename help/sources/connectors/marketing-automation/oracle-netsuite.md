---
title: Übersicht über Oracle NetSuite Source
description: Erfahren Sie, wie Sie Oracle NetSuite mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2024-01-30T00:00:00Z
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 10%

---

# [!DNL Oracle NetSuite]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten in Marketing-Automatisierungssystemen von Drittanbietern. Der Support für Anbieter von Marketing-Automatisierung umfasst [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) ist eine Cloud-basierte Business-Management-Suite, die ERP-/Finanz-, CRM- und E-Commerce-Lösungen umfasst.

Sie können zwei verschiedene Quellen verwenden, um Daten von [!DNL Oracle NetSuite] in Experience Platform aufzunehmen:

* Verwenden Sie die [!DNL Oracle NetSuite Activities], um Ereignisdaten aufzunehmen.
* Verwenden Sie die [!DNL Oracle NetSuite Entities], um Kunden- und Kontaktdaten aufzunehmen.

In der folgenden Tabelle finden Sie weitere Informationen zu den beiden [!DNL Oracle NetSuite].

| Quelle | Typ | Beschreibung |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Ereignis | Rufen Sie geplante Aktivitäten ab, die Ihrem Kalender hinzugefügt wurden. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kundin bzw. Kunde | Rufen Sie bestimmte Kundendaten ab, einschließlich Details wie Kundennamen, Adressen und Schlüsselkennungen. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kontakt | Abrufen von Kontaktnamen, E-Mails, Telefonnummern und allen benutzerdefinierten Kontaktfeldern, die mit Kunden verknüpft sind. |

## Zulassungsliste von IP-Adressen {#ip-allow-list}

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre [!DNL Oracle NetSuite] Daten in Experience Platform übertragen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* **Ein [!DNL Oracle NetSuite]-Konto**.
   * Wenden Sie sich an [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml), wenn Sie noch kein gültiges Konto haben.
* Ein **aktives Abonnement** für ein beliebiges [!DNL Oracle NetSuite].
* Eine **Konto-ID**.
   * Die [!DNL Oracle NetSuite] verwendet OAuth 2.0 für die Kommunikation mit den [!DNL Oracle NetSuite]-APIs. Wenn Sie Ihre Konto-ID nicht haben, lesen Sie die [!DNL Oracle]-Dokumentation unter [So rufen Sie Ihre Konto-ID ab](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Eine **Client-ID** und **Client-Geheimnis** Kombination.
   * Für den Zugriff auf [!DNL Oracle NetSuite] APIs sind die Client-ID und das Client-Geheimnis erforderlich. In diesem Schritt müssen Sie auch sicherstellen, dass Ihr Administrator über Folgendes verfügt:
      * Die OAuth 2.0-Funktion wurde aktiviert und die entsprechenden OAuth 2.0-Rollen wurden eingerichtet.
      * Benutzende wurden den OAuth 2.0-Rollen zugewiesen und die erforderlichen Integrationsdatensätze erstellt.
* Ein **Zugriffstoken** und ein **Aktualisierungstoken**.
   * Informationen zum Generieren Ihrer Zugriffs[!DNL Oracle] und Aktualisierungs-Token finden Sie im [&#x200B; zu &#x200B;](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)OAuth 2.0 Authorization Code Grant Flow.

### Sammeln erforderlicher Anmeldedaten {#gather-credentials}

Um [!DNL Oracle NetSuite] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Der Client-ID-Wert, der beim Erstellen des Integrationsdatensatzes in [!DNL Oracle NetSuite] generiert wird. Weitere Informationen finden Sie im [!DNL Oracle] zum [&#x200B; von &#x200B;](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)-Einträgen . | `7fce.....b42f`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| Client-Geheimnis | Der Client-Geheimniswert, der beim Erstellen des Integrationsdatensatzes generiert wird. Weitere Informationen finden Sie im [!DNL Oracle] zum [&#x200B; von &#x200B;](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)-Einträgen . | `5c98.....1b46`<br>Der Wert ist eine Zeichenfolge mit 64 Zeichen. |
| URL für den Autorisierungstest | (Optional) Ihre URL für den [!DNL NetSuite]-Autorisierungstest. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Zugriffs-Token | Das Zugriffstoken hat das JSON Web Token (JWT)-Format und ist nur 60 Minuten lang gültig. Weitere Informationen zum Abrufen Ihres Zugriffs-Tokens finden Sie im [!DNL Oracle] zu [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, formatiert als JSON Web Token (JWT). |
| Token aktualisieren | Verwenden Sie die Aktualisierung, um nach Ablauf Ihres Zugriffstokens ein neues Zugriffstoken zu generieren. Das Aktualisierungs-Token ist sieben Tage lang gültig. Weitere Informationen zum Abrufen Ihres Zugriffs-Tokens finden Sie im [!DNL Oracle] zu [OAuth 2.0-Autorisierung für NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Der Wert ist eine Zeichenfolge mit 1024 Zeichen, formatiert als JSON Web Token (JWT). |
| Zugriffstoken-URL | Der Token-Endpunkt, an den die Anwendung die POST-Anfragen sendet. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Nachdem ein Aktualisierungs-Token abgelaufen ist, müssen Sie in Experience Platform ein neues Konto mit Ihren aktualisierten Token erstellen.

## Verbinden von [!DNL Oracle NetSuite Activities] mit Experience Platform {#oracle-netsuite-activities}

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Oracle NetSuite Activities] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL Oracle NetSuite Activities]  mithilfe von APIs in Experience Platform zu &#x200B;](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Verbinden Ihres - [!DNL Oracle NetSuite Activities]  mit Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Erstellen eines Datenflusses für eine Quellverbindung mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).

## Verbinden von [!DNL Oracle NetSuite Entities] mit Experience Platform {#oracle-netsuite-entities}

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Oracle NetSuite Entities] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL Oracle NetSuite Entities]  mithilfe von APIs in Experience Platform zu &#x200B;](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Verbinden Ihres - [!DNL Oracle NetSuite Entities]  mit Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Erstellen eines Datenflusses für eine Quellverbindung mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
