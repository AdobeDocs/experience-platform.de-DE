---
title: Freigegebene private Erweiterungspakete
description: Erfahren Sie, wie Sie private Erweiterungspakete in Adobe Experience Platform Tags freigeben können.
source-git-commit: f45f58b4679b619708204cdb0c18174a4836ce8d
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Freigegebene private Erweiterungspakete

Adobe Experience Platform Tags unterstützt jetzt **[!UICONTROL Usage Authorizations]**, eine leistungsstarke Funktion, mit der Sie private Erweiterungspakete sicher für vertrauenswürdige Partner freigeben können, ohne sie im Erweiterungskatalog öffentlich verfügbar zu machen. Diese Funktion schafft eine sichere Brücke zwischen Organisationen, sodass Sie den benutzerdefinierten Erweiterungs-Code der anderen nutzen und gleichzeitig den Datenschutz und die Kontrolle über Ihre proprietären Lösungen behalten können.

## Freigeben von Erweiterungspaketen für andere Organisationen

>[!NOTE]
>
>Erweiterungspakete müssen eine private oder öffentliche Version aufweisen, damit sie über „Verwendungsautorisierungen“ [!UICONTROL  werden ]. Versionen, die als Entwicklungsverfügbarkeit gekennzeichnet sind, können nicht freigegeben werden und werden nicht in der Autorisierungs-Dropdown-Liste angezeigt. Dies gilt auch dann, wenn bereits eine frühere Version (z. B. 1.0.0) freigegeben wurde. Neuere Versionen (z. B. 1.0.1) müssen mindestens als privat eingestuft werden, bevor sie von empfangenden Organisationen autorisiert oder installiert werden können.
>
>Alle Hinweise zur Freigabe privater Erweiterungspakete gelten auch, wenn Sie diese Pakete später veröffentlichen. Dieselben Überlegungen hinsichtlich Sichtbarkeit, Versionierung, Sicherheit, Kompatibilität, Support und Dokumentation bleiben unabhängig vom Verfügbarkeitsstatus des Pakets relevant.

Sowohl öffentliche als auch private Erweiterungspakete können über [!UICONTROL Verwendungsautorisierungen“ freigegeben werden] wobei für Erweiterungen in der Entwicklungsverfügbarkeit keine Berechtigungen erforderlich sind.

Unternehmen entwickeln häufig spezielle Erweiterungen, die auf ihre individuellen Geschäftsanforderungen zugeschnitten sind. Diese Erweiterungen können proprietäre Logik, benutzerdefinierte Integrationen oder vertrauliche Konfigurationen enthalten, die nicht öffentlich zugänglich gemacht werden sollten. Nutzungsautorisierungen lösen diese Herausforderung, indem sie Folgendes ermöglichen:

- **Selektive Freigabe**: Freigeben privater Erweiterungen nur für vertrauenswürdige Partnerorganisationen
- **Wahrung der**: Vertraulichen Erweiterungs-Code aus dem öffentlichen Katalog ausschließen
- **Partizipative Entwicklung**: Profitieren Sie von Ihren individuellen Lösungen durch vertrauenswürdige Partner.
- **Kontrollierter Zugriff**: Behalten Sie die volle Kontrolle darüber, wer auf Ihre privaten Erweiterungen zugreifen und sie verwenden kann

Der Freigabeprozess umfasst zwei Hauptbeteiligte:

1. **Freigabeorganisation**: Die Organisation, die im Besitz des privaten Erweiterungspakets ist und dieses freigibt
2. **Empfängerorganisation**: Die vertrauenswürdige Organisation, die Zugriff auf die freigegebene Erweiterung erhält

Wenn eine private Version freigegeben wird, erhält die empfangende Organisation Zugriff auf diese spezifische Version, wodurch eine direkte Verbindung zwischen den beiden Organisationen hergestellt wird. Wenn eine neuere Version später als privat eingestuft wird, steht sie auch der empfangenden Organisation zur Verfügung, ohne dass diese zusätzliche Schritte ausführen muss.

## Erstellen einer Autorisierung für die Verwendung von Erweiterungspaketen

Um eine Erweiterung freizugeben, navigieren Sie zur Datenerfassungs-Benutzeroberfläche und wählen **[!UICONTROL Tags]** in der linken Navigationsleiste aus. Wählen Sie hier eine vorhandene Eigenschaft aus oder erstellen Sie eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **[!UICONTROL auf]** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Nutzungsberechtigungen]** aus.

