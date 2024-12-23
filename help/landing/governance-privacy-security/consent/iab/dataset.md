---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consensus
solution: Experience Platform
title: Erstellen von Datensätzen zur Erfassung von IAB TCF 2.0-Einverständnisdaten
description: Dieses Dokument enthält Schritte zum Einrichten der beiden erforderlichen Datensätze zur Erfassung der IAB TCF 2.0-Zustimmungsdaten.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 3%

---

# Erstellen von Datensätzen zur Erfassung von IAB TCF 2.0-Einwilligungsdaten

Damit Adobe Experience Platform Kundeneinwilligungsdaten gemäß IAB [!DNL Transparency & Consent Framework] (TCF) 2.0 verarbeiten kann, müssen diese Daten an Datensätze gesendet werden, deren Schemas TCF 2.0-Einwilligungsfelder enthalten.

Für die Erfassung von TCF 2.0-Einwilligungsdaten sind zwei Datensätze erforderlich:

* Ein Datensatz, der auf der [!DNL XDM Individual Profile] -Klasse basiert und für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert ist.
* Ein Datensatz, der auf der [!DNL XDM ExperienceEvent] -Klasse basiert.

>[!IMPORTANT]
>
>Platform erzwingt nur die TCF-Zeichenfolgen, die im Datensatz &quot;Individuelles Profil&quot;erfasst werden. Auch wenn ein ExperienceEvent-Datensatz im Rahmen dieses Workflows weiterhin benötigt wird, um einen Datastream zu erstellen, müssen Sie nur Daten in den Profildatensatz aufnehmen. Der ExperienceEvent-Datensatz kann weiterhin verwendet werden, wenn Sie Zustimmungsänderungsereignisse im Laufe der Zeit verfolgen möchten. Diese Werte werden jedoch nicht bei der Erzwingung der Segmentaktivierung verwendet.

In diesem Dokument werden die Schritte zum Einrichten dieser beiden Datensätze beschrieben. Einen Überblick über den vollständigen Workflow zum Konfigurieren Ihrer Platform-Datenvorgänge für TCF 2.0 finden Sie in der [IAB TCF 2.0-Kompatibilitätsübersicht](./overview.md).

## Voraussetzungen

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Ermöglicht die Verknüpfung von Kundenidentitäten aus unterschiedlichen Datenquellen über Geräte und Systeme hinweg.
   * [Identitäts-Namespaces](../../../../identity-service/features/namespaces.md): Kundenidentitätsdaten müssen unter einem bestimmten Identitäts-Namespace bereitgestellt werden, der von Identity Service erkannt wird.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Nutzt [!DNL Identity Service] , damit Sie aus Ihren Datensätzen detaillierte Kundenprofile in Echtzeit erstellen können. [!DNL Real-Time Customer Profile] ruft Daten aus dem Data Lake ab und behält Kundenprofile in seinem eigenen separaten Datenspeicher bei.

## TCF 2.0-Feldergruppen {#field-groups}

Die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent Details] enthält Felder für die Kundenzustimmung, die für die Unterstützung von TCF 2.0 erforderlich sind. Es gibt zwei Versionen dieser Feldergruppe: eine ist mit der Klasse [!DNL XDM Individual Profile] kompatibel und die andere mit der Klasse [!DNL XDM ExperienceEvent].

In den folgenden Abschnitten wird die Struktur der einzelnen Feldergruppen beschrieben, einschließlich der Daten, die sie bei der Erfassung erwarten.

### Profilfeldgruppe {#profile-field-group}

Bei Schemas, die auf [!DNL XDM Individual Profile] basieren, stellt die Feldergruppe [!UICONTROL IAB TCF 2.0 Consent Details] ein einzelnes Zuordnungsfeld (`identityPrivacyInfo`) bereit, das Kundenidentitäten ihren TCF-Zustimmungseinstellungen zuordnet. Diese Feldergruppe muss in einem datensatzbasierten Schema enthalten sein, das für das Echtzeit-Kundenprofil aktiviert ist, damit die automatische Durchsetzung erfolgt.

Weitere Informationen zu Struktur und Anwendungsfall finden Sie im [Referenzhandbuch](../../../../xdm/field-groups/profile/iab.md) für diese Feldergruppe.

### Ereignisfeldgruppe {#event-field-group}

Wenn Sie Zustimmungsänderungsereignisse im Zeitverlauf verfolgen möchten, können Sie die Feldergruppe [!UICONTROL IAB TCF 2.0 Consent Details] zu Ihrem Schema [!UICONTROL XDM ExperienceEvent] hinzufügen.

