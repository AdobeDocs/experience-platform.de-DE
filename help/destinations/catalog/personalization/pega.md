---
title: (V1) Pega CDH RealTime Audience-Verbindung
description: Verwenden Sie das Echtzeit-Zielgruppenziel Pega Customer Decision Hub in Adobe Experience Platform, um Profilattribute und Daten zur Zielgruppenzugehörigkeit zur nächstbesten Entscheidungsoption an Pega Customer Decision Hub zu senden.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 71de5b0d3e9c4413caa911fbe174e74c0e409d89
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 18%

---

# Pega CDH RealTime Audience-Verbindung

>[!IMPORTANT]
>
>Diese Version des Echtzeit-Zielgruppen-Ziels von Pega Customer Decision Hub unterstützt nur eine einzige Anwendung von Pega Customer Decision. Wenn Sie mehrere Pega Customer Decision Hub-Programme konfiguriert haben, müssen Sie den [(V2) Pega CDH RealTime Audience Destination Connector verwenden](./pega-v2.md).

## Überblick {#overview}

Verwenden Sie das [!DNL Pega Customer Decision Hub] Echtzeit-Zielgruppenziel in Adobe Experience Platform, um Profilattribute und Zielgruppenzugehörigkeitsdaten zur Entscheidungsfindung für die nächste beste Aktion an [!DNL Pega Customer Decision Hub] zu senden.

Wenn die Profilzielgruppenzugehörigkeit aus Adobe Experience Platform in [!DNL Pega Customer Decision Hub] geladen wird, kann sie als Prädiktor in adaptiven Modellen verwendet werden und dazu beitragen, die richtigen kontextuellen Daten und Verhaltensdaten für Entscheidungszwecke für die nächste beste Aktion bereitzustellen.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden von Pegasystems erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Pega [hier](mailto:support@pega.com).

## Anwendungsfälle

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Customer Decision Hub]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Telekommunikation

Ein Marketing-Experte möchte die Erkenntnisse aus der auf einem Datenwissenschaftsmodell basierenden Next-Best-Action-Aktion nutzen, die von [!DNL Pega Customer Decision Hub] für die Kundeninteraktion bereitgestellt wird. [!DNL Pega Customer Decision Hub] ist in hohem Maße von der Kundenabsicht abhängig - z. B. „Interested_In_5G“, „Interested_In_Unlimited_Dataplan“ oder „Interest_In_iPhone_Accessories“.

### Finanz-Services

Ein Marketing-Experte möchte die Angebote für Kunden optimieren, die sich für Newsletter zu Pensionsplänen oder Altersvorsorgeplänen angemeldet oder abgemeldet haben. Finanzdienstleister können mehrere Kunden-IDs aus ihren eigenen CRMs in Adobe Experience Platform aufnehmen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und Profile, die in die Zielgruppen eintreten und diese verlassen, senden, um in ausgehenden Kanälen für die nächstbeste Aktion (NBA) zu [!DNL Pega Customer Decision Hub].

## Voraussetzungen {#prerequisites}

Bevor Sie dieses Ziel zum Exportieren von Daten aus Adobe Experience Platform verwenden können, müssen Sie die folgenden Voraussetzungen in [!DNL Pega Customer Decision Hub] erfüllen:

