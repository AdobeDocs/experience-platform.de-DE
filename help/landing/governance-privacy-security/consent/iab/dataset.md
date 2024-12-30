---
keywords: Experience Platform;Startseite;IAB;IAB 2.0;Einverständnis;Einverständnis
solution: Experience Platform
title: Erstellen von Datensätzen zur Erfassung von IAB TCF 2.0-Einverständnisdaten
description: In diesem Dokument werden die Schritte zum Einrichten der beiden erforderlichen Datensätze beschrieben, um IAB TCF 2.0-Einverständnisdaten zu erfassen.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 3%

---

# Erstellen von Datensätzen zur Erfassung von IAB TCF 2.0-Einverständnisdaten

Damit Adobe Experience Platform Kundeneinverständnisdaten gemäß IAB [!DNL Transparency & Consent Framework] (TCF) 2.0 verarbeiten kann, müssen diese Daten an Datensätze gesendet werden, deren Schemata TCF 2.0-Einverständnisfelder enthalten.

Insbesondere sind zwei Datensätze erforderlich, um TCF 2.0-Einverständnisdaten zu erfassen:

* Ein auf der [!DNL XDM Individual Profile] basierender Datensatz, der für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert ist.
* Ein auf der [!DNL XDM ExperienceEvent] basierender Datensatz.

>[!IMPORTANT]
>
>Platform erzwingt nur die TCF-Zeichenfolgen, die im Datensatz „Individuelles Profil“ erfasst sind. Während ein ExperienceEvent-Datensatz im Rahmen dieses Workflows weiterhin erforderlich ist, um einen Datenstrom zu erstellen, müssen Sie nur Daten in den Profildatensatz aufnehmen. Der ExperienceEvent-Datensatz kann weiterhin verwendet werden, wenn Sie Einverständnisänderungsereignisse im Laufe der Zeit verfolgen möchten, aber diese Werte werden beim Erzwingen der Segmentaktivierung nicht in verwendet.

In diesem Dokument werden die Schritte zum Einrichten dieser beiden Datensätze beschrieben. Einen Überblick über den gesamten Workflow zur Konfiguration der Platform-Datenvorgänge für TCF 2.0 erhalten Sie im Abschnitt [IAB TCF 2.0-Kompatibilitätsübersicht](./overview.md).

## Voraussetzungen

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Erfahren Sie mehr über die Grundbausteine von XDM-Schemata.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Ermöglicht es Ihnen, Kundenidentitäten aus Ihren unterschiedlichen Datenquellen geräte- und systemübergreifend zu verbinden.
   * [Identity-Namespaces](../../../../identity-service/features/namespaces.md): Kundenidentitätsdaten müssen unter einem bestimmten Identity-Namespace bereitgestellt werden, der von Identity Service erkannt wird.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Nutzt [!DNL Identity Service], um Ihnen die Erstellung detaillierter Kundenprofile aus Ihren Datensätzen in Echtzeit zu ermöglichen. [!DNL Real-Time Customer Profile] ruft Daten aus dem Data Lake ab und speichert Kundenprofile in einem eigenen separaten Datenspeicher.

## TCF 2.0-Feldergruppen {#field-groups}

Die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent Details] stellt Felder für das Kundeneinverständnis bereit, die für die TCF 2.0-Unterstützung erforderlich sind. Es gibt zwei Versionen dieser Feldergruppe: eine ist mit der [!DNL XDM Individual Profile]-Klasse kompatibel und die andere mit der [!DNL XDM ExperienceEvent]-Klasse.

In den folgenden Abschnitten wird die Struktur jeder dieser Feldergruppen erläutert, einschließlich der Daten, die während der Aufnahme erwartet werden.

### Profilfeldgruppe {#profile-field-group}

Für Schemata, die auf [!DNL XDM Individual Profile] basieren, bietet die Feldergruppe [!UICONTROL IAB TCF 2.0 Consent Details] ein einziges Feld vom Typ Zuordnung, `identityPrivacyInfo`, das Kundenidentitäten ihren TCF-Einverständnisvoreinstellungen zuordnet. Diese Feldergruppe muss in einem datensatzbasierten Schema enthalten sein, das für das Echtzeit-Kundenprofil aktiviert ist, damit die automatische Durchsetzung stattfindet.

