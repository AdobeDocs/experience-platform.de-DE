---
title: Mailchimp-Tags
description: Das Mailchimp Tags -Ziel ermöglicht es Ihnen, Ihre Kontodaten zu exportieren und in Mailchimp zu aktivieren, um mit Kontakten zu interagieren.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 24%

---

# [!DNL Mailchimp Tags]-Verbindung

[[!DNL Mailchimp]](https://mailchimp.com) *(auch als [!DNL Intuit Mailchimp] bezeichnet)* ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, der von Unternehmen verwendet wird, um Kontakte zu verwalten und mit *(Kunden, Kunden oder anderen interessierten Parteien)* mithilfe von Mailinglisten und E-Mail-Marketing-Kampagnen zu kommunizieren.

[!DNL Mailchimp Tags] verwendet [Audiences](https://mailchimp.com/help/getting-started-audience/) und [Tags](https://mailchimp.com/help/getting-started-tags/), um Ihre Kontaktinformationen zu verwalten. Tags sind Kennzeichnungen, mit denen Sie Ihre Kontakte organisieren und für Ihre interne Kategorisierung in [!DNL Mailchimp] kennzeichnen können.

Im Gegensatz zu [!DNL Mailchimp Interest Categories], mit denen Sie Ihre Kontakte nach ihren Interessen und Vorlieben sortieren würden, soll [!DNL Mailchimp Tags] Abonnements für Themen verwalten, die für Ihre Kontakte von Interesse sein könnten. *Beachten Sie, dass Experience Platform auch eine Verbindung für [!DNL Mailchimp Interest Categories] hat. Sie können sie auf der [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) auschecken.*

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt den [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/). Sie können **neue Kontakte hinzufügen** oder **Tags vorhandener [!DNL Mailchimp] Kontakte aktualisieren** innerhalb einer bestehenden [!DNL Mailchimp] Zielgruppe, nachdem Sie sie in einer neuen Zielgruppe aktiviert haben. [!DNL Mailchimp Tags] verwendet die ausgewählten Zielgruppennamen aus Experience Platform als Tag-Namen in [!DNL Mailchimp].

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Mailchimp Tags]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketing-Kampagnen {#use-case-send-emails}

Die Verkaufsabteilung eines Unternehmens möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Kontaktliste senden. Die Kontaktlisten werden stapelweise von verschiedenen Offline-Quellen empfangen und müssen daher verfolgt werden. Das Team identifiziert eine bestehende [!DNL Mailchimp]-Zielgruppe und beginnt mit der Erstellung der Experience Platform-Zielgruppen, denen die Kontakte aus jeder Liste hinzugefügt werden. Wenn diese Zielgruppen nach dem Senden an [!DNL Mailchimp Tags] in der ausgewählten [!DNL Mailchimp]-Zielgruppe keine Kontakte vorhanden sind, werden sie mit einem zugehörigen Tag hinzugefügt, das den Zielgruppennamen enthält, zu dem der Kontakt gehört. Wenn in der [!DNL Mailchimp] Zielgruppe bereits Kontakte vorhanden sind, wird ein neues Tag mit dem Namen der Zielgruppe hinzugefügt. Da die Kennzeichnungen in [!DNL Mailchimp] sichtbar sind, können die Offline-Quellen leicht identifiziert werden. Nachdem die Daten an [!DNL Mailchimp] gesendet wurden, senden sie die E-Mail zur Marketing-Kampagne an die Audience.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Mailchimp] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL Mailchimp Tags]-Ziel sammeln müssen.

### Voraussetzungen in Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das [!DNL Mailchimp Tags]-Ziel aktivieren, müssen Sie ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Audiences](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) in [!DNL Experience Platform] erstellt haben.

### Voraussetzungen für das [!DNL Mailchimp Tags] Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten aus Experience Platform in Ihr [!DNL Mailchimp Tags]-Konto zu exportieren:

#### Sie benötigen ein [!DNL Mailchimp]-Konto {#prerequisites-account}

