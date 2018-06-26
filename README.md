# gitlab-runner
Install and register a GitLab CI runner

## Description
This role sets up a GitLab CI runner, registering it to some GitLab server.

## Configuration
| Name | Default value | Description |
| ---- | ------------- | ----------- |
| `gitlab_runner_apt_old_repos` | (see `defaults/main.yml`) | Old (pre 10.x) GitLab runner repository URLs |
| `gitlab_runner_apt_repos` | (see `defaults/main.yml`) | Current GitLab repository URLs |
| `gitlab_runner` | `[]` | GitLab runner configuration, see below |

An example configuration might look like this:
```
gitlab_runner:
  concurrent_builds: 2
  runners:
    - name: "{{ ansible_hostname }}"
      state: present
      ci_server: https://gitlab.example.org
      token: Very$ecret
      executor: docker
      docker_image: debian:{{ ansible_distribution_release }}
```
which would set up the CI runner with the `docker` strategy, registering it to `https://gitlab.example.org` and allowing a maximum of two concurrent builds.
