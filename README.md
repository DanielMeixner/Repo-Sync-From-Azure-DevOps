

# 🚀 SyncToGH: Azure DevOps ➡️ GitHub Repository Sync

This project provides an Azure DevOps pipeline that automatically syncs **all branches and tags** from your Azure DevOps repository to a specified GitHub repository. The pipeline is triggered on any branch change and ensures your GitHub mirror stays up to date. 🟢



## 🛠️ Getting Started


### ✅ Prerequisites
- 🏗️ An Azure DevOps project with repository access
- 🐙 A GitHub repository to sync to
- 🔑 A GitHub Personal Access Token (PAT) with repo permissions


### ⚡ Setup
1. 🍴 Fork or clone this repository into your Azure DevOps project.
2. 🛠️ In Azure DevOps, create a new pipeline using the provided `azure-pipelines.yml` file.
3. 🔒 Add a pipeline secret variable named `GH_PAT` containing your GitHub PAT.
4. ✏️ (Optional) Adjust the `GitHubUrl` variable in the pipeline if you want to sync to a different GitHub repository.
5. ▶️ Run the pipeline. On every branch change, all branches and tags will be force-pushed to the GitHub repository.



## ⚙️ How It Works

The pipeline performs the following steps:
1. 📥 Checks out the full repository history from Azure DevOps.
2. 👤 Configures Git with a generic user for commits.
3. 🔗 Adds the GitHub repository as a remote using the provided PAT.
4. 🔄 Fetches all remote branches and creates local tracking branches for each:

	 ```sh
	 for branch in $(git branch -r | grep -v '\->' | grep 'origin/' | sed 's/origin\///'); do
		 if [ "$branch" != "HEAD" ]; then
			 git branch --track "$branch" "origin/$branch" 2>/dev/null || true
		 fi
	 done
	 ```
	 This ensures every branch from Azure DevOps is available locally and will be pushed to GitHub.

5. 🚀 Pushes all branches and tags to GitHub, keeping your mirror up to date.

🧪 No build or test steps are included; the pipeline is solely for repository synchronization.



## 🤝 Contribute

Contributions are welcome! Please open issues or pull requests to suggest improvements or report problems. 💡

