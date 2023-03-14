---
title: (API) Oracle Eloqua-Verbindung
description: Mit dem (API) Oracle Eloqua-Ziel können Sie Ihre Kontodaten exportieren und innerhalb von Oracle Eloqua für Ihre Geschäftsanforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 40%

---

# [!DNL (API) Oracle Eloqua]-Verbindung

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) ermöglicht es Marketing-Experten, Kampagnen zu planen und auszuführen und gleichzeitig ein personalisiertes Kundenerlebnis für ihre potenziellen Kunden bereitzustellen. Dank integrierter Lead-Verwaltung und einfacher Kampagnenerstellung können Marketingexperten die richtige Zielgruppe zum richtigen Zeitpunkt auf der Journey ansprechen und elegant skalieren, um Zielgruppen kanalübergreifend zu erreichen, einschließlich E-Mail, Display-Suche, Video und Mobil. Vertriebsteams können mehr Angebote schneller schließen und so den Marketing-ROI durch Echtzeiteinblicke steigern.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [Kontakt aktualisieren](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) Vorgang von [!DNL Oracle Eloqua] REST-API, mit der Sie Identitäten innerhalb eines Segments in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] uses [Grundlegende Authentifizierung](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) zur Kommunikation mit dem [!DNL Oracle Eloqua] REST-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Oracle Eloqua]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Als Marketing-Experte können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Segmente aus Ihren Offline-Daten erstellen und diese Segmente an [!DNL Oracle Eloqua] senden, damit sie in den Feeds der Benutzer angezeigt werden, sobald Segmente und Profile in Adobe Experience Platform aktualisiert werden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Oracle Eloqua]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Dokumentation zur Experience Platform für [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zum Segmentstatus benötigen.

### Voraussetzungen für [!DNL Oracle Eloqua] {#prerequisites-destination}

So exportieren Sie Daten von Platform in Ihre [!DNL Oracle Eloqua] -Konto, für das Sie eine [!DNL Oracle Eloqua] -Konto.

#### Sammeln von [!DNL Oracle Eloqua]-Anmeldeinformationen {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Oracle Eloqua] Ziel:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Username` | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. |
| `Password` | Das Kennwort Ihres [!DNL Oracle Eloqua] -Konto. |

## Leitplanken {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] Benutzerdefinierte Kontaktfelder werden automatisch unter Verwendung der Namen der Segmente erstellt, die während der **[!UICONTROL Segmente auswählen]** Schritt.


* [!DNL Oracle Eloqua] hat eine maximale Anzahl von 250 benutzerdefinierten Kontaktfeldern.
* Stellen Sie vor dem Export neuer Segmente sicher, dass die Anzahl der Platform-Segmente und die Anzahl der vorhandenen Segmente in [!DNL Oracle Eloqua] diese Grenze nicht überschreiten.
* Wenn diese Grenze überschritten wird, tritt bei der Experience Platform ein Fehler auf. Dies liegt daran, dass die Variable [!DNL Oracle Eloqua] Die API kann die Anfrage nicht validieren und antwortet mit einem - *400: Überprüfungsfehler* - Fehlermeldung, die das Problem beschreibt.
* Wenn Sie die oben angegebene Grenze erreicht haben, müssen Sie vorhandene Zuordnungen aus Ihrem Ziel entfernen und die entsprechenden benutzerdefinierten Kontaktfelder in Ihrem [!DNL Oracle Eloqua] , bevor Sie weitere Segmente exportieren können.

* Siehe Abschnitt [Oracle Eloqua Erstellen von Kontaktfeldern](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) Seite mit Informationen zu zusätzlichen Beschränkungen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Oracle Eloqua] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beispiel | Beschreibung | Obligatorisch |
|---|---|---|---|
| `EloquaId` | `111111` | Eindeutige Kennung des Kontakts. | Ja |

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL (API) Oracle Eloqua]. Alternativ können Sie sie unter der **[!UICONTROL E-Mail-Marketing]** Kategorie.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden Sie im Abschnitt [ [!DNL Oracle Eloqua] Sammeln von -Anmeldeinformationen](#gather-credentials).
* **[!UICONTROL Passwort]**: Das Kennwort Ihres [!DNL Oracle Eloqua] -Konto.
* **[!UICONTROL Benutzername]**: Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Zugriffssteuerung – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Oracle Eloqua]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen.

