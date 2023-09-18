---
title: Mailchimp-Interessenkategorien
description: Mailchimp (auch Intuit Mailchimp genannt) ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, die von Unternehmen verwendet werden, um Kontakte (Kunden, Kunden oder andere interessierte Parteien) mithilfe von Mailinglisten und E-Mail-Marketing-Kampagnen zu verwalten und mit ihnen zu kommunizieren. Verwenden Sie diesen Connector, um Ihre Kontakte nach deren Interessen und Präferenzen zu sortieren.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 23%

---

# [!DNL Mailchimp Interest Categories]-Verbindung

[[!DNL Mailchimp]](https://mailchimp.com) ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, der von Unternehmen zur Verwaltung und Kommunikation von Kontakten verwendet wird. *(Kunden, Kunden oder sonstige interessierte Parteien)* Verwendung von Mailinglisten und E-Mail-Marketing-Kampagnen. Verwenden Sie diesen Connector, um Ihre Kontakte nach deren Interessen und Präferenzen zu sortieren.

[!DNL Mailchimp Interest Categories] uses [Zielgruppen](https://mailchimp.com/help/getting-started-audience/), [Gruppen](https://mailchimp.com/help/getting-started-with-groups/), Interessenkategorien *(auch als Gruppennamen oder Gruppentitel bezeichnet)*. Jeder [!DNL Mailchimp] -Gruppe ist eine Liste von Interessenkategorien. Kontakte werden einer Interessenkategorie zugeordnet, wenn sie über ein Anmeldeformular auf Ihrer Website eine oder mehrere Interessenskategorien abonnieren. Innerhalb einer Zielgruppe können Sie die Kontakte auch in Gruppen organisieren und sie Interessenkategorien zuordnen. Diese können dann zur Erstellung von Segmenten verwendet werden. Sie können diese Zielgruppen verwenden, um zielgerichtete Kampagnen-E-Mails an die angemeldeten Kontakte zu senden.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) verwendet die [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API zum Erstellen [Interessenkategorien](https://mailchimp.com/developer/marketing/api/interest-categories/) und fügen dann Kontakte aus den ausgewählten Platform-Audiences in eine entsprechende Interessenkategorie ein. Sie können **neue Kontakte hinzufügen** oder **Aktualisierung vorhandener Informationen [!DNL Mailchimp] contact**, dann **sie zu den gewünschten Gruppen hinzufügen oder daraus entfernen** innerhalb eines vorhandenen [!DNL Mailchimp] Zielgruppe, nachdem sie in einem neuen Segment aktiviert wurden. [!DNL Mailchimp Interest Groups] verwendet die ausgewählten Zielgruppennamen aus Platform als Interessenkategorien in [!DNL Mailchimp].

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Mailchimp Interest Categories]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Verkaufsabteilung einer Sportartikelwebsite möchte eine E-Mail-basierte Marketing-Kampagne an eine Liste von Kontakten senden, die sich selbst als an Fußball interessiert identifiziert haben. Die Kontaktlisten werden als Batches im Datenexport getrennt, die vom Entwicklungsteam der Website empfangen wurden, und müssen daher verfolgt werden. Das Team identifiziert ein vorhandenes [!DNL Mailchimp] und beginnt mit der Erstellung der Experience Platform-Audiences, in die die Kontakte aus den einzelnen Listen aufgenommen werden. Nach dem Senden dieser Zielgruppen an [!DNL Mailchimp Interest Categories], wenn in der ausgewählten Option keine Kontakte vorhanden sind [!DNL Mailchimp] Zielgruppe hinzugefügt werden, wird sie einer Gruppe mit dem Zielgruppennamen hinzugefügt, zu dem der Kontakt gehört. Wenn bereits Kontakte im [!DNL Mailchimp] Zielgruppe oder Gruppe erstellen, werden deren Informationen aktualisiert. Sobald die Daten an [!DNL Mailchimp Interest Categories]kann das Sales-Team die Marketing-Kampagnen-E-Mail auswählen und an die Fußball-Interessengruppe innerhalb der [!DNL Mailchimp] Zielgruppe.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie unter Experience Platform einrichten müssen. [!DNL Mailchimp] und für Informationen, die Sie vor der Arbeit mit dem [!DNL Mailchimp Interest Categories] Ziel.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Mailchimp Interest Categories]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen für die [!DNL Mailchimp Interest Categories] Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihre [!DNL Mailchimp] Konto:

#### Sie müssen über eine [!DNL Mailchimp] account {#prerequisites-account}

