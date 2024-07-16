---
title: Verbinden Ihres PathFactory-Kontos mit dem Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Benutzeroberfläche Ihr PathFactory-Konto mit Experience Platform verbinden.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 21%

---

# Verbinden Ihres [!DNL PathFactory]-Kontos mit Experience Platform über die Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL PathFactory]-Daten zu Besuchern, Sitzungen und Seitenansichten über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein [!DNL PathFactory] -Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Thema [Bringen von Daten zur Marketing-Automatisierung über die Benutzeroberfläche](../../dataflow/marketing-automation.md) an Experience Platform fortfahren.

### Erforderliche Anmeldedaten sammeln {#gather-credentials}

Um auf Ihr PathFactory-Konto in Platform zuzugreifen, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Benutzername | Der Benutzername Ihres PathFactory-Kontos. Dies ist für die Identifikation Ihres Kontos im System unerlässlich. |
| Kennwort | Das Ihrem PathFactory-Konto zugeordnete Kennwort. Stellen Sie sicher, dass dies geschützt ist, um einen unbefugten Zugriff zu verhindern. |
| Domain | Die mit Ihrem PathFactory-Konto verknüpfte Domäne. Dies bezieht sich normalerweise auf die eindeutige Kennung in Ihrer PathFactory-URL. |
| Zugriffs-Token | Ein eindeutiges Token für die API-Authentifizierung, um eine sichere Kommunikation zwischen Ihren Systemen und PathFactory sicherzustellen. |
| API-Endpunkte | Bestimmte API-Endpunkte für den Zugriff auf Daten: Besucher, Sitzungen und Seitenansichten. Jeder Endpunkt entspricht verschiedenen Datensätzen, die Sie abrufen können. **Hinweis:** Diese sind durch [!DNL PathFactory] vordefiniert und spezifisch für die Daten, auf die Sie zugreifen möchten: <ul><li>**Besucherendpunkt**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sitzungsendpunkt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpunkt &quot;Seitenansichten&quot;**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Ausführliche Anleitungen zum Sichern und Verwenden Ihrer Anmeldeinformationen sowie Informationen zum Abrufen und Aktualisieren Ihres Zugriffstokens finden Sie im [PathFactory Support Center](https://support.pathfactory.com/categories/adobe/). Diese Ressource enthält umfassende Anleitungen zur Verwaltung Ihrer Anmeldedaten und zur Sicherstellung einer effektiven und sicheren API-Integration.


## Verbinden Ihres [!DNL PathFactory]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die von Experience Platform unterstützt werden.

Sie können die gewünschte Kategorie aus der Liste der Kategorien auswählen. Sie können auch die Suchleiste verwenden, um nach einer bestimmten Quelle zu filtern.

Wählen Sie unter der Kategorie [!UICONTROL Marketing-Automatisierung] die Option **[!UICONTROL PathFactory]** und dann **[!UICONTROL Einrichten]** aus.

![Der Quellkatalog mit der ausgewählten PathFactory-Quelle.](../../../../images/tutorials/create/pathfactory/catalog.png)

Die Seite **[!UICONTROL Verbindung zu PathFactory]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto erstellen oder ein vorhandenes Konto verwenden.

### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie einen Namen für Ihr Konto, eine optionale Beschreibung und die Authentifizierungsberechtigungen an, die Ihrem [!DNL PathFactory]-Konto entsprechen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, über die Sie ein neues Konto für PathFactory authentifizieren können.](../../../../images/tutorials/create/pathfactory/new.png)

### Vorhandenes Konto

Wenn Sie bereits über ein vorhandenes Konto verfügen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die vorhandene Kontoschnittstelle, über die Sie aus einer Liste vorhandener PathFactory-Konten auswählen können.](../../../../images/tutorials/create/pathfactory/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PathFactory]-Konto und Experience Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss erstellen, um Ihre Daten zur Marketing-Automatisierung in Experience Platform](../../dataflow/marketing-automation.md) zu importieren.