Wenn Sie nicht planen, Zustimmungsänderungsereignisse im Laufe der Zeit zu verfolgen, müssen Sie diese Feldergruppe nicht in Ihr Ereignisschema aufnehmen. Beim automatischen Erzwingen von TCF-Zustimmungswerten verwendet Experience Platform nur die neuesten Zustimmungsinformationen, die in die [Profilfeldgruppe](#profile-field-group) aufgenommen wurden. Die von Ereignissen erfassten Zustimmungswerte nehmen nicht an automatischen Durchsetzungs-Workflows teil.

Weitere Informationen zu Struktur und Anwendungsfall finden Sie im [Referenzhandbuch](../../../../xdm/field-groups/event/iab.md) für diese Feldergruppe.

## Erstellen von Einverständnisschemata für Kunden {#create-schemas}

Um Datensätze zu erstellen, die Einwilligungsdaten erfassen, müssen Sie zunächst XDM-Schemas erstellen, auf denen diese Datensätze basieren.

Wie im vorherigen Abschnitt erwähnt, ist ein Schema erforderlich, das die Klasse [!UICONTROL XDM Individual Profile] verwendet, um die Zustimmung in nachgelagerten Platform-Workflows zu erzwingen. Sie können optional auch ein separates Schema basierend auf [!UICONTROL XDM ExperienceEvent] erstellen, wenn Sie Zustimmungsänderungen im Laufe der Zeit verfolgen möchten. Beide Schemas müssen ein `identityMap` -Feld und eine entsprechende TCF 2.0-Feldergruppe enthalten.

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** aus, um den Arbeitsbereich [!UICONTROL Schemas] zu öffnen. Führen Sie von hier aus die Schritte in den folgenden Abschnitten aus, um jedes erforderliche Schema zu erstellen.

>[!NOTE]
>
>Wenn Sie über vorhandene XDM-Schemas verfügen, mit denen Sie stattdessen Einwilligungsdaten erfassen möchten, können Sie diese Schemas bearbeiten, anstatt neue Schemas zu erstellen. Wenn jedoch ein vorhandenes Schema für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, kann seine primäre Identität nicht ein direkt identifizierbares Feld sein, das nicht in interessensbasierter Werbung verwendet werden darf, z. B. eine E-Mail-Adresse. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.
>
>Darüber hinaus können bei der Bearbeitung vorhandener Schemas nur additive (nicht brechende) Änderungen vorgenommen werden. Weitere Informationen finden Sie im Abschnitt zu den [Prinzipien der Schemaentwicklung](../../../../xdm/schema/composition.md#evolution) .

### Erstellen eines Profilzustimmungsschemas {#profile-schema}

Wählen Sie **[!UICONTROL Schema erstellen]** und dann **[!UICONTROL XDM Individual Profile]** aus dem Dropdown-Menü.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Das Dialogfeld **[!UICONTROL Feldgruppen hinzufügen]** wird angezeigt, mit dem Sie sofort mit dem Hinzufügen von Feldergruppen zum Schema beginnen können. Wählen Sie hier **[!UICONTROL IAB TCF 2.0 Consent Details]** aus der Liste aus. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Suchen Sie anschließend die Feldergruppe **[!UICONTROL IdentityMap]** aus der Liste und wählen Sie sie auch aus. Sobald beide Feldergruppen in der rechten Leiste aufgelistet sind, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

Die Arbeitsfläche wird wieder angezeigt und zeigt an, dass die Felder `identityPrivacyInfo` und `identityMap` zur Schemastruktur hinzugefügt wurden.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Bevor Sie dem Schema weitere Felder hinzufügen, wählen Sie das Stammfeld aus, um in der rechten Leiste **[!UICONTROL Schemaeigenschaften]** anzuzeigen. Hier können Sie einen Namen und eine Beschreibung für das Schema angeben.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Nachdem Sie einen Namen und eine Beschreibung angegeben haben, können Sie optional weitere Felder zum Schema hinzufügen, indem Sie auf der linken Seite der Arbeitsfläche unter dem Abschnitt **[!UICONTROL Feldergruppen]** die Option **[!UICONTROL Hinzufügen]** auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Wenn Sie ein vorhandenes Schema bearbeiten, das bereits für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert wurde, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu bestätigen, bevor Sie mit dem Abschnitt zum Erstellen eines Datensatzes basierend auf Ihrem Einwilligungsschema fortfahren.](#dataset) [ Wenn Sie ein neues Schema erstellen, führen Sie die im folgenden Unterabschnitt beschriebenen Schritte aus.

#### Aktivieren des Schemas für die Verwendung in [!DNL Real-Time Customer Profile]

Damit Platform die eingehenden Zustimmungsdaten bestimmten Kundenprofilen zuordnen kann, muss das Einwilligungsschema für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert sein.

>[!NOTE]
>
>Das in diesem Abschnitt gezeigte Beispielschema verwendet sein `identityMap` -Feld als primäre Identität. Wenn Sie ein anderes Feld als primäre Identität festlegen möchten, stellen Sie sicher, dass Sie eine indirekte Kennung wie eine Cookie-ID verwenden und nicht ein direkt identifizierbares Feld, das in interessensbasierter Werbung nicht verwendet werden darf, z. B. eine E-Mail-Adresse. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.
>
>Schritte zum Festlegen eines primären Identitätsfelds für ein Schema finden Sie im Handbuch [[!UICONTROL Schemas] Benutzeroberfläche](../../../../xdm/ui/fields/identity.md) .

Um das Schema für [!DNL Profile] zu aktivieren, wählen Sie in der linken Leiste den Namen des Schemas aus, um den Abschnitt **[!UICONTROL Schemaeigenschaften]** zu öffnen. Wählen Sie hier die Schaltfläche **[!UICONTROL Profil]**-Umschalter aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Es wird ein Popup angezeigt, das auf eine fehlende primäre Identität hinweist. Aktivieren Sie das Kontrollkästchen für die Verwendung einer alternativen primären Identität, da die primäre Identität im Feld `identityMap` enthalten sein wird.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Wählen Sie abschließend **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu bestätigen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Erstellen eines Zustimmungsschemas für Ereignisse {#event-schema}

>[!NOTE]
>
>Einwilligungsschemata für Ereignisse werden nur verwendet, um Einwilligungsänderungen im Laufe der Zeit zu verfolgen, und nehmen nicht an nachgelagerten Durchsetzungs-Workflows teil. Wenn Sie Zustimmungsänderungen im Laufe der Zeit nicht verfolgen möchten, können Sie mit dem nächsten Abschnitt zum Erstellen von Einwilligungsdatensätzen [ fortfahren.](#datasets)

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemas]** die Option **[!UICONTROL Schema erstellen]** und wählen Sie dann **[!UICONTROL XDM ExperienceEvent]** aus der Dropdown-Liste.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Das Dialogfeld **[!UICONTROL Feldgruppen hinzufügen]** wird angezeigt. Wählen Sie hier **[!UICONTROL IAB TCF 2.0 Consent Details]** aus der Liste aus. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Suchen Sie anschließend die Feldergruppe **[!UICONTROL IdentityMap]** aus der Liste und wählen Sie sie auch aus. Sobald beide Feldergruppen in der rechten Leiste aufgelistet sind, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

Die Arbeitsfläche wird wieder angezeigt und zeigt an, dass die Felder `consentStrings` und `identityMap` zur Schemastruktur hinzugefügt wurden.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Bevor Sie dem Schema weitere Felder hinzufügen, wählen Sie das Stammfeld aus, um in der rechten Leiste **[!UICONTROL Schemaeigenschaften]** anzuzeigen. Hier können Sie einen Namen und eine Beschreibung für das Schema angeben.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Nachdem Sie einen Namen und eine Beschreibung angegeben haben, können Sie optional weitere Felder zum Schema hinzufügen, indem Sie auf der linken Seite der Arbeitsfläche unter dem Abschnitt **[!UICONTROL Feldergruppen]** die Option **[!UICONTROL Hinzufügen]** auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Nachdem die erforderlichen Feldergruppen hinzugefügt wurden, schließen Sie die Auswahl von **[!UICONTROL Speichern]** ab.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Erstellen von Datensätzen basierend auf Ihren Einwilligungsschemas {#datasets}

Für jedes der oben beschriebenen erforderlichen Schemas müssen Sie einen Datensatz erstellen, in dem letztendlich die Zustimmungsdaten Ihrer Kunden erfasst werden. Der Datensatz, der auf dem Datensatzschema basiert, muss für [!DNL Real-Time Customer Profile] aktiviert sein, während der Datensatz, der auf dem Zeitreihenschema **basiert, nicht** [!DNL Profile]-fähig sein sollte.

Wählen Sie zunächst **[!UICONTROL Datensätze]** im linken Navigationsbereich und dann oben rechts **[!UICONTROL Datensatz erstellen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Wählen Sie auf der nächsten Seite **[!UICONTROL Datensatz aus Schema erstellen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Der Workflow **[!UICONTROL Datensatz aus Schema erstellen]** wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Schema auswählen]** . Suchen Sie in der bereitgestellten Liste eines der zuvor erstellten Einwilligungsschemas. Sie können optional die Suchleiste verwenden, um Ergebnisse einzuschränken und Ihr Schema leichter zu finden. Wählen Sie das Optionsfeld neben dem gewünschten Schema aus und wählen Sie dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz ein, bevor Sie **[!UICONTROL Beenden]** auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem Zeitreihenschema basiert, ist der Prozess abgeschlossen. Wenn der Datensatz auf Ihrem Datensatzschema basiert, besteht der letzte Schritt im Prozess darin, den Datensatz zur Verwendung in [!DNL Real-Time Customer Profile] zu aktivieren.

Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profil]** und dann im Bestätigungs-Popup die Option **[!UICONTROL Aktivieren]** aus, um das Schema für [!DNL Profile] zu aktivieren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Führen Sie die oben genannten Schritte erneut aus, um einen ereignisbasierten Datensatz zu erstellen, wenn Sie ein Schema dafür erstellt haben.

## Nächste Schritte

In diesem Tutorial haben Sie mindestens einen Datensatz erstellt, der jetzt zur Erfassung von Kundenzustimmungsdaten verwendet werden kann:

* Ein datensatzbasierter Datensatz, der für die Verwendung im Echtzeit-Kundenprofil aktiviert ist. **(Erforderlich)**
* Ein zeitreihenbasierter Datensatz, der nicht für [!DNL Profile] aktiviert ist. (Optional)

Sie können jetzt zur [IAB TCF 2.0 - Übersicht](./overview.md#merge-policies) zurückkehren, um den Prozess der Konfiguration von Platform für die TCF 2.0-Konformität fortzusetzen.
