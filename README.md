## spcn09 
## Kubernetes In Windows

## Wakatime
https://wakatime.com/@spcn09/projects/mibvulurid?start=2023-03-13&end=2023-03-19

## 1. Install Kubectl
   - Ref 
   - https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
   - https://youtube.com/playlist?list=PLJz1XVERx6ACV-vTC6eG7HSMdBUR0dZId
   - https://youtube.com/playlist?list=PLJz1XVERx6ACkMfMdLmziWg5P7wswAGV7
   - https://github.com/TanankornMoonprathom/Kube




   - download Kubectl.exe to path want

      ```
      curl.exe -LO "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
      ``` 
   - Add Path to environment variable
      - Search environment
  
        ![image](https://user-images.githubusercontent.com/119097663/224904080-a7de4fcd-c43d-4760-b483-0734aaeca796.png)


      - Click Environment Variables...

        ![image](https://user-images.githubusercontent.com/119097663/224904504-ac4bb0b8-4a35-4ddd-87c0-d0f665c86d04.png)

       - Select Path Click Edit

        ![image](https://user-images.githubusercontent.com/119097836/226183940-0ab3dcef-c532-4c98-be4e-1bf6b2b8096b.png)

       - Click New
        
        ![image](https://user-images.githubusercontent.com/119097836/226183877-99da52f9-aefa-49da-847d-550a43801da7.png)

      - Add Path that have kubectl.exe
      - Click OK
  
      - Test Kubectl enable in command
      ```ruby
      kubectl version --client
      ```

## 2. Install minikube
   - Ref
    - https://minikube.sigs.k8s.io/docs/start/

      - download minikube.exe

      ```ruby
      New-Item -Path 'c:<path want to install>' -Name 'minikube' -ItemType Directory -Force #create folder minikube
      Invoke-WebRequest -OutFile 'c:<path want to install>\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing #download install to path
      ```

      - Add Path to environment variable
      ```ruby
      $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
      if ($oldPath.Split(';') -inotcontains 'C:<path folder minikube.exe>'){ `
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:<path folder minikube.exe>' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
      }
      ```
   - Restart Terminal

## 3. Install Docker Desktop
   - Ref
    - https://docs.docker.com/desktop/install/windows-install/

## Test minikube start
1. Start a cluster using the docker driver
   ```ruby
   minikube start --driver=docker
   ```
  

2. Run with open dashboard
   ```ruby
   minikube dashboard
   ```
   

3. Test services
   ```ruby
   minikube service hello-minikube
   ```
  

4. Test Stop minikube
   ```ruby
   minikube pause
   ```
   

## 4. Install traefik
1. Install Traefik Resource Definitions
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
   ```
   

2. Install RBAC for Traefik
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
   ```
     

3. Install Traefik Helmchart
   ```ruby
   helm repo add traefik https://traefik.github.io/charts 
   helm repo update 
   helm install traefik traefik/traefik 
   ```
   

4. Verify service is running
   ```ruby
   kubectl get svc -l app.kubernetes.io/name=traefik
   kubectl get po -l app.kubernetes.io/name=traefik
   ```
   

5. copy user in dashboard-secret place it at user in traefik-dashboard


6. Deploy
   ```ruby
   kubectl apply -f . 
   ```

## Result

## 1. dashboard

![2023-03-19_230220](https://user-images.githubusercontent.com/117457958/226188709-0f1e7347-e059-44cb-8f43-950e6fbdad39.png)

## 2. https://traefik.spcn09.local/dashboard/#/http/routers

![2023-03-19_224404](https://user-images.githubusercontent.com/117457958/226188844-ef73d09f-1e43-44cb-9397-61450dbcc84f.png)

## 5. http://web.spcn09.local/

![2023-03-19_224439](https://user-images.githubusercontent.com/117457958/226188884-01d3ae9d-17bc-40ca-a31f-c05e72003bd8.png)