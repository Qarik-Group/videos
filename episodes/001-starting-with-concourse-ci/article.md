Learn a little about [Concourse CI](https://concourse.ci/) and get your own Concourse CI running on your laptop with Vagrant.

<iframe src="https://player.vimeo.com/video/167371982? quality=720p" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

```
vagrant init concourse/lite
vagrant up
```

Visit http://192.168.100.4:8080/ in your browser.

Click on your operating system logo to download the `fly` CLI.

For OS X and Linux you need to make it executable:

```
mv ~/Downloads/fly ~/bin/fly
chmod +x ~/bin/fly
fly -v
```

Alias your local Concourse CI with the name `tutorial`:

```
fly -t tutorial login -c http://192.168.100.4:8080/
```

There is a "Hello, world" pipeline example at the bottom of http://concourse.ci/.

Create `hello.yml`:

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

And register the new pipeline:

```
fly -t tutorial set-pipeline -p hello-world -c hello.yml
```

View the pipeline and run the job via http://192.168.100.4:8080/pipelines/hello-world

Click the "hello-world" job to view it, and click its Plus (+) button on the top right to manually trigger the job to start. In future tutorials we will learn about triggering jobs when external resources change.

When the job is completed it changes to green. Click the home icon to return to the pipeline dashboard and see that the job appears green too.

To tear down your Concourse CI:

```
vagrant destroy
```
