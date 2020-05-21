# Grafana-LDAP AD Authentication
#### How to configure the AD/LDAP Authentication fro grafana
The steps to configure the Grafana LDAP integration are as follow:

Step 1:- Goto Ambari Server UI -> AMBARI_METRICS -> Configs -> Advanced ams-grafana-ini  

Step 2 :- Filter for auth.ldap; 
  Edit to the following: 

    [auth.ldap] 
    enabled = true 
    config_file = /etc/ambari-metrics-grafana/ldap.toml 

 create the ldap.toml with the right ACL by following the instructions on link below: 
http://docs.grafana.org/installation/ldap/#example-config


Step3 :- 
   
     [[servers]]
        # Ldap server host (specify multiple hosts space separated)
        host = "sme-2012-ad.support.com"
        # Default port is 389 or 636 if use_ssl = true
        port = 389
        # Set to true if ldap server supports TLS
        use_ssl = false
        # Set to true if connect ldap server with STARTTLS pattern (create connection in insecure, then upgrade to secure connection with TLS)
        start_tls = false
        # set to true if you want to skip ssl cert validation
        ssl_skip_verify = false
        # set to the path to your root CA certificate or leave unset to use system defaults
        # root_ca_cert = "/path/to/certificate.crt"
        # Authentication against LDAP servers requiring client certificates
        # client_cert = "/path/to/client.crt"
        # client_key = "/path/to/client.key"
        # Search user bind dn
    bind_dn = "CN=test1,OU=hortonworks,DC=SUPPORT,DC=COM"
    # Search user bind password
    # If the password contains # or ; you have to wrap it with triple quotes. Ex """#password;"""
    bind_password = <password>

    # User search filter, for example "(cn=%s)" or "(sAMAccountName=%s)" or "(uid=%s)"
    # Allow login from email or username, example "(|(sAMAccountName=%s)(userPrincipalName=%s))"
    search_filter = "(sAMAccountName=%s)"

    # An array of base dns to search through
    search_base_dns = ["dc=support,dc=com"]

     group_search_filter = "(&(objectClass=group)(memberOf=%s))"
     group_search_filter_user_attribute = "member"
     group_search_base_dns = ["dc=support,dc=com"]

    # Specify names of the ldap attributes your ldap uses
    [servers.attributes]
    name = "sAMAccountName"
    surname = "sn"
    username = "sAMAccountName"
    member_of = "memberOf"
    email =  "email"
