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
  1. Create a new file named "docker" inside the folder `/etc/munin/plugin-conf.d/`
  2. Insert the following content in the new docker file:
  ```
  [docker_*]
  user root
  ```
6. Restart the munin-node service.

### Extra options: ###

#### Truncate ####
You can also enable name truncation for blockio and netio graphs by adding a line into the `/etc/munin/plugin-conf.d/docker` file.

```
[docker_*]
user root
env.truncate yes
```

This will lead into more readable graphs as the values will not be line wrapped under if the names of the containers are longer this comes with a cost of less readibility for the names of the containers.

#### Total ####
You can also enable showing sum of all values in graph by adding a line into the `/etc/munin/plugin-conf.d/docker` file.

```
[docker_*]
user root
env.total yes
```
