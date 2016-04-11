DITA Open Toolkit Project Docker Configurations
===============================================

Configuration files for Docker containers for the base DITA Open Toolkit
as released by the DITA Open Toolkit project (http://dita-ot.org).

This project provides Docker configuration files (Dockerfile) for Docker containers
that provide DITA Open Toolkit images that reflect the out-of-the-box DITA Open
Toolkit.

See http://www.dita-community.org/dita-ot-project-docker/ for the full documentation
on how to use and extend the DITA OT containers.

The dita-ot-base container provides an extendable container that can be used to
create additional containers with additional plugins or other resources added.

The dita-ot container is a working container that provides the volumes needed
by other containers to work with the Open Toolkit or use the container with
files on the host machine. It cannot be used for extension (because the volume
containing the Open Toolkit itself gets reset on subsequent layers once it's
set in the Dockerfile).

The base container defines two volumes intended to be mount points
for host directories:

- VOLUME /opt/dita-ot/data - Mount directory containing the source data to process. Because of permissions complexities under 
Windows and OS X this is effectively a read-only directory.
- VOLUME /opt/dita-ot/out - Mount directory to hold output. This directory must be writable by the OT process, 
so under Windows and OS X this may need to be a directory in the Docker machine running the container,
e.g., /srv/dita-ot/out. You can access this directory in various ways, including using secure copy (scp) or
rsync from the docker machine. 

In addition, working DITA OT containers should define the volume /opt/dita-ot/DITA-OT, which makes
the DITA OT itself available to other containers via the --volumes-from Docker runtime parameter.

To generate the HTML5 version of the project Web site, do the following:

1. If you haven't ready, make a new clone of the project and check out branch "gh-pages". 
This clone will be the target of the output
2. Run the following Docker command (OS X version, for Windows add "/c" before "/Users" in the -v parameter):
  ```
  docker run \
    -v /Users/ekimber/workspace-dita-community:/opt/dita/data dita4publishers/dita-ot \
    ant -Dargs.input /opt/dita/data/dita-ot-project-docker/docs/dita-ot-docker-guide.ditamap \
        -Doutput.dir /opt/dita/data/dita-ot-project-docker_gh-pages \
        -Dtranstype d4p-html5
  ```

  Where "/Users/ekimber/workspace-dita-community" is the directory you have both clones of the project. 
  This directory must be under the /Users directory.
3. Check the generated HTML in the gh-pages clone. If it's good, commit and push.


