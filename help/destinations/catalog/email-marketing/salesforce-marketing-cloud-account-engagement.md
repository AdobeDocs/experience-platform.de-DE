---
title: Kundenkontointeraktion in Salesforce Marketing Cloud
description: Erfahren Sie, wie Sie mit dem Salesforce Marketing Cloud Account Engagement (ehemals Pardot)-Ziel Ihre Kontodaten exportieren und innerhalb der Salesforce Marketing Cloud Account Engagement für Ihre Geschäftsanforderungen aktivieren können.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 30%

---

# [!DNL Salesforce Marketing Cloud Account Engagement]-Verbindung

Verwenden Sie das Ziel [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(ehemals [!DNL Pardot])*, um Leads zu erfassen, zu verfolgen, zu bewerten und zu bewerten. Sie können auch Lead-Tracks für alle Phasen der Pipeline für zielgerichtete Marktzielgruppen und Kundengruppen über E-Mail-Drip-Kampagnen und Lead-Management mit Pflege-, Scoring- und Kampagnensegmentierung erstellen.

Im Vergleich zu [!DNL Salesforce Marketing Cloud Engagement] , das stärker auf das **B2C**-Marketing ausgerichtet ist, ist [!DNL Marketing Cloud Account Engagement] ideal für **B2B**-Anwendungsfälle, an denen mehrere Abteilungen und Entscheidungsträger beteiligt sind, die längere Verkaufs- und Entscheidungszyklen benötigen. Zusätzlich erhalten Sie eine engere Nähe und Integration in Ihr CRM, um geeignete Verkaufs- und Marketingentscheidungen treffen zu können. *Beachten Sie, dass Experience Platform auch Verbindungen für [!DNL Salesforce Marketing Cloud Engagement] hat, können Sie sie auf den Seiten [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) und [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) überprüfen.*

Dieses [!DNL Adobe Experience Platform] [ Ziel](/help/destinations/home.md) nutzt den [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) -Endpunkt, um **Ihre Leads hinzuzufügen oder zu aktualisieren** , nachdem sie in einem neuen [!DNL Marketing Cloud Account Engagement] -Segment aktiviert wurden.

[!DNL Marketing Cloud Account Engagement] verwendet das OAuth 2-Protokoll mit Autorisierungscode , um sich bei der [!DNL Account Engagement]-API zu authentifizieren. Anweisungen zur Authentifizierung bei Ihrer [!DNL Marketing Cloud Account Engagement]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Marketing Cloud Account Engagement]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Marketingabteilung einer Online-Plattform möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Audience von B2B-Leads senden. Das Marketing-Team der Plattform kann neue Leads hinzufügen oder vorhandene Lead-Informationen über Adobe Experience Platform aktualisieren, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Marketing Cloud Account Engagement] senden, die dann zum Senden der E-Mail-Adresse der Marketing-Kampagne verwendet werden können.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Salesforce] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL Marketing Cloud Account Engagement]-Ziel erfassen müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Marketing Cloud Account Engagement]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen in [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihr [!DNL Marketing Cloud Account Engagement] -Konto zu exportieren:

#### Sie benötigen ein [!DNL Marketing Cloud Account Engagement]-Konto {#prerequisites-account}

Um fortzufahren, ist ein [!DNL Marketing Cloud Account Engagement] -Konto mit einem Abonnement für das Marketing Cloud [Interaktion mit Kundenkonto](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) erforderlich.

Ihr [!DNL Salesforce]-Konto sollte die [!DNL Salesforce] `Account Engagement Administrator role` aufweisen. Dies ist erforderlich, um [benutzerdefinierte Interessensfelder erstellen](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Schließlich sollte Ihr Konto auch auf den [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5) zugreifen können.

Wenden Sie sich an den [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) oder Ihren [!DNL Salesforce] -Kontoadministrator, wenn Sie kein Konto haben oder das Konto das [!DNL Marketing Cloud Account Engagement]-Abonnement oder den [!DNL Account Engagement Administrator role] fehlt.

#### Sammeln von [!DNL Marketing Cloud Account Engagement]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich beim [!DNL Marketing Cloud Account Engagement]-Ziel authentifizieren.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Username` | Ihr [!DNL Marketing Cloud Account Engagement] -Konto-Benutzername. |
| `Password` | Ihr [!DNL Marketing Cloud Account Engagement] Kontokennwort. |
| `Account Engagement Business Unit ID` | Um die Kennung der Geschäftseinheit für Kontointeraktion zu ermitteln, verwenden Sie Einrichtung in [!DNL Salesforce]. Geben Sie unter &quot;Einrichtung&quot;im Feld &quot;Schnellsuche&quot;den Eintrag *Einrichtung der Geschäftseinheit* ein. Ihre Business Unit-ID für Kontointeraktion beginnt mit `0Uv` und ist 18 Zeichen lang. Wenn Sie nicht auf die Informationen zur Einrichtung der Geschäftseinheit zugreifen können, bitten Sie Ihren [!DNL Salesforce] -Kontoadministrator, Ihnen die `Account Engagement Business Unit ID` anzugeben. Wenn Sie zusätzliche Anleitungen benötigen, lesen Sie die Leitlinie zu [[!DNL Salesforce] Authentifizierung](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) . |

{style="table-layout:auto"}

### Leitplanken {#guardrails}

Beachten Sie die [!DNL Marketing Cloud Account Engagement] [Ratenbeschränkungen](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) , in denen die durch Ihren Plan festgelegten Beschränkungen aufgeführt sind und die auch für die Experience Platform-Ausführungen gelten würden.

>[!IMPORTANT]
>
>Wenn Ihr [!DNL Salesforce] -Kontoadministrator eingeschränkten Zugriff auf vertrauenswürdige IP-Bereiche hat, müssen Sie ihn kontaktieren, damit die [Experience Platform IP&#39;s](/help/destinations/catalog/streaming/ip-address-allow-list.md)-Adresse auf die Zulassungsliste gesetzt wird. Weitere Informationen finden Sie in der Dokumentation [!DNL Salesforce] [Beschränken des Zugriffs auf vertrauenswürdige IP-Bereiche für eine Connected App](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) .

## Unterstützte Identitäten {#supported-identities}

[!DNL Marketing Cloud Account Engagement] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | Prospect Email Address | Obligatorisch |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird der entsprechende Segmentstatus [!DNL Salesforce Marketing Cloud Account Engagement] mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Salesforce Marketing Cloud Account Engagement]. Alternativ können Sie ihn unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Sie werden zur Anmeldeseite [!DNL Salesforce] navigiert. Geben Sie Ihre [!DNL Marketing Cloud Account Engagement] -Kontoanmeldeinformationen ein und wählen Sie [!DNL Log In] aus.

![Screenshot der Platform-Benutzeroberfläche, in dem gezeigt wird, wie die Authentifizierung für die Interaktion mit Marketing Cloud-Konten erfolgt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Wählen Sie anschließend [!UICONTROL Zulassen] im nachfolgenden Fenster aus, um der **Adobe Experience Platform**-App Berechtigungen für den Zugriff auf Ihr [!DNL Salesforce Marketing Cloud Account Engagement]-Konto zu erteilen. *Sie müssen dies nur einmal tun*.

![Salesforce App-Screenshot-Bestätigungs-Popup, um der Experience Platform-App Zugriff auf die Marketing Cloud-Kontointeraktion zu gewähren.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine Meldung an: *Sie haben eine erfolgreiche Verbindung zum Salesforce Marketing Cloud Account Engagement Account Account Account Account Account Account Interaction account* und ein **[!UICONTROL Connected]** -Status mit einem grünen Häkchen, Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist. Eine Anleitung finden Sie im Abschnitt [Anmeldedaten sammeln [!DNL Marketing Cloud Account Engagement] 2} .](#gather-credentials)

![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden. |
| **[!UICONTROL Beschreibung]** | Eine Beschreibung, die Ihnen bei der Identifizierung dieses Ziels in der Zukunft hilft. |
| **[!UICONTROL Kennung der Geschäftseinheit Kontointeraktion]** | Ihr [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Marketing Cloud Account Engagement]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den [!DNL Marketing Cloud Account Engagement] -Zielfeldern zuzuordnen.

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** aus, wählen Sie das XDM-Attribut aus oder wählen Sie den Eintrag **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** den Eintrag **[!UICONTROL Identitäts-Namespace auswählen]** aus, wählen Sie eine Identität aus oder wählen Sie die Kategorie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie in der Liste von [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) aus dem verfügbaren Schema an.

   * Wiederholen Sie diese Schritte, um Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Marketing Cloud Account Engagement] hinzuzufügen:

     | Quellfeld | Zielfeld | Obligatorisch |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Ja |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Nachfolgend finden Sie ein Beispiel mit den oben aufgeführten Zuordnungen:
     ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnungen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Navigieren Sie zu einer der Zielgruppen, die Sie ausgewählt haben. Wählen Sie die Registerkarte **[!DNL Activation data]** aus. In der Spalte **[!UICONTROL Zuordnungs-ID]** wird der Name des benutzerdefinierten Felds angezeigt, das auf der Seite [!DNL Marketing Cloud Account Engagement Prospects] generiert wird.
   ![Screenshot der Platform-Benutzeroberfläche mit der Zuordnungs-ID für ein ausgewähltes Segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Melden Sie sich bei der Website [[!DNL Salesforce]](https://login.salesforce.com/) an. Navigieren Sie dann zur Seite **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** und überprüfen Sie, ob die Interessenten aus der Zielgruppe hinzugefügt/aktualisiert wurden. Alternativ können Sie auch auf [[!DNL Salesforce Pardot]](https://pi.pardot.com/) und die Seite **[!DNL Prospects]** zugreifen.
   ![Salesforce UI-Screenshot mit der Seite &quot;Perspektiven&quot;.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Um zu überprüfen, ob die Interessenten aktualisiert wurden, wählen Sie einen Interessenten aus und überprüfen Sie, ob das benutzerdefinierte Interessensfeld mit dem Zielgruppenstatus Experience Platform aktualisiert wurde.
   ![Salesforce UI-Screenshot mit der ausgewählten Interessensseite. Das benutzerdefinierte Interessensfeld wird mit dem Zielgruppenstatus aktualisiert.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-Dokumentation](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
