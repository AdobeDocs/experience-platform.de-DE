---
keywords: Segmentstreaming-Ziele aktivieren; Segmentstreaming-Ziele aktivieren; Daten aktivieren
title: Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele
type: Tutorial
seo-title: Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppendaten aktivieren, indem Sie Segmente Segmenten Segmentstreaming-Zielen zuordnen.
seo-description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppendaten aktivieren, indem Sie Segmente Segmenten Segmentstreaming-Zielen zuordnen.
source-git-commit: 65e74041aeb285cb80c67e47ccdaca18de9889fa
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 4%

---


# Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform-Segmentstreaming-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie über eine erfolgreiche [Verbindung zu einem Ziel](./connect-destination.md) verfügen. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Ziel auswählen {#select-destination}

1. Gehen Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus.

   ![Registerkarte &quot;Ziel durchsuchen&quot;](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. Wählen Sie die Schaltfläche **[!UICONTROL Segmente hinzufügen]** aus, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltflächen aktivieren](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. Navigieren Sie zum nächsten Abschnitt [wählen Sie Ihre Segmente](#select-segments) aus.

## Segmente auswählen {#select-segments}

Verwenden Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Segmente auswählen](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Zuordnen von Attributen und Identitäten {#mapping}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Umwandlung anwenden"
>abstract="Aktivieren Sie diese Option bei Verwendung von nicht gehashten Quellfeldern, damit Adobe Experience Platform sie bei Aktivierung automatisch hash."

>[!IMPORTANT]
>
>Dieser Schritt gilt nur für einige Segment-Streaming-Ziele. Wenn für Ihre Ziele kein Schritt **[!UICONTROL Mapping]** vorhanden ist, überspringen Sie zu [Segmentexport planen](#scheduling).

Bei einigen Segmentstreaming-Zielen müssen Sie Quellattribute oder Identitäts-Namespaces auswählen, um sie als Zielidentitäten im Ziel zuzuordnen.

1. Wählen Sie auf der Seite **[!UICONTROL Mapping]** die Option **[!UICONTROL Neues Mapping hinzufügen]** aus.

   ![Neues Mapping hinzufügen](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Quellfeld]** aus.

   ![Quellfeld auswählen](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Verwenden Sie auf der Seite **[!UICONTROL Quellfeld]** auswählen die Optionen **[!UICONTROL Attribute auswählen]** oder **[!UICONTROL Identitäts-Namespace auswählen]** , um zwischen den beiden Kategorien der verfügbaren Quellfelder zu wechseln. Wählen Sie aus den verfügbaren [!DNL XDM]-Profilattributen und Identitäts-Namespaces die Namespaces aus, die Sie dem Ziel zuordnen möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   ![Quellfeldseite auswählen](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Wählen Sie die Schaltfläche rechts neben dem Eintrag **[!UICONTROL Zielfeld]** aus.

   ![Zielgruppenfeld auswählen](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Zielfeld]** aus, wählen Sie den Zielidentitäts-Namespace aus, dem Sie das Quellfeld zuordnen möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Zielfeldseite auswählen](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 5.

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Facebook Custom Audience] {#example-facebook}

Nachstehend finden Sie ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Facebook Custom Audience].

Auswählen von Quellfeldern:

* Wählen Sie den Namespace `Email` als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht sind.
* Wählen Sie den Namespace `Email_LC_SHA256` als Quellidentität aus, wenn Sie Kunden-E-Mail-Adressen bei der Datenerfassung in [!DNL Platform] gehasht haben, gemäß [!DNL Facebook] [E-Mail-Hashing-Anforderungen](../catalog/social/facebook.md#email-hashing-requirements).
* Wählen Sie den Namespace `PHONE_E.164` als Quellkennung aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] werden die Telefonnummern hash, um die  [!DNL Facebook] Anforderungen zu erfüllen.
* Wählen Sie den Namespace `Phone_SHA256` als Quellidentität aus, wenn Sie bei der Datenerfassung Telefonnummern gemäß [!DNL Facebook] [ [!DNL Platform]Anforderungen an das Hashing von Telefonnummern](../catalog/social/facebook.md#phone-number-hashing-requirements) gehasht haben.
* Wählen Sie den Namespace `IDFA` als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den Namespace `GAID` als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den Namespace `Custom` als Quellidentität aus, wenn Ihre Daten aus einem anderen Kennungstyp bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `Email_LC_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` lauten.
* Wählen Sie den Namespace `Phone_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256` lauten.
* Wählen Sie die Namespaces `IDFA` oder `GAID` als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` lauten.
* Wählen Sie den Namespace `Extern_ID` als Zielidentität aus, wenn Ihr Quellnamespace ein benutzerdefinierter Namespace ist.

>[!IMPORTANT]
>
>Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.
> 
>Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash.

![Identitätszuordnung](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match] {#example-gcm}

Dies ist ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Google Customer Match].

Auswählen von Quellfeldern:

* Wählen Sie den Namespace `Email` als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht sind.
* Wählen Sie den Namespace `Email_LC_SHA256` als Quellidentität aus, wenn Sie Kunden-E-Mail-Adressen bei der Datenerfassung in [!DNL Platform] gehasht haben, gemäß [!DNL Google Customer Match] [E-Mail-Hashing-Anforderungen](../catalog/social/../advertising/google-customer-match.md).
* Wählen Sie den Namespace `PHONE_E.164` als Quellkennung aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] werden die Telefonnummern hash, um die  [!DNL Google Customer Match] Anforderungen zu erfüllen.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Quellidentität aus, wenn Sie bei der Datenerfassung Telefonnummern gemäß [!DNL Facebook] [ [!DNL Platform]Anforderungen an das Hashing von Telefonnummern](../catalog/social/../advertising/google-customer-match.md) gehasht haben.
* Wählen Sie den Namespace `IDFA` als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den Namespace `GAID` als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den Namespace `Custom` als Quellidentität aus, wenn Ihre Daten aus einem anderen Kennungstyp bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `Email_LC_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` lauten.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256_E.164` lauten.
* Wählen Sie die Namespaces `IDFA` oder `GAID` als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` lauten.
* Wählen Sie den Namespace `User_ID` als Zielidentität aus, wenn Ihr Quellnamespace ein benutzerdefinierter Namespace ist.

![Identitätszuordnung](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.

Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash.

![Identity Mapping Transformation](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Segmentexport planen {#scheduling}

1. Wählen Sie auf der Seite **[!UICONTROL Segment schedule]** jedes Segment aus und konfigurieren Sie dann mithilfe der Selektoren **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** das Zeitintervall für das Senden von Daten an Ihr Ziel.

   ![Segmentplan](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Bei einigen Zielen müssen Sie für jedes Segment den **[!UICONTROL Ursprung der Zielgruppe]** mithilfe des Dropdown-Menüs unter den Kalenderselektoren auswählen. Wenn Ihr Ziel diesen Selektor nicht enthält, überspringen Sie diesen Schritt.

      ![Mapping-ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Bei einigen Zielen müssen Sie [!DNL Platform]-Segmente manuell ihrem Gegenstück im Ziel zuordnen. Wählen Sie dazu jedes Segment aus und geben Sie dann die entsprechende Segment-ID aus der Zielplattform in das Feld **[!UICONTROL Zuordnungs-ID]** ein. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

      ![Mapping-ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Bei einigen Zielen müssen Sie eine **[!UICONTROL App-ID]** eingeben, wenn Sie [!DNL IDFA]- oder [!DNL GAID]-Segmente aktivieren. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

      ![App-ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Wählen Sie **[!UICONTROL Next]** aus, um zur Seite [!UICONTROL Review] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Data Governance-Dokumentation.

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-segment-streaming-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}

Überprüfen Sie Ihr Zielkonto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihre Zielplattform eingefügt.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
