---
title: Erstellen einer Zendesk Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Zendesk-Quellverbindung erstellen.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 30%

---

# Erstellen eines Quell-Connectors für [!DNL Zendesk] in der Benutzeroberfläche

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Zendesk]-Quellverbindung mithilfe der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihr [!DNL Zendesk]-Konto in Experience Platform zugreifen zu können, müssen Sie Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Die eindeutige Domain, die für Ihr Konto während des Registrierungsprozesses erstellt wurde. | `yoursubdomain` |
| Zugriffs-Token | Zendesk-API-Token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Zendesk] finden Sie unter [[!DNL Zendesk] Quelle - Übersicht](../../../../connectors/customer-success/zendesk.md).

![Zendesk-API-Token](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Erstellen eines Experience Platform-Schemas für [!DNL Zendesk]

Bevor Sie eine [!DNL Zendesk] Quellverbindung erstellen, müssen Sie auch sicherstellen, dass Sie zunächst ein Experience Platform-Schema erstellen, das für Ihre Quelle verwendet werden soll. Eine ausführliche Anleitung zum Erstellen [ Schemas finden Sie ](../../../../../xdm/schema/composition.md) Tutorial zum Erstellen eines Experience Platform-Schemas .

Weitere Anleitungen zu Ihrem für die [!DNL Zendesk Search API] erforderlichen [!DNL Zendesk] finden Sie im Abschnitt [Beschränkungen](#limits) unten.

![Schema erstellen](../../../../images/tutorials/create/zendesk/schema.png)

## Verbinden Ihres [!DNL Zendesk]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Customer Success* die Option **[!UICONTROL Zendesk]** und dann **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/zendesk/catalog.png)

Die **[!UICONTROL Verbinden eines Zendesk-]**&quot; wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das *Zendesk*-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]** um fortzufahren.

![vorhanden](../../../../images/tutorials/create/zendesk/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/zendesk/new.png)

### Daten auswählen

Nachdem Ihre Quelle authentifiziert wurde, wird die Seite in eine interaktive Schemastruktur aktualisiert, in der Sie die Hierarchie Ihrer Daten untersuchen und überprüfen können. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung zwischen Ihrem [!DNL Zendesk]-Konto und Experience Platform authentifiziert und hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Customer Success-Daten in Experience Platform zu importieren](../../dataflow/customer-success.md).

## Zusätzliche Ressourcen

Die folgenden Abschnitte enthalten zusätzliche Ressourcen, auf die Sie bei Verwendung der [!DNL Zendesk] verweisen können.

### Validierung {#validation}

Im Folgenden wird beschrieben, wie Sie überprüfen können, ob Sie Ihre [!DNL Zendesk] erfolgreich verbunden haben und ob [!DNL Zendesk] Profile in Experience Platform aufgenommen werden.

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Datensätze]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Datensätze] zuzugreifen. Der [!UICONTROL Datensatzaktivität] zeigt die Details der Ausführungen an.

![Aktivitätsseite](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Wählen Sie als Nächstes die Datenflussausführungs-ID des Datenflusses aus, den Sie anzeigen möchten, um spezifische Details zu dieser Datenflussausführung anzuzeigen.

![Datenflussseite](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Wählen Sie abschließend **[!UICONTROL Vorschau des Datensatzes]** aus, um die aufgenommenen Daten anzuzeigen.

![Zendesk-](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Sie können Ihre Experience Platform-Daten auch mit den Daten auf Ihrer Seite [!DNL Zendesk] > [!DNL Customers] vergleichen.

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk-Schema

In der folgenden Tabelle sind die unterstützten Zuordnungen aufgeführt, die für Zendesk eingerichtet werden müssen.

>[!TIP]
>
>Weitere [ zur API finden Sie unter ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)Zendesk-Such-API > Suchergebnisse exportieren.

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

* Die [Zendesk Search-API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) gibt maximal 1.000 Datensätze pro Seite zurück.
   * Der Wert für den ``filter[type]``-Parameter ist auf ``user`` festgelegt, daher gibt die Zendesk-Verbindung nur Benutzer zurück.
   * Die Anzahl der Ergebnisse pro Seite wird vom ``page[size]``-Parameter verwaltet. Der Wert wird auf ``100`` festgelegt. Dies geschieht, um die Auswirkungen der von Zendesk festgelegten Geschwindigkeitsreduzierungsbeschränkungen zu reduzieren.
   * Siehe [Beschränkungen](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) und [Paginierung](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Sie können auch auf &quot;[ durch Listen mithilfe der Cursor-Paginierung“ ](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
