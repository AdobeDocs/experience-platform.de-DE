---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Source übermitteln
description: Das folgende Dokument beschreibt die Schritte zum Testen und Überprüfen einer neuen Quelle mithilfe der Flow Service-API und zum Integrieren einer neuen Quelle über Selbstbedienungsquellen (Batch-SDK).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 16%

---

# Übermitteln Ihrer Quelle

Der letzte Schritt bei der Integration Ihrer neuen -Quelle in Adobe Experience Platform mithilfe von Selbstbedienungsquellen (Batch-SDK) besteht darin, Ihre -Quelle zur Überprüfung zu testen. Nach erfolgreicher Veröffentlichung können Sie Ihre neue Quelle übermitteln, indem Sie sich an Ihren Adobe-Support-Mitarbeiter wenden.

Im folgenden Dokument erfahren Sie, wie Sie Ihre Quelle mit der [[!DNL Flow Service] API) testen und ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

* Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).
* Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
* Informationen zum Einrichten von [!DNL Postman] für Platform-APIs finden Sie im Tutorial zum Einrichten [ Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).
* Um Ihren Test- und Debugging-Prozess zu unterstützen, laden Sie die [Sammlung und Umgebung für die Selbstbedienungsquellen-Verifizierung hier herunter](../assets/sdk-verification.zip) und führen Sie die folgenden Schritte aus.

## Testen der Quelle

Um Ihre Quelle zu testen, müssen Sie die Sammlung und Umgebung [Selbstbedienungsquellen-Überprüfung](../assets/sdk-verification.zip) auf [!DNL Postman] ausführen und dabei die entsprechenden Umgebungsvariablen angeben, die sich auf Ihre Quelle beziehen.

Um mit dem Testen zu beginnen, müssen Sie zunächst die Sammlung und die Umgebung in [!DNL Postman] einrichten. Geben Sie als Nächstes die Verbindungsspezifikations-ID an, die Sie testen möchten.

### `authSpecName` angeben

Nachdem Sie Ihre Verbindungsspezifikations-ID eingegeben haben, müssen Sie die `authSpecName` angeben, die Sie für Ihre Basisverbindung verwenden. Je nach Auswahl kann dies entweder `OAuth 2 Refresh Code` oder `Basic Authentication` sein. Nachdem Sie Ihre `authSpecName` angegeben haben, müssen Sie die erforderlichen Anmeldeinformationen in Ihre Umgebung einbeziehen. Wenn Sie beispielsweise `authSpecName` als `OAuth 2 Refresh Code` angeben, müssen Sie die erforderlichen Anmeldeinformationen für OAuth 2 angeben, die `host` und `accessToken` sind.

### `sourceSpec` angeben

Nachdem Sie die Parameter Ihrer Authentifizierungsspezifikation hinzugefügt haben, müssen Sie die erforderlichen Eigenschaften aus Ihrer Quellspezifikation hinzufügen. Die erforderlichen Eigenschaften finden Sie in `sourceSpec.spec.properties`. Im folgenden [!DNL MailChimp Members] Beispiel ist nur die Eigenschaft `listId` erforderlich, d. h. `listId` und der entsprechende ID-Wert für Ihre [!DNL Postman].

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Sobald Ihre Authentifizierungs- und Quellspezifikationsparameter angegeben wurden, können Sie mit dem Ausfüllen des Rests Ihrer Umgebungsvariablen beginnen. Siehe dazu die nachstehende Tabelle:

>[!NOTE]
>
>Alle folgenden Beispielvariablen sind Platzhalterwerte, die Sie aktualisieren müssen, mit Ausnahme von `flowSpecificationId` und `targetConnectionSpecId`, bei denen es sich um feste Werte handelt.

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `x-api-key` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Weitere Informationen zum Abrufen [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `x-api-key`&quot;. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und ihren Mitgliedern Zugang gewähren kann. Anweisungen zum Abrufen Ihrer `x-gw-ims-org-id` finden [ im Tutorial zum Einrichten  [!DNL Postman]](../../../landing/postman.md) Entwicklerkonsole und . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Das zum Abschließen von Aufrufen an Experience Platform-APIs erforderliche Autorisierungs-Token. Weitere Informationen zum Abrufen [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `authorizationToken`&quot;. | `Bearer authorizationToken` |
| `schemaId` | Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Die eindeutige Version, die Ihrem Schema entspricht. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Die `meta:altId`, die zusammen mit dem `schemaId` beim Erstellen eines neuen Schemas zurückgegeben wird. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mit Zuordnungssätzen lässt sich definieren, wie Daten in einem Quellschema den Daten eines Zielschemas zugeordnet werden sollen. Ausführliche Anweisungen zum Erstellen einer Zuordnung finden Sie im Tutorial zum Erstellen [ Zuordnungssatzes mithilfe der API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Die eindeutige ID, die Ihrem Zuordnungssatz entspricht. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. Dies ist die ID, die Sie nach dem Erstellen [ neuen Verbindungsspezifikation generiert ](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Die Flussspezifikations-ID von `RestStorageToAEP`. **Dies ist ein fester**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | Die Zielverbindungs-ID des Data Lake, in dem die aufgenommenen Daten landen. **Dies ist ein fester**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Das vorgesehene Zeitintervall, das bei der Überprüfung auf den Abschluss eines Flussdurchgangs einzuhalten ist. | `40` |
| `startTime` | Die vorgesehene Startzeit für Ihren Datenfluss. Die Startzeit muss in Unix-Zeit formatiert sein. | `1597784298` |

Nachdem Sie alle Umgebungsvariablen bereitgestellt haben, können Sie mit der Ausführung der Sammlung über die [!DNL Postman] beginnen. Klicken Sie in der [!DNL Postman] auf die Auslassungspunkte (**…**) neben [!DNL Sources SSSs Verification Collection] und wählen Sie **Sammlung ausführen**.

![Runner](../assets/runner.png)

Die [!DNL Runner] Benutzeroberfläche wird angezeigt, über die Sie die Ausführungsreihenfolge Ihres Datenflusses konfigurieren können. Wählen **SSS-Verifizierungssammlung ausführen**, um die Sammlung auszuführen.

>[!NOTE]
>
>Sie können **Fluss löschen** in der Checkliste für die Ausführungsreihenfolge deaktivieren, wenn Sie das Dashboard zur Quellenüberwachung in der Platform-Benutzeroberfläche verwenden möchten. Nachdem Sie jedoch mit dem Testen fertig sind, müssen Sie sicherstellen, dass Ihre Testflüsse gelöscht werden.

![run-collection](../assets/run-collection.png)

## Übermitteln Ihrer Quelle

Sobald Ihre Quelle den gesamten Workflow abschließen kann, können Sie sich an Ihren Adobe-Support-Mitarbeiter wenden und Ihre Quelle zur Integration übermitteln.
