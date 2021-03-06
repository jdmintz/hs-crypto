---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# Fehlerbehebung
{: #troubleshooting}

Zu den allgemeinen Problemen bei der Verwendung von {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} kann beispielsweise die Angabe korrekter Header oder Berechtigungsnachweise bei der Interaktion mit der API gehören. In vielen Fällen können Sie diese Probleme beheben, indem Sie eine Reihe einfacher Schritte ausführen.
{: shortdesc}

## Beim Löschen einer initialisierten {{site.data.keyword.hscrypto}}-Instanz ist ein Fehler aufgetreten.

Beim Löschen einer initialisierten {{site.data.keyword.hscrypto}}-Instanz kann ein Fehler wie der folgende auftreten:

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

Sie haben die initialisierte {{site.data.keyword.hscrypto}}-Instanz vor dem Löschen der Instanz nicht bereinigt (genullt).
{: tsCauses}

Führen Sie vor dem Löschen der Instanz folgenden Befehl aus:
{: tsResolve}

```
ibmcloud tke cryptounit-zeroize
```
{: codeblock}

## Nicht berechtigtes Token nach Ausführung von Befehlen im Zusammenhang mit dem Plug-in "Trusted Key Entry"

Nach Ausführung eines `tke`-CLI-Befehls erhalten Sie möglicherweise eine Nachricht wie die folgende:

```
ibmcloud tke cryptounits
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

Das Token wurde nicht aktualisiert.
{: tsCauses}

Melden Sie sich mit dem Befehl `ibmcloud login` erneut bei {{site.data.keyword.cloud_notm}} an, um das Token zu aktualisieren.
{: tsResolve}

## Erhalt von `error CKR_IBM_WK_NOT_INITIALIZED` bei Verwendung der CLI oder API

Wenn Sie die CLI oder API verwenden, erhalten Sie möglicherweise eine Fehlernachricht ähnlich der folgenden:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

Nachdem Sie den Befehl `ibmcloud tke cryptounit-compare` ausgeführt haben, erhalten Sie keine Bestätigung `Valid` in CURRENT MASTER KEY REGISTER (aktuelles Masterschlüssel-Register).
{: tsCauses}

Stellen Sie sicher, dass der HSM-Masterschlüssel ordnungsgemäß festgelegt wurde.
{: tsResolve}

## Schlüssel können nicht erstellt oder gelöscht werden
{: #unable-to-create-keys}

Beim Zugriff auf die {{site.data.keyword.hscrypto}}-Benutzerschnittstelle werden die Optionen für das Hinzufügen oder Löschen von Schlüsseln nicht angezeigt.

Wählen Sie im {{site.data.keyword.cloud_notm}}-Dashboard Ihre Instanz des {{site.data.keyword.hscrypto}}-Service aus.
{: tsSymptoms}

Eine Liste mit Schlüsseln wird angezeigt, nicht jedoch die Optionen zum Hinzufügen oder Löschen von Schlüsseln.

Sie verfügen nicht über die korrekte Berechtigung für die Durchführung von {{site.data.keyword.hscrypto}}-Aktionen.
{: tsCauses}

Wenden Sie sich an den zuständigen Administrator und prüfen Sie, ob Ihnen die korrekte Rolle in der entsprechenden Ressourcengruppe oder Serviceinstanz zugewiesen ist. Weitere Informationen zu Rollen finden Sie in [Rollen und Berechtigungen](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Hilfe und Unterstützung anfordern
{: #getting-help}

Wenn bei der Verwendung von {{site.data.keyword.hscrypto}} Probleme auftreten oder Fragen entstehen, können Sie den Status von {{site.data.keyword.cloud_notm}} überprüfen, nach Informationen suchen oder Fragen in einem Forum stellen. Sie haben auch die Möglichkeit, ein Support-Ticket zu öffnen.
{: shortdesc}

Sie können überprüfen, ob {{site.data.keyword.cloud_notm}} verfügbar ist, indem Sie die [Statusseite![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/status?tags=platform,runtimes,services) aufrufen.

Sie können die Foren überprüfen, um festzustellen, ob bei anderen Benutzern dasselbe Problem aufgetreten ist. Wenn Sie in den Foren eine Frage stellen, versehen Sie Ihre Frage mit einem Tag, sodass sie von den {{site.data.keyword.cloud_notm}}-Entwicklungsteams gesehen wird.

- Bei technischen Fragen zu {{site.data.keyword.hscrypto}} posten Sie diese in [Stack Overflow ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://stackoverflow.com/){: new_window} und kennzeichnen Sie sie mit den Tags "ibm-cloud" und "hyperprotect-crypto".
- Antworten auf Fragen zum Service und Anweisungen für den Einstieg erhalten Sie über das Forum [IBM developerWorks dW Answers ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/answers/index.html){: new_window}. Schließen Sie die Tags "ibm-cloud" und "hyperprotect-crypto" ein.

Weitere Details zur Nutzung der Foren finden Sie unter [Hilfe anfordern ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}.

Weitere Informationen zum Öffnen eines {{site.data.keyword.IBM_notm}} Support-Tickets bzw. zu Supportebenen und zur Priorität von Tickets finden Sie in [Kontaktaufnahme mit dem Support![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}.
