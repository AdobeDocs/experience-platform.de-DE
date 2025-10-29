---
title: (V2) Pega CDH RealTime Audience-Verbindung
description: Verwenden Sie das Echtzeit-Zielgruppenziel Pega Customer Decision Hub in Adobe Experience Platform, um Profilattribute und Daten zur Zielgruppenzugehörigkeit zur nächstbesten Entscheidungsoption an Pega Customer Decision Hub zu senden.
exl-id: cbb998f9-c268-4d65-87d8-fab56c0844dc
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 14%

---

# (V2) Pega CDH RealTime Audience-Verbindung

## Überblick {#overview}

Verwenden Sie das [!DNL Pega CDH Realtime Audience]-Ziel (V2) in Adobe Experience Platform, um Profilattribute und Daten zur Zielgruppenzugehörigkeit zur Entscheidungsfindung für die nächste beste Aktion an [!DNL Pega Customer Decision Hub] zu senden.

Wenn die Profilzielgruppenzugehörigkeit aus Adobe Experience Platform in [!DNL Pega Customer Decision Hub] geladen wird, kann sie als Prädiktor in adaptiven Modellen verwendet werden und dazu beitragen, die richtigen kontextuellen Daten und Verhaltensdaten für Entscheidungszwecke für die nächste beste Aktion bereitzustellen.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden von Pegasystems erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Pega [hier](mailto:support@pega.com).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Customer Decision Hub]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Telekommunikation {#telecommunications}

Ein Marketing-Experte möchte die Erkenntnisse aus der auf einem Datenwissenschaftsmodell basierenden nächsten besten Aktion nutzen, die von [!DNL Pega Customer Decision Hub] für die Kundeninteraktion bereitgestellt wird. [!DNL Pega Customer Decision Hub] beruht in hohem Maße auf der Kundenabsicht, z. B. „Interested_In_5G“, „Interested_In_Unlimited_Dataplan“ oder „Interest_In_iPhone_Accessories“, um die Entscheidung über die nächstbeste Aktion (NBA) in ausgehenden Kanälen zu bestimmen.

### Finanz-Services {#financial-services}

Ein Marketing-Experte möchte die Angebote für Kunden optimieren, die sich für Newsletter zu Pensionsplänen oder Altersvorsorgeplänen angemeldet oder abgemeldet haben. Finanzdienstleister können mehrere Kunden-IDs aus ihren eigenen CRMs in Adobe Experience Platform aufnehmen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und Profile, die in die Zielgruppen eintreten und diese verlassen, senden, um in ausgehenden Kanälen für die nächstbeste Aktion (NBA) zu [!DNL Pega Customer Decision Hub].

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Ziel zum Exportieren von Daten aus Adobe Experience Platform verwenden können, müssen Sie die folgenden Voraussetzungen in [!DNL Pega Customer Decision Hub] erfüllen:

* Konfigurieren Sie die Komponente für die Integration von Adobe Experience Platform-Profil und Zielgruppenmitgliedschaft [&#x200B; Ihrer &#x200B;](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html).[!DNL Pega Customer Decision Hub]
* Konfigurieren Sie OAuth 2[0 (Client-Registrierung mit Client](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)Anmeldeinformationen) und gewähren Sie den Typ in Ihrer [!DNL Pega Customer Decision Hub].
* Konfigurieren Sie [&#x200B; Datenfluss &#x200B;](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) Echtzeit-Ausführung für den Datenfluss der Adobe-Zielgruppenzugehörigkeit in Ihrer [!DNL Pega Customer Decision Hub].

## Unterstützte Identitäten {#supported-identities}

[!DNL Pega Customer Decision Hub] unterstützt die Aktivierung benutzerdefinierter Benutzer-IDs, die in der folgenden Tabelle beschrieben werden. Weitere Informationen finden Sie unter [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `CustomerID` | Kunden-ID | Allgemeine Benutzerkennung, die ein Profil in [!DNL Pega Customer Decision Hub] und Adobe Experience Platform eindeutig identifiziert. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Exportieren Sie alle Mitglieder einer Zielgruppe mit Identifikatoren (*CustomerID*), Attributen (Nachname, Vorname, Standort usw.) und Daten zur Zielgruppenzugehörigkeit. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind immer aktive API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Weitere Informationen finden Sie unter [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

#### Authentifizierung mit Client-Anmeldedaten für OAuth 2 {#oauth-2-client-credentials-authentication}

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie mithilfe von OAuth 2 mit Authentifizierung über Client-Anmeldeinformationen eine Verbindung zum Pega-CDH-Ziel herstellen können](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Füllen Sie die folgenden Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus:

* **[!UICONTROL Access Token URL]**: Die OAuth 2-Zugriffstoken-URL auf Ihrer [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Client ID]**: Die OAuth 2-[!DNL client ID], die Sie in Ihrer [!DNL Pega Customer Decision Hub] generiert haben.
* **[!UICONTROL Client Secret]**: Die OAuth 2-[!DNL client secret], die Sie in Ihrer [!DNL Pega Customer Decision Hub] generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Geben Sie nach Herstellung der Authentifizierungsverbindung zum [!DNL Pega Customer Decision Hub] die folgenden Informationen für das Ziel an:

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Pega-CDH-Zieldetails](../../assets/catalog/personalization/pega/pega-connect-destination-v2.png)

Um Details für das Ziel zu konfigurieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Next]** aus.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Pega CDH Host Name]**: Der Pega Customer Decision Hub-Hostname, in den das Profil als JSON-Daten exportiert wird.
* **[!UICONTROL Application alias]**: Der Anwendungsalias, den Sie für Ihr Customer Decision Hub-Konto konfiguriert haben. Weitere Informationen finden Sie unter [Hinzufügen eines Anwendungs-URL-Alias](https://docs.pega.com/bundle/platform/page/platform/user-experience/adding-application-url-alias.html) in Ihrer [!DNL Pega Customer Decision Hub].

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-streaming-profile-destinations.md) „Aktivieren von Zielgruppendaten für Streaming Profilexportziele“.

### Zuordnung {#mapping}

Wählen Sie im [!UICONTROL Mapping] Schritt eine eindeutige Kennung aus Ihrem Vereinigungsschema und allen anderen XDM-Feldern aus, die Sie an das Ziel exportieren möchten.

### Zuordnungsbeispiel: Aktivieren von Profilaktualisierungen in [!DNL Pega Customer Decision Hub] {#mapping-example}

Nachfolgend finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Exportieren von Profilen in [!DNL Pega Customer Decision Hub].

* Wählen Sie eine Quellidentität aus, die ein Profil in Adobe Experience Platform und [!DNL Pega Customer Decision Hub] eindeutig identifiziert. Beispiel: `CustomerID`.
* Wählen Sie die Zielprofilattribute aus, denen Sie die ausgewählten Quellprofilattribute zuordnen möchten.

![Identitätszuordnung](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Bei einer erfolgreichen Aktualisierung der Zielgruppenzugehörigkeit für ein Profil würden die Zielgruppenkennung, der Name und die Status in den Datenspeicher für die Pega-Marketing-Zielgruppenzugehörigkeit eingefügt. Die Mitgliedschaftsdaten werden mit einem Kunden verknüpft, der in [!DNL Pega Customer Decision Hub] das Kundenprofil Designer verwendet, wie unten dargestellt.

![Abbildung des Bildschirms der Benutzeroberfläche, mit dem Sie mithilfe des Kundenprofils Designer Daten zur Zielgruppenzugehörigkeit von Adobe mit dem Kunden verknüpfen können](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Die Daten zur Zielgruppenzugehörigkeit werden in den Pega-Designer-Interaktionsrichtlinien mit der nächsten besten Aktion für die Entscheidungsfindung mit der nächsten besten Aktion verwendet, wie unten dargestellt.

![Abbildung des Bildschirms der Benutzeroberfläche, auf dem Sie Felder für die Zielgruppenzugehörigkeit als Bedingungen in den Interaktionsrichtlinien von Pega Next-Best-Action Designer hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png)

Die Datenfelder für die Kundenzielgruppenzugehörigkeit werden wie unten dargestellt als Prädiktoren in adaptiven Modellen hinzugefügt.

![Abbildung des Bildschirms der Benutzeroberfläche, auf dem Sie mithilfe von Prediction Studio Zielgruppenzugehörigkeitsfelder als Prädikatoren in adaptiven Modellen hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Weitere Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der folgenden [!DNL Pega]-Dokumentation:

* [Einrichten einer OAuth 2.0-Client-Registrierung](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [Erstellen einer Echtzeit-Ausführung für Datenflüsse](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [Verwalten von Kundendatensätzen in der Designer des Kundenprofils](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
