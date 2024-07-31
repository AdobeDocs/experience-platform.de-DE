---
title: Mailchimp-Interessenkategorien
description: Mailchimp (auch Intuit Mailchimp genannt) ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, die von Unternehmen verwendet werden, um Kontakte (Kunden, Kunden oder andere interessierte Parteien) mithilfe von Mailinglisten und E-Mail-Marketing-Kampagnen zu verwalten und mit ihnen zu kommunizieren. Verwenden Sie diesen Connector, um Ihre Kontakte nach deren Interessen und Präferenzen zu sortieren.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 20%

---

# [!DNL Mailchimp Interest Categories]-Verbindung

[[!DNL Mailchimp]](https://mailchimp.com) ist eine beliebte Marketing-Automatisierungsplattform und ein E-Mail-Marketing-Service, die von Unternehmen verwendet werden, um Kontakte zu verwalten *(Kunden, Kunden oder sonstige interessierte Parteien)* und diese über Mailinglisten und E-Mail-Marketing-Kampagnen zu erreichen. Verwenden Sie diesen Connector, um Ihre Kontakte nach deren Interessen und Präferenzen zu sortieren.

[!DNL Mailchimp Interest Categories] verwendet [Zielgruppen](https://mailchimp.com/help/getting-started-audience/), [Gruppen](https://mailchimp.com/help/getting-started-with-groups/) und Interessenkategorien *(auch als Gruppennamen oder Gruppentitel bezeichnet)*. Jede [!DNL Mailchimp] Gruppe ist eine Liste von Interessenskategorien. Kontakte werden einer Interessenkategorie zugeordnet, wenn sie über ein Anmeldeformular auf Ihrer Website eine oder mehrere Interessenskategorien abonnieren. Innerhalb einer Zielgruppe können Sie die Kontakte auch in Gruppen organisieren und sie Interessenkategorien zuordnen. Diese können dann zur Erstellung von Segmenten verwendet werden. Sie können diese Zielgruppen verwenden, um zielgerichtete Kampagnen-E-Mails an die angemeldeten Kontakte zu senden.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) verwendet die [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/)-API, um [Interessenkategorien](https://mailchimp.com/developer/marketing/api/interest-categories/) zu erstellen und dann Kontakte aus den ausgewählten Platform-Audiences zu einer entsprechenden Interessenkategorie hinzuzufügen. Sie können **neue Kontakte hinzufügen** oder **die Informationen vorhandener [!DNL Mailchimp] Kontakte aktualisieren** und diese dann in einer vorhandenen [!DNL Mailchimp]-Zielgruppe durch **Hinzufügen oder Entfernen aus den gewünschten Gruppen** hinzufügen, nachdem Sie sie in einem neuen Segment aktiviert haben. [!DNL Mailchimp Interest Groups] verwendet die ausgewählten Zielgruppennamen aus Platform als Interessenkategorien in [!DNL Mailchimp].

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Mailchimp Interest Categories]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Verkaufsabteilung einer Sportartikelwebsite möchte eine E-Mail-basierte Marketing-Kampagne an eine Liste von Kontakten senden, die sich selbst als an Fußball interessiert identifiziert haben. Die Kontaktlisten werden als Batches im Datenexport getrennt, die vom Entwicklungsteam der Website empfangen wurden, und müssen daher verfolgt werden. Das Team identifiziert eine vorhandene [!DNL Mailchimp] -Zielgruppe und beginnt mit der Erstellung der Experience Platform-Zielgruppen, in die die Kontakte aus den einzelnen Listen aufgenommen werden. Nachdem diese Zielgruppen an [!DNL Mailchimp Interest Categories] gesendet wurden, werden Kontakte, die in der ausgewählten [!DNL Mailchimp] -Zielgruppe nicht vorhanden sind, zu einer Gruppe mit dem Zielgruppennamen hinzugefügt, zu der der Kontakt gehört. Wenn bereits Kontakte in der [!DNL Mailchimp] -Zielgruppe oder -Gruppe vorhanden sind, werden deren Informationen aktualisiert. Sobald die Daten an [!DNL Mailchimp Interest Categories] gesendet wurden, kann das Sales-Team die Marketing-Kampagnen-E-Mail auswählen und an die Fußball-Interessengruppe innerhalb der [!DNL Mailchimp] -Zielgruppe senden.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL Mailchimp] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL Mailchimp Interest Categories]-Ziel erfassen müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Mailchimp Interest Categories]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen für das [!DNL Mailchimp Interest Categories]-Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihr [!DNL Mailchimp] -Konto zu exportieren:

#### Sie müssen über ein [!DNL Mailchimp] -Konto verfügen. {#prerequisites-account}

