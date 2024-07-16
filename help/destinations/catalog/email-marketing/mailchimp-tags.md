---
title: Mailchimp-Tags
description: Mit dem Ziel Mailchimp Tags können Sie Ihre Kontodaten exportieren und in Mailchimp aktivieren, um Kontakte zu gewinnen.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 27%

---

# [!DNL Mailchimp Tags]-Verbindung

[[!DNL Mailchimp]](https://mailchimp.com) *(auch als [!DNL Intuit Mailchimp] bezeichnet)* ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, die von Unternehmen verwendet werden, um *(Kunden, Kunden oder sonstige interessierte Parteien) zu verwalten und mit ihnen über Mailinglisten und E-Mail-Marketing-Kampagnen zu kommunizieren.*

[!DNL Mailchimp Tags] verwendet [Audiences](https://mailchimp.com/help/getting-started-audience/) und [Tags](https://mailchimp.com/help/getting-started-tags/), um Ihre Kontaktinformationen zu verwalten. Tags sind Bezeichnungen, mit denen Sie Ihre Kontakte organisieren und für Ihre interne Kategorisierung in [!DNL Mailchimp] kennzeichnen können.

Im Vergleich zu [!DNL Mailchimp Interest Categories] , mit dem Sie Ihre Kontakte nach ihren Interessen und Vorlieben sortieren würden, ist [!DNL Mailchimp Tags] zur Verwaltung von Anmeldungen zu Themen gedacht, die für Ihre Kontakte von Interesse sein könnten. *Beachten Sie, dass Experience Platform auch eine Verbindung für [!DNL Mailchimp Interest Categories] hat, können Sie sie auf der [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md)-Seite auschecken.*

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt den [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) -Endpunkt. Sie können **neue Kontakte hinzufügen** oder **Tags vorhandener [!DNL Mailchimp] Kontakte** in einer vorhandenen [!DNL Mailchimp]-Zielgruppe aktualisieren, nachdem Sie sie in einer neuen Zielgruppe aktiviert haben. [!DNL Mailchimp Tags] verwendet die ausgewählten Zielgruppennamen aus Platform als Tag-Namen in [!DNL Mailchimp].

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Mailchimp Tags]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Vertriebsabteilung einer Organisation möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Kontaktliste senden. Die Kontaktlisten werden in Stapeln aus verschiedenen Offline-Quellen empfangen und müssen daher verfolgt werden. Das Team identifiziert eine vorhandene [!DNL Mailchimp] -Zielgruppe und beginnt mit der Erstellung der Experience Platform-Zielgruppen, in die die Kontakte aus den einzelnen Listen aufgenommen werden. Nachdem diese Zielgruppen an [!DNL Mailchimp Tags] gesendet wurden und in der ausgewählten [!DNL Mailchimp] -Zielgruppe keine Kontakte vorhanden sind, werden sie mit einem zugehörigen Tag hinzugefügt, das den Zielgruppennamen enthält, zu dem der Kontakt gehört. Wenn bereits Kontakte in der [!DNL Mailchimp] -Audience vorhanden sind, wird ein neues Tag mit dem Namen der Audience hinzugefügt. Da die Beschriftungen in [!DNL Mailchimp] sichtbar sind, können die Offline-Quellen leicht identifiziert werden. Nachdem die Daten an [!DNL Mailchimp] gesendet wurden, senden sie die E-Mail der Marketing-Kampagne an die Audience.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Mailchimp] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL Mailchimp Tags]-Ziel erfassen müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Ziel [!DNL Mailchimp Tags] aktivieren, müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Zielgruppen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen für das [!DNL Mailchimp Tags]-Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihr [!DNL Mailchimp Tags] -Konto zu exportieren:

#### Sie benötigen ein [!DNL Mailchimp]-Konto {#prerequisites-account}

