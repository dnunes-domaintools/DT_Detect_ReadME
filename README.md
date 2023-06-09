DomainTools is an essential component in the security stack of mature enterprises and performance-driven security teams.
This integration was integrated and tested with version xx of DomainToolsIrisDetect

## Configure DomainTools Iris Detect on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for DomainTools Iris Detect.
3. Click **Add instance** to create and configure a new integration instance.

   | **Parameter** | **Description** | **Required** |
      | --- | --- | --- |
   | DomainTools API Username | DomainTools API Username | True |
   | DomainTools API Key | DomainTools API Key | True |
   | Enabled on New Domains | If selected, each pull will create a new incident every time the enrichment is run, with the new domains attached as indicators to the incident. Whois and DNS information is preserved in comments. | False |
   | Enabled on Changed Domains | If selected, each pull will create a new incident every time the enrichment is run, with the new domains attached as indicators to the incident. Whois and DNS information is preserved in comments. | False |
   | Enabled on Blocked Domains | If selected, each pull will create a new incident every time the enrichment is run, with the new domains attached as indicators to the incident. Whois and DNS information is preserved in comments. | False |
   | Risk score Ranges | List of risk score ranges to filter domains by | False |
   | Include Domain Data | Includes DNS and whois data in the response | False |
   | First fetch timestamp (&lt;number&gt; &lt;time unit&gt;, e.g., 10 minutes, 12 hours, 7 days) | First Fetch timestamp, Default is 3 days. The maximum time range is 30 days. | False |
   | Maximum number of incidents to fetch | Maximum Number of Incidents fetch limit. Maximum Default limit is 50. | False |
   | Trust any certificate (not secure) | Trust any certificate \(not secure\) | False |
   | Use system proxy settings | Use system proxy settings | False |
   | Fetch indicators |  | False |
   | Indicator Reputation | Indicators from this integration instance will be marked with this reputation. | False |
   | Source Reliability | Reliability of the source providing the intelligence data. | True |
   | Tags | Supports CSV values. | False |
   | Traffic Light Protocol Color | The Traffic Light Protocol \(TLP\) designation to apply to indicators fetched from the feed | False |
   | Bypass exclusion list | When selected, the exclusion list is ignored for indicators from this feed. This means that if an indicator from this feed is on the exclusion list, the indicator might still be added to the system. | False |
   | Incremental Feed | Incremental feeds pull only new or modified indicators that have been sent from the integration. As the determination if the indicator is new or modified happens on the 3rd-party vendor's side, and only indicators that are new or modified are sent to Cortex XSOAR, all indicators coming from these feeds are labeled new or modified. | False |
   | Incident type |  | False |
   | Fetch incidents |  | False |

4. Click **Test** to validate the URLs, token, and connection.

## Commands

You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.

### domaintools-iris-detect-escalate-domains

***
Escalate a given domain to Google Phishing Protection, leveraging the protections Google puts into Chrome to protect
billions of users. Mozilla Firefox and Apple's Safari browsers are also known to pick up these blocking rules.

#### Base Command

`domaintools-iris-detect-escalate-domains`

#### Input

| **Argument Name**    | **Description**                             | **Required** |
|----------------------|---------------------------------------------|--------------|
| watchlist_domain_ids | List of Iris Detect domain IDs to escalate. | Required     | 

#### Context Output

There is no context output for this command.

#### Command example

```!domaintools-iris-detect-escalate-domains watchlist_domain_ids="jaMzYv2plE"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Indicators": {
      "dt_created_by": "nvojjala@loginsoft.com",
      "dt_created_date_result": "2023-04-11T05:20:49.104498+00:00",
      "dt_escalation_type": "google_safe",
      "dt_id": "5ebALaKgQW",
      "dt_updated_date": "2023-04-11T05:20:49.104498+00:00",
      "dt_watchlist_domain_id": "jaMzYv2plE"
    }
  }
}
```

#### Human Readable Output

> ### Escalated Domains
>|dt_created_by|dt_created_date_result|dt_escalation_type|dt_id|dt_updated_date|dt_watchlist_domain_id|
>|---|---|---|---|---|---|
>| nvojjala@loginsoft.com | 2023-04-11T05:20:49.104498+00:00 | google_safe | 5ebALaKgQW | 2023-04-11T05:20:49.104498+00:00 | jaMzYv2plE |

### domaintools-iris-detect-blocklist-domains

***
Mark a given domain as blocked, which allows a script against the Iris Detect API to pass these domains on to other
teams or security controls within your organization to block them in email, web, or other filtering controls.

#### Base Command

`domaintools-iris-detect-blocklist-domains`

#### Input

| **Argument Name**    | **Description**                          | **Required** |
|----------------------|------------------------------------------|--------------|
| watchlist_domain_ids | List of Iris Detect domain IDs to block. | Required     | 

#### Context Output

There is no context output for this command.

#### Command example

```!domaintools-iris-detect-blocklist-domains watchlist_domain_ids="vEwp2mQxYP"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Indicators": {
      "dt_created_by": "nvojjala@loginsoft.com",
      "dt_created_date_result": "2023-04-11T05:20:43.339439+00:00",
      "dt_escalation_type": "blocked",
      "dt_id": "47E4ZwAboq",
      "dt_updated_date": "2023-04-11T05:20:43.339439+00:00",
      "dt_watchlist_domain_id": "vEwp2mQxYP"
    }
  }
}
```

#### Human Readable Output

> ### Blocked Domains
>|dt_created_by|dt_created_date_result|dt_escalation_type|dt_id|dt_updated_date|dt_watchlist_domain_id|
>|---|---|---|---|---|---|
>| nvojjala@loginsoft.com | 2023-04-11T05:20:43.339439+00:00 | blocked | 47E4ZwAboq | 2023-04-11T05:20:43.339439+00:00 | vEwp2mQxYP |

### domaintools-iris-detect-watch-domains

***
Mark a given domain as watched, which will trigger more frequent scanning by DomainTools automation. Changes to watched
domains can trigger incidents if enabled, or manually queried via the domaintools-iris-detect-get-watched-domains
command.

#### Base Command

`domaintools-iris-detect-watch-domains`

#### Input

| **Argument Name**    | **Description**                              | **Required** |
|----------------------|----------------------------------------------|--------------|
| watchlist_domain_ids | List of Iris Detect domain IDs to watchlist. | Required     | 

#### Context Output

There is no context output for this command.

#### Command example

```!domaintools-iris-detect-watch-domains watchlist_domain_ids="OWxlNO23VW"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Indicators": {
      "dt_changed_date": "2023-04-09T09:50:36.000000+00:00",
      "dt_discovered_date": "2023-04-09T09:49:49.447000+00:00",
      "dt_domain": "amazonpayinsurance.ie",
      "dt_domain_id": "OWxlNO23VW",
      "dt_state": "watched"
    }
  }
}
```

#### Human Readable Output

