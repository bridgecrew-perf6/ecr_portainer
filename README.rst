====
Portainer (With ECR support)
====

(Taken from https://github.com/portainer/portainer/issues/1533#issuecomment-689927288)

----
Usage
----

.. code-block:: bash

  $ ./build.sh
  $ docker swarm init --advertise-addr=<your-public-or-private-ip>
  $ docker stack deploy -c ecr-portainer-agent-stack.yml portainer


----
Caveats
----

* For some reason, the enviroment: tag is set on the stack file, however, it is not set during deploy. It has to be manually set for now.
* In case you want to test out, enter portainer console under Containers > portainer container:

.. code-block:: bash

  / # ./docker pull <ECR Repo/image>

* You will not be able to pull images from the Portainer UI, however, you can use ECR repository images in Stacks inside Portainer, like so:

.. code-block:: yml

  version: "3.3"
  services:
    my-awesome-service:
      image: <registy-id>.dkr.ecr.<aws-region>.amazonaws.com/<repository-name>:<image-tag>
