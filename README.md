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

How about repos within my company's organization which contain the name of one employee's dog?
```
$ ./ghg jake | wc -l
      35
```
Lots of results there! (We have an internal tool named after the dog.)

## When is this useful?

Imagine you are the maintainer of a popular open source project. You'd like to know how popular your brand new `shinyFeature` is becoming. Are your users adopting it? If you tried using github's web UI to find out, you'd be stuck sifting through pages and pages of search results showing each individual line of usage. Since your open source project is of course very well tested, all of your own tests surrounding `shinyFeature` are cluttering up the results. Running `ghg shinyFeature` helps you see which other projects are using your feature (assuming it has a relatively unique name). 

Imagine you are now at your day job, trying to help your company deprecate some `legacySadness`. How many of your internal repos are using this monstrosity that you and all your coworkers have agreed was ill-conceived from the start? You try using the github web UI to search, but you get pages and pages of results. They seem like they're all coming from the same couple of repos but it's hard to tell. You run `ghg legacySadness` and are relieved to confirm there are only three results. Maybe this deprecation won't be too bad!

## Caveats

All the usual caveats about github's code search capability apply. It doesn't search branches and they *still* don't support exact text match search. They only allow queries on the first 1000 results, so for searches with a very large number of high scoring search results, the list of repos can't be guaranteed to be exhaustive. 

When this tool pages through results, it has the potential to exceed github's rate limiting. Currently this results in an unhelpful error (`jq: error (at <stdin>:1): Cannot iterate over null (null)`) which I plan to improve. 

Paging is also disappointingly slow.
