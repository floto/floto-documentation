Domain Specific Language
========================

Floto uses a domain specific language (DSL) to describe and configure systems.
This language is embedded in JavaScript, allowing system descriptions to take full advantage of all language features.

Basic structure
---------------

A system description consist of three main components:

 * **Hosts** - virtual or physical machines
 * **Images** - abstract container classes
 * **Containers** - concrete container instances
 
Each of these components is declared via a function taking its name and a definition.

.. function:: host(name, definition)

   Declare a host

   :param name: the host's name
   :param definiton: the host's definition
  
   
.. function:: image(name, definition)

   Declare an abstract container image

   :param name: the image name
   :param definiton: the image definition
   
   The image definition contains one field named `build`, which is a function running a series of build steps (see below).
   
.. function:: container(name, definition)

   Declare a concrete container

   :param name: the container name
   :param definiton: the container definition
   
   The container definition contains the following fields:
   
   * **host** - the host to run this container on
   * **image** - the image to base this container on
   * **prepare** (optional) - a preparation function, used to distributed configuration information before the actual containers are built
   * **configure** - a configuration function, which may contain further build steps to configure the container

Build steps
-----------

In an image's build function, and a container's configure function, the following function may be invoked to perform certain steps during the container build process.
These steps translate directly to Dockerfile build steps.

.. function:: from(rootImage)

   Use a root image as image base. *(Only for images)*
   
   This function translates directly into a Docker FROM instruction.
   This function must be invoked first in every build definition.

   :param rootImage: the root image name in a docker registry

.. function:: run(command)

   Run command during the build step.
   This function translates directly into a Docker RUN instruction.

   :param command: the command to execute
   
.. function:: env(key, value)

   Set an environment variable
   This function translates directly into a Docker ENV instruction.

   :param key: the environment key to set
   :param value: the environment value to set
   
.. function:: workdir(workingDirectory)

   Set an environment variable
   This function translates directly into a Docker WORKDIR instruction.

   :param workingDirectory: the working directory to use
   
.. function:: volume(path, name, options)

   Create a data volume
   This function creates a volume on the host system using the name, which is mounted at path in the container.
   The volume is persisted and survives container redeploys

   :param path: the target path inside the container
   :param name: the name to use for this volume, must be unique for each container
   :param options: additional options
   
.. function:: mount(hostPath, containerPath)

   Mount a directory inside the container
   This function allows sharing data between containers on the same host

   :param hostPath: the path on the host system
   :param containerPath: the target path inside the container
   
.. function:: addTemplate(templatePath, destinationPath, templateConfig)

   Use a file as template and copy it to the image

   :param templatePath: path to the Freemarker template file in the system running floto
   :param destinationPath: the destination path in the image
   :param templateConfig: an object used to fill in template parameters
   
.. function:: cmd(command)

   Set the command to run when starting a container.
   
   This only translates indirectly to the Docker RUN instruction.
   In particular, the command is wrapped to allow restarts and propagate SIGTERM and SIGKILL signals,
   as well as document exit codes
   
   :param command: the command to run when the container is started
   
   
   
   
   

   

