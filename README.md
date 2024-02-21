1. Setup accounts (5 minutes)
    - Create a Northflank account
        - https://app.northflank.com/signup 
        - Select Developer sandbox plan on team creation
        - Navigate to https://app.northflank.com/s/account/billing/claim-coupon and enter coupon AUSNAV-WS
        - no payment information required for Workshop
    - Create a Civo account - no payment information required for Workshop
    -   https://www.civo.com/seminar-signup
2. Create BYOC Cluster for Civo
    - Generate Civo API Key https://dashboard.civo.com/security
    - https://app.northflank.com/s/account/cloud/clusters/new/civo
    - Make sure to use 3 `Large - Standard (g4s.kube.large)` nodes
3. Create two repositories
    - Application repository 
        - https://github.com/northflank-civo/webapp-with-redis
    - GitOps repository
        - https://github.com/northflank-civo/gitops-northflank
4. Link Northflank account with GitHub App
    - https://app.northflank.com/s/account/integrations/vcs
    - Create a template for production
        - https://app.northflank.com/s/account/templates
        - Enable GitOps and select the GitHub repository `gitops-northflank`
        
          ![Added Services](./screenshots/template-1-gitops.png)
        - Set template to create a project
        - Select Bring your Own Cloud and the Civo cluster we just created
          ![Added Services](./screenshots/template-2-byoc.png)
        - Update the repositories in the template for the build services (`prod-builder` and `preview-builder`)
          ![Added Services](./screenshots/template-3-builders.png)
    - Run the template
5. Create pipeline
    - Add the `prod-web` service and the `redis` addon to the production stage
      
      ![Add Services](./screenshots/pipeline-1-add-services.png)
      ![Added Services](./screenshots/pipeline-2-with-services.png)
    - Add release flow ton the production stage

      ![Add Release Flow](./screenshots/pipeline-3-add-release-flow.png)
    - Configure the release flow to use GitOps

      ![Release Flow Configuration](./screenshots/pipeline-4-release-flow-config.png)
    - Run the release flow
    - Create preview environment via pipeline
      
      ![Add Preview Env](./screenshots/preview-env-1-add.png)
    - Copy the JSON config from [`./preview-env.json`](./preview-env.json) into the code editor
      
      ![Add Preview Env 2](./screenshots/preview-env-2-code.png)
    - Create a git trigger with Trigger reference “git-trigger”  under Preview > Settings tab for the webapp repository
    
      ![Add Preview Env 2](./screenshots/preview-env-3-triggers.png)
6. Create a PR and preview environment
    - Make a modification to your `webapp-with-redis` repository and create PR on GitHub
    - Watch a new preview environment being created for your PR
      
      ![Add Preview Env 2](./screenshots/preview-env-4-run.png)  
    - Merge PR to show fully end-to-end lifecycle management
8. Optional todos after:
    - Invite colleagues for multiplayer DevOps
    - Customize template with new micro-services and databases
    - Setup billing or use free developer tier
