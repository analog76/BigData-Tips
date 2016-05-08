Ambari alert configuration tips. 


## How to get all the alert definitions from ambari server

    curl -v -X GET -u  <<username:password>>  -H 'X-Requested-By:ambari' https://localhost:8080/api/v1/clusters/<<cluster_name>>/alert_definitions

For example,

    curl -v -X GET -u  admin:admin -H 'X-Requested-By:ambari' https://localhost:8080/api/v1/clusters/dz/alert_definitions



## How to get details of a particular alert definition

    curl  -X GET -u <<username:password>> http://localhost:8080/api/v1/clusters/<<cluster_name>>/alert_definitions/49


For example,

     curl  -X GET -u admin:admin http://localhost:8080/api/v1/clusters/dz/alert_definitions/19


This command will give the output like this. 

     	{
		  "href" : "http://localhost:8080/api/v1/clusters/dz/alert_definitions/19",
	  "AlertDefinition" : {
		"cluster_name" : "dz",
		"component_name" : "APP_TIMELINE_SERVER",
		"description" : "This host-level alert is triggered if the App Timeline Server Web UI is unreachable.",
		"enabled" : true,
		"id" : 19,
		"ignore_host" : false,
		"interval" : 1,
		"label" : "App Timeline Web UI",
		"name" : "yarn_app_timeline_server_webui",
		"scope" : "ANY",
		"service_name" : "YARN",
		"source" : {
		  "reporting" : {
			"ok" : {
			  "text" : "HTTP {0} response in {2:.3f}s"
			},
			"warning" : {
			  "text" : "HTTP {0} response from {1} in {2:.3f}s ({3})"
			},
			"critical" : {
			  "text" : "Connection failed to {1} ({3})"
			}
		  },
		  "type" : "WEB",
		  "uri" : {
			"http" : "{{yarn-site/yarn.timeline-service.webapp.address}}",
			"https" : "{{yarn-site/yarn.timeline-service.webapp.https.address}}",
			"https_property" : "{{yarn-site/yarn.http.policy}}",
			"https_property_value" : "HTTPS_ONLY",
			"kerberos_keytab" : "{{yarn-site/yarn.timeline-service.http-authentication.kerberos.keytab}}",
			"kerberos_principal" : "{{yarn-site/yarn.timeline-service.http-authentication.kerberos.principal}}",
			"default_port" : 0.0,
			"connection_timeout" : 5.0
		  }
		}
	  }
	}



To increase the connection time out, create a json file with increase_19_alert.json

	{
	   "AlertDefinition" : {
		"cluster_name" : "dz",
		"component_name" : "APP_TIMELINE_SERVER",
		"description" : "This host-level alert is triggered if the App Timeline Server Web UI is unreachable.",
		"enabled" : true,
		"id" : 19,
		"ignore_host" : false,
		"interval" : 1,
		"label" : "App Timeline Web UI",
		"name" : "yarn_app_timeline_server_webui",
		"scope" : "ANY",
		"service_name" : "YARN",
		"source" : {
		  "reporting" : {
			"ok" : {
			  "text" : "HTTP {0} response in {2:.3f}s"
			},
			"warning" : {
			  "text" : "HTTP {0} response from {1} in {2:.3f}s ({3})"
			},
			"critical" : {
			  "text" : "Connection failed to {1} ({3})"
			}
		  },
		  "type" : "WEB",
		  "uri" : {
			"http" : "{{yarn-site/yarn.timeline-service.webapp.address}}",
			"https" : "{{yarn-site/yarn.timeline-service.webapp.https.address}}",
			"https_property" : "{{yarn-site/yarn.http.policy}}",
			"https_property_value" : "HTTPS_ONLY",
			"kerberos_keytab" : "{{yarn-site/yarn.timeline-service.http-authentication.kerberos.keytab}}",
			"kerberos_principal" : "{{yarn-site/yarn.timeline-service.http-authentication.kerberos.principal}}",
			"default_port" : 0.0,
			"connection_timeout" : 30.0
		  }
		}
	  }
	}


Run the following command to update the json file to the ambari-server.

    curl -H "X-Requested-By: ambari" -X PUT -u admin:admin http://localhost:8080/api/v1/clusters/dz/alert_definitions/19 -d @increase_19_alert.json