Bevor Sie ein [!DNL Mailchimp Tags] Ziel erstellen können, müssen Sie zunächst sicherstellen, dass Sie über ein [!DNL Mailchimp] verfügen. Wenn Sie noch keine haben, besuchen Sie die [[!DNL Mailchimp] Anmeldeseite](https://login.mailchimp.com/signup/) um sich zu registrieren und Ihr Konto zu erstellen.

#### Erfassen [!DNL Mailchimp] API-Schlüssels {#gather-credentials}

Sie benötigen Ihren [!DNL Mailchimp] **API-Schlüssel**, um das [!DNL Mailchimp Interest Categories]-Ziel für Ihr [!DNL Mailchimp]-Konto zu authentifizieren. Der **API-Schlüssel** dient als **Kennwort** wenn Sie [das Ziel authentifizieren](#authenticate).

Wenn Sie nicht über Ihren **API-Schlüssel** verfügen, melden Sie sich bei Ihrem [!DNL Mailchimp]-Konto an und lesen Sie die [!DNL Mailchimp]-Dokumentation unter [So generieren Sie Ihren API-Schlüssel](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Ein Beispiel für einen API-Schlüssel ist `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Wenn Sie den **API-Schlüssel** generieren, schreiben Sie ihn auf, da Sie nach der Generierung nicht mehr darauf zugreifen können.

#### Identifizieren des [!DNL Mailchimp] Rechenzentrums {#identify-data-center}

Als Nächstes müssen Sie Ihr [!DNL Mailchimp] Rechenzentrum identifizieren. Melden Sie sich dazu bei Ihrem [!DNL Mailchimp]-Konto an und navigieren Sie zum Abschnitt **API-Schlüssel** Ihres Kontos.

Die Datenzentrum-ID ist der erste Abschnitt der URL, die Sie in Ihrem Browser sehen. Wenn die URL *https://`us14`.mailchimp.com/account/api/* lautet, wird das Rechenzentrum `us14`.

Die Rechenzentrum-ID wird auch in der Form *key-dc* an Ihren API-Schlüssel angehängt. Wenn beispielsweise Ihr API-Schlüssel `0123456789abcdef0123456789abcde-us14` ist, wird das Rechenzentrum `us14`.

Notieren Sie sich den *des Rechenzentrums (`us14` in diesem Beispiel)*. Sie benötigen diesen Wert, wenn Sie [die Zieldetails angeben](#destination-details).

Weitere Anleitungen finden Sie in der Dokumentation zu [[!DNL Mailchimp] Grundlagen](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Leitlinien {#guardrails}

Siehe [!DNL Mailchimp]Ratenbeschränkungen[&#x200B; für &#x200B;](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) Informationen zu den Beschränkungen, die durch die [!DNL Mailchimp]-API auferlegt werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Mailchimp] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | Die E-Mail-Adresse des Kontakts. | Obligatorisch |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *z. B. E-Mail-Adresse, Telefonnummer, Nachname)* entsprechend Ihrer Feldzuordnung.</li><li> Für jede in Experience Platform ausgewählte Zielgruppe wird der entsprechende [!DNL Mailchimp Tags] Segmentstatus mit dem Zielgruppenstatus aus Experience Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Manage Destinations]** [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** nach [!DNL Mailchimp Tags]. Alternativ können Sie es unter der Kategorie **[!UICONTROL Email marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Username]** | Ihr [!DNL Mailchimp]. |
| **[!UICONTROL Password]** | Ihr [!DNL Mailchimp] **API-**), den Sie im Abschnitt [Sammeln [!DNL Mailchimp] Anmeldeinformationen](#gather-credentials) notiert hatten.<br> Ihr API-Schlüssel hat die Form von `{KEY}-{DC}`, wobei der `{KEY}` Teil auf den Wert verweist, der im Abschnitt [[!DNL Mailchimp] API-Schlüssel](#gather-credentials) angegeben ist, und der `{DC}` Teil auf das [[!DNL Mailchimp] Rechenzentrum](#identify-data-center). <br>Sie können entweder den `{KEY}` Teil oder das gesamte Formular angeben.<br> Wenn Ihr API-Schlüssel beispielsweise <br>*`0123456789abcdef0123456789abcde-us14`*ist, können <br> entweder *`0123456789abcdef0123456789abcde`*oder *`0123456789abcdef0123456789abcde-us14`*als Wert angeben. |

{style="table-layout:auto"}

Screenshot der ![Experience Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche einen **[!UICONTROL Connected]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können. |
| **[!UICONTROL Description]** | Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren. |
| **[!UICONTROL Data center]** | Ihr [!DNL Mailchimp]-Konto `data center`. Eine Anleitung dazu finden [&#x200B; im Abschnitt  [!DNL Mailchimp] Identifizieren](#identify-data-center)Datenzentrum“. |
| **[!UICONTROL Audience Name (Please enter Data center first)]** | Nachdem Sie Ihre **[!UICONTROL Data center]** eingegeben haben, wird dieses Dropdown-Menü automatisch mit den Zielgruppennamen aus Ihrem [!DNL Mailchimp]-Konto gefüllt. Wählen Sie die Zielgruppe aus, die Sie mit Daten aus Experience Platform aktualisieren möchten. |

{style="table-layout:auto"}

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) unter Aktivieren von Zielgruppen für Streaming-Ziele .

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Mailchimp Tags]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den [!DNL Mailchimp Tags]-Zielfeldern korrekt zuzuordnen:

1. Wählen Sie im **[!UICONTROL Mapping]** Schritt **[!UICONTROL Add new mapping]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im **[!UICONTROL Select source field]** die Option **[!UICONTROL Select identity namespace]** und wählen Sie den `Email` Identity-Namespace aus.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit dem Feld &quot;Source&quot; als E-Mail aus dem Identity-Namespace.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. Wählen Sie im **[!UICONTROL Select target field]** die Option **[!UICONTROL Select identity namespace]** und wählen Sie den `Email` Identity-Namespace aus.

   Screenshot der ![Experience Platform-Benutzeroberfläche mit dem Zielfeld als E-Mail aus dem Identity-Namespace.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Die Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Mailchimp Tags] lauten wie folgt:

   | Quellfeld | Zielfeld | Obligatorisch |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | Ja |

   Nachfolgend finden Sie ein Beispiel mit den abgeschlossenen Zuordnungen:
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Feldzuordnungen.![](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Melden Sie sich bei Ihrem [[!DNL Mailchimp]](https://login.mailchimp.com/) an. Navigieren Sie dann zur Seite **[!DNL Audience]** > **[!DNL All Contacts]** und überprüfen Sie, ob die Kontakte aus der Audience hinzugefügt und die Kontakte in der Audience mit dem Audience-Namen aktualisiert wurden.
   ![Screenshot der Mailchimp-Benutzeroberfläche mit der Seite „Zielgruppe“.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Auf der [[!DNL Mailchimp] Fehlerseite](https://mailchimp.com/developer/marketing/docs/errors/) finden Sie eine umfassende Liste von Status- und Fehler-Codes mit Erläuterungen.

## Weitere Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Mailchimp] Dokumentation finden Sie unten:

* [Erste Schritte mit [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Erste Schritte mit Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Zielgruppe erstellen](https://mailchimp.com/help/create-audience/)
* [Erste Schritte mit Tags](https://mailchimp.com/help/getting-started-tags/)
* [Marketing-API](https://mailchimp.com/developer/marketing/api/)
