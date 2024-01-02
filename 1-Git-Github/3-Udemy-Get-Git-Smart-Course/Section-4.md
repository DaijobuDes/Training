# Section 4: Real World Use for Power Users

## Github Structure 101
- A repository is a project that can be pushed to GitHub and can have one or more branches
- A repository can have one or more contributors and each contributor can contribute to one or more repositories
- Each repository is either owned by a single person or an organization

## Cloning remote repos
- Copy the repository url and in GUI git based applications, the URL can be pasted directly and in CLI, this can be done by
`git clone <remote_url>`

## Introducing the terminal
- Using git via the command line, perform basic commands instead of using the GUI

## How and when to force push
- `git push origin branch_name -f`
- `git push -f`

## Diff stats for refactors
- Easy readability and maintenance but not changing the functionality

## Picking cherries
- `git diff` show differences between to commits
- `git diff --stat` shows statistics of the differences
- `git diff --stat .cs` shows statistics of the differences for cs files

## Large File System (LFS)
- Version control for large files greater than 100 MB file size

## A Tour of GitHub in 2019
- Pull Request - notifies the owner of the repository to apply your changes to his project
- Issue - issues reported about the project
- Github Marketplace - you can get extensions and add-ons to improve the project
- Explore - lets you explore other repositories you may be interested in
- Notifications - where you can see all the notifications
- Create a New Repository - lets you create a new repository
- Import Repository - imports an existing repository to your account
- New Gist - share code snippets to the public or even unlist it
- New Organization - creates an organization
- Profile - shows your profile
- Your Repositories - list of all your repositories
- Settings - github settings, account settings can also be found here


## Blame and history
- `git blame` who and when was the code committed
- History lists all the past commits of the repository