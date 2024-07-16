---
title: Adobe Campaign Managed Cloud Services-Verbindung
description: Adobe Campaign Managed Cloud Services bietet eine Plattform für die Konzeption kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Kampagnenorchestrierung, Interaktionsverwaltung in Echtzeit und die kanalübergreifende Ausführung.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: 299868e5ca1b8fde667c4c0ec9a7435634a1717d
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 31%

---

# Adobe Campaign Managed Cloud Services-Verbindung {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Diese Integration funktioniert mit [Adobe Campaign-Version 8.4 oder höher](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Übersicht {#overview}

Adobe Campaign Managed Cloud Services bietet eine Plattform für die Gestaltung kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Orchestrierung von Kampagnen, das Management von Interaktionen in Echtzeit und die kanalübergreifende Ausführung. [Erste Schritte mit Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=de)

Mit Campaign haben Sie folgende Möglichkeiten:

* Personalisierung und Interaktion durch eine einzige zugängliche Ansicht des Kunden fördern,
* Integrieren von E-Mail-, Mobile-, Online- und Offline-Kanälen in die Journey des Kunden,
* Automatisieren Sie die Bereitstellung aussagekräftiger und zeitnaher Nachrichten und Angebote.

## Leitplanken {#guardrails}

Beachten Sie bei der Verwendung der Adobe Campaign Managed Cloud Services-Verbindung die folgenden Limits:

* Sie können für dieses Ziel [maximal 25 Zielgruppen aktivieren](#activate).

  Sie können diese Beschränkung ändern, indem Sie den Wert der Option **NmsCdp_Aep_Audience_List_Limit** im Ordner **[!UICONTROL Administration]** > **[!UICONTROL Plattform]** > **[!UICONTROL Optionen]** des Campaign-Explorer aktualisieren.

* Für jede Zielgruppe können Sie bis zu 20 Felder zu [map](#map) zu Adobe Campaign hinzufügen.

  Sie können diese Beschränkung ändern, indem Sie den Wert der Option **NmsCdp_aep_Destinations_Max_Columns** im Ordner **[!UICONTROL Administration]** > **[!UICONTROL Plattform]** > **[!UICONTROL Optionen]** des Campaign-Explorer aktualisieren.

* Datenbeibehaltung in Azure Blob Storage Data Landing Zone (DLZ) : 7 Tage.
* Die Aktivierungshäufigkeit beträgt mindestens 3 Stunden.
* Die maximale Länge des Dateinamens, die von dieser Verbindung unterstützt wird, beträgt 255 Zeichen. Wenn Sie [den exportierten Dateinamen konfigurieren](../../ui/activate-batch-profile-destinations.md#configure-file-names), stellen Sie sicher, dass der Dateiname 255 Zeichen nicht überschreitet. Wenn die maximale Länge des Dateinamens überschritten wird, treten Aktivierungsfehler auf.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Adobe Campaign-Verwaltungsdienstziel verwenden sollten, finden Sie hier ein Beispielanwendungsbeispiel, das Adobe Experience Platform-Kunden mithilfe dieses Ziels lösen können.

* Adobe Experience Platform erstellt ein Kundenprofil, das Informationen wie das Identitätsdiagramm, Verhaltensdaten aus Analysen, das Zusammenführen von Offline- und Online-Daten usw. enthält. Durch diese Integration können Sie die Segmentierungsfunktionen, die bereits in Adobe Campaign vorhanden sind, mit den Adobe Experience Platform-basierten Zielgruppen erweitern und diese Daten in Campaign aktivieren.

  Ein Sportartikelunternehmen möchte beispielsweise die Adobe Experience Platform-gestützten Zielgruppen nutzen und sie mithilfe von Adobe Campaign aktivieren, um über die verschiedenen von Adobe Campaign unterstützten Kanäle Kontakt zu seinem Kundenstamm aufzunehmen. Nachdem die Nachrichten gesendet wurden, sollen sie das Kundenprofil in der Adobe Experience Platform mit Erlebnisdaten aus Adobe Campaign wie Sendungen, Öffnungen und Klicks verbessern.

  Das Ergebnis sind kanalübergreifende Kampagnen, die im gesamten Adobe Experience Cloud-Ökosystem konsistenter sind, und ein umfangreiches Kundenprofil, das sich schnell anpasst und lernt.


* Zusätzlich zur Zielgruppenaktivierung in Campaign können Sie das Adobe Campaign Managed Services-Ziel nutzen, um zusätzliche Profilattribute einzubringen, die mit einem Profil in Adobe Experience Platform verknüpft sind und einen Synchronisierungsprozess durchführen, damit sie in der Adobe Campaign-Datenbank aktualisiert werden.

  Nehmen wir beispielsweise an, Sie erfassen Opt-in- und Opt-out-Werte in Adobe Experience Platform. Mit dieser Verbindung können Sie diese Werte in Adobe Campaign übernehmen und einen Synchronisierungsprozess einrichten, damit sie regelmäßig aktualisiert werden.

  >[!NOTE]
  >
  >Die Synchronisierung von Profilattributen ist für Profile verfügbar, die bereits in der Adobe Campaign-Datenbank vorhanden sind.

[Weitere Informationen zur Integration von Adobe Campaign mit Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=de)

## Unterstützte Identitäten {#supported-identities}

*Adobe Campaign Managed Cloud Services* unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. Es wird empfohlen, diese Identität zu verwenden und sie der ID in Ihrer Campaign-Instanz zuzuordnen, die den Kunden repräsentiert (loyalty_ID, account_ID, customer_ID..). |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](/help/identity-service/features/ecid.md) . |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute auswählen des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Instanz auswählen]**: Ihre **[!DNL Campaign]** Marketing-Instanz.
* **[!UICONTROL Zielgruppen-Mapping]**: Wählen Sie das Zielgruppen-Mapping aus, das Sie in **[!DNL Adobe Campaign]** zum Senden von Sendungen verwenden. [Weitere Informationen](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Wählen Sie den Synchronisierungstyp]** aus:

   * **[!UICONTROL Zielgruppensynchronisierung]**: Mit dieser Option können Sie Adobe Experience Platform-Zielgruppen an Adobe Campaign senden.
   * **[!UICONTROL Profilsynchronisierung (nur aktualisieren)]**: Verwenden Sie diese Option, um Adobe Experience Platform-Profilattribute in Adobe Campaign zu importieren und einen Synchronisierungsprozess einzurichten, damit sie regelmäßig aktualisiert werden können.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Governance-Richtlinie und Durchsetzungsmaßnahmen {#governance}

Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Für Adobe Campaign wird empfohlen, die Marketing-Aktion **[!UICONTROL E-Mail-Targeting]** auszuwählen.

Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Datennutzungsrichtlinien – Übersicht](/help/data-governance/policies/overview.md).

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppendaten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) .

