# Create Neon branches with githooks
This repository contains a script for automating the creation of Neon branches when you create a new Git branch. The script works by listening to the post-checkout hook, which is invoked whenever you switch branches in Git. If you're creating a new branch, the script will prompt you to also create a new Neon branch with the same name.

### Pre-requisites
To use this script, you will need:

- Git installed on your system
- jq, a lightweight and flexible command-line JSON processor
- Your Neon project ID and API key

### Installation
1. Clone this repository to your local machine:

```bash
git clone https://github.com/raoufchebri/create-neon-branch-with-githooks.git
```

2. Navigate to the repository:

```bash
cd create-neon-branch-with-githooks
```
3. Add the PROJECT_ID and API_KEY to your environment variables:

```bash
export NEON_PROJECT_ID=<neon_project_id>
export NEON_API_KEY=<neon_api_key>
```

You can [create an API_KEY](https://neon.tech/docs/manage/api-keys#create-an-api-key) in the console.

The `neon_project_id` for a Neon project is found on the Settings page in the Neon Console, or you can find it by listing the projects for your Neon account using the Neon API.

4. Move the script to the .git/hooks directory in your Git repository:

```bash
mv post-checkout create-neon-branch-with-githooks/.git/hooks/
```

5. Make the script executable:

```bash
chmod +x your-git-repository/.git/hooks/post-checkout
```

### Usage
With the script in place, whenever you create a new Git branch, you'll be prompted to create a corresponding Neon branch. If you choose to do so, the script will send a request to the Neon API to create the branch, then write the connection URI to your .env file.

If a Neon branch with the same name already exists, the script will inform you and terminate.

If you switch to an existing Git branch, or if you create a new branch but choose not to create a corresponding Neon branch, the script will simply skip the Neon branch creation process.

Please be aware that this script only checks and prompts for Neon branch creation when a new Git branch is created. It does not automatically delete Neon branches when Git branches are deleted.