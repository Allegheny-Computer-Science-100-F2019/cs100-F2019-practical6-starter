# cs100-F2019-practical6-solution

## Table of Contents

* [Table of Contents](#table-of-contents)
* [Introduction](#introduction)
* [Continuous Learning](#continuous-learning)
* [System Commands](#system-commands)
  + [Using Docker](#using-docker)
  + [Using Gradle](#using-gradle)
* [Expected Program Output](#expected-program-output)
* [Automated Checks with GatorGrader](#automated-checks-with-gatorgrader)
* [Downloading Project Updates](#downloading-project-updates)
* [Using Travis CI](#using-travis-ci)
* [System Requirements](#system-requirements)
* [Reporting Problems](#reporting-problems)
* [Receiving Assistance](#receiving-assistance)
* [Project Assessment](#project-assessment)

## Introduction

This assignment requires a programmer to implement and manually test a Java
program, called `RollAndSumDice`, that will produce textual output that rolls
dice and sums their output. This program will construct instances of objects,
call a method provided by those objects, perform a computation, and then output
the result of the computation. Please see the comments in the source code and
the laboratory assignment sheet for more details. As verified by
[Checkstyle](https://github.com/checkstyle/checkstyle), the source code for the
`MadLibs.java` file must adhere to all of the requirements in the [Google Java
Style Guide](https://google.github.io/styleguide/javaguide.html). The source
code in the `RollAndSumDice.java` file must also pass additional tests set by
the [GatorGrader tool](https://github.com/GatorEducator/gatorgrader).

The source code in the `RollAndSumDice.java` file must also pass additional
tests set by the [GatorGrader
tool](https://github.com/GatorEducator/gatorgrader). As before, GatorGrader will
check to ensure `RollAndSumDice` uses the `new Date()` construct in the Java
code. GatorGrader will also check that your program produces the correct number
of output lines with the correct methods.

A carefully formatted assignment sheet for this project provides more details
about the steps that a computer scientist should take to complete this
assignment. You can view this assignment sheet by visiting the listing of
laboratories on the course web site created by the course instructor. Please pay
attention to the icons in the left-hand margin of the assignment sheet as they
will help you to understand and remember what steps you should take at key parts
of the assignment.

## Continuous Learning

If you have not done so already, please read all of the relevant [GitHub
Guides](https://guides.github.com/) that explain how to use many of the features
that GitHub provides. In particular, please make sure that you have read the
following GitHub guides: [Mastering
Markdown](https://guides.github.com/features/mastering-markdown/), [Hello
World](https://guides.github.com/activities/hello-world/), and [Documenting Your
Projects on GitHub](https://guides.github.com/features/wikis/). Each of these
guides will help you to understand how to use both [GitHub](http://github.com) and
[GitHub Classroom](https://classroom.github.com/).

Students who want to learn more about how to use
[Docker](https://www.docker.com) should review the [Docker
Documentation](https://docs.docker.com/). Students are also encouraged to review
the documentation for their text editor, which is available for text editors
like [Atom](https://atom.io/docs) and [VS
Code](https://code.visualstudio.com/docs). You should also review the [Git
documentation](https://git-scm.com/doc) to learn more about how to use the Git
command-line client. In addition to talking with the instructor and technical
leader for your course, students are encouraged to search
[StackOverflow](https://stackoverflow.com/) for answers to their technical
questions.

To do well on this assignment, you should also review Chapters 1 through 3.
Finally, please read Sections 4.1 and 4.2 to learn more about Java classes and
objects. Please see the course instructor or one of the teaching assistants or
tutors if you have questions about any of these reading assignments.

## System Commands

This project invites students to enter system commands into a terminal window.
This assignment uses [Docker](https://www.docker.com) to deliver programs, such
as `gradle` and the source code and packages needed to run
[GatorGrader](https://github.com/GatorEducator/gatorgrader), to a students'
computer, thereby eliminating the need for a programmer to install them on their
development workstation. Individuals who do not want to install Docker can
optionally install of the programs mentioned in the [Project
Requirements](#requirements) section of this document.

### Using Docker

Once you have installed [Docker
Desktop](https://www.docker.com/products/docker-desktop), you can use the
following `docker run` command to start `gradle grade` as a containerized
application, using the [DockaGator](https://github.com/GatorEducator/dockagator)
Docker image available on
[DockerHub](https://cloud.docker.com/u/gatoreducator/repository/docker/gatoreducator/dockagator).

```bash
docker run --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator
```

The aforementioned command will use `"$(pwd)"` (i.e., the current directory) as
the project directory and `"$HOME/.dockagator"` as the cached GatorGrader
directory. Please note that both of these directories must exist, although only
the project directory must contain something. Generally, the project directory
should contain the source code and technical writing of this assignment, as
provided to a student through GitHub. Additionally, the cache directory should
not contain anything other than directories and programs created by DockaGator,
thus ensuring that they are not otherwise overwritten during the completion of
the assignment. To ensure that the previous command will work correctly, you
should create the cache directory by running the command `mkdir
$HOME/.dockagator`. If the above `docker run` command does not work correctly on
the Windows operating system, you may need to instead run the following command
to work around limitations in the terminal window:

```bash
docker run --rm --name dockagator \
  -v "$(pwd):/project" \
  -v "$HOME/.dockagator:/root/.local/share" \
  gatoreducator/dockagator
```

If that Docker command does not work correctly, then you should first consider
writing the command on a single line in your terminal window and then replacing
`$(pwd)` and `$HOME` with the fully qualified name of the directory that those
variables represent. Students who are stuck on this step should explain to the
course instructor what they have already tried and what challenges they
currently face.

Here are some additional commands that you may need to run when using Docker:

* `docker info`: display information about how Docker runs on your workstation
* `docker images`: show the Docker images installed on your workstation
* `docker container list`: list the active images running on your workstation
* `docker system prune`: remove many types of "dangling" components from your workstation
* `docker image prune`: remove all "dangling" docker images from your workstation
* `docker container prune`: remove all stopped docker containers from your workstation
* `docker rmi $(docker images -q) --force`: remove all docker images from your workstation

### Using Gradle

Since the above `docker run` command uses a Docker images that, by default, runs
`gradle grade` and then exits the Docker container, you may want to instead run
the following command so that you enter an "interactive terminal" that will
allow you to repeatedly run commands within the Docker container.

```bash
docker run -it --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator /bin/bash
```

Once you have typed this command, you can use the [GatorGrader
tool](https://github.com/GatorEducator/gatorgrader) in the Docker container by
typing the command `gradle grade` in your terminal. Running this command will
produce a lot of output that you should carefully inspect. If GatorGrader's
output shows that there are no mistakes in the assignment, then your source code
and writing are passing all of the automated baseline checks. However, if the
output indicates that there are mistakes, then you will need to understand what
they are and then try to fix them.

You can also complete several important Java programming tasks by using the
`gradle` tool. For instance, you can compile (i.e., create bytecode from the
program's source code if it is correct) the program using the command `gradle
build`. Here are some other commands that you can type:

* `gradle grade`: run the [GatorGrader](https://github.com/GatorEducator/gatorgrader) tool to check your work
* `gradle clean`: clean the project of all the derived files
* `gradle check`: check the quality of the code using Checkstyle
* `gradle build`: create the bytecode from the Java source code
* `gradle run`: run the Java program in the command-line
* `gradle tasks`: display details about the Gradle system

To run one of these commands, you must be in the main (i.e., "home base")
directory for this assignment where the `build.gradle` file is located.

## Expected Program Output

Typing the command `gradle run` in the terminal window should produce the
following output for the completed version of `RollAndSumDice`. As long as your
program adheres to all of the requirements for the assignment and passes all of
the verification checks, your version should produce similar output. With that
said, program output may vary according to, for instance, the name of the
programmer and the date on which you ran the program and the output of the
random number generator. Here is a sample of the output:

```
> Configure project :
Configured GatorGradle 0.4.4

> Task :run
Die One's Face Value: 3
Die Two's Face Value: 5
Die Three's Face Value: 3
The Sum of the Three Die is: 11

BUILD SUCCESSFUL in 887ms
2 actionable tasks: 1 executed, 1 up-to-date
```

Running the command `gradle -q --console plain run` will suppress the display of
Gradle's diagnostic information and produce output like the following sample.

```
Die One's Face Value: 3
Die Two's Face Value: 5
Die Three's Face Value: 3
The Sum of the Three Die is: 11
```

## Automated Checks with GatorGrader

In addition to meeting all of the requirements outlined in the assignment sheet,
your submission must pass the following checks that
[GatorGrader](https://github.com/GatorEducator/gatorgrader) automatically
assesses:

- The Die.java in src/main/java/practicalsix has at least 2 multiple-line Java comment(s)
- The Die.java in src/main/java/practicalsix has at least 4 single-line Java comment(s)
- The Die.java in src/main/java/practicalsix has exactly 0 of the `Add Your Name Here` fragment
- The Die.java in src/main/java/practicalsix has exactly 0 of the `TODO` fragment
- The Die.java in src/main/java/practicalsix has exactly 1 of the `package practicalsix;` fragment
- The RollAndSumDice.java in src/main/java/practicalsix has at least 2 multiple-line Java comment(s)
- The RollAndSumDice.java in src/main/java/practicalsix has at least 4 single-line Java comment(s)
- The RollAndSumDice.java in src/main/java/practicalsix has exactly 0 of the `Add Your Name Here` fragment
- The RollAndSumDice.java in src/main/java/practicalsix has exactly 0 of the `TODO` fragment
- The RollAndSumDice.java in src/main/java/practicalsix has exactly 1 of the `package practicalsix;` fragment
- The command `gradle -q --console plain run` executes correctly
- The command `gradle build` executes correctly
- The command output has at least 1 of the `Face Value` fragment
- The command output has at least 1 of the `The Sum` fragment
- The command output has exactly 4 lines
- The file Die.java exists in the src/main/java/practicalsix directory
- The file RollAndSumDice.java exists in the src/main/java/practicalsix directory
- The repository has at least 5 commit(s)

If [GatorGrader's](https://github.com/GatorEducator/gatorgrader) automated
checks pass correctly, the tool will produce the output like the following in
addition to returning a zero exit code (which you can access by typing the
command `echo $?`).

```
        ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
        ┃ Passed 18/18 (100%) of checks for cs100-F2019-practical6! ┃
        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

## Downloading Project Updates

If the course instructor pushes updates to this assignment and you received it
through GitHub Classroom and you would like to also receive these updates, then
you can type this command in the main directory for this assignment:

```
git remote add download git@github.com:Allegheny-Computer-Science-100-F2019/cs100-F2019-practical6-starter.git
```

You should only need to type this command once; running the command additional
times may yield an error message but will not negatively influence the state of
your Git repository. Now, you are ready to download the updates provided by the
GatorGrader maintainers by typing this command:

```
git pull download master
```

This second command can be run whenever the maintainers needs to provide you
with new source code for this assignment. However, please note that, if you have
edited the files that we updated, running the previous command may lead to Git
merge conflicts. If this happens, you may need to manually resolve them with the
help of the instructor or a student technical leader. Finally, please note that
the [Gradle plugin](https://github.com/GatorEducator/gatorgradle) for
[GatorGrader](https://github.com/GatorEducator/gatorgrader) will automatically
download the newest version of GatorGrader.

## Using Travis CI

This assignment uses [Travis CI](https://travis-ci.com/) to automatically run
[GatorGrader](https://github.com/GatorEducator/gatorgrader) and additional
checking programs every time you commit to your GitHub repository. The checking
will start as soon as you have accepted the assignment &mdash; thus creating your own
private repository &mdash; and the course instructor and/or GitHub enables Travis for
it. If you are using Travis for the first time, you will need to authorize
Travis CI to access the private repositories that you created on GitHub. If you
do not see either a yellow &#9679; or a green &#x2714; or a red &#x2717; in your
listing of commits, then please ask the instructor to see whether or not
Travis CI was correctly enabled.

## System Requirements

We developed this assignment to work with the following software and versions:

- Docker Desktop
- Operating Systems
  - Linux
  - MacOS
  - Windows 10 Pro
  - Windows 10 Enterprise
- Programming Language Tools
  - Gradle 5.4
  - MDL 0.5.0
  - OpenJDK 11.0.4
  - Proselint 0.10.2
  - Python 3.6 or 3.7

## Reporting Problems

If you have found a problem with this assignment's provided source code or
documentation, then you can go to the [Computer Science 100 Fall 2019 Practical
5](https://github.com/Allegheny-Computer-Science-100-F2019/cs100-F2019-practical6-starter)
repository and [raise an
issue](https://github.com/Allegheny-Computer-Science-100-F2019/cs100-F2019-practical6-starter/issues).
If you have found a problem with the [GatorGrader
tool](https://github.com/GatorEducator/gatorgrader) and the way that it checks
your assignment, then you can also [raise an
issue](https://github.com/GatorEducator/gatorgrader/issues) in that repository.
To ensure that your issue is properly resolved, please provide as many details
as is possible about the problem that you experienced. If you discover a problem
with the assignment sheet for this project, then please raise an issue in the
GitHub repository that provides the assignment sheets for your course.

Whenever possible, individuals who find, and use the appropriate GitHub issue
tracker to correctly document, a mistake in any aspect of this assignment will
receive free [GitHub stickers](https://octodex.github.com/) and extra credit
towards their grade for the project.

## Receiving Assistance

If you are having trouble completing any part of this project, then please talk
with either the course instructor or a student technical leader during the
course session. Alternatively, you may ask questions in the Slack workspace for
this course. Finally, you can schedule a meeting during the course instructor's
office hours.

## Project Assessment

Taking inspiration from the principles of [specification-based
grading](http://rtalbert.org/return-to-specs-grading-calculus/), the grade that
a student receives on this assignment will have the following characterization:

- **Travis CI Build Status**: Since additional checks on the source code or
  documentation may be encoded in Travis CI's actions and, moreover, all of the
  GatorGrader checks are also run in Travis CI, students will receive a
  checkmark grade if their last before-the-deadline build passes and a green
  &#x2714; appears in their GitHub commit log instead of a red &#x2717;.
  Students are encouraged to repeatedly revise their source code and technical
  writing in an attempt to get their Travis CI build to pass.

All grades for this project will be reported through a student's GitHub
repository using either messages in the GitHub commit log or issues raised in
the issue tracker. Students should ask questions about their grade for this
project in GitHub so as to facilitate an effective conversation about the
submitted deliverables.
