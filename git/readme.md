# git

## SSH Keygen
```sh
# generate a ed25519 ssh key
ssh-keygen -t ed25519 -C "comment"

# show public key
cat ~/.ssh/id_ed25519.pub
```

## Signing Commits (GPG)

- Generate GPG Key
```sh
gpg --full-gen-key
```

- Show list of GPG Keys
```sh
gpg --list-secret-keys --keyid-format LONG <EMAIL>

# OUTPUT
sec   rsa4096/30F2B65B9246B6CA 2017-08-18 [SC]
      D5E4F29F3275DC0CDA8FFC8730F2B65B9246B6CA
uid                   [ultimate] Mr. Robot <your_email>
ssb   rsa4096/B7ABC0813E4028C0 2017-08-18 [E]

#----------------------------------------------------
``````md
# Template
sec   rsa4096/**<______ID______>** 2017-08-18 [SC]
      D5E4F29F3275DC0CDA8FFC8730F2B65B9246B6CA
uid                   [ultimate] Mr. Robot <your_email>
ssb   rsa4096/B7ABC0813E4028C0 2017-08-18 [E]
```

- Show GPG Public Key
```sh
# cat 
gpg --armor --export <ID>

# In the example above, the specific command would be 
gpg --armor --export 30F2B65B9246B6CA
```

- Adding GPG to git
```sh
# Omit `--global` if you don't want it to be a global git change
git config --global user.signingkey <ID>

# Using the example ID above, the command would look like this
git config --global user.signingkey 30F2B65B9246B6CA

```

- Resources:
  - https://docs.gitlab.com/ee/user/project/repository/signed_commits/gpg.html
  - https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key


## Removing Git Submodules

- What happens if you accidentally add a git repo inside a git repo, and you want to just have the outer repo track the changes on the inner repo?
  - Check diagram below for better explaination!

```mermaid
---
title: Removing accidental added git repos with a git repo
---

flowchart LR

    subgraph Problem
        direction TB
        subgraph outer-repo[Repository]
        direction LR
        a1(Outer Source Code)
        %% -.- b1(Inner Source Code)
            subgraph inner-repo["Inner Repo"]
            b1(Inner Source Code)
            end
        end
    end

    subgraph Solution
        subgraph repo[Repository]
        direction LR
            a2(Outer Source Code)
            %% -.- b2(Inner Source Cde)
            b2(Inner Source Code)
        end
    end

    Problem --> Solution


    %% subgraph Explainer
    %%    id("
    %%    There is a .git directory (Inner Repo)
    %%    within a .git directory (Repository)
    %%    that has been accidentally added,
    %%    so this diagram explains what is
    %%    trying to do")
    %% end


    style Problem fill:#fff,stroke:#C51
    style Solution fill:#fff,stroke:#30C517
    %% style inner-repo font-weight:bold
```

- The commands to fix issue:
  - `git rm --cached <dir> --force`: removes the added code
  - `rm -rf <dir>/.git` : removes the inner .git module

```bash
# template
git rm --cached <dir> --force
rm -rf <dir>/.git

# example
git rm --cached examples/rust --force
rm -rf examples/rust

```