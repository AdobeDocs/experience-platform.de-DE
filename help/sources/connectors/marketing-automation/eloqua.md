---
title: Übersicht über Oracle Eloqua (v2) Source
description: Erfahren Sie, wie Sie Oracle Eloqua mit Adobe Experience Platform verbinden.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# Übersicht über die [!DNL Oracle Eloqua] (V2)-Quelle

>[!IMPORTANT]
>
>Die ursprüngliche [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md)-Quelle wird seit Januar 2026 nicht mehr unterstützt. Für diese veraltete Quelle sind keine Migrationen verfügbar und Sie müssen Ihre Daten mit der neuen [!DNL Oracle Eloqua] (V2)-Quelle erneut implementieren.

[!DNL Oracle Eloqua] ist eine leistungsstarke Marketing-Automatisierungsplattform auf Unternehmensniveau, die Unternehmen - hauptsächlich im B2B-Bereich - dabei unterstützt, den komplexen Prozess der Lead-Verwaltung und der Orchestrierung von Journey zu automatisieren und zu personalisieren. Es dient als zentraler Treffpunkt, an dem Marketing-Teams ausgefeilte Kampagnen über mehrere digitale Kanäle definieren, bereitstellen und messen können, um sicherzustellen, dass potenzielle Kunden die richtigen Inhalte genau zu dem Zeitpunkt erhalten, an dem sie am meisten interagieren. Die unterstützten Objekte für die Aufnahme über [!DNL Eloqua] sind **Kontakte**, **Konten**, **Kampagnen** und **Aktivitäten**. Nach Abschluss der ersten Aufnahme werden alle geänderten Daten im Rahmen eines geplanten inkrementellen Prozesses importiert.

Sie können die [!DNL Eloqua] verwenden, um Ihr [!DNL Eloqua]-Konto mit Adobe Experience Platform zu verbinden. Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie beginnen.

## Anwendungsbeispiele {#use-case-examples}

In der folgenden Tabelle sind die Marketing-Objekte aufgeführt, die von der [!DNL Eloqua] (V2)-Integration mit Adobe Experience Platform unterstützt werden. Für jedes Objekt finden Sie eine Beschreibung zusammen mit Beispielanwendungsfällen, um zu veranschaulichen, wie die Integration [!DNL Eloqua] Daten in Real-Time CDP die Marketing-Effektivität und die Kampagnenergebnisse steigern kann.

| Objekt | Beschreibung | Anwendungsbeispiele |
| --- | --- | --- |
| Kontakte | Nehmen Sie Kontaktdaten (wie Name, E-Mail, Telefonnummer, Stellenbezeichnung) in Real-Time CDP auf, um detaillierte, einheitliche Kundenprofile zu erstellen, die alle Interaktionen und Interaktionen mit jedem einzelnen Kontakt zusammenfassen. | **Kampagnenoptimierung:** Durch die Integration von Kontaktdaten aus [!DNL Eloqua] kann Ihr Marketing-Team Interessenten mit hoher Priorität anhand aktueller Aktivitäten wie E-Mail-Öffnungen, Formularübermittlungen und Ereignisregistrierungen identifizieren. Real-Time CDP bietet eine 360°-Ansicht des Verhaltens jedes Kontakts auf E-Mail-, Website- und anderen Marketing-Touchpoints, sodass Marketing-Teams Kampagnen anpassen und das Messaging für eine bessere Interaktion und Konversion optimieren können. |
| Konten | Nehmen Sie Daten auf Kontoebene auf (z. B. Firmenname, Branche, Unternehmensgröße, Umsatz, Standort), um Strategien für Account-Based Marketing (ABM) in Real-Time CDP zu erstellen, und ermöglichen Sie Ihrem Team, die richtigen Unternehmen anzusprechen und mit relevantem Messaging zu interagieren. | **ABM-Kampagnen:** Die Integration von Account-Daten aus [!DNL Eloqua] hilft bei der Erstellung zielgerichteter ABM-Kampagnen. Ein Softwareunternehmen könnte beispielsweise die Kontodaten verwenden, um maßgeschneiderte E-Mail-Kampagnen zu segmentieren und an Entscheidungsträger in Unternehmen des Finanzsektors zu senden und so neue, auf ihre Branche zugeschnittene Lösungen zu fördern. |
| Kampagnen | Nehmen Sie Kampagnendaten (wie Kampagnennamen, -typen, -ziele, Leistungsmetriken wie Öffnungsraten und CTRs) in die Real-Time CDP auf, um die Kampagnenleistung kanalübergreifend zu verfolgen und zu optimieren. Verwenden Sie diese Daten, um den ROI zu messen und Ihre Strategien zu verfeinern. | **Kanalübergreifende Attribution:** Wenn [!DNL Eloqua] Kampagnendaten an Real-Time CDP sendet, können Marketing-Teams die Performance von Kampagnen auf verschiedenen Kanälen (E-Mail, Social Media, Anzeigen usw.) anzeigen, Konversionen den richtigen Touchpoints zuordnen und zukünftige Strategien auf der Grundlage dieser insight verfeinern. |
| Aktivitäten | Nehmen Sie Aktivitätsdaten (wie E-Mail-Öffnungen, Klicks, Website-Besuche, Formularübermittlungen, Webinar-Anwesenheit) auf, um das Echtzeit-Verhalten und die Kontakte über verschiedene Kanäle hinweg zu verfolgen und so Möglichkeiten für personalisierte Interaktion in Echtzeit zu schaffen. | **Echtzeit-Pflege:** Durch die Integration von Aktivitätsdaten aus [!DNL Eloqua] kann Real-Time CDP personalisierte E-Mails oder Benachrichtigungen an Vertriebsteams Triggern, wenn ein Kontakt mit Inhalten interagiert (z. B. beim Herunterladen eines Whitepapers oder beim Klicken auf einen E-Mail-Link), was eine zeitnahe Nachverfolgung und bessere Konversionsmöglichkeiten ermöglicht. |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung vorzunehmen, die Sie durchführen müssen, bevor Sie Ihre Quelle mit Experience Platform verbinden können.

