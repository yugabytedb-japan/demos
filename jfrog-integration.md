# YugabyteDB for JFrog database

## Overview

The detail requirements are listed in JFrog's [webpages](https://www.jfrog.com/confluence/display/JFROG/Configuring+the+Database#ConfiguringtheDatabase-DatabaseConnectionSettings).

## schema in postgresql

### tables

```
                        List of relations
 Schema |              Name              |   Type   |    Owner
--------+--------------------------------+----------+-------------
 public | access_configs                 | table    | artifactory
 public | access_db_check                | table    | artifactory
 public | access_distributed_lock        | table    | artifactory
 public | access_emails_log              | table    | artifactory
 public | access_federation_log          | table    | artifactory
 public | access_federation_servers      | table    | artifactory
 public | access_groups                  | table    | artifactory
 public | access_groups_custom_data      | table    | artifactory
 public | access_master_key_status       | table    | artifactory
 public | access_nodes                   | table    | artifactory
 public | access_permission_action       | table    | artifactory
 public | access_permissions             | table    | artifactory
 public | access_permissions_custom_data | table    | artifactory
 public | access_platform_config         | table    | artifactory
 public | access_schema_version          | table    | artifactory
 public | access_servers                 | table    | artifactory
 public | access_tokens                  | table    | artifactory
 public | access_topology                | table    | artifactory
 public | access_unique_ids              | table    | artifactory
 public | access_users                   | table    | artifactory
 public | access_users_custom_data       | table    | artifactory
 public | access_users_groups            | table    | artifactory
 public | archive_names                  | table    | artifactory
 public | archive_paths                  | table    | artifactory
 public | artifact_bundles               | table    | artifactory
 public | artifactory_servers            | table    | artifactory
 public | binaries                       | table    | artifactory
 public | binaries_tasks                 | table    | artifactory
 public | binary_blobs                   | table    | artifactory
 public | blob_infos                     | table    | artifactory
 public | build_artifacts                | table    | artifactory
 public | build_dependencies             | table    | artifactory
 public | build_modules                  | table    | artifactory
 public | build_promotions               | table    | artifactory
 public | build_props                    | table    | artifactory
 public | builds                         | table    | artifactory
 public | bundle_blobs                   | table    | artifactory
 public | bundle_files                   | table    | artifactory
 public | configs                        | table    | artifactory
 public | db_properties                  | table    | artifactory
 public | distributed_locks              | table    | artifactory
 public | indexed_archives               | table    | artifactory
 public | indexed_archives_entries       | table    | artifactory
 public | jobs                           | table    | artifactory
 public | master_key_status              | table    | artifactory
 public | md_configs                     | table    | artifactory
 public | md_contributors                | table    | artifactory
 public | md_database_migrations         | table    | artifactory
 public | md_fil_qualifiers              | table    | artifactory
 public | md_fil_targets                 | table    | artifactory
 public | md_files                       | table    | artifactory
 public | md_files_versions              | table    | artifactory
 public | md_licenses                    | table    | artifactory
 public | md_lock                        | table    | artifactory
 public | md_packages                    | table    | artifactory
 public | md_pkg_descriptions            | table    | artifactory
 public | md_pkg_info_sources            | table    | artifactory
 public | md_pkg_licenses                | table    | artifactory
 public | md_pkg_op_risk                 | table    | artifactory
 public | md_pkg_qualifiers              | table    | artifactory
 public | md_pkg_stats                   | table    | artifactory
 public | md_pkg_tags                    | table    | artifactory
 public | md_pkg_user_properties         | table    | artifactory
 public | md_pkg_vulns_sum               | table    | artifactory
 public | md_repos                       | table    | artifactory
 public | md_servers                     | table    | artifactory
 public | md_sources                     | table    | artifactory
 public | md_task_batches                | table    | artifactory
 public | md_tasks                       | table    | artifactory
 public | md_ver_contributors            | table    | artifactory
 public | md_ver_licenses                | table    | artifactory
 public | md_ver_op_risk                 | table    | artifactory
 public | md_ver_qualifiers              | table    | artifactory
 public | md_ver_repos                   | table    | artifactory
 public | md_ver_stats                   | table    | artifactory
 public | md_ver_tags                    | table    | artifactory
 public | md_ver_user_properties         | table    | artifactory
 public | md_ver_vulns_sum               | table    | artifactory
 public | md_versions                    | table    | artifactory
 public | migration_status               | table    | artifactory
 public | module_props                   | table    | artifactory
 public | node_event_cursor              | table    | artifactory
 public | node_event_priorities          | table    | artifactory
 public | node_events                    | table    | artifactory
 public | node_events_errors             | table    | artifactory
 public | node_events_event_id_seq       | sequence | artifactory
 public | node_events_tmp                | table    | artifactory
 public | node_meta_infos                | table    | artifactory
 public | node_props                     | table    | artifactory
 public | nodes                          | table    | artifactory
 public | schema_change_log              | table    | artifactory
 public | stats                          | table    | artifactory
 public | stats_remote                   | table    | artifactory
 public | tasks                          | table    | artifactory
 public | trusted_keys                   | table    | artifactory
 public | ui_session                     | table    | artifactory
 public | ui_session_attributes          | table    | artifactory
 public | unique_ids                     | table    | artifactory
 public | watches                        | table    | artifactory
(99 rows)
```

