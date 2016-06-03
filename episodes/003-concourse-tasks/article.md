Our goal is for you to become proficient and comfortable with Concourse. In the future you will have many pipelines orchestrating development, operations and even business functions for your team/company. The basic unit of custom work in Concourse is the "Task".

This episode follows on from the previous Concourse episode, [001 - What is Concourse CI? How to get started?](https://www.starkandwayne.com/videos/001-what-is-concourse-and-getting-started/).

In this episode we explore the basics of running tasks:

* How to run a single task outside of a pipeline, using `fly execute` command
* The structure of a Task file
* How to provide dynamic inputs to a Task
* How to select target platforms to run a Task from Linux, OS X or Windows
* How to choose the base file system image for a Task
* How to run a complex script in a Task

<iframe src="https://player.vimeo.com/video/169023009? quality=720p" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

We follow the first three steps of the Stark & Wayne [Concourse Tutorial](https://github.com/starkandwayne/concourse-tutorial).

To prepare for the above episode, we clone the tutorial repo and boot up Concourse using Vagrant/Virtualbox:

```
git clone https://github.com/starkandwayne/concourse-tutorial.git
cd concourse-tutorial
vagrant up
```

It is assumed that you have `fly` CLI installed from episode 1.

In all the tutorials we login and alias our Vagrant concourse `tutorial`. We can also run `fly sync` to ensure we have the right version of the `fly` CLI for the target Concourse.

```
fly --target tutorial login  --concourse-url http://192.168.100.4:8080
fly -t tutorial sync
```

### Running hello world task

```
cd 01_task_hello_world
fly -t tutorial execute -c task_hello_world.yml
```

The `fly execute` command is also aliased as `fly e`, which we use in the episode.

```
fly -t tutorial e -c task_hello_world.yml
```

In the episode we make several modifications to this task YAML file to demonstrate the attributes of the task.

### Providing inputs

A task runs a single command. This is only interesting if we can provide it bespoke input. In a pipeline, a task's inputs might come from other tasks or from external resources (s3 objects, git repos, etc).

In our episode, using the `fly execute` command we pass in inputs from our local machine using the `-i` flag:

```
cd ../02_task_inputs
fly -t tutorial e -c inputs_required.yml -i some-important-input=.
```

An input to a task is always a folder.

Inside the task container each input is available as a folder with the name of the input. If the input is called `some-important-input` then the folder inside the container will be `./some-important-input`.

Specifying `-i some-important-input=.` is saying "pass the nested contents of the current directory on this machine (`.`) as the input called `some-important-input`".

A task only accepts an input if it is specified in the task file:

```yaml
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

inputs:
- name: some-important-input

run:
  path: ls
  args: ['-alR']
```

### Run complex scripts

In the task file above the command to run `ls -alR` is simple, and can be coded directly into the task file. It is common to want to run complex scripts. We pass them into the task container as inputs - in the same way we might pass in data/content to process.

```
cd ../03_task_scripts
fly -t tutorial e -c task_show_uname.yml
```

The `03_task_scripts/task_show_uname.yml` task differs from `01_task_hello_world/task_ubuntu_uname.yml` in that we pass in a `03_task_scripts/task_show_uname.sh` script and run that instead. The example script is not complex but could be replaced with complex behavior - in bash, another scripting language, or any other executable.

In the `fly e` command above, the current folder (`03_task_scripts`) matches the name of the input below and so does not need to be specified in the `fly e` command.

```yaml
---
platform: linux

image_resource:
  type: docker-image
  source: {repository: busybox}

inputs:
- name: 03_task_scripts

run:
  path: ./03_task_scripts/task_show_uname.sh
```

The `task_show_uname.sh` script must already be executable.

As we discuss in the episode the `task_show_uname.sh` script is available at `./03_task_scripts/task_show_uname.sh` because the input name was `03_task_scripts`.

### Bonus after the episode

Try renaming the input to `scripts` and then adjust the `run.path` to match (`./scripts/task_show_uname.sh`). You will now need to specify the input explicitly in the `fly e` command:

```
fly -t tutorial e -c task_show_uname.yml -i scripts=.
```

### Learn more about Tasks

For more information about the available attributes of Tasks you can see the [Tasks documentation](http://concourse.ci/running-tasks.html). We will also introduce them in future Concourse episodes.
