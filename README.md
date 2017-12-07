## Configuration ##

1. Install the munin-node on the Docker server. For more information check the following URL: [munin guide](http://guide.munin-monitoring.org/en/latest/installation/install.html).
2. Copy the *docker_* file to the munin plugin folder: `/usr/share/munin/plugins`.
3. Set plugin permissions: `chmod +x docker_`
4. Create symbolic links.

  ```
  cd /etc/munin/plugins/

  ln -s /usr/share/munin/plugins/docker_ docker_cpu
  ln -s /usr/share/munin/plugins/docker_ docker_memory
  ln -s /usr/share/munin/plugins/docker_ docker_memory_nocache
  ln -s /usr/share/munin/plugins/docker_ docker_blockio
  ln -s /usr/share/munin/plugins/docker_ docker_netio

  ln -s /usr/share/munin/plugins/docker_ docker_compose_cpu
  ln -s /usr/share/munin/plugins/docker_ docker_compose_memory
  ln -s /usr/share/munin/plugins/docker_ docker_compose_memory_nocache
  ln -s /usr/share/munin/plugins/docker_ docker_compose_blockio
  ln -s /usr/share/munin/plugins/docker_ docker_compose_netio

  ln -s /usr/share/munin/plugins/docker_ docker_volumes
  ```
5. Give root privilege to the docker plugin. Root privilege is required for munin to execute the Docker command.
  1. Create a new file named "docker" inside the folder /etc/munin/plugin-conf.d/
  2. Insert the following content in the new docker file:
  ```
  [docker_*]
  user root
  ```
6. Restart the munin-node service.