### indexes

```
# \di
                                       List of relations
 Schema |              Name              | Type  |    Owner    |             Table
--------+--------------------------------+-------+-------------+--------------------------------
 public | access_config_key_pk           | index | artifactory | access_platform_config
 public | access_configs_pk              | index | artifactory | access_configs
 public | access_db_check_pk             | index | artifactory | access_db_check
 public | access_distributed_lock_key_pk | index | artifactory | access_distributed_lock
 public | access_emails_log_last_sent    | index | artifactory | access_emails_log
 public | access_emails_log_pk           | index | artifactory | access_emails_log
 public | access_fed_log_created_idx     | index | artifactory | access_federation_log
 public | access_fed_log_pk              | index | artifactory | access_federation_log
 public | access_fed_ser_pk              | index | artifactory | access_federation_servers
 public | access_group_lower_name_idx    | index | artifactory | access_groups
 public | access_groups_data_key_idx     | index | artifactory | access_groups_custom_data
 public | access_groups_data_pk          | index | artifactory | access_groups_custom_data
 public | access_groups_data_value_idx   | index | artifactory | access_groups_custom_data
 public | access_groups_name_idx         | index | artifactory | access_groups
 public | access_groups_pk               | index | artifactory | access_groups
 public | access_kid_pk                  | index | artifactory | access_master_key_status
 public | access_master_key              | index | artifactory | access_master_key_status
 public | access_nodes_pk                | index | artifactory | access_nodes
 public | access_perm_action_perm_id_idx | index | artifactory | access_permission_action
 public | access_perm_action_pk          | index | artifactory | access_permission_action
 public | access_perm_data_pk            | index | artifactory | access_permissions_custom_data
 public | access_perm_disp_name_constr   | index | artifactory | access_permissions
 public | access_perm_lower_display_idx  | index | artifactory | access_permissions
 public | access_perm_perm_id_unique_idx | index | artifactory | access_permissions
 public | access_permissions_pk          | index | artifactory | access_permissions
 public | access_schema_version_pk       | index | artifactory | access_schema_version
 public | access_schema_version_s_idx    | index | artifactory | access_schema_version
 public | access_servers_name_unique_idx | index | artifactory | access_servers
 public | access_servers_pk              | index | artifactory | access_servers
 public | access_tokens_pk               | index | artifactory | access_tokens
 public | access_tokens_rfrsh_tkn_idx    | index | artifactory | access_tokens
 public | access_topology_pk             | index | artifactory | access_topology
 public | access_tplgy_router_id_idx     | index | artifactory | access_topology
 public | access_unique_ids_pk           | index | artifactory | access_unique_ids
 public | access_username_idx            | index | artifactory | access_tokens
 public | access_username_type_idx       | index | artifactory | access_tokens
 public | access_users_data_key_idx      | index | artifactory | access_users_custom_data
 public | access_users_data_pk           | index | artifactory | access_users_custom_data
 public | access_users_data_value_idx    | index | artifactory | access_users_custom_data
 public | access_users_groups_pk         | index | artifactory | access_users_groups
 public | access_users_pk                | index | artifactory | access_users
 public | access_users_username_idx      | index | artifactory | access_users
 public | archive_names_name_idx         | index | artifactory | archive_names
 public | archive_names_pk               | index | artifactory | archive_names
 public | archive_paths_path_idx         | index | artifactory | archive_paths
 public | archive_paths_pk               | index | artifactory | archive_paths
 public | artifactory_servers_pk         | index | artifactory | artifactory_servers
 public | binaries_md5_idx               | index | artifactory | binaries
 public | binaries_pk                    | index | artifactory | binaries
 public | binaries_sha256_idx            | index | artifactory | binaries
 public | binaries_tasks_count_idx       | index | artifactory | binaries_tasks
 public | binaries_tasks_pk              | index | artifactory | binaries_tasks
 public | binaries_tasks_server_id_idx   | index | artifactory | binaries_tasks
 public | binaries_tasks_start_time_idx  | index | artifactory | binaries_tasks
 public | binaries_tasks_time_idx        | index | artifactory | binaries_tasks
 public | binary_blobs_pk                | index | artifactory | binary_blobs
 public | blob_infos_checksum            | index | artifactory | blob_infos
 public | build_artifacts_md5_idx        | index | artifactory | build_artifacts
 public | build_artifacts_module_id_idx  | index | artifactory | build_artifacts
 public | build_artifacts_pk             | index | artifactory | build_artifacts
 public | build_artifacts_sha1_idx       | index | artifactory | build_artifacts
 public | build_dependencies_md5_idx     | index | artifactory | build_dependencies
 public | build_dependencies_module_idx  | index | artifactory | build_dependencies
 public | build_dependencies_pk          | index | artifactory | build_dependencies
 public | build_dependencies_sha1_idx    | index | artifactory | build_dependencies
 public | build_modules_build_id_idx     | index | artifactory | build_modules
 public | build_modules_pk               | index | artifactory | build_modules
 public | build_promotions_created_idx   | index | artifactory | build_promotions
 public | build_promotions_status_idx    | index | artifactory | build_promotions
 public | build_props_build_id_idx       | index | artifactory | build_props
 public | build_props_pk                 | index | artifactory | build_props
 public | build_props_prop_key_idx       | index | artifactory | build_props
 public | build_props_prop_value_idx     | index | artifactory | build_props
 public | builds_name_num_date_repo_idx  | index | artifactory | builds
 public | builds_pk                      | index | artifactory | builds
 public | bundle_blobs_pk                | index | artifactory | bundle_blobs
 public | bundle_files_node_id_idx       | index | artifactory | bundle_files
 public | bundle_id_bundle_files_idx     | index | artifactory | bundle_files
 public | bundle_id_idx                  | index | artifactory | bundle_blobs
 public | bundle_node_pk                 | index | artifactory | bundle_files
 public | bundle_pk                      | index | artifactory | artifact_bundles
 public | configs_pk                     | index | artifactory | configs
 public | db_properties_pk               | index | artifactory | db_properties
 public | distributed_locks_owner        | index | artifactory | distributed_locks
 public | distributed_locks_owner_thread | index | artifactory | distributed_locks
 public | identifier_pk                  | index | artifactory | migration_status
 public | indexed_archives_entries_pk    | index | artifactory | indexed_archives_entries
 public | indexed_archives_id_uq         | index | artifactory | indexed_archives
 public | indexed_archives_pk            | index | artifactory | indexed_archives
 public | indexed_entries_name_idx       | index | artifactory | indexed_archives_entries
 public | indexed_entries_path_idx       | index | artifactory | indexed_archives_entries
 public | jobs_index                     | index | artifactory | jobs
 public | jobs_pk                        | index | artifactory | jobs
 public | kid_pk                         | index | artifactory | master_key_status
 public | lock_key_idx                   | index | artifactory | distributed_locks
 public | locks_pk                       | index | artifactory | distributed_locks
 public | md_cnt_name_idx                | index | artifactory | md_contributors
 public | md_configs_config_name_idx     | index | artifactory | md_configs
 public | md_configs_pkey                | index | artifactory | md_configs
 public | md_contributors_pkey           | index | artifactory | md_contributors
 public | md_database_migrations_pkey    | index | artifactory | md_database_migrations
 public | md_fil_qualifiers_pkey         | index | artifactory | md_fil_qualifiers
 public | md_fil_targets_pkey            | index | artifactory | md_fil_targets
 public | md_fil_unique_idx              | index | artifactory | md_fil_qualifiers
 public | md_file_target_unique_idx      | index | artifactory | md_fil_targets
 public | md_files_md5_idx               | index | artifactory | md_files
 public | md_files_name_idx              | index | artifactory | md_files
 public | md_files_pkey                  | index | artifactory | md_files
 public | md_files_sha1_idx              | index | artifactory | md_files
 public | md_files_sha256_idx            | index | artifactory | md_files
 public | md_files_sha256_name_idx       | index | artifactory | md_files
 public | md_files_versions_pkey         | index | artifactory | md_files_versions
 public | md_flv_file_id_idx             | index | artifactory | md_files_versions
 public | md_flv_version_id_idx          | index | artifactory | md_files_versions
 public | md_licenses_name_idx           | index | artifactory | md_licenses
 public | md_licenses_pkey               | index | artifactory | md_licenses
 public | md_lock_pkey                   | index | artifactory | md_lock
 public | md_packages_lowercase_name_idx | index | artifactory | md_packages
 public | md_packages_name_idx           | index | artifactory | md_packages
 public | md_packages_pkey               | index | artifactory | md_packages
 public | md_packages_pkgid_idx          | index | artifactory | md_packages
 public | md_pkg_descriptions_pkey       | index | artifactory | md_pkg_descriptions
 public | md_pkg_info_sources_pkey       | index | artifactory | md_pkg_info_sources
 public | md_pkg_ins_package_id_idx      | index | artifactory | md_pkg_info_sources
 public | md_pkg_ins_source_id_idx       | index | artifactory | md_pkg_info_sources
 public | md_pkg_licenses_name_idx       | index | artifactory | md_pkg_licenses
 public | md_pkg_licenses_package_id_idx | index | artifactory | md_pkg_licenses
 public | md_pkg_licenses_pkey           | index | artifactory | md_pkg_licenses
 public | md_pkg_op_risk_pkey            | index | artifactory | md_pkg_op_risk
 public | md_pkg_qlf_package_id_idx      | index | artifactory | md_pkg_qualifiers
 public | md_pkg_qualifiers_pkey         | index | artifactory | md_pkg_qualifiers
 public | md_pkg_stats_pkey              | index | artifactory | md_pkg_stats
 public | md_pkg_tags_package_id_idx     | index | artifactory | md_pkg_tags
 public | md_pkg_tags_pkey               | index | artifactory | md_pkg_tags
 public | md_pkg_user_properties_pkey    | index | artifactory | md_pkg_user_properties
 public | md_pkg_usp_name_idx            | index | artifactory | md_pkg_user_properties
 public | md_pkg_usp_package_id_idx      | index | artifactory | md_pkg_user_properties
 public | md_pkg_vulns_sum_pkey          | index | artifactory | md_pkg_vulns_sum
 public | md_repos_name_idx              | index | artifactory | md_repos
 public | md_repos_pkey                  | index | artifactory | md_repos
 public | md_servers_node_unique_id_idx  | index | artifactory | md_servers
 public | md_servers_pkey                | index | artifactory | md_servers
 public | md_sources_name_idx            | index | artifactory | md_sources
 public | md_sources_pkey                | index | artifactory | md_sources
 public | md_task_batches_pkey           | index | artifactory | md_task_batches
 public | md_task_batches_progress_idx   | index | artifactory | md_task_batches
 public | md_tasks_pkey                  | index | artifactory | md_tasks
 public | md_tasks_progress_idx          | index | artifactory | md_tasks
 public | md_ver_cnt_contributor_id_idx  | index | artifactory | md_ver_contributors
 public | md_ver_cnt_version_id_idx      | index | artifactory | md_ver_contributors
 public | md_ver_contributors_pkey       | index | artifactory | md_ver_contributors
 public | md_ver_licenses_name_idx       | index | artifactory | md_ver_licenses
 public | md_ver_licenses_pkey           | index | artifactory | md_ver_licenses
 public | md_ver_licenses_version_id_idx | index | artifactory | md_ver_licenses
 public | md_ver_op_risk_pkey            | index | artifactory | md_ver_op_risk
 public | md_ver_qlf_name_idx            | index | artifactory | md_ver_qualifiers
 public | md_ver_qlf_version_id_idx      | index | artifactory | md_ver_qualifiers
 public | md_ver_qualifiers_pkey         | index | artifactory | md_ver_qualifiers
 public | md_ver_repos_lead_file_pth_idx | index | artifactory | md_ver_repos
 public | md_ver_repos_lead_hash_idx     | index | artifactory | md_ver_repos
 public | md_ver_repos_pkey              | index | artifactory | md_ver_repos
 public | md_ver_repos_repo_id_idx       | index | artifactory | md_ver_repos
 public | md_ver_repos_version_id_idx    | index | artifactory | md_ver_repos
 public | md_ver_stats_pkey              | index | artifactory | md_ver_stats
 public | md_ver_tags_pkey               | index | artifactory | md_ver_tags
 public | md_ver_tags_value_idx          | index | artifactory | md_ver_tags
 public | md_ver_tags_version_id_idx     | index | artifactory | md_ver_tags
 public | md_ver_user_properties_pkey    | index | artifactory | md_ver_user_properties
 public | md_ver_usp_name_idx            | index | artifactory | md_ver_user_properties
 public | md_ver_usp_version_id_idx      | index | artifactory | md_ver_user_properties
 public | md_ver_vulns_sum_pkey          | index | artifactory | md_ver_vulns_sum
 public | md_versions_id_created_idx     | index | artifactory | md_versions
 public | md_versions_id_deletion_idx    | index | artifactory | md_versions
 public | md_versions_lowercase_name_idx | index | artifactory | md_versions
 public | md_versions_name_idx           | index | artifactory | md_versions
 public | md_versions_pkey               | index | artifactory | md_versions
 public | md_versions_pkg_id_name_idx    | index | artifactory | md_versions
 public | md_versions_pkgid_ordinal_idx  | index | artifactory | md_versions
 public | module_props_module_id_idx     | index | artifactory | module_props
 public | module_props_pk                | index | artifactory | module_props
 public | module_props_prop_key_idx      | index | artifactory | module_props
 public | module_props_prop_value_idx    | index | artifactory | module_props
 public | name_ver_sta_date_typ_repo_idx | index | artifactory | artifact_bundles
 public | name_version_idx               | index | artifactory | artifact_bundles
 public | node_events_errors_idx         | index | artifactory | node_events_errors
 public | node_events_errors_pk          | index | artifactory | node_events_errors
 public | node_events_full_idx           | index | artifactory | node_events
 public | node_events_pk                 | index | artifactory | node_events
 public | node_events_tmp_event_id_idx   | index | artifactory | node_events_tmp
 public | node_events_tmp_idx            | index | artifactory | node_events_tmp
 public | node_meta_infos_pk             | index | artifactory | node_meta_infos
 public | node_props_node_prop_value_idx | index | artifactory | node_props
 public | node_props_pk                  | index | artifactory | node_props
 public | node_props_prop_key_value_idx  | index | artifactory | node_props
 public | node_props_prop_value_key_idx  | index | artifactory | node_props
 public | nodes_md5_actual_idx           | index | artifactory | nodes
 public | nodes_node_name_idx            | index | artifactory | nodes
 public | nodes_node_path_idx            | index | artifactory | nodes
 public | nodes_pk                       | index | artifactory | nodes
 public | nodes_repo_path_checksum       | index | artifactory | nodes
 public | nodes_repo_path_name_idx       | index | artifactory | nodes
 public | nodes_sha1_actual_idx          | index | artifactory | nodes
 public | nodes_sha256_idx               | index | artifactory | nodes
 public | operator_id_pk                 | index | artifactory | node_event_cursor
 public | priority_id_pk                 | index | artifactory | node_event_priorities
 public | repo_path_bundle_files_idx     | index | artifactory | bundle_files
 public | schema_change_log_pkey         | index | artifactory | schema_change_log
 public | stats_pk                       | index | artifactory | stats
 public | stats_remote_pk                | index | artifactory | stats_remote
 public | tasks_type_context_idx         | index | artifactory | tasks
 public | trusted_keys_alias             | index | artifactory | trusted_keys
 public | trusted_keys_pk                | index | artifactory | trusted_keys
 public | ui_session_attributes_ix1      | index | artifactory | ui_session_attributes
 public | ui_session_attributes_pk       | index | artifactory | ui_session_attributes
 public | ui_session_ix1                 | index | artifactory | ui_session
 public | ui_session_pk                  | index | artifactory | ui_session
 public | unique_ids_pk                  | index | artifactory | unique_ids
 public | unique_key                     | index | artifactory | master_key_status
 public | watches_node_id_idx            | index | artifactory | watches
 public | watches_pk                     | index | artifactory | watches
(220 rows)
```

### missing `artifactory_servers`
details are here https://gist.github.com/tichimura/0d27498bce45bb2d43253416e2d97d93

```
\d artifactory_servers
                         Table "public.artifactory_servers"
          Column          |          Type          | Collation | Nullable | Default
--------------------------+------------------------+-----------+----------+---------
 server_id                | character varying(128) |           | not null |
 start_time               | bigint                 |           | not null |
 context_url              | character varying(255) |           |          |
 membership_port          | integer                |           |          |
 server_state             | character varying(12)  |           | not null |
 server_role              | character varying(255) |           | not null |
 last_heartbeat           | bigint                 |           | not null |
 artifactory_version      | character varying(128) |           | not null |
 artifactory_revision     | integer                |           |          |
 artifactory_release      | bigint                 |           |          |
 artifactory_running_mode | character varying(12)  |           | not null |
 license_hash             | character varying(41)  |           | not null |
Indexes:
    "artifactory_servers_pk" PRIMARY KEY, btree (server_id)
```
