---
title: "Using version control"
order: 75
page_id: "version_control"
warning: false
updated: 2022-03-23
contextual_links:
  - type: section
    name: "Prerequisites"
  - type: link
    name: "Grouping requests in Collections"
    url: "/docs/sending-requests/intro-to-collections/"
  - type: section
    name: "Additional Resources"
  - type: subtitle
    name: "Videos"
  - type: link
    name: "Version Control for Collections | Postman Level Up"
    url: "https://www.youtube.com/watch?v=QKxukXJWRPI&list=PLM-7VG-sgbtC5tNXxd28cmePSa9BYwqeU&index=7"
  - type: subtitle
    name: "Blog Posts"
  - type: link
    name: "Introducing Environment Forking and Pull Requests"
    url: "https://blog.postman.com/introducing-environment-forking-and-pull-requests/"
  - type: link
    name: "Streamline the API Development Lifecycle with Postman Version Control"
    url: "https://blog.postman.com/streamline-api-development-lifecycle-with-postman-version-control/"
  - type: subtitle
    name: "Case Studies"
  - type: link
    name: "Youi"
    url: "https://www.postman.com/case-studies/youi/"
  - type: section
    name: "Next Steps"
  - type: link
    name: "Versioning APIs"
    url: "/docs/designing-and-developing-your-api/versioning-an-api/"
---

Postman's _version control_ features can help you and your team to collaboratively build an API. You can fork a collection or environment, make updates to the fork, create a pull request, and merge your changes into the parent element.

> Version control for collections and environments is different from API versioning. For information on managing multiple versions of APIs, see [Versioning APIs](/docs/designing-and-developing-your-api/versioning-an-api/).

