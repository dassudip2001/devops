Step 1: Create a New Monorepo

    Initialize a New Repository:
    Create a new empty repository that will serve as your monorepo.

    bash

    mkdir monorepo
    cd monorepo
    git init

Step 2: Add Existing Repositories as Subdirectories

    Add Remotes:
    Add the existing repositories as remotes.

    bash

git remote add repo1 <url_to_repo1>
git remote add repo2 <url_to_repo2>
git remote add repo3 <url_to_repo3>

Fetch and Merge Branches:
Fetch and merge the branches from each repository into the new monorepo.

bash

    git fetch repo1
    git merge repo1/main --allow-unrelated-histories

    git fetch repo2
    git merge repo2/main --allow-unrelated-histories

    git fetch repo3
    git merge repo3/main --allow-unrelated-histories

Step 3: Reorganize Directory Structure (Optional)

    Reorganize if Needed:
    If the existing repositories had different directory structures, you may want to reorganize the monorepo directory structure to suit your needs.

    bash

    # Move contents of repo1 to a subdirectory
    mkdir repo1
    git mv -k * repo1/

    # Repeat for repo2 and repo3

Step 4: Resolve Conflicts

    Resolve Conflicts:
    If there are conflicts during the merge, resolve them manually.

    bash

    git mergetool  # opens a tool to help resolve conflicts
    git commit -m "Merge conflicts resolved"

Step 5: Push Changes

    Push Changes:
    Push the changes to the new monorepo.

    bash

    git push origin main

Step 6: Update Submodules (If used)

    Update Submodules (If Applicable):
    If any of the existing repositories were using Git submodules, update them accordingly.

    bash

    git submodule update --init --recursive

Step 7: Cleanup (Optional)

    Remove Old Remotes (Optional):
    Optionally, you can remove the remote repositories if they are no longer needed.

    bash

    git remote remove repo1
    git remote remove repo2
    git remote remove repo3

Notes:

    The --allow-unrelated-histories flag is used to merge repositories with unrelated commit histories.
    Make sure to adapt the branch names and remote URLs according to your specific setup.
    Be cautious and make backups before performing such operations.

Keep in mind that merging repositories with a long history or complex dependencies might require additional considerations, and it's essential to thoroughly test the resulting monorepo to ensure its integrity.
