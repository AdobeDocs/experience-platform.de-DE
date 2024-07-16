---
title: Pega Customer Decision Hub-Verbindung
description: Verwenden Sie das Pega Customer Decisioning Hub-Ziel in Adobe Experience Platform, um Profilattribute und Zielgruppenmitgliedsdaten an Pega Customer Decisioning Hub zu senden, um die Entscheidungsfindung für nächstbeste Maßnahmen zu treffen.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 20%

---

# Pega Customer Decision Hub-Verbindung

## Übersicht {#overview}

Verwenden Sie das Ziel &quot;[!DNL Pega Customer Decision Hub]&quot;in Adobe Experience Platform, um Profilattribute und Zielgruppenmitgliedsdaten an [!DNL Pega Customer Decision Hub] zu senden, damit eine Entscheidung für die nächste beste Aktion getroffen werden kann.

Die Profil-Zielgruppenmitgliedschaft aus Adobe Experience Platform kann beim Laden in [!DNL Pega Customer Decision Hub] als Prädikator in adaptiven Modellen verwendet werden und dazu beitragen, die richtigen kontextbezogenen und verhaltensbezogenen Daten für Entscheidungszwecke mit der nächsten besten Aktion bereitzustellen.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden von Pegasystemen erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Pega [hier](mailto:support@pega.com).

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Customer Decision Hub]-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Telekommunikation

Ein Marketing-Experte möchte Einblicke aus der auf dem Datenwissenschaftsmodell basierenden nächsten Best Action nutzen, die von [!DNL Pega Customer Decision Hub] für die Kundeninteraktion bereitgestellt wird. [!DNL Pega Customer Decision Hub] ist stark von der Kundenabsicht abhängig, z. B. &quot;Interessant_In_5G&quot;, &quot;Interessant_in_Unlimited_Dataplan&quot;oder &quot;Interest_in_iPhone_Zubehör&quot;.

### Finanz-Services

Ein Marketing-Experte möchte die Angebote für Kunden optimieren, die Newsletter im Pensionsplan oder Pensionsplan abonniert oder abbestellt haben. Finanzdienstleistungsunternehmen können mehrere Kunden-IDs aus ihren eigenen CRMs in Adobe Experience Platform erfassen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und Profile, die die Zielgruppen aufrufen und verlassen, an [!DNL Pega Customer Decision Hub] senden, um die Entscheidung über die nächste beste Aktion (NBA) in ausgehenden Kanälen zu treffen.

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Ziel zum Exportieren von Daten aus Adobe Experience Platform verwenden können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen in [!DNL Pega Customer Decision Hub] erfüllen:

