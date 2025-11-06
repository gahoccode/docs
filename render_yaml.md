# Render.yaml Reference for Python Projects

## 1. Hello World Minimal Example

```yaml
services:
  - type: web
    name: my-python-app
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
```

***

## 2. Complete Schema Reference

### Root-Level Keys

**databases** | `list` | optional | default: `[]`  
List of Postgres database instances.  
Example: `databases: [{name: mydb, plan: free}]`  
⚠️ Databases expire after 30 days on free plan.

**envVarGroups** | `list` | optional | default: `[]`  
Shared environment variable groups.  
Example: `envVarGroups: [{name: shared, envVars: [{key: API_KEY, value: xyz}]}]`

**previewsEnabled** | `bool` | optional | default: `false`  
Enable preview environments for PRs.  
Allowed: `true | false`  
Example: `previewsEnabled: true`

**previewsExpireAfterDays** | `int` | optional | default: `never`  
Days to retain idle preview environments.  
Example: `previewsExpireAfterDays: 7`

**projects** | `list` | optional | default: `[]`  
Define projects and environments (advanced).  
Example: `projects: [{name: myproject, environments: [...]}]`

**services** | `list` | required  
List of non-Postgres services (web, worker, cron, static, private, keyvalue).  
Example: `services: [{type: web, name: api, ...}]`

**ungrouped** | `map` | optional  
Resources not belonging to any environment.  
Example: `ungrouped: {services: [...], databases: [...]}`

***

### Service Keys (services[])

**autoDeploy** | `enum` | optional | default: `true`  
Control auto-deploy on git push.  
Allowed: `true | false`  
Example: `autoDeploy: false`  
⚠️ Replaces deprecated `autoDeployEnabled`.

**branch** | `string` | optional | default: `repo default branch`  
Git branch to track.  
Example: `branch: main`  
⚠️ Don't set for preview envs or PR branch won't be used.

**buildCommand** | `string` | optional  
Command to build your service.  
Example: `buildCommand: pip install -r requirements.txt`  
💡 Consumes billable pipeline minutes.

**buildFilter** | `map` | optional  
Paths to include/ignore when triggering builds (glob syntax).  
Example: `buildFilter: {paths: [api/**], ignoredPaths: [*.md]}`  
💡 Essential for monorepos.

