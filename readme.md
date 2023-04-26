# General notes:
Subtree: `app/commonFeatures/DataDebugger`

This subtree allows you to keep the code referring to this `subtree core`, the following explains how the
code should be updated from the mobile application (App) to the shared common code (CORE-MOBILE) and vice versa.

Make sure you have included the following REMOTE repository:
* git remote add CORE-MOBILE https://git.formos.com/formos/perfect-core-mobile

Note: App refers the LOCAL mobile application that you are working on (i.e. Make and Pack)

**IMPORTANT:**

- `commonFeatures_data_debugger` is the branch that has the common shared code between App and Core Mobile
- `iteration_1` is the LOCAL branch for the App where you want to pull/push the changes in your LOCAL App
- `commonFeatures` is the REMOTE branch from where you want to pull/push the changes in Core Mobile

## A. Update from Core Mobile to App

1. Open Git terminal in **LOCAL App** to bring changes from Core Mobile:
2. Checkout to the desirable branch (Core Mobile) to bring the changes: (for example: commonFeatures)
* `git fetch CORE-MOBILE`
* `git checkout CORE-MOBILE/commonFeatures`
3. Split (update) code to commonFeatures_data_debugger branch. Note the name 'commonFeatures_data_debugger' is an arbitrary name
   depending on the needs one can change it
* `git subtree split -P app/commonFeatures/DataDebugger -b commonFeatures_data_debugger`
* `git checkout commonFeatures_data_debugger`
* `git push --set-upstream origin commonFeatures_data_debugger`
4. Checkout to the target branch in the current App (for example: iteration_1) and update:
* `git checkout iteration_1`
* `git subtree pull --prefix app/commonFeatures/DataDebugger origin commonFeatures_data_debugger --squash -m "[CoreMobile] put your comment"`
5. Push changes of the target branch:
* `git push --set-upstream origin iteration_1`

## B. Update from App to Core Mobile
1. Open Git terminal in **LOCAL App** to send/push changes to Core Mobile:
2. Checkout to the desirable branch to push the changes: (for example: iteration_1)
* `git fetch CORE-MOBILE`
* `git checkout origin/iteration_1`
3. Commit changes in the desirable branch
* `git commit -a -m "[idChildApp] put your comment"`
4. Split (update) code to core-mobile_shared_code branch
* `git subtree split -P app/commonFeatures/DataDebugger -b commonFeatures_data_debugger`
* `git checkout commonFeatures_data_debugger`
* `git push --set-upstream origin commonFeatures_data_debugger`
5. Checkout to the target branch in REMOTE (for example: commonFeatures in Core Mobile)
   and create a TEMPORAL branch and update:
* `git fetch CORE-MOBILE`
* `git checkout CORE-MOBILE/commonFeatures -b temp_branch`
* `git subtree pull --prefix app/commonFeatures/DataDebugger origin commonFeatures_data_debugger --squash -m "[idChildApp] put your comment"`
6. Push updated code in REMOTE CORE-MOBILE, HEAD:commonFeatures:
* `git push CORE-MOBILE HEAD:commonFeatures`

7. Delete temporal branch (if needed):
* `git checkout master`
* `git branch --delete temp_branch`

## ONLY FIRST TIME: Only for reference - NO RUN THIS:
NO NEED TO RUN THIS ANYMORE THIS WAS DONE ON **April 5, 2023**. but it is included as a reference, it was executed at the beginning:

### Add subtree if the folder does not exist yet (No need to run this anymore - just reference)

Add subtree folder in App and Core Mobile, the shared folder must be empty. For example this is applied in the following path (`app/commonFeatures/DataDebugger`):
* `git subtree add --prefix app/commonFeatures/DataDebugger commonFeatures_data_debugger --squash`
* `git push --set-upstream origin iteration_1`


### Add subtree if the folder already exist (No need to run this anymore - just reference)

Open Git terminal in LOCAL App and you can create the subtree, Example:

# A. In Local App (NO NEED TO RUN THIS AGAIN)
1. Open Git terminal in LOCAL App
2. Checkout the desirable branch and commit any changes in this branch
* `git checkout -b iteration_1`
* `git commit -a -m "[App] Save last changes"`

3. Checkout the remote branch that you want to pull/push the shared code:
* `git fetch CORE-MOBILE`
* `git checkout -b core_source CORE-MOBILE/commonFeatures`

4. Create a new branch that will have the remote shared code
* `git subtree split -P app/commonFeatures/DataDebugger -b commonFeatures_data_debugger`

5. Remove the remote branch since it is not needed anymore:
* `git checkout commonFeatures_data_debugger`
* `git branch -d core_source`

6. Take the shared code and apply to the target branch and set the shared folder as subtree
* `git checkout iteration_1`
* `git subtree add --prefix app/commonFeatures/DataDebugger commonFeatures_data_debugger --squash`
* `git push --set-upstream origin commonFeatures_data_debugger`
* `git push --set-upstream origin iteration_1`

7. Delete the temporal branch:
* `git checkout master`
* `git branch --delete core_source`

# B. In Core Mobile (NO NEED TO RUN THIS AGAIN)
1. Open Git terminal in LOCAL App

2. Update the remote information and checkout to the desirable branch
* `git fetch CORE-MOBILE`
* `git checkout origin/iteration_1`

3. Commit any changes in this branch
* `git commit -a -m "[App] Save last changes"`

4. Split the shared code in the common shared branch
* `git subtree split -P app/commonFeatures/DataDebugger -b commonFeatures_data_debugger`
*  `git push --set-upstream origin commonFeatures_data_debugger`

5. Create a temporal branch where you want to apply the shared code
* `git fetch CORE-MOBILE`
* `git checkout CORE-MOBILE/commonFeatures-b core_source`

6. Remove the folder that you want to share with Core Mobile
* `git rm -r app/commonFeatures/DataDebugger`
* `git commit -m "[coreMobile]: Remove before to use sub-tree"`

7. Bring the shared code from the shared common branch
* `git subtree add --prefix app/commonFeatures/DataDebugger commonFeatures_data_debugger --squash`

8. Push the shared code in the REMOTE
* `git push CORE-MOBILE HEAD:kinesis`

9. Delete the temporal branch:
* `git checkout master`
* `git branch --delete core_source`