Hier sehen Sie eine Liste der vorhandenen freigegebenen Berechtigungen, die in zwei Kategorien unterteilt sind:

- **Für diese Organisation freigegeben**: Erweiterungen, die andere Organisationen für Sie freigegeben haben.
- **Für andere Organisationen freigegeben**: Erweiterungen, die Sie für andere Organisationen freigegeben haben.

Wählen Sie **[!UICONTROL Berechtigung hinzufügen]** aus.

![Die Registerkarte [!UICONTROL Nutzungsberechtigungen] mit einer Liste von Erweiterungen, die für diese Organisation freigegeben wurden, Hervorhebung [!UICONTROL Autorisierung hinzufügen]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>Sie müssen die **`Organization ID`** der Zielorganisation als Verantwortlichen der Organisation abrufen. Organisationen können nicht nach Namen durchsucht werden.

Wählen Sie **[!UICONTROL Erweiterung]** aus, die Sie aus Ihren verfügbaren Erweiterungen im Dropdown-Menü freigeben möchten. In der Liste werden Erweiterungen angezeigt, die Ihrem Unternehmen gehören, zusammen mit ihrem Verfügbarkeitsstatus. Erweiterungen, deren neueste Version die Verfügbarkeit **Entwicklung** aufweist, werden nicht in dieser Liste angezeigt.

Geben Sie als Nächstes die Kennung der empfangenden Organisation ein und wählen Sie dann **[!UICONTROL Speichern]**.

![Die Seite [!UICONTROL Verwendungsautorisierung des Erweiterungspakets erstellen] auf der eine ausgewählte Erweiterung und die eingegebene Adobe-Organisations-ID angezeigt werden, wobei [!UICONTROL  hervorgehoben ist]](../images/shared-extensions/save-authorization.png)

Sie kehren zur Registerkarte [!UICONTROL Nutzungsberechtigungen] zurück, auf der Sie die Erweiterung in Ihrer Liste **[!UICONTROL Für andere Organisationen freigegeben]** sehen. Der Status **„Genehmigung ausstehend**, bis die empfangende Organisation die Autorisierung genehmigt hat. Anschließend wird sie auf &quot;**&quot;**.

![Die Registerkarte [!UICONTROL Nutzungsberechtigungen] mit einer Liste der für andere Organisationen freigegebenen Erweiterungen, in der die neue Autorisierung hervorgehoben ist](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>Sie können Erweiterungen auch direkt über den **[!UICONTROL Erweiterungskatalog“ freigeben]** indem Sie auf der Erweiterungskarte das Menü (⋯) auswählen und dann im Menü die Option Freigeben auswählen.

Wenn eine Autorisierung aktiv ist, zeigt die freigegebene Erweiterung im Katalog ein ***Freigabe***-Badge an, das angibt, dass sie für andere Organisationen freigegeben wird.

![Die Registerkarte [!UICONTROL Katalog] mit der freigegebenen Erweiterung und dem Badge](../images/shared-extensions/sharing-badge.png)

## Freigegebene Erweiterungen autorisieren und verwalten

>[!NOTE]
>
>Als empfangende Organisation können Sie nur freigegebene Erweiterungen genehmigen oder ablehnen. Sie können die Autorisierungsdetails nicht verwalten oder ändern, da diese von der Freigabeorganisation gesteuert werden.

Um eine freigegebene Erweiterung für Ihr Unternehmen zu autorisieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche, wählen **[!UICONTROL Tags]** aus dem linken Navigationsbereich aus und wählen Sie die Eigenschaft aus. Wählen Sie anschließend **[!UICONTROL linken Navigationsbereich]** Erweiterungen“ und dann die Registerkarte **[!UICONTROL Nutzungsberechtigungen]** aus.

Eine Liste der freigegebenen Erweiterungen, einschließlich der Erweiterungen **Genehmigung ausstehend** finden Sie im Abschnitt **[!UICONTROL Freigegeben für diese Organisation]** . Wählen Sie die Erweiterung aus, die Sie genehmigen möchten, und wählen Sie dann **[!UICONTROL Genehmigen]**.

![Die Registerkarte [!UICONTROL Nutzungsberechtigungen] mit einer Liste von Erweiterungen, die für diese Organisation freigegeben wurden, mit der ausgewählten Erweiterung, die auf Genehmigung wartet, Hervorhebung [!UICONTROL Genehmigen]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>Sie können eine Anfrage auch auf der Registerkarte **[!UICONTROL Nutzungsberechtigungen]** ablehnen, wenn die freigegebene Erweiterung für Ihre Organisation nicht mehr erforderlich ist.

Wählen **[!UICONTROL OK]** im Dialogfeld **[!UICONTROL Verwendung für Autorisierung]** aus.

![Dialogfeld [!UICONTROL Autorisierungsverwendungen], Hervorhebung [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

Sie kehren zur Registerkarte [!UICONTROL Nutzungsberechtigungen“ zurück] auf der die Erweiterung angezeigt wird und nun den Status **Genehmigt** aufweist.

![Die Registerkarte [!UICONTROL Nutzungsberechtigungen] mit einer Liste der für diese Organisation freigegebenen Erweiterungen, wobei die Erweiterung mit dem Status Genehmigt hervorgehoben wird](../images/shared-extensions/approved-authorization.png)

Sobald die Autorisierung genehmigt wurde, ist die Erweiterung in Ihrem Katalog verfügbar und kann wie jede andere Erweiterung installiert und verwendet werden. Die freigegebene Erweiterung weist mit einem ***Empfangen*** -Badge darauf hin, dass es sich um eine Erweiterung handelt, die von einer anderen Organisation für Sie freigegeben wurde.

![Die Registerkarte [!UICONTROL Katalog] mit der freigegebenen Erweiterung mit dem Badge „Empfangen“](../images/shared-extensions/receiving-badge.png)

## Widerrufen von Berechtigungen

Als Eigentümerorganisation können Sie eine Autorisierung jederzeit löschen, unabhängig von ihrem aktuellen Status (Warten auf Genehmigung, Abgelehnt oder Genehmigt).

**Wenn Ihre Erweiterung nie veröffentlicht wurde:**
- Alle privaten Versionen, die die empfangende Organisation bereits installiert hat, werden weiterhin in der Liste der installierten Erweiterungen angezeigt.
- Wenn die empfangende Organisation Ihre Erweiterung nie installiert hat, wird sie an keiner Stelle mehr in der Benutzeroberfläche angezeigt.

**Wenn Ihre Erweiterung veröffentlicht wurde:**
- Alle privaten Versionen, die von der empfangenden Organisation installiert wurden, bleiben in der Liste der installierten Erweiterungen sichtbar.
- Wenn Ihre private Version nie installiert wurde, wird die neueste öffentliche Version weiterhin im Katalog angezeigt und kann installiert werden.
- Sie können bei Bedarf auch ein Downgrade von Ihrer privaten Version auf die neueste verfügbare öffentliche Version durchführen.

Wenn Sie eine Autorisierung widerrufen, behält die empfangende Organisation bestimmte Rechte zum Schutz ihrer vorhandenen Implementierungen bei:

- **Weitere Verwendung**: Die empfangende Organisation kann weiterhin eine private Version verwenden, die bereits installiert wurde, selbst wenn Sie den Zugriff widerrufen haben.
- **Build-Schutz**: Wenn die empfangende Organisation Ihre private Version 1.0.0 installiert hat und Sie später eine private Version 1.0.1 veröffentlichen, wird die neuere Version nicht angezeigt, aber die Erstellung mit Version 1.0.0 kann ohne Unterbrechung fortgesetzt werden.
- **Zukünftige Upgrades**: Wenn Sie Ihre Erweiterung später veröffentlichen (z. B. Version 2.0.0 öffentlich freigeben), kann die empfangende Organisation von ihrer privaten Version 1.0.0 direkt auf die neue öffentliche Version 2.0.0 aktualisieren.

>[!IMPORTANT]
>
>Durch das Widerrufen der Autorisierung werden bestehende Builds oder Implementierungen nicht beschädigt. Empfängerorganisationen behalten den Zugriff auf bereits installierte private Versionen, um die Business Continuity sicherzustellen.

## Nächste Schritte

In diesem Dokument wurde gezeigt, wie die Funktion „Freigegebene Erweiterung“ in Experience Platform verwendet wird. Informationen zur Entwicklung von Erweiterungen finden Sie im [Benutzerhandbuch zur Erweiterungsentwicklung](./getting-started.md).

Einen umfassenden Überblick über die Entwicklung von Erweiterungen in Experience Platform finden Sie in der [Übersichtsdokumentation](./overview.md).
