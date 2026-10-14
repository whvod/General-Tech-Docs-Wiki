# How to Download the Entire Code from a GitHub Pull Request

You can download the files from a GitHub pull request (PR) as a ZIP archive, fetch its branch with Git, or save its changes as a diff. Choose the method that matches what you need.

## 1. Download a ZIP from GitHub

This method does not require Git and gives you a snapshot of the PR's files.

1. Open the pull request on GitHub, for example `https://github.com/OWNER/REPO/pull/NUMBER`.
2. Open the **Files changed** tab.
3. Use the **Download** button, if it is available, to download the changed files as a ZIP.
4. Extract the ZIP archive to a folder.

The ZIP is a snapshot; it does not include the PR's commit history.

## 2. Fetch the pull request locally with Git

Use this method if you want to inspect, test, or modify the code locally and retain its commit history.

1. Clone the repository and enter its directory:

   ```bash
   git clone https://github.com/OWNER/REPO.git
   cd REPO
   ```

2. Fetch the PR's head into a local branch, replacing `NUMBER` with the pull request number:

   ```bash
   git fetch origin pull/NUMBER/head:pr-NUMBER
   ```

3. Check out the local branch:

   ```bash
   git checkout pr-NUMBER
   ```

If you know the source branch name and it is in the repository's `origin` remote, you can fetch and check it out by name instead:

```bash
git fetch origin BRANCH_NAME
git checkout BRANCH_NAME
```

To look up the source branch with GitHub CLI:

```bash
gh pr view NUMBER --json headBranch --jq '.headBranch'
```

## 3. Save the PR changes as a diff

If you only need the changes in a text file, use GitHub CLI:

```bash
gh pr diff NUMBER > pr.diff
```

Alternatively, use the GitHub REST API for a public repository:

```bash
curl -L \
  -H "Accept: application/vnd.github.diff" \
  https://api.github.com/repos/OWNER/REPO/pulls/NUMBER \
  -o pr.diff
```


## Which method should you choose?

- **Quick snapshot:** Download a ZIP from GitHub.
- **Full local working copy with history:** Fetch the PR with Git.
- **Changes only:** Save a diff file.