Bevor Sie ein [!DNL Mailchimp Interest Categories] -Ziel erstellen können, müssen Sie zunächst sicherstellen, dass Sie über ein [!DNL Mailchimp] -Konto verfügen. Wenn Sie noch kein Konto haben, besuchen Sie die [[!DNL Mailchimp] Anmeldeseite](https://login.mailchimp.com/signup/) , um sich zu registrieren und Ihr Konto zu erstellen.

#### Sammeln von [!DNL Mailchimp] API-Schlüssel {#gather-credentials}

Sie benötigen Ihren [!DNL Mailchimp] **API-Schlüssel**, um das [!DNL Mailchimp Interest Categories]-Ziel für Ihr [!DNL Mailchimp]-Konto zu authentifizieren. Der **API-Schlüssel** dient als **Kennwort**, wenn Sie [das Ziel authentifizieren](#authenticate).

Wenn Sie Ihren **API-Schlüssel** nicht haben, melden Sie sich bei Ihrem Konto an und lesen Sie die Dokumentation zum Erstellen Ihres API-Schlüssels [[!DNL Mailchimp] Generate your API key](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) , um einen zu erstellen.

Ein Beispiel für einen API-Schlüssel ist `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Wenn Sie den **API-Schlüssel** generieren, schreiben Sie ihn auf, da Sie nach der Generierung nicht mehr darauf zugreifen können.

#### Identifizieren Sie [!DNL Mailchimp] Rechenzentrum {#identify-data-center}

Als Nächstes müssen Sie Ihr [!DNL Mailchimp] -Rechenzentrum identifizieren. Melden Sie sich dazu bei Ihrem [!DNL Mailchimp] -Konto an und navigieren Sie zum Abschnitt **API-Schlüssel** Ihres Kontos.

Der Wert ist der erste Teil der URL, die im Browser angezeigt wird. Wenn die URL *https://`us14`.mailchimp.com/account/api/* ist, ist das Rechenzentrum `us14`.

Er wird auch im Format *key-dc* an Ihren API-Schlüssel angehängt. Wenn Ihr API-Schlüssel `0123456789abcdef0123456789abcde-us14` ist, ist das Rechenzentrum `us14`.

Notieren Sie den Rechenzentrumswert *(`us14` in diesem Beispiel)*. Sie benötigen diesen Wert, wenn Sie [Zieldetails ausfüllen](#destination-details).

Wenn Sie weitere Anleitungen benötigen, lesen Sie die [[!DNL Mailchimp] Grundlagendokumentation](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Leitplanken {#guardrails}

Jede Ihrer [!DNL Mailchimp] Zielgruppen kann bis zu 60 Gruppennamen (oder Interessenkategorien) in einer Gruppe oder über mehrere Gruppen innerhalb derselben Zielgruppe hinweg enthalten. Weitere Informationen finden Sie unter [!DNL Mailchimp] [Gruppen](https://mailchimp.com/help/getting-started-with-groups/) . Wenn Sie diese Grenze erreichen, erhalten Sie eine `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` -Meldung als Fehlerantwort von der [!DNL Mailchimp] -API.

Weitere Informationen zu den Beschränkungen, die durch die [!DNL Mailchimp] -API auferlegt werden, finden Sie unter [!DNL Mailchimp] [Ratenbeschränkungen](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) .

## Unterstützte Identitäten {#supported-identities}

[!DNL Mailchimp] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adresse kontaktieren | Obligatorisch |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird der entsprechende Segmentstatus [!DNL Mailchimp Interest Categories] mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Mailchimp Interest Categories]. Alternativ können Sie ihn unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Benutzername]** | Ihr [!DNL Mailchimp Interest Categories] Benutzername. |
| **[!UICONTROL Passwort]** | Ihr [!DNL Mailchimp] **API-Schlüssel**, den Sie im Abschnitt [Anmeldedaten des Zusammenführers [!DNL Mailchimp] eingegeben haben](#gather-credentials) notiert haben.<br> Ihr API-Schlüssel hat die Form &quot;`{KEY}-{DC}`&quot;, wobei der &quot;`{KEY}`&quot;-Teil auf den im Abschnitt &quot;[[!DNL Mailchimp] API-Schlüssel](#gather-credentials)&quot; verzeichneten Wert verweist und der &quot;`{DC}`&quot;-Teil auf das &quot;[[!DNL Mailchimp] Rechenzentrum](#identify-data-center)&quot;. <br>Sie können entweder den Abschnitt `{KEY}` oder das gesamte Formular angeben.<br> Wenn Ihr API-Schlüssel beispielsweise <br>*`0123456789abcdef0123456789abcde-us14`*, <br> ist, können Sie entweder *`0123456789abcdef0123456789abcde`*oder *`0123456789abcdef0123456789abcde-us14`*als Wert angeben. |

{style="table-layout:auto"}

![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden. |
| **[!UICONTROL Beschreibung]** | Eine Beschreibung, die Ihnen bei der Identifizierung dieses Ziels in der Zukunft hilft. |
| **[!UICONTROL Rechenzentrum]** | Ihr [!DNL Mailchimp] Konto `data center`. Eine Anleitung dazu finden Sie im Abschnitt [Identifizieren [!DNL Mailchimp] des Rechenzentrums](#identify-data-center) . |
| **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Data Center aus)]** | Nachdem Sie Ihr **[!UICONTROL Rechenzentrum]** ausgewählt haben, wird diese Dropdown-Liste automatisch mit den Zielgruppennamen aus Ihrem [!DNL Mailchimp] -Konto gefüllt. Wählen Sie die Zielgruppe aus, die mit Daten aus Platform aktualisiert werden soll. |
| **[!UICONTROL Interessenkategorie (Bitte wählen Sie zuerst Data Center und Audience Name aus)]** | Nachdem Sie Ihren **[!UICONTROL Zielgruppennamen]** ausgewählt haben, wird diese Dropdown-Liste automatisch mit den Namen der Interessengruppen-Kategorien aus Ihrem [!DNL Mailchimp]-Konto gefüllt. Wählen Sie den Kategorienamen aus, den Sie mit Daten aus Platform aktualisieren möchten. |

{style="table-layout:auto"}

>[!TIP]
>
> Wenn der im Feld **[!UICONTROL Kennwort]** angegebene API-Schlüssel oder der Wert **[!UICONTROL Data Center]** falsch sind, zeigt die Benutzeroberfläche eine [!DNL Mailchimp] API-Fehlerantwort an: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*, wie unten dargestellt. In diesem Fall können Sie keinen Wert aus dem Feld **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Rechenzentrum aus)]** auswählen. Um diesen Fehler zu beheben, geben Sie die richtigen Werte an.

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

Um Ihre Zielgruppendaten korrekt von Adobe Experience Platform an das Ziel [!DNL Mailchimp Interest Categories] zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den [!DNL Mailchimp Interest Categories] -Zielfeldern zuzuordnen:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** aus, wählen Sie das XDM-Attribut aus oder wählen Sie den Eintrag **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** den Eintrag **[!UICONTROL Identitäts-Namespace auswählen]** aus, wählen Sie eine Identität aus oder wählen Sie die Kategorie **[!UICONTROL Attribute auswählen]** und wählen Sie aus der Liste der Attribute aus, die in der API [!DNL Mailchimp] eingetragen sind. *Alle benutzerdefinierten Attribute, die Sie der ausgewählten [!DNL Mailchimp] Zielgruppe hinzugefügt haben, stehen ebenfalls zur Auswahl als Zielfelder zur Verfügung.*

   Die zwischen Ihrem XDM-Profilschema und [!DNL Mailchimp Interest Categories] verfügbaren Zuordnungen sind wie folgt:

   | Quellfeld | Zielfeld | Anmerkungen |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: email` | Obligatorisch: ja |
   | `xdm: person.name.firstName` | `Attribute: FNAME` | |
   | `xdm: person.name.lastName` | `Attribute: LNAME` | |
   | `xdm: person.birthDayAndMonth` | `Attribute: BIRTHDAY` | |

   Außerdem ist `ADDRESS` ein spezielles Zielfeld, das in Ihrer [!DNL Mailchimp] -Zielgruppe als `merge field` bezeichnet wird. Die [[!DNL Mailchimp] Dokumentation](https://mailchimp.com/developer/marketing/docs/merge-fields/) definiert die erforderlichen Schlüssel als `addr1`, `city`, `state` und `zip` sowie die optionalen Schlüssel `addr2` und `country`. Die Werte für diese Felder müssen Zeichenfolgen sein. Wenn eine der `ADDRESS` -Feldzuordnungen vorhanden ist, übergibt das Ziel das `ADDRESS` -Objekt zur Aktualisierung an die [!DNL Mailchimp] -API. Alle nicht zugeordneten `ADDRESS` -Felder haben den Standardwert `NULL` , außer für das Land, das standardmäßig auf `US` festgelegt ist.

   Die für das Feld `ADDRESS` verfügbaren Zuordnungen sind wie folgt:

   | Quellfeld | Zielfeld |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Beispielsweise möchten Sie den Wert für `country` mit den vorhandenen Adressfeldern `addr1`, `city`, `state` und `zip` als `132, My Street, Kingston`, `New York`, `New York` und `12401` aktualisieren. Um die `country` zu aktualisieren, müssen Sie die vorhandenen Werte mit den Änderungen *(falls vorhanden)* und dem neuen Wert für &quot;country&quot;übergeben. Die Werte in Ihrem Datensatz sollten also `132, My Street, Kingston`, `New York`, `New York`, `12401` und `US` sein. Wenn Sie nur `country` übergeben und keine Werte für `addr1`, `city`, `state` und `zip` bereitstellen, werden diese von `NULL` überschrieben.

   Nachfolgend finden Sie ein Beispiel mit den abgeschlossenen Zuordnungen:
   ![Screenshot der Platform-Benutzeroberfläche mit Feldzuordnungen.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

* Melden Sie sich bei Ihrem [[!DNL Mailchimp]](https://login.mailchimp.com/) -Konto an. Navigieren Sie dann zur Seite **[!DNL Audience]** . Erweitern Sie anschließend das Menü **[!DNL Manage Contacts]** und wählen Sie **[!DNL Groups]** aus.

![Mailchimp UI-Screenshot mit der Seite &quot;Zielgruppe&quot;.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Wählen Sie die Gruppe aus und prüfen Sie, ob die ausgewählten Zielgruppen als Kategorien mit dem Zielgruppennamen aus Platform erstellt wurden. Dem können automatisch generierte Suffix folgen.
   * Dieses Ziel verwendet die Namen der ausgewählten Segmente, um die Interessenkategorie mithilfe der API [[!DNL Mailchimp] Interessenkategorie hinzufügen](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/) zu erstellen. Wenn Sie ein neues Ziel erstellen und dieselben Zielgruppen erneut aktivieren, fügt [!DNL Mailchimp] ein Suffix hinzu, um zwischen den vorhandenen und den neuen Segmenten zu unterscheiden.
* Kontakte, deren E-Mails nicht in der Gruppe vorhanden waren, werden der neu erstellten Kategorie hinzugefügt.
* Für Kontakte, die bereits in der Gruppe vorhanden sind, werden die Attributfelddaten aktualisiert und der Kontakt zur neu erstellten Kategorie hinzugefügt.

![Mailchimp UI-Screenshot mit den Zielgruppen-Kategorien.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Fehler bei fehlerhafter Eingabe von [!DNL Mailchimp] API-Schlüssel oder Rechenzentrumswerten {#incorrect-credentials-error}

Wenn der im Feld **[!UICONTROL Kennwort]** angegebene API-Schlüssel oder der Wert **[!UICONTROL Data Center]** falsch sind, zeigt die Benutzeroberfläche eine [!DNL Mailchimp] API-Fehlerantwort an: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*, wie unten dargestellt. In diesem Fall können Sie keinen Wert aus dem Feld **[!UICONTROL Zielgruppenname (Bitte wählen Sie zuerst Rechenzentrum aus)]** auswählen.

![Der Screenshot der Platform-Benutzeroberfläche zeigt einen Fehler, wenn der Mailchimp-API-Schlüssel oder die Werte des Rechenzentrums falsch sind.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Um diesen Fehler zu beheben und mit dem nächsten Schritt fortzufahren, müssen Sie die richtigen Werte angeben. Siehe [Identifizieren [!DNL Mailchimp] Rechenzentrum](#identify-data-center) und
[Sammeln Sie  [!DNL Mailchimp] API-Schlüssel](#gather-credentials), wenn Sie Anleitungen benötigen.

### Fehler bei Überschreitung der [!DNL Mailchimp] Gruppennamengrenze {#group-name-limits-error}

Beim Erstellen des Ziels erhalten Sie möglicherweise die folgenden Fehlermeldungen: *`Cannot have more than 60 interests per list (Across all categories)`* oder *`400 BAD_REQUEST`*. Dies geschieht, wenn Sie die 60 Gruppennamen (oder Interessenkategorien) in einer einzelnen Gruppe oder über mehrere Gruppen innerhalb desselben Zielgruppenlimits überschreiten, wie im Abschnitt [Limits](#guardrails) beschrieben. Um diesen Fehler zu beheben, stellen Sie sicher, dass Sie die Gruppennamenbeschränkung in [!DNL Mailchimp] nicht überschreiten.

### [!DNL Mailchimp] Status- und Fehlercodes

Eine umfassende Liste der Status- und Fehlercodes mit Erläuterungen finden Sie auf der [[!DNL Mailchimp] Fehlerseite](https://mailchimp.com/developer/marketing/docs/errors/) .

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Mailchimp] -Dokumentation finden Sie unten:
* [Erste Schritte mit  [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Erste Schritte mit Zielgruppen](https://mailchimp.com/help/getting-started-audience/)
* [Erstellen einer Zielgruppe](https://mailchimp.com/help/create-audience/)
* [Erste Schritte mit Gruppen](https://mailchimp.com/help/getting-started-with-groups/)
* [Erstellen einer neuen Zielgruppe](https://mailchimp.com/help/create-new-audience-group/)
* [Interessenkategorien](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [Marketing-API](https://mailchimp.com/developer/marketing/api/)
