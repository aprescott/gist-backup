### gist-backup – Creates a backup of all your gist repos

This Bash script backs up your public and private gists to a given directory as git repositories including the full revision history.
If the directories already exist, the gist repos will be updated.
It's all implemented as a simple Bash script.
It probably breaks if you have a lot of gists. Also, watch out for rate limiting.

#### Setup

Because this script backs up your private repos, not just your public ones, you'll need to generate an OAuth token.
This will also include write access to your gists although the script does not use it!
Here is how you can request the API token:

    $ curl -u github-user-name:github-password \
      -H "Content-Type: application/json" \
      -X POST \
      -d '{"scopes":["gist"], "note": "gist backup"}' \
      https://api.github.com/authorizations

Your account password is required here because v3 of the API is not accessible with your account token.

Take the token given in the response and set it in your git config as `github.gist.oauth.token`.

    $ git config --global github.gist.oauth.token TOKEN

You can revoke this token at any time by visiting <https://github.com/settings/applications>.

#### Usage

When you have set the gist token as described above, you can start backing up all your gists using the following command:

    $ ./gist-backup ~/gist-backups

This will clone all gist repositories to the local folder `~/gist-backups`.

When you call the script again, it will simply update the repos (pull changes) if they exist already.

#### Copyright & License

Copyright (C) 2012, Adam Prescott, licensed under the MIT license. See LICENSE.
