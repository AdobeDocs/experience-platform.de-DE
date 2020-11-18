---
keywords: airship tags;airship destination
title: Ziel der Airship Tags
seo-title: Ziel der Airship Tags
description: Übergeben Sie nahtlos Daten zur Audience der Adobe als Audience-Tags für das Targeting innerhalb von Airship an Airship.
seo-description: Übergeben Sie nahtlos Daten zur Audience der Adobe als Audience-Tags für das Targeting innerhalb von Airship an Airship.
translation-type: tm+mt
source-git-commit: f08b90531455cdbeb73deb83eed05ba7a9b19df6
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 12%

---


# (Beta) [!DNL Airship Tags] Ziel {#airship-tags-destination}

>[!IMPORTANT]
>
>Das [!DNL Airship Tags] Ziel in Adobe Experience Platform befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

## Übersicht

[!DNL Airship] ist die führende Plattform für Kundeninteraktion, mit der Sie Ihren Benutzern in jeder Phase des Kundenlebenszyklus aussagekräftige, personalisierte Omniannel-Nachrichten bereitstellen können.

Diese Integration übergibt Adobe Experience Platform-Segmentdaten zum Targeting oder Auslösen [!DNL Airship] als [Tags](https://docs.airship.com/guides/audience/tags/) .

Weitere Informationen finden Sie [!DNL Airship]in den [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Diese Dokumentationsseite wurde vom [!DNL Airship] Team erstellt. Bei Fragen oder Aktualisierungen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen 

Bevor Sie Ihre Adobe Experience Platform-Segmente an [!DNL Airship]senden können, müssen Sie:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship] Projekt.
* Generieren Sie ein Inhabertoken zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie ein [!DNL Airship] Konto über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) , falls noch nicht geschehen.

### Tag-Gruppen

