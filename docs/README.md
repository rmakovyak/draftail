# Draftail documentation

> :warning: Have a look at [draftail.org](https://www.draftail.org/).

## Editor behavior

### Expected behavior

- Pressing return on an empty list item should un-indent it until it is not nested, and then remove it.
- Pressing return at the end of a block should create an empty unstyled block.
- Atomic blocks (images, embeds, `hr`) are always preceded and followed by a block (empty if no other block is present). See [facebook/draft-js#327](https://github.com/facebook/draft-js/issues/327).
- Blocks starting with "- ", "\* ", "1. " are automatically converted to list items.
- Pasting content with block nesting above the configured maximum should reduce the depth up to the maximum.

## Upgrade considerations

### Draft.js

Draft.js is relatively stable but also historically slow to address bugs. Draftail sometimes has to override behavior in a way that may be problematic if the Draft.js API is updated.

When upgrading to a more recent Draft.js version, always review the full [CHANGELOG](https://github.com/facebook/draft-js/blob/master/CHANGELOG.md) as well as individual changes.

Here are specific parts of the code that **should always be reviewed before upgrading**, and may need to be updated, or that we may be able to remove:

- https://github.com/springload/draftail/blob/df903f86c882bd5101eb05e152e8b8a8b9a4915e/lib/blocks/MediaBlock.js#L60-L71
- https://github.com/springload/draftail/commit/431c3fd09c4cfc043c8b334544b05b9f580b75d2
- https://github.com/springload/draftail/blob/df903f86c882bd5101eb05e152e8b8a8b9a4915e/lib/api/behavior.js#L100-L110
- https://github.com/springload/draftail/blob/df903f86c882bd5101eb05e152e8b8a8b9a4915e/lib/api/behavior.js#L23:L26
- https://github.com/springload/draftail/commit/88ae9adcda1929c92f065655a03c1b33fcfe6c2d
- https://github.com/springload/draftail/commit/e05df07f8ed6c5df65c79824bbb1dcd6e8800bdd
- Type errors silenced with `$FlowFixMe`

## Troubleshooting

- In Firefox, the [`dom.event.clipboardevents.enabled`](https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Preference_reference/dom.event.clipboardevents.enabled) setting must be turned on, otherwise the editor will crash on copy-paste. This could be off in [Iceweasel](https://wiki.debian.org/Iceweasel). See [wagtail/wagtail#4346](https://github.com/wagtail/wagtail/issues/4346).
