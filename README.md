ansible-graylog-input
=====================

A role to configure some given graylog inputs.

Requirements
------------


Role Variables
--------------


Dependencies
------------

This is a standalone role.

Example Playbook
----------------

Configure an input and a dedicated extractor.

    - hosts: servers
      roles:
         - ansible-graylog-input
      vars:
         graylog_api: http://graylog.local/api
         graylog_login: foo
         graylog_password: bar
 
         graylog_inputs:
             - input:
                    title: "GELF - webservice"
                    global: true
                    type: "org.graylog2.inputs.gelf.http.GELFHttpInput"
                    configuration:
                         idle_writer_timeout: 60
                         recv_buffer_size: 1048576
                         max_chunk_size: 65536
                         tcp_keepalive: false
                         enable_cors: true
                         tls_client_auth_cert_file: ""
                         bind_address: "0.0.0.0"
                         tls_cert_file: ""
                         decompress_size_limit: 8388608
                         port: 8081
                         tls_key_file: ""
                         tls_enable: false
                         tls_key_password: ""
                         tls_client_auth: "disabled"
                         override_source: null
               extractors:
                     - title: "Message en JSON"
                       cut_or_copy: "cut"
                       extractor_type: "json"
                       converters: []
                       source_field: "message"
                       target_field:
                       condition_type: "regex"
                       condition_value: "^\\{"
                       extractor_config:
                          flatten: false
                          list_separator: ", "
                          kv_separator: "="
                          key_prefix: ""
                          key_separator: "_"
                          replace_key_whitespace: false
                          key_whitespace_replacement: "_"

License
-------

GPL-3+

Author Information
------------------

Mathieu GRZYBEK
