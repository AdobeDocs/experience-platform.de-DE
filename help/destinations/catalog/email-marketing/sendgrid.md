---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; sendgrid; sendgrid; sendgrid-Ziel
title: SendGrid-Verbindung
description: Mit dem SendGrid-Ziel können Sie Ihre Erstanbieterdaten exportieren und in SendGrid für Ihre geschäftlichen Anforderungen aktivieren.
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 24%

---

# [!DNL SendGrid]-Verbindung

## Übersicht {#overview}

[SendGrid](https://www.sendgrid.com) ist eine beliebte Kundenkommunikationsplattform für Transaktions- und Marketing-E-Mails.

Dieses [!DNL Adobe Experience Platform] [ Ziel](/help/destinations/home.md) nutzt den [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts), mit dem Sie Ihre Erstanbieter-E-Mail-Profile exportieren und in einer neuen SendGrid-Zielgruppe aktivieren können, um Ihre geschäftlichen Anforderungen zu erfüllen.

SendGrid verwendet API-Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit der SendGrid-API.

## Voraussetzungen {#prerequisites}

Die folgenden Elemente sind erforderlich, bevor Sie mit der Konfiguration des Ziels beginnen.

1. Sie benötigen ein SendGrid-Konto.
   * Rufen Sie die Seite SendGrid [Sign-up](https://signup.sendgrid.com/) auf, um sich zu registrieren und ein SendGrid-Konto zu erstellen, sofern noch keines vorhanden ist.
1. Nach der Anmeldung beim SendGrid-Portal müssen Sie auch ein API-Token generieren.
1. Navigieren Sie zur SendGrid-Website und rufen Sie die Seite **[!DNL Settings]** > **[!DNL API Keys]** auf. Alternativ können Sie in der [SendGrid-Dokumentation](https://app.sendgrid.com/settings/api_keys) auf den entsprechenden Abschnitt in der SendGrid-App zugreifen.
1. Wählen Sie abschließend die Schaltfläche **[!DNL Create API Key]** aus.
   * Lesen Sie die [SendGrid-Dokumentation](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key) , wenn Sie Anleitungen zu den auszuführenden Aktionen benötigen.
   * Wenn Sie Ihren API-Schlüssel programmgesteuert generieren möchten, lesen Sie die [SendGrid-Dokumentation](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

Bevor Sie Daten für das SendGrid-Ziel aktivieren, müssen Sie über ein [Schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden. Siehe auch den Abschnitt [limits](#limits) weiter unten auf dieser Seite.

>[!IMPORTANT]
>
>* Für die SendGrid-API, die zum Erstellen der Mailing-Liste aus E-Mail-Profilen verwendet wird, müssen innerhalb jedes Profils eindeutige E-Mail-Adressen angegeben werden. Dies gilt unabhängig davon, ob es als Wert für *email* oder *alternative email* verwendet wird. Da die SendGrid-Verbindung Zuordnungen für E-Mail- und alternative E-Mail-Werte unterstützt, stellen Sie sicher, dass alle verwendeten E-Mail-Adressen in jedem Profil des *Datensatzes* eindeutig sein sollten. Andernfalls tritt beim Senden der E-Mail-Profile an SendGrid ein Fehler auf, und dieses E-Mail-Profil ist im Datenexport nicht vorhanden.
>
>* Derzeit gibt es keine Funktion zum Entfernen von Profilen aus SendGrid, wenn sie in Experience Platform aus Zielgruppen entfernt werden.

## Unterstützte Identitäten {#supported-identities}

SendGrid unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adresse | Beachten Sie, dass sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von [!DNL Adobe Experience Platform] unterstützt werden. Wenn das Quellfeld der Experience Platform ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation anwenden]** , damit [!DNL Platform] die Daten bei Aktivierung automatisch hasst.<br/><br/> Beachten Sie, dass **SendGrid** keine Hash-E-Mail-Adressen unterstützt, sodass nur Textdaten ohne Umwandlung an das Ziel gesendet werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das SendGrid-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die [!DNL Experience Platform] -Kunden mit diesem Ziel lösen können.

### Erstellen einer Marketingliste für mehrere Marketingaktivitäten

Marketingteams, die SendGrid verwenden, können eine Mailingliste in SendGrid erstellen und diese mit E-Mail-Adressen füllen. Die jetzt in SendGrid erstellte Mailingliste kann später für mehrere Marketing-Aktivitäten verwendet werden.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

1. Navigieren Sie in der Konsole [!DNL Adobe Experience Platform] zu **Ziele**.

1. Wählen Sie die Registerkarte **Katalog** aus und suchen Sie nach *SendGrid*. Wählen Sie dann **Einrichten** aus. Nachdem Sie eine Verbindung zum Ziel hergestellt haben, ändert sich die Beschriftung der Benutzeroberfläche in **Segmente aktivieren**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. Ihnen wird ein Assistent angezeigt, der Sie bei der Konfiguration des SendGrid-Ziels unterstützt. Erstellen Sie das neue Ziel, indem Sie **Neues Ziel konfigurieren** auswählen.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. Wählen Sie die Option **Neues Konto** aus und geben Sie den Wert **Trägertoken** ein. Dieser Wert ist der SendGrid *API-Schlüssel* , der zuvor im Abschnitt [Voraussetzungen ](#prerequisites) erwähnt wurde.
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. Wählen Sie **Mit Ziel verbinden** aus. Wenn der von Ihnen angegebene SendGrid *API-Schlüssel* gültig ist, zeigt die Benutzeroberfläche den Status **Connected** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren, um zusätzliche Informationsfelder auszufüllen.

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### Ausfüllen der Zieldetails {#destination-details}

Beim [Einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Der Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine optionale Beschreibung, die Ihnen bei der Identifizierung dieses Ziels in der Zukunft hilft.

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Weitere Informationen zu diesem Ziel finden Sie in den folgenden Bildern.

1. Wählen Sie eine oder mehrere Zielgruppen aus, die in SendGrid exportiert werden sollen.
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. Im Schritt **[!UICONTROL Mapping]** wird nach Auswahl von **[!UICONTROL Neues Mapping hinzufügen]** die Zuordnungsseite angezeigt, auf der die Quell-XDM-Felder den SendGrid-API-Zielfeldern zugeordnet werden. Die folgenden Abbildungen zeigen, wie Identitäts-Namespaces zwischen Experience Platform und SendGrid zugeordnet werden. Stellen Sie sicher, dass das Feld **[!UICONTROL Source]** *E-Mail* dem Feld **[!UICONTROL Ziel]** *external_id* zugeordnet werden sollte, wie unten dargestellt.
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. Ordnen Sie die gewünschten [!DNL Adobe Experience Platform] -Attribute, die Sie exportieren möchten, dem SendGrid-Ziel zu.
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. Wählen Sie nach Abschluss der Zuordnungen **[!UICONTROL Weiter]** aus, um zum Überprüfungsbildschirm zu gelangen.
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. Wählen Sie **[!UICONTROL Beenden]** aus, um das Setup abzuschließen.
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

Nachfolgend finden Sie eine umfassende Liste der unterstützten Attributzuordnungen, die für die Marketing-Kontakte mit dem Namen [SendGrid > Kontakt-API hinzufügen oder aktualisieren](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) eingerichtet werden können.

| Quellfeld | Zielfeld | Typ | Beschreibung | Beschränkungen |
|---|---|---|---|---|
| xdm:<br/> homeAddress.street1 | xdm:<br/> address_line_1 | Zeichenfolge | Die erste Zeile der Adresse. | Max. Länge:<br/> 100 Zeichen |
| xdm:<br/> homeAddress.street2 | xdm:<br/> address_line_2 | Zeichenfolge | Eine optionale zweite Zeile für die Adresse. | Max. Länge:<br/> 100 Zeichen |
| xdm:<br/> _extconndev.alternate_emails | xdm:<br/> alternative_emails | Array of String | Zusätzliche E-Mails, die mit dem Kontakt verknüpft sind. | <ul><li>Maximal 5 Elemente</li><li>Min.: 0 Elemente</li></ul> |
| xdm:<br/> homeAddress.city | xdm:<br/> city | Zeichenfolge | Die Stadt des Kontakts. | Max. Länge:<br/> 60 Zeichen |
| xdm:<br/> homeAddress.country | xdm:<br/> country | Zeichenfolge | Das Land des Kontakts. Kann ein vollständiger Name oder eine Abkürzung sein. | Max. Länge:<br/> 50 Zeichen |
| identityMap:<br/> Email | Identität:<br/> external_id | Zeichenfolge | Die primäre E-Mail des Kontakts. Dies muss eine gültige E-Mail sein. | Max. Länge:<br/> 254 Zeichen |
| xdm:<br/> person.name.firstName | xdm:<br/> first_name | Zeichenfolge | Name des Kontakts | Max. Länge:<br/> 50 Zeichen |
| xdm:<br/> person.name.lastName | xdm:<br/> last_name | Zeichenfolge | Familienname des Kontakts | Max. Länge:<br/> 50 Zeichen |
| xdm:<br/> homeAddress.postalCode | xdm:<br/> postal_code | Zeichenfolge | Postleitzahl des Kontakts oder andere Postleitzahlen. | |
| xdm:<br/> homeAddress.stateProvince | xdm:<br/> state_Province_region | Zeichenfolge | Das Bundesland, die Provinz oder die Region des Kontakts. | Max. Länge:<br/> 50 Zeichen |

## Validieren des Datenexports in SendGrid {#validate}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** aus, um zur Liste der Ziele zu navigieren.
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL aktiviert]** ist.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. Wechseln Sie zur Registerkarte **[!DNL Activation data]** und wählen Sie einen Zielgruppennamen aus.
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. Überwachen Sie die Zielgruppenzusammenfassung und überprüfen Sie, ob die Anzahl der Profile der im Datensatz erstellten Anzahl entspricht.
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. Die Marketing-Listen [SendGrid > Liste erstellen-API](https://docs.sendgrid.com/api-reference/lists/create-list) wird verwendet, um innerhalb von SendGrid eindeutige Kontaktlisten zu erstellen, indem der Wert des Attributs *list_name* und der Zeitstempel des Datenexports hinzugefügt werden. Navigieren Sie zur SendGrid-Site und überprüfen Sie, ob die neue Kontaktliste erstellt wurde, die dem Namensmuster entspricht.
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. Wählen Sie die neu erstellte Kontaktliste aus und überprüfen Sie, ob der neue E-Mail-Datensatz aus dem von Ihnen erstellten Datensatz in der neuen Kontaktliste eingetragen wird.

1. Überprüfen Sie außerdem einige E-Mails, um zu überprüfen, ob die Feldzuordnung korrekt ist.
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Dieses SendGrid-Ziel nutzt die folgenden APIs:
* [SendGrid-Marketinglisten > Listen-API erstellen](https://docs.sendgrid.com/api-reference/lists/create-list)
* [Marketingkontakte für SendGrid > Kontakt-API hinzufügen oder aktualisieren](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### Beschränkungen {#limits}

* Die Marketing-Kontakte [SendGrid > Kontakt-API hinzufügen oder aktualisieren](https://api.sendgrid.com/v3/marketing/contacts) kann 30.000 Kontakte oder 6 MB an Daten akzeptieren, je nachdem, welcher Wert niedriger ist.
