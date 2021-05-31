---
title: Managing Pull Requests
---

If you'd like to help out managing PRs on the Gatsby repo on GitHub, this document is for you. We'll go over conventions the team prefers, what we check for on various types of pull requests, permissions, and guidelines on how to leave feedback.

We have over 2,000 contributors and so much of what makes Gatsby great is contributed by folks like you.

Needless to say, we get a lot of PRs and we've been merging over a [100 contributions](https://twitter.com/kylemathews/status/1111435640581689345) every week. Yes, _every week_.

Let's talk a little about how we manage pull requests in the Gatsby repo.

For an introduction on what Pull Requests are and how to file one, check out the contributing doc on [How to Open a Pull Request](/contributing/how-to-open-a-pull-request).

## Verifying a Pull Request

### General Guidelines

Some general things to verify in a pull request are:

- Links ought to be relative instead of absolute when linking to docs (`/docs/some-reference/` instead of `https://www.gatsbyjs.org/docs/some-reference/`)
- Language ought to be inclusive and accessible
- Issues and RFCs (if any) that this PR addresses ought to be linked to

> 💡 When looking at a PR for the first time, it can help to read up on linked issues or [RFCs](/contributing/rfc-process/) (if there are any) to gain context on what the PR intends to add or fix.

Note for Gatsby Core or Learning team members: if a PR has merge conflicts or needs a little help to push it across the finish line, contributing directly to a fork or branch can be a great way to resolve it. See notes on [pushing to a remote fork in Git](#pushing-changes-to-a-remote-fork).

### Type Specific Guidelines

Each kind of PR also requires a different set of specific checks from us before they are merged in.

Let's go over them below.

#### Documentation

We typically look for the following in [PRs that add documentation](/contributing/docs-contributions/):

- Correctness — whether the added documentation is technically correct
- Style — whether the written language follows our [style guide](/contributing/gatsby-style-guide/)
- Headings – whether the heading levels in a doc start with h2 (`##` in Markdown) and grow in order, establishing an accessible content hierarchy
- Type & Format – whether docs and learning materials align with our recommendations and [docs templates](/contributing/docs-templates/)

If a PR includes code examples, tutorials, recipes, or actionable guides, the reviewer must test out the material to ensure accuracy. **No PRs should be approved or merged that haven't been vetted for errors or omissions.**

#### Code

For [PRs that add code](/contributing/code-contributions/) (whether a feature or fix), we look for the following:

- Correctness — whether the code does what we think it does
- Tests — when fixing a bug or adding a new feature, it can be very valuable to add tests. While we do merge some small PRs without them, more often than not, it's good to have tests asserting behavior. This can be a combination of unit tests for the specific package, snapshot tests, and end to end tests. The goal here is to ensure that something that is being fixed or added _remains_ fixed or working the way we expect it to. Good tests ensure this.
- Code Quality — focus on reasonable changes that will likely improve code maintenance, comprehension, or correctness. Stylistic changes are typically linted for by Prettier. Don't nitpick.
- Documentation in the package's README if you're adding something

#### Starters or Site Showcase

For PRs that add a site or a starter to the showcase, we ought to check:

- Check if the site or starter is built with Gatsby
- Links — check if the links are working and accessible
- Tags — ensure the tags match existing tags
- Featured Status — new sites should not be marked as featured. Featured sites are occasionally updated by a member of the Gatsby team.

#### Blog posts

For PRs that add a blog post, we ought to check:

- Approval – has the [blog post been approved](/contributing/blog-contributions/) by marketing or another Gatsby internal team?
- Correctness — whether the added documentation is technically correct
- Style — whether the written language follows our [style guide](/contributing/gatsby-style-guide/)
- Subject matter — blog posts should not be purely promotional, spammy, or inappropriate. An author should check with a member of the Gatsby team that their post is appropriate for the blog before creating their PR.
- Time Sensitivity — blog posts are more time dependent than docs, especially since they get buried after more posts are published. If something is continually relevant and more of a general how-to, it should go in the [Reference Guides](/docs/guides/) or [Tutorials](/tutorial/) section of the docs.

## Automated Checks

Our repository on [GitHub](https://github.com/gatsbyjs/gatsby) has several automated CI checks that are run automatically for all PRs. These include tests, linting and even preview builds for [gatsbyjs.org](https://www.gatsbyjs.org).

We want all of these checks to pass. While it's okay to review a work in progress PR with some failed checks, a PR is only ready to ship when all the tests have passed.

Let's go over some common failure cases and how to fix them:

### Linting

We lint all code and documentation for consistency. You might find that your PR fails on the linting check.

If this is your PR and you have the code checked out on your machine, you can run:

```shell
npm run format
```

This will automatically re-format your changes to match the linting requirements. Don't forget to git commit and push your new changes.

## Other Checks

### Testing Locally

While we have many _many_ tests in our repository (that are run automatically on every commit), there can be times when there exists an edge case (or five) that isn't covered by these.

In situations like this, testing the change locally can be very valuable.

> 💡 In case this is the first time you're doing this, you might have to [set up your development environment](/contributing/setting-up-your-local-dev-environment).

Testing out unpublished packages locally can be tricky. We have just the tool to make that easy for you.

Say hello to your new best friend, `gatsby-dev-cli`.

#### gatsby-dev-cli

`gatsby-dev-cli` is a command-line tool for local Gatsby development. When making changes in gatsby packages, this helps copy changes in the packages to a Gatsby site that you can test your changes on.

Check out the [`gatsby-dev-cli` README](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-dev-cli) to learn more.

### Commit and PR Title

It's good to have descriptive commit messages so that other folks can make sense of what your commit is doing. We like [conventional commits](https://www.conventionalcommits.org/en/v1.0.0-beta.3).

However, PRs get squashed when merged into our repository so individual commit messages are not as important as PR titles.

Let's look at some examples of good and bad PR titles:

#### Good PR Titles ✅

- chore(docs): Fix links in contributing page
- feat(gatsby): Add support for per page manifests
- fix(gatsby-plugin-sharp): Ensure images exist before attempting conversion

These are good PR titles because they are concise, specific and use the [conventional commit](https://www.conventionalcommits.org/en/v1.0.0-beta.3) format.

#### Bad PR Titles ❌

- new tests
- add support for my new cms
- fix bug in gatsby

These are bad PR titles because they are generic, don't communicate the change properly and don't use the conventional commit format.

## Giving Feedback

- Be _kind_. We're stronger every day because of our community, so compassion is important. We want all contributors to feel welcome.
- Make suggestions using [GitHub's suggestions feature](https://help.github.com/en/articles/commenting-on-a-pull-request#adding-line-comments-to-a-pull-request) if possible. This makes accepting your suggestions easier for the author.
- Link to examples when necessary
- Try not to [bikeshed](http://bikeshed.com/) too much
- Note when a suggestion is optional (as opposed to required)
- Be objective and limit nitpicks (a few are fine if they add value or improve code readability)
- Don't suggest and expect changes out of scope which are best addressed in a separate PR

## Pushing changes to a remote fork

Sometimes the easiest way to unblock a stalled PR is to sort out merge conflicts or apply remaining suggestions. When the GitHub UI won't cut it, you can (often) apply changes directly to someone's remote fork with Git:

- Add their Gatsby fork as a remote:<br />`git remote add <forkname> git@github.com:<username>/gatsby.git`
- Fetch the branches:<br />`git fetch <forkname>`
- Check out their branch locally:<br />`git checkout -b <branch-name> <forkname>/<branch-name>`
- Make your changes, add some commits
- Push branch to the remote fork (also see [Gotchas](#gotchas) below):<br /> `git push <forkname> head:<branch-name>`

Alternatively, you can manage forks and branches with [hub](https://github.com/github/hub).

## Rights and Permissions

### Who can review a PR?

If you're a member of the [gatsbyjs](https://github.com/gatsbyjs) organization on GitHub, you can review **most** PRs. PRs with [`topic: internal`](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aopen+is%3Aissue+label%3A%22topic%3A+internal%22) are reserved for Core and Learning team members as they are typically part of an internal project or hiring process.

> 💡 Not a member yet? Want to [get involved in contributing](/contributing/how-to-contribute/) to open source projects? Make your first contribution and you'll be invited automatically!

### Who can approve a PR?

Every PR opened in the repository needs to be approved before it can be merged. While anyone who is a member of the [gatsbyjs](https://github.com/gatsbyjs) organization can approve a PR, to be merged in, it needs to be reviewed by a member of the team that owns that part of Gatsby.

Typically this is:

- **gatsbyjs/core** for Code
- **gatsbyjs/learning** for Documentation

We also have `CODEOWNERS` set on different parts of the repo and an approval by someone in the `CODEOWNERS` for the file(s) the PR is changing can also suffice.

### Who can merge a PR?

PRs can only be merged by members of the core team and Gatsbot.

#### Gatsbot

Gatsbot is our little android friend that automatically merges PRs that are ready to go. If a PR is approved and all checks are passing, add the `bot: merge on green` label and Gatsbot will merge it in automatically.

## Gotchas

- Sometimes you might want to fix something on someone else's PR. This is perfectly okay to do as long as the author doesn't mind. However, depending on their settings, you might find that you are not able to push to their fork. In such a case, just leave your changes as suggestions.

## Frequently Asked Questions

We don't have any at the moment but if you have one, feel free to contribute it here.
