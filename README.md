# How to

1) Create a copy of this CRON repository and then configure it:
    - `Settings` → `Actions` → `General`, in section `Actions permissions` select `Allow all actions and reusable workflows`, and then save.
    - Edit the file `.github/workflows/mirror.yml` to change the URL of the cloned repo and the URL of the destination mirror repo.
2) Create a [new empty repository](https://github.com/new). Don't create a `README.md` or anything else. It will be used as the mirror and so it needs to be empty.
3) Create a new `Fine-grained personal access token` so that the CI can push to your GitHub mirror repo:
    - Open https://github.com/settings/personal-access-tokens/new
    - Fill in the following information:
        - **Token name**: choose any name you want, it doesn't matter.
        - **Expiration**: set it to the max (as of writing 1 year is the max :-/).
        - **Repository access**: choose `Only select repositories` and then pick **only** the GitHub repository where the mirror will be pushed. In my case it's `nextcloud-htmlviewer`.
        - **Repository permissions**: choose `Read and write` for the `Contents` permission and `No access` for everything else.
        - **Account permissions**: select `No access` for everything.
    - Click on `Generate token` and then copy the token. For example mine starts with `github_pat_`.
4) Create a new GitHub Actions secret for that token in the CRON repository that you created in the first step:
    - `Settings` → `Secrets and variables` → `Actions` and fill in this:
        - **Name**: `MIRROR_REPOSITORY_PERSONAL_ACCESS_TOKEN`
        - **Secret**: paste the generated token that you created in the previous step. Not the name of the token, but the token itself. In my case it starts with `github_path_`.
    - Click on `Add secret`.
5) Trigger the action for the first time from the CRON repo you created in the first step:
    - `Actions` → `Update devnoname120/nextcloud-htmlviewer mirror` → `Run workflow` → `Run workflow`.

■
