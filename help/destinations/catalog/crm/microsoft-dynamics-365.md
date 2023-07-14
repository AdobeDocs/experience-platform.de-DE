---
keywords: crm;CRM;CRM-Ziele;Microsoft Dynamics 365;Microsoft Dynamics 365 CRM-Ziel
title: Verbindung mit Microsoft Dynamics 365
description: Mit dem Microsoft Dynamics 365-Ziel können Sie Ihre Kontodaten exportieren und in Microsoft Dynamics 365 für Ihre geschäftlichen Anforderungen aktivieren.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 82%

---

# [!DNL Microsoft Dynamics 365]-Verbindung

## Übersicht {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/de-de/) ist eine Cloud-basierte Plattform für geschäftliche Anwendungen, die Enterprise Resource Planning (ERP) und Customer Relationship Management (CRM) mit Produktivitätsanwendungen und KI-Tools kombiniert, um einen rundum reibungsloseren und besser kontrollierten Betrieb, besseres Wachstumspotenzial und Kostenreduzierungen zu erzielen.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), mit dem Sie Identitäten innerhalb einer Audience in aktualisieren können. [!DNL Dynamics 365].

[!DNL Dynamics 365] verwendet OAuth 2 mit Autorisierungs-Grant als Authentifizierungsmechanismus für die Kommunikation mit der [!DNL Contact Entity Reference API]. Anweisungen zur Authentifizierung bei Ihrer [!DNL Dynamics 365]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Als Marketing-Experte können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Zielgruppen aus Ihren Offline-Daten erstellen und diese Zielgruppen an senden [!DNL Dynamics 365], um in den Feeds der Benutzer anzuzeigen, sobald Audiences und Profile in Adobe Experience Platform aktualisiert wurden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Dynamics 365]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Dokumentation von Adobe für [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) wenn Sie Anleitungen zum Zielgruppenstatus benötigen.

### Voraussetzungen für [!DNL Microsoft Dynamics 365] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL Dynamics 365], um Daten von Platform in Ihr [!DNL Dynamics 365]-Konto zu exportieren:

#### Sie benötigen ein [!DNL Microsoft Dynamics 365]-Konto {#prerequisites-account}

