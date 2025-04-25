# GitOps CI/CD Pipeline with GitHub Actions, Docker, and ArgoCD

## Architecture

The project consists of two repositories:
- [The Application Repository](https://github.com/Minhaz00/ArgoCD-Project-App-Repo)
- [The K8s Manifests Repository](https://github.com/Minhaz00/ArgoCD-Project-Manifests-Repo) 

This separation follows the GitOps approach, where application code and deployment configurations are managed separately.

![](./images/1.svg)


The architecture consists of:

1. **GitHub Repositories**:
   - **app-repo**: Contains application code, tests, Dockerfile, and GitHub workflows
   - **manifests-repo**: Contains Kubernetes manifests and ArgoCD configuration

2. **CI/CD Pipeline**:
   - GitHub Actions workflows in app-repo build, test, and push Docker images
   - A second workflow updates the Kubernetes manifests in manifests-repo

3. **Deployment**:
   - ArgoCD watches the manifests-repo
   - When changes are detected, ArgoCD applies them to the Kubernetes cluster



## Project Structure

The project consists of two repositories: `app-repo` and `manifests-repo`. Below is the detailed structure for each repository.

### 1. App-Repo Structure

```
app-repo/
│
├── .github/
│   └── workflows/
│       ├── test-build-push.yaml       
│       └── update-k8s-manifest.yaml   
│
├── node_modules/                      
│
├── .gitignore
├── Dockerfile
├── index.js
├── index.test.js
├── package.json
└── package-lock.json
```

#### Key Files in App-Repo:

- **index.js**: Contains the Express application code
- **index.test.js**: Contains tests for the application
- **Dockerfile**: Instructions for building the application container
- **package.json**: Project metadata and dependencies
- **workflow files**: GitHub Actions pipelines for CI/CD

### 2. Manifests-Repo Structure

```
manifests-repo/
│
├── argocd/
│   ├── application.yml             
│   └── project.yml                   
│
└── k8s-manifests/
    ├── deployment.yml                 
    └── service.yml                   
```

#### Key Files in Manifests-Repo:

- **argocd/project.yml**: Defines the boundaries and permissions for the ArgoCD project
- **argocd/application.yml**: Configures how ArgoCD should deploy the application
- **k8s-manifests/deployment.yml**: Defines how the application should be deployed to Kubernetes
- **k8s-manifests/service.yml**: Defines how the application should be exposed

This separation of concerns follows GitOps principles:
- Application code, tests, and build configurations are in `app-repo`
- Infrastructure definitions and deployment configurations are in `manifests-repo`

This structure provides clear separation between application development and infrastructure management, allowing teams to work independently while maintaining a consistent deployment process.
