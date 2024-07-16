---
title: Erstellen einer Zendesk-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Zendesk-Quellverbindung erstellen.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 35%

---

# Erstellen eines Quell-Connectors für [!DNL Zendesk] in der Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen einer 0-Quell-Verbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.[!DNL Zendesk]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihr [!DNL Zendesk] -Konto in Platform zugreifen zu können, müssen Sie Werte für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Die eindeutige Domäne, die für Ihr Konto spezifisch ist, das während des Registrierungsprozesses erstellt wurde. | `yoursubdomain` |
| Zugriffs-Token | Zendesk-API-Token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Zendesk]-Quelle finden Sie in der [[!DNL Zendesk] Quellübersicht](../../../../connectors/customer-success/zendesk.md).

![Zendesk-API-Token](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Erstellen eines Platform-Schemas für [!DNL Zendesk]

Bevor Sie eine [!DNL Zendesk]-Quellverbindung erstellen, müssen Sie außerdem sicherstellen, dass Sie zunächst ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Umfassende Schritte zum Erstellen eines Schemas finden Sie im Tutorial zum Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) .[

Weitere Anleitungen zum [!DNL Zendesk]-Schema, das für [!DNL Zendesk Search API] erforderlich ist, finden Sie im Abschnitt [limits](#limits) unten.

![Schema erstellen](../../../../images/tutorials/create/zendesk/schema.png)

## Verbinden Ihres [!DNL Zendesk]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Customer Success* die Option **[!UICONTROL Zendesk]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/zendesk/catalog.png)

Die Seite **[!UICONTROL Zendesk-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das Konto *Zendesk* aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** , um fortzufahren.

![vorhanden](../../../../images/tutorials/create/zendesk/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/zendesk/new.png)

### Daten auswählen

Sobald Ihre Quelle authentifiziert ist, wird die Seite in eine interaktive Schemastruktur aktualisiert, in der Sie die Hierarchie Ihrer Daten untersuchen und untersuchen können. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Zendesk]-Konto und Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss erstellen, um Kundenerfolgsdaten in Platform](../../dataflow/customer-success.md) zu importieren.

## Zusätzliche Ressourcen

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der Quelle [!DNL Zendesk] verweisen können.

### Validierung {#validation}

Im Folgenden werden die Schritte beschrieben, die Sie ausführen können, um zu überprüfen, ob Sie Ihre [!DNL Zendesk]-Quelle erfolgreich verbunden haben und ob [!DNL Zendesk]-Profile in Platform aufgenommen werden.

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Datensätze]** aus, um auf den Arbeitsbereich [!UICONTROL Datensätze] zuzugreifen. Im Bildschirm [!UICONTROL Datensatzaktivität] werden die Details der Ausführungen angezeigt.

![Aktivitätsseite](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Wählen Sie anschließend die Datenfluss-Start-ID des Datenflusses aus, den Sie anzeigen möchten, um bestimmte Details zu diesem Datenfluss anzuzeigen.

![Dataflow page](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Vorschau des Datensatzes anzeigen]** aus, um die erfassten Daten anzuzeigen.

![Zendesk-Datensatz](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Sie können Ihre Platform-Daten auch anhand der Daten auf Ihrer Seite [!DNL Zendesk] > [!DNL Customers] überprüfen.

![zendesk-Customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für Zendesk eingerichtet werden müssen.

>[!TIP]
>
>Weitere Informationen zur API finden Sie unter [Zendesk Search API > Export Search Results](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) .

| Quelle | Typ |
|---|---|
| `results.active` | Boolesch |
| `results.alias` | Zeichenfolge |
| `results.created_at` | Zeichenfolge |
| `results.custom_role_id` | Ganzzahl |
| `results.default_group_id` | Ganzzahl |
| `results.details` | Zeichenfolge |
| `results.email` | Zeichenfolge |
| `results.external_id` | Ganzzahl |
| `results.iana_time_zone` | Zeichenfolge |
| `results.id` | Ganzzahl |
| `results.last_login_at` | Zeichenfolge |
| `results.locale` | Zeichenfolge |
| `results.locale_id` | Ganzzahl |
| `results.moderator` | Boolesch |
| `results.name` | Zeichenfolge |
| `results.notes` | Zeichenfolge |
| `results.only_private_comments` | Boolesch |
| `results.organization_id` | Ganzzahl |
| `results.phone` | Zeichenfolge |
| `results.photo` | Zeichenfolge |
| `results.report_csv` | Boolesch |
| `results.restricted_agent` | Boolesch |
| `results.result_type` | Zeichenfolge |
| `results.role` | Zeichenfolge |
| `results.role_type` | Ganzzahl |
| `results.shared` | Boolesch |
| `results.shared_agent` | Boolesch |
| `results.shared_phone_number` | Boolesch |
| `results.signature` | Zeichenfolge |
| `results.suspended` | Boolesch |
| `results.ticket_restriction` | Zeichenfolge |
| `results.time_zone` | Zeichenfolge |
| `results.two_factor_auth_enabled` | Boolesch |
| `results.updated_at` | Zeichenfolge |
| `results.url` | Zeichenfolge |
| `results.verified` | Boolesch |

{style="table-layout:auto"}

### Beschränkungen {#limits}

* Die [Zendesk-Such-API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) gibt maximal 1.000 Datensätze pro Seite zurück.
   * Der Wert für den Parameter ``filter[type]`` ist auf ``user`` festgelegt und daher gibt die Zendesk-Verbindung nur Benutzer zurück.
   * Die Anzahl der Ergebnisse pro Seite wird vom Parameter ``page[size]`` verwaltet. Der Wert ist auf ``100`` gesetzt. Dies geschieht, um die Auswirkungen der von Zendesk festgelegten Geschwindigkeitsbegrenzungen zu reduzieren.
   * Siehe [Beschränkungen](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) und [Paginierung](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Sie können auch auf [Paginieren durch Listen mit der Cursor-Paginierung](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/) verweisen.
