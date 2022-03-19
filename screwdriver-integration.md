
## Reference

  - Docs
    1. [Getting Started Developing](https://docs.screwdriver.cd/about/contributing/getting-started-developing#developing-locally)
  - Github
    1. [screwdriver-cd/ui](https://github.com/screwdriver-cd/ui)
    2. [screwdriver-cd/screwdriver](https://github.com/screwdriver-cd/screwdriver)
    3. [screwdriver-cd/store](https://github.com/screwdriver-cd/store)

## Setup for Mac OSX

- edit `/etc/hosts` 

  - add an entry in below

  ```
  127.0.0.1 sd.screwdriver.cd
  ```
  
- architecture

  ```
  % uname -m
  arm64  
  ```
  
  - you may need to run with x86_64 with Docker/Docker Desktop


## Screwdriver Setup

### setup node and npm (for ember-cli )


  https://github.com/ember-cli/ember-cli/blob/master/docs/node-support.md
   
  ```
  % node -v
  v14.19.0
  % npm -v
  6.14.16
  ```

### run in `ui`

 - run 'npm install'

   ```
   % npm install
   ```
  
 - install 'ember-cli'

   ```
   npm install -g ember-cli
   ```
   
 - edit `config/local.js`

    - slightly differed from 
    
    ```
    'use strict';

    const SDAPI_HOSTNAME = 'http://sd.screwdriver.cd:9001';
    const SDSTORE_HOSTNAME = 'http://sd.screwdriver.cd:9002';

    const APP_CONFIG = {
      SDAPI_HOSTNAME,
      SDSTORE_HOSTNAME
    };

    module.exports = APP_CONFIG;
    ```

### run in `screwdriver`

- run `npm install` at `screwdriver`

  ```
  % npm install
  ```

- To work with `postgresql` as a dialect, we need to add `pg`, `pg-hstore`, also `pg-native` just in case.

    - check this page [link](https://sequelize.org/master/manual/dialect-specific-things.html#postgresql)
      - [pg](https://www.npmjs.com/package/pg) 
      - [pg-hstore](https://www.npmjs.com/package/pg-hstore)
      - [pg-native](https://www.npmjs.com/package/pg-native)

- edit `config/local.yaml`

  just followed [docs](https://docs.screwdriver.cd/about/contributing/getting-started-developing#developing-locally)
  
  ```
  auth:
    jwtPrivateKey: |
        -----BEGIN RSA PRIVATE KEY-----        
        <NEED_TO_ADD>
        -----END RSA PRIVATE KEY-----    
    jwtPublicKey: |
        -----BEGIN PUBLIC KEY-----
        <NEED_TO_ADD>
        -----END PUBLIC KEY-----    

    httpd:
      # Port to listen on
      port: 9001

      # Host to listen on (set to localhost to only accept connections from this machine)
      host: 0.0.0.0

      uri: http://0.0.0.0:9001

    scms:
        github:
            plugin: github
            config:
                # github
                oauthClientId: <NEED_TO_ADD>
                oauthClientSecret: <NEED_TO_ADD>
                secret: <MAY_NEED_TO_ADD>

    ecosystem:
      # Externally routable URL for the User Interface
      ui: http://sd.screwdriver.cd:4200

      # Externally routable URL for the Artifact Store
      store: http://sd.screwdriver.cd:9002

      allowCors: ['http://sd.screwdriver.cd', 'http://sd.screwdriver.cd:9001']
  
    datastore:
      plugin: sequelize
      sequelize:
        dialect: postgres
        database: screwdriver
        username: yugabyte
        host: 127.0.0.1
        port: 5433
    ## if postgresql
    #    dialect: 'postgres'
    #    database: 'screwdriver'
    #    username: 'tichimura'
    #    password:
    #    host: 127.0.0.1
    #    port: 5432
    ## if sqlite
    #    dialect: sqlite
    #    storage: ./mw-data/storage.db

    ```

- Results in PostgreSQL
  
  ```
  % npm start

  > screwdriver-api@4.1.0 start /Users/tichimura/demodir/screwdriver/screwdriver
  > ./bin/server

  (sequelize) Warning: PostgresSQL does not support 'INTEGER' with LENGTH, UNSIGNED or ZEROFILL. Plain 'INTEGER' will be used instead.
  >> Check: http://www.postgresql.org/docs/9.4/static/datatype.html
  {"level":"info","message":"Datastore ddl sync enabled: true","timestamp":"2022-03-17T23:13:58.675Z"}
  {"level":"info","message":"Server running at http://0.0.0.0:9001","timestamp":"2022-03-17T23:13:59.347Z"}
  ```


  ```
  screwdriver=# \d
                    List of relations
   Schema |         Name         |   Type   |   Owner
  --------+----------------------+----------+-----------
   public | banners              | table    | tichimura
   public | banners_id_seq       | sequence | tichimura
   public | buildClusters        | table    | tichimura
   public | buildClusters_id_seq | sequence | tichimura
   public | builds               | table    | tichimura
   public | builds_id_seq        | sequence | tichimura
   public | collections          | table    | tichimura
   public | collections_id_seq   | sequence | tichimura
   public | commandTags          | table    | tichimura
   public | commandTags_id_seq   | sequence | tichimura
   public | commands             | table    | tichimura
   public | commands_id_seq      | sequence | tichimura
   public | events               | table    | tichimura
   public | events_id_seq        | sequence | tichimura
   public | jobs                 | table    | tichimura
   public | jobs_id_seq          | sequence | tichimura
   public | pipelines            | table    | tichimura
   public | pipelines_id_seq     | sequence | tichimura
   public | secrets              | table    | tichimura
   public | secrets_id_seq       | sequence | tichimura
   public | steps                | table    | tichimura
   public | steps_id_seq         | sequence | tichimura
   public | templateTags         | table    | tichimura
   public | templateTags_id_seq  | sequence | tichimura
   public | templates            | table    | tichimura
   public | templates_id_seq     | sequence | tichimura
   public | tokens               | table    | tichimura
   public | tokens_id_seq        | sequence | tichimura
   public | triggers             | table    | tichimura
   public | triggers_id_seq      | sequence | tichimura
   public | users                | table    | tichimura
   public | users_id_seq         | sequence | tichimura
  (32 rows)

  ```


- Results in PostgreSQL

    ```
    % npm start

    > screwdriver-api@4.1.0 start /Users/tichimura/demodir/screwdriver/screwdriver
    > ./bin/server

    (sequelize) Warning: PostgresSQL does not support 'INTEGER' with LENGTH, UNSIGNED or ZEROFILL. Plain 'INTEGER' will be used instead.
    >> Check: http://www.postgresql.org/docs/9.4/static/datatype.html
    {"level":"info","message":"Datastore ddl sync enabled: true","timestamp":"2022-03-17T23:51:23.221Z"}
    {"level":"info","message":"Server running at http://0.0.0.0:9001","timestamp":"2022-03-17T23:58:56.180Z"}
    ```


    ```
    screwdriver=# \d
                      List of relations
     Schema |         Name         |   Type   |  Owner
    --------+----------------------+----------+----------
     public | banners              | table    | yugabyte
     public | banners_id_seq       | sequence | yugabyte
     public | buildClusters        | table    | yugabyte
     public | buildClusters_id_seq | sequence | yugabyte
     public | builds               | table    | yugabyte
     public | builds_id_seq        | sequence | yugabyte
     public | collections          | table    | yugabyte
     public | collections_id_seq   | sequence | yugabyte
     public | commandTags          | table    | yugabyte
     public | commandTags_id_seq   | sequence | yugabyte
     public | commands             | table    | yugabyte
     public | commands_id_seq      | sequence | yugabyte
     public | events               | table    | yugabyte
     public | events_id_seq        | sequence | yugabyte
     public | jobs                 | table    | yugabyte
     public | jobs_id_seq          | sequence | yugabyte
     public | pipelines            | table    | yugabyte
     public | pipelines_id_seq     | sequence | yugabyte
     public | secrets              | table    | yugabyte
     public | secrets_id_seq       | sequence | yugabyte
     public | steps                | table    | yugabyte
     public | steps_id_seq         | sequence | yugabyte
     public | templateTags         | table    | yugabyte
     public | templateTags_id_seq  | sequence | yugabyte
     public | templates            | table    | yugabyte
     public | templates_id_seq     | sequence | yugabyte
     public | tokens               | table    | yugabyte
     public | tokens_id_seq        | sequence | yugabyte
     public | triggers             | table    | yugabyte
     public | triggers_id_seq      | sequence | yugabyte
     public | users                | table    | yugabyte
     public | users_id_seq         | sequence | yugabyte
    (32 rows)

    screwdriver=# \di
                                       List of relations
     Schema |                    Name                    | Type  |  Owner   |     Table
    --------+--------------------------------------------+-------+----------+---------------
     public | banners_is_active                          | index | yugabyte | banners
     public | banners_message_createTime_type_key        | index | yugabyte | banners
     public | banners_pkey                               | index | yugabyte | banners
     public | buildClusters_name_scmContext_key          | index | yugabyte | buildClusters
     public | buildClusters_pkey                         | index | yugabyte | buildClusters
     public | build_clusters_name                        | index | yugabyte | buildClusters
     public | builds_eventId_jobId_key                   | index | yugabyte | builds
     public | builds_event_id_create_time                | index | yugabyte | builds
     public | builds_job_id                              | index | yugabyte | builds
     public | builds_parent_build_id                     | index | yugabyte | builds
     public | builds_pkey                                | index | yugabyte | builds
     public | builds_template_id                         | index | yugabyte | builds
     public | collections_pkey                           | index | yugabyte | collections
     public | collections_userId_name_key                | index | yugabyte | collections
     public | collections_user_id                        | index | yugabyte | collections
     public | commandTags_namespace_name_tag_key         | index | yugabyte | commandTags
     public | commandTags_pkey                           | index | yugabyte | commandTags
     public | command_tags_name                          | index | yugabyte | commandTags
     public | command_tags_namespace                     | index | yugabyte | commandTags
     public | command_tags_tag                           | index | yugabyte | commandTags
     public | commands_name                              | index | yugabyte | commands
     public | commands_namespace                         | index | yugabyte | commands
     public | commands_namespace_version_name_key        | index | yugabyte | commands
     public | commands_pkey                              | index | yugabyte | commands
     public | events_createTime_pipelineId_sha_key       | index | yugabyte | events
     public | events_create_time_pipeline_id             | index | yugabyte | events
     public | events_group_event_id                      | index | yugabyte | events
     public | events_parent_event_id                     | index | yugabyte | events
     public | events_pipeline_id                         | index | yugabyte | events
     public | events_pkey                                | index | yugabyte | events
     public | events_type                                | index | yugabyte | events
     public | jobs_name_pipelineId_key                   | index | yugabyte | jobs
     public | jobs_pipeline_id_state                     | index | yugabyte | jobs
     public | jobs_pkey                                  | index | yugabyte | jobs
     public | jobs_state                                 | index | yugabyte | jobs
     public | jobs_template_id                           | index | yugabyte | jobs
     public | pipelines_pkey                             | index | yugabyte | pipelines
     public | pipelines_scmUri_key                       | index | yugabyte | pipelines
     public | pipelines_scm_uri                          | index | yugabyte | pipelines
     public | pipelines_subscribed_scm_urls_with_actions | index | yugabyte | pipelines
     public | secrets_pipelineId_name_key                | index | yugabyte | secrets
     public | secrets_pipeline_id                        | index | yugabyte | secrets
     public | secrets_pkey                               | index | yugabyte | secrets
     public | steps_buildId_name_key                     | index | yugabyte | steps
     public | steps_build_id                             | index | yugabyte | steps
     public | steps_name                                 | index | yugabyte | steps
     public | steps_pkey                                 | index | yugabyte | steps
     public | templateTags_namespace_name_tag_key        | index | yugabyte | templateTags
     public | templateTags_pkey                          | index | yugabyte | templateTags
     public | template_tags_name                         | index | yugabyte | templateTags
     public | template_tags_namespace                    | index | yugabyte | templateTags
     public | template_tags_tag                          | index | yugabyte | templateTags
     public | templates_name                             | index | yugabyte | templates
     public | templates_name_version_namespace_key       | index | yugabyte | templates
     public | templates_namespace                        | index | yugabyte | templates
     public | templates_pkey                             | index | yugabyte | templates
     public | tokens_hash                                | index | yugabyte | tokens
     public | tokens_hash_key                            | index | yugabyte | tokens
     public | tokens_pipeline_id                         | index | yugabyte | tokens
     public | tokens_pkey                                | index | yugabyte | tokens
     public | tokens_user_id                             | index | yugabyte | tokens
     public | triggers_dest                              | index | yugabyte | triggers
     public | triggers_pkey                              | index | yugabyte | triggers
     public | triggers_src                               | index | yugabyte | triggers
     public | triggers_src_dest_key                      | index | yugabyte | triggers
     public | users_pkey                                 | index | yugabyte | users
     public | users_scm_context                          | index | yugabyte | users
     public | users_username                             | index | yugabyte | users
     public | users_username_scmContext_key              | index | yugabyte | users
    (69 rows)
    ```


### run in `store`

```
% cd store
tichimura@ store % npm install && npm run start
npm WARN deprecated topo@3.0.3: This module has moved and is now available at @hapi/topo. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
npm WARN deprecated hoek@6.1.3: This module has moved and is now available at @hapi/hoek. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
npm WARN deprecated querystring@0.2.0: The querystring API is considered Legacy. new code should use the URLSearchParams API instead.
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated hoek@5.0.3: This version has been deprecated in accordance with the hapi support policy (hapi.im/support). Please upgrade to the latest version to get the best features, bug fixes, and security patches. If you are unable to upgrade at this time, paid support is available for older versions (hapi.im/commercial).
npm WARN deprecated boom@7.3.0: This module has moved and is now available at @hapi/boom. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
npm WARN deprecated catbox@10.0.6: This module has moved and is now available at @hapi/catbox. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
npm WARN deprecated catbox-s3@4.0.0: this package is no longer maintained
npm WARN deprecated uuid@3.3.2: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated joi@14.3.1: This module has moved and is now available at @hapi/joi. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
npm WARN deprecated core-js@2.6.12: core-js@<3.4 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Please, upgrade your dependencies to the actual version of core-js.

added 519 packages, and audited 520 packages in 49s

70 packages are looking for funding
  run `npm fund` for details

9 moderate severity vulnerabilities

To address issues that do not require attention, run:
  npm audit fix

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.

> screwdriver-store@4.0.0 start
> ./bin/server

{"level":"info","message":"Server running at http://localhost","timestamp":"2022-03-16T06:08:48.906Z"}
```

## QuickStart

- fork, and clone the sample apps

  ```
  % git clone https://github.com/tichimura/quickstart-generic.git
  Cloning into 'quickstart-generic'...
  remote: Enumerating objects: 31, done.
  remote: Total 31 (delta 0), reused 0 (delta 0), pack-reused 31
  Receiving objects: 100% (31/31), 19.35 KiB | 6.45 MiB/s, done.
  Resolving deltas: 100% (12/12), done.
  tichimura@ screwdriver % cd quickstart-generic
  tichimura@ quickstart-generic % ls
  LICENSE			Makefile		README.md		my_script.sh		screwdriver.yaml  
  ```
  
  - edit `screwdriver.yaml`

  ```YAML
  # Shared definition block
  # This is where you would define any attributes that all your jobs will
  # inherit. In our example, we state that all our Jobs will use the same Docker
  # container for building in.
  shared:
    # Docker image to use as the desired build container. This typically takes the
    # form of "repo_name". Alternatively, you can define the image as
    # "repo_name:tag_label".
    #
    # (Source: https://hub.docker.com/r/library/buildpack-deps/)
    image: buildpack-deps

  # Job definition block
  # "main" is a default job that all pipelines have
  jobs:
    # Jobs are defined by name.
    # All pipelines have "main" implicitly defined. The definitions in your
    # screwdriver.yaml file will override the implied defaults.
    main:
      # Requires is a single job name or array of job names that will trigger the job to run.
      # Jobs defined with "requires: ~pr" are started by pull-request events.
      # Jobs defined with "requires: ~commit" are started by push events.
      # Jobs defined with "requires: ~sd@123:main" are started by job "main" from pipeline "123".
      # Jobs defined with "requires: main" are started after "main" is done.
      # Jobs defined with "requires: [deploy-west, deploy-east] are started after "deploy-west" and "deploy-east" are both done running successfully.
      requires: [~pr, ~commit]
      # Steps is the list of commands to execute.
      steps:
        # Each step takes the form "step_name: command_to_run".
        # The "step_name" is a convenient label to reference it by. The
        # "command_to_run" is the single command that is executed during this
        # step. Environment variables will be passed between steps, within
        # the same job (as shown below).
        - export: export GREETING="Hello, world!"
        - hello: echo $GREETING
        # Metadata is a structured key/value storage of relevant information about a build.
        # Metadata will be shared with subsequent builds in the same workflow.
        # You can set any key using the command "meta set <key> <value>".
        - set-metadata: meta set example.coverage 99.95
    # We define another Job called "second_job". In this Job, we intend on running
    # a different set of commands.
    second_job:
      requires: main
      steps:
        # The "make_target" step calls a Makefile target to perform some set of
        # actions. This is incredibly useful when you need to perform a multi-line
        # command.
        - make_target: make greetings
        # You can get metadata that was set using the command "meta get <key>".
        - get-metadata: meta get example
        # The "run_arbitrary_script" executes a script. This is an alternative to
        # a Makefile target where you want to run a series of commands related to
        # this step
        - run_arbitrary_script: ./my_script.sh
  ```
  
  ## Quickstart
  
  <img width="1487" alt="image" src="https://user-images.githubusercontent.com/1793451/159113673-5291bd6f-1b61-4177-8cae-b11ea4088aff.png">
  
  - [INFO]the console log at `screwdriver` is like below
  
  ```
  220319/082336.576, (1647678216576:Tomohiros-MacBook-Pro.local:48333:l0xeswh1:10000) [response,api,auth,context] http://sd.screwdriver.cd:9001: get /v4/auth/contexts {} 200 (6ms)
  220319/082336.661, (1647678216661:Tomohiros-MacBook-Pro.local:48333:l0xeswh1:10001) [response] http://sd.screwdriver.cd:9001: options /v4/banners {} 204 (1ms)
  {"level":"info","message":"Executed (default): SELECT \"id\", \"message\", \"isActive\", \"createTime\", \"createdBy\", \"type\" FROM \"banners\" AS \"banners\" ORDER BY \"banners\".\"id\" DESC;","timestamp":"2022-03-19T08:23:37.159Z"}
  220319/082336.662, (1647678216662:Tomohiros-MacBook-Pro.local:48333:l0xeswh1:10002) [response,api,banners] http://sd.screwdriver.cd:9001: get /v4/banners {} 200 (498ms)  
  ```

  - create new pipeline

  <img width="1487" alt="image" src="https://user-images.githubusercontent.com/1793451/159113878-3c0a3272-7f01-4679-91c7-3970b893f00c.png">


  <img width="1487" alt="image" src="https://user-images.githubusercontent.com/1793451/159113929-86252e42-5061-4a8d-b788-754a11ea774d.png">
  
    this time, not choosing the `I will create the screwdriver.yaml  later`. 
  
  - now it moves to Pipeline page automatically.

  <img width="1487" alt="image" src="https://user-images.githubusercontent.com/1793451/159113989-1710e801-ff15-43bb-abda-bed6125f9c81.png">
  
  - click `Start` and see the console log

  <img width="1487" alt="image" src="https://user-images.githubusercontent.com/1793451/159114052-a3c92abe-e667-4553-bc39-4c678602553f.png">

  - error has been shown

  ```
  {"level":"error","message":"Breaker with function function () { [native code] } was tripped on Sat, 19 Mar 2022 08:39:32 GMT","timestamp":"2022-03-19T08:39:32.421Z"}
  {"level":"info","message":"Getting errors with [{\"url\":\"https://kubernetes.default/api/v1/namespaces/default/pods\",\"method\":\"POST\",\"json\":{\"apiVersion\":\"v1\",\"kind\":\"Pod\",\"metadata\":{\"name\":\"101-ye528\",\"labels\":{\"app\":\"screwdriver\",\"tier\":\"builds\",\"sdbuild\":\"101\"}},\"spec\":{\"serviceAccountName\":\"default\",\"automountServiceAccountToken\":false,\"terminationGracePeriodSeconds\":30,\"restartPolicy\":\"Never\",\"dnsPolicy\":\"ClusterFirst\",\"containers\":[{\"name\":\"101\",\"image\":\"buildpack-deps\",\"imagePullPolicy\":\"Always\",\"securityContext\":{\"privileged\":false},\"resources\":{\"limits\":{\"cpu\":\"2000m\",\"memory\":\"2Gi\"}},\"env\":[{\"name\":\"SD_HAB_ENABLED\",\"value\":\"true\"},{\"name\":\"SD_RUNTIME_CLASS\",\"value\":null},{\"name\":\"SD_PUSHGATEWAY_URL\",\"value\":null},{\"name\":\"SD_TERMINATION_GRACE_PERIOD_SECONDS\",\"value\":\"30\"},{\"name\":\"CONTAINER_IMAGE\",\"value\":\"buildpack-deps\"},{\"name\":\"SD_PIPELINE_ID\",\"value\":\"1\"},{\"name\":\"SD_BUILD_PREFIX\",\"value\":\"\"},{\"name\":\"NODE_ID\",\"valueFrom\":{\"fieldRef\":{\"fieldPath\":\"spec.nodeName\"}}},{\"name\":\"SD_BASE_COMMAND_PATH\",\"value\":\"/sd/commands/\"},{\"name\":\"SD_TEMP\",\"value\":\"/opt/sd_tmp\"}],\"command\":[\"/opt/sd/launcher_entrypoint.sh\"],\"args\":[\"/opt/sd/run.sh \\\"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6MTAxLCJzY21Db250ZXh0IjoiZ2l0aHViOmdpdGh1Yi5jb20iLCJzY29wZSI6WyJ0ZW1wb3JhbCJdLCJpc1BSIjpmYWxzZSwiam9iSWQiOjEsImV2ZW50SWQiOjEwMSwicGlwZWxpbmVJZCI6MSwiaWF0IjoxNjQ3Njc5MTcyLCJleHAiOjE2NDc3MjIzNzIsImp0aSI6IjM1MzVhZmRjLTI1NjQtNGVjZC04OGNlLTAxNjg1NGI4ZTdjMiJ9.Td2hbLSs9C5OeSazu5NJ1Zm6QyVEcLQPIyRaZGsfItXN9_A_xYtEc1vKbe7a4HHzDcsT_qgU0rrVcQgG1dItcgydVnudFg4F-LQY0ZPcCnYn5Bh4brIV3e8ZdBleyPzOlPePYHub502AlE64waX8UpVhgGXN7J7_T9aeUIz90EDmOopc4WdYfDlGIoCFTXjxl67XnhSrdFere6IsZMuMc6Y_Sq_TpEl9otlPx5nW2Bv81BTOKbz_pvGvXIHq5ryiMvMeALLPoHo8wciVSfu3fVyVDQxQPjBgL5Meb6li_-LZDtj9nUNiFWR-hwvjDBKQTA71UQ8xNFs_39yBiTyVtA\\\" \\\"http://sd.screwdriver.cd:9001\\\" \\\"http://sd.screwdriver.cd:9002\\\" \\\"90\\\" \\\"101\\\" \\\"http://sd.screwdriver.cd:4200\\\"\\n\"],\"volumeMounts\":[{\"name\":\"podinfo\",\"mountPath\":\"/etc/podinfo\",\"readOnly\":true},{\"mountPath\":\"/opt/sd\",\"name\":\"screwdriver\",\"readOnly\":true},{\"mountPath\":\"/opt/sd_tmp\",\"name\":\"sdtemp\"},{\"mountPath\":\"/workspace\",\"name\":\"workspace\"}]}],\"initContainers\":[{\"name\":\"launcher-101\",\"image\":\"screwdrivercd/launcher:stable\",\"command\":[\"/bin/sh\",\"-c\",\"echo launcher_start_ts:`date \\\"+%s\\\"` > /workspace/metrics && if ! [ -f /opt/launcher/launch ]; then TEMP_DIR=`mktemp -d -p /opt/launcher` && cp -a /opt/sd/* $TEMP_DIR && mkdir -p $TEMP_DIR/hab && cp -a /hab/* $TEMP_DIR/hab && mv $TEMP_DIR/* /opt/launcher && rm -rf $TEMP_DIR || true; else ls /opt/launcher; fi; echo launcher_end_ts:`date \\\"+%s\\\"` >> /workspace/metrics\"],\"volumeMounts\":[{\"mountPath\":\"/opt/launcher\",\"name\":\"screwdriver\"},{\"mountPath\":\"/workspace\",\"name\":\"workspace\"}]}],\"volumes\":[{\"name\":\"podinfo\",\"downwardAPI\":{\"items\":[{\"path\":\"labels\",\"fieldRef\":{\"fieldPath\":\"metadata.labels\"}},{\"path\":\"annotations\",\"fieldRef\":{\"fieldPath\":\"metadata.annotations\"}}]}},{\"name\":\"screwdriver\",\"type\":\"DirectoryOrCreate\",\"hostPath\":{\"path\":\"/opt/screwdriver/sdlauncher/stable\"}},{\"name\":\"sdtemp\",\"type\":\"DirectoryOrCreate\",\"hostPath\":{\"path\":\"/opt/screwdriver/tmp_101\"}},{\"name\":\"workspace\",\"emptyDir\":{}}]}},\"headers\":{\"Authorization\":\"Bearer \"},\"https\":{\"rejectUnauthorized\":false}}]: Error: 500 Reason \"Internal server error\"","timestamp":"2022-03-19T08:39:32.421Z"}
  {"level":"error","message":"Failed to run pod for build id:101: 500 Reason \"Internal server error\"","timestamp":"2022-03-19T08:39:32.423Z"}
  220319/083932.423, (1647679168041:Tomohiros-MacBook-Pro.local:48333:l0xeswh1:10205) [request,server,error] data: Error: 500 Reason "Internal server error"
      at throwError (/Users/tichimura/demodir/screwdriver/screwdriver/node_modules/screwdriver-request/index.js:14:17)
      at /Users/tichimura/demodir/screwdriver/screwdriver/node_modules/screwdriver-request/index.js:56:28
      at runMicrotasks (<anonymous>)
      at processTicksAndRejections (internal/process/task_queues.js:95:5)
  220319/083928.041, (1647679168041:Tomohiros-MacBook-Pro.local:48333:l0xeswh1:10205) [response,api,events] http://sd.screwdriver.cd:9001: post /v4/events {} 500 (4382ms)  
  ```

  ```