Bevor Sie eine [!DNL Mailchimp Interest Categories] Ziel müssen Sie zunächst sicherstellen, dass Sie über eine [!DNL Mailchimp] -Konto. Wenn Sie noch keine haben, rufen Sie die Seite [[!DNL Mailchimp] Anmeldeseite](https://login.mailchimp.com/signup/) , um sich zu registrieren und Ihr Konto zu erstellen.

#### Gather [!DNL Mailchimp] API-Schlüssel {#gather-credentials}

Sie benötigen Ihre [!DNL Mailchimp] **API-Schlüssel** zum Authentifizieren der [!DNL Mailchimp Interest Categories] Ziel gegen [!DNL Mailchimp] -Konto. Die **API-Schlüssel** dient als **Passwort** wenn Sie [das Ziel authentifizieren](#authenticate).

Wenn Sie Ihre **API-Schlüssel**, Melden Sie sich bei Ihrem Konto an und lesen Sie den Abschnitt [[!DNL Mailchimp] API-Schlüssel generieren](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) Dokumentation zu erstellen.

Ein Beispiel für einen API-Schlüssel ist `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Wenn Sie die **API-Schlüssel**, schreiben Sie es auf, da Sie nach der Generierung nicht mehr darauf zugreifen können.

#### Identifizieren [!DNL Mailchimp] Rechenzentrum {#identify-data-center}

Als Nächstes müssen Sie Ihre [!DNL Mailchimp] Rechenzentrum. Melden Sie sich dazu bei Ihrem [!DNL Mailchimp] -Konto und navigieren Sie zum **API-Schlüsselabschnitt** Ihres Kontos.

Der Wert ist der erste Teil der URL, die im Browser angezeigt wird. Wenn die URL *https://`us14`.mailchimp.com/account/api/*, dann ist das Rechenzentrum `us14`.

Er wird auch an Ihren API-Schlüssel im Formular angehängt *key-dc*; wenn Ihr API-Schlüssel `0123456789abcdef0123456789abcde-us14`, dann ist das Rechenzentrum `us14`.

Notieren Sie sich den Wert des Rechenzentrums. *(`us14` in diesem Beispiel)* benötigen Sie diesen Wert, wenn Sie [Zieldetails ausfüllen](#destination-details).

Weitere Informationen finden Sie im Abschnitt [[!DNL Mailchimp] Dokumentation zu Grundlagen](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Leitplanken {#guardrails}

Jeder Ihrer [!DNL Mailchimp] Zielgruppen können bis zu 60 Gruppennamen (oder Interessenkategorien) in einer einzelnen Gruppe oder über mehrere Gruppen innerhalb derselben Zielgruppe hinweg enthalten. Siehe Abschnitt [!DNL Mailchimp] [Gruppen](https://mailchimp.com/help/getting-started-with-groups/) für alle erforderlichen Klarstellungen. Wenn Sie diese Grenze erreichen, erhalten Sie eine `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` Meldung als Fehlerantwort von [!DNL Mailchimp] API.

Weitere Informationen finden Sie im Abschnitt [!DNL Mailchimp] [Grenzwerte](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) für ausführliche Informationen über die durch die [!DNL Mailchimp] API.

## Unterstützte Identitäten {#supported-identities}

[!DNL Mailchimp] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adresse kontaktieren | Obligatorisch |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird die entsprechende [!DNL Mailchimp Interest Categories] Der Segmentstatus wird mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Within **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**, suchen Sie nach [!DNL Mailchimp Interest Categories]. Alternativ können Sie sie unter der **[!UICONTROL E-Mail-Marketing]** Kategorie.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Benutzername]** | Ihre [!DNL Mailchimp Interest Categories] Benutzername. |
| **[!UICONTROL Passwort]** | Ihre [!DNL Mailchimp] **API-Schlüssel**, die Sie im Abschnitt [Gather [!DNL Mailchimp] Anmeldeinformationen](#gather-credentials) Abschnitt.<br> Ihr API-Schlüssel hat die Form `{KEY}-{DC}`, wobei `{KEY}` Der Teil bezieht sich auf den im [[!DNL Mailchimp] API-Schlüssel](#gather-credentials) und `{DC}` -Teil auf [[!DNL Mailchimp] Rechenzentrum](#identify-data-center). <br>Sie können entweder `{KEY}` oder das gesamte Formular.<br> Wenn Ihr API-Schlüssel beispielsweise <br>*`0123456789abcdef0123456789abcde-us14`*,<br> Sie können *`0123456789abcdef0123456789abcde`*oder *`0123456789abcdef0123456789abcde-us14`*als Wert. |

{style="table-layout:auto"}

![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können. |
| **[!UICONTROL Beschreibung]** | Eine Beschreibung, die Ihnen bei der Identifizierung dieses Ziels in der Zukunft hilft. |
| **[!UICONTROL Rechenzentrum]** | Ihre [!DNL Mailchimp] account `data center`. Siehe Abschnitt [Identifizieren [!DNL Mailchimp] Rechenzentrum](#identify-data-center) für Hinweise. |
| **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Data Center aus)]** | Nachdem Sie die **[!UICONTROL Rechenzentrum]** enthalten, wird diese Dropdown-Liste automatisch mit den Zielgruppennamen aus Ihren [!DNL Mailchimp] -Konto. Wählen Sie die Zielgruppe aus, die mit Daten aus Platform aktualisiert werden soll. |
| **[!UICONTROL Interessenkategorie (Bitte wählen Sie zuerst Data Center und Zielgruppenname aus)]** | Nachdem Sie die **[!UICONTROL Zielgruppenname]** enthält, wird diese Dropdown-Liste automatisch mit den Namen der Interessengruppen-Kategorien aus Ihrem [!DNL Mailchimp] -Konto. Wählen Sie den Kategorienamen aus, den Sie mit Daten aus Platform aktualisieren möchten. |

{style="table-layout:auto"}

>[!TIP]
>
> Wenn der API-Schlüssel, den Sie im **[!UICONTROL Passwort]** oder **[!UICONTROL Rechenzentrum]** -Wert falsch ist, zeigt die Benutzeroberfläche eine [!DNL Mailchimp] API-Fehlerantwort: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* wie unten dargestellt. In diesem Fall können Sie keinen Wert aus der **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Data Center aus)]** -Feld. Um diesen Fehler zu beheben, geben Sie die richtigen Werte an.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

So senden Sie Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an die [!DNL Mailchimp Interest Categories] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen.

So ordnen Sie Ihre XDM-Felder korrekt der [!DNL Mailchimp Interest Categories] Gehen Sie wie folgt vor:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität.
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität oder **[!UICONTROL Attribute auswählen]** und wählen Sie aus der Liste der Attribute aus, die aus der [!DNL Mailchimp] API. *Alle benutzerdefinierten Attribute, die Sie der ausgewählten [!DNL Mailchimp] Die Zielgruppe kann auch als Zielfelder ausgewählt werden.*

   Die Zuordnungen, die zwischen Ihrem XDM-Profilschema und [!DNL Mailchimp Interest Categories] wie folgt aussehen: | Quellfeld | Zielfeld | Anmerkungen | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Obligatorisch: ja | |`xdm: person.name.firstName`|`Attribute: FNAME`| | |`xdm: person.name.lastName`|`Attribute: LNAME`| | |`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   Zusätzlich `ADDRESS` ist ein spezielles Zielfeld, das als `merge field` in [!DNL Mailchimp] Zielgruppe. Die [[!DNL Mailchimp] Dokumentation](https://mailchimp.com/developer/marketing/docs/merge-fields/) definiert die erforderlichen Schlüssel als `addr1`, `city`, `state`, und `zip`und die optionalen Schlüssel `addr2` und `country`. Die Werte für diese Felder müssen Zeichenfolgen sein. Wenn einer der `ADDRESS` Feldzuordnungen vorhanden sind, übergibt das Ziel die `ADDRESS` -Objekt [!DNL Mailchimp] API zur Aktualisierung. Alle `ADDRESS` Felder, die nicht zugeordnet sind, haben den Standardwert `NULL` mit Ausnahme des Landes, in dem der Standardwert `US`.

   Die für die `ADDRESS` wie folgt aussehen:

   | Quellfeld | Zielfeld |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Sie möchten beispielsweise den Wert für `country` mit dem vorhandenen Adressfeld des Kontakts `addr1`, `city`, `state`, und `zip` Werte als `132, My Street, Kingston`, `New York`, `New York` und `12401`. So aktualisieren Sie die `country` Sie müssen die vorhandenen Werte mit Änderungen übergeben *(falls vorhanden)* und den neuen Wert für &quot;country&quot;. Daher sollten die Werte in Ihrem Datensatz `132, My Street, Kingston`, `New York`, `New York`, `12401`, und `US`. So wiederholen Sie, wenn Sie nur `country` und stellen keine Werte für `addr1`, `city`, `state`, und `zip` werden sie von `NULL`.

   Nachfolgend finden Sie ein Beispiel mit den abgeschlossenen Zuordnungen:
   ![Screenshot der Platform-Benutzeroberfläche mit Feldzuordnungen.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Nächste]**.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

* Melden Sie sich bei Ihrer [[!DNL Mailchimp]](https://login.mailchimp.com/) -Konto. Navigieren Sie dann zum **[!DNL Audience]** Seite. Erweitern Sie anschließend die **[!DNL Manage Contacts]** Menü und wählen Sie **[!DNL Groups]**.

![Screenshot der Benutzeroberfläche von Mailchimp mit der Seite &quot;Zielgruppe&quot;.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Wählen Sie die Gruppe aus und prüfen Sie, ob die ausgewählten Zielgruppen als Kategorien mit dem Zielgruppennamen aus Platform erstellt wurden. Dem können automatisch generierte Suffix folgen.
   * Dieses Ziel verwendet die Namen der ausgewählten Segmente, um mithilfe der [[!DNL Mailchimp] Interessenkategorie-API hinzufügen](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Wenn Sie ein neues Ziel erstellen und dieselben Zielgruppen erneut aktivieren, [!DNL Mailchimp] fügt ein Suffix hinzu, um zwischen den vorhandenen und den neuen Segmenten zu unterscheiden.
* Kontakte, deren E-Mails nicht in der Gruppe vorhanden waren, werden der neu erstellten Kategorie hinzugefügt.
* Für Kontakte, die bereits in der Gruppe vorhanden sind, werden die Attributfelddaten aktualisiert und der Kontakt zur neu erstellten Kategorie hinzugefügt.

![Screenshot der Benutzeroberfläche von Mailchimp mit den Kategorien der Zielgruppe.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Fehler bei [!DNL Mailchimp] API-Schlüssel oder Werte im Rechenzentrum sind falsch {#incorrect-credentials-error}

Wenn der API-Schlüssel, den Sie im **[!UICONTROL Passwort]** oder **[!UICONTROL Rechenzentrum]** -Wert falsch ist, zeigt die Benutzeroberfläche eine [!DNL Mailchimp] API-Fehlerantwort: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* wie unten dargestellt. In diesem Fall können Sie keinen Wert aus der **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Data Center aus)]** -Feld.

![Der Screenshot der Platform-Benutzeroberfläche zeigt einen Fehler, wenn der Mailchimp-API-Schlüssel oder die Werte des Rechenzentrums falsch sind.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Um diesen Fehler zu beheben und mit dem nächsten Schritt fortzufahren, müssen Sie die richtigen Werte angeben. Siehe Abschnitt [Identifizieren [!DNL Mailchimp] Rechenzentrum](#identify-data-center) und
[Gather [!DNL Mailchimp] API-Schlüssel](#gather-credentials) Abschnitte, wenn Sie Anleitungen benötigen.

### Fehler bei [!DNL Mailchimp] Gruppennamenlimit überschritten {#group-name-limits-error}

Beim Erstellen des Ziels erhalten Sie möglicherweise die folgenden Fehlermeldungen: *`Cannot have more than 60 interests per list (Across all categories)`* oder *`400 BAD_REQUEST`*. Dies geschieht, wenn Sie die 60 Gruppennamen (oder Interessenkategorien) in einer einzelnen Gruppe oder über mehrere Gruppen innerhalb desselben Zielgruppenlimits überschreiten, wie im Abschnitt [Limits](#guardrails) Abschnitt. Um diesen Fehler zu beheben, dürfen Sie die Gruppennamengrenze in [!DNL Mailchimp].

### [!DNL Mailchimp] Status- und Fehlercodes

Siehe Abschnitt [[!DNL Mailchimp] Fehlerseite](https://mailchimp.com/developer/marketing/docs/errors/) für eine umfassende Liste von Status- und Fehlercodes mit Erläuterungen.

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Mailchimp]Dokumentation finden Sie im Folgenden:
* [Erste Schritte mit [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Erste Schritte mit Zielgruppen](https://mailchimp.com/help/getting-started-audience/)
* [Erstellen von Zielgruppen](https://mailchimp.com/help/create-audience/)
* [Erste Schritte mit Gruppen](https://mailchimp.com/help/getting-started-with-groups/)
* [Neue Zielgruppe erstellen](https://mailchimp.com/help/create-new-audience-group/)
* [Interessenkategorien](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [Marketing-API](https://mailchimp.com/developer/marketing/api/)