### Einrichten der Anwendung für die Authentifizierung

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Eloqua]-Konto einrichten und mithilfe der Standardauthentifizierung eine Verbindung zu Experience Platform herstellen.

Melden Sie sich zunächst als Administrator bei Ihrer [!DNL Eloqua]-Instanz an (oder als Benutzer, der Zugriff zum Erstellen von Benutzern, Sicherheitsgruppen und Programmen hat).

![Das My Eloqua-Dashboard.](../../images/tutorials/create/eloqua/admin.png)

Navigieren Sie zu **Einstellungen** > **Platform-** > **App Cloud Developer** > **Create App**. Geben Sie Details für Ihre App an, einschließlich Name, Beschreibung, Symbol und OAuth-Callback-URL. Wählen Sie **Speichern**, wenn Sie fertig sind.

![Das Bedienfeld für App-Entwickler und die Schaltfläche „App erstellen“ im Eloqua-Dashboard.](../../images/tutorials/create/eloqua/create-app.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| Name | Der Name Ihrer App. |
| Beschreibung | Eine kurze Beschreibung für Ihre App. |
| Symbol | Die URL für das Symbol. |
| OAuth Callback-URL | Die URL, zu der Benutzer nach der Installation der App und der Authentifizierung bei [!DNL Eloqua] umgeleitet werden sollten. |

![Das Fenster „App erstellen“ in Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Navigieren Sie nach der Erstellung Ihrer App zu [!DNL Authentication to Eloqua] und rufen Sie die **Client-ID** und das **Client-Geheimnis** aus der neu erstellten App ab. Diese Werte werden später beim Herstellen einer Verbindung mit Experience Platform verwendet.

![Die Client-ID und das Client-Geheimnis in Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

Mit Sicherheitsgruppen können Admins steuern, auf welche Zugriffsebenen Benutzer auf Assets, Funktionen, Schnittstellen usw. zugreifen können. Um eine Sicherheitsgruppe zu erstellen, navigieren Sie zu **Einstellungen** > **Benutzer**. Wählen Sie anschließend im linken Bereich die **Gruppe** und dann **Neue Sicherheitsgruppe erstellen** aus.

![Das User Management-Dashboard in Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Verwenden Sie das Fenster **[!DNL Security Group Overview]** , um einen Namen und ein Akronym für Ihre Sicherheitsgruppe anzugeben. Navigieren Sie nach der Erstellung zu [!DNL Action Permissions] und fügen Sie die [!DNL Consume] API-Berechtigung aus der Liste hinzu und klicken Sie auf **Speichern**.

![Das Fenster Sicherheitsgruppenübersicht in Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![Das Auswahlfenster für die Consume-API](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume] API ist eine erforderliche Berechtigung, Sie können jedoch je nach Nutzung der App weitere Berechtigungen hinzufügen.

Um Kampagnendaten aufzunehmen, navigieren Sie zur Benutzeroberfläche **Benutzer bearbeiten** und fügen Sie Ihrer ausgewählten Sicherheitsgruppe [!DNL Guided Campaigns] hinzu.

![Die Sicherheitsgruppe mit hinzugefügten geführten Kampagnen.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Optional können Sie einen zusätzlichen Benutzer erstellen und diesen Benutzer zu einer Sicherheitsgruppe hinzufügen. Ausführliche Anweisungen finden Sie in der [!DNL Eloqua] Dokumentation unter [Erstellen eines ](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) und [Zuweisen eines Benutzers zu einer Sicherheitsgruppe](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL Eloqua] mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Client-ID | Die öffentlich zugängliche Kennung, die von [!DNL Eloqua] zur Identifizierung Ihres Kontos bei der Autorisierung für Experience Platform verwendet wird. |
| Client-Geheimnis | Der vertrauliche Schlüssel, der nur der Client-Anwendung und dem Autorisierungsserver bekannt ist. Dieser Schlüssel ist zusammen mit der Client-ID erforderlich, um Ihr Konto zu authentifizieren. |
| Benutzername | Der Benutzername, der Ihrem [!DNL Eloqua]-Konto zugeordnet ist. Dies wird verwendet, um Ihren Zugriff zu überprüfen und zu autorisieren. Der Benutzername folgt dem Format von `CompanyName\Username`. |
| Passwort | Das mit Ihrem [!DNL Eloqua]-Konto verknüpfte Kennwort. Zusammen mit Ihrem Benutzernamen gewährt es Zugriff auf Ihre Eloqua-Umgebung. |
| Basis-Endpunkt | Das Präfix Ihres Authentifizierungsbasis-URI für [!DNL Eloqua]. Der Basis-Endpunkt sollte bei der Authentifizierung weder `http://` noch `https://` enthalten. |

## Handbuch zur [!DNL Eloqua]

>[!NOTE]
>
>Im Folgenden finden Sie die Delta-Felder, die intern für das inkrementelle Laden von Daten verwendet werden:
>
>- **Kontakte:** `C_DateModified`
>- **Konten:** `M_DateModified`
>- **Aktivität:** `CreatedAt`
>- **Benutzerdefinierte Objekte:** `UpdatedAt`
>- **Kampagne:** `updatedAt`

Die folgenden Tabellen enthalten detaillierte Zuordnungen zwischen [!DNL Eloqua] Quellfeldern und den entsprechenden Zielfeldern des Experience-Datenmodells (XDM) in Experience Platform. Jede Zeile beschreibt die Umwandlungslogik, ob das Feld unveränderlich ist, und bietet zusätzliche Hinweise, die Ihnen dabei helfen zu verstehen, wie Ihre [!DNL Eloqua] Daten in Experience Platform aufgenommen und strukturiert werden.

### Konten

| Eloqua Source-Spalte | XDM-Zielpfad | Anmerkungen |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Dieses Feld ist immer auf den festen Wert „Eloqua“ festgelegt. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Der Connector kann Ihre CRM-Instanz-ID nicht automatisch erkennen. Sie müssen `${CRM_INSTANCE_ID}` manuell durch Ihre eigentliche CRM-Instanz-ID ersetzen, entweder Ihre Salesforce- oder Dynamics-Instanz-ID. Wenn `M_SFDCAccountID` vorhanden ist, generiert der Connector während der Aufnahme den externen Schlüssel mit diesem Wert und hängt `\@CRM_INSTANCE_ID.Salesforce` an. Wenn dieses Feld leer ist, verwendet der Connector stattdessen `M_MSCRMAccountID` und hängt `\@CRM_INSTANCE_ID.Dynamics` an. Wenn beide Felder leer sind, wird dieses Feld auf null gesetzt. |

{style="table-layout:auto"}

### Aktivitäten

| Eloqua Source-Spalte | XDM-Zielpfad | Anmerkungen |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Dieses Feld ist immer auf den festen Wert „Eloqua“ festgelegt. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | Basierend auf ActivityType wird der entsprechende Wert für Experience Platform eventType ausgefüllt. Für externe Aktivitäten gibt es in Experience Platform keinen eventType. Sie können diese Zuordnung ändern, um mehr Typen zu verarbeiten. |
| `ActivityDate` | Zeitstempel | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Kampagnen

| Eloqua Source-Spalte | XDM-Zielpfad | Anmerkungen |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Dieses Feld ist immer auf den festen Wert „Eloqua“ festgelegt. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Kontakte

| Eloqua Source-Spalte | XDM-Zielpfad | Anmerkungen |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Dieses Feld ist immer auf den festen Wert „Eloqua“ festgelegt. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | Der `SOURCE_INSTANCE_ID` wird automatisch durch den Connector ersetzt. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Wenn die [!DNL Eloqua] mit Salesforce synchronisiert wird, behalten Sie diese Zuordnung bei. Andernfalls entfernen Sie sie. Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte Salesforce-Instanz-ID ersetzen. Dieselbe Zuordnung gilt für personComponents und extSourceSystemAudit. Behalten Sie also beide bei. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Wenn die [!DNL Eloqua] mit Dynamics synchronisiert wird, behalten Sie diese Zuordnung bei. Andernfalls entfernen Sie sie. Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte Dynamics-Instanz-ID ersetzen. Dieselbe Zuordnung gilt für personComponents und extSourceSystemAudit. Behalten Sie also beide bei. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Wenn die [!DNL Eloqua] mit Salesforce synchronisiert wird, behalten Sie diese Zuordnung bei. Andernfalls entfernen Sie sie. Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte Salesforce-Instanz-ID ersetzen. Dieselbe Zuordnung gilt für personComponents und extSourceSystemAudit. Behalten Sie also beide bei. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Wenn die [!DNL Eloqua] mit Dynamics synchronisiert wird, behalten Sie diese Zuordnung bei. Andernfalls entfernen Sie sie. Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte Dynamics-Instanz-ID ersetzen. Dieselbe Zuordnung gilt für personComponents und extSourceSystemAudit. Behalten Sie also beide bei. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte CRM-Instanz-ID ersetzen, entweder durch die Salesforce-Instanz-ID oder die Dynamics-Instanz-ID. Diese Zuordnung gilt sowohl für b2b.accountKey als auch für personComponents.sourceAccountKey. Behalten Sie also beide bei. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | Der Connector hat keine Möglichkeit, die CRM_INSTANCE_ID zu bestimmen. Daher müssen Sie ${CRM_INSTANCE_ID} durch Ihre synchronisierte CRM-Instanz-ID ersetzen, entweder durch die Salesforce-Instanz-ID oder die Dynamics-Instanz-ID. Diese Zuordnung gilt sowohl für b2b.accountKey als auch für personComponents.sourceAccountKey. Behalten Sie also beide bei. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Aktivitätstyp-Zuordnungsreferenz

| Eloqua-Aktivitätstyp | XDM-Ereignistyp |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | Durchlauf unverändert |

{style="table-layout:auto"}

### Variable Platzhalter

Die Zuordnungsvorlagen verwenden die folgenden Variablenplatzhalter, die ersetzt werden, sobald ein Datenfluss ausgeführt wird:

| Platzhalter | Beschreibung | Nutzung |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Eindeutige ID für Eloqua-Quellinstanz | Wird in Quellschlüsseln verwendet |
| `${CRM_INSTANCE_ID}` | Eindeutige ID für das CRM-System (Salesforce/Dynamics) | Wird in externen Schlüsseln verwendet |

## Verbinden von [!DNL Eloqua] mit Experience Platform

Fahren Sie mit der Konfiguration Ihrer [!DNL Eloqua]-Quellverbindung in Experience Platform fort. Eine schrittweise Anleitung zum Einrichten der Verbindung über die Benutzeroberfläche finden Sie im [Tutorial hier](../../tutorials/ui/create/marketing-automation/eloqua.md). Lesen Sie dieses Tutorial, um mehr über das Verbinden Ihres [!DNL Eloqua]-Kontos, das Auswählen von Daten, das Zuordnen von Feldern, das Planen von Aufnahmen und das Überwachen Ihrer Datenflüsse zu erfahren.

