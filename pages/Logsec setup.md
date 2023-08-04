- ## Git Hooks
- path: notes/.git/hooks
- The two file should be executable
	- `chmod +x pre-commit post-commit`
- ### pre-commit file
- ```bash
  #!/bin/sh
  #
  #
  # Pull before committing
  # Credential handling options:
  #  - hardcode credentials in URL
  #  - use ssh with key auth
  #  - https://git-scm.com/docs/git-credential-store
  #  - git credential helper on windows
  
  # Redirect output to stderr, uncomment for more output for debugging
  # exec 1>&2
  
  output=$(git pull --no-rebase)
  
  # Handle non error output as otherwise it gets shown with any exit code by logseq
  if [ "$output" = "Already up to date." ]; then
      # no output
      :
  else
      # probably error print it to screen
      echo "${output}"
  fi
  
  git add -A
  ```
- ### post-commit file
- ```bash
  #!/bin/sh
  
  git push origin main
  ```
- ## Plugins
	- Git
	- Tags
	- Markdown Table Editor
	- Bullet Threading
	- Journals calendar
	- logseq-psummarise-plugin
	- logseq-plantuml-plugin