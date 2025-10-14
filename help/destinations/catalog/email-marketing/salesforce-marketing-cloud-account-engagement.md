---
title: Salesforce Marketing Cloud-Kundeninteraktion
description: Erfahren Sie, wie Sie mit dem Ziel Salesforce Marketing Cloud Account Engagement (ehemals Pardot) Ihre Kontodaten exportieren und in Salesforce Marketing Cloud Account Engagement für Ihre Geschäftsanforderungen aktivieren können.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 29%

---

# [!DNL Salesforce Marketing Cloud Account Engagement]-Verbindung

Verwenden Sie das [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(früher als [!DNL Pardot] bezeichnet)* Ziel, um Leads zu erfassen, nachzuverfolgen, zu bewerten und einzustufen. Sie können auch Lead-Tracks für alle Stadien der Pipeline für ausgewählte Markt-Audiences und Kundengruppen erstellen, indem Sie E-Mail-Ablagekampagnen und das Lead-Management mit Pflege, Bewertung und Kampagnensegmentierung nutzen.

Im Vergleich zu [!DNL Salesforce Marketing Cloud Engagement], das stärker auf **B2C**-Marketing ausgerichtet ist, ist [!DNL Marketing Cloud Account Engagement] ideal für **B2B**-Anwendungsfälle, an denen mehrere Abteilungen und Entscheidungsträger beteiligt sind, die längere Verkaufs- und Entscheidungszyklen erfordern. Darüber hinaus pflegen Sie auch eine engere Nähe und Integration mit Ihrem CRM, um geeignete Verkaufs- und Marketingentscheidungen zu treffen. *Beachten Sie, dass Experience Platform auch über Verbindungen für [!DNL Salesforce Marketing Cloud Engagement] verfügt. Sie können diese auf den [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md)- und [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) überprüfen.*

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt den [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email)-Endpunkt, um Ihre Leads **hinzuzufügen oder zu aktualisieren** nachdem sie in einem neuen [!DNL Marketing Cloud Account Engagement] Segment aktiviert wurden.

[!DNL Marketing Cloud Account Engagement] verwendet das OAuth 2-Protokoll mit Autorisierungs-Code , um sich bei der [!DNL Account Engagement]-API zu authentifizieren. Anweisungen zur Authentifizierung bei Ihrer [!DNL Marketing Cloud Account Engagement]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Marketing Cloud Account Engagement]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketing-Kampagnen {#use-case-send-emails}

Die Marketing-Abteilung einer Online-Plattform möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Zielgruppe von B2B-Leads senden. Das Marketing-Team der Plattform kann neue Leads hinzufügen oder bestehende Lead-Informationen über Adobe Experience Platform aktualisieren, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Marketing Cloud Account Engagement] senden, die dann zum Senden der E-Mail mit der Marketing-Kampagne verwendet werden können.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Salesforce] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL Marketing Cloud Account Engagement]-Ziel sammeln müssen.

### Voraussetzungen in Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Marketing Cloud Account Engagement]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen in [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten aus Experience Platform in Ihr [!DNL Marketing Cloud Account Engagement]-Konto zu exportieren:

#### Sie benötigen ein [!DNL Marketing Cloud Account Engagement]-Konto {#prerequisites-account}

Ein [!DNL Marketing Cloud Account Engagement] Konto mit einem Abonnement für das Produkt [Marketing Cloud Account Engagement](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) ist erforderlich, um fortzufahren.

Ihr [!DNL Salesforce]-Konto sollte die [!DNL Salesforce] `Account Engagement Administrator role` haben. Dies ist erforderlich, um [benutzerdefinierte Felder für Interessenten erstellen](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&type=5).

Schließlich sollte Ihr Konto auch in der Lage sein, auf die [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&type=5) zuzugreifen.

Wenden Sie sich an [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) oder Ihren [!DNL Salesforce]-Kontoadministrator, wenn Sie kein Konto haben oder dem Konto das [!DNL Marketing Cloud Account Engagement]-Abonnement oder die [!DNL Account Engagement Administrator role] fehlt.

#### Sammeln von [!DNL Marketing Cloud Account Engagement]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL Marketing Cloud Account Engagement]-Ziel authentifizieren.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Username` | Benutzername Ihres [!DNL Marketing Cloud Account Engagement]. |
| `Password` | Ihr [!DNL Marketing Cloud Account Engagement]-Passwort. |
| `Account Engagement Business Unit ID` | Um die Business Unit-ID für die Kontointeraktion zu finden, verwenden Sie Setup in [!DNL Salesforce]. Geben Sie in „Setup *im Feld „Schnellsuche* „Setup für Geschäftseinheiten“ ein. Ihre Business Unit-ID für die Kontointeraktion beginnt mit `0Uv` und ist 18 Zeichen lang. Wenn Sie nicht auf die Informationen zur Einrichtung der Geschäftseinheit zugreifen können, bitten Sie Ihren [!DNL Salesforce]-Kontoadministrator, Ihnen die `Account Engagement Business Unit ID` zur Verfügung zu stellen. Weitere Anleitungen finden Sie auf der Seite [[!DNL Salesforce] Authentifizierungsrichtlinien](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) . |

