---
title: PathFactory Source - Überblick
description: Erfahren Sie, wie Sie PathFactory über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 16%

---

# [!DNL PathFactory]

>[!NOTE]
>
>Die [!DNL PathFactory]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

[[!DNL PathFactory]](https://www.pathfactory.com/) bietet eine Cloud-basierte Plattform, mit der Unternehmen Content-Journey verwalten und Interaktionen durch intelligente Inhaltseinblicke fördern können. In diesem Handbuch wird beschrieben, wie Sie Daten von PathFactory in Experience Platform integrieren können, indem Sie die Connectoren von PathFactory für eine optimale Datenerfassung verwenden.

Sie können Daten aus [[!DNL PathFactory]](https://www.pathfactory.com/) mit drei primären Quellen erfassen:

* **[!DNL Visitors]**: Erfassen Sie Kunden- und Kontaktdaten als Datensätze, um Ihre Zielgruppe besser zu verstehen.
* **[!DNL Sessions]**: Zeitreihenereignisse, die einzelne Benutzersitzungsaktivitäten auf Ihrer Plattform verfolgen.
* **[!DNL Page Views]**: Zeitreihenereignisse, die Einblicke in die angezeigten Seiten bieten und Ihnen dabei helfen, die Inhaltsleistung zu analysieren.

Im folgenden Dokument erfahren Sie, wie Sie Ihr [!DNL PathFactory] -Quellkonto einrichten können.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie mit der Integration von [[!DNL PathFactory]](https://www.pathfactory.com/) -Connectoren mit Experience Platform beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* **Ein [PathFactory -Konto]**.
   * Kontaktieren Sie [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) , wenn Sie noch kein gültiges Konto haben.
* **Ein aktives Abonnement** für ein beliebiges [!DNL PathFactory] Produkt.
* **Benutzername, Kennwort und Domäne**.
   * Diese Anmeldedaten sind erforderlich, um auf Ihr [!DNL PathFactory] -Konto und dessen Daten zuzugreifen.
* **Zugriffstoken** und **API-Endpunkte**.
   * Diese sind für die Verbindung mit [!DNL PathFactory] -APIs erforderlich.

### Erhalten von Anmeldedaten und Zugriffstoken {#gather-credentials}

Um [!DNL PathFactory] mit Experience Platform zu verbinden, müssen Sie die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung | Endpunkt |
| --- | --- | --- |
| Benutzername | Ihr [!DNL PathFactory] -Konto-Benutzername. | Nicht zutreffend |
| Kennwort | Ihr [!DNL PathFactory] Kontokennwort. | Nicht zutreffend |
| Domain | Die mit Ihrem [!DNL PathFactory] -Konto verknüpfte Domäne. | Nicht zutreffend |
| Zugriffs-Token | Ein eindeutiges Token für die API-Authentifizierung. | Nicht zutreffend |
| Besucher-Endpunkt | Der API-Endpunkt für Besucherdaten. | `/api/public/v3/data_lake_apis/visitors.json` |
| Sitzungsendpunkt | Der API-Endpunkt für Sitzungsdaten. | `/api/public/v3/data_lake_apis/sessions.json` |
| Seitenansichten-Endpunkt | Der API-Endpunkt für Seitenansichtsdaten. | `/api/public/v3/data_lake_apis/page_views.json` |

Ausführliche Anweisungen zum Abrufen Ihres Benutzernamen, Passworts, Ihrer Domäne und des Zugriffstokens finden Sie im [[!DNL PathFactory] Support Center](https://support.pathfactory.com/categories/adobe/) . Diese Ressource enthält umfassende Anleitungen zum Abrufen und Verwalten Ihrer Anmeldeinformationen.

### Berechtigungen auf Experience Platform konfigurieren

Sie müssen sowohl über die Berechtigung **[!UICONTROL Quellen anzeigen]** als auch über die Berechtigung **[!UICONTROL Quellen verwalten]** für Ihr Konto verfügen, um Ihr [!DNL PathFactory]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im Benutzerhandbuch zur Zugriffskontrolle [.](../../../access-control/ui/overview.md)

## Verbinden von [!DNL PathFactory] mit Platform {#pathfactory-connect}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL PathFactory] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL PathFactory] Daten mithilfe von APIs an Platform zu bringen](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Verbinden Sie Ihr [!DNL PathFactory] Konto über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/pathfactory.md) mit dem Experience Platform.
* [Erstellen Sie einen Datenfluss für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
