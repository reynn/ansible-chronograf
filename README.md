chronograf
========

[![Build Status](https://travis-ci.org/kbrebanov/ansible-chronograf.svg?branch=master)](https://travis-ci.org/kbrebanov/ansible-chronograf)

Installs and configures Chronograf.

Requirements
------------

This role requires Ansible 1.9 or higher.

Role Variables
--------------

| Name                                             | Default                | Description                                                                                                                                                |
|:-------------------------------------------------|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| chronograf_version                                 | 1.0.2                  | Version of Chronograf to install                                                                                                                             |
| chronograf_hostname                                | ''                     | Use this option to manually set the hostname                                                                                                               |
| chronograf_reporting_disabled                      | false                  | When enabled, Chronograf will report usage data every 24 hours to usage.influxdata.com                                                                       |
| chronograf_meta_dir                                | /var/lib/chronograf/meta | Where the metadata/raft database is stored                                                                                                                 |
| chronograf_meta_retention_autocreate               | true                   |                                                                                                                                                            |
| chronograf_meta_logging_enabled                    | true                   | If log messages are printed for the meta service                                                                                                           |
| chronograf_meta_pprof_enabled                      | false                  |                                                                                                                                                            |
| chronograf_meta_lease_duration                     | 1m0s                   | The default duration for leases                                                                                                                            |
| chronograf_data_enabled                            | true                   | Controls if this node holds time series data shards in the cluster                                                                                         |
| chronograf_data_dir                                | /var/lib/chronograf/data |                                                                                                                                                            |
| chronograf_data_wal_dir                            | /var/lib/chronograf/wal  |                                                                                                                                                            |
| chronograf_data_wal_logging_enabled                | true                   | If log messages are printed for the storage engine                                                                                                         |
| chronograf_data_trace_logging_enabled              | false                  | Trace logging provides more verbose output around the tsm engine. Turning this on can provide more useful output for debugging tsm engine issues           |
| chronograf_data_query_log_enabled                  | true                   | Whether queries should be logged before execution. Very useful for troubleshooting, but will log any sensitive data contained within a query               |
| chronograf_data_cache_max_memory_size              | 524288000              | Maximum size a shard's cache can reach before it starts rejecting writes                                                                                   |
| chronograf_data_cache_snapshot_memory_size         | 26214400               | Size at which the engine will snapshot the cache and write it to a TSM file, freeing up memory                                                             |
| chronograf_data_cache_snapshot_write_cold_duration | 1h                     | Length of time at which the engine will snapshot the cache and write it to a new TSM file if the shard hans't received writes or deletes                   |
| chronograf_data_compact_min_file_count             | 3                      | Minimum number of TSM files that need to exist before a compaction cycle will run                                                                          |
| chronograf_data_compact_full_write_cold_duration   | 24h                    | Duration at which the engine will compact all TSM files in a shard if it hasn't received a write or delete                                                 |
| chronograf_data_max_points_per_block               | 1000                   | Maximum number of points in an encoded block in a TSM file. Larger numbers may yield better compression but could incur a perfomance penalty when querying |
| chronograf_coordinator_write_timeout               | 10s                    |                                                                                                                                                            |
| chronograf_coordinator_max_concurrent_queries      | 0                      |                                                                                                                                                            |
| chronograf_coordinator_query_timeout               | 0                      |                                                                                                                                                            |
| chronograf_coordinator_log_queries_after           | 0                      |                                                                                                                                                            |
| chronograf_coordinator_max_select_point            | 0                      |                                                                                                                                                            |
| chronograf_coordinator_max_select_series           | 0                      |                                                                                                                                                            |
| chronograf_coordinator_max_select_buckets          | 0                      |                                                                                                                                                            |
| chronograf_retention_enabled                       | true                   |                                                                                                                                                            |
| chronograf_retention_check_interval                | 30m                    |                                                                                                                                                            |
| chronograf_shard_precreation_enabled               | true                   |                                                                                                                                                            |
| chronograf_shard_precreation_check_interval        | 10m                    |                                                                                                                                                            |
| chronograf_shard_precreation_advance_period        | 30m                    |                                                                                                                                                            |
| chronograf_monitor_store_enabled                   | true                   | Whether to record statistics internally                                                                                                                    |
| chronograf_monitor_store_database                  | _internal              | The destination database for recorded statistics                                                                                                           |
| chronograf_monitor_store_interval                  | 10s                    | The interval at which to record statistics                                                                                                                 |
| chronograf_admin_enabled                           | true                   |                                                                                                                                                            |
| chronograf_admin_bind_address                      | ":8083"                |                                                                                                                                                            |
| chronograf_admin_https_enabled                     | false                  |                                                                                                                                                            |
| chronograf_admin_https_certificate                 | /etc/ssl/chronograf.pem  |                                                                                                                                                            |
| chronograf_http_enabled                            | true                   |                                                                                                                                                            |
| chronograf_http_bind_address                       | ":8086"                |                                                                                                                                                            |
| chronograf_http_auth_enabled                       | false                  |                                                                                                                                                            |
| chronograf_http_log_enabled                        | true                   |                                                                                                                                                            |
| chronograf_http_write_tracing                      | false                  |                                                                                                                                                            |
| chronograf_http_pprof_enabled                      | false                  |                                                                                                                                                            |
| chronograf_http_https_enabled                      | false                  |                                                                                                                                                            |
| chronograf_http_https_certificate                  | /etc/ssl/chronograf.pem  |                                                                                                                                                            |
| chronograf_http_https_private_key                  | ''                     | Use a separate private key location                                                                                                                        |
| chronograf_http_max_row_limit                      | 10000                  |                                                                                                                                                            |
| chronograf_http_realm                              | Chronograf               |                                                                                                                                                            |
| chronograf_subscriber_enabled                      | true                   |                                                                                                                                                            |
| chronograf_subscriber_http_timeout                 | 30s                    |                                                                                                                                                            |
| chronograf_graphite_enabled                        | false                  |                                                                                                                                                            |
| chronograf_graphite_database                       | graphite               |                                                                                                                                                            |
| chronograf_graphite_bind_address                   | ":2003"                |                                                                                                                                                            |
| chronograf_graphite_protocol                       | tcp                    |                                                                                                                                                            |
| chronograf_graphite_consistency_level              | one                    |                                                                                                                                                            |
| chronograf_graphite_batch_size                     | 5000                   |                                                                                                                                                            |
| chronograf_graphite_batch_pending                  | 10                     |                                                                                                                                                            |
| chronograf_graphite_batch_timeout                  | 1s                     |                                                                                                                                                            |
| chronograf_graphite_udp_read_buffer                | 0                      |                                                                                                                                                            |
| chronograf_graphite_separator                      | .                      |                                                                                                                                                            |
| chronograf_graphite_tags                           | []                     |                                                                                                                                                            |
| chronograf_graphite_templates                      | []                     |                                                                                                                                                            |
| chronograf_collectd_enabled                        | false                  |                                                                                                                                                            |
| chronograf_collectd_bind_address                   | ''                     |                                                                                                                                                            |
| chronograf_collectd_database                       | ''                     |                                                                                                                                                            |
| chronograf_collectd_typesdb                        | ''                     |                                                                                                                                                            |
| chronograf_collectd_batch_size                     | 1000                   |                                                                                                                                                            |
| chronograf_collectd_batch_pending                  | 5                      |                                                                                                                                                            |
| chronograf_collectd_batch_timeout                  | 1s                     |                                                                                                                                                            |
| chronograf_collectd_read_buffer                    | 0                      |                                                                                                                                                            |
| chronograf_opentsdb_enabled                        | false                  |                                                                                                                                                            |
| chronograf_opentsdb_bind_address                   | ":4242"                |                                                                                                                                                            |
| chronograf_opentsdb_database                       | opentsdb               |                                                                                                                                                            |
| chronograf_opentsdb_retention_policy               | ''                     |                                                                                                                                                            |
| chronograf_opentsdb_consistency_level              | one                    |                                                                                                                                                            |
| chronograf_opentsdb_tls_enabled                    | false                  |                                                                                                                                                            |
| chronograf_opentsdb_certificate                    | ''                     |                                                                                                                                                            |
| chronograf_opentsdb_log_point_errors               | true                   |                                                                                                                                                            |
| chronograf_opentsdb_batch_size                     | 1000                   |                                                                                                                                                            |
| chronograf_opentsdb_batch_pending                  | 5                      |                                                                                                                                                            |
| chronograf_opentsdb_batch_timeout                  | 1s                     |                                                                                                                                                            |
| chronograf_udp_enabled                             | false                  |                                                                                                                                                            |
| chronograf_udp_bind_address                        | ''                     |                                                                                                                                                            |
| chronograf_udp_database                            | udp                    |                                                                                                                                                            |
| chronograf_udp_retention_policy                    | ''                     |                                                                                                                                                            |
| chronograf_udp_batch_size                          | 1000                   |                                                                                                                                                            |
| chronograf_udp_batch_pending                       | 5                      |                                                                                                                                                            |
| chronograf_udp_batch_timeout                       | 1s                     |                                                                                                                                                            |
| chronograf_udp_read_buffer                         | 0                      |                                                                                                                                                            |
| chronograf_udp_payload_size                        | 65536                  |                                                                                                                                                            |
| chronograf_continuous_queries_log_enabled          | true                   |                                                                                                                                                            |
| chronograf_continuous_queries_enabled              | true                   |                                                                                                                                                            |
| chronograf_continuous_queries_run_interval         | 1s                     |                                                                                                                                                            |

Dependencies
------------

None

Example Playbook
----------------

Install Chronograf
```yaml
- hosts: all
  roles:
    - kbrebanov.chronograf
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
