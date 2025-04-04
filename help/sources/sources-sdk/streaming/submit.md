---
title: Testen und Senden der Source
description: Das folgende Dokument beschreibt die Schritte zum Testen und Überprüfen einer neuen Quelle mithilfe der Flow Service-API und zum Integrieren einer neuen Quelle über Selbstbedienungsquellen (Streaming-SDK).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 18%

---

# Testen und Senden der Quelle

>[!NOTE]
>
>Selbstbedienungsquellen-Streaming SDK befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Die letzten Schritte zur Integration Ihrer neuen -Quelle in Adobe Experience Platform mithilfe von Selbstbedienungsquellen (Streaming-SDK) bestehen darin, Ihre neue -Quelle zu testen und zu übermitteln. Nachdem Sie Ihre Verbindungsspezifikation abgeschlossen und die Streaming-Flussspezifikation aktualisiert haben, können Sie mit dem Testen der Funktionalität Ihrer Quelle entweder über die API oder die Benutzeroberfläche beginnen. Bei Erfolg können Sie dann Ihre neue Quelle übermitteln, indem Sie sich an Ihren Adobe-Support-Mitarbeiter wenden.

Im folgenden Dokument erfahren Sie, wie Sie Ihre Quelle mit der [[!DNL Flow Service] API) testen und ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

* Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../landing/api-guide.md).
* Informationen zum Generieren Ihrer Anmeldeinformationen für Experience Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
* Informationen zum Einrichten von [!DNL Postman] für Experience Platform-APIs finden Sie im Tutorial zum [ von Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).
* Um Ihren Test- und Debugging-Prozess zu unterstützen, laden Sie die [Sammlung und Umgebung für die Selbstbedienungsquellen-Verifizierung hier herunter](../assets/sdk-verification.zip) und führen Sie die folgenden Schritte aus.

## Testen der Quelle mithilfe der API

Um Ihre Quelle mithilfe der API zu testen, müssen Sie die Sammlung und Umgebung [Selbstbedienungsquellen-Überprüfung](../assets/sdk-verification.zip) auf [!DNL Postman] ausführen und dabei die entsprechenden Umgebungsvariablen angeben, die sich auf Ihre Quelle beziehen.

Um mit dem Testen zu beginnen, müssen Sie zunächst die Sammlung und die Umgebung in [!DNL Postman] einrichten. Geben Sie als Nächstes die Verbindungsspezifikations-ID an, die Sie testen möchten.

