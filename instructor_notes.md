# Instructor notes on the Game of Life activity

This is a living document of notes for instructors. "Living" means you
should feel free to make any changes, additions, updates, or otherwise
to this -- either by editing it right on GitHub, making a fork and PR,
or just leaving an issue in the repo.

Think of this like a wiki -- something that gets frequently updated and
modified, and remember [Wikipedia's "be bold" editing
guideline](https://en.wikipedia.org/wiki/Wikipedia:Be_bold).

## General notes




## Common problems

### Test runner not finding all tests

I've seen situations where the initial build seems to work fine, but
that's because the JUnit test runner doesn't find the tests, and
therefore doesn't throw any errors for failing tests. This seems to be
better after 40f44a8. For posterity, some comments from Paul in Slack:

> Ah, lovely: that previous commit pinned to 5.9 broken when a VS Code
> JUnit plugin update invisibly required ≥5.10 — but then apparently
> JUnit 5.12 broke the plugin. So going to the latest 5.x used to fix
> it…until JUnit 5.12 was released.
>
> Specifying 5.11.+ in build.gradle fixes it, but I fully expect it to
> break 3 days into class when the VS Code people update the JUnit
> plugin or something. This is ridiculous; investigating whether there’s
> a proper fix.
>
> Found my way back to this miserable thread:
> https://github.com/microsoft/vscode-java-test/issues/1740 Note the
> commits at the bottom: they’re still actively updating the VS Code
> extension to match specific minor versions of JUnit. AFAICT, that
> means (1) this problem will just keep occurring and (2) there’s diddly
> we can do about it.
>
> Aha, I think I dug up the magic incantation from a fix that Abby
> applied once (and no idea how they found it). Try adding
> the testRuntimeOnly clause so that your dependencies section looks like
> this:
>
> ```
> dependencies {
>    implementation group: 'com.github.mac-comp127',name: 'kilt-graphics', version: '1.+'
>    testImplementation group:'org.junit.jupiter', name: 'junit-jupiter', version: '5.+'
>    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
> }
> ```
>
> If that fixed it for you, I’ll mass-apply to all the course repos later
> tonight.

(It did seem to fix things: see 489d288.

## Interesting student-made rules

Just for fun, let's record any particularly interesting examples that
students come up with the optional make-up-your-own-rules activity.
