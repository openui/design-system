# OpenUI Design System RFC

The OpenUI Design System is meant to provide a global, accessible, and themable design system for the web platform by creating high-quality and accessible components that work across any web framework.

The normal GitHub pull request workflow will be used to provide bug fixes and documentation improvements to existing components, however creating new components or significantly modifying existing ones by creating variations will need to have more thorough review/discussion.

This RFC (request for comments) process will allow anyone to submit issues using the provided template to begin discussions and provide the ability for new components to make their way into the design system.

## When to follow this process

It is necessary to follow the RFC process when you are intend to create any significant changes to the OpenUI Design System. Examples of these types of changes are:

* A change which provides significantly alters existing functionality, provides new functionality, or a new primative component.
* The removal of an existing feature or functionality

Another way to look at it is, if your suggested change will require a new semantic version, or breaking change to an existing feature, it will need to go through the RFC process.

This RFC process is a great way to get involved in the community, suggest new ideas, and discuss them with the community and contributors. It can also be started prior to any design or functionality has been finalized.

Changes that **do not** require an RFC are:
* Changes in documentation
* Rephrasing, reorganizing, or refactoring without any functional changes
* Additions to existing components which are strictly new improvements, accessibility updates, or are bug fixes.

## What the process is

To get a change into the design system, the RFC will first be merged into the repo under the `/rfcs/active` directory. At that point, work on inclusion of the code and documentation can begin. Once the RFC is accepted it will be moved into the `/rfcs/accepted` directory to provide history on the decision process for each component.

To create a new RFC you will:

* Fork the OpenUI Design System repo - https://github.com/openui/design-system
* Copy the `/rfcs/0000-template.md` file to `/rfcs/active` and rename it to `0000-proposed-component.md` where "proposed-component" is a descriptive title of your component.
* Fill out the RFC template with your suggestions. Be sure to take care into filling out each portion of the template. **RFCs that do not conform to the template, demonstrate understanding of the imipact of the update, or are disingenous about the impact or alternatives tend to be poorly received**
* Submit a pull request. Once it's a pull request, the RFC will receive feedback and discussion from the community. Don't worry about getting feedback, it serves to help make the process better. **Be prepared to update and revise your pull request based on community feedback.**
* Build conensus around your RFC by engaging with the community and their feedback. RFCs with broad support are much more likely to be accepted than those without any comments.
* RFCs which are candidates for inclusion will be tagged as such and enter a "final comment period" lasting no longer than a week.
* Any RFC may be modified based on feedback from the community. Significant modifications may trigger a new "final comment period".
* An RFC may be rejected by the community after public discussion has settled and the rationale for rejection has been provided in the comments on the pull request. Once this happens, the associated pull request will be closed by one of the moderators.
* An RFC may be accepted at the close of the "final comment period" without any significant changes or challenges. At this point it will be merged in and become Active.

## The RFC Lifecycle

Once an RFC becomes merged and active, the authors may implement it and submit the feature as a pull request to the repo. Becoming 'active' is not a guarantee the method of implementation will be accepted, nor does it mean the feature will automatically be merged. It means the work can begin, but additional community feedback and revisions are likely.

If during the process of implementing an RFC there are significant changes needed, the RFC can be re-opened in followup pull requests.

Once the feature is code complete, documentation done, and testing provided, a final pull request will be created to officially merge the feature into the next release. Part of this pull request will also need to move the RFC from the Active directory (`/rfcs/active`) to the Accepted directory (`/rfcs/accepted`).

## Implementing an RFC

The author of the RFC does not have to be the person to implement it, however they should be ready to help once it is set to active if they would like to see it finally accepted. All community members are also welcome to help with the implementation of any active RFC.

If you are interested in working on an active RFC, please engage the communtiy in the Discord channel to discuss how best to get started.

## Reviewing RFCs

The core team will review open RFC requests as they come in, and try to provide timely feedback. Weekly OpenUI meetings in Discord will likely be where this discussion occurs, but all final comments and findings will be put into the comments of the respective pull request.


**OpenUI's RFC process owes its inspiration to the [Carbon RFC Process], [React RFC Process], [Yarn RFC process], and the [Ember RFC Process]**

[Carbon RFC process]: https://github.comcarbon-design-system/rfcs/
[React RFC process]: https://github.com/reactjs/rfcs
[Yarn RFC process]: https://github.com/yarnpkg/rfcs
[Rust RFC process]: https://github.com/rust-lang/rfcs
[Ember RFC process]: https://github.com/emberjs/rfcs