> ### Watched Domains
>|dt_changed_date|dt_discovered_date|dt_domain|dt_domain_id|dt_state|
>|---|---|---|---|---|
>| 2023-04-09T09:50:36.000000+00:00 | 2023-04-09T09:49:49.447000+00:00 | amazonpayinsurance.ie | OWxlNO23VW | watched |

### domaintools-iris-detect-ignore-domains

***
Ignore a given domain, removing it from new and block lists, if applicable.

#### Base Command

`domaintools-iris-detect-ignore-domains`

#### Input

| **Argument Name**    | **Description**                           | **Required** |
|----------------------|-------------------------------------------|--------------|
| watchlist_domain_ids | List of Iris Detect domain IDs to ignore. | Required     | 

#### Context Output

There is no context output for this command.

#### Command example

```!domaintools-iris-detect-ignore-domains watchlist_domain_ids="OWxlNO23VW"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Indicators": {
      "dt_changed_date": "2023-04-09T09:50:36.000000+00:00",
      "dt_discovered_date": "2023-04-09T09:49:49.447000+00:00",
      "dt_domain": "amazonpayinsurance.ie",
      "dt_domain_id": "OWxlNO23VW",
      "dt_state": "ignored"
    }
  }
}
```

#### Human Readable Output

> ### Ignored Domains
>|dt_changed_date|dt_discovered_date|dt_domain|dt_domain_id|dt_state|
>|---|---|---|---|---|
>| 2023-04-09T09:50:36.000000+00:00 | 2023-04-09T09:49:49.447000+00:00 | amazonpayinsurance.ie | OWxlNO23VW | ignored |

### domaintools-iris-detect-get-monitors-list

