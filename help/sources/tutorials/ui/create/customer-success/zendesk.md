---
keywords: Experience Platform;Zendesk;Quellen;Connectoren;Quell-Connectoren;Sources SDK;SDK;SDK;Zendesk;Zendesk
title: Erstellen einer Zendesk-Quellverbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Zendesk-Quellverbindung erstellen.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 36%

---

# (Beta) Erstellen Sie eine [!DNL Zendesk] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Zendesk]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen – Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Quellen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Zendesk] Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Zendesk] -Konto in Platform angeben, müssen Sie Werte für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Die eindeutige Domäne, die für Ihr Konto spezifisch ist, das während des Registrierungsprozesses erstellt wurde. | `yoursubdomain` |
| Zugriffstoken | Zendesk-API-Token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Zendesk] -Quelle, siehe [[!DNL Zendesk] Quellübersicht](../../../../connectors/customer-success/zendesk.md).

![Zendesk-API-Token](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Erstellen eines Platform-Schemas für [!DNL Zendesk]

Vor der Erstellung [!DNL Zendesk] -Quellverbindung erstellen, müssen Sie außerdem sicherstellen, dass Sie zunächst ein Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Siehe Tutorial zu [Erstellen eines Platform-Schemas](../../../../../xdm/schema/composition.md) für umfassende Schritte zum Erstellen eines Schemas.

Zusätzliche Anleitungen zu Ihrer [!DNL Zendesk] -Schema, das für die [!DNL Zendesk Search API], siehe [limits](#limits) unten.

![Schema erstellen](../../../../images/tutorials/create/zendesk/schema.png)

## Verbinden Ihres [!DNL Zendesk]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *Kundenerfolg* category, select **[!UICONTROL Zendesk]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/zendesk/catalog.png)

Die **[!UICONTROL Zendesk-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die *Zendesk* Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/zendesk/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/zendesk/new.png)

### Daten auswählen

Sobald Ihre Quelle authentifiziert ist, wird die Seite in eine interaktive Schemastruktur aktualisiert, in der Sie die Hierarchie Ihrer Daten untersuchen und untersuchen können. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Zendesk]-Konto und Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Kundenerfolgsdaten in Platform zu bringen](../../dataflow/customer-success.md).

## Weitere Ressourcen

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei der Verwendung der Variablen [!DNL Zendesk] -Quelle.

### Validierung {#validation}

In den folgenden Schritten wird beschrieben, wie Sie überprüfen können, ob Sie Ihre [!DNL Zendesk] und [!DNL Zendesk] Profile werden in Platform erfasst.

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Datensätze]** über die linke Navigationsleiste auf [!UICONTROL Datensätze] Arbeitsbereich. Die [!UICONTROL Datensatzaktivität] zeigt die Details der Ausführungen an.

![Aktivitätsseite](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Wählen Sie anschließend die Datenfluss-Start-ID des Datenflusses aus, den Sie anzeigen möchten, um bestimmte Details zu diesem Datenfluss anzuzeigen.

![Dataflow-Seite](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Vorschau des Datensatzes anzeigen]** , um die erfassten Daten anzuzeigen.

![Zendesk-Datensatz](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Sie können Ihre Platform-Daten auch anhand der Daten auf Ihrer [!DNL Zendesk] > [!DNL Customers] Seite.

![zendesk-Customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für Zendesk eingerichtet werden müssen.

>[!TIP]
>
>Siehe [Zendesk Search API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) für weitere Informationen zur API.

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

{style=&quot;table-layout:auto&quot;}

### Beschränkungen {#limits}

* Die [Zendesk Search API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) gibt maximal 1.000 Datensätze pro Seite zurück.
   * Der Wert für ``filter[type]`` -Parameter auf ``user`` und daher gibt die Zendesk-Verbindung nur Benutzer zurück.
   * Die Anzahl der Ergebnisse pro Seite wird von der ``page[size]`` Parameter. Der Wert wird auf ``100``. Dies geschieht, um die Auswirkungen der von Zendesk festgelegten Geschwindigkeitsbegrenzungen zu reduzieren.
   * Siehe [Beschränkungen](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) und [Paginierung](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Weitere Informationen finden Sie unter [Paginieren durch Listen mit der Cursor-Paginierung](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
