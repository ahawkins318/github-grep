# github-grep

Use the github code search API to get a list of repositories which have code containing the search string.

```
usage: ./ghg [-rvh] [query]
  -r      show raw search results
  -v      verbose
  -h      display this help message
```

## Set up environment variables

`GITHUB_USER`: your github account username

`GITHUB_TOKEN`: your github [API token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)

`GITHUB_ORG`: (optional) the name of your github organization. If unset, search all public repos on github.

## Example

Let's see which repos have code containing the word `foo`:

```
$ GITHUB_ORG="" ./ghg foo
09-yarn-phonecall
ABRTuner
Asus-RT-N16
CanFestival-transplanted2stm32
Chromium
Driveonpolymer
Java-Diversos
Java-Training
JavaScriptCore
K3C-merlin
Kodi_test
LG-F320K_G2_Android_JB
LGP769_JB_android
Libxml2
```

Sure enough, we can verify that the resulting repos indeed talk a lot about `foo`. The [`09-yarn-phonecall` repo](https://github.com/techstormteam/09-yarn-phonecall) has [1000 results for `foo`](https://github.com/techstormteam/09-yarn-phonecall/search?q=foo&type=Code).

