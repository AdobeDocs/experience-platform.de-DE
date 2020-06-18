---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Couchbase-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# Erstellen eines Couchbase-Quellconnectors in der Benutzeroberfläche

> [!NOTE]
> Der Couchbase-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Source Connectors [!DNL Adobe Experience Platform] bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines Couchbase-Quellconnectors über die [!DNL Platform] Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten [!DNL Platform]:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Zusammensetzung](../../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige Couchbase-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zur [Konfiguration eines Datenflusses](../../dataflow/databases.md)fortfahren.

### Erforderliche Berechtigungen erfassen

Um den Couchbase-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die zum Herstellen einer Verbindung mit Ihrer Couchbase-Instanz verwendet wird. Das Verbindungszeichenfolgen-Muster für Couchbase ist `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in der Dokumentation zur [Couchbase-Verbindung](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Verbinden Sie Ihr Couchbase-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Couchbase-Konto zu erstellen, mit dem eine Verbindung hergestellt werden soll [!DNL Platform].

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den *[!UICONTROL Quellarbeitsbereich]* zuzugreifen. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden eine Reihe von Quellen angezeigt, mit denen Sie ein eingehendes Konto erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse an, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *[!UICONTROL Datenbanken]* &quot;die Option **[!UICONTROL Couchbase]** durch Klicken **auf das Pluszeichen (+)** , um einen neuen Couchbase-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/couchbase/catalog.png)

Die Seite *[!UICONTROL Verbindung zu Couchbase]* herstellen wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie &quot; **[!UICONTROL Neues Konto]**&quot;aus. Geben Sie im angezeigten Eingabedatum einen Namen, eine optionale Beschreibung und Ihre Couchbase-Anmeldeinformationen für die Verbindung ein. Wenn Sie fertig sind, wählen Sie &quot;Mit Quelle **[!UICONTROL verbinden&quot;]** und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das Couchbase-Konto, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann in der rechten oberen Ecke die Option **[!UICONTROL Weiter]** , um fortzufahren.

![existing](../../../../images/tutorials/create/couchbase/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem Couchbase-Konto hergestellt. Sie können jetzt mit dem nächsten Lernprogramm fortfahren und einen Datendurchlauf [konfigurieren, um Daten in die Platform](../../dataflow/databases.md)zu bringen.