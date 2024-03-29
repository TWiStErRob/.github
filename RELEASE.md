# Release Process

 1. Draft a new release on GitHub
    * "_Tag version_": `vx.y.z` @ Target: `main`
    * "_Release title_": `x.y.z Two Word Summary` (e.g. biggest change / reason for release)
    * "_Describe this release_": use the template from [Releases on GitHub](#projects-releases-on-github)
 1. Do the release (see project specific docs/release.md file)
 1. Publish drafted release on GitHub  
    Note: _this will create a tag on `main`, equivalent to:_
    ```shell
    git checkout main
    git tag vx.y
    git push origin vx.y # or --tags
    ```
 1. Close `x.y.z` milestone
    * "_Due date_": release date
    * "_Description_": link to Release on GitHub

## Steps to build and publish an Android App

1. Merge everything to `main` that needs to be in the release.
    * Current active milestone might help to see what's missing.
    * Review `version.properties` is right for the target release, if not, PR.
1. Run `gradlew releaseRelease` to produce an APK and mapping file while on latest `main`.  
   **Latest `main` is important, because the commit counter will influence the version name/version code.**
1. Create a new Release in the Alpha track.
   * Upload the APK and the mapping file either to App Bundle Explorer or inline.
   * Action any potential warnings or errors.
   * Replace pre-populated release name (`<versionCode> (<versionName>)`) with just `<versionName>`. 
   * Copy Release Notes from previous alpha or production release.
   * Review and publish.
1. Smoke test on a real device installed from Google Play Store.
1. Promote to Production with 100% or staged rollout.


# Release Notes

<img src="https://yuml.me/diagram/boring;dir:LR;scale:100/class/[%3C%3CGitHub%3E%3E;Release%7Cversion%20name;version%20code;(date);change%20descriptions;tag;artifacts],%20[%3C%3CWebsite%3E%3E;%23history%7Cversion%20name;date;minor%20changes],%20[%3C%3Cpublished%3E%3E;Release%20Notes%7Cversion%20name;date;major%20changes],%20[%3C%3CGitHub%3E%3E;Milestone%7Cversion;date;all%20changes],%20[%3C%3CGitHub%3E%3E;issue%7Cfeature%20description;problem%20details],%20[%3C%3CGitHub%3E%3E;PR%7Cimplementation%20details],%20[%3C%3CGitHub%3E%3E;diff%7Clist%20of%20changes%20without%20context],%20[%3C%3Cgit%3E%3E;commit%7Cdetails%20of%20change],%20[%23history]-[note:%20Historical%20*Release%20Notes*%20for%20the%20end%20users.%7Bbg:wheat%7D],%20[Release]%3C%3E-1..n%3E[Milestone],%20[Milestone]%3C%3E-1..n%3E[issue],%20[Milestone]%3C%3E-1..n%3E[PR],%20[diff]++-1..n%3E[commit],%20[issue]-0..1%3E[PR],%20[PR]%3C%3E-1..n%3E[commit],%20[Milestone]-.-%3E[Release],%20[Release]-.-%3E[Milestone],%20[Release]-.-%3E[%23history],%20[Release]-.-%3E[diff],%20[Release]-.-%3E[PR],%20[Release]-.-%3E[issue],%20[Release%20Notes]-.-%3E[%23history],%20[%23history]-.-%3E[Release],%20[commit]-.-%3E[issue],%20[commit]-.-%3E[PR],%20[PR]-.-%3E[issue],.png" />

## Information sources
 * Commits since last release in Git repository
 * Milestones in GitHub
   * Pull requests in GitHub associated with Milestones
   * Issues resolved in GitHub associated with Milestones

## Deployment Targets

### Project Listing on my Website (`#history`)
Under https://www.twisterrob.net/project/ each project has a "History" section.  
**Target audience**: end users, tech savvy end users  
**Contents**:
 * Release version: the name of the release, usually in `v0.0.0#x` format
 * Release date: the date the release was first publicly available.
 * Bullet point list of all user-facing changes.
 * Link to Release on GitHub

**Template** (Jekyll GFM):
```
### [0.0.0#x](https://github.com/TWiStErRob/net.twisterrob.?/releases/tag/v0.0.0) (yyyy-mm-dd)
{: #v00000000}
 * Feature: ...
 * Enhancement: ...
 * Fix: ...
 * Experimental: ...
 * ...
   * Feature: ...
   * Enhancement: ...
   * Fix: ...
   * Experimental: ...
```

### User Release Notes
Published release notes (Google Play Store, Gradle Plugin Portal, etc.)  
**Target audience**: end users  
**Contents**:
 * Very short bullet point summary of features, relevant fixes
 * Limited to 500 characters.
 * Link to website

**Template** (plain text):
```
<versionName.latest> (<release date:YYYY-MM-DD>)
* <Major change.>
* <Feature: description.>
* <Fix: description.>

<versionName.older> (<release date:YYYY-MM-DD>)
* <even shorter list>

Full listing: http://www.twisterrob.net/project/<project>/#history
```

### ~~CHANGELOG.md~~ file in Git repository
*This target was obsoleted by GitHub Releases' description.*  
**Contents**:
 * Release version
 * Release date
 * Changes with links to PRs/Issues.

### Project's Releases on GitHub
**Target audience**: tech-savvy end users, contributors  
**Contents**:
 * Link to website
 * Development time range
 * Link to milestone
 * Full list of features with issue/PR links

**Template** (GFM):
```
## Release
<!-- TODO the day the release is published. -->
*Date*: yyyy-mm-dd
*Version*: 0.0.0

* **New**: ...major change...
* **Breaking**: ...major change...

See also the [public release notes on my website][3].

## Changes
For the full list of changes see [release milestone][1] and [diff][2].

<!-- TODO Each bullet point: `component: Title (#issue/#pr)`. -->

### Breaking
 * TODO ...

### New
 * TODO ...

### Fixes
 * TODO ...

### Internal
 * TODO ...

<!-- TODO Update these links. -->
[1]: https://github.com/TWiStErRob/net.twisterrob.?/milestone/0?closed=1
[2]: https://github.com/TWiStErRob/net.twisterrob.?/compare/v0.0.0...v0.0.0
[3]: https://www.twisterrob.net/project/?/#v00000000
```
Steps after pasting:
 * Fix TODOs
 * remove empty sections

### Project's Milestone on GitHub
**Target audience**: contributors  
**Contents**:
 * Name of milestone: `vx.y.z`
 * Date of milestone: release date
 * Description of milestone:
   * Link to Release on GitHub
