---
title: Vorlage für Selbstbedienung der Dokumentation // Durch den Namen Ihres Ziels ersetzen
description: Verwenden Sie diese Vorlage, um eine öffentliche Dokumentation für Ihr Ziel im Adobe Experience Platform-Katalog zu erstellen. // Ersetzen durch den Absatz im Übersichtsabschnitt
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 3%

---

# YOURDESTINATION {#your-destination}

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle Absätze kursiv (beginnend mit dieser).*

*Beginn durch Aktualisieren der Metadaten (Titel und Beschreibung) oben auf der Seite. Ignorieren Sie alle Instanzen von UICONTROL auf dieser Seite. Dieses Tag hilft unseren maschinellen Übersetzungsprozessen, die Seite korrekt in mehrere Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation Tags hinzu, nachdem Sie sie gesendet haben.*

## Übersicht {#overview}

*Geben Sie einen kurzen Überblick über Ihre Firma, einschließlich des Kundenwerts. Fügen Sie einen Link zu Ihrer Produktdokumentations-Homepage ein, um ihn weiter zu lesen.*

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde erstellt von *YOURDESTINATION* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an die zuständigen Behörden unter *Link oder E-Mail-Adresse einfügen, wo Sie für Aktualisierungen erreichbar sind*

## Voraussetzungen {#prerequisites}

*hinzufügen Informationen in diesem Abschnitt über alles, was Kunden wissen müssen, bevor sie mit der Einrichtung des Ziels in der Adobe Experience Platform-Benutzeroberfläche beginnen. Hier geht es um:*

* *muss einer Zulassungsliste hinzugefügt werden*
* *Anforderungen für E-Mail-Hashing*
* *alle Kontoangaben auf Ihrer Seite*
* *wie Sie einen API-Schlüssel für die Verbindung mit Ihrer Plattform erhalten*

*Wenn dies für Kunden von Nutzen wäre, können Sie einen Link zu Ihrer relevanten Dokumentation herstellen.*

## Unterstützte Identitäten {#supported-identities}

*hinzufügen Informationen in diesem Abschnitt über die von Ihrem Ziel unterstützten Identitäten. Wir haben die Tabelle mit einigen Standardwerten vorausgefüllt. Löschen Sie die Werte, die nicht für Ihr Ziel gelten, und alle Werte, die nicht vorausgefüllt sind.*

*YOURDESTINATION* unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben ist. Weitere Informationen [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Identität der Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielgruppe-Identität aus, wenn Ihre Quellkennung ein GAID-Namensraum ist. |
| IDFA | Apple ID for Advertisers | Wählen Sie die IDFA-Zielgruppe-Identität aus, wenn Ihre Quellkennung ein IDFA-Namensraum ist. |
| ECID | Experience Cloud ID | Ein Namensraum, der die ECID darstellt. Auf diesen Namensraum können auch die folgenden Aliasse verweisen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Siehe folgendes Dokument: [ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) für weitere Informationen. |
| phone_sha256 | Telefonnummern mit Hash-Algorithmus SHA256 | Sowohl einfache Textnachrichten als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungelöste Attribute enthält, überprüfen Sie die **[!UICONTROL Transformation anwenden]** Option [!DNL Platform] Daten auf Aktivierung automatisch hash. |
| email_lc_sha256 | E-Mail-Adressen mit SHA256-Algorithmus | Sowohl reine Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungelöste Attribute enthält, überprüfen Sie die **[!UICONTROL Transformation anwenden]** Option [!DNL Platform] Daten auf Aktivierung automatisch hash. |
| extern_id | Benutzerspezifische Benutzer-IDs | Wählen Sie diese Zielgruppe-Identität aus, wenn Ihre Quellkennung ein benutzerdefinierter Namensraum ist. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport** - Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer oder andere), die in der *YOURDESTINATION* Ziel.

## Anwendungsfälle

Um Ihnen ein besseres Verständnis zu vermitteln, wie und wann Sie *YOURDESTINATION* Ziel, hier sind Beispielverwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Fall Nr. 1 verwenden

*Für mobile Messaging-Plattformen:*

*Eine Home-Miet- und Verkaufsplattform möchte mobile Benachrichtigungen an Android- und iOS-Geräte der Kunden senden, um ihnen mitzuteilen, dass es 100 aktualisierte Einträge in dem Bereich gibt, in dem sie zuvor nach einer Miete gesucht haben.*

### Fall Nr. 2 verwenden

*Für soziale Netzwerkplattformen:*

*Eine sportliche Bekleidungsmarke möchte bestehende Kunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen von ihrem eigenen CRM nach Adobe Experience Platform erfassen, Segmente aus ihren eigenen Offline-Daten aufbauen und diese Segmente an YOURDESTINATION senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.*

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die in der [Übungen zur Zielkonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

### Verbindungsparameter {#parameters}

Während [einrichten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) an diesem Ziel angeben, müssen Sie die folgenden Informationen angeben:

*hinzufügen die Felder, die Kunden bei der Konfiguration eines neuen Ziels ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration im Ziel-SDK ab. Die Felder Ihres Ziels dürfen nicht mit denen im Folgenden übereinstimmen.*

* **[!UICONTROL Name]**: Ein Name, unter dem Sie dieses Ziel in der Zukunft erkennen.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre *YOURDESTINATION* Konto-ID.


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## Segmente zu diesem Ziel aktivieren {#activate}

Gelesen [Profil und Segmente für Streaming-Segmentexportziele aktivieren](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) für Anweisungen zum Aktivieren von Audiencen-Segmenten für dieses Ziel.

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## Exportierte Daten {#exported-data}

*hinzufügen einen Hinweis darüber, wie Daten an Ihr Ziel exportiert werden. Dies würde dem Kunden dabei helfen, sicherzustellen, dass er sich korrekt in Ihr Ziel integriert hat. Sie können z. B. eine JSON-Beispieldatei wie die unten angegebene bereitstellen.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Nutzung und Verwaltung von Daten {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele entsprechen bei der Verarbeitung Ihrer Daten den Datenschutzrichtlinien. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Datenverwaltung, lesen Sie die [Datenverwaltung - Überblick](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Weitere Ressourcen {#additional-resources}

*Sie können weitere Links zu Ihrer Produktdokumentation oder anderen Ressourcen bereitstellen, die Sie für den Erfolg des Kunden als wichtig erachten.*