Weitere Informationen [ Struktur und Anwendungsfall finden ](../../../../xdm/field-groups/profile/iab.md) im „Referenzhandbuch“ für diese Feldergruppe.

### Ereignisfeldgruppe {#event-field-group}

Wenn Sie Einverständnisänderungsereignisse im Laufe der Zeit verfolgen möchten, können Sie die Feldergruppe [!UICONTROL IAB TCF 2.0 Einverständnisdetails] zu Ihrem [!UICONTROL XDM ExperienceEvent]-Schema hinzufügen.

Wenn Sie nicht planen, Einverständnisänderungsereignisse im Laufe der Zeit zu verfolgen, müssen Sie diese Feldergruppe nicht in Ihr Ereignisschema aufnehmen. Beim automatischen Durchsetzen von TCF-Einverständniswerten verwendet Experience Platform nur die neuesten Einverständnisinformationen, die in die [Profilfeldgruppe“ aufgenommen ](#profile-field-group). Die von Ereignissen erfassten Einverständniswerte sind nicht Teil der automatischen Erzwingungs-Workflows.

Weitere Informationen zu [ Struktur und ](../../../../xdm/field-groups/event/iab.md) Anwendungsfall dieser Feldergruppe finden Sie im „Referenzhandbuch“ für diese Feldergruppe .

## Erstellen von Kundeneinverständnisschemata {#create-schemas}

Um Datensätze zu erstellen, die Einverständnisdaten erfassen, müssen Sie zunächst XDM-Schemata erstellen, auf denen diese Datensätze basieren.

Wie im vorherigen Abschnitt erwähnt, ist ein Schema erforderlich, das die Klasse [!UICONTROL XDM Individual Profile] verwendet, um das Einverständnis in nachgelagerten Platform-Workflows zu erzwingen. Optional können Sie auch ein separates Schema auf der Grundlage von [!UICONTROL XDM ExperienceEvent] erstellen, wenn Sie Einverständnisänderungen im Laufe der Zeit verfolgen möchten. Beide Schemata müssen ein `identityMap` und eine entsprechende TCF 2.0-Feldergruppe enthalten.

Wählen Sie in der Platform **[!UICONTROL Benutzeroberfläche im linken Navigationsbereich die Option]** Schemata“ aus, um den Arbeitsbereich [!UICONTROL Schemata] zu öffnen. Führen Sie von hier aus die Schritte in den folgenden Abschnitten aus, um jedes erforderliche Schema zu erstellen.

>[!NOTE]
>
>Wenn Sie über vorhandene XDM-Schemata verfügen, mit denen Sie stattdessen Einverständnisdaten erfassen möchten, können Sie diese Schemata bearbeiten, anstatt neue zu erstellen. Wenn ein vorhandenes Schema jedoch für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, kann seine primäre Identität kein direkt identifizierbares Feld sein, das in interessenbasierter Werbung wie einer E-Mail-Adresse nicht verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.
>
>Darüber hinaus können beim Bearbeiten vorhandener Schemata nur additive (nicht unterbrechende) Änderungen vorgenommen werden. Weitere Informationen finden Sie im Abschnitt [Grundsätze ](../../../../xdm/schema/composition.md#evolution) Schemaentwicklung“.

### Erstellen eines Einverständnisschemas für Profile {#profile-schema}

Wählen **[!UICONTROL Schema erstellen]** und dann **[!UICONTROL Individuelles XDM-Profil]** aus dem Dropdown-Menü aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Der **[!UICONTROL Feldergruppen hinzufügen]** wird angezeigt, sodass Sie sofort mit dem Hinzufügen von Feldergruppen zum Schema beginnen können. Wählen Sie hier **[!UICONTROL IAB TCF 2.0 Consent Details]** aus der Liste aus. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Suchen Sie als Nächstes die **[!UICONTROL IdentityMap]**-Feldergruppe aus der Liste und wählen Sie sie ebenfalls aus. Sobald beide Feldergruppen in der rechten Leiste aufgeführt sind, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

Die Arbeitsfläche wird erneut angezeigt und zeigt an, dass die Felder `identityPrivacyInfo` und `identityMap` zur Schemastruktur hinzugefügt wurden.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Bevor Sie weitere Felder zum Schema hinzufügen, wählen Sie das Stammfeld aus, um **[!UICONTROL Schemaeigenschaften]** in der rechten Leiste anzuzeigen, wo Sie einen Namen und eine Beschreibung für das Schema angeben können.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Nachdem Sie einen Namen und eine Beschreibung angegeben haben, können Sie optional weitere Felder zum Schema hinzufügen, indem Sie **[!UICONTROL Hinzufügen]** im Abschnitt **[!UICONTROL Feldergruppen]** auf der linken Seite der Arbeitsfläche auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Wenn Sie ein vorhandenes Schema bearbeiten, das bereits für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert wurde, wählen Sie **[!UICONTROL Speichern]** aus, um Ihre Änderungen zu bestätigen, bevor Sie mit dem Abschnitt [Erstellen eines Datensatzes basierend auf Ihrem Einverständnisschema“ ](#dataset). Wenn Sie ein neues Schema erstellen, fahren Sie mit den im folgenden Unterabschnitt beschriebenen Schritten fort.

#### Aktivieren des Schemas für die Verwendung in [!DNL Real-Time Customer Profile]

Damit Platform die erhaltenen Einverständnisdaten mit bestimmten Kundenprofilen verknüpfen kann, muss das Einverständnisschema für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert sein.

>[!NOTE]
>
>Das in diesem Abschnitt dargestellte Beispielschema verwendet sein `identityMap` Feld als primäre Identität. Wenn Sie ein anderes Feld als primäre Identität festlegen möchten, stellen Sie sicher, dass Sie eine indirekte Kennung wie eine Cookie-ID und kein direkt identifizierbares Feld verwenden, das in interessenbasierter Werbung wie einer E-Mail-Adresse nicht verwendet werden darf. Wenden Sie sich an Ihren Rechtsbeistand, wenn Sie sich nicht sicher sind, welche Felder eingeschränkt sind.
>
>Anweisungen zum Festlegen eines primären Identitätsfelds für ein Schema finden Sie im [[!UICONTROL  zur Benutzeroberfläche ]Schemas](../../../../xdm/ui/fields/identity.md).

Um das Schema für die [!DNL Profile] zu aktivieren, wählen Sie den Namen des Schemas in der linken Leiste aus, um den Abschnitt **[!UICONTROL Schemaeigenschaften]** zu öffnen. Wählen Sie von hier aus den **[!UICONTROL Profil]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Ein Pop-up wird angezeigt, das auf eine fehlende primäre Identität hinweist. Aktivieren Sie das Kontrollkästchen für die Verwendung einer alternativen primären Identität, da die primäre Identität im Feld `identityMap` enthalten sein wird.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Klicken Sie abschließend **[!UICONTROL Speichern]**, um Ihre Änderungen zu bestätigen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Erstellen eines Ereignis-Einverständnisschemas {#event-schema}

>[!NOTE]
>
>Ereigniseinverständnisschemata werden nur verwendet, um Einverständnisänderungsereignisse im Laufe der Zeit zu verfolgen, und werden nicht in nachgelagerten Durchsetzungs-Workflows einbezogen. Wenn Sie Einverständnisänderungen nicht im Laufe der Zeit verfolgen möchten, können Sie mit dem nächsten Abschnitt zum Erstellen [ Einverständnisdatensätzen ](#datasets).

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemata]** die Option **[!UICONTROL Schema erstellen]** und wählen Sie dann **[!UICONTROL XDM ExperienceEvent]** aus der Dropdown-Liste aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Das **[!UICONTROL Feldergruppen hinzufügen]** wird angezeigt. Wählen Sie hier **[!UICONTROL IAB TCF 2.0 Consent Details]** aus der Liste aus. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und die Feldergruppe leichter zu finden.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Suchen Sie als Nächstes die **[!UICONTROL IdentityMap]**-Feldergruppe aus der Liste und wählen Sie sie ebenfalls aus. Sobald beide Feldergruppen in der rechten Leiste aufgeführt sind, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

Die Arbeitsfläche wird erneut angezeigt und zeigt an, dass die Felder `consentStrings` und `identityMap` zur Schemastruktur hinzugefügt wurden.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Bevor Sie weitere Felder zum Schema hinzufügen, wählen Sie das Stammfeld aus, um **[!UICONTROL Schemaeigenschaften]** in der rechten Leiste anzuzeigen, wo Sie einen Namen und eine Beschreibung für das Schema angeben können.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Nachdem Sie einen Namen und eine Beschreibung angegeben haben, können Sie optional weitere Felder zum Schema hinzufügen, indem Sie **[!UICONTROL Hinzufügen]** im Abschnitt **[!UICONTROL Feldergruppen]** auf der linken Seite der Arbeitsfläche auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Nachdem die erforderlichen Feldergruppen hinzugefügt wurden, klicken Sie zum Abschluss auf **[!UICONTROL Speichern]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Erstellen von Datensätzen basierend auf Ihren Einverständnisschemata {#datasets}

Für jedes der oben beschriebenen erforderlichen Schemata müssen Sie einen Datensatz erstellen, der letztendlich die Einverständnisdaten Ihrer Kunden aufnimmt. Der Datensatz, der auf dem Datensatzschema basiert, muss für [!DNL Real-Time Customer Profile] aktiviert sein, während der Datensatz, der auf dem Zeitreihenschema basiert (**nicht**), [!DNL Profile] sein sollte.

Wählen Sie zunächst **[!UICONTROL linken Navigationsbereich]** Datensätze“ und dann oben rechts **[!UICONTROL Datensatz erstellen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Wählen Sie auf der nächsten Seite **[!UICONTROL Datensatz aus Schema erstellen]** aus.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Der **[!UICONTROL Datensatz aus Schema erstellen]** wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Schema auswählen]**. Suchen Sie in der bereitgestellten Liste nach einem der Einverständnisschemata, die Sie zuvor erstellt haben. Sie können optional die Suchleiste verwenden, um die Ergebnisse einzugrenzen und Ihr Schema leichter zu finden. Klicken Sie auf das Optionsfeld neben dem gewünschten Schema und dann auf **[!UICONTROL Weiter]** um fortzufahren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie einen eindeutigen, leicht identifizierbaren Namen und eine Beschreibung für den Datensatz an, bevor Sie **[!UICONTROL Beenden]** auswählen.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Die Detailseite für den neu erstellten Datensatz wird angezeigt. Wenn der Datensatz auf Ihrem Zeitreihenschema basiert, ist der Prozess abgeschlossen. Wenn der Datensatz auf Ihrem Datensatzschema basiert, besteht der letzte Schritt des Prozesses darin, den Datensatz für die Verwendung in [!DNL Real-Time Customer Profile] zu aktivieren.

Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profil]** und wählen Sie dann im Bestätigungs-]**die Option**[!UICONTROL  Aktivieren, um das Schema für die [!DNL Profile] zu aktivieren.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Führen Sie die oben genannten Schritte erneut aus, um einen ereignisbasierten Datensatz zu erstellen, wenn Sie ein Schema dafür erstellt haben.

## Nächste Schritte

In diesem Tutorial haben Sie mindestens einen Datensatz erstellt, der jetzt zur Erfassung von Kundeneinverständnisdaten verwendet werden kann:

* Ein datensatzbasierter Datensatz, der für die Verwendung im Echtzeit-Kundenprofil aktiviert ist. **(erforderlich)**
* Ein zeitreihenbasierter Datensatz, der nicht für die [!DNL Profile] aktiviert ist. (Optional)

Sie können jetzt zur Übersicht über [IAB TCF 2.0](./overview.md#merge-policies) zurückkehren, um mit der Konfiguration von Platform für die Einhaltung von TCF 2.0 fortzufahren.
