# cover2cover

A script for converting JaCoCo XML coverage reports into Cobertura XML coverage
reports.

## Motivation

I created this script because I wanted code coverage reports in Jenkins[1].
Since Cobertura[2] doesn't support Java 1.7 or higher (the project seems
abandoned), we had to use JaCoCo[3], which is great coverage tool and very easy
to use.

However, the Jenkins JaCoCo plugin[4] leaves a lot to be desired, while Cobertura's
Jenkins plugin[5] is a lot better. To be precise, it supports:

  * Trend graphs for packages, classes, etc. instead of just lines
  * Trend graphs in percentages instead of absolute numbers
  * High and low "water marks" that cause the build to become unstable in Jenkins

Until the JaCoCo plugin is up to speed, this script can be used to convert
JaCoCo XML reports into Cobertura XML reports, so we can continue to use the
Cobertura Jenkins plugin to track coverage.

Not every feature is supported, but close enough.

## Usage

Add the following "post step" to your Jenkins build:

    mkdir -p target/site/cobertura && cover2cover.py target/site/jacoco/jacoco.xml src/main/java > target/site/cobertura/coverage.xml

And add the Cobertura plugin with the following path:

    **/target/site/cobertura/coverage.xml

> (Note: The above assumes a Maven project)

## References

[1]: http://jenkins-ci.org/ "Jenkins"
[2]: http://cobertura.sourceforge.net/ "Cobertura"
[3]: http://www.eclemma.org/jacoco/ "JaCoCo"
[4]: https://wiki.jenkins-ci.org/display/JENKINS/JaCoCo+Plugin "Jenkins JaCoCo plugin"
[5]: https://wiki.jenkins-ci.org/display/JENKINS/Cobertura+Plugin "Jenkins Cobertura plugin"
