
## 🎓 Context
During this milestone, we were asked two main goals:

+ I**mplement Docker**
	- Containerized the **API, web app, and database** with Docker.
	- Configured an **internal network** to link necessary containers.
	- Set up **named volumes** for data persistence and **bind mounts** for custom configurations.
	- Orchestrated the services with **Docker Compose**.
	- Used an **environment file (`.env`)** to manage environment variables.
	- Published **Docker images** to **GitLab's Container Registry**.
	
- **Automate Workflow with GitLab CI/CD**
	- Deployed a **GitLab Runner** on our **OVH instance**.
	- Created a **CI/CD pipeline** to run jobs automatically.
	- Implemented the following CI/CD jobs for the **API and web app**:
	    - **Compile the code**
	    - **Run unit & integration tests**
	    - **Build and publish Docker images** to GitLab's Container Registry without admin privileges
	    - **Deploy the applications** to **staging & production** servers via SSH
	- Optimized performance by:
	    - **Caching dependencies** during the compilation stage.
	- Separated **CI configurations** in several files.
	- **Parallelized jobs** wherever possible to speed up execution.
	- Configured **GitLab Environments** for **staging** and **production**.
	- Set up **GitLab CI/CD secret variables** per environment.

## 📝 Progress
I haven't finished the following projects:
- Webapp test staging doesn't work (missing `CHROME_BIN` env variable)

I have produced the following bonuses:
- Integrated **Traefik** as a reverse proxy for **API & web app routing**.
- Enabled **HTTPS support** via Let's Encrypt.
- **Caching Docker images** to speed up the delivery stage.
- **Secure server** by not granting privileged rights and not using DinD.
- **Reusing artifacts**  with dependencies to speed up deployment stage.

## 🤔 Difficulties
List of difficulties I have encountered:
- Some issues while **configuring Traefik** for HTTPS and reverse proxying.
- Multiple issues with **GitLab CI/CD pipelines**, particularly during deployment.
    - Debugging took time due to the need to **wait for each pipeline run** before verifying fixes.
    - Encountered frequent **Docker Hub rate limits**, which temporarily blocked progress.
- **Webapp tests** don't work (`node run test`) because the variable environment `CHROME_ENV` is missing.

## ✅ Note Sonarqube:
My project is currently 0 days in debt.

