---
title: Verbinden Ihres PathFactory-Kontos mit dem Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Benutzeroberfläche Ihr PathFactory-Konto mit Experience Platform verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 21%

---

# Verbinden Sie [!DNL PathFactory] Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL PathFactory] Daten zu Besuchern, Sitzungen und Seitenansichten über die Benutzeroberfläche an Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine [!DNL PathFactory] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Einbringen von Daten zur Marketing-Automatisierung zum Experience Platform über die Benutzeroberfläche](../../dataflow/marketing-automation.md).

### Erforderliche Anmeldedaten sammeln {#gather-credentials}

Um auf Ihr PathFactory-Konto in Platform zuzugreifen, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Benutzername | Der Benutzername Ihres PathFactory-Kontos. Dies ist für die Identifikation Ihres Kontos im System unerlässlich. |
| Kennwort | Das Ihrem PathFactory-Konto zugeordnete Kennwort. Stellen Sie sicher, dass dies geschützt ist, um einen unbefugten Zugriff zu verhindern. |
| Domain | Die mit Ihrem PathFactory-Konto verknüpfte Domäne. Dies bezieht sich normalerweise auf die eindeutige Kennung in Ihrer PathFactory-URL. |
| Zugriffs-Token | Ein eindeutiges Token für die API-Authentifizierung, um eine sichere Kommunikation zwischen Ihren Systemen und PathFactory sicherzustellen. |
| API-Endpunkte | Bestimmte API-Endpunkte für den Zugriff auf Daten: Besucher, Sitzungen und Seitenansichten. Jeder Endpunkt entspricht verschiedenen Datensätzen, die Sie abrufen können. **Hinweis:** Diese werden vordefiniert durch [!DNL PathFactory] und spezifisch für die Daten sind, auf die Sie zugreifen möchten: <ul><li>**Besucher-Endpunkt**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sitzungsendpunkt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Seitenansichten-Endpunkt**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Eine ausführliche Anleitung zum Sichern und Verwenden Ihrer Anmeldeinformationen sowie Informationen zum Abrufen und Aktualisieren Ihres Zugriffstokens finden Sie unter [PathFactory-Unterstützungszentrum](https://support.pathfactory.com/categories/adobe/). Diese Ressource enthält umfassende Anleitungen zur Verwaltung Ihrer Anmeldedaten und zur Sicherstellung einer effektiven und sicheren API-Integration.


## Verbinden Ihres [!DNL PathFactory]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die von Experience Platform unterstützt werden.

Sie können die gewünschte Kategorie aus der Liste der Kategorien auswählen. Sie können auch die Suchleiste verwenden, um nach einer bestimmten Quelle zu filtern.

Unter dem [!UICONTROL Marketing-Automatisierung] category, select **[!UICONTROL PathFactory]** und wählen Sie **[!UICONTROL Einrichten]**.

![Der Quellkatalog mit der ausgewählten PathFactory-Quelle.](../../../../images/tutorials/create/pathfactory/catalog.png)

Die **[!UICONTROL Mit PathFactory verbinden]** angezeigt. Auf dieser Seite können Sie entweder ein neues Konto erstellen oder ein vorhandenes Konto verwenden.

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie einen Namen für Ihr Konto, eine optionale Beschreibung und die Authentifizierungsberechtigungen an, die Ihrer [!DNL PathFactory] -Konto.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie ein neues Konto für PathFactory authentifizieren können.](../../../../images/tutorials/create/pathfactory/new.png)

### Vorhandenes Konto

Wenn Sie bereits über ein bestehendes Konto verfügen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die vorhandene Kontoschnittstelle, in der Sie aus einer Liste vorhandener PathFactory-Konten auswählen können.](../../../../images/tutorials/create/pathfactory/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PathFactory] Konto und Experience Platform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Ihre Daten zur Marketing-Automatisierung in Experience Platform zu bringen](../../dataflow/marketing-automation.md).
