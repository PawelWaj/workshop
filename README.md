# Workshop: Creating Kubernetes Apps with Backstage

This hands-on workshop will guide you through creating Kubernetes application manifests using Backstage Software Templates. You'll create a complete set of Kubernetes manifests that can be deployed through ArgoCD.

## Prerequisites

- Access to the Backstage portal
- GitHub account
- Access to ArgoCD dashboard (for verification)

## Workshop Steps

### 1. Access the Backstage Portal

Navigate to the Backstage portal in your browser.

### 2. Create a New Component

1. Click on the **Create** button in the left navigation panel
2. Find and select the **Kubernetes Application Template**
   - Template URL: `https://github.com/PawelWaj/workshop/blob/main/templates/kubernetes-app-template.yaml`

### 3. Fill in Template Details

Complete the form with the following details:

**Application Information:**
- **Application Name**: Enter a name for your application (use lowercase letters only)
- **Team Name**: Enter your team name (this will also be used as the namespace)
- **Application Description**: Enter a brief description of your application

**Configuration Details:**
- **Container Image**: Use the default (`nginx:latest`) or specify another image
- **Replicas**: Set the number of replicas (default is 1)
- **Custom Label**: Add any random text as a custom label

**Repository Information:**
- **Repository Location**: Select the repository where you want to create the Kubernetes manifests

### 4. Generate the Template

Click the **Create** button at the bottom of the form to generate your Kubernetes manifests.

### 5. Make Repository Public

⚠️ **Important**: The template creates a private GitHub repository by default, but ArgoCD can't access private repositories with this setup.

1. Go to your newly created GitHub repository
2. Click on **Settings** at the top of the repository page
3. Scroll down to the **Danger Zone** section
4. Find **Change repository visibility** and click **Change visibility**
5. Select **Make public** and confirm by typing the repository name

### 6. Create an ArgoCD Application

Now that your manifests are in a public repository, create an ArgoCD application to deploy them:

1. Log in to the ArgoCD dashboard
2. Click the **+ New App** button
3. Fill in the application details:
   - **Application Name**: Use the same name as in Backstage
   - **Project**: Select `default` or the appropriate project
   - **Repository URL**: Enter your GitHub repository URL
   - **Path**: Enter `k8s` (this is where your manifests are located)
   - **Cluster**: Select your target Kubernetes cluster
   - **Namespace**: Enter the team name you used in Backstage

4. Click **Create** to deploy your application

### 7. Verify Deployment

1. In the ArgoCD dashboard, click on your newly created application
2. Check that all resources are synced and healthy
3. Verify the deployment in Kubernetes:
   ```bash
   kubectl get all -n <your-team-name>
   ```

## Success Criteria

✅ You have successfully:
- Created Kubernetes manifests using Backstage templates
- Made your repository public for ArgoCD access
- Created an ArgoCD application that refers to your manifests
- Deployed your application to Kubernetes

## Troubleshooting

- **Registration Error**: If you encounter registration errors in Backstage, make sure all form fields are filled out correctly
- **ArgoCD Sync Error**: If ArgoCD can't sync, verify that your repository is public
- **Deployment Issues**: Check ArgoCD logs and event messages for any deployment errors

## Next Steps

Once you've completed the workshop, consider:
- Adding more resources to your manifests (ConfigMaps, Secrets, etc.)
- Setting up CI/CD pipelines to update your manifests
- Exploring more advanced Backstage templates
