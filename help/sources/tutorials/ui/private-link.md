---
title: Azure Private Link für Quellen in der Benutzeroberfläche verwenden
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche private Azure-Links für Quellen verwenden.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 4f6e3049ac320cecdd56dc661dbf90030f0d7d7d
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 1%

---

# Verwenden von [!DNL Azure Private Link] für Quellen in der Benutzeroberfläche

>[!AVAILABILITY]
>
>Diese Funktion befindet sich in der Beta-Phase und wird derzeit nur für die folgenden Quellen unterstützt:
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Sie können die [!DNL Azure Private Link]-Funktion verwenden, um private Endpunkte zu erstellen, mit denen sich Ihre Adobe Experience Platform-Quellen verbinden können. Verbinden Sie Ihre Quellen sicher mit einem virtuellen Netzwerk, indem Sie private IP-Adressen verwenden. Dadurch entfallen öffentliche IP-Adressen, und die Angriffsfläche wird reduziert.Vereinfachen Sie die Netzwerkeinrichtung, indem Sie komplexe Konfigurationen für die Übersetzung von Firewall- oder Netzwerkadressen überflüssig machen und gleichzeitig sicherstellen, dass der Datenverkehr nur genehmigte Services erreicht.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie den Quellarbeitsbereich in der Experience Platform-Benutzeroberfläche verwenden können, um einen privaten Endpunkt zu erstellen und zu verwenden.

## Erstellen eines privaten Endpunkts

Um mit [!DNL Azure Private Link] zu beginnen, navigieren Sie zum Katalog *[!UICONTROL Quellen]* der Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Private Endpunkte]** aus dem Menü der Registerkarten im Arbeitsbereich „Quellen“ aus.

![Der Quellkatalog mit „privaten Endpunkten“.](../../images/tutorials/private-links/catalog.png)

Über die Benutzeroberfläche können Sie Informationen zu vorhandenen privaten Endpunkten anzeigen, z. B. ihre ID, die zugehörige Quelle und den aktuellen Status. Um einen neuen privaten Endpunkt zu erstellen, wählen Sie **[!UICONTROL Privaten Endpunkt erstellen]** aus.

![Die Benutzeroberfläche „Private Endpunkte“ mit ausgewähltem „Privaten Endpunkt erstellen“.](../../images/tutorials/private-links/private-endpoints.png)

