---
title: Adobe Campaign Managed Cloud Services-Verbindung
description: Adobe Campaign Managed Cloud Services bietet eine Plattform für die Gestaltung kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Kampagnenorchestrierung, die Echtzeit-Interaktionsverwaltung und die kanalübergreifende Ausführung.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 31%

---

# Adobe Campaign Managed Cloud Services-Verbindung {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Diese Integration funktioniert mit [Adobe Campaign Version 8.4 oder höher](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=de#release-8-4-1).

## Überblick {#overview}

Adobe Campaign Managed Cloud Services bietet eine Plattform für die Gestaltung kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Orchestrierung von Kampagnen, das Management von Interaktionen in Echtzeit und die kanalübergreifende Ausführung. [Erste Schritte mit Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=de)

Mit Campaign haben Sie folgende Möglichkeiten:

* Personalisierung und Interaktion mit der Hilfe einer umfassenden, zentralen Sicht auf den Kunden fördern,
* E-Mail-, Mobil-, Online- und Offline-Kanäle in die Kunden-Journey integrieren,
* Zielführende, zeitlich optimal abgestimmte Nachrichten und Angebote automatisch versenden.

## Leitlinien {#guardrails}

Beachten Sie die folgenden Leitplanken bei der Verwendung der Adobe Campaign Managed Cloud Services-Verbindung:

