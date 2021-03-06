# Host Scanner DEB/RPM Distributions

The `deb` and `rpm` folders contain the `Dockerfile` and scripts to pull, compile and package the latest revision. The `.deb` package is generated with the current Debian Stable (`debian:latest` in Docker Hub) while the `.rpm` package is generated with the current Fedora version. (`fedora:latest`)

Since Boost is statically linked during compilation, the dynamic dependencies for now are `libcurl`, `libsqlite3` and `zlib` for both distributions.

The files will be generated by CMake's packaging component, CPack, whose configuration can be found in `CPackConfig.cmake`.

In order to set up these build environments, you must first compile the container:

    cd distrib/deb
    docker build -t debbuild .

After this, the `debbuild` container will be available for any compilations needs. To bake a fresh `.deb`, just run:

    docker run -it debbuild

This will pull a fresh copy of the repository _inside_ the container, therefore any changes to the repository on your host machine will not be reflected. If you wish to compile you own fork or a different branch, you'll have to modify the `compile.sh` file next to the preferred `Dockerfile` and rebuild the container.