* Konfigurieren Sie die Komponente für die Integration von Adobe Experience Platform-Profil und Zielgruppenmitgliedschaft [&#128279;](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html) Ihrer [!DNL Pega Customer Decision Hub].
* Konfigurieren Sie OAuth 2[0 (Client-Registrierung mit Client](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)Anmeldeinformationen) und gewähren Sie den Typ in Ihrer [!DNL Pega Customer Decision Hub].
* Konfigurieren Sie [&#x200B; Datenfluss &#x200B;](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) Echtzeit-Ausführung für den Datenfluss der Adobe-Zielgruppenzugehörigkeit in Ihrer [!DNL Pega Customer Decision Hub].

## Unterstützte Identitäten {#supported-identities}

[!DNL Pega Customer Decision Hub] unterstützt die Aktivierung benutzerdefinierter Benutzer-IDs, die in der folgenden Tabelle beschrieben werden. Weitere Informationen finden Sie unter [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| *CustomerID* | Allgemeine Benutzerkennung, die ein Profil in [!DNL Pega Customer Decision Hub] und Adobe Experience Platform eindeutig identifiziert |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Exportieren Sie alle Mitglieder einer Zielgruppe mit Identifikatoren (*CustomerID*), Attributen (Nachname, Vorname, Standort usw.) und Daten zur Zielgruppenzugehörigkeit. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind immer aktive API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Weitere Informationen finden Sie unter [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

#### Authentifizierung mit Client-Anmeldeinformationen für OAuth 2 {#oauth-2-client-credentials-authentication}

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie mithilfe von OAuth 2 mit Authentifizierung über Client-Anmeldeinformationen eine Verbindung zum Pega-CDH-Ziel herstellen können](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Füllen Sie die folgenden Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**:

* **[!UICONTROL Zugriffstoken-URL]**: Die OAuth 2-Zugriffstoken-URL auf Ihrer [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Client-ID]**: Die OAuth 2-[!DNL client ID], die Sie in Ihrer [!DNL Pega Customer Decision Hub]-Instanz generiert haben.
* **[!UICONTROL Client-Geheimnis]**: Das OAuth 2-[!DNL client secret], das Sie in Ihrer [!DNL Pega Customer Decision Hub]-Instanz generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Geben Sie nach Herstellung der Authentifizierungsverbindung zum [!DNL Pega Customer Decision Hub] die folgenden Informationen für das Ziel an:

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Pega-CDH-Zieldetails](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Um Details für das Ziel zu konfigurieren, füllen Sie die erforderlichen Felder aus und klicken Sie auf **[!UICONTROL Weiter]**.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Pega CDH Host Name]**: Der Hostname des Pega Customer Decision Hub, in den das Profil als JSON-Daten exportiert wird.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-streaming-profile-destinations.md) „Aktivieren von Zielgruppendaten für Streaming Profilexportziele“.

### Zielattribute {#attributes}

Im Schritt [[!UICONTROL Attribute auswählen]](../../ui/activate-streaming-profile-destinations.md#select-attributes) empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

### Zuordnungsbeispiel: Aktivieren von Profilaktualisierungen in [!DNL Pega Customer Decision Hub] {#mapping-example}

Nachfolgend finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Exportieren von Profilen in [!DNL Pega Customer Decision Hub].

Auswahl der Quellfelder:

* Wählen Sie eine Kennung (z. B.: Kunden-ID) als Quellidentität aus, die ein Profil in Adobe Experience Platform und [!DNL Pega Customer Decision Hub] eindeutig identifiziert.
* Wählen Sie Änderungen am XDM-Quellprofilattribut aus, die in [!DNL Pega Customer Decision Hub] exportiert und aktualisiert werden müssen.

Auswählen der Zielfelder:

* Wählen Sie den `CustomerID` Namespace als Zielidentität aus.
* Wählen Sie Zielprofilattributnamen aus, die den entsprechenden XDM-Quellprofilattributen zugeordnet werden müssen.

![Identitätszuordnung](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Bei einer erfolgreichen Aktualisierung der Zielgruppenzugehörigkeit für ein Profil würden die Zielgruppenkennung, der Name und die Status in den Datenspeicher für die Pega-Marketing-Zielgruppenzugehörigkeit eingefügt. Die Mitgliedschaftsdaten werden mit einem Kunden verknüpft, der in [!DNL Pega Customer Decision Hub] das Kundenprofil Designer verwendet, wie unten dargestellt.
![Abbildung des Bildschirms der Benutzeroberfläche, mit dem Sie mithilfe des Kundenprofils Designer Daten zur Zielgruppenzugehörigkeit von Adobe mit dem Kunden verknüpfen können](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Die Daten zur Zielgruppenzugehörigkeit werden in den Pega-Designer-Interaktionsrichtlinien mit der nächsten besten Aktion für die Entscheidungsfindung mit der nächsten besten Aktion verwendet, wie unten dargestellt.
![Abbildung des Bildschirms der Benutzeroberfläche, auf dem Sie Felder für die Zielgruppenzugehörigkeit als Bedingungen in den Interaktionsrichtlinien von Pega Next-Best-Action Designer hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png)

Die Datenfelder für die Kundenzielgruppenzugehörigkeit werden wie unten dargestellt als Prädiktoren in adaptiven Modellen hinzugefügt.
![Abbildung des Bildschirms der Benutzeroberfläche, auf dem Sie mithilfe von Prediction Studio Zielgruppenzugehörigkeitsfelder als Prädiktoren in adaptiven Modellen hinzufügen können](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der [!DNL Pega] Dokumentation zu den folgenden Ressourcen:

* [Einrichten einer OAuth 2.0-Client-Registrierung](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [Erstellen einer Echtzeit-Ausführung für Datenflüsse](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [Verwalten von Kundendatensätzen in der Designer des Kundenprofils](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