* [Forking Postman entities](#forking-postman-entities)
    * [Creating a fork](#creating-a-fork)
    * [Viewing fork information](#viewing-fork-information)
* [Creating pull requests](#creating-pull-requests)
    * [Creating public pull requests](#creating-public-pull-requests)
    * [Pull request settings](#pull-request-settings)
* [Watching a pull request](#watching-a-pull-request)
* [Reviewing pull requests](#reviewing-pull-requests)
    * [Viewing the diff](#viewing-the-diff)
    * [Adding comments](#adding-comments)
    * [Editing or declining a pull request](#editing-or-declining-a-pull-request)
    * [Approving a pull request](#approving-a-pull-request)
    * [Pulling updates](#pulling-updates)
    * [Merging changes](#merging-changes)
* [Resolving conflicts](#resolving-conflicts)

## Forking Postman entities

A _fork_ is a new instance of an element that you can change without making any changes to the parent element. In Postman, you can fork collections, environments, and flows. Forking also enables you to contribute to an element without having an [Editor access](/docs/collaborating-in-postman/roles-and-permissions/#element-based-roles) for that element.

### Creating a fork

> To fork a collection, environment, or flow within a public workspace, you must enable your public profile in your [profile settings](https://go.postman.co/settings/me). For more information on making your profile public, see [Managing your account](/docs/getting-started/postman-account/#making-your-profile-public).

When you fork a Postman Collection, environment, or flow, you create a copy of it in a different workspace. You must sign in to Postman to create a fork.

To fork an element:

1. Select the element in the sidebar.
2. In the overview tab that appears, select **Fork** <img alt="Fork icon" src="https://assets.postman.com/postman-docs/icon-fork.jpg#icon" width="14px"> in the upper right.

    > You can also create a fork by hovering over the element in the sidebar and selecting the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> next to its name, then **Create a Fork**.

3. Enter a label for your fork, and select a workspace to save it to.
4. Select **Fork Collection**, **Fork Environment**, or **Fork Flow**.

    <img src="https://assets.postman.com/postman-docs/fork-collection-v9.1.jpg" alt="Create fork tab" width="400px"/>

Postman creates your fork in the selected workspace.

If there are any [mocks](/docs/designing-and-developing-your-api/mocking-data/setting-up-mock/) or [monitors](/docs/monitoring-your-api/intro-monitors/) associated with the parent element, they aren't linked to the forked element. You must create mocks and monitors specifically for the fork if you need them.

> If a collection is in a public workspace that you aren't a member of, you won't be able to send a request within that workspace. To send requests or make changes to a collection, you must fork the collection into a personal workspace or a team workspace that you belong to.

### Viewing fork information

Fork information shows details about forks and the users who have created them. You will be able to identify the users who are actively consuming and contributing to your APIs.

To access the list of users who have forked a collection, environment, or flow:

1. Select the number next to the fork icon <img alt="Fork icon" src="https://assets.postman.com/postman-docs/icon-fork.jpg#icon" width="14px"> to reveal the list of users who have active forks.

    <img alt="View the fork information count" src="https://assets.postman.com/postman-docs/fork-information-count-v9.12.jpg" width="400px"/>

To access the list of forks for a collection, environment, or flow:

1. Select the fork icon <img alt="Fork icon" src="https://assets.postman.com/postman-docs/icon-fork.jpg#icon" width="14px"> in the context bar.
1. Select the fork name under **Forks**.

    > You can also select the user's avatar under **Forks** to view the user's public profile.

    <img alt="View the list of forks" src="https://assets.postman.com/postman-docs/fork-information-list-v9.12.jpg" width="350px"/>

## Creating pull requests

> The pull request process isn't available for flows.

When you have made the changes that you want to a forked collection or environment, you can create a _pull request_. Creating a pull request means that you want to merge the changes you made in the forked element (the _source_) into the parent element (the _destination_). As part of the pull request process, you will request that reviewers look at your changes. Reviewers can make comments on your changes and will decide whether to approve them and merge them into the parent element.

To create a pull request:

1. Hover over the element in the sidebar.
1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> next to its name.

1. Select **Create pull request**.

    <img alt="Create Pull Request" src="https://assets.postman.com/postman-docs/create-pull-request.jpg" width="250px"/>

1. Select **Changes** to review the changes in the pull request.

    ![Pull Request Changes](https://assets.postman.com/postman-docs/pull-request-changes.jpg)

    * If the parent element has any changes since you last updated your fork, you can [pull those changes](#pulling-updates) into your fork before merging.

    * If there are any conflicts between the fork and the parent element, Postman highlights them so that you can [resolve them](#resolving-conflicts).

1. Select **Overview**.
1. Enter a title and description for your pull request, and select up to 50 reviewers from the dropdown list. Reviewers must have [Editor access](/docs/collaborating-in-postman/roles-and-permissions/#element-based-roles) on the element to merge your changes.
1. Select **Create Pull Request**.

    <img alt="Create Pull Request" src="https://assets.postman.com/postman-docs/pull-request-overview.jpg" width="350px"/>

Postman notifies the reviewers you selected about your pull request. You will receive a notification if the reviewers [comment on](#adding-comments), [approve](#approving-a-pull-request), or [merge](#merging-changes-from-a-pull-request) the pull request.

> A reviewer must have an Editor role for the element to merge changes. If you add a user who doesn't have Editor access as a reviewer, there will be a warning icon next to their name.
>
> <img alt="Reviewer permission" src="https://assets.postman.com/postman-docs/pull-request-reviewer-permission.jpg" width="350px"/>

### Creating public pull requests

To create a pull request on a public collection or environment, you must fork the parent element into a public workspace so that the users you ask to [review it](#reviewing-pull-requests) have access to it.

1. Begin the pull request process described in [Creating pull requests](#creating-pull-requests). A note tells you to move the source element to a public workspace.
1. Select the public workspace where you want to move the element.
1. Select **Move Collection** or **Move Environment**.

    <img src="https://assets.postman.com/postman-docs/make-source-collection-public-v9.jpg" alt="Make the source collection public" width="400px"/>

1. After you move the fork to a public workspace, proceed with the workflow in [Creating pull requests](#creating-pull-requests).

Once you create the pull request, you will get a notification that it was **Shared to public workspace**.

### Pull request settings

> Pull request settings are available on [Postman Professional and Enterprise plans](https://www.postman.com/pricing).

Pull request settings let you manage permissions for reviewers and assign merge checks.

#### Manage reviewer permissions

1. Hover over the element in the sidebar.
1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> next to its name.
1. Select **Manage roles**.

    <img alt="Collection Manage Roles" src="https://assets.postman.com/postman-docs/collection-manage-roles-v9.1.jpg" width="300px"/>

1. Select **Editor** for the users you want to give Editor access to.
1. Select **Update Roles**.

    [![manage roles](https://assets.postman.com/postman-docs/manage-roles-collection-v9.12.jpg)](https://assets.postman.com/postman-docs/manage-roles-collection-v9.12.jpg)

#### Assign merge checks

For collections, you can assign merge checks before approving changes.

There are two different types of checks that you can enable for a pull request:

* **Approved once** - You need at least one approval to merge the pull request.
* **Approved by a collection editor** - You need the approval of a user who has [Editor access for the collection](/docs/collaborating-in-postman/roles-and-permissions/#collection-roles) to merge the pull request.

To set merge checks for pull requests on a specific collection:

1. Hover over the collection in the sidebar.
1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> next to its name.
1. Select **Manage roles**.
1. Select the merge checks that you want to set for the collection.

<img alt="Merge Check" src="https://assets.postman.com/postman-docs/manage-roles-set-merge-checks.jpg" width="800px"/>

If the merge conditions for a pull request aren't met, the option to **Merge** it into the parent collection will be active.

<img alt="Merge option isn't active" src="https://assets.postman.com/postman-docs/view-merge-conditions-v9.12.jpg" width="300px"/>

For information about the pull request's merge conditions, select **View Merge Conditions**.

<img alt="Merge Condition" src="https://assets.postman.com/postman-docs/merge-conditions.jpg" width="400px"/>

## Watching a pull request

The watch option enables you to receive an in-app notification when a team member modifies the pull request. If you watch a pull request, you will get notifications about actions such as adding a new comment, approving or removing approval, merging, and editing or declining a pull request.

To watch a pull request:

1. Select **Watch**.

<img alt="Watch a pull request" src="https://assets.postman.com/postman-docs/watching-a-pull-request-v9.12.jpg" width="300px"/>

To change your watching notification settings:

1. Select **Watching**.
1. Select or clear the desired notification options.

<img alt="Conditions for watch notifications" src="https://assets.postman.com/postman-docs/watching-conditions-notifications-v9.jpg" width="350px"/>

To view notifications for a watched pull request:

1. Select the notifications icon <img alt="Notifications icon" src="https://assets.postman.com/postman-docs/icon-notification-bell-v9.jpg#icon" width="18px"> in the Postman header. The popup indicates further information about the changes  to the pull request.

> If you create a pull request and make changes to it from the same Postman account, you won't receive any notifications about changes made to the pull request.

## Reviewing pull requests

If you're tagged as a reviewer on a pull request, you can view the changes, comment, approve or decline the request, and merge the forked collection or environment into the parent element.

To access the list of pull requests:

1. Go to the element and select the pull requests icon <img alt="Pull request icon" src="https://assets.postman.com/postman-docs/icon-pull-request.jpg#icon" width="16px"> in the context bar.

<img src="https://assets.postman.com/postman-docs/open-pull-request-list-v9.12.jpg" alt="Pull request list" width="350px"/>

Each item shows the pull request's status, which will be `OPEN` for any that haven't been merged or declined. Select a pull request's name to open it.

### Viewing the diff

When you review a pull request, it's important to understand the changes that the pull request will introduce into the parent collection or environment. The difference between the fork and the parent element is called the _diff_.

To view the diff:

1. In the pull request, view the diff under the **Changes** heading.

<img alt="View diff when reviewing pull request" src="https://assets.postman.com/postman-docs/pull-request-review-view-diff-v9.12.jpg" width="450px"/>

The diff will tell you whether a change is an addition, a deletion, or a modification. You can use the **Jump to** pane on the right side of the pull request to open the folders and API requests included in the pull request.

### Adding comments

Adding comments as a reviewer is an important part of the pull request process, facilitating meaningful conversations and allowing stakeholders to have a voice in the process.

To add a comment to a pull request:

1. Select the comment icon <img alt="Comments icon" src="https://assets.postman.com/postman-docs/icon-comments-v9.jpg#icon" width="18px"> next to the change that you want to comment on.
1. Once you've written your comment, select **Add Comment**.

<img alt="Add a comment to a pull review" src="https://assets.postman.com/postman-docs/pr-add-comment-v9.12.jpg" width="450px"/>

> To tag another user in your comment, use the **@** symbol before their username.

### Editing or declining a pull request

You can edit a pull request's details before approving it, or you can decline it.

<img alt="Refresh, edit, or decline a pull request" src="https://assets.postman.com/postman-docs/refresh-edit-decline-pull-request.jpg" width="350px"/>

To edit the pull request details:

1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> at the upper right and select **Edit**.
1. Make any changes to the pull request's title, description, and list of reviewers.
1. Select **Save Changes**.

If you don't want to merge the pull request into the parent element, you can decline it. You can't reopen a pull request that you have declined, so if you want to request edits or offer feedback, [add a comment](#adding-comments) instead. To decline the pull request:

1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> at the upper right and select **Decline**.
1. Select **Decline Pull Request**.

### Approving a pull request

If you're tagged as a reviewer on a pull request you can approve the pull request.

To approve a pull request, select **Approve**.

> If you need to revoke your approval, select **Unapprove**.

<img alt="Approve a pull request" src="https://assets.postman.com/postman-docs/pull-request-approve-v9.12.jpg" width="300px"/>

After you approve the pull request, its status in the list of pull requests is **Approved**.

<img src="https://assets.postman.com/postman-docs/pull-request-list-approved-v9.12.jpg" alt="Approved pull request" width="350px"/>

### Pulling updates

You can keep your forked collections and environments up to date with any changes to the parent element, for example if another team member has merged changes into the parent element.

1. Open the pull request. Postman will warn you that the parent element has changed since you last updated it.
1. Select **Pull Changes** to update your fork with the changes to the parent element.

![Pull recent changes](https://assets.postman.com/postman-docs/pr-pull-changes-v9.12.jpg)

### Merging changes

When you are ready to add the changes from a pull request or fork, you will _merge_ them into the parent collection or environment.

#### Merging changes from a pull request

After the requested reviewer approves a pull request, you can merge it into the parent element.

1. From the approved pull request, select **Merge**.

    ![Merge a pull request](https://assets.postman.com/postman-docs/pull-request-merge-fork-v9.12.jpg)

    > If the parent element has any changes since you last updated your fork, you can [pull those changes](#pulling-updates) before merging.

1. Select one of the following merge options:
    * **Merge changes** - Merge the changes into the parent element. This doesn't make any changes to the fork. You must have Editor access to the parent element.
    * **Merge changes and update source** - Merge the changes into the parent element. Any differences in the parent element are also made to the fork. You must have Editor access to both the parent and forked entities.
    * **Merge changes and delete source** - Merge the changes into the parent element. After the merge process is complete, Postman deletes the fork. You must have Editor access to both the parent and forked entities.

    <img src="https://assets.postman.com/postman-docs/merge-fork-options-v9.12.jpg" alt="Merge Fork Options" width="400px"/>

1. Select **Merge**.

#### Merging changes from a fork

If you have Editor access on the element, you can merge a fork into the parent element without going through the [pull request process](#creating-pull-requests). For example, if you’re using forks in a personal workspace to organize your work, you can merge changes in a fork directly back into the parent element. If you are collaborating with others, though, merging directly lacks the safeguards built into the pull request process. Many teams require pull requests as part of their version control workflow.

To merge changes from a fork without opening a pull request:

1. Hover over the fork in the sidebar.
1. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> next to its name.

1. Select **Merge changes**.
1. Review the diff and select **Merge all changes**.

    ![Merge Fork](https://assets.postman.com/postman-docs/merge-fork-collection-change-v2.jpg)

1. Proceed with the merge process described in [Merging changes from a pull request](#merging-changes-from-a-pull-request).

## Resolving conflicts

A merge conflict happens when you try to merge changes into an updated parent element and Postman isn't able to automatically resolve the differences between the two. If there's a conflict when you try to merge a fork, you will need to decide how you want to resolve them before continuing.

> Merge conflicts can involve changes in more than one workspace.

To resolve a merge conflict:

1. Look at the differences between the two entities. The **Source** line shows the changes on your fork, and the **Destination** line shows the changes on the parent element.
1. Select **Use this** next to the version you want to include when you merge.

<img src="https://assets.postman.com/postman-docs/conflicts-pull-changes-v2.jpg" alt="Pull Changes" width="450px"/>

After you resolve the conflicts, select **Pull changes** to [pull the updates](#pulling-updates).
