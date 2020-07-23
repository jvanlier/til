GitLab CI Runner with Local Docker Image - pull_policy
========================================

I lost some time yesterday trying to get this to work: a pipeline that builds an image in the first stage (if needed, e.g. dockerfile or dependencies change) for fast linting and testing in the following stages. We didn't want to push the image in order to not pollute the container registry and to avoid implementing lifecycle policies. So: build locally, register in local Docker deamon, then use local image in the next step. This, of course, only works if there's only one runner active.

Turns out that this doesn't work by default! GitLab runners, by default, always try to pull an image from the registry. If it's not there, it'll fail, even though the image is available locally.

See `pull_policy` in the [Advanced configuration](https://docs.gitlab.com/runner/configuration/advanced-configuration.html): default is `always`, can be changed to `never` or `if-not-present`.