>[!NOTE]
>
>Alle folgenden Beispielvariablen sind Platzhalterwerte, die Sie aktualisieren müssen, mit Ausnahme von `flowSpecificationId` und `targetConnectionSpecId`, bei denen es sich um feste Werte handelt.

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `x-api-key` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Informationen zum Abrufen Ihrer `x-api-key` finden [ im Tutorial zum ](../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und ihren Mitgliedern Zugang gewähren kann. Anweisungen zum Abrufen Ihrer `x-gw-ims-org-id` finden [ im Tutorial zum Einrichten  [!DNL Postman]](../../../landing/postman.md) Entwicklerkonsole und . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Das Autorisierungs-Token, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `authorizationToken` finden [ im Tutorial zum ](../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `Bearer authorizationToken` |
| `schemaId` | Damit die Quelldaten in Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Die eindeutige Version, die Ihrem Schema entspricht. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Die `meta:altId`, die zusammen mit dem `schemaId` beim Erstellen eines neuen Schemas zurückgegeben wird. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mit Zuordnungssätzen lässt sich definieren, wie Daten in einem Quellschema den Daten eines Zielschemas zugeordnet werden sollen. Ausführliche Anweisungen zum Erstellen einer Zuordnung finden Sie im Tutorial zum Erstellen [ Zuordnungssatzes mithilfe der API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Die eindeutige ID, die Ihrem Zuordnungssatz entspricht. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. Dies ist die ID, die Sie nach dem Erstellen [ neuen Verbindungsspezifikation generiert ](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Die Flussspezifikations-ID von `GenericStreamingAEP`. **Dies ist ein fester**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | Die Zielverbindungs-ID des Data Lake, in dem die aufgenommenen Daten landen. **Dies ist ein fester**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Das vorgesehene Zeitintervall, das bei der Überprüfung auf den Abschluss eines Flussdurchgangs einzuhalten ist. | `40` |
| `startTime` | Die vorgesehene Startzeit für Ihren Datenfluss. Die Startzeit muss in Unix-Zeit formatiert sein. | `1597784298` |

Nachdem Sie alle Umgebungsvariablen bereitgestellt haben, können Sie mit der Ausführung der Sammlung über die [!DNL Postman] beginnen. Klicken Sie in der [!DNL Postman] auf die Auslassungspunkte (**…**) neben [!DNL Sources SSSs Verification Collection] und wählen Sie **Sammlung ausführen**.

![Runner](../assets/runner.png)

Die [!DNL Runner] Benutzeroberfläche wird angezeigt, über die Sie die Ausführungsreihenfolge Ihres Datenflusses konfigurieren können. Wählen **SSS-Verifizierungssammlung ausführen**, um die Sammlung auszuführen.

>[!NOTE]
>
>Sie können **Fluss löschen** in der Checkliste für die Ausführungsreihenfolge deaktivieren, wenn Sie das Dashboard zur Quellenüberwachung in der Experience Platform-Benutzeroberfläche verwenden möchten. Nachdem Sie jedoch mit dem Testen fertig sind, müssen Sie sicherstellen, dass Ihre Testflüsse gelöscht werden.

![run-collection](../assets/run-collection.png)

## Testen der Quelle mithilfe der Benutzeroberfläche

Um Ihre Quelle in der Benutzeroberfläche zu testen, navigieren Sie zum Quellkatalog der Sandbox Ihres Unternehmens in der Experience Platform-Benutzeroberfläche. Von hier aus sollte Ihre neue Quelle unter der Kategorie *Streaming“*.

Da Ihre neue Quelle jetzt in Ihrer Sandbox verfügbar ist, müssen Sie dem Quell-Workflow folgen, um die Funktionen zu testen. Wählen Sie zunächst **[!UICONTROL Einrichten]** aus.

![Der Quellkatalog, der die neue Streaming-Quelle anzeigt.](../assets/testing/catalog-test.png)

Der Schritt [!UICONTROL Daten hinzufügen] wird angezeigt. Um zu testen, ob Ihre Quelle Daten streamen kann, verwenden Sie die linke Seite der Schnittstelle, um ([ JSON-Beispieldaten) ](../assets/testing/raw.json.zip). Nach dem Hochladen Ihrer Daten wird auf der rechten Seite der Benutzeroberfläche eine Vorschau der Dateihierarchie Ihrer Daten angezeigt. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Schritt „Daten hinzufügen“ im Quell-Workflow, in dem Sie Ihre Daten vor der Aufnahme hochladen und in der Vorschau anzeigen können.](../assets/testing/add-data-test.png)

Auf der Seite [!UICONTROL Datenflussdetails] können Sie auswählen, ob Sie einen vorhandenen Datensatz oder einen neuen Datensatz verwenden möchten. Während dieses Vorgangs können Sie auch Ihre Daten für die Aufnahme in Profile konfigurieren und Einstellungen wie [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Aufnahme] aktivieren.

Wählen Sie zum Testen **[!UICONTROL Neuer Datensatz]** und geben Sie einen Namen für den Ausgabedatensatz an. In diesem Schritt können Sie auch eine optionale Beschreibung angeben, um weitere Informationen zu Ihrem Datensatz hinzuzufügen. Wählen Sie als Nächstes mithilfe der Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemata im Dropdown-Menü ein Schema zum Zuordnen aus. Nachdem Sie ein Schema ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ im Quell-Workflow.](../assets/testing/dataflow-details-test.png)

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../data-prep/ui/mapping.md)

Nachdem Ihre Quelldaten erfolgreich zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Zuordnungsschritt des Quell-Workflows.](../assets/testing/mapping-test.png)

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt Ihren Kontonamen, den Quelltyp und andere verschiedene Informationen an, die für die von Ihnen verwendete Streaming-Cloud-Speicherquelle spezifisch sind.
* **[!UICONTROL Datensatz zuweisen und Felder zuordnen]**: Zeigt den Zieldatensatz und das Schema an, die Sie für Ihren Datenfluss verwenden.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Quell-Workflows.](../assets/testing/review-test.png)

Schließlich müssen Sie den Streaming-Endpunkt Ihres Datenflusses abrufen. Dieser Endpunkt wird verwendet, um Ihren Webhook zu abonnieren, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann. Um Ihren Streaming-Endpunkt abzurufen, gehen Sie zur Seite [!UICONTROL Datenflussaktivität] des soeben erstellten Datenflusses und kopieren Sie den Endpunkt am unteren Rand des Bedienfelds [!UICONTROL Eigenschaften].

![Der Streaming-Endpunkt in der Datenflussaktivität.](../assets/testing/endpoint-test.png)

## Übermitteln Ihrer Quelle

Sobald Ihre Quelle den gesamten Workflow abschließen kann, können Sie sich an Ihren Adobe-Support-Mitarbeiter wenden und Ihre Quelle zur Integration in anderen Experience Platform-Organisationen übermitteln.