***
This command allows users to retrieve the list of monitored terms and respective IDs associated with your organization's
Iris Detect account. New terms can only be set up and configured directly within the Iris Detect
UI (https://iris.domaintools.com/detect/)

#### Base Command

`domaintools-iris-detect-get-monitors-list`

#### Input

| **Argument Name**     | **Description**                                                                                                                                                | **Required** |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| datetime_counts_since | ISO 8601 datetime format: default None. Conditionally required if the include_counts parameter is set to True. for example 2022-05-18T12:19:51.685496.         | Required     | 
| include_counts        | Includes counts for each monitor for new, watched, changed, and escalated domains. Possible values are: True, False.                                           | Optional     | 
| sort                  | Sort order for monitor list. Valid values are an ordered list of the following: ["term", "created_date", "domain_counts_changed", "domain_counts_discovered"]. | Optional     | 
| order                 | Sort order "asc" or "desc".                                                                                                                                    | Optional     | 

#### Context Output

| **Path**                                                 | **Type** | **Description**             |
|----------------------------------------------------------|----------|-----------------------------|
| DomainToolsIrisDetect.Monitor.term                       | String   | Domain Name.                | 
| DomainToolsIrisDetect.Monitor.match_substring_variations | Boolean  | Substring Variations.       | 
| DomainToolsIrisDetect.Monitor.nameserver_exclusions      | Unknown  | Nameserver Exclusions list. | 
| DomainToolsIrisDetect.Monitor.text_exclusions            | unknown  | Text Exclusions list.       | 
| DomainToolsIrisDetect.Monitor.id                         | String   | Monitor Id.                 | 
| DomainToolsIrisDetect.Monitor.created_date               | String   | Creation Date.              | 
| DomainToolsIrisDetect.Monitor.updated_date               | String   | Last Updated Date.          | 
| DomainToolsIrisDetect.Monitor.state                      | String   | Monitor Domain State.       | 
| DomainToolsIrisDetect.Monitor.status                     | String   | Monitor Domain Status.      | 
| DomainToolsIrisDetect.Monitor.created_by                 | String   | Monitor Created By.         | 

#### Command example

```!domaintools-iris-detect-get-monitors-list datetime_counts_since="2022-01-01"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Monitor": [
      {
        "created_by": "nvojjala@loginsoft.com",
        "created_date": "2022-09-20T06:01:56.760955+00:00",
        "id": "QEMba8wmxo",
        "match_substring_variations": false,
        "nameserver_exclusions": [],
        "state": "active",
        "status": "completed",
        "term": "aliexpress",
        "text_exclusions": [],
        "updated_date": "2022-09-20T06:02:33.358799+00:00"
      },
      {
        "created_by": "nvojjala@loginsoft.com",
        "created_date": "2022-09-16T22:29:20.567614+00:00",
        "id": "rA7bn46jQ3",
        "match_substring_variations": false,
        "nameserver_exclusions": [],
        "state": "active",
        "status": "completed",
        "term": "amazon",
        "text_exclusions": [],
        "updated_date": "2022-09-16T22:30:16.212269+00:00"
      },
      {
        "created_by": "nvojjala@loginsoft.com",
        "created_date": "2022-09-20T05:35:21.203482+00:00",
        "id": "YNrbr6Gbkx",
        "match_substring_variations": false,
        "nameserver_exclusions": [],
        "state": "active",
        "status": "completed",
        "term": "loginsoft",
        "text_exclusions": [],
        "updated_date": "2022-09-20T05:35:28.630194+00:00"
      }
    ]
  }
}
```

#### Human Readable Output

> ### Monitor List
>|dt_created_by|dt_created_date|dt_match_substring_variations|dt_monitor_id|dt_nameserver_exclusions|dt_state|dt_status|dt_term|dt_text_exclusions|dt_updated_date|
>|---|---|---|---|---|---|---|---|---|---|
>| nvojjala@loginsoft.com | 2022-09-20T06:01:56.760955+00:00 | false | QEMba8wmxo |  | active | completed | aliexpress |  | 2022-09-20T06:02:33.358799+00:00 |
>| nvojjala@loginsoft.com | 2022-09-16T22:29:20.567614+00:00 | false | rA7bn46jQ3 |  | active | completed | amazon |  | 2022-09-16T22:30:16.212269+00:00 |
>| nvojjala@loginsoft.com | 2022-09-20T05:35:21.203482+00:00 | false | YNrbr6Gbkx |  | active | completed | loginsoft |  | 2022-09-20T05:35:28.630194+00:00 |

### domaintools-iris-detect-get-new-domains

***
Manually retrieve new domains matching all of your monitored terms, or a specific term specified by a "monitor_id" that
can be retrieved using the domaintools-iris-detect-get-monitors-list command. The number of domains returned is limited
to 50 if including DNS and whois details, or 500 otherwise. Use the offset parameter for pagination.

#### Base Command

`domaintools-iris-detect-get-new-domains`

#### Input

| **Argument Name**   | **Description**                                                                                                                   | **Required** |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|--------------|
| discovered_since    | Filter domains by when they were discovered. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.       | Optional     | 
| monitor_id          | Monitor ID from monitors response. Only used when requesting domains for a specific monitor.                                      | Optional     | 
| tlds                | List of TLDs to filter domains by. Possible values are: Filter domains by if they have an MX record in DNS..                      | Optional     | 
| mx_exists           | Filter domains by if they have an MX record in DNS. Possible values are: True, False.                                             | Optional     | 
| risk_score_ranges   | List of risk score ranges to filter domains by. Valid values are: ["0-0", "1-39", "40-69", "70-99", "100-100"].                   | Optional     | 
| search              | A "contains" search for any portion of a domain name.                                                                             | Optional     | 
| sort                | Sort order for domain list. Valid values are an ordered list of the following: ["discovered_date", "changed_date", "risk_score"]. | Optional     | 
| include_domain_data | Includes DNS and whois data in the response. Possible values are: True, False.                                                    | Optional     | 
| preview             | Preview mode used for testing. If set to True, only the first 10 results are returned but not limited by hourly restrictions.     | Optional     | 
| order               | Sort order "asc" or "desc".                                                                                                       | Optional     | 
| limit               | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                | Optional     | 
| offset              | Default 0. Offset for pagination.                                                                                                 | Optional     | 

#### Context Output

| **Path**                                                                | **Type** | **Description**                       |
|-------------------------------------------------------------------------|----------|---------------------------------------|
| DomainToolsIrisDetect.New.state                                         | String   | State of the Domain.                  | 
| DomainToolsIrisDetect.New.domain                                        | String   | Domain Name.                          | 
| DomainToolsIrisDetect.New.status                                        | String   | Status of the Domain.                 | 
| DomainToolsIrisDetect.New.discovered_date                               | String   | Creation Date.                        | 
| DomainToolsIrisDetect.New.changed_date                                  | String   | Last Updated Date.                    | 
| DomainToolsIrisDetect.New.risk_score                                    | String   | Risk Score for the Domain.            | 
| DomainToolsIrisDetect.New.risk_score_status                             | Number   | Risk Score Status for the Domain.     | 
| DomainToolsIrisDetect.New.risk_score_components.proximity               | Number   | Proximity Score for the Domain.       | 
| DomainToolsIrisDetect.New.risk_score_components.threat_profile.phishing | Number   | Phishing Score for the Domain.        | 
| DomainToolsIrisDetect.New.risk_score_components.threat_profile.malware  | Number   | Malware Score for the Domain.         | 
| DomainToolsIrisDetect.New.risk_score_components.threat_profile.spam     | Number   | Spam Score for the Domain.            | 
| DomainToolsIrisDetect.New.risk_score_components.threat_profile.evidence | unknown  | Evidence for the Domain.              | 
| DomainToolsIrisDetect.New.mx_exists                                     | Boolean  | MX Exists for the Domain.             | 
| DomainToolsIrisDetect.New.tld                                           | String   | Domain TLD.                           | 
| DomainToolsIrisDetect.New.id                                            | String   | Domain ID.                            | 
| DomainToolsIrisDetect.New.escalations.escalation_type                   | String   | Escalation Type for the Domain.       | 
| DomainToolsIrisDetect.New.escalations.id                                | String   | Escalation ID for the Domain.         | 
| DomainToolsIrisDetect.New.escalations.created                           | String   | Escalation Created Date.              | 
| DomainToolsIrisDetect.New.escalations.created_by                        | String   | Escalation Created By.                | 
| DomainToolsIrisDetect.New.monitor_ids                                   | String   | Domain Monitor Id.                    | 
| DomainToolsIrisDetect.New.assigned_by                                   | String   | Escalation Assigned By.               | 
| DomainToolsIrisDetect.New.assigned_date                                 | String   | Escalation Assigned Date.             | 
| DomainToolsIrisDetect.New.registrant_contact_email                      | String   | Registrant Email.                     | 
| DomainToolsIrisDetect.New.name_server                                   | String   | Associated Nameserver for the Domain. | 
| DomainToolsIrisDetect.New.registrar                                     | String   | Registrant Name.                      | 
| DomainToolsIrisDetect.New.create_date                                   | String   | Created Date.                         | 
| DomainToolsIrisDetect.New.ip.country_code                               | String   | Country code for the ip.              | 
| DomainToolsIrisDetect.New.ip.ip                                         | String   | Associated ip for the Domain.         | 
| DomainToolsIrisDetect.New.ip.isp                                        | String   | Associated isp for the Domain.        | 

#### Command example

```!domaintools-iris-detect-get-new-domains limit="2"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "New": [
      {
        "changed_date": "2023-04-11T05:16:56.483000+00:00",
        "discovered_date": "2023-04-11T05:16:56.483000+00:00",
        "domain": "amazontask.shop",
        "escalations": [],
        "id": "KW3ykVGZrE",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": null,
        "risk_score_status": null,
        "state": "new",
        "status": "active",
        "tld": "shop"
      },
      {
        "changed_date": "2023-04-11T05:15:42.000000+00:00",
        "discovered_date": "2023-04-11T05:12:22.081000+00:00",
        "domain": "rambojombojo998amazon.com",
        "escalations": [],
        "id": "gWlYVZxmja",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": 79,
        "risk_score_components": {
          "proximity": 4,
          "threat_profile": {
            "phishing": 79
          }
        },
        "risk_score_status": "provisional",
        "state": "new",
        "status": "active",
        "tld": "com"
      }
    ]
  }
}
```

#### Human Readable Output

> ### New Domains
>|dt_changed_date|dt_create_date|dt_discovered_date|dt_domain|dt_domain_id|dt_escalations|dt_monitor_ids|dt_mx_exists|dt_proximity_score|dt_registrant_contact_email|dt_registrar|dt_risk_score|dt_risk_status|dt_state|dt_status|dt_threat_profile_evidence|dt_threat_profile_malware|dt_threat_profile_phishing|dt_threat_profile_spam|dt_tld|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 2023-04-11T05:16:56.483000+00:00 |  | 2023-04-11T05:16:56.483000+00:00 | amazontask.shop | KW3ykVGZrE |  | rA7bn46jQ3 | false |  |  |  |  |  | new | active |  |  |  |  | shop |
>| 2023-04-11T05:15:42.000000+00:00 |  | 2023-04-11T05:12:22.081000+00:00 | rambojombojo998amazon.com | gWlYVZxmja |  | rA7bn46jQ3 | false | 4 |  |  | 79 | provisional | new | active |  |  | 79 |  | com |

### domaintools-iris-detect-get-watched-domains

***
Manually retrieve changes to domains that have been marked as "watched" by users of your organization, matching all of
your monitored terms, or a specific term specified by a "monitor_id" that can be retrieved using the
domaintools-iris-detect-get-monitors-list command. The number of domains returned is limited to 50 if including DNS and
whois details, or 500 otherwise. Use the offset parameter for pagination.

#### Base Command

`domaintools-iris-detect-get-watched-domains`

#### Input

| **Argument Name**   | **Description**                                                                                                                                                 | **Required** |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| escalation_types    | escalation_types: List[str]: default None. List of escalation types to filter domains by. Valid values are: ["blocked", "google_safe"].                         | Optional     | 
| monitor_id          | Monitor ID from monitors response. Only used when requesting domains for a specific monitor.                                                                    | Optional     | 
| tlds                | List of TLDs to filter domains by.                                                                                                                              | Optional     | 
| mx_exists           | Filter domains by if they have an MX record in DNS. Possible values are: True, False.                                                                           | Optional     | 
| changed_since       | Filter domains by when they were last changed. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                   | Optional     | 
| search              | A "contains" search for any portion of a domain name.                                                                                                           | Optional     | 
| sort                | Sort order for domain list. Valid values are an ordered list of the following: ["discovered_date", "changed_date", "risk_score"].                               | Optional     | 
| include_domain_data | Includes DNS and whois data in the response. Possible values are: True, False.                                                                                  | Optional     | 
| preview             | Preview mode used for testing. If set to True, only the first 10 results are returned but not limited by hourly restrictions. Possible values are: True, False. | Optional     | 
| escalated_since     | Filter domains by when they were last escalated. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                 | Optional     | 
| order               | Sort order "asc" or "desc".                                                                                                                                     | Optional     | 
| risk_score_ranges   | List of risk score ranges to filter domains by. Valid values are: ["0-0", "1-39", "40-69", "70-99", "100-100"].                                                 | Optional     | 
| limit               | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                                              | Optional     | 
| offset              | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                                              | Optional     | 

#### Context Output

| **Path**                                                                    | **Type** | **Description**                       |
|-----------------------------------------------------------------------------|----------|---------------------------------------|
| DomainToolsIrisDetect.Watched.state                                         | String   | State of the Domain.                  | 
| DomainToolsIrisDetect.Watched.domain                                        | String   | Domain Name.                          | 
| DomainToolsIrisDetect.Watched.status                                        | String   | Status of the Domain.                 | 
| DomainToolsIrisDetect.Watched.discovered_date                               | String   | Creation Date.                        | 
| DomainToolsIrisDetect.Watched.changed_date                                  | String   | Last Updated Date.                    | 
| DomainToolsIrisDetect.Watched.risk_score                                    | String   | Risk Score for the Domain.            | 
| DomainToolsIrisDetect.Watched.risk_score_status                             | Number   | Risk Score Status for the Domain.     | 
| DomainToolsIrisDetect.Watched.risk_score_components.proximity               | Number   | Proximity Score for the Domain.       | 
| DomainToolsIrisDetect.Watched.risk_score_components.threat_profile.phishing | Number   | Phishing Score for the Domain.        | 
| DomainToolsIrisDetect.Watched.risk_score_components.threat_profile.malware  | Number   | Malware Score for the Domain.         | 
| DomainToolsIrisDetect.Watched.risk_score_components.threat_profile.spam     | Number   | Spam Score for the Domain.            | 
| DomainToolsIrisDetect.Watched.risk_score_components.threat_profile.evidence | Unknown  | Evidence for the Domain.              | 
| DomainToolsIrisDetect.Watched.mx_exists                                     | Boolean  | MX Exists for the Domain.             | 
| DomainToolsIrisDetect.Watched.tld                                           | String   | Domain TLD.                           | 
| DomainToolsIrisDetect.Watched.id                                            | String   | Domain ID.                            | 
| DomainToolsIrisDetect.Watched.escalations.escalation_type                   | String   | Escalation Type for the Domain.       | 
| DomainToolsIrisDetect.Watched.escalations.id                                | String   | Escalation ID for the Domain.         | 
| DomainToolsIrisDetect.Watched.escalations.created                           | String   | Escalation Created Date.              | 
| DomainToolsIrisDetect.Watched.escalations.created_by                        | String   | Escalation Created By.                | 
| DomainToolsIrisDetect.Watched.monitor_ids                                   | String   | Domain Monitor Id.                    | 
| DomainToolsIrisDetect.Watched.assigned_by                                   | String   | Escalation Assigned By.               | 
| DomainToolsIrisDetect.Watched.assigned_date                                 | String   | Escalation Assigned Date.             | 
| DomainToolsIrisDetect.Watched.registrant_contact_email                      | String   | Registrant Email.                     | 
| DomainToolsIrisDetect.Watched.name_server                                   | String   | Associated Nameserver for the Domain. | 
| DomainToolsIrisDetect.Watched.registrar                                     | String   | Registrant Name.                      | 
| DomainToolsIrisDetect.Watched.create_date                                   | String   | Created Date.                         | 
| DomainToolsIrisDetect.Watched.ip.country_code                               | String   | Country code for the ip.              | 
| DomainToolsIrisDetect.Watched.ip.ip                                         | String   | Associated ip for the Domain.         | 
| DomainToolsIrisDetect.Watched.ip.isp                                        | String   | Associated isp for the Domain.        | 

#### Command example

```!domaintools-iris-detect-get-watched-domains limit="2"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Watched": [
      {
        "assigned_by": "nvojjala@loginsoft.com",
        "assigned_date": "2023-04-11T04:46:39.000000+00:00",
        "changed_date": "2023-04-10T07:52:11.000000+00:00",
        "discovered_date": "2023-04-10T07:45:31.478000+00:00",
        "domain": "amazonmetaworld.net.tr",
        "escalations": [
          {
            "created": "2023-04-11T04:46:39.181378+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "google_safe",
            "id": "43gB2Pwg6m"
          }
        ],
        "id": "8Wq8Qj9X7P",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": 8,
        "risk_score_components": {
          "proximity": 5,
          "threat_profile": {
            "evidence": [],
            "malware": 1,
            "phishing": 6,
            "spam": 8
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "net.tr"
      },
      {
        "changed_date": "2023-04-10T05:58:01.000000+00:00",
        "discovered_date": "2023-04-10T04:52:28.545000+00:00",
        "domain": "alixpress.co",
        "escalations": [
          {
            "created": "2023-04-10T14:33:11.342255+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "blocked",
            "id": "nzgWDr3b9Y"
          }
        ],
        "id": "gaeMyYl1Va",
        "monitor_ids": [
          "QEMba8wmxo"
        ],
        "mx_exists": true,
        "risk_score": 21,
        "risk_score_components": {
          "proximity": 21,
          "threat_profile": {
            "evidence": [],
            "malware": 20,
            "phishing": 15,
            "spam": 17
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "co"
      }
    ]
  }
}
```

#### Human Readable Output

> ### Watched Domains
>|dt_changed_date|dt_create_date|dt_discovered_date|dt_domain|dt_domain_id|dt_escalations|dt_monitor_ids|dt_mx_exists|dt_proximity_score|dt_registrant_contact_email|dt_registrar|dt_risk_score|dt_risk_status|dt_state|dt_status|dt_threat_profile_evidence|dt_threat_profile_malware|dt_threat_profile_phishing|dt_threat_profile_spam|dt_tld|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 2023-04-10T07:52:11.000000+00:00 |  | 2023-04-10T07:45:31.478000+00:00 | amazonmetaworld.net.tr | 8Wq8Qj9X7P | {'escalation_type': 'google_safe', 'id': '43gB2Pwg6m', 'created': '2023-04-11T04:46:39.181378+00:00', 'created_by': 'nvojjala@loginsoft.com'} | rA7bn46jQ3 | false | 5 |  |  | 8 | full | watched | active |  | 1 | 6 | 8 | net.tr |
>| 2023-04-10T05:58:01.000000+00:00 |  | 2023-04-10T04:52:28.545000+00:00 | alixpress.co | gaeMyYl1Va | {'escalation_type': 'blocked', 'id': 'nzgWDr3b9Y', 'created': '2023-04-10T14:33:11.342255+00:00', 'created_by': 'nvojjala@loginsoft.com'} | QEMba8wmxo | true | 21 |  |  | 21 | full | watched | active |  | 20 | 15 | 17 | co |

### domaintools-iris-detect-get-ignored-domains

***
Manually retrieve domains that your organization has marked as ignored, matching all of your monitored terms, or a
specific term specified by a "monitor_id" that can be retrieved using the domaintools-iris-detect-get-monitors-list
command. This is most useful in cases when a domain might have been mistakenly ignored. The number of domains returned
is limited to 50 if including DNS and whois details, or 500 otherwise. Use the offset parameter for pagination.

#### Base Command

`domaintools-iris-detect-get-ignored-domains`

#### Input

| **Argument Name**   | **Description**                                                                                                                                                 | **Required** |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| risk_score_ranges   | List of risk score ranges to filter domains by. Valid values are: ["0-0", "1-39", "40-69", "70-99", "100-100"].                                                 | Optional     | 
| monitor_id          | Monitor ID from monitors response. Only used when requesting domains for a specific monitor.                                                                    | Optional     | 
| tlds                | List of TLDs to filter domains by.                                                                                                                              | Optional     | 
| mx_exists           | Filter domains by if they have an MX record in DNS. Possible values are: True, False.                                                                           | Optional     | 
| changed_since       | Filter domains by when they were last changed. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                   | Optional     | 
| escalated_since     | Filter domains by when they were last escalated. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                 | Optional     | 
| search              | A "contains" search for any portion of a domain name.                                                                                                           | Optional     | 
| sort                | Sort order for domain list. Valid values are an ordered list of the following: ["discovered_date", "changed_date", "risk_score"].                               | Optional     | 
| include_domain_data | Includes DNS and whois data in the response. Possible values are: True, False.                                                                                  | Optional     | 
| preview             | Preview mode used for testing. If set to True, only the first 10 results are returned but not limited by hourly restrictions. Possible values are: True, False. | Optional     | 
| order               | Sort order "asc" or "desc".                                                                                                                                     | Optional     | 
| limit               | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                                              | Optional     | 
| offset              | Default 0. Offset for pagination.                                                                                                                               | Optional     | 

#### Context Output

| **Path**                                                                    | **Type** | **Description**                       |
|-----------------------------------------------------------------------------|----------|---------------------------------------|
| DomainToolsIrisDetect.Ignored.state                                         | String   | State of the Domain.                  | 
| DomainToolsIrisDetect.Ignored.domain                                        | String   | Domain Name.                          | 
| DomainToolsIrisDetect.Ignored.status                                        | String   | Status of the Domain.                 | 
| DomainToolsIrisDetect.Ignored.discovered_date                               | String   | Creation Date.                        | 
| DomainToolsIrisDetect.Ignored.changed_date                                  | String   | Last Updated Date.                    | 
| DomainToolsIrisDetect.Ignored.risk_score                                    | String   | Risk Score for the Domain.            | 
| DomainToolsIrisDetect.Ignored.risk_score_status                             | Number   | Risk Score Status for the Domain.     | 
| DomainToolsIrisDetect.Ignored.risk_score_components.proximity               | Number   | Proximity Score for the Domain.       | 
| DomainToolsIrisDetect.Ignored.risk_score_components.threat_profile.phishing | Number   | Phishing Score for the Domain.        | 
| DomainToolsIrisDetect.Ignored.risk_score_components.threat_profile.malware  | Number   | Malware Score for the Domain.         | 
| DomainToolsIrisDetect.Ignored.risk_score_components.threat_profile.spam     | Number   | Spam Score for the Domain.            | 
| DomainToolsIrisDetect.Ignored.risk_score_components.threat_profile.evidence | unknown  | Evidence for the Domain.              | 
| DomainToolsIrisDetect.Ignored.mx_exists                                     | Boolean  | MX Exists for the Domain.             | 
| DomainToolsIrisDetect.Ignored.tld                                           | String   | Domain TLD.                           | 
| DomainToolsIrisDetect.Ignored.id                                            | String   | Domain ID.                            | 
| DomainToolsIrisDetect.Ignored.escalations.escalation_type                   | String   | Escalation Type for the Domain.       | 
| DomainToolsIrisDetect.Ignored.escalations.id                                | String   | Escalation ID for the Domain.         | 
| DomainToolsIrisDetect.Ignored.escalations.created                           | String   | Escalation Created Date.              | 
| DomainToolsIrisDetect.Ignored.escalations.created_by                        | String   | Escalation Created By.                | 
| DomainToolsIrisDetect.Ignored.monitor_ids                                   | String   | Domain Monitor Id.                    | 
| DomainToolsIrisDetect.Ignored.assigned_by                                   | String   | Escalation Assigned By.               | 
| DomainToolsIrisDetect.Ignored.assigned_date                                 | String   | Escalation Assigned Date.             | 
| DomainToolsIrisDetect.Ignored.registrant_contact_email                      | String   | Registrant Email.                     | 
| DomainToolsIrisDetect.Ignored.name_server                                   | String   | Associated Nameserver for the Domain. | 
| DomainToolsIrisDetect.Ignored.registrar                                     | String   | Registrant Name.                      | 
| DomainToolsIrisDetect.Ignored.create_date                                   | String   | Created Date.                         | 
| DomainToolsIrisDetect.Ignored.ip.country_code                               | String   | Country code for the ip.              | 
| DomainToolsIrisDetect.Ignored.ip.ip                                         | String   | Associated ip for the Domain.         | 
| DomainToolsIrisDetect.Ignored.ip.isp                                        | String   | Associated isp for the Domain.        | 

#### Command example

```!domaintools-iris-detect-get-ignored-domains limit="2"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Ignored": [
      {
        "assigned_by": "nvojjala@loginsoft.com",
        "assigned_date": "2023-03-27T04:45:19.000000+00:00",
        "changed_date": "2023-03-30T09:07:59.000000+00:00",
        "discovered_date": "2023-03-21T13:57:47.094000+00:00",
        "domain": "amazonn.shop",
        "escalations": [
          {
            "created": "2023-03-21T17:33:51.787271+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "blocked",
            "id": "VrxaQQ2xnK"
          },
          {
            "created": "2023-03-21T17:35:10.150279+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "google_safe",
            "id": "kzbwQQ2Ey2"
          }
        ],
        "id": "VE87zKvOXa",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": true,
        "risk_score": 100,
        "risk_score_components": {
          "proximity": 100,
          "threat_profile": {
            "evidence": [
              "registrant",
              "domain name",
              "name server"
            ],
            "malware": 98,
            "phishing": 99,
            "spam": 82
          }
        },
        "risk_score_status": "full",
        "state": "ignored",
        "status": "active",
        "tld": "shop"
      },
      {
        "changed_date": "2023-03-25T08:04:15.000000+00:00",
        "discovered_date": "2023-02-08T10:32:18.665000+00:00",
        "domain": "awswalletamazon.com",
        "escalations": [],
        "id": "ya6dKwrRZP",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": true,
        "risk_score": 100,
        "risk_score_components": {
          "proximity": 100,
          "threat_profile": {
            "evidence": [
              "domain name",
              "registrar",
              "name server"
            ],
            "malware": 19,
            "phishing": 95,
            "spam": 43
          }
        },
        "risk_score_status": "full",
        "state": "ignored",
        "status": "active",
        "tld": "com"
      }
    ]
  }
}
```

#### Human Readable Output

> ### Ignored Domains
>|dt_changed_date|dt_create_date|dt_discovered_date|dt_domain|dt_domain_id|dt_escalations|dt_monitor_ids|dt_mx_exists|dt_proximity_score|dt_registrant_contact_email|dt_registrar|dt_risk_score|dt_risk_status|dt_state|dt_status|dt_threat_profile_evidence|dt_threat_profile_malware|dt_threat_profile_phishing|dt_threat_profile_spam|dt_tld|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 2023-03-30T09:07:59.000000+00:00 |  | 2023-03-21T13:57:47.094000+00:00 | amazonn.shop | VE87zKvOXa | {'escalation_type': 'blocked', 'id': 'VrxaQQ2xnK', 'created': '2023-03-21T17:33:51.787271+00:00', 'created_by': 'nvojjala@loginsoft.com'},<br/>{'escalation_type': 'google_safe', 'id': 'kzbwQQ2Ey2', 'created': '2023-03-21T17:35:10.150279+00:00', 'created_by': 'nvojjala@loginsoft.com'} | rA7bn46jQ3 | true | 100 |  |  | 100 | full | ignored | active | registrant,<br/>domain name,<br/>name server | 98 | 99 | 82 | shop |
>| 2023-03-25T08:04:15.000000+00:00 |  | 2023-02-08T10:32:18.665000+00:00 | awswalletamazon.com | ya6dKwrRZP |  | rA7bn46jQ3 | true | 100 |  |  | 100 | full | ignored | active | domain name,<br/>registrar,<br/>name server | 19 | 95 | 43 | com |

### domaintools-iris-detect-get-escalated-domains

***
Manually retrieve domains that your organization has escalated to Google Phishing Protection, matching all of your
monitored terms, or a specific term specified by a "monitor_id" that can be retrieved using the
domaintools-iris-detect-get-monitors-list command. The number of domains returned is limited to 50 if including DNS and
whois details, or 500 otherwise. Use the offset parameter for pagination.

#### Base Command

`domaintools-iris-detect-get-escalated-domains`

#### Input

| **Argument Name**   | **Description**                                                                                                                                                 | **Required** |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| risk_score_ranges   | List of risk score ranges to filter domains by. Valid values are: ["0-0", "1-39", "40-69", "70-99", "100-100"].                                                 | Optional     | 
| monitor_id          | Monitor ID from monitors response. Only used when requesting domains for a specific monitor.                                                                    | Optional     | 
| tlds                | List of TLDs to filter domains by.                                                                                                                              | Optional     | 
| mx_exists           | Filter domains by if they have an MX record in DNS.                                                                                                             | Optional     | 
| changed_since       | Filter domains by when they were last changed. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                   | Optional     | 
| escalated_since     | Filter domains by when they were last escalated. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                 | Optional     | 
| search              | A "contains" search for any portion of a domain name.                                                                                                           | Optional     | 
| sort                | Sort order for domain list. Valid values are an ordered list of the following: ["discovered_date", "changed_date", "risk_score"].                               | Optional     | 
| include_domain_data | Includes DNS and whois data in the response. Possible values are: True, False.                                                                                  | Optional     | 
| preview             | Preview mode used for testing. If set to True, only the first 10 results are returned but not limited by hourly restrictions. Possible values are: True, False. | Optional     | 
| order               | Sort order "asc" or "desc".                                                                                                                                     | Optional     | 
| limit               | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                                              | Optional     | 
| offset              | Default 0. Offset for pagination.                                                                                                                               | Optional     | 

#### Context Output

| **Path**                                                                      | **Type** | **Description**                       |
|-------------------------------------------------------------------------------|----------|---------------------------------------|
| DomainToolsIrisDetect.Escalated.state                                         | String   | State of the Domain.                  | 
| DomainToolsIrisDetect.Escalated.domain                                        | String   | Domain Name.                          | 
| DomainToolsIrisDetect.Escalated.status                                        | String   | Status of the Domain.                 | 
| DomainToolsIrisDetect.Escalated.discovered_date                               | String   | Creation Date.                        | 
| DomainToolsIrisDetect.Escalated.changed_date                                  | String   | Last Updated Date.                    | 
| DomainToolsIrisDetect.Escalated.risk_score                                    | String   | Risk Score for the Domain.            | 
| DomainToolsIrisDetect.Escalated.risk_score_status                             | Number   | Risk Score Status for the Domain.     | 
| DomainToolsIrisDetect.Escalated.risk_score_components.proximity               | Number   | Proximity Score for the Domain.       | 
| DomainToolsIrisDetect.Escalated.risk_score_components.threat_profile.phishing | Number   | Phishing Score for the Domain.        | 
| DomainToolsIrisDetect.Escalated.risk_score_components.threat_profile.malware  | Number   | Malware Score for the Domain.         | 
| DomainToolsIrisDetect.Escalated.risk_score_components.threat_profile.spam     | Number   | Spam Score for the Domain.            | 
| DomainToolsIrisDetect.Escalated.risk_score_components.threat_profile.evidence | Unknown  | Evidence for the Domain.              | 
| DomainToolsIrisDetect.Escalated.mx_exists                                     | Boolean  | MX Exists for the Domain.             | 
| DomainToolsIrisDetect.Escalated.tld                                           | String   | Domain TLD.                           | 
| DomainToolsIrisDetect.Escalated.id                                            | String   | Domain ID.                            | 
| DomainToolsIrisDetect.Escalated.escalations.escalation_type                   | String   | Escalation Type for the Domain.       | 
| DomainToolsIrisDetect.Escalated.escalations.id                                | String   | Escalation ID for the Domain.         | 
| DomainToolsIrisDetect.Escalated.escalations.created                           | String   | Escalation Created Date.              | 
| DomainToolsIrisDetect.Escalated.escalations.created_by                        | String   | Escalation Created By.                | 
| DomainToolsIrisDetect.Escalated.monitor_ids                                   | String   | Domain Monitor Id.                    | 
| DomainToolsIrisDetect.Escalated.assigned_by                                   | String   | Escalation Assigned By.               | 
| DomainToolsIrisDetect.Escalated.assigned_date                                 | String   | Escalation Assigned Date.             | 
| DomainToolsIrisDetect.Escalated.registrant_contact_email                      | String   | Registrant Email.                     | 
| DomainToolsIrisDetect.Escalated.name_server                                   | String   | Associated Nameserver for the Domain. | 
| DomainToolsIrisDetect.Escalated.registrar                                     | String   | Registrant Name.                      | 
| DomainToolsIrisDetect.Escalated.create_date                                   | String   | Created Date.                         | 
| DomainToolsIrisDetect.Escalated.ip.country_code                               | String   | Country code for the ip.              | 
| DomainToolsIrisDetect.Escalated.ip.ip                                         | String   | Associated ip for the Domain.         | 
| DomainToolsIrisDetect.Escalated.ip.isp                                        | String   | Associated isp for the Domain.        | 

#### Command example

```!domaintools-iris-detect-get-escalated-domains limit="2"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Escalated": [
      {
        "assigned_by": "nvojjala@loginsoft.com",
        "assigned_date": "2023-04-11T04:46:39.000000+00:00",
        "changed_date": "2023-04-10T07:52:11.000000+00:00",
        "discovered_date": "2023-04-10T07:45:31.478000+00:00",
        "domain": "amazonmetaworld.net.tr",
        "escalations": [
          {
            "created": "2023-04-11T04:46:39.181378+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "google_safe",
            "id": "43gB2Pwg6m"
          }
        ],
        "id": "8Wq8Qj9X7P",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": 8,
        "risk_score_components": {
          "proximity": 5,
          "threat_profile": {
            "evidence": [],
            "malware": 1,
            "phishing": 6,
            "spam": 8
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "net.tr"
      },
      {
        "assigned_by": "nvojjala@loginsoft.com",
        "assigned_date": "2023-04-11T05:18:05.000000+00:00",
        "changed_date": "2023-04-05T12:44:21.000000+00:00",
        "discovered_date": "2023-04-05T12:07:54.646000+00:00",
        "domain": "amazon.nexus",
        "escalations": [
          {
            "created": "2023-04-11T05:18:05.262047+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "google_safe",
            "id": "43gB2a3g6m"
          }
        ],
        "id": "ZadmVQOJ0E",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": 0,
        "risk_score_components": {
          "proximity": 0,
          "threat_profile": {
            "phishing": 53
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "nexus"
      }
    ]
  }
}
```

#### Human Readable Output

> ### Escalated Domains
>|dt_changed_date|dt_create_date|dt_discovered_date|dt_domain|dt_domain_id|dt_escalations|dt_monitor_ids|dt_mx_exists|dt_proximity_score|dt_registrant_contact_email|dt_registrar|dt_risk_score|dt_risk_status|dt_state|dt_status|dt_threat_profile_evidence|dt_threat_profile_malware|dt_threat_profile_phishing|dt_threat_profile_spam|dt_tld|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 2023-04-10T07:52:11.000000+00:00 |  | 2023-04-10T07:45:31.478000+00:00 | amazonmetaworld.net.tr | 8Wq8Qj9X7P | {'escalation_type': 'google_safe', 'id': '43gB2Pwg6m', 'created': '2023-04-11T04:46:39.181378+00:00', 'created_by': 'nvojjala@loginsoft.com'} | rA7bn46jQ3 | false | 5 |  |  | 8 | full | watched | active |  | 1 | 6 | 8 | net.tr |
>| 2023-04-05T12:44:21.000000+00:00 |  | 2023-04-05T12:07:54.646000+00:00 | amazon.nexus | ZadmVQOJ0E | {'escalation_type': 'google_safe', 'id': '43gB2a3g6m', 'created': '2023-04-11T05:18:05.262047+00:00', 'created_by': 'nvojjala@loginsoft.com'} | rA7bn46jQ3 | false | 0 |  |  | 0 | full | watched | active |  |  | 53 |  | nexus |

### domaintools-iris-detect-get-blocklist-domains

***
Manually retrieve domains that your organization has marked as "blocklisted", matching all of your monitored terms, or a
specific term specified by a "monitor_id" that can be retrieved using the domaintools-iris-detect-get-monitors-list
command. The number of domains returned is limited to 50 if including DNS and whois details, or 500 otherwise. Use the
offset parameter for pagination.

#### Base Command

`domaintools-iris-detect-get-blocklist-domains`

#### Input

| **Argument Name**   | **Description**                                                                                                                                                 | **Required** |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| monitor_id          | Monitor ID from monitors response. Only used when requesting domains for a specific monitor.                                                                    | Optional     | 
| tlds                | List of TLDs to filter domains by.                                                                                                                              | Optional     | 
| mx_exists           | Filter domains by if they have an MX record in DNS. Possible values are: True, False.                                                                           | Optional     | 
| changed_since       | Filter domains by when they were last changed. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                   | Optional     | 
| search              | Sort order for domain list. Valid values are an ordered list.                                                                                                   | Optional     | 
| sort                | Sort order for domain list. Possible values are: discovered_date, changed_date, risk_score.                                                                     | Optional     | 
| include_domain_data | Includes DNS and whois data in the response. Possible values are: True, False.                                                                                  | Optional     | 
| preview             | Preview mode used for testing. If set to True, only the first 10 results are returned but not limited by hourly restrictions. Possible values are: True, False. | Optional     | 
| escalated_since     | Filter domains by when they were last escalated. Provide a datetime in ISO 8601 format, for example 2022-05-18T12:19:51.685496.                                 | Optional     | 
| order               | Sort order "asc" or "desc".                                                                                                                                     | Optional     | 
| risk_score_ranges   | List of risk score ranges to filter domains by. Valid values are: ["0-0", "1-39", "40-69", "70-99", "100-100"].                                                 | Optional     | 
| limit               | Default 100. Limit for pagination. Restricted to maximum 50 if include_domain_data is set to True.                                                              | Optional     | 
| offset              | Default 0. Offset for pagination.                                                                                                                               | Optional     | 

#### Context Output

| **Path**                                                                    | **Type** | **Description**                       |
|-----------------------------------------------------------------------------|----------|---------------------------------------|
| DomainToolsIrisDetect.Blocked.state                                         | String   | State of the Domain.                  | 
| DomainToolsIrisDetect.Blocked.domain                                        | String   | Domain Name.                          | 
| DomainToolsIrisDetect.Blocked.status                                        | String   | Status of the Domain.                 | 
| DomainToolsIrisDetect.Blocked.discovered_date                               | String   | Creation Date.                        | 
| DomainToolsIrisDetect.Blocked.changed_date                                  | String   | Last Updated Date.                    | 
| DomainToolsIrisDetect.Blocked.risk_score                                    | String   | Risk Score for the Domain.            | 
| DomainToolsIrisDetect.Blocked.risk_score_status                             | Number   | Risk Score Status for the Domain.     | 
| DomainToolsIrisDetect.Blocked.risk_score_components.proximity               | Number   | Proximity Score for the Domain.       | 
| DomainToolsIrisDetect.Blocked.risk_score_components.threat_profile.phishing | Number   | Phishing Score for the Domain.        | 
| DomainToolsIrisDetect.Blocked.risk_score_components.threat_profile.malware  | Number   | Malware Score for the Domain.         | 
| DomainToolsIrisDetect.Blocked.risk_score_components.threat_profile.spam     | Number   | Spam Score for the Domain.            | 
| DomainToolsIrisDetect.Blocked.risk_score_components.threat_profile.evidence | Unknown  | Evidence for the Domain.              | 
| DomainToolsIrisDetect.Blocked.mx_exists                                     | Boolean  | MX Exists for the Domain.             | 
| DomainToolsIrisDetect.Blocked.tld                                           | String   | Domain TLD.                           | 
| DomainToolsIrisDetect.Blocked.id                                            | String   | Domain ID.                            | 
| DomainToolsIrisDetect.Blocked.escalations.escalation_type                   | String   | Escalation Type for the Domain.       | 
| DomainToolsIrisDetect.Blocked.escalations.id                                | String   | Escalation ID for the Domain.         | 
| DomainToolsIrisDetect.Blocked.escalations.created                           | String   | Escalation Created Date.              | 
| DomainToolsIrisDetect.Blocked.escalations.created_by                        | String   | Escalation Created By.                | 
| DomainToolsIrisDetect.Blocked.monitor_ids                                   | String   | Domain Monitor Id.                    | 
| DomainToolsIrisDetect.Blocked.assigned_by                                   | String   | Escalation Assigned By.               | 
| DomainToolsIrisDetect.Blocked.assigned_date                                 | String   | Escalation Assigned Date.             | 
| DomainToolsIrisDetect.Blocked.registrant_contact_email                      | String   | Registrant Email.                     | 
| DomainToolsIrisDetect.Blocked.name_server                                   | String   | Associated Nameserver for the Domain. | 
| DomainToolsIrisDetect.Blocked.registrar                                     | String   | Registrant Name.                      | 
| DomainToolsIrisDetect.Blocked.create_date                                   | String   | Created Date.                         | 
| DomainToolsIrisDetect.Blocked.ip.country_code                               | String   | Country code for the ip.              | 
| DomainToolsIrisDetect.Blocked.ip.ip                                         | String   | Associated ip for the Domain.         | 
| DomainToolsIrisDetect.Blocked.ip.isp                                        | String   | Associated isp for the Domain.        | 

#### Command example

```!domaintools-iris-detect-get-blocklist-domains limit="2"```

#### Context Example

```json
{
  "DomainToolsIrisDetect": {
    "Blocked": [
      {
        "changed_date": "2023-04-10T05:58:01.000000+00:00",
        "discovered_date": "2023-04-10T04:52:28.545000+00:00",
        "domain": "alixpress.co",
        "escalations": [
          {
            "created": "2023-04-10T14:33:11.342255+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "blocked",
            "id": "nzgWDr3b9Y"
          }
        ],
        "id": "gaeMyYl1Va",
        "monitor_ids": [
          "QEMba8wmxo"
        ],
        "mx_exists": true,
        "risk_score": 21,
        "risk_score_components": {
          "proximity": 21,
          "threat_profile": {
            "evidence": [],
            "malware": 20,
            "phishing": 15,
            "spam": 17
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "co"
      },
      {
        "assigned_by": "nvojjala@loginsoft.com",
        "assigned_date": "2023-04-11T05:18:00.000000+00:00",
        "changed_date": "2023-04-05T15:08:54.000000+00:00",
        "discovered_date": "2023-04-05T15:01:50.701000+00:00",
        "domain": "amazon.mov",
        "escalations": [
          {
            "created": "2023-04-11T05:17:59.782456+00:00",
            "created_by": "nvojjala@loginsoft.com",
            "escalation_type": "blocked",
            "id": "nzgWDAzb9Y"
          }
        ],
        "id": "gaeMVJX8ea",
        "monitor_ids": [
          "rA7bn46jQ3"
        ],
        "mx_exists": false,
        "risk_score": 0,
        "risk_score_components": {
          "proximity": 0,
          "threat_profile": {
            "phishing": 53
          }
        },
        "risk_score_status": "full",
        "state": "watched",
        "status": "active",
        "tld": "mov"
      }
    ]
  }
}
```

#### Human Readable Output

> ### Blocked Domains
>|dt_changed_date|dt_create_date|dt_discovered_date|dt_domain|dt_domain_id|dt_escalations|dt_monitor_ids|dt_mx_exists|dt_proximity_score|dt_registrant_contact_email|dt_registrar|dt_risk_score|dt_risk_status|dt_state|dt_status|dt_threat_profile_evidence|dt_threat_profile_malware|dt_threat_profile_phishing|dt_threat_profile_spam|dt_tld|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 2023-04-10T05:58:01.000000+00:00 |  | 2023-04-10T04:52:28.545000+00:00 | alixpress.co | gaeMyYl1Va | {'escalation_type': 'blocked', 'id': 'nzgWDr3b9Y', 'created': '2023-04-10T14:33:11.342255+00:00', 'created_by': 'nvojjala@loginsoft.com'} | QEMba8wmxo | true | 21 |  |  | 21 | full | watched | active |  | 20 | 15 | 17 | co |
>| 2023-04-05T15:08:54.000000+00:00 |  | 2023-04-05T15:01:50.701000+00:00 | amazon.mov | gaeMVJX8ea | {'escalation_type': 'blocked', 'id': 'nzgWDAzb9Y', 'created': '2023-04-11T05:17:59.782456+00:00', 'created_by': 'nvojjala@loginsoft.com'} | rA7bn46jQ3 | false | 0 |  |  | 0 | full | watched | active |  |  | 53 |  | mov |

### domaintools-iris-detect-reset-fetch-indicators

***
This command will reset your fetch history.

#### Base Command

`domaintools-iris-detect-reset-fetch-indicators`

#### Input

There are no input arguments for this command.

#### Context Output

There is no context output for this command.

#### Command example

```!domaintools-iris-detect-reset-fetch-indicators```

#### Human Readable Output

> Fetch history deleted successfully