Das Konzept der Segmente in der Adobe Experience Platform ähnelt dem von [Tags](https://docs.airship.com/guides/audience/tags/) in Airship, wobei sich die Implementierung geringfügig unterscheidet. Diese Integration ordnet den Status der [Mitgliedschaft eines Benutzers in einem Experience Platform-Segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) dem Vorhandensein oder Nichtvorhandensein eines [!DNL Airship] -Tags zu. Beispiel: In einem Plattformsegment, in dem sich das `xdm:status` Tag ändert, wird das Tag dem `realized`[!DNL Airship] Kanal oder dem benannten Benutzer hinzugefügt, dem dieses Profil zugeordnet wird. Wenn sich die `xdm:status` Änderung auf `exited`, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* mit dem [!DNL Airship] Namen `adobe-segments`.

>[!IMPORTANT]
>
>Beim Erstellen der neuen Tag-Gruppe **Nicht aktivieren** Sie das Optionsfeld mit der Meldung &quot;[!DNL Allow these tags to be set only from your server]&quot;. Dadurch schlägt die Integration der Adobe-Tags fehl.

Anweisungen zum Erstellen der Tag-Gruppe finden Sie unter Tag-Gruppen [verwalten](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) .

### Platzhalter-Token

1. Gehen Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie im Menü links **[!UICONTROL Token]** .
1. Klicken Sie auf Token **[!UICONTROL erstellen]**.
1. Geben Sie einen benutzerfreundlichen Namen für das Token ein, z. B. &quot;Ziel der Adobe-Tags&quot;und wählen Sie &quot;Zugriff für alle&quot;für die Rolle.
1. Klicken Sie auf &quot;Token **[!UICONTROL erstellen]** &quot;und speichern Sie die Details als vertraulich.


## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Airship Tags] Ziel verwenden sollten, finden Sie hier Beispiele für Anwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Verwendungsfall Nr. 1

Einzelhändler oder Unterhaltungsplattformen können Profil für ihre Treuekunden erstellen und diese Segmente [!DNL Airship] für das Messaging-Targeting auf mobilen Kampagnen weiterleiten.

### Verwendungsfall Nr. 2

Auslösen von Eins-zu-Eins-Nachrichten in Echtzeit, wenn Benutzer in bestimmte Segmente innerhalb von Adobe Experience Platform fallen oder aus diesen herausfallen.

Ein Einzelhändler richtet beispielsweise ein markenspezifisches Jeans-Segment in Platform ein. Dieser Händler kann nun eine Mobilnachricht auslösen, sobald jemand seine Jeans-Präferenz auf eine bestimmte Marke setzt.

## Connect to [!DNL Airship Tags] {#connect-airship-tags}

1. Blättern Sie unter **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** zur Kategorie **[!UICONTROL Mobile Interaktion]** . Wählen Sie **[!DNL Airship Tags]** und dann **[!UICONTROL Konfigurieren]**.

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

   ![Verbindung zu Airship Tags](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. In the **Account** step, if you had previously set up a connection to your [!DNL Airship Tags] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Airship Tags]. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden, um Adobe Experience Platform mit Ihrem [!DNL Airship] Projekt zu verbinden, indem Sie das Inhabertoken verwenden, das Sie aus dem [!DNL Airship] Dashboard generiert haben.

   >[!NOTE]
   >
   >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Airship] account. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

   ![Verbindung zu Airship Tags](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. Once your credentials are confirmed and Adobe Experience Platform is connected to your [!DNL Airship] project, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein. <br> Außerdem können Sie in diesem Schritt entweder das US- oder das EU-Rechenzentrum auswählen, je nachdem, welches [!DNL Airship] Rechenzentrum für dieses Ziel gilt. Wählen Sie schließlich einen oder mehrere Anwendungsfälle für das Marketing aus, für die Daten an das Ziel exportiert werden. Sie können aus den von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder eigene Anwendungsfälle erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br> Wählen Sie Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben.

   ![Verbindung zu Airship Tags](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten {#activate-segments}

Gehen Sie wie folgt vor, um Segmente zu aktivieren [!DNL Airship Tags]:

1. Wählen Sie unter **[!UICONTROL Ziele > Durchsuchen]** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten. [!DNL Airship Tags] ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.
Beachten Sie, dass, wenn für ein Ziel bereits ein Seitenfluss vorhanden ist, die Aktivierungen angezeigt werden, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option **[!UICONTROL Aktivierung bearbeiten]** und führen Sie die unten beschriebenen Schritte aus, um die Aktivierungsdetails zu ändern.  ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. Wählen Sie **[!UICONTROL Aktivieren]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Airship Tags].
   ![Segment an Ziel](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. Wählen Sie im Schritt **[!UICONTROL Zuordnung]** aus dem [XDM](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/home.html) -Schema, welche Attribute und Identitäten dem Ziel-Schema zugeordnet werden sollen. Wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]** aus, um Ihr Schema zu durchsuchen und es der entsprechenden Zielgruppe zuzuordnen.
   ![Anfangsbildschirm zur Identitätszuordnung](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] -Tags können entweder auf einem Kanal eingestellt werden, der eine Geräteinstanz darstellt, z. B. iPhone, oder auf einem benannten Benutzer, der alle Geräte eines Benutzers einem allgemeinen Bezeichner wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ohne Hashing) verwenden, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Quellattributen]** aus und ordnen Sie es dem [!DNL Airship] benannten Benutzer in der rechten Spalte unter &quot; **[!UICONTROL Zielgruppen-IDs]**&quot;zu, wie unten dargestellt.
   ![Benannte Benutzerzuordnung](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)Für IDs, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, dem entsprechenden Kanal basierend auf der Quelle zugeordnet werden. Die folgenden Abbildungen zeigen, wie eine Google Advertising-ID einem [!DNL Airship] Android-Kanal zugeordnet wird.
   ![Verbindung zu Airship Tags](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![Verbindung zu Airship Tags](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![Zuordnung von Kanälen](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. Auf der Seite &quot; **[!UICONTROL Segmentplan]** &quot;ist die Planung derzeit deaktiviert. Klicken Sie auf **[!UICONTROL Weiter]** , um mit dem Review-Schritt fortzufahren.
7. Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob die Datenschutzrichtlinien verletzt wurden. Unten sehen Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Segmentarbeitsablauf erst dann abschließen, wenn Sie die Aktivierung gelöst haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](/help/rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Datenverwaltung.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Fertig stellen]** , um Ihre Auswahl zu bestätigen und den Beginn, der Daten an das Ziel sendet, zu bestätigen.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## Nutzung und Verwaltung von Daten {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind beim Umgang mit Ihren Daten mit den Datenverwendungsrichtlinien konform. Ausführliche Informationen zur [!DNL Adobe Experience Platform] Durchsetzung der Datenverwaltung finden Sie unter [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md).

