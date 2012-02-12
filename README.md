Backs up your public and private gists to a given directory as full git repositories. If the directories already exist, the gist repos will be updated. At the moment it's nothing more than a simple shell script. It probably breaks if you have a lot of gists. Also, watch out for rate limiting.

Because this script backs up your private repos, not just your public ones, you'll need to generate an OAuth token (which has write access to your gists -- this script does not use the write access!):

    $ curl -u github-user-name:github-password \
      -H "Content-Type: application/json" \
      -X POST \
      -d '{"scopes":["gist"], "note": "gist backup"}' \
      https://api.github.com/authorizations

Your account password is required here because v3 of the API is not accessible with your account token.

Take the token given in the response and set it in your git config as `github.gist.oauth.token`.

    $ git config --global github.gist.oauth.token TOKEN

You can revoke this token at any time by visiting <https://github.com/settings/applications>.

Copyright (C) 2012, Adam Prescott, licensed under the MIT license. See LICENSE.