Bevor Sie ein [!DNL Mailchimp Tags] -Ziel erstellen können, müssen Sie zunächst sicherstellen, dass Sie über ein [!DNL Mailchimp] -Konto verfügen. Wenn Sie noch keinen haben, rufen Sie die [[!DNL Mailchimp] Anmeldeseite](https://login.mailchimp.com/signup/) auf, um sich zu registrieren und Ihr Konto zu erstellen.

#### Sammeln von [!DNL Mailchimp] API-Schlüssel {#gather-credentials}

Sie benötigen Ihren [!DNL Mailchimp] **API-Schlüssel**, um das [!DNL Mailchimp Interest Categories]-Ziel für Ihr [!DNL Mailchimp]-Konto zu authentifizieren. Der **API-Schlüssel** dient als **Kennwort**, wenn Sie [das Ziel authentifizieren](#authenticate).

Wenn Sie nicht über Ihren **API-Schlüssel** verfügen, melden Sie sich bei Ihrem [!DNL Mailchimp]-Konto an und lesen Sie die [!DNL Mailchimp]-Dokumentation unter [, wie Sie Ihren API-Schlüssel generieren](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Ein Beispiel für einen API-Schlüssel ist `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Wenn Sie den **API-Schlüssel** generieren, schreiben Sie ihn auf, da Sie nach der Generierung nicht mehr darauf zugreifen können.

#### Identifizieren des [!DNL Mailchimp]-Rechenzentrums {#identify-data-center}

Als Nächstes müssen Sie Ihr [!DNL Mailchimp] -Rechenzentrum identifizieren. Melden Sie sich dazu bei Ihrem [!DNL Mailchimp] -Konto an und navigieren Sie zum Abschnitt **API-Schlüssel** Ihres Kontos.

Die Rechenzentrum-ID ist der erste Abschnitt der URL, die im Browser angezeigt wird. Wenn die URL *https://`us14`.mailchimp.com/account/api/* ist, ist das Rechenzentrum `us14`.

Die Rechenzentrum-ID wird auch im Format *key-dc* an Ihren API-Schlüssel angehängt. Wenn Ihr API-Schlüssel beispielsweise `0123456789abcdef0123456789abcde-us14` ist, ist das Rechenzentrum `us14`.

Notieren Sie den Rechenzentrumswert *(`us14` in diesem Beispiel)*. Sie benötigen diesen Wert, wenn Sie [die Zieldetails ausfüllen](#destination-details).

Wenn Sie weitere Anleitungen benötigen, lesen Sie die [[!DNL Mailchimp] Grundlagendokumentation](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Leitplanken {#guardrails}

Detaillierte Informationen zu den Beschränkungen, die durch die [!DNL Mailchimp] -API auferlegt werden, finden Sie unter [!DNL Mailchimp] [Ratenbeschränkungen](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) .

## Unterstützte Identitäten {#supported-identities}

[!DNL Mailchimp] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | Die E-Mail-Adresse des Kontakts. | Obligatorisch |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *(z. B. E-Mail-Adresse, Telefonnummer, Nachname)* gemäß Ihrer Feldzuordnung.</li><li> Für jede in Platform ausgewählte Zielgruppe wird der entsprechende Segmentstatus [!DNL Mailchimp Tags] mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Mailchimp Tags]. Alternativ können Sie ihn unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Benutzername]** | Ihr [!DNL Mailchimp] Benutzername. |
| **[!UICONTROL Passwort]** | Ihr [!DNL Mailchimp] **API-Schlüssel**, den Sie im Abschnitt [Anmeldedaten des Zusammenführers [!DNL Mailchimp] eingegeben haben](#gather-credentials) notiert haben.<br> Ihr API-Schlüssel hat die Form &quot;`{KEY}-{DC}`&quot;, wobei der &quot;`{KEY}`&quot;-Teil auf den im Abschnitt &quot;[[!DNL Mailchimp] API-Schlüssel](#gather-credentials)&quot; verzeichneten Wert verweist und der &quot;`{DC}`&quot;-Teil auf das &quot;[[!DNL Mailchimp] Rechenzentrum](#identify-data-center)&quot;. <br>Sie können entweder den Abschnitt `{KEY}` oder das gesamte Formular angeben.<br> Wenn Ihr API-Schlüssel beispielsweise <br>*`0123456789abcdef0123456789abcde-us14`*, <br> ist, können Sie entweder *`0123456789abcdef0123456789abcde`*oder *`0123456789abcdef0123456789abcde-us14`*als Wert angeben. |

{style="table-layout:auto"}

![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden. |
| **[!UICONTROL Beschreibung]** | Eine Beschreibung, die Ihnen bei der Identifizierung dieses Ziels in der Zukunft hilft. |
| **[!UICONTROL Rechenzentrum]** | Ihr [!DNL Mailchimp] Konto `data center`. Eine Anleitung dazu finden Sie im Abschnitt [Identifizieren [!DNL Mailchimp] des Rechenzentrums](#identify-data-center) . |
| **[!UICONTROL Zielgruppenname (Bitte geben Sie zuerst Data Center ein)]** | Nach Eingabe Ihres **[!UICONTROL Rechenzentrums]** wird dieses Dropdown-Menü automatisch mit den Zielgruppennamen aus Ihrem [!DNL Mailchimp] -Konto gefüllt. Wählen Sie die Zielgruppe aus, die mit Daten aus Platform aktualisiert werden soll. |

{style="table-layout:auto"}

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppen für Streaming-Ziele](/help/destinations/ui/activate-segment-streaming-destinations.md) .

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Mailchimp Tags]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den [!DNL Mailchimp Tags] -Zielfeldern zuzuordnen:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Option **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie den Identitäts-Namespace `Email` aus.

   ![Screenshot der Platform-Benutzeroberfläche mit Source-Feld als E-Mail aus dem Identitäts-Namespace.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Option **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie den Identitäts-Namespace `Email` aus.

   ![Screenshot der Platform-Benutzeroberfläche mit dem Target-Feld als E-Mail aus dem Identitäts-Namespace.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Die Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Mailchimp Tags] lauten wie folgt:
| Source Field | Zielfeld | Obligatorisch |
| — | — | — |
|`IdentityMap: Email`|`Identity: Email`| Ja |

   Nachfolgend finden Sie ein Beispiel mit den abgeschlossenen Zuordnungen:
   ![Screenshot der Platform-Benutzeroberfläche mit Feldzuordnungen.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Melden Sie sich bei Ihrem [[!DNL Mailchimp]](https://login.mailchimp.com/) -Konto an. Navigieren Sie dann zur Seite **[!DNL Audience]** > **[!DNL All Contacts]** und überprüfen Sie, ob die Kontakte aus der Audience hinzugefügt und die Kontakte innerhalb der Audience mit dem Zielgruppennamen aktualisiert wurden.
   ![Mailchimp UI-Screenshot mit der Seite &quot;Zielgruppe&quot;.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Eine umfassende Liste der Status- und Fehlercodes mit Erläuterungen finden Sie auf der [[!DNL Mailchimp] Fehlerseite](https://mailchimp.com/developer/marketing/docs/errors/) .

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Mailchimp] -Dokumentation finden Sie unten:
* [Erste Schritte mit  [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Erste Schritte mit Zielgruppen](https://mailchimp.com/help/getting-started-audience/)
* [Erstellen einer Zielgruppe](https://mailchimp.com/help/create-audience/)
* [Erste Schritte mit Tags](https://mailchimp.com/help/getting-started-tags/)
* [Marketing-API](https://mailchimp.com/developer/marketing/api/)
