---
keywords: airship attributes;airship destination
title: Ziel der Luftverkehrsattribute
seo-title: Ziel der Luftverkehrsattribute
description: Übermitteln Sie die Daten zur Audience der Adobe nahtlos an Airship als Audiencen-Attribute für das Targeting innerhalb von Airship.
seo-description: Übermitteln Sie die Daten zur Audience der Adobe nahtlos an Airship als Audiencen-Attribute für das Targeting innerhalb von Airship.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 12%

---


# (Beta) [!DNL Airship Attributes] Ziel {#airship-attributes-destination}

>[!IMPORTANT]
>
>Das [!DNL Airship Attributes] Ziel in Adobe Experience Platform befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

[!DNL Airship] ist die führende Plattform für Kundeninteraktion, mit der Sie Ihren Benutzern in jeder Phase des Kundenlebenszyklus aussagekräftige, personalisierte Omniannel-Nachrichten bereitstellen können.

Durch diese Integration werden Profil-Daten der Adobe [!DNL Airship] als [Attribute](https://docs.airship.com/guides/audience/attributes/) zum Targeting oder Auslösen übergeben.

Weitere Informationen finden Sie [!DNL Airship]in den [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Diese Dokumentationsseite wurde vom [!DNL Airship] Team erstellt. Bei Fragen oder Aktualisierungen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen  {#prerequisites}

Bevor Sie Ihre Audiencen-Segmente an [!DNL Airship]senden können, müssen Sie:

* Aktivieren Sie Attribute in Ihrem [!DNL Airship] Projekt.
* Generieren Sie ein Inhabertoken zur Authentifizierung.

>[!TIP]
>
>Erstellen Sie ein [!DNL Airship] Konto über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) , falls noch nicht geschehen.

### Attribute aktivieren {#enable-attributes}

Adobe Experience Platform-Profil-Attribute ähneln den [!DNL Airship] Attributen und können in der Plattform einfach zugeordnet werden, indem Sie das unten auf dieser Seite dargestellte Zuordnungswerkzeug verwenden.

[!DNL Airship] Projekte haben mehrere vordefinierte und standardmäßige Attribute. Wenn Sie ein benutzerdefiniertes Attribut haben, müssen Sie es [!DNL Airship] zuerst definieren. Weitere Informationen finden Sie unter Attribute [einrichten und verwalten](https://docs.airship.com/tutorials/audience/attributes/) .

### Platzhalter-Token {#bearer-token}

1. Gehen Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie im Menü links **[!UICONTROL Token]** .
1. Klicken Sie auf Token **[!UICONTROL erstellen]**.
1. Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Zielort für Adoben-Attribute&quot;und wählen Sie &quot;Zugriff für alle&quot;für die Rolle.
1. Klicken Sie auf &quot;Token **[!UICONTROL erstellen]** &quot;und speichern Sie die Details als vertraulich.


## Anwendungsbeispiele {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Airship Attributes] Ziel verwenden sollten, finden Sie hier Beispiele für Anwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Verwendungsfall Nr. 1

Nutzen Sie die in Adobe Experience Platform erfassten Profil-Daten zur Personalisierung der Nachricht und des Rich-Content in einem der Kanal [!DNL Airship]der Website. Verwenden Sie beispielsweise [!DNL Experience Platform] Profil-Daten, um Standortattribute innerhalb von festzulegen [!DNL Airship]. Dadurch kann eine Hotelmarke ein Bild für den nächstgelegenen Hotelstandort für jeden Benutzer anzeigen.

### Verwendungsfall Nr. 2

Nutzen Sie Attribute von Adobe Experience Platform, um [!DNL Airship] Profil noch weiter zu bereichern und mit SDK- oder [!DNL Airship] Vorhersagedaten zu kombinieren. Ein Einzelhändler kann beispielsweise ein Segment mit Treuestatus- und Standortdaten (Attribute von Plattform) erstellen und Daten abgeben, um hochgradig zielgerichtete Nachrichten an Benutzer im Goldloyalitätsstatus zu senden, die in Las Vegas, NV leben und eine hohe Wahrscheinlichkeit haben, gerettet zu werden. [!DNL Airship]

## Connect to [!DNL Airship Attributes] {#connect-airship-attributes}

1. Blättern Sie unter **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** zur Kategorie **[!UICONTROL Mobile Interaktion]** . Wählen Sie **[!DNL Airship Attributes]** und dann **[!UICONTROL Konfigurieren]**.

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

   ![Verbindung zu Luftverkehrsattributen](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. In the **Account** step, if you had previously set up a connection to your [!DNL Airship Attributes] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Airship Attributes]. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden, um Adobe Experience Platform mit Ihrem [!DNL Airship] Projekt zu verbinden, indem Sie das Inhabertoken verwenden, das Sie aus dem [!DNL Airship] Dashboard generiert haben.

   >[!NOTE]
   >
   >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Airship] account. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

   ![Verbindung zu Luftverkehrsattributen](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. Once your credentials are confirmed and Adobe Experience Platform is connected to your [!DNL Airship] project, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein. <br> Außerdem können Sie in diesem Schritt entweder das US- oder das EU-Rechenzentrum auswählen, je nachdem, welches [!DNL Airship] Rechenzentrum für dieses Ziel gilt. Wählen Sie schließlich einen oder mehrere Anwendungsfälle für das Marketing aus, für die Daten an das Ziel exportiert werden. Sie können aus den von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder eigene Anwendungsfälle erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br> Wählen Sie Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben.

   ![Verbindung zu Luftverkehrsattributen](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten {#activate-segments}

Gehen Sie wie folgt vor, um Segmente zu aktivieren [!DNL Airship Attributes]:

1. Wählen Sie unter **[!UICONTROL Ziele > Durchsuchen]** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten.[!DNL Airship Attributes]
   ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.
Beachten Sie, dass, wenn für ein Ziel bereits ein Seitenfluss vorhanden ist, die Aktivierungen angezeigt werden, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option **[!UICONTROL Aktivierung bearbeiten]** und führen Sie die unten beschriebenen Schritte aus, um die Aktivierungsdetails zu ändern. ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. Wählen Sie **[!UICONTROL Aktivieren]**.
1. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Airship Attributes].
   ![Segment an Ziel](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. Wählen Sie im Schritt **[!UICONTROL Zuordnung]** aus dem [XDM](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/home.html) -Schema, welche Attribute und Identitäten dem Ziel-Schema zugeordnet werden sollen. Wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]** aus, um Ihr Schema zu durchsuchen und es der entsprechenden Zielgruppe zuzuordnen.
   ![Anfangsbildschirm zur Identitätszuordnung](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] Attribute können entweder auf einem Kanal festgelegt werden, der eine Geräteinstanz darstellt, z. B. iPhone, oder auf einem benannten Benutzer, der alle Geräte eines Benutzers einem allgemeinen Bezeichner wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ohne Hashing) verwenden, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Quellattributen]** aus und ordnen Sie es dem [!DNL Airship] benannten Benutzer in der rechten Spalte unter &quot; **[!UICONTROL Zielgruppen-IDs]**&quot;zu, wie unten dargestellt.
   ![Benannte Benutzerzuordnung](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)Für IDs, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, dem entsprechenden Kanal basierend auf der Quelle zugeordnet werden. Die folgenden Bilder zeigen, wie zwei Zuordnungen erstellt werden:

   * IDFA-iOS-Anzeigen-ID für einen [!DNL Airship] iOS-Kanal
   * Adobe- `fullName` Attribut zu [!DNL Airship] &quot;Vollständiger Name&quot;

   >[!NOTE]
   >
   >Verwenden Sie den benutzerfreundlichen Namen, der im [!DNL Airship] Dashboard angezeigt wird, wenn Sie das Feld &quot;Zielgruppe&quot;für Ihre Attributzuordnung auswählen.

   **Zuordnen der Identität**Quellfeld auswählen:
   ![Verbindung zu Luftverkehrsattributen](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)Zielgruppe auswählen:
   ![Verbindung zu Luftverkehrsattributen](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **Map-Attribut**

   Quellattribut auswählen:
   ![Quellfeld](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)auswählen Zielgruppe-Attribut auswählen:
   ![Wählen Sie die](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)Zuordnung für das Feld &quot;Zielgruppe&quot;aus:
   ![Zuordnung von Kanälen](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. Auf der Seite &quot; **[!UICONTROL Segmentplan]** &quot;ist die Planung derzeit deaktiviert. Klicken Sie auf **[!UICONTROL Weiter]** , um mit dem Review-Schritt fortzufahren. ![Zeitplanung derzeit deaktiviert](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob die Datenschutzrichtlinien verletzt wurden. Unten sehen Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Segmentarbeitsablauf erst dann abschließen, wenn Sie die Aktivierung gelöst haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](/help/rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Datenverwaltung.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Fertig stellen]** , um Ihre Auswahl zu bestätigen und den Beginn, der Daten an das Ziel sendet, zu bestätigen.

![überprüfen](/help/rtcdp/destinations/assets/airship11-review-step.png)

## Nutzung und Verwaltung von Daten {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind beim Umgang mit Ihren Daten mit den Datenverwendungsrichtlinien konform. Ausführliche Informationen zur [!DNL Adobe Experience Platform] Durchsetzung der Datenverwaltung finden Sie unter [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md).
