# Plan: Convert Nested Repo Into a Real Submodule

## Current state

- This folder exists at `workspace/git-submodules-example-repo`
- It has its own local Git repository
- It is currently a nested repo, not a real Git submodule
- GitHub CLI (`gh`) is installed and authenticated as `rahul-parmar-rp`

## Goal

Convert this local nested repository into:

1. its own GitHub repository
2. a proper Git submodule inside the parent `portfolio` repository

## Planned steps

### 1. Prepare and commit the child repo locally

- Review the files inside `git-submodules-example-repo`
- Stage the initial files
- Create the first commit on `main`

Purpose:

- Make sure the child repo has a clean, pushable history before creating the remote

### 2. Create the GitHub repository with GitHub CLI

- Use `gh repo create` to create `rahul-parmar-rp/git-submodules-example-repo`
- Decide whether the repo should be public or private
- Set the new remote as `origin`

Purpose:

- Create the standalone remote repository directly from the CLI without using the GitHub website

### 3. Push the child repo to GitHub

- Push `main` to the new GitHub repository
- Verify that the remote repo is connected correctly

Purpose:

- Ensure the child repo exists independently on GitHub before wiring it back into the parent repo as a submodule

### 4. Remove the nested-repo form from the parent repo

- Move or remove the current nested folder from the parent repo working tree in the correct way
- Avoid leaving the parent repo in a mixed nested-repo state

Purpose:

- Prevent conflicts between a raw nested repo and a formal submodule setup

### 5. Add the GitHub repo back as a real submodule

- From the parent `portfolio` repo, run `git submodule add <repo-url> workspace/git-submodules-example-repo`
- Generate the `.gitmodules` entry automatically

Purpose:

- Register this project as a proper Git submodule tracked by the parent repo

### 6. Commit the parent repo changes

- Stage `.gitmodules`
- Stage the submodule pointer entry
- Commit the parent repo changes

Purpose:

- Save the formal parent-child relationship in the `portfolio` repository

## Expected end state

- `git-submodules-example-repo` exists as a standalone GitHub repository
- `portfolio` tracks it as a proper submodule
- The parent repo contains a `.gitmodules` file
- VS Code Source Control will still usually show two repositories, but that will now be the correct submodule setup

## Tools to be used

- `git` for local repository and submodule operations
- `gh` for GitHub repository creation and remote setup

## Notes

- A nested repo and a submodule can both appear as separate repositories in VS Code Source Control
- The difference is that a submodule is formally tracked by the parent repository
- The cleanest flow is: create remote repo, push child repo, then re-add it as a submodule