Navigieren Sie zur [Testversion-Seite](https://dynamics.microsoft.com/de-de/dynamics-365-free-trial/) von [!DNL Dynamics 365], um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben.

#### Erstellen eines Felds in [!DNL Dynamics 365] {#prerequisites-custom-field}

Benutzerdefiniertes Feld vom Typ erstellen `Simple` mit dem Felddatentyp als `Single Line of Text` welche Experience Platform verwendet, um den Zielgruppenstatus in [!DNL Dynamics 365].
Weitere Anleitung finden Sie in der [!DNL Dynamics 365]-Dokumentation zu [Erstellen eines Felds (Attribut)](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1).

Im Folgenden sehen Sie ein Beispiel-Setup in [!DNL Dynamics 365]:
![Screenshot der Benutzeroberfläche von Dynamics 365 mit den benutzerdefinierten Feldern.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrieren von Programmen und Programmbenutzern in Azure Active Directory {#prerequisites-app-user}

Um [!DNL Dynamics 365] für den Zugriff auf Ressourcen zu aktivieren, müssen Sie sich mit Ihrem [!DNL Azure Account] bei [[!DNL Azure Active Directory]](https://docs.microsoft.com/de-de/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) anmelden und Folgendes erstellen:
* Ein [!DNL Azure Active Directory]-Programm
* Einen Dienstprinzipal
* Einen Programm-Geheim-Code

Sie müssen außerdem [Programmbenutzer](https://docs.microsoft.com/de-de/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] erstellen und sie mit dem neu erstellten Programm verknüpfen.

#### Sammeln von [!DNL Dynamics 365]-Anmeldeinformationen {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL Dynamics 365]-CRM-Ziel authentifizieren:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Client ID` | Die [!DNL Dynamics 365]-Client-ID für Ihr [!DNL Azure Active Directory]-Programm. Eine Anleitung finden Sie in der [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in). | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | Den [!DNL Dynamics 365]-Client-Geheim-Code für Ihr [!DNL Azure Active Directory]-Programm. Sie würden Option 2 innerhalb der [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options) verwenden. | `abcde~abcdefghijklmnopqrstuvwxyz12345678` für Anleitung. |
| `Tenant ID` | Die [!DNL Dynamics 365]-Mandanten-ID für Ihr [!DNL Azure Active Directory]-Programm. Eine Anleitung dazu finden Sie in der [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in). | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | Siehe die [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1), um eine Anleitung zu erhalten. | Wenn Ihre [!DNL Dynamics 365]-Domain wie im Folgenden aussieht, benötigen Sie den hervorgehobenen Wert.<br> *`org57771b33`.crm.dynamics.com* |

## Leitplanken {#guardrails}

Auf der Seite [Anforderungsbeschränkungen und Zuweisungen](https://docs.microsoft.com/de-de/power-platform/admin/api-request-limits-allocations) werden die [!DNL Dynamics 365]-API-Beschränkungen für Ihre [!DNL Dynamics 365]-Lizenz detailliert aufgeführt. Sie müssen sicherstellen, dass Ihre Daten und Payloads innerhalb dieser Beschränkungen liegen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Dynamics 365] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beispiel | Beschreibung | Zu beachten |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Eindeutige Kennung für einen Kontakt. | **Obligatorisch**. Siehe die [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), um weitere Informationen zu erhalten. |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Zielgruppenstatus in [!DNL Dynamics 365] wird mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example) Schritt.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform basierend auf der Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Dynamics 365]. Alternativ können Sie es unter der **[!UICONTROL CRM]**-Kategorie finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden Sie im Abschnitt [Sammeln von Dynamics 365-Anmeldeinformationen](#gather-credentials).
* **[!UICONTROL Client-ID]**: Die [!DNL Dynamics 365]-Client-ID für Ihr [!DNL Azure Active Directory]-Programm.
* **[!UICONTROL Mandanten-ID]**: Die [!DNL Dynamics 365]-Mandanten-ID für Ihr [!DNL Azure Active Directory]-Programm.
* **[!UICONTROL Client-Geheimnis]**: Der [!DNL Dynamics 365]-Client-Geheim-Code für Ihr [!DNL Azure Active Directory]-Programm.
* **[!UICONTROL Umgebungs-URL]**: Ihre [!DNL Dynamics 365]-Umgebungs-URL.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppenexport-Ziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Dynamics 365]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen. Um Ihre XDM-Felder den [!DNL Dynamics 365]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche für „Neue Zuordnung hinzufügen“.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Identity-Namespace auswählen]** und klicken Sie auf `contactId`.
   ![Screenshot-Beispiel der Platform-Benutzeroberfläche für die Quellzuordnung.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** den Typ des Zielfelds aus, dem Sie Ihr Quellfeld zuordnen möchten.
   * **[!UICONTROL Identity-Namespace auswählen]**: Wählen Sie diese Option aus, um Ihr Quellfeld einem Identity-Namespace aus der Liste zuzuordnen.
     ![Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnung für contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Fügen Sie die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrer [!DNL Dynamics 365]-Instanz hinzu:
|XDM-Profilschema|[!DNL Dynamics 365] Instanz| Obligatorisch|
|---|---|---|
|`contactId`|`contactId`| Ja |

   * **[!UICONTROL Benutzerdefinierte Attribute auswählen]**: Wählen Sie diese Option aus, um Ihr Quellfeld einem benutzerdefinierten Attribut zuzuordnen, das Sie im Feld **[!UICONTROL Attributname]** definieren. Eine umfassende Liste der unterstützten Attribute finden Sie in der [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties).
     ![Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnung für LastName.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

     >[!IMPORTANT]
     >
     >Wenn Sie ein Quellfeld für Datum oder Zeitstempel haben, das einem [Datum- oder Zeitstempel](https://docs.microsoft.com/de-de/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest)-Zielfeld von [!DNL Dynamics 365] zugeordnet ist, stellen Sie sicher, dass der zugeordnete Wert nicht leer ist. Wenn der übergebene Wert leer ist, wird die Fehlermeldung *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* angezeigt und die Daten werden nicht aktualisiert. Dies ist eine [!DNL Dynamics 365]-Beschränkung.

   * Fügen Sie je nach den Werten, die Sie aktualisieren möchten, beispielsweise die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrer [!DNL Dynamics 365]-Instanz ein: 
|XDM-Profilschema|[!DNL Dynamics 365] Instanz|

|---|---|

|`person.name.firstName`|`FirstName`|

|`person.name.lastName`|`LastName`|

|`personalEmail.address`|`Email`|

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnungen.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Zielgruppenexport und Beispiel planen {#schedule-segment-export-example}

Im [[!UICONTROL Zielgruppenexport planen]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt des Aktivierungs-Workflows müssen Sie Platform-Zielgruppen manuell dem benutzerdefinierten Feldattribut in [!DNL Dynamics 365].

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Feldattribut aus [!DNL Dynamics 365] im Feld **[!UICONTROL Zuordnungs-ID]** an.

>[!IMPORTANT]
>
>Der für die **[!UICONTROL Zuordnungs-ID]** verwendete Wert sollte genau mit dem Namen des benutzerdefinierten Feldattributs übereinstimmen, das in [!DNL Dynamics 365] erstellt wurde. Siehe die [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1), wenn Sie Anleitungen zum Auffinden Ihrer benutzerdefinierten Feldattribute benötigen.

Nachfolgend finden Sie ein Beispiel:
![Screenshot-Beispiel der Platform-Benutzeroberfläche mit der Option Zielgruppenexport planen](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** aus, um zur Liste der Ziele zu navigieren.
   ![Screenshot der Platform-Benutzeroberfläche mit den Durchsuchen-Zielen.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL aktiviert]** ist.
   ![Screenshot der Platform-Benutzeroberfläche mit Zielen der Datenflussausführung.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Wechseln Sie zu **[!DNL Activation data]** und wählen Sie einen Zielgruppennamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Melden Sie sich bei der [!DNL Dynamics 365] Website und navigieren Sie dann zur [!DNL Customers] > [!DNL Contacts] und überprüfen Sie, ob die Profile aus der Audience hinzugefügt wurden. Sie können sehen, dass jeder Zielgruppenstatus in [!DNL Dynamics 365] mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example) Schritt.
   ![Screenshot der Benutzeroberfläche von Dynamics 365 mit der Seite Kontakte mit aktualisierten Zielgruppenstatus.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Pushen von Ereignissen an das Ziel aufgetreten {#unknown-errors}

Wenn Sie beim Überprüfen eines Datenflusses die folgende Fehlermeldung erhalten: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung wegen fehlerhafter Anfrage.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Um diesen Fehler zu beheben, überprüfen Sie, ob die Variable **[!UICONTROL Zuordnungs-ID]** Sie haben [!DNL Dynamics 365] für Ihre Platform-Zielgruppe gültig ist und in [!DNL Dynamics 365].

## Weitere Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [[!DNL Dynamics 365] Dokumentation](https://docs.microsoft.com/de-de/dynamics365/) finden Sie im Folgenden:
* [Die Methode IOrganizationService.Update(Entity)](https://docs.microsoft.com/de-de/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Aktualisieren und Löschen von Tabellenzeilen mithilfe der Web-API](https://docs.microsoft.com/de-de/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
