---
layout: page
title: Build Metadata Reference
redirect_from:
 - /manual/html_node/Metadata.html

---

Information used by update.py to compile the public index comes from two
sources:

1.  the APK files in the repo directory, and
2.  the metadata files in the metadata directory.

The original metadata files are simple, easy to edit text files, always
named as the application’s package ID with ’.txt’ appended.
Additionally, you can use JSON, XML, or YAML for app metadata, using the
same fields as the original ’.txt’ format.

Note that although the metadata files are designed to be easily read and
writable by humans, they are also processed and written by various
scripts. The original ’.txt’ format can be automatically cleaned up when
necessary. The structure and comments will be preserved correctly,
although the order of fields will be standardised. (In the event that
the original file was in a different order, comments are considered as
being attached to the field following them). In fact, you can
standardise all the ’.txt’ metadata in a single command, without
changing the functional content, by running:

```
fdroid rewritemeta
```

Or just run it on a specific app:

```
fdroid rewritemeta org.adaway
```

The following sections describe the fields recognised within the file.

- [Categories](#Categories)
- [Author Name](#Author-Name)
- [Author Email](#Author-Email)
- [License](#License)
- [Auto Name](#Auto-Name)
- [Name](#Name)
- [Provides](#Provides)
- [Web Site](#Web-Site)
- [Source Code](#Source-Code)
- [Issue Tracker](#Issue-Tracker)
- [Changelog](#Changelog)
- [Donate](#Donate)
- [FlattrID](#FlattrID)
- [Bitcoin](#Bitcoin)
- [Litecoin](#Litecoin)
- [Summary](#Summary)
- [Description](#Description)
- [Maintainer Notes](#Maintainer-Notes)
- [Repo Type](#Repo-Type)
- [Repo](#Repo)
- [Binaries](#Binaries)
- [Build](#Build)
- [AntiFeatures](#AntiFeatures)
- [Disabled](#Disabled)
- [Requires Root](#Requires-Root)
- [Archive Policy](#Archive-Policy)
- [Update Check Mode](#Update-Check-Mode)
- [Update Check Ignore](#Update-Check-Ignore)
- [Vercode Operation](#Vercode-Operation)
- [Update Check Name](#Update-Check-Name)
- [Update Check Data](#Update-Check-Data)
- [Auto Update Mode](#Auto-Update-Mode)
- [Current Version](#Current-Version)
- [Current Version Code](#Current-Version-Code)
- [No Source Since](#No-Source-Since)



### 7.1 Categories<a name="Categories"></a>


Any number of categories for the application to be placed in. There is
no fixed list of categories - both the client and the web site will
automatically show any categories that exist in any applications.
However, if your metadata is intended for the main F-Droid repository,
you should use one of the existing categories (look at the site/client),
or discuss the proposal to add a new one.

Categories must be separated by a single comma character, ’,’. For
backwards compatibility, F-Droid will use the first category given as
&lt;category&gt; element for older clients to at least see one category.

This is converted to (`<categories>`) in the XML file (_index.xml_).



### 7.2 Author Name<a name="Author-Name"></a>


The name of the author, either full, abbreviated or pseudonym. If
present, it should represent the name(s) as published by upstream, e.g.
in their copyright or authors file. This can be omitted (or left blank).

This is converted to (`<author>`) in the XML file (_index.xml_).



### 7.3 Author Email<a name="Author-Email"></a>


The e-mail address of the author(s). This can be omitted (or left
blank).

This is converted to (`<email>`) in the XML file (_index.xml_).



### 7.4 License<a name="License"></a>


The overall license for the application, or in certain cases, for the
source code only. Values should correspond to short identifiers of the
[SPDX](https://spdx.org/licenses/) license list. In some cases an
older, non-standard naming scheme is still used.

This is converted to (`<license>`) in the XML file (_index.xml_).



### 7.5 Auto Name<a name="Auto-Name"></a>


The name of the application as can best be retrieved from the source
code. This is done so that the commitupdates script can put a familiar
name in the description of commits created when a new update of the
application is found. The Auto Name entry is generated automatically
when `fdroid checkupdates` is run.

This is converted to (`<name>`) in the XML file (_index.xml_).



### 7.6 Name<a name="Name"></a>


The name of the application. Normally, this field should not be present
since the application’s correct name is retrieved from the APK file.
However, in a situation where an APK contains a bad or missing
application name, it can be overridden using this. Note that this only
overrides the name in the list of apps presented in the client; it
doesn’t changed the name or application label in the source code.

This is converted to (`<name>`) in the XML file (_index.xml_).



### 7.7 Provides<a name="Provides"></a>


Comma-separated list of application IDs that this app provides. In other
words, if the user has any of these apps installed, F-Droid will show
this app as installed instead. It will also appear if the user clicks on
urls linking to the other app IDs. Useful when an app switches package
name, or when you want an app to act as multiple apps.

Currently this functionality is a stub.

This is converted to (`<provides>`) in the XML file (_index.xml_).



### 7.8 Web Site<a name="Web-Site"></a>


The URL for the application’s web site. If there is no relevant web
site, this can be omitted (or left blank).

This is converted to (`<web>`) in the XML file (_index.xml_).



### 7.9 Source Code<a name="Source-Code"></a>


The URL to view or obtain the application’s source code. This should be
something human-friendly. Machine-readable source-code is covered in the
’Repo’ field.

This is converted to (`<source>`) in the XML file (_index.xml_).



### 7.10 Issue Tracker<a name="Issue-Tracker"></a>


The URL for the application’s issue tracker. Optional, since not all
applications have one.

This is converted to (`<tracker>`) in the XML file (_index.xml_).



### 7.11 Changelog<a name="Changelog"></a>


The URL for the application’s changelog. Optional, since not all
applications have one.

This is converted to (`<changelog>`) in the XML file (_index.xml_).



### 7.12 Donate<a name="Donate"></a>


The URL to donate to the project. This should be the project’s donate
page if it has one.

It is possible to use a direct PayPal link here, if that is all that is
available. However, bear in mind that the developer may not be aware of
that direct link, and if they later changed to a different PayPal
account, or the PayPal link format changed, things could go wrong. It is
always best to use a link that the developer explicitly makes public,
rather than something that is auto-generated ’button code’.

This is converted to (`<donate>`) in the XML file (_index.xml_).



### 7.13 FlattrID<a name="FlattrID"></a>


The project’s Flattr (http://flattr.com) ID, if it has one. This should
be a numeric ID, such that (for example) https://flattr.com/thing/xxxx
leads directly to the page to donate to the project.

This is converted to (`<flattr>`) in the XML file (_index.xml_).



### 7.14 Bitcoin<a name="Bitcoin"></a>


A bitcoin address for donating to the project.

This is converted to (`<bitcoin>`) in the XML file (_index.xml_).



### 7.15 Litecoin<a name="Litecoin"></a>


A litecoin address for donating to the project.

This is converted to (`<litecoin>`) in the XML file (_index.xml_).



### 7.16 Summary<a name="Summary"></a>


A brief summary of what the application is. Since the summary is only
allowed one line on the list of the F-Droid client, keeping it to within
80 characters will ensure it fits most screens.

This is converted to (`<summary>`) in the XML file (_index.xml_).



### 7.17 Description<a name="Description"></a>


A full description of the application, relevant to the latest version.
This can span multiple lines (which should be kept to a maximum of 80
characters), and is terminated by a line containing a single ’.’.

Basic MediaWiki-style formatting can be used. Leaving a blank line
starts a new paragraph. Surrounding text with `''` make it italic, and
with `'''` makes it bold.

You can link to another app in the repo by using `[[app.id]]`. The link
will be made appropriately whether in the Android client, the web repo
browser or the wiki. The link text will be the apps name.

Links to web addresses can be done using `[http://example.com Text]`.

Bulletted lists are done by simply starting each item with a `*` on a
new line, and numbered lists are the same but using `#`. There is
currently no support for nesting lists - you can have one level only.

It can be helpful to note information pertaining to updating from an
earlier version; whether the app contains any prebuilts built by the
upstream developers or whether non-free elements were removed; whether
the app is in rapid development or whether the latest version lags
behind the current version; whether the app supports multiple
architectures or whether there is a maximum SDK specified (such info not
being recorded in the index).

This is converted to (`<desc>`) in the XML file (_index.xml_).



### 7.18 Maintainer Notes<a name="Maintainer-Notes"></a>


This is a multi-line field using the same rules and syntax as the
description. It’s used to record notes for F-Droid maintainers to assist
in maintaining and updating the application in the repository.

This information is also published to the wiki.



### 7.19 Repo Type<a name="Repo-Type"></a>


The type of repository - for automatic building from source. If this is
not specified, automatic building is disabled for this application.
Possible values are:

-   ‘git’
-   ‘svn’
-   ‘git-svn’
-   ‘hg’
-   ‘bzr’
-   ‘srclib’



### 7.20 Repo<a name="Repo"></a>


The repository location. Usually a git: or svn: URL, for example.

The git-svn option connects to an SVN repository, and you specify the
URL in exactly the same way, but git is used as a back-end. This is
preferable for performance reasons, and also because a local copy of the
entire history is available in case the upstream repository disappears.
(It happens!). In order to use Tags as update check mode for this VCS
type, the URL must have the tags= special argument set. Likewise, if you
intend to use the RepoManifest/branch scheme, you would want to specify
branches= as well. Finally, trunk= can also be added. All these special
arguments will be passed to "git svn" in order, and their values must be
relative paths to the svn repo root dir. Here’s an example of a complex
git-svn Repo URL:
http://svn.code.sf.net/p/project/code/svn;trunk=trunk;tags=tags;branches=branches

If the Repo Type is `srclib`, then you must specify the name of the
according srclib .txt file. For example if `scrlibs/FooBar.txt` exist
and you want to use this srclib, then you have to set Repo to `FooBar`.



### 7.21 Binaries<a name="Binaries"></a>


The location of binaries used in verification process.

If specified, F-Droid will verify the output apk file of a build against
the one specified. You can use %v and %c to point to the version name
and version code of the current build. To verify the F-Droid client
itself you could use:
`Binaries:https://f-droid.org/repo/org.fdroid.fdroid_%c.apk`

F-Droid will use upstream binaries if the verification succeeded.



### 7.22 Build<a name="Build"></a>


Any number of these fields can be present, each specifying a version to
automatically build from source. The value is a comma-separated list.
For example:

‘Build:1.2,12’

The above specifies to build version 1.2, which has a version code of
12. The `commit=` parameter specifies the tag, commit or revision number
from which to build it in the source repository. It is the only
mandatory flag, which in this case could for example be `commit=v1.2`.

In addition to the three, always required, parameters described above,
further parameters can be added (in name=value format) to apply further
configuration to the build. These are (roughly in order of application):

`disable=<message>`

:   Disables this build, giving a reason why. (For backwards
    compatibility, this can also be achieved by starting the commit ID
    with ’!’)

    The purpose of this feature is to allow non-buildable releases (e.g.
    the source is not published) to be flagged, so the scripts don’t
    generate repeated messages about them. (And also to record the
    information for review later). If an apk has already been built,
    disabling causes it to be deleted once `fdroid update` is run; this
    is the procedure if ever a version has to be replaced.

`subdir=<path>`

:   Specifies to build from a subdirectory of the checked out source
    code. Normally this directory is changed to before building,

`submodules=yes`

:   Use if the project (git only) has submodules - causes
    `git submodule update --init --recursive` to be executed after the
    source is cloned. Submodules are reset and cleaned like the main app
    repository itself before each build.

`init=xxxx`

:   As for ’prebuild’, but runs on the source code BEFORE any other
    processing takes place.

    You can use \$\$SDK\$\$, \$\$NDK\$\$, \$\$MVN3\$\$ and \$\$QT\$\$ to
    substitute the paths to the android SDK and NDK directories, maven 3
    executable, and Qt SDK directory respectively. The following
    per-build variables are available likewise: \$\$VERSION\$\$,
    \$\$VERCODE\$\$ and \$\$COMMIT\$\$.

`oldsdkloc=yes`

:   The sdk location in the repo is in an old format, or the build.xml
    is expecting such. The ’new’ format is sdk.dir while the VERY OLD
    format is sdk-location. Typically, if you get a message along the
    lines of: "com.android.ant.SetupTask cannot be found" when trying to
    build, then try enabling this option.

`target=<target>`

:   Specifies a particular SDK target for compilation, overriding the
    value defined in the code by upstream. This has different effects
    depending on what build system used — this flag currently affects
    Ant, Maven and Gradle projects only. Note that this does not change
    the target SDK in the AndroidManifest.xml, which determines the
    level of features that can be included in the build.

    In the case of an Ant project, it modifies project.properties of the
    app and possibly sub-projects. This is likely to cause the whole
    build.xml to be rewritten, which is fine if it’s a ’standard’
    android file or doesn’t already exist, but not a good idea if it’s
    heavily customised.

`update=<auto/dirs>`

:   By default, ’android update’ is used in Ant builds to generate or
    update the project and all its referenced projects. Specifying
    update=no bypasses that. Note that this is useless in builds that
    don’t use Ant.

    Default value is ’`auto`’, which recursively uses the paths in
    project.properties to find all the subprojects to update.

    Otherwise, the value can be a comma-separated list of directories in
    which to run ’android update’ relative to the application directory.

`encoding=xxxx`

:   Adds a java.encoding property to local.properties with the
    given value. Generally the value will be ’utf-8’. This is picked up
    by the SDK’s ant rules, and forces the Java compiler to interpret
    source files with this encoding. If you receive warnings during the
    compile about character encodings, you probably need this.

`forceversion=yes`

:   If specified, the package version in AndroidManifest.xml is replaced
    with the version name for the build as specified in the metadata.

    This is useful for cases when upstream repo failed to update it for
    specific tag; to build an arbitrary revision; to make it apparent
    that the version differs significantly from upstream; or to make it
    apparent which architecture or platform the apk is designed to
    run on.

`forcevercode=yes`

:   If specified, the package version code in the AndroidManifest.xml is
    replaced with the version code for the build. See also forceversion.

`rm=<path1>[,<path2>,...]`

:   Specifies the relative paths of files or directories to delete
    before the build is done. The paths are relative to the base of the
    build directory - i.e. the root of the directory structure checked
    out from the source respository - not necessarily the directory that
    contains AndroidManifest.xml.

    Multiple files/directories can be specified by separating them with
    ’,’. Directories will be recursively deleted.

`extlibs=<lib1>[,<lib2>,...]`

:   Comma-separated list of external libraries (jar files) from the
    `build/extlib` library, which will be placed in the `libs` directory
    of the project.

`srclibs=[n:]a@r,[n:]b@r1,...`

:   Comma-separated list of source libraries or Android projects. Each
    item is of the form name@rev where name is the predefined source
    library name and rev is the revision or tag to use in the respective
    source control.

    For Ant projects, you can optionally append a number with a colon at
    the beginning of a srclib item to automatically place it in
    project.properties as a library under the specified number. For
    example, if you specify `1:somelib@1.0`, F-Droid will automatically
    do the equivalent of the legacy practice
    `prebuild=echo "android.library.reference.1=$$somelib$$" >> project.properties`.

    Each srclib has a metadata file under srclibs/ in the repository
    directory, and the source code is stored in build/srclib/. Repo
    Type: and Repo: are specified in the same way as for apps; Subdir:
    can be a comma separated list, for when directories are renamed by
    upstream; Update Project: updates the projects in the working
    directory and one level down; Prepare: can be used for any kind of
    preparation: in particular if you need to update the project with a
    particular target. You can then also use \$\$name\$\$ in the
    init/prebuild/build command to substitute the relative path to the
    library directory, but it could need tweaking if you’ve changed into
    another directory.

    Currently srclibs are necessary when upstream uses jar files or
    pulls dependencies from non-trusted repositories. While there is no
    guarantee that those binaries are free and correspondent to the
    source code, F-Droid allows the following known repositories until a
    source-built alternative is available:

    -   ‘mavenCentral’ - the original repo, hardcoded in Maven
        and Gradle.
    -   ‘jCenter’ - hardcoded in Gradle, this repo by Bintray tries to
        provide easier handling. It should sync with mavenCentral from
        time to time.
    -   ‘OSS Sonatype’ - maintained by the people behind mavenCentral,
        this repository focuses on hosting services for open source
        project binaries.
    -   ‘OSS JFrog’ - maintained by the people behind jCenter, this
        repository focuses on hosting services for open source project
        binaries.
    -   ‘JitPack.io’ - builds directly from Github repositories.
        However, they do not provide any option to reproduce or verify
        the resulting binaries. Builds pre-release versions in
        some cases.
    -   ‘Clojars’ - Clojure libraries repo.
    -   ‘CommonsWare’ - repo holding a collection of open-source libs.

`patch=x`

:   Apply patch(es). ’x’ names one (or more - comma-seperated) files
    within a directory below the metadata, with the same name as the
    metadata file but without the extension. Each of these patches is
    applied to the code in turn.

`prebuild=xxxx`

:   Specifies a shell command (or commands - chain with &&) to run
    before the build takes place. Backslash can be used as an escape
    character to insert literal commas, or as the last character on a
    line to join that line with the next. It has no special meaning in
    other contexts; in particular, literal backslashes should not
    be escaped.

    The command runs using bash.

    Note that nothing should be built during this prebuild phase -
    scanning of the code and building of the source tarball, for
    example, take place after this. For custom actions that actually
    build things or produce binaries, use ’build’ instead.

    You can use \$\$name\$\$ to substitute the path to a referenced
    srclib - see the `srclib` directory for details of this.

    You can use \$\$SDK\$\$, \$\$NDK\$\$ and \$\$MVN3\$\$ to substitute
    the paths to the android SDK and NDK directories, and Maven 3
    executable respectively e.g. for when you need to run
    `android update project` explicitly. The following per-build
    variables are available likewise: \$\$VERSION\$\$, \$\$VERCODE\$\$
    and \$\$COMMIT\$\$.

`scanignore=<path1>[,<path2>,...]`

:   Enables one or more files/paths to be excluded from the scan
    process. This should only be used where there is a very good reason,
    and probably accompanied by a comment explaining why it
    is necessary.

    When scanning the source tree for problems, matching files whose
    relative paths start with any of the paths given here are ignored.

`scandelete=<path1>[,<path2>,...]`

:   When running the scan process, any files that trigger errors - like
    binaries - will be removed. It acts just like scanignore=, but
    instead of ignoring the files, it removes them.

    Useful when a source code repository includes binaries or other
    unwanted files which are not needed for the build. Instead of
    removing them manually via rm=, using scandelete= is easier.

`build=xxxx`

:   As for ’prebuild’, but runs during the actual build phase (but
    before the main Ant/Maven build). Use this only for actions that do
    actual building. Any prepartion of the source code should be done
    using ’init’ or ’prebuild’.

    Any building that takes place before build= will be ignored, as
    either Ant, mvn or gradle will be executed to clean the build
    environment right before build= (or the final build) is run.

    You can use \$\$SDK\$\$, \$\$NDK\$\$ and \$\$MVN3\$\$ to substitute
    the paths to the android SDK and NDK directories, and maven 3
    executable respectively. The following per-build variables are
    available likewise: \$\$VERSION\$\$, \$\$VERCODE\$\$
    and \$\$COMMIT\$\$.

`buildjni=[yes|no|<dir list>]`

:   Enables building of native code via the ndk-build script before
    doing the main Ant build. The value may be a list of directories
    relative to the main application directory in which to run
    ndk-build, or ’yes’ which corresponds to ’.’ . Using explicit list
    may be useful to build multi-component projects.

    The build and scan processes will complain (refuse to build) if this
    parameter is not defined, but there is a `jni` directory present. If
    the native code is being built by other means like a Gradle task,
    you can specify `no` here to avoid that. However, if the native code
    is actually not required or used, remove the directory instead
    (using `rm=jni` for example). Using `buildjni=no` when the jni code
    isn’t used nor built will result in an error saying that native
    libraries were expected in the resulting package.

`ndk=<version>`

:   Version of the NDK to use in this build. Defaults to the latest NDK
    release that included legacy toolchains, so as to not break builds
    that require toolchains no longer included in current versions of
    the NDK.

    The buildserver supports r9b with its legacy toolchains, r10e, r11c
    r12b, and the latest release as of writing this document, r13b. You may
    add support for more versions by adding them to ’ndk\_paths’ in your
    config file.

`gradle=<flavour1>[,<flavour2>,...]`

:   Build with Gradle instead of Ant, specifying what flavours to use.
    Flavours are case sensitive since the path to the output apk is
    as well.

    If only one flavour is given and it is ’yes’, no flavour will be
    used. Note that for projects with flavours, you must specify at
    least one valid flavour since ’yes’ will build all of
    them separately.

`maven=yes[@<dir>]`

:   Build with Maven instead of Ant. An extra @&lt;dir&gt; tells F-Droid
    to run Maven inside that relative subdirectory. Sometimes it is
    needed to use @.. so that builds happen correctly.

`preassemble=<task1>[,<task2>,...]`

:   List of Gradle tasks to be run before the assemble task in a Gradle
    project build.

`gradleprops=<prop1>[,<prop2>,...]`

:   List of Gradle properties to pass via the command line to Gradle. A
    property can be of the form `foo` or of the form `key=value`.

    For example: `gradleprops=enableFoo,someSetting=bar` will result in
    `gradle -PenableFoo -PsomeSetting=bar`.

`antcommands=<target1>[,<target2>,...]`

:   Specify an alternate set of Ant commands (target) instead of the
    default ’release’. It can’t be given any flags, such as the path to
    a build.xml.

`output=glob/to/output.apk`

:   Specify a glob path where the resulting unsigned release apk from
    the build should be. This can be used in combination with build
    methods like `gradle=yes` or `maven=yes`, but if no build method is
    specified, the build is manual. You should run your build commands,
    such as `make`, in `build=`.

`novcheck=yes`

:   Don’t check that the version name and code in the resulting apk are
    correct by looking at the build output - assume the metadata
    is correct. This takes away a useful level of sanity checking, and
    should only be used if the values can’t be extracted.

Another example, using extra parameters:

‘Build Version:1.09.03,10903,45,subdir=Timeriffic,oldsdkloc=yes’



### 7.23 AntiFeatures<a name="AntiFeatures"></a>


This is optional - if present, it contains a comma-separated list of any
of the following values, describing an anti-feature the application has.
It is a good idea to mention the reasons for the anti-feature(s) in the
description:

-   ‘Ads’ - the application contains advertising.
-   ‘Tracking’ - the application tracks and reports your activity to
    somewhere without your consent. It’s commonly used for when
    developers obtain crash logs without the user’s consent, or when an
    app is useless without some kind of authentication.
-   ‘NonFreeNet’ - the application relies on computational services that
    are impossible to replace or that the replacement cannot be
    connected to without major changes to the app.
-   ‘NonFreeAdd’ - the application promotes non-free add-ons, such that
    the app is effectively an advert for other non-free software.
-   ‘NonFreeDep’ - the application depends on a non-free application
    (e.g. Google Maps) - i.e. it requires it to be installed on the
    device, but does not include it.
-   ‘UpstreamNonFree’ - the application is or depends on non-free
    software. This does not mean that non-free software is included with
    the app: Most likely, it has been patched in some way to remove the
    non-free code. However, functionality may be missing.
-   ‘NonFreeAssets’ - the application contains and makes use of
    non-free assets. The most common case is apps using artwork -
    images, sounds, music, etc - under a non-commercial license.
-   ‘KnownVuln’ - the application has known security vulnerabilities.

This is converted to (`<antifeatures>`) in the XML file (_index.xml_).



### 7.24 Disabled<a name="Disabled"></a>


If this field is present, the application does not get put into the
public index. This allows metadata to be retained while an application
is temporarily disabled from being published. The value should be a
description of why the application is disabled. No apks or source code
archives are deleted: to purge an apk see the Build Version section or
delete manually for developer builds. The field is therefore used when
an app has outlived it’s usefulness, because the source tarball is
retained.



### 7.25 Requires Root<a name="Requires-Root"></a>


Set this optional field to "Yes" if the application requires root
privileges to be usable. This lets the client filter it out if the user
so desires. Whether root is required or not, it is good to give a
paragraph in the description to the conditions on which root may be
asked for and the reason for it.

This is converted to (`<requirements>`) in the XML file (_index.xml_).



### 7.26 Archive Policy<a name="Archive-Policy"></a>


This determines the policy for moving old versions of an app to the
archive repo, if one is configured. The configuration sets a default
maximum number of versions kept in the main repo, after which older ones
are moved to the archive. This app-specific policy setting can override
that.

Currently the only supported format is "n versions", where n is the
number of versions to keep. Defaults to "3 versions".



### 7.27 Update Check Mode<a name="Update-Check-Mode"></a>


This determines the method using for determining when new releases are
available - in other words, the updating of the Current Version and
Current Version Code fields in the metadata by the `fdroid checkupdates`
process.

Valid modes are:

-   `None` - No checking is done because there’s no appropriate
    automated way of doing so. Updates should be checked for manually.
    Use this, for example, when deploying unstable or patched versions;
    when builds are done in a directory different to where the
    AndroidManifest.xml is; if the developers use the Gradle build
    system and store version info in a separate file; if the developers
    make a new branch for each release and don’t make tags; or if you’ve
    changed the package name or version code logic.
-   `Static` - No checking is done - either development has ceased or
    new versions are not desired. This method is also used when there is
    no other checking method available and the upstream developer keeps
    us posted on new versions.
-   `RepoManifest` - At the most recent commit, the AndroidManifest.xml
    file is looked for in the directory where it was found in the the
    most recent build. The appropriateness of this method depends on the
    development process used by the application’s developers. You should
    not specify this method unless you’re sure it’s appropriate. For
    example, some developers bump the version when commencing
    development instead of when publishing. It will return an error if
    the AndroidManifest.xml has moved to a different directory or if the
    package name has changed. The current version that it gives may not
    be accurate, since not all versions are fit to be published.
    Therefore, before building, it is often necessary to check if the
    current version has been published somewhere by the upstream
    developers, either by checking for apks that they distribute or for
    tags in the source code repository.

    It currently works for every repository type to different extents,
    except the srclib repo type. For git, git-svn and hg repo types, you
    may use "RepoManifest/yourbranch" as UCM so that "yourbranch" would
    be the branch used in place of the default one. The default values
    are "master" for git, "default" for hg and none for git-svn (it
    stays in the same branch). On the other hand, branch support hasn’t
    been implemented yet in bzr and svn, but RepoManifest may still be
    used without it.

-   `RepoTrunk` - For svn and git-svn repositories, especially those who
    don’t have a bundled AndroidManifest.xml file, the Tags and
    RepoManifest checks will not work, since there is no version
    information to obtain. But, for those apps who automate their build
    process with the commit ref that HEAD points to, RepoTrunk will set
    the Current Version and Current Version Code to that number.
-   `Tags` - The AndroidManifest.xml file in all tagged revisions in the
    source repository is checked, looking for the highest version code.
    The appropriateness of this method depends on the development
    process used by the application’s developers. You should not specify
    this method unless you’re sure it’s appropriate. It shouldn’t be
    used if the developers like to tag unstable versions or are known to
    forget to tag releases. Like RepoManifest, it will not return the
    correct value if the directory containing the AndroidManifest.xml
    has moved. Despite these caveats, it is the often the favourite
    update check mode.

    It currently only works for git, hg, bzr and git-svn repositories.
    In the case of the latter, the repo URL must contain the path to the
    trunk and tags or else no tags will be found.

    Optionally append a regex pattern at the end - separated with a
    space - to only check the tags matching said pattern. Useful when
    apps tag non-release versions such as X.X-alpha, so you can filter
    them out with something like `.*[0-9]$` which requires tag names to
    end with a digit.

-   `HTTP` - HTTP requests are used to determine the current version
    code and version name. This is controlled by the `Update Check Data`
    field, which is of the form `urlcode|excode|urlver|exver`.

    Firstly, if `urlcode` is non-empty, the document from that URL is
    retrieved, and matched against the regular expression `excode`, with
    the first group becoming the version code.

    Secondly, if `urlver` is non-empty, the document from that URL is
    retrieved, and matched against the regular expression `exver`, with
    the first group becoming the version name. The `urlver` field can be
    set to simply ’.’ which says to use the same document returned for
    the version code again, rather than retrieving a different one.



### 7.28 Vercode Operation<a name="Vercode-Operation"></a>


Operation to be applied to the vercode obtained by the defined
`Update Check Mode`. `%c` will be replaced by the actual vercode, and
the whole string will be passed to python’s `eval` function.

Especially useful with apps that we want to compile for different ABIs,
but whose vercodes don’t always have trailing zeros. For example, with
`Vercode Operation` set at something like `%c*10 + 4`, we will be able
to track updates and build up to four different versions of every
upstream version.



### 7.29 Update Check Ignore<a name="Update-Check-Ignore"></a>


When checking for updates (via `Update Check Mode`) this can be used to
specify a regex which, if matched against the version name, causes that
version to be ignored. For example, ’beta’ could be specified to ignore
version names that include that text.



### 7.30 Update Check Name<a name="Update-Check-Name"></a>


When checking for updates (via `Update Check Mode`) this can be used to
specify the package name to search for. Useful when apps have a static
package name but change it programmatically in some app flavors, by e.g.
appending ".open" or ".free" at the end of the package name.

You can also use `Ignore` to ignore package name searching. This should
only be used in some specific cases, for example if the app’s
build.gradle file does not contain the package name.



### 7.31 Update Check Data<a name="Update-Check-Data"></a>


Used in conjunction with `Update Check Mode` for certain modes.



### 7.32 Auto Update Mode<a name="Auto-Update-Mode"></a>


This determines the method using for auto-generating new builds when new
releases are available - in other words, adding a new Build Version line
to the metadata. This happens in conjunction with the ’Update Check
Mode’ functionality - i.e. when an update is detected by that, it is
also processed by this.

Valid modes are:

-   `None` - No auto-updating is done
-   `Version` - Identifies the target commit (i.e. tag) for the new
    build based on the given version specification, which is simply text
    in which %v and %c are replaced with the required version name and
    version code respectively.

    For example, if an app always has a tag "2.7.2" corresponding to
    version 2.7.2, you would simply specify "Version %v". If an app
    always has a tag "ver\_1234" for a version with version code 1234,
    you would specify "Version ver\_%c".

    Additionally, a suffix can be added to the version name at this
    stage, to differentiate F-Droid’s build from the original.
    Continuing the first example above, you would specify that as
    "Version +-fdroid %v" - "-fdroid" is the suffix.



### 7.33 Current Version<a name="Current-Version"></a>


The [name of the version](https://developer.android.com/guide/topics/manifest/manifest-element.html#vname) that is the recommended release. There may be newer versions of
the application than this (e.g. unstable versions), and there will
almost certainly be older ones. This should be the one that is
recommended for general use. In the event that there is no source code
for the current version, or that non-free libraries are being used, this
would ideally be the latest version that is still free, though it may
still be expedient to retain the automatic update check — see No Source
Since.

This field is normally automatically updated - see Update Check Mode.

This is converted to (`<marketversion>`) in the XML file (_index.xml_).



### 7.34 Current Version Code<a name="Current-Version-Code"></a>


The [version code](https://developer.android.com/guide/topics/manifest/manifest-element.html#vcode) corresponding to the [Current Version](#Current-Version) field. Both these
fields must be correct and matching although it’s the current version
code that’s used by Android to determine version order and by F-Droid
client to determine which version should be recommended.

This field is normally automatically updated - see
[Update Check Mode](#Update-Check-Mode).

If not set or set to `0`, clients will recommend the highest version
they can, as if the `Current Version Code` was infinite.

This is converted to (`<marketvercode>`) in the XML file (_index.xml_).



### 7.35 No Source Since<a name="No-Source-Since"></a>


In case we are missing the source code for the Current Version reported
by Upstream, or that non-free elements have been introduced, this
defines the first version that began to miss source code. Apps that are
missing source code for just one or a few versions, but provide source
code for newer ones are not to be considered here - this field is
intended to illustrate which apps do not currently distribute source
code, and since when have they been doing so.



