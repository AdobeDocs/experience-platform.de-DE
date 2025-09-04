---
title: Verbinden Ihres PathFactory-Kontos mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr PathFactory-Konto über die Benutzeroberfläche mit Experience Platform verbinden.
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 18%

---

# Verbinden Ihres [!DNL PathFactory] über die Benutzeroberfläche mit Experience Platform

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL PathFactory]-Besucher-, Sitzungs- und Seitenansichtsdaten über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein [!DNL PathFactory]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Übertragen von Daten zur Marketing-Automatisierung in Experience Platform mithilfe der Benutzeroberfläche“ ](../../dataflow/marketing-automation.md).

### Sammeln erforderlicher Anmeldeinformationen {#gather-credentials}

Um auf Ihr PathFactory-Konto in der Experience Platform zuzugreifen, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Benutzername | Benutzername Ihres PathFactory-Kontos. Dies ist für die Identifizierung Ihres Kontos im System unerlässlich. |
| Passwort | Das Ihrem PathFactory-Konto zugeordnete Kennwort. Sicherstellen, dass dieser sicher aufbewahrt wird, um nicht autorisierten Zugriff zu verhindern. |
| Domain | Die Domain, die Ihrem PathFactory-Konto zugeordnet ist. Dies bezieht sich normalerweise auf die eindeutige Kennung in Ihrer PathFactory-URL. |
| Zugriffs-Token | Ein eindeutiges Token, das für die API-Authentifizierung verwendet wird, um eine sichere Kommunikation zwischen Ihren Systemen und PathFactory sicherzustellen. |
| API-Endpunkte | Spezifische API-Endpunkte für den Datenzugriff: Besucher, Sitzungen und Seitenansichten. Jeder Endpunkt entspricht verschiedenen Datensätzen, die Sie abrufen können. **Hinweis:** Diese sind von [!DNL PathFactory] vordefiniert und beziehen sich speziell auf die Daten, auf die Sie zugreifen möchten: <ul><li>**Besucher-Endpunkt**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sessions Endpoint**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Seitenansichten-Endpunkt**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Ausführliche Anleitungen zum Schützen und Verwenden Ihrer Anmeldeinformationen sowie Informationen zum Abrufen und Aktualisieren Ihres Zugriffstokens finden Sie im [PathFactory Support Center](https://support.pathfactory.com/categories/adobe/). Diese Ressource bietet umfassende Anleitungen zum Verwalten Ihrer -Anmeldeinformationen und zur Sicherstellung einer effektiven und sicheren API-Integration.


## Verbinden Ihres [!DNL PathFactory]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die von Experience Platform unterstützt werden.

Sie können die entsprechende Kategorie aus der Liste der Kategorien auswählen. Sie können auch die Suchleiste verwenden, um nach einer bestimmten Quelle zu filtern.

Wählen Sie unter der Kategorie [!UICONTROL Marketing]Automatisierung **[!UICONTROL die Option PathFactory]** und dann **[!UICONTROL Einrichten]**.

![Der Quellkatalog mit der ausgewählten PathFactory-Quelle.](../../../../images/tutorials/create/pathfactory/catalog.png)

Die **[!UICONTROL Verbindung mit PathFactory herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto erstellen oder ein vorhandenes Konto verwenden.

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen für Ihr Konto, eine optionale Beschreibung und die Authentifizierungsdaten an, die mit Ihrem [!DNL PathFactory]-Konto übereinstimmen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie ein neues Konto für PathFactory authentifizieren können.](../../../../images/tutorials/create/pathfactory/new.png)

### Vorhandenes Konto

Wenn Sie bereits über ein vorhandenes Konto verfügen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann aus der angezeigten Liste das Konto aus, das Sie verwenden möchten.

![Die Benutzeroberfläche für vorhandene Konten, in der Sie aus einer Liste vorhandener PathFactory-Konten auswählen können.](../../../../images/tutorials/create/pathfactory/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PathFactory]-Konto und Experience Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Ihre Daten zur Marketing-Automatisierung in Experience Platform zu importieren](../../dataflow/marketing-automation.md).
