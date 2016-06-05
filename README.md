### GICC (git in-code comments) ###

GICC is git client hook for extracting "special" comments from source code files.

It works by extracting comments that start with `@comment:` from source code files.
It will then save these in a temporary file and will include them in the final commit message.

This way you can focus on writing your code and add usefull comments *WHILE* writing the code. Not hours later when you decide to actually commit the changes.

The creation of this code was inspired by [commit-comments](https://github.com/thebearjew/commit-comments).

#### early alpha version ####

Please note that these scripts you are looking at are currently in alpha testing phase. 
**Use at own risk!!!**
I'll remove this section once I'm sure it won't to any damage and has ~~no more~~less errors.

#### distinction to commit-comments ####
The commit-comments hook uses a `prepare-commit-msg`' and a `post-commit` script. The commit messages in the code will be inserted as git comment message while commiting. But the commit messages in code will also appear inside the git history of the file as they will be removed inside the `post-commit` hook.

I wanted to create the same behaviour, with one exception. I don't want to include **ANY** in-code commit message inside git. The "@commit:" message should not be part of the git history. Therefore gicc uses a `pre-commit` (1) and `prepare-commit-msg` (2) hook.
In pre-commit (1) it will extract the in-code commit messages and save them for later inclusion inside the git commit message.
The prepare-commit-msg step will check if there is a gicc commit message to inlcude. If so it will add this message to the git commit message.

#### know bugs ####
- includes in-code messages twice
- when calling 'git commit -m "foo"' will print "foo" after the in-code messages

#### ToDo: ####
- remove `@comment:` from git commit message itself
  Instead of "@comment: foo" include only "foo"
- include file name (and maybe line number) where gicc comment was extracted
- Test system compatibility (developed on os x)
- remove "ggrep" command and determine command to use on the fly
- include some examples in the readme
