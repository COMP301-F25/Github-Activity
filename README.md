# Github-Activity
# COMP301 Git Activity

Welcome to our collaborative Git exercise! In this activity, you will first work independently, then in pairs and teams, to practice branching, committing, resolving merge conflicts, and making pull requests.

---

## What You Will Learn

- Creating and pushing branches.  
- Making pull requests to a protected main branch.  
- Working with shared files in a team.  
- Encountering and resolving merge conflicts.  
- Organizing contributions from many people into one shared project.  

---

## (Required) Part 1: Individual Contribution (No Conflicts)

IntelliJ is not necessary for this activity, and it is meant to be done on the command line.  

(There are helpful commands at the bottom of the instructions)

1. Make a fork of this repository by clicking the "fork" button on the website.
2. Clone your newly created repository to your computer.
3. You will need to set the upstream to point at the class COMP301-F25 repo.  There are a list of commands at the bottom of the instructions to help you do this.
4. Verify that the origin and remote are properly set by typing `git remote -v`.  Once you have verified that everything looks right, you are ready to begin.
5. You will see folders for the morning section and the afternoon section. Choose the appropriate folder to work in.  
6. Create a new branch named `solo/<onyen>`.  
7. Now navigate to the `solo/` folder (unrelated to branch name). Inside it, create a new text file named `<onyen>.txt`.  
8. Add your full name inside the file.  
9. Stage, commit, and push your branch to your fork on GitHub.  
10. Open a pull request **from your fork’s branch** to the **upstream repository’s `main`** with the title `solo: <onyen>`.  

Each student will have their own file, so there should be no conflicts in this step.

---

## (optional if time) Part 2: Pair and Team Contribution (Designed Conflicts)

1. Your group of 4–6 students is a **team**. Choose a unique team identifier (for example, `UNC-Alpha`, `Sharks`, `Team42`).  

2. One person in the team acts as **Integrator**. The Integrator’s **fork** will be the team’s working fork. The Integrator:  
   - Adds teammates as **collaborators** on their fork (Repo → Settings → Collaborators).  
   - Creates the base branch `team/<team-id>/base` on their fork.  
   - Creates `teams/<team-id>/roster.md` with:  
     ```
     # Team <team-id> Roster (alphabetical by last name)
     Members:
     ```

3. All teammates add the **team remote** (the Integrator’s fork) to their local clones:  
   ```bash
   git remote add team https://github.com/<integrator-username>/<class-repo>.git
   git fetch team
   ```

4. Each pair branches **from the team base branch** and pushes to the **team remote**:  
   ```bash
   git checkout -b team/<team-id>/pair-<lastname1>-<lastname2> team/<team-id>/base
   # edit teams/<team-id>/roster.md (add exactly one line under 'Members:')
   git add teams/<team-id>/roster.md
   git commit -m "Add <Name1> + <Name2> — Team name: <team name>"
   git push -u team team/<team-id>/pair-<lastname1>-<lastname2>
   ```

   **OR (no collaborator access):** push to your own fork and open a PR **into the Integrator’s fork base branch**.

5. The Integrator opens PRs (or reviews incoming PRs) from each pair branch **into** `team/<team-id>/integration` (created from `team/<team-id>/base`). Resolve conflicts as specified.

---

## (Optional) Part 3: Conflict Resolution and Integration

1. The Integrator should create a new branch `team/<team-id>/integration` from the base on their fork.  
2. Then, merge each pair branch into the integration branch, one by one.  
   - This will cause conflicts in the `roster.md` file.  
   - Resolve the conflicts by keeping only one `Members:` header, then making sure all lines are included.  
   - The final list of pairs must be in **alphabetical order by last name**.  
   - Each line must show both names and the team name.  
3. After all conflicts are resolved and merged, push the integration branch.  

---

## (Optional) Part 4: Class Roster Pull Request

1. The Integrator should append the team’s final roster to the file `class-roster.md`.  
   - Add a section starting with `## <team-id>` followed by the list of pairs.  
2. Commit and push the update to the integration branch on their fork.  
3. Open a pull request **from the Integrator’s fork** `team/<team-id>/integration` **to** the **upstream repository’s `main`** with the title `<team-id> → class-roster`.  

---

## Quick Reference (Commands in Alphabetical Order)

- `git add <file>` — stage changes to be committed.  
- `git branch -vv` — show local branches and their remote tracking.  
- `git checkout -b <new-branch>` — create and switch to a new branch.  
- `git checkout <branch>` — switch to an existing branch.  
- `git clean -fd` — remove untracked files and folders (use with caution).  
- `git clone <repo-url>` — clone the repository to your computer.  
- `git commit -m "<message>"` — commit staged changes with a message.  
- `git diff` — show unstaged changes.  
- `git diff --staged` — show staged but uncommitted changes.  
- `git fetch --all` — fetch all updates from remote branches.  
- `git log --oneline --graph --decorate --all` — visualize branch history.  
- `git merge <branch>` — merge another branch into your current branch.  
- `git merge --abort` — cancel a merge attempt.  
- `git pull --ff-only` — update your branch with the latest changes from remote.  
- `git push -u origin <branch>` — push your branch to GitHub and set upstream.  
- `git reflog` — view recent HEAD movements to recover from mistakes.  
- `git remote add upstream <url>` — add the class repo as upstream.  
- `git remote add team <url>` — add the Integrator’s fork as team.  
- `git reset --hard origin/main` — reset your branch to match your fork’s main branch.  
- `git restore <file>` — discard changes to a file before staging.  

**Update local main from upstream:**
```bash
git checkout main
git fetch upstream
git merge --ff-only upstream/main
git push origin main
```

---

## Common Mistakes

1. **Confusing branch names with folder names.**  
Remember: `solo/{{ONYEN}}` is the branch name; `solo/` is the folder. Both are required.

2. **Forgetting to pull the latest changes before branching or merging.**  
Always run `git pull --ff-only` on `main` or your base branch to avoid diverging histories.

3. **Leaving merge conflict markers in files.**  
Always remove `<<<<<<<`, `=======`, and `>>>>>>>`. Ensure the final `roster.md` is clean and alphabetized.

---

## Extra Debugging Commands

- `git status` — check current branch and file state.  
- `git log` — view commit history.
- `git remote -v` - view current origin and remote urls.

---

**Setup remotes (run once per local clone):**
```bash
# already set automatically when you clone YOUR fork
git remote -v

# add the class repo as 'upstream'
git remote add upstream https://github.com/COMP301-F25/Github-Activity.git
git fetch upstream
```

**Keep your fork up to date (before new work):**
```bash
git checkout main
git fetch upstream
git merge --ff-only upstream/main
git push origin main
```