* Sie [&#x200B; maximal 25 &#x200B;](#activate) für dieses Ziel aktivieren.

  Sie können dieses Limit ändern, indem Sie den Wert der Option **NmsCdp_Aep_Audience_List_Limit** im Ordner **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** des Campaign-Explorers aktualisieren.

* Für jede Zielgruppe können Sie bis zu 20 Felder zu &quot;[&quot; &#x200B;](#map) Adobe Campaign hinzufügen.

  Sie können diesen Grenzwert ändern, indem Sie den Wert der Option **NmsCdp_Aep_Destinations_Max_Columns** im Ordner **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** des Campaign-Explorers aktualisieren.

* Datenaufbewahrung in der Azure Blob Storage Data Landing Zone (DLZ) : 7 Tage.
* Die Aktivierungshäufigkeit beträgt mindestens 3 Stunden.
* Die von dieser Verbindung unterstützte maximale Länge von Dateinamen beträgt 255 Zeichen. Wenn Sie [den Namen der exportierten Datei konfigurieren](../../ui/activate-batch-profile-destinations.md#configure-file-names) stellen Sie sicher, dass der Dateiname 255 Zeichen nicht überschreitet. Eine Überschreitung der maximalen Dateinamenlänge führt zu Aktivierungsfehlern.

## Anwendungsszenarien {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Ziel &quot;Adobe Campaign Manage Service“ verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

* Adobe Experience Platform erstellt ein Kundenprofil, das Informationen wie das Identitätsdiagramm, Verhaltensdaten aus Analytics sowie Offline- und Online-Daten enthält. Mit dieser Integration können Sie die Segmentierungsfunktionen, die bereits in Adobe Campaign vorhanden sind, um diese von Adobe Experience Platform unterstützten Zielgruppen erweitern, sodass Sie diese Daten in Campaign aktivieren können.

  Ein Sportbekleidungsunternehmen möchte beispielsweise die von Adobe Experience Platform unterstützten Zielgruppen nutzen und mithilfe von Adobe Campaign aktivieren, um sich über die verschiedenen von Adobe Campaign unterstützten Kanäle mit ihrem Kundenstamm zu verbinden. Nach dem Versand der Nachrichten möchten sie das Kundenprofil in Adobe Experience Platform mit Erlebnisdaten aus Adobe Campaign wie Sendungen, Öffnungen und Klicks verbessern.

  Das Ergebnis sind Cross-Channel-Kampagnen, die im gesamten Adobe Experience Cloud-Ökosystem konsistenter sind, und ein umfangreiches Kundenprofil, das sich schnell anpasst und lernt.


* Zusätzlich zur Zielgruppenaktivierung in Campaign können Sie das Adobe Campaign Managed Services-Ziel nutzen, um zusätzliche Profilattribute einzufügen, die an ein Profil in Adobe Experience Platform gebunden sind und einen Synchronisierungsprozess aufweisen, damit sie in der Adobe Campaign-Datenbank aktualisiert werden.

  Nehmen wir beispielsweise an, Sie erfassen Opt-in- und Opt-out-Werte in Adobe Experience Platform. Mit dieser Verbindung können Sie diese Werte in Adobe Campaign übernehmen und einen Synchronisierungsprozess einrichten, damit sie regelmäßig aktualisiert werden.

  >[!NOTE]
  >
  >Die Synchronisierung von Profilattributen ist für Profile verfügbar, die bereits in der Adobe Campaign-Datenbank vorhanden sind.

[Erfahren Sie mehr über die Integration von Adobe Campaign mit Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=de)

## Unterstützte Identitäten {#supported-identities}

*Adobe Campaign Managed Cloud Services* unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| EXTERNAL_ID | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. Es wird empfohlen, diese Identität zu verwenden und sie der ID in Ihrer Campaign-Instanz zuzuordnen, die für den Kunden steht (Loyalty_ID, Account_ID, Customer_ID usw.) |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Profilattribute auswählen“ im Workflow &quot;[-Aktivierung“ &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Instanz auswählen]**: Ihre **[!DNL Campaign]** Marketing-Instanz.
* **[!UICONTROL Zielgruppen-Mapping]** Wählen Sie das Zielgruppen-Mapping aus, das Sie **[!DNL Adobe Campaign]** Versand verwenden. [Weitere Informationen](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html?lang=de).
* **[!UICONTROL Synchronisierungstyp auswählen]**:

   * **[!UICONTROL Zielgruppensynchronisierung]**: Verwenden Sie diese Option, um Adobe Experience Platform-Zielgruppen an Adobe Campaign zu senden.
   * **[!UICONTROL Profilsynchronisierung (nur Update)]**: Verwenden Sie diese Option, um Adobe Experience Platform-Profilattribute in Adobe Campaign zu importieren und einen Synchronisierungsprozess einzurichten, damit sie regelmäßig aktualisiert werden können.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Governance-Richtlinie und Durchsetzungsmaßnahmen {#governance}

Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Für Adobe Campaign empfehlen wir die Marketing **[!UICONTROL Aktion „E-Mail]** Targeting“.

Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Datennutzungsrichtlinien – Übersicht](/help/data-governance/policies/overview.md).

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppendaten für dieses Ziel finden Sie &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=de)Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele“.

### Zuordnen von Attributen und Identitäten {#map}

Wählen Sie die XDM-Felder aus, die mit den Profilen exportiert werden sollen, und ordnen Sie sie den entsprechenden Adobe Campaign-Feldern zu.[Erfahren Sie mehr über die Auswahl von Identitäten und Attributen für E-Mail-Marketing-Ziele](overview.md)

1. Quellfelder auswählen:

   * Wählen Sie eine **Kennung** (z. B. das E-Mail-Feld) als Quellidentität aus, die ein Profil in Adobe Experience Platform und Adobe Campaign eindeutig identifiziert.

   * Wählen Sie alle anderen **XDM-Quellprofilattribute** aus, die nach Adobe Campaign exportiert werden müssen.

   >[!NOTE]
   >
   >Das Feld „segmentMembershipStatus“ ist eine erforderliche Zuordnung, um den segmentMembership-Status widerzuspiegeln. Dieses Feld wird standardmäßig hinzugefügt und kann nicht geändert oder entfernt werden.

1. Ordnen Sie jedes Feld seinem Zielfeld in Adobe Campaign zu. Verfügbare Zielfelder werden durch das beim Erstellen des Ziels [&#x200B; Zielgruppen-Mapping &#x200B;](#destination-details).

1. Identifizieren Sie obligatorische Attribute und Deduplizierungsschlüssel. Beachten Sie, dass Werte in Attributen, die als „obligatorisch“ oder „Deduplizierungsschlüssel“ markiert sind, nicht null sein dürfen.

   * [Obligatorische Attribute](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) Stellen Sie sicher, dass alle Profildatensätze die ausgewählten Attribute enthalten. Beispiel: Alle exportierten Profile enthalten eine E-Mail-Adresse. Es wird empfohlen, sowohl das Identitätsfeld als auch das als Deduplizierungsschlüssel verwendete Feld auf obligatorisch festzulegen.
   * [Ein Deduplizierungsschlüssel](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) ist ein Primärschlüssel, der die Identität bestimmt, mit der Benutzer ihre Profile deduplizieren lassen möchten.

     >[!IMPORTANT]
     >
     >Stellen Sie sicher, dass der Name des Deduplizierungsschlüsselattributs mit einem Spaltennamen der ausgewählten Zielzuordnung übereinstimmt.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Sobald die Zuordnung durchgeführt wurde, können Sie die Zielkonfiguration überprüfen und abschließen, um mit dem Senden von Daten an **[!DNL Campaign]** zu beginnen.
   [Erfahren Sie, wie Sie die Zielkonfiguration überprüfen und abschließen](/help/destinations/destination-types.md#review).

## Exportierte Daten/Datenexport validieren {#exported-data}

Nachdem ein Ziel aktiviert wurde, können Sie in Campaign auf den entsprechenden Auftrag und die exportierten Daten zugreifen.

### Überwachen von Datenexportvorgängen {#jobs}

Navigieren Sie zum Menü **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience-Ladevorgänge]**, um alle von Adobe Experience Platform aktivierten Exportvorgänge zu überwachen.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Zugreifen auf exportierte Daten {#data}

Bei **[!UICONTROL Zielgruppensynchronisierung]** können Sie die exportierte Zielgruppe überprüfen, indem Sie zum Menü **[!UICONTROL Profil und Ziel]** > **[!UICONTROL Liste]** > **[!UICONTROL AEP-Zielgruppen]**.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Bei **[!UICONTROL Profilsynchronisierung (nur Aktualisierung)]** werden die Daten automatisch für jedes Profil, das von der im Ziel aktivierten Audience angesprochen wird, in der Campaign-Datenbank aktualisiert.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