**disk** | `map` | optional  
Attach persistent disk (can't scale if disk attached).  
Example: `disk: {name: data, mountPath: /var/data, sizeGB: 10}`  
⚠️ Can increase size but never decrease.

**dockerCommand** | `string` | optional  
Override CMD for Docker-based services.  
Example: `dockerCommand: python app.py`

**dockerContext** | `string` | optional | default: `repo root`  
Docker build context path.  
Example: `dockerContext: ./services/api`

**dockerfilePath** | `string` | optional | default: `./Dockerfile`  
Path to Dockerfile.  
Example: `dockerfilePath: ./docker/Dockerfile.prod`

**domains** | `list[string]` | optional  
Custom domains (web services only).  
Example: `domains: [example.com, www.example.com]`  
💡 Render auto-adds www subdomain for root domains.

**env** | `enum` | required (for non-docker)  
Runtime environment.  
Allowed: `python | node | ruby | go | rust | elixir | docker | image | static`  
Example: `env: python`  
⚠️ Cannot modify after creation.

**envVars** | `list` | optional | default: `[]`  
Environment variables.  
Example: `envVars: [{key: DEBUG, value: "false"}]`

**healthCheckPath** | `string` | optional  
Endpoint for health checks (web services only).  
Example: `healthCheckPath: /health`  
💡 Must return 2xx/3xx; 5s timeout; enables zero-downtime deploys.

**image** | `map` | optional  
Pull prebuilt Docker image (`runtime: image`).  
Example: `image: {url: myrepo/app:latest, registryCredential: mycred}`

**imagePullCredentials** | `string` | optional  
Registry credential name for private images.  
Example: `imagePullCredentials: dockerhub-cred`

**maxShutdownDelaySeconds** | `int` | optional | default: `30`  
Max graceful shutdown time (30-300 seconds).  
Example: `maxShutdownDelaySeconds: 120`

**name** | `string` | required  
Service identifier.  
Example: `name: api-server`  
⚠️ Cannot modify after creation.

**numInstances** | `int` | optional | default: `1`  
Fixed instance count for manual scaling.  
Example: `numInstances: 3`

**plan** | `enum` | optional | default: `starter`  
Instance type.  
Allowed: `free | starter | starter_plus | standard | standard_plus | pro | pro_plus | pro_max | pro_ultra | custom`  
Example: `plan: starter`  
⚠️ Free expires after 30 days.

**preDeployCommand** | `string` | optional  
Command before each deploy (migrations, etc).  
Example: `preDeployCommand: python manage.py migrate`  
💡 Runs after build, before new instances start.

**previewPlan** | `enum` | optional | default: same as `plan`  
Instance type for preview environments.  
Example: `previewPlan: starter`

**previewsEnabled** | `enum` | optional | default: `false`  
Enable PR previews for this service.  
Allowed: `true | false | manual`  
Example: `previewsEnabled: true`

**region** | `enum` | optional | default: `oregon`  
Deployment region.  
Allowed: `oregon | ohio | virginia | frankfurt | singapore`  
Example: `region: frankfurt`  
⚠️ Cannot modify after creation.

**repo** | `string` | optional  
Git repo URL (omit to use Blueprint repo).  
Example: `repo: https://github.com/user/repo.git`

**rootDir** | `string` | optional | default: `repo root`  
Service root directory in repo.  
Example: `rootDir: services/api`  
💡 All paths relative to this after set.

**scaling** | `map` | optional  
Autoscaling config (Professional workspace required).  
Example: `scaling: {minInstances: 1, maxInstances: 10, targetCPUPercent: 60, targetMemoryPercent: 70}`  
⚠️ Can't scale services with disks.

**schedule** | `string` | required (for cron jobs)  
Cron expression (cron jobs only).  
Example: `schedule: "0 2 * * *"`  
💡 Uses UTC; standard cron syntax.

**startCommand** | `string` | required  
Command to start service.  
Example: `startCommand: gunicorn app:app --bind 0.0.0.0:$PORT`

**type** | `enum` | required  
Service type.  
Allowed: `web | pserv | worker | cron | static | keyvalue`  
Example: `type: web`  
⚠️ Cannot modify after creation. `keyvalue` is Redis-compatible.

***

### Database Keys (databases[])

**databaseName** | `string` | optional | default: auto-generated  
Database name in Postgres instance.  
Example: `databaseName: myapp_db`  
⚠️ Cannot modify after creation.

**databaseUser** | `string` | optional | default: auto-generated  
Postgres username.  
Example: `databaseUser: admin`  
⚠️ Cannot modify after creation.

**ipAllowList** | `list` | optional  
IP ranges allowed to connect (CIDR notation).  
Example: `ipAllowList: [{cidr: "0.0.0.0/0", description: "all"}]`  
💡 Empty list blocks all external connections.

**name** | `string` | required  
Database identifier.  
Example: `name: production-db`  
⚠️ Cannot modify after creation.

**plan** | `enum` | optional | default: `starter`  
Postgres instance type.  
Allowed: `free | starter | standard | pro | pro_plus | basic | standard_ha | pro_ha`  
Example: `plan: free`

**postgresMajorVersion** | `string` | optional | default: `"17"`  
Postgres major version.  
Example: `postgresMajorVersion: "16"`  
⚠️ Cannot modify after creation.

**region** | `enum` | optional | default: `oregon`  
Database region (same as services).  
Example: `region: oregon`  
⚠️ Cannot modify after creation.

***

### Environment Variable Keys (envVars[])

**fromDatabase** | `map` | optional  
Reference Postgres property.  
Example: `fromDatabase: {name: mydb, property: connectionString}`  
Properties: `connectionString | user | password | databaseName`

**fromGroup** | `string` | optional  
Reference env group.  
Example: `fromGroup: shared-vars`

**fromService** | `map` | optional  
Reference service property.  
Example: `fromService: {type: web, name: api, property: host}`  
Properties: `host | port | hostport | connectionString`

**generateValue** | `bool` | optional  
Auto-generate base64 secret.  
Example: `generateValue: true`  
💡 Generates 256-bit secret.

**key** | `string` | required  
Variable name.  
Example: `key: DATABASE_URL`

**previewValue** | `string` | optional  
Override for preview environments.  
Example: `previewValue: "debug mode"`  
⚠️ Cannot use with `sync: false`.

**sync** | `bool` | optional | default: `true`  
Whether to sync value (false = prompt during creation).  
Example: `sync: false`  
⚠️ Prompted only once; not in previews or env groups.

**value** | `string` | optional  
Variable value.  
Example: `value: "production"`  
⚠️ Don't commit secrets; use `sync: false`.

***

### Disk Keys (disk)

**mountPath** | `string` | required  
Where to mount disk.  
Example: `mountPath: /var/data`

**name** | `string` | required  
Disk identifier.  
Example: `name: app-storage`

**sizeGB** | `int` | required  
Disk size in GB.  
Example: `sizeGB: 20`  
⚠️ Can increase but never decrease.

***

### Scaling Keys (scaling)

**maxInstances** | `int` | required  
Maximum instance count.  
Example: `maxInstances: 10`

**minInstances** | `int` | required  
Minimum instance count.  
Example: `minInstances: 1`

**targetCPUPercent** | `int` | optional  
Target CPU utilization (triggers scale).  
Example: `targetCPUPercent: 60`

**targetMemoryPercent** | `int` | optional  
Target memory utilization (triggers scale).  
Example: `targetMemoryPercent: 70`  
💡 Need at least one target; uses larger if both set.

***

## 3. Real-World Recipe Snippets

### 3.1 Background Worker

```yaml
services:
  - type: worker
    name: celery-worker
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: celery -A tasks worker
    envVars:
      - key: REDIS_URL
        fromService: {type: keyvalue, name: cache, property: connectionString}
```

### 3.2 Cron Job

```yaml
services:
  - type: cron
    name: daily-report
    env: python
    schedule: "0 2 * * *"
    buildCommand: pip install -r requirements.txt
    startCommand: python generate_report.py
```

### 3.3 Private Service

```yaml
services:
  - type: pserv
    name: internal-api
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn internal:app
    plan: starter
```

### 3.4 Autoscaling Web Service

```yaml
services:
  - type: web
    name: api
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
    scaling:
      minInstances: 2
      maxInstances: 10
      targetCPUPercent: 70
      targetMemoryPercent: 80
```

### 3.5 Monorepo with Build Filter

```yaml
services:
  - type: web
    name: api-service
    env: python
    rootDir: services/api
    buildFilter:
      paths: [services/api/**, shared/**]
      ignoredPaths: ["**.md", tests/**]
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
```

### 3.6 Persistent Disk + Database

```yaml
databases:
  - name: maindb
    plan: starter
    region: oregon

services:
  - type: web
    name: django-app
    env: python
    disk:
      name: media
      mountPath: /var/media
      sizeGB: 10
    buildCommand: pip install -r requirements.txt
    preDeployCommand: python manage.py migrate
    startCommand: gunicorn mysite.wsgi:application
    envVars:
      - key: DATABASE_URL
        fromDatabase: {name: maindb, property: connectionString}
      - key: SECRET_KEY
        generateValue: true
```

### 3.7 Docker with Health Checks

```yaml
services:
  - type: web
    name: fastapi-app
    env: docker
    dockerfilePath: ./Dockerfile
    dockerContext: .
    healthCheckPath: /health
    maxShutdownDelaySeconds: 60
    envVars:
      - key: ENVIRONMENT
        value: production
```

### 3.8 Environment Groups

```yaml
envVarGroups:
  - name: shared-config
    envVars:
      - key: LOG_LEVEL
        value: info
      - key: REGION
        value: us-west

services:
  - type: web
    name: app
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
    envVars:
      - fromGroup: shared-config
      - key: APP_ENV
        value: production
        previewValue: staging
```

### 3.9 Preview Environments

```yaml
previewsEnabled: true
previewsExpireAfterDays: 3

services:
  - type: web
    name: web-app
    env: python
    plan: standard
    previewPlan: starter
    previewsEnabled: true
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
    envVars:
      - key: DEBUG
        value: "false"
        previewValue: "true"
```

### 3.10 Multi-Service with Redis

```yaml
services:
  - type: keyvalue
    name: cache
    plan: free
    ipAllowList:
      - cidr: "0.0.0.0/0"
        description: allow all

  - type: web
    name: api
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn app:app
    envVars:
      - key: REDIS_URL
        fromService: {type: keyvalue, name: cache, property: connectionString}
      
  - type: worker
    name: task-processor
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: celery -A tasks worker
    envVars:
      - key: REDIS_URL
        fromService: {type: keyvalue, name: cache, property: connectionString}
```

***

## 4. Footnotes

### Official Documentation
- Blueprint Spec: https://render.com/docs/blueprint-spec[1]
- Infrastructure as Code: https://render.com/docs/infrastructure-as-code[2]
- Changelog: https://render.com/changelog[3]

### Common Validation Errors

| Error Message | Cause | Fix |
|--------------|-------|-----|
| `cannot simultaneously specify fields value and sync` | Used `value` with `sync: false` | Remove `value` when `sync: false` |
| `services[N]: required field missing` | Missing `type`, `name`, or `env` | Add all required service fields |
| `environment group not found` | Referenced non-existent env group | Create group in `envVarGroups` first |
| `invalid region` | Typo in region name | Use: oregon, ohio, virginia, frankfurt, singapore |
| `cannot modify runtime after creation` | Changed `env` field | Delete and recreate service |
| `disk not supported for scaled services` | Using `disk` with `scaling` | Choose one: disk OR scaling |
| `healthCheckPath invalid` | Path doesn't start with `/` | Use absolute path like `/health` |
| `plan not available for service type` | Wrong plan for service | Check allowed plans per type |
| `previewValue without value` | Only `previewValue` set | Add `value` field |
| `invalid cron expression` | Bad `schedule` syntax | Use valid cron: `"0 2 * * *"` |

Sources
[1] Blueprint YAML Reference https://render.com/docs/blueprint-spec
[2] Render Blueprints (IaC) https://render.com/docs/infrastructure-as-code
[3] Changelog https://render.com/changelog
[4] Docs + Quickstarts https://render.com/docs
[5] $ref renders schema type as any instead of object in ... https://github.com/swagger-api/swagger-ui/issues/10157
[6] Deploying FastAPI Applications Using Render https://www.geeksforgeeks.org/python/deploying-fastapi-applications-using-render/
[7] How do you get\know all the yaml options? : r/kubernetes https://www.reddit.com/r/kubernetes/comments/y583tz/how_do_you_getknow_all_the_yaml_options/
[8] Monorepo Support https://render.com/docs/monorepo-support
[9] Deploy a Django App on Render https://render.com/docs/deploy-django
[10] YAML schema reference for Azure Pipelines https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/?view=azure-pipelines
[11] Deploying a Python Web App on Render (Step-by ... https://python.plainenglish.io/deploying-a-python-web-app-on-render-step-by-step-guide-2025-adfa7c1f0456
[12] Environment Variables and Secrets https://render.com/docs/configure-environment-variables
[13] YAML | IntelliJ IDEA Documentation https://www.jetbrains.com/help/idea/yaml.html
[14] Deploy a Flask App on Render https://render.com/docs/deploy-flask
[15] 8 Setting options with YAML https://quarto-tdg.org/yaml.html
[16] Deploying on Render https://render.com/docs/deploys
[17] YAML Schema https://docs.axway.com/bundle/axway-open-docs/page/docs/apim_yamles/apim_yamles_references/yamles_yaml_schema/index.html
[18] How To Deploy a Django App to Render.com https://www.swyx.io/django-on-render
[19] Structure of the YAML input file https://docs.rendercv.com/user_guide/structure_of_the_yaml_input_file/
[20] Web Services https://render.com/docs/web-services
[21] Modules, Questions, Inputs, and Documents YAML Reference https://govready-q.readthedocs.io/en/latest/authoring-guide/modules-questions-inputs-documents-yaml-reference.html
[22] Spring-Boot one @Scheduled task using multiple cron ... https://stackoverflow.com/questions/40929161/spring-boot-one-scheduled-task-using-multiple-cron-expressions-from-yaml-file
[23] Render.yaml preview environment variables https://community.render.com/t/render-yaml-preview-environment-variables/2602
[24] Health Checks – Render Docs https://render.com/docs/health-checks
[25] Scheduling jobs with cron.yaml | App Engine flexible ... https://docs.cloud.google.com/appengine/docs/flexible/scheduling-jobs-with-cron-yaml
[26] How can I do a health check for a Rails-based app on ... https://stackoverflow.com/questions/65794152/how-can-i-do-a-health-check-for-a-rails-based-app-on-render
[27] Environmental Variables not appearing from render.yaml https://community.render.com/t/environmental-variables-not-appearing-from-render-yaml/6869
[28] Best Practices for Maximizing Uptime https://render.com/docs/uptime-best-practices
[29] Cron Jobs https://render.com/docs/cronjobs
[30] Default Environment Variables https://render.com/docs/environment-variables
[31] Health check & sveltekit https://community.render.com/t/health-check-sveltekit/2288
[32] Cron jobs with render.com (mini tutorial) https://community.redwoodjs.com/t/cron-jobs-with-render-com-mini-tutorial/4086
[33] Rails cron job configuration with the whenever gem https://community.render.com/t/rails-cron-job-configuration-with-the-whenever-gem/9675
[34] Development → Staging → Production render.yml example https://community.render.com/t/development-staging-production-render-yml-example/1441
[35] postgresml/render-healthcheck https://github.com/postgresml/render-healthcheck
[36] Deploying a Ruby on Rails App on Render with a Database ... https://railsnotes.xyz/blog/deploying-ruby-on-rails-on-render-with-databse-redis-sidekiq-cron
[37] Preview Environments https://render.com/docs/preview-environments
[38] GENERAL: What does 'system.yaml validation failed' mean ... https://jfrog.com/help/r/general-what-does-system-yaml-validation-failed-mean-and-how-to-resolve-it/general-what-does-system.yaml-validation-failed-mean-and-how-to-resolve-it
[39] Kubernetes: Pull an Image from a Private Registry using ... https://www.devopsschool.com/blog/kubernetes-pull-an-image-from-a-private-registry-using-yaml-and-helm-file/
[40] Helm Chart Validation Error https://drdroid.io/stack-diagnosis/helm-helm-chart-validation-error
[41] Pull an Image from a Private Registry https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
[42] Using Service Workers - Web APIs | MDN https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers
[43] helpful error messages when Quarto chunk options are mis ... https://github.com/quarto-dev/quarto-cli/issues/2434
[44] Image pull from private registry fails because of missing ... https://github.com/k3s-io/k3s/issues/8808
[45] Render Service Types https://render.com/docs/service-types
[46] Render.yaml fails to create web service https://community.render.com/t/render-yaml-fails-to-create-web-service/1274
[47] Standard way of keeping Dockerhub credentials in ... https://stackoverflow.com/questions/58516712/standard-way-of-keeping-dockerhub-credentials-in-kubernetes-yaml-resource
[48] Service worker inside Web Workers https://stackoverflow.com/questions/32251193/service-worker-inside-web-workers
[49] Web service fails with no error with render.yaml https://community.render.com/t/web-service-fails-with-no-error-with-render-yaml/4204
[50] Deploy a Prebuilt Docker Image https://render.com/docs/deploying-an-image
[51] WTH are so many clicks needed to get error messages ... https://community.home-assistant.io/t/wth-are-so-many-clicks-needed-to-get-error-messages-from-failed-yaml-configurations/469890
[52] Creating docker-registry secret using a YAML file https://discuss.kubernetes.io/t/creating-docker-registry-secret-using-a-yaml-file/7042
[53] YAML parser error when rendering Quarto document https://stackoverflow.com/questions/74219641/yaml-parser-error-when-rendering-quarto-document
[54] YAML processor runtimes via docker https://github.com/yaml/yaml-runtimes
[55] Scaling Render Services https://render.com/docs/scaling
[56] Flexible Plans for Render Postgres https://render.com/docs/postgresql-refresh
[57] Three Ways To Scale Your Apps With Render https://dzone.com/articles/three-ways-to-scale-your-apps-with-render
[58] Native Runtimes https://render.com/docs/native-runtimes
[59] Deploy for Free – Render Docs https://render.com/docs/free
[60] Auto scalling and YAML config https://community.render.com/t/auto-scalling-and-yaml-config/1903
[61] AWS EC2 Auto Scaling Groups: I get Min and Max, but ... https://stackoverflow.com/questions/36270873/aws-ec2-auto-scaling-groups-i-get-min-and-max-but-whats-desired-instances-lim
[62] Deploy a Python Flask App to Render with Docker https://blog.appsignal.com/2025/08/06/deploy-a-python-flask-app-to-render-with-docker.html
[63] The Official Render MCP Server https://github.com/render-oss/render-mcp-server
[64] Scaling Preview Environments https://community.render.com/t/scaling-preview-environments/4488
[65] Docker on Render https://render.com/docs/docker
[66] Pricing https://render.com/pricing
[67] New Scaling tab (with Autoscaling) - Announcements https://community.render.com/t/new-scaling-tab-with-autoscaling/1355
[68] Supported Languages https://render.com/docs/language-support
[69] Render Postgres Legacy Instance Types https://render.com/docs/postgresql-legacy-instance-types
[70] Enable preview environment group override https://feedback.render.com/features/p/enable-preview-environment-group-override
[71] Configure a Pod to Use a PersistentVolume for Storage https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/
[72] Persistent Disks https://render.com/docs/disks
[73] Regions – Render Docs https://render.com/docs/regions
[74] Set a value in render.yaml for production ONLY https://community.render.com/t/set-a-value-in-render-yaml-for-production-only/2823
[75] Kubernetes Series - Volume: gắn disk storage vào container https://viblo.asia/p/kubernetes-series-bai-6-volume-gan-disk-storage-vao-container-OeVKB6rrKkW
[76] New Region in Early Access: Virginia (US East) https://render.com/blog/new-region-in-early-access-virginia-us-east
[77] Preview only environment group https://community.render.com/t/preview-only-environment-group/1067
[78] Kubernetes Deployment Persistent Volume and VM disk size https://stackoverflow.com/questions/57048823/kubernetes-deployment-persistent-volume-and-vm-disk-size
[79] Connecting to MongoDB Atlas https://render.com/docs/connect-to-mongodb-atlas
[80] Render - Integrations https://electric-sql.com/docs/integrations/render
[81] Connecting with SSH – Render Docs https://render-web.onrender.com/docs/ssh
[82] YAML Preview pull requests, environment variables and ... https://community.render.com/t/yaml-preview-pull-requests-environment-variables-and-not-activating/624
[83] Render Deployment - Strapi Developer Documentation https://docs-v3.strapi.io/developer-docs/latest/setup-deployment-guides/deployment/hosting-guides/render.html
[84] Automatically point to PR preview database https://community.render.com/t/automatically-point-to-pr-preview-database/2215

