Get your own Concourse CI running on your laptop with Vagrant.

This episode is the pre-cursor to a series of episodes for learning to use Concourse via Stark & Wayne's [Concourse Tutorial](https://github.com/starkandwayne/concourse-tutorial). The repository includes a `Vagrantfile` to get started and dozens of tutorials. These tutorials will be the basis for future videos as well.

```
git clone https://github.com/starkandwayne/concourse-tutorial.git
cd concourse-tutorial
vagrant box add concourse/lite --box-version $(cat VERSION)
vagrant up
```

Visit http://192.168.100.4:8080/ in your browser.

Click on your operating system logo to download the `fly` CLI.

For OS X and Linux you need to make it executable:

```
mv ~/Downloads/fly ~/bin/fly
chmod +x ~/bin/fly
```

Test that the `fly` CLI is working and target your local Concourse CI:

```
fly -v
fly -t tutorial login -c http://192.168.100.4:8080/
fly -t tutorial pipelines
```

Deploy the sample pipeline from http://concourse.ci/

Create `tmp/hello.yml`:

```yaml
jobs:
- name: hello-world
  plan:
  - task: say-hello
    config:
      platform: linux
      image_resource:
        type: docker-image
        source: {repository: ubuntu}
      run:
        path: echo
        args: ["Hello, world!"]
```

To register the new pipeline:

```
fly -t tutorial set-pipeline -p hello-world -c hello.yml
fly -t tutorial pipelines
```

View the pipeline and run the job via http://192.168.100.4:8080/pipelines/hello-world

To tear down your Concourse CI:

```
vagrant destroy
```
