# mitlib-wp-demo

[![CircleCI](https://circleci.com/gh/MITLibraries/mitlib-wp-demo.svg?style=shield)](https://circleci.com/gh/MITLibraries/mitlib-wp-demo)
[![Dashboard mitlib-wp-demo](https://img.shields.io/badge/dashboard-mitlib_wp_demo-yellow.svg)](https://dashboard.pantheon.io/sites/5f779c92-08a8-42fe-9a9a-a23f95089bb7#dev/code)
[![Dev Site mitlib-wp-demo](https://img.shields.io/badge/site-mitlib_wp_demo-blue.svg)](http://dev-mitlib-wp-demo.pantheonsite.io/)

This is a demonstration WordPress application. It exists to give our engineers
a place to experiment.

## Git workflow note

If your work needs to be coordinated with configuration changes within the
WordPress application, the following steps should be repeatable:

1. Make and commit any code changes on your local repository.
2. Wait for the PR build to appear, and make the needed configuration changes.
3. Use the WP-CFM form under Wordpress Settings to export any changes to the
   PR build's file system. There is a bundle defined for all configuration
   already.
4. After you have used the Push command to export database configuration to this
   file, visit the Pantheon dashboard for the PR build, and you should see a
   change waiting in the code tab. Make sure that the only pending change is
   to the config bundle. Commit this to Pantheon's git system using the web form
   in the dashboard.
5. Fetch the updated branch - from the Pantheon git remote, not GitHub - and
   transfer this commit back to your PR branch. There are probably multiple ways
   to do this, but this one seems to work reliably:

```
git fetch pantheon --prune
git format-patch -1 <sha>
git am < <file.patch>
git push origin
```

This workflow should result in both your code changes, and the related
configuration changes, being in a single branch for code review on GitHub.

## Visual regression testing on Circle

There are a number of testing steps configured for this application on CircleCI.
Some of them appear to be fragile, in particular the step for running visual
regression tests. If your work will have no noticeable visual impact, or you are
comfortable with visual regressions being introduced, you can cause this step to
be skipped by using the `--skip-vr` flag within your commit message.