### Zuordnen von Attributen und Identitäten {#map}

Wählen Sie XDM-Felder aus, die mit den Profilen exportiert werden sollen, und ordnen Sie sie den entsprechenden Adobe Campaign-Feldern zu.[Weitere Informationen zur Auswahl von Identitäts- und Attributen für E-Mail-Marketing-Ziele](overview.md)

1. Quellfelder auswählen:

   * Wählen Sie eine **Kennung** (z. B. das E-Mail-Feld) als Quellidentität aus, die ein Profil in Adobe Experience Platform und Adobe Campaign eindeutig identifiziert.

   * Wählen Sie alle anderen **XDM-Quellprofilattribute** aus, die nach Adobe Campaign exportiert werden sollen.

   >[!NOTE]
   >
   >Das Feld &quot;segmentMembershipStatus&quot;ist ein erforderliches Mapping, das den Segmentzugehörigkeitsstatus widerspiegelt. Dieses Feld wird standardmäßig hinzugefügt und kann nicht geändert oder entfernt werden.

1. Ordnen Sie jedes Feld dem Zielfeld in Adobe Campaign zu. Die verfügbaren Zielfelder werden durch das beim [Erstellen des Ziels](#destination-details) ausgewählte Zielgruppen-Mapping bestimmt.

1. Identifizieren Sie erforderliche Attribute und Deduplizierungsschlüssel. Beachten Sie, dass Werte in Attributen, die als &quot;Obligatorisch&quot;oder &quot;Deduplizierungsschlüssel&quot;markiert sind, nicht null sein können.

   * [Obligatorische Attribute](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) stellen sicher, dass alle Profildatensätze die ausgewählten Attribute enthalten. Beispiel: Alle exportierten Profile enthalten eine E-Mail-Adresse. Es wird empfohlen, sowohl das Identitätsfeld als auch das als Deduplizierungsschlüssel verwendete Feld als obligatorisch festzulegen.
   * [Ein Deduplizierungsschlüssel](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) ist ein Primärschlüssel, der die Identität bestimmt, anhand derer Benutzer ihre Profile deduplizieren möchten.

     >[!IMPORTANT]
     >
     >Stellen Sie sicher, dass der Name des Deduplizierungsschlüsselattributs mit dem Spaltennamen des ausgewählten Zielgruppen-Mappings übereinstimmt.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Nachdem die Zuordnung durchgeführt wurde, können Sie die Zielkonfiguration überprüfen und abschließen, um mit dem Senden von Daten an **[!DNL Campaign]** zu beginnen.
   [Erfahren Sie, wie Sie die Zielkonfiguration überprüfen und abschließen](/help/destinations/destination-types.md#review).

## Exportierte Daten/Datenexport validieren {#exported-data}

Nachdem ein Ziel aktiviert wurde, können Sie in Campaign auf den entsprechenden Auftrag und die exportierten Daten zugreifen.

### Überwachen von Datenexportvorgängen {#jobs}

Navigieren Sie zum Menü **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load-Aufträge]** , um alle Exportvorgänge zu überwachen, die von Adobe Experience Platform aktiviert wurden.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Auf exportierte Daten zugreifen {#data}

Für die **[!UICONTROL Zielgruppensynchronisierung]** können Sie die exportierte Zielgruppe überprüfen, indem Sie zum Menü **[!UICONTROL Profil und Ziel]** > **[!UICONTROL Liste]** > **[!UICONTROL AEP-Zielgruppen]** navigieren.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Bei der **[!UICONTROL Profilsynchronisierung (nur Aktualisierung)]** werden die Daten für jedes Profil, das von der im Ziel aktivierten Zielgruppe angesprochen wird, automatisch in die Campaign-Datenbank aktualisiert.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