Wählen Sie als Nächstes Ihre gewünschte Quelle aus und geben Sie dann Werte für die folgenden Eigenschaften ein:

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres privaten Endpunkts. |
| `subscriptionId` | Die ID, die Ihrem [!DNL Azure]-Abonnement zugeordnet ist. Weitere Informationen finden Sie im [!DNL Azure] unter [Abrufen Ihrer Abonnement- und Mandanten-IDs aus der [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Der Name Ihrer Ressourcengruppe auf [!DNL Azure]. Eine Ressourcengruppe enthält zugehörige Ressourcen für eine [!DNL Azure]. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Verwalten von Ressourcengruppen](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceGroup` | Der Name Ihrer Ressource. In [!DNL Azure] bezieht sich eine Ressource auf Instanzen wie virtuelle Maschinen, Web-Anwendungen und Datenbanken. Weitere Informationen finden Sie im [!DNL Azure] Handbuch unter [Grundlegendes zum Ressourcen [!DNL Azure] Manager](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | Die vollqualifizierten Domain-Namen für Ihre Quelle. **HINWEIS**: Diese Eigenschaft ist nur bei Verwendung der [!DNL Snowflake] erforderlich. |

{style="table-layout:auto"}

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Absenden]**..

![Das Authentifizierungsfenster zum Erstellen eines neuen privaten Endpunkts im Arbeitsbereich der Quell-Benutzeroberfläche.](../../images/tutorials/private-links/create-private-endpoint.png)

### Genehmigen eines privaten Endpunkts

Ein neu erstellter Endpunkt verbleibt im Status „Ausstehend“, bis er von einem Administrator genehmigt wird.

Um eine private Endpunktanfrage für die [!DNL Azure Blob] und [!DNL Azure Data Lake Gen2] Quellen zu genehmigen, melden Sie sich bei der [!DNL Azure Portal] an. Klicken Sie in der linken Navigation auf **[!DNL Data storage]** und gehen Sie dann zur Registerkarte **[!DNL Security + networking]** und wählen Sie **[!DNL Networking]** aus. Wählen Sie als Nächstes **[!DNL Private endpoints]** aus, um eine Liste der mit Ihrem Konto verknüpften privaten Endpunkte und deren aktuellen Verbindungsstatus anzuzeigen. Um eine ausstehende Anfrage zu genehmigen, wählen Sie den gewünschten Endpunkt aus und klicken Sie auf **[!DNL Approve]**.

![Das Azure-Portal mit einer Liste ausstehender privater Endpunkte.](../../images/tutorials/private-links/azure.png)

## Erstellen eines Kontos mit einem privaten Endpunkt

Navigieren Sie zum Quellkatalog und wählen Sie eine Quelle aus, die private Endpunkte unterstützt. Erstellen Sie als Nächstes ein neues Konto mit Ihrer Quelle und wählen Sie während der Kontoauthentifizierung den **[!UICONTROL Privater Endpunkt]** aus. Geben Sie die Authentifizierungsdaten Ihrer Quelle ein und wählen Sie **[!UICONTROL Mit Quelle verbinden]** Warten Sie einige Minuten, bis die Verbindung hergestellt ist.

>[!NOTE]
>
>Wenn die Option [!UICONTROL Privater Endpunkt] aktiviert ist, prüft Experience Platform, ob für die ausgewählte Quelle ein genehmigter privater Endpunkt vorhanden ist. Wenn kein genehmigter Endpunkt gefunden wird, können Sie keine Verbindung herstellen.

![Der Schritt zur Authentifizierung eines neuen Kontos mit aktivierten privaten Endpunkten.](../../images/tutorials/private-links/new-account.png)

Navigieren Sie dann zur [!UICONTROL Vorhandenes Konto] Ihrer Quelle. Über diese Benutzeroberfläche können Sie eine Liste Ihrer bestehenden Konten und der entsprechenden Status anzeigen. Sie können das Filtersymbol ![Filtersymbol](../../../images/icons/filter.png) auswählen, um nur die Konten anzuzeigen, die für die Verbindung mit einem privaten Endpunkt aktiviert wurden.

![Die vorhandene Kontoschnittstelle im Quell-Workflow zeigt nur die gefilterten Konten an, die für private Endpunktverbindungen aktiviert sind.](../../images/tutorials/private-links/existing-private-endpoints.png)

Wählen Sie das gewünschte Konto aus und aktivieren Sie dann **[!UICONTROL Interaktives Authoring]**. Dieser Umschalter aktiviert [!UICONTROL Interaktives Authoring], eine [!DNL Azure] Funktion, mit der Sie Verbindungen testen, Ordnerlisten durchsuchen und Daten in der Vorschau anzeigen können. Die Aktivierung [!UICONTROL Interaktives Authoring] ist für private Endpunktverbindungen erforderlich. Beachten Sie, dass Sie diesen Umschalter nicht manuell deaktivieren können. Er wird nach 60 Minuten automatisch deaktiviert.

[!UICONTROL Interaktives Authoring] benötigt einige Minuten, um zu aktivieren. Nachdem die Einstellung aktiviert ist, klicken Sie **[!UICONTROL Weiter]**, um mit dem nächsten Schritt fortzufahren und die Daten auszuwählen, die Sie aufnehmen möchten.

![Ein vorhandenes Konto wird ausgewählt und die interaktive Bearbeitung ist aktiviert.](../../images/tutorials/private-links/interactive-authoring.png)

## Nächste Schritte

Nachdem Sie erfolgreich einen privaten Endpunkt erstellt haben, können Sie Quellverbindungen und Datenflüsse erstellen und Daten mithilfe privater Endpunkte aufnehmen. In den folgenden Handbüchern finden Sie Informationen zum Erstellen von Datenflüssen in der Benutzeroberfläche:

* [Datenfluss für eine Cloud-Speicherquelle erstellen](../ui/dataflow/batch/cloud-storage.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle](../ui/dataflow/databases.md)