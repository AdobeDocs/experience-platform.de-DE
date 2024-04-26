---
title: PathFactory-Quellübersicht
description: Erfahren Sie, wie Sie PathFactory über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 16%

---

# [!DNL PathFactory]

>[!NOTE]
>
>Die [!DNL PathFactory]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

[[!DNL PathFactory]](https://www.pathfactory.com/) bietet eine Cloud-basierte Plattform, die Unternehmen bei der Verwaltung von Journey und der Förderung von Interaktionen durch intelligente Inhaltseinblicke unterstützt. In diesem Handbuch wird beschrieben, wie Sie Daten von PathFactory in Experience Platform integrieren können, indem Sie die Connectoren von PathFactory für eine optimale Datenerfassung verwenden.

Sie können Daten aus [[!DNL PathFactory]](https://www.pathfactory.com/) Verwendung von drei Primärquellen:

* **[!DNL Visitors]**: Erfassen Sie Kunden- und Kontaktdaten als Datensätze, um Ihre Zielgruppe besser zu verstehen.
* **[!DNL Sessions]**: Zeitreihenereignisse, die einzelne Benutzersitzungsaktivitäten auf Ihrer Plattform verfolgen.
* **[!DNL Page Views]**: Zeitreihenereignisse, die Einblicke in die angezeigten Seiten bieten und Ihnen so bei der Analyse der Inhaltsleistung helfen.

Weitere Informationen zur Einrichtung der [!DNL PathFactory] Quellkonto.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie mit der Integration beginnen [[!DNL PathFactory]](https://www.pathfactory.com/) Stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* **A [PathFactory-Konto]**.
   * Kontakt [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) wenn Sie noch kein gültiges Konto haben.
* **Ein aktives Abonnement** auf [!DNL PathFactory] Produkt.
* **Benutzername, Kennwort und Domäne**.
   * Diese Anmeldeinformationen sind für den Zugriff auf Ihre [!DNL PathFactory] -Konto und dessen Daten.
* **Zugriffstoken** und **API-Endpunkte**.
   * Diese sind für die Verbindung mit [!DNL PathFactory] APIs.

### Erhalten von Anmeldedaten und Zugriffstoken {#gather-credentials}

Verbindung herstellen [!DNL PathFactory] zum Experience Platform müssen Sie die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung | Endpunkt |
| --- | --- | --- |
| Benutzername | Ihre [!DNL PathFactory] Benutzername des Kontos. | Nicht zutreffend |
| Kennwort | Ihre [!DNL PathFactory] Kontokennwort. | Nicht zutreffend |
| Domain | Die Ihrer [!DNL PathFactory] -Konto. | Nicht zutreffend |
| Zugriffs-Token | Ein eindeutiges Token für die API-Authentifizierung. | Nicht zutreffend |
| Besucher-Endpunkt | Der API-Endpunkt für Besucherdaten. | `/api/public/v3/data_lake_apis/visitors.json` |
| Sitzungsendpunkt | Der API-Endpunkt für Sitzungsdaten. | `/api/public/v3/data_lake_apis/sessions.json` |
| Seitenansichten-Endpunkt | Der API-Endpunkt für Seitenansichtsdaten. | `/api/public/v3/data_lake_apis/page_views.json` |

Detaillierte Anweisungen zum Abrufen Ihres Benutzernamen, Kennworts, Ihrer Domäne und des Zugriffstokens finden Sie unter [[!DNL PathFactory] Support Center](https://support.pathfactory.com/categories/adobe/). Diese Ressource enthält umfassende Anleitungen zum Abrufen und Verwalten Ihrer Anmeldeinformationen.

### Berechtigungen auf Experience Platform konfigurieren

Sie müssen beide **[!UICONTROL Quellen anzeigen]** und **[!UICONTROL Quellen verwalten]** für Ihr Konto aktivierte Berechtigungen, um Ihre [!DNL PathFactory] -Konto auf Experience Platform. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im Abschnitt [UI-Handbuch zur Zugriffskontrolle](../../../access-control/ui/overview.md).

## Verbinden von [!DNL PathFactory] mit Platform {#pathfactory-connect}

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL PathFactory] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL PathFactory] Daten an Platform mithilfe von APIs](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Verbinden Sie [!DNL PathFactory] Konto für Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Erstellen eines Datenflusses für eine Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