`EloquaID` ist erforderlich, um Attribute zu aktualisieren, die der Identität entsprechen. Die `emailAddress` ist auch erforderlich, da ohne sie die API einen Fehler wie unten angegeben ausgibt:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

In der Variablen **[!UICONTROL Zielfeld]** sollte genau wie in der Tabelle der Attributzuordnungen beschrieben benannt werden, da diese Attribute den Anfragetext bilden.

In der Variablen **[!UICONTROL Quellfeld]** keine solchen Einschränkungen befolgen. Sie können sie jedoch nach Bedarf zuordnen, wenn das Datenformat beim Senden an [!DNL Oracle Eloqua] wird ein Fehler ausgegeben.

Sie können beispielsweise **[!UICONTROL Quellfeld]** Identitäts-Namespace `contact key`, `ABC ID` usw. nach **[!UICONTROL Zielfeld]** : `EloquaID` nachdem sichergestellt wurde, dass die ID-Werte dem Format entsprechen, das von [!DNL Oracle Eloqua].

Um Ihre XDM-Felder den [!DNL Oracle Eloqua]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut aus oder wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität oder **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und wählen Sie nach Bedarf ein Attribut aus.
   * Wiederholen Sie diese Schritte, um die folgenden Zuordnungen zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Oracle Eloqua] instance: |Quellfeld|Zielfeld| Erforderlich| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Ja | |`IdentityMap: Eid`|`Identity: EloquaId`| Ja |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
      ![Screenshot der Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Beide `emailAddress` und `EloquaId` Zielattribut-Zuordnungen sind obligatorisch.

Wenn Sie mit der Bereitstellung der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Nächste]**.

>[!NOTE]
>
>Bei jeder Ausführung fügt das Ziel den ausgewählten Segmentnamen automatisch eine eindeutige Kennung hinzu, wenn die Kontaktinformationen an [!DNL Oracle Eloqua]. Dadurch wird sichergestellt, dass sich die Kontaktfeldnamen, die Ihren Segmentnamen entsprechen, nicht überschneiden. Siehe Abschnitt [Datenexport überprüfen](#exported-data) Screenshot-Beispiel eines Abschnitts [!DNL Oracle Eloqua] Kontaktinformationen-Seite mit benutzerdefiniertem Kontaktfeld, das mithilfe der Segmentnamen erstellt wurde.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und navigieren Sie zur Liste der Ziele.
1. Wählen Sie als Nächstes das Ziel aus und wechseln Sie zur **[!UICONTROL Aktivierungsdaten]** und wählen Sie einen Segmentnamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Überwachen Sie die Segmentzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Melden Sie sich bei der [!DNL Oracle Eloqua] Website und navigieren Sie dann zur **[!UICONTROL Kontaktübersicht]** -Seite, um zu überprüfen, ob die Profile aus dem Segment hinzugefügt wurden. Um den Segmentstatus anzuzeigen, führen Sie einen Drilldown in eine **[!UICONTROL Kontaktdetails]** und überprüfen Sie, ob das Kontaktfeld mit dem ausgewählten Segmentnamen als Präfix erstellt wurde.

![Oracle Eloqua UI-Screenshot mit der Seite &quot;Kontaktdetails&quot;mit dem benutzerdefinierten Kontaktfeld, das mit dem Segmentnamen erstellt wurde.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Erstellen des Ziels erhalten Sie möglicherweise eine der folgenden Fehlermeldungen: `400: There was a validation error` oder `400 BAD_REQUEST`. Dies geschieht, wenn Sie die Beschränkung von 250 benutzerdefinierten Kontaktfeldern überschreiten, wie im Abschnitt [Limits](#guardrails) Abschnitt. Um diesen Fehler zu beheben, dürfen Sie die benutzerdefinierte Feldbegrenzung in [!DNL Oracle Eloqua].
![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Siehe Abschnitt [[!DNL Oracle Eloqua] HTTP-Statuscodes](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) und [[!DNL Oracle Eloqua] Validierungsfehler](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) Seiten für eine umfassende Liste von Status- und Fehlercodes mit Erklärungen.

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Oracle ELoqua]Dokumentation finden Sie im Folgenden:
* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST-API für Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)