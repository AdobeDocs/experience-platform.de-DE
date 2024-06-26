---
title: Adobe Campaign Managed Cloud Services-Verbindung
description: Adobe Campaign Managed Cloud Services bietet eine Plattform für die Konzeption kanalübergreifender Kundenerlebnisse und eine Umgebung für die visuelle Kampagnenorchestrierung, Interaktionsverwaltung in Echtzeit und die kanalübergreifende Ausführung.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: 9757931f03f57b722c47955d83cb074629d9a883
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 34%

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

>[!IMPORTANT]
>
>Beachten Sie bei der Verwendung der Adobe Campaign Managed Cloud Services-Verbindung die folgenden Limits:
>
>* Maximal 50 Segmente können [enabled](#activate) für das Ziel,
>* Für jedes Segment können Sie bis zu 20 Felder zu [map](#map) nach Adobe Campaign,
>* Datenbeibehaltung in Azure Blob Storage Data Landing Zone (DLZ) : 7 Tage,
>* Die Aktivierungshäufigkeit beträgt mindestens 3 Stunden.
>* Die maximale Länge des Dateinamens, die von dieser Verbindung unterstützt wird, beträgt 255 Zeichen. Wenn Sie [den exportierten Dateinamen konfigurieren](../../ui/activate-batch-profile-destinations.md#configure-file-names)darf der Dateiname nicht länger als 255 Zeichen sein. Wenn die maximale Länge des Dateinamens überschritten wird, treten Aktivierungsfehler auf.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Adobe Campaign-Verwaltungsdienstziel verwenden sollten, finden Sie hier ein Beispielanwendungsbeispiel, das Adobe Experience Platform-Kunden mithilfe dieses Ziels lösen können.

* Adobe Experience Platform erstellt ein Kundenprofil, das Informationen wie das Identitätsdiagramm, Verhaltensdaten aus Analysen, das Zusammenführen von Offline- und Online-Daten usw. enthält. Durch diese Integration können Sie die Segmentierungsfunktionen, die bereits in Adobe Campaign vorhanden sind, mit den Adobe Experience Platform-basierten Zielgruppen erweitern und diese Daten in Campaign aktivieren.

  Ein Sportartikelunternehmen möchte beispielsweise die Adobe Experience Platform-gestützten Smart-Segmente nutzen und sie mithilfe von Adobe Campaign aktivieren, um über die verschiedenen von Adobe Campaign unterstützten Kanäle zu seinem Kundenstamm zu gelangen. Nachdem die Nachrichten gesendet wurden, sollen sie das Kundenprofil in der Adobe Experience Platform mit Erlebnisdaten aus Adobe Campaign wie Sendungen, Öffnungen und Klicks verbessern.

  Das Ergebnis sind kanalübergreifende Kampagnen, die im gesamten Adobe Experience Cloud-Ökosystem konsistenter sind, und ein umfangreiches Kundenprofil, das sich schnell anpasst und lernt.


* Zusätzlich zur Segmentaktivierung in Campaign können Sie das Adobe Campaign Managed Services-Ziel nutzen, um zusätzliche Profilattribute einzubringen, die mit einem Profil in Adobe Experience Platform verknüpft sind und einen Synchronisierungsprozess durchführen, damit sie in der Adobe Campaign-Datenbank aktualisiert werden.

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
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Siehe folgendes Dokument unter [ECID](/help/identity-service/features/ecid.md) für weitere Informationen. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Instanz auswählen]**: Ihr **[!DNL Campaign]** Marketing-Instanz.
* **[!UICONTROL Zielgruppen-Mapping]**: Wählen Sie das Zielgruppen-Mapping aus, das Sie in verwenden **[!DNL Adobe Campaign]** zum Versand. [Weitere Informationen](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Synchronisierungstyp auswählen]**:

   * **[!UICONTROL Zielgruppensynchronisierung]**: Verwenden Sie diese Option, um Adobe Experience Platform-Zielgruppen an Adobe Campaign zu senden.
   * **[!UICONTROL Profilsynchronisierung (nur Aktualisierung)]**: Verwenden Sie diese Option, um Adobe Experience Platform-Profilattribute in Adobe Campaign zu importieren und einen Synchronisierungsprozess einzurichten, damit sie regelmäßig aktualisiert werden können.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Governance-Richtlinie und Durchsetzungsmaßnahmen {#governance}

Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Für Adobe Campaign wird empfohlen, die **[!UICONTROL E-Mail-Targeting]** Marketing-Aktion.

Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Datennutzungsrichtlinien – Übersicht](/help/data-governance/policies/overview.md).

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Lesen [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) für Anweisungen zum Aktivieren von Zielgruppendaten für dieses Ziel.

### Zuordnen von Attributen und Identitäten {#map}

Wählen Sie XDM-Felder aus, die mit den Profilen exportiert werden sollen, und ordnen Sie sie den entsprechenden Adobe Campaign-Feldern zu.[Weitere Informationen zur Auswahl von Identitäts- und Attributen für E-Mail-Marketing-Ziele](overview.md)

1. Quellfelder auswählen:

   * Wählen Sie eine **identifier** (z. B. das E-Mail-Feld) als Quellidentität, die ein Profil in Adobe Experience Platform und Adobe Campaign eindeutig identifiziert.

   * Alle anderen auswählen **XDM-Quellprofilattribute** die nach Adobe Campaign exportiert werden müssen.

   >[!NOTE]
   >
   >Das Feld &quot;segmentMembershipStatus&quot;ist ein erforderliches Mapping, das den Segmentzugehörigkeitsstatus widerspiegelt. Dieses Feld wird standardmäßig hinzugefügt und kann nicht geändert oder entfernt werden.

1. Ordnen Sie jedes Feld dem Zielfeld in Adobe Campaign zu. Die verfügbaren Zielfelder werden durch das beim [Erstellen des Ziels](#destination-details).

1. Identifizieren Sie erforderliche Attribute und Deduplizierungsschlüssel. Beachten Sie, dass Werte in Attributen, die als &quot;Obligatorisch&quot;oder &quot;Deduplizierungsschlüssel&quot;markiert sind, nicht null sein können.

   * [Obligatorische Attribute](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) stellen sicher, dass alle Profildatensätze die ausgewählten Attribute enthalten. Beispiel: Alle exportierten Profile enthalten eine E-Mail-Adresse. Es wird empfohlen, sowohl das Identitätsfeld als auch das als Deduplizierungsschlüssel verwendete Feld als obligatorisch festzulegen.
   * [Deduplizierungsschlüssel](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) ist ein Primärschlüssel, der die Identität bestimmt, anhand derer Benutzer ihre Profile deduplizieren möchten.

     >[!IMPORTANT]
     >
     >Stellen Sie sicher, dass der Name des Deduplizierungsschlüsselattributs mit dem Spaltennamen des ausgewählten Zielgruppen-Mappings übereinstimmt.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Nachdem die Zuordnung durchgeführt wurde, können Sie die Zielkonfiguration überprüfen und abschließen, um mit dem Senden von Daten an zu beginnen. **[!DNL Campaign]**.
   [Erfahren Sie, wie Sie die Zielkonfiguration überprüfen und abschließen](/help/destinations/destination-types.md#review).

## Exportierte Daten/Datenexport validieren {#exported-data}

Nachdem ein Ziel aktiviert wurde, können Sie in Campaign auf den entsprechenden Auftrag und die exportierten Daten zugreifen.

### Überwachen von Datenexportvorgängen {#jobs}

Navigieren Sie zum **[!UICONTROL Administration]** > **[!UICONTROL Prüfung]** > **[!UICONTROL Audience-Ladevorgänge]** -Menü, um alle von Adobe Experience Platform aktivierten Exportvorgänge zu überwachen.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Auf exportierte Daten zugreifen {#data}

Für **[!UICONTROL Zielgruppensynchronisierung]** können Sie die exportierte Zielgruppe überprüfen, indem Sie zu der **[!UICONTROL Profil und Zielgruppe]** > **[!UICONTROL Liste]** > **[!UICONTROL AEP-Zielgruppen]** Menü.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Für **[!UICONTROL Profilsynchronisierung (nur Aktualisierung)]** werden die Daten für jedes Profil, das in das im Ziel aktivierte Segment aufgenommen wird, automatisch in die Campaign-Datenbank aktualisiert.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