{style="table-layout:auto"}

### Leitlinien {#guardrails}

Weitere Informationen finden Sie [!DNL Marketing Cloud Account Engagement] Abschnitt [Ratenbeschränkungen](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) in dem die durch Ihren Plan auferlegten Beschränkungen aufgeführt sind und auch für die Experience Platform-Ausführungen gelten.

>[!IMPORTANT]
>
>Wenn Ihr [!DNL Salesforce]-Kontoadministrator den Zugriff auf vertrauenswürdige IP-Bereiche beschränkt hat, müssen Sie sich an ihn wenden, um [Experience Platform auf die Zulassungsliste setzen IPs](/help/destinations/catalog/streaming/ip-address-allow-list.md) zu erhalten. Weitere Anleitungen finden Sie in der [!DNL Salesforce] [Zugriff auf vertrauenswürdige IP-Bereiche für eine &#x200B;](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) App beschränken“.

## Unterstützte Identitäten {#supported-identities}

[!DNL Marketing Cloud Account Engagement] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adresse des Interessenten | Obligatorisch |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Experience Platform wird der entsprechende [!DNL Salesforce Marketing Cloud Account Engagement] Segmentstatus mit dem Zielgruppenstatus aus Experience Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Salesforce Marketing Cloud Account Engagement]. Alternativ können Sie es unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Sie werden zur Anmeldeseite von [!DNL Salesforce] weitergeleitet. Geben Sie Ihre [!DNL Marketing Cloud Account Engagement] Kontoanmeldeinformationen ein und wählen Sie [!DNL Log In] aus.

Screenshot der ![Experience Platform-Benutzeroberfläche, auf dem die Authentifizierung bei der Marketing Cloud-Kontointeraktion gezeigt wird.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Wählen Sie als Nächstes [!UICONTROL Zulassen] im nachfolgenden Fenster aus, um der **Adobe Experience Platform**-App Berechtigungen für den Zugriff auf Ihr [!DNL Salesforce Marketing Cloud Account Engagement] zu erteilen. *Sie müssen dies nur einmal tun*.

![Bestätigungs-Popup für den Screenshot der Salesforce-App, um der Experience Platform-App Berechtigungen für den Zugriff auf die Marketing Cloud-Kontointeraktion zu erteilen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine Meldung an: *Sie haben erfolgreich eine Verbindung mit dem Salesforce Marketing Cloud-Konto hergestellt*, und eine Meldung **[!UICONTROL Verbunden]** mit einem grünen Häkchen. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist. Eine Anleitung dazu finden [&#x200B; im Abschnitt  [!DNL Marketing Cloud Account Engagement] Sammeln](#gather-credentials)Anmeldeinformationen“.

Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können. |
| **[!UICONTROL Beschreibung]** | Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren. |
| **[!UICONTROL Business Unit-ID für Kontointeraktion]** | Ihre [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Marketing Cloud Account Engagement]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den [!DNL Marketing Cloud Account Engagement]-Zielfeldern korrekt zuzuordnen.

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder den **[!UICONTROL Identity-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Kategorie **[!UICONTROL Identity-Namespace auswählen]** und wählen Sie eine Identität aus oder wählen Sie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie in der Liste der [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) aus dem verfügbaren Schema an.

   * Wiederholen Sie diese Schritte, um alle Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Marketing Cloud Account Engagement] hinzuzufügen:

     | Quellfeld | Zielfeld | Obligatorisch |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Ja |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Nachfolgend finden Sie ein Beispiel mit den oben genannten Zuordnungen:

     Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Ziel-Zuordnungen.![&#128279;](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Navigieren Sie zu einer der ausgewählten Zielgruppen. Wählen Sie die Registerkarte **[!DNL Activation data]** aus. Die Spalte **[!UICONTROL Zuordnungs]** zeigt den Namen des benutzerdefinierten Felds an, das innerhalb der [!DNL Marketing Cloud Account Engagement Prospects] generiert wird.
   Beispiel-Screenshot der ![Experience Platform-Benutzeroberfläche mit der Zuordnungs-ID für ein ausgewähltes Segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Melden Sie sich bei der [[!DNL Salesforce]](https://login.salesforce.com/)-Website an. Navigieren Sie dann zur Seite **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** und überprüfen Sie, ob die potenziellen Kunden aus der Audience hinzugefügt/aktualisiert wurden. Alternativ können Sie auch auf [[!DNL Salesforce Pardot]](https://pi.pardot.com/) und die **[!DNL Prospects]** zugreifen.
   ![Screenshot der Salesforce-Benutzeroberfläche mit der Seite „Interessenten“.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Um zu überprüfen, ob die Interessenten aktualisiert wurden, wählen Sie einen Interessenten aus und überprüfen Sie, ob das benutzerdefinierte Feld des Interessenten mit dem Zielgruppenstatus von Experience Platform aktualisiert wurde.
   ![Screenshot der Salesforce-Benutzeroberfläche mit der ausgewählten Interessentenseite. Das benutzerdefinierte Feld des Interessenten wird mit dem Zielgruppenstatus aktualisiert.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
