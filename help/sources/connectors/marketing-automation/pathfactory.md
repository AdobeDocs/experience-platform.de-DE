---
title: Übersicht über PathFactory Source
description: Erfahren Sie, wie Sie PathFactory mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 11%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/) bietet eine Cloud-basierte Plattform, die Unternehmen bei der Verwaltung von Content-Journey und der Förderung von Interaktionen durch intelligente Inhaltserkenntnisse unterstützt. In diesem Handbuch wird beschrieben, wie Sie Daten aus PathFactory in Experience Platform integrieren und dabei die Connectoren von PathFactory für eine optimale Datenaufnahme verwenden können.

Sie können Daten aus [[!DNL PathFactory]](https://www.pathfactory.com/) mithilfe von drei primären Quellen aufnehmen:

* **[!DNL Visitors]**: Nehmen Sie Kunden- und Kontaktdaten als Datensätze auf, um Ihre Audience besser zu verstehen.
* **[!DNL Sessions]**: Zeitreihenereignisse, die die Aktivitäten einzelner Benutzersitzungen auf Ihrer Plattform verfolgen.
* **[!DNL Page Views]**: Zeitreihenereignisse, die Einblicke in die angezeigten Seiten bieten und Ihnen bei der Analyse der Content-Performance helfen.

Lesen Sie das folgende Dokument, um Informationen zum Einrichten Ihres [!DNL PathFactory]-Quellkontos zu erhalten.

## IP-Adressen-Zulassungsliste {#ip-allow-list}

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste möglicherweise eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen {#prerequisites}

Bevor Sie mit der Integration von [[!DNL PathFactory]](https://www.pathfactory.com/) Connectoren in Experience Platform beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* **Ein [PathFactory-]**.
   * Wenden Sie sich an [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml), wenn Sie noch kein gültiges Konto haben.
* **Aktives Abonnement** für jedes [!DNL PathFactory].
* **Benutzername, Kennwort und Domain**.
   * Diese Anmeldeinformationen sind erforderlich, um auf Ihr [!DNL PathFactory]-Konto und dessen Daten zuzugreifen.
* **Zugriffstoken** und **API-Endpunkte**.
   * Diese sind für die Verbindung mit [!DNL PathFactory] APIs erforderlich.

### Abrufen von Anmeldeinformationen und Zugriffs-Token {#gather-credentials}

Um [!DNL PathFactory] mit Experience Platform zu verbinden, müssen Sie die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung | Endpunkt |
| --- | --- | --- |
| Benutzername | Benutzername Ihres [!DNL PathFactory]. | Nicht zutreffend |
| Passwort | Ihr [!DNL PathFactory]-Passwort. | Nicht zutreffend |
| Domain | Die Ihrem [!DNL PathFactory]-Konto zugeordnete Domain. | Nicht zutreffend |
| Zugriffs-Token | Ein eindeutiges Token, das für die API-Authentifizierung verwendet wird. | Nicht zutreffend |
| Visitors-Endpunkt | Der API-Endpunkt für Besucherdaten. | `/api/public/v3/data_lake_apis/visitors.json` |
| Sessions-Endpunkt | Der API-Endpunkt für Sitzungsdaten. | `/api/public/v3/data_lake_apis/sessions.json` |
| Seitenansichten-Endpunkt | Der API-Endpunkt für Seitenansichtsdaten. | `/api/public/v3/data_lake_apis/page_views.json` |

Ausführliche Anweisungen zum Abrufen Ihres Benutzernamens, Kennworts, Ihrer Domain und Ihres Zugriffstokens finden Sie im [[!DNL PathFactory] Support Center](https://support.pathfactory.com/categories/adobe/). Diese Ressource bietet umfassende Anleitungen zum Abrufen und Verwalten Ihrer -Anmeldeinformationen.

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL PathFactory]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

## Verbinden von [!DNL PathFactory] mit Experience Platform {#pathfactory-connect}

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL PathFactory] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um  [!DNL PathFactory]  mithilfe von APIs in Experience Platform zu &#x200B;](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Verbinden Ihres - [!DNL PathFactory]  mit Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Erstellen eines Datenflusses für eine Quellverbindung mithilfe der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md).