* Konfigurieren Sie die Integrationskomponente [Adobe Experience Platform-Profil und Zielgruppenmitgliedschaft](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) in Ihrer [!DNL Pega Customer Decision Hub] -Instanz.
* Konfigurieren Sie die OAuth 2.0 [Client-Registrierung mit dem Grant-Typ Client-Anmeldedaten](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in Ihrer [!DNL Pega Customer Decision Hub] -Instanz.
* Konfigurieren Sie den Datenfluss [ der Echtzeit-Ausführung](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) für den Datenfluss der Adobe-Zielgruppenmitgliedschaft in Ihrer [!DNL Pega Customer Decision Hub] -Instanz.

## Unterstützte Identitäten {#supported-identities}

[!DNL Pega Customer Decision Hub] unterstützt die Aktivierung benutzerdefinierter Benutzer-IDs, die in der folgenden Tabelle beschrieben sind. Weitere Informationen finden Sie unter [identities](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| *CustomerID* | Allgemeine Benutzer-ID, die ein Profil in [!DNL Pega Customer Decision Hub] und Adobe Experience Platform eindeutig identifiziert |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Exportieren Sie alle Mitglieder einer Zielgruppe mit Kennung (*CustomerID*), Attributen (Nachname, Vorname, Ort usw.) und Daten zur Zielgruppenzugehörigkeit. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind immer auf API-basierten Verbindungen basiert. Sobald ein Profil auf der Experience Platform aktualisiert wird, sendet der Connector basierend auf der Zielgruppenbewertung die Aktualisierung an die Zielplattform. Weitere Informationen finden Sie unter [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

#### Authenifizierung mit Client-Anmeldeinformationen für OAuth 2 {#oauth-2-client-credentials-authentication}

![Bild des UI-Bildschirms, auf dem Sie eine Verbindung zum Pega CDH-Ziel herstellen können, indem Sie OAuth 2 mit Client Credentials authentication verwenden](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Füllen Sie die folgenden Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus:

* **[!UICONTROL Zugriffstoken-URL]**: Die OAuth 2-Zugriffstoken-URL auf Ihrer [!DNL Pega Customer Decision Hub]-Instanz.
* **[!UICONTROL Client-ID]**: Die OAuth 2 [!DNL client ID], die Sie in Ihrer [!DNL Pega Customer Decision Hub] -Instanz generiert haben.
* **[!UICONTROL Client-Geheimnis]**: Das OAuth 2 [!DNL client secret], das Sie in Ihrer [!DNL Pega Customer Decision Hub]-Instanz generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Geben Sie nach Einrichtung der Authentifizierungsverbindung zum [!DNL Pega Customer Decision Hub] die folgenden Informationen für das Ziel ein:

![Bild des UI-Bildschirms mit ausgefüllten Feldern für die Pega CDH-Zieldetails](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Um Details für das Ziel zu konfigurieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Weiter]** aus.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Hostname]**: Der Hostname des Pega Customer Decisioning Hub, in den das Profil als JSON-Daten exportiert wird.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Profilexport-Ziele](../../ui/activate-streaming-profile-destinations.md) .

### Zielattribute {#attributes}

Im Schritt [[!UICONTROL Attribute auswählen]](../../ui/activate-streaming-profile-destinations.md#select-attributes) empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

### Zuordnungsbeispiel: Aktivieren von Profilaktualisierungen in [!DNL Pega Customer Decision Hub] {#mapping-example}

Im Folgenden finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Export von Profilen in [!DNL Pega Customer Decision Hub].

Quellfelder auswählen:

* Wählen Sie eine Kennung (z. B. CustomerID) als Quellidentität aus, die ein Profil in Adobe Experience Platform eindeutig identifiziert und [!DNL Pega Customer Decision Hub].
* Wählen Sie XDM-Quellprofilattributänderungen aus, die in [!DNL Pega Customer Decision Hub] exportiert und aktualisiert werden müssen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `CustomerID` als Zielidentität aus.
* Wählen Sie Zielprofilattributnamen aus, die den entsprechenden XDM-Quellprofilattributen zugeordnet werden müssen.

![Identitätszuordnung](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Bei einer erfolgreichen Aktualisierung der Zielgruppenzugehörigkeit für ein Profil werden die Zielgruppenkennung, der Name und der Status in den Mitgliederdatenspeicher der Pega-Marketing-Zielgruppe eingefügt. Die Mitgliedschaftsdaten werden mit einem Kunden verknüpft, der das Kundenprofil Designer in [!DNL Pega Customer Decision Hub] verwendet, wie unten dargestellt.
![Bild des UI-Bildschirms, auf dem Sie Adobe Audience Membership-Daten mithilfe des Kundenprofils Designer mit dem Kunden verknüpfen können](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Die Daten zur Zielgruppenzugehörigkeit werden in den Interaktionsrichtlinien von Pega Next-Best-Action für die nächste beste Aktion verwendet, wie unten dargestellt.
![Bild des UI-Bildschirms, auf dem Sie Zielgruppenmitgliedsfelder als Bedingungen in den Interaktionsrichtlinien von Pega Next-Best-Action Designer hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Die Datenfelder für die Mitgliedschaft in einer Zielgruppe für Kunden werden wie unten dargestellt als Prädikatoren in adaptiven Modellen hinzugefügt.
![Bild des UI-Bildschirms, auf dem Sie Zielgruppenmitgliedsfelder als Prädikatoren in adaptiven Modellen mithilfe von Predictive Studio hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Zusätzliche Ressourcen {#additional-resources}

Siehe [Einrichten einer OAuth 2.0-Client-Registrierung](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

Siehe [Erstellen einer Echtzeitausführung für Datenflüsse](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

Siehe [Verwalten von Kundendatensätzen im Kundenprofil Designer](